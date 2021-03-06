# Production Ready Domain
Payara Server comes with a default domain, `domain1`, which has been inherited from GlassFish. This domain (and its accompanying template) has not been modified in any way. The default domain is not, however, designed to be run in production but to be a usable example for development and testing purposes.

Since the creation of `domain1` in GlassFish, there have been changes in how the server is used, along with the changes implemented by the Payara development team. To better highlight these changes and new features, the `payaradomain` was created.

###Usage
`payaradomain` is located in the default  directory for domains `${PAYARA_HOME}/glassfish/domains/`, alongside `domain1`. This means it can be used as-is by simply naming the domain after running the `start-domain` subcommand and without specifying the domain directory location:

```
asadmin> start-domain payaradomain 
```
Alternatively, many Payara Server users completely delete existing domains and recreate their own domains with custom settings. `payaradomain` can be used here too, since the domain is also provided as a template in the `${PAYARA_HOME}/glassfish/common/templates/gf` directory. You will need to specify the full path to the location of the template jar as follows:

```
asadmin> create-domain --template ${PAYARA_HOME}/glassfish/common/templates/gf/payara-domain.jar myNewPayaraDomain 
```

###Differences to `domain1`
The configuration of `payaradomain` has been made with production in mind, so there are a number of differences when compared to `domain1` which are listed below. Not all of these will be wanted for development environments, but all are good practice for production domains.

#####Differences in Server Configuration
1. Autodeployment has been disabled  
Payara Server comes with a deployment scanner. This is a security risk for production, so is disabled by default. in the domain.xml  

2. Dynamic application reloading disabled  
For the same reason as above, this is disabled by default in the domain.xml  

3. Dynamic reloading of JSP pages in `default-web.xml` disabled  
The `<init-param>` setting `reload-interval` in the default-web.xml has been set to a value of `-1` so that it is disabled.  

4. The EJB container `max-pool-size` has been set to `128`  

5. The `max-thread-pool-size` setting for `thread-pool-1` has been increased to `250`  

6. File caching has been enabled for both default HTTP listeners  

7. Isolated classloading has been enabled by default at the server level  
The property `fish.payara.classloading.delegate` has been set to `false`  

8. A default transaction timeout of 300 seconds has been added for xa and non-xa transactions  

9. Default group-to-role mapping is enabled  

10. The maximum size for the thread pool `http-thread-pool` has been increased from `5` to `50`.

#####Differences in JVM Options
With the aim of `payaradomain` being to target production, we have excluded `PermGen` configuration, since it is only relevant in Java 7. Payara Server does support Java 7, but JDK 7 reached end-of-life and therefore it is a security risk to run a JVM lower than version 8 in production.

The following JVM options are present in `domain1`, but different in `payaradomain`:
* `-XX:+UseG1GC`
* `-XX:+UseStringDeduplication`
* `-Xmx2g`
* `-Xms2g`
* `-server`
* `-Djdk.tls.rejectClientInitiatedRenegotiation=true`

The following JVM options are present in `domain1` but are not present in `payaradomain`:

* `-XX:MaxPermSize=192m`
* `-Dosgi.shell.telnet.port=6666`
* `-Dosgi.shell.telnet.maxconn=1`
* `-Dosgi.shell.telnet.ip=127.0.0.1`
* `-Dgosh.args=--nointeractive`
* `-Dfelix.fileinstall.poll=5000`
* `-Dfelix.fileinstall.log.level=2`
* `-Dfelix.fileinstall.bundles.new.start=true`
* `-Dfelix.fileinstall.bundles.startTransient=true`
* `-Dfelix.fileinstall.disableConfigSave=false`
* `-Dcom.ctc.wstx.returnNullForDefaultNamespace=true`
* `-Dorg.glassfish.additionalOSGiBundlesToStart=org.apache.felix.shell, org.apache.felix.gogo.runtime, org.apache.felix.gogo.shell, org.apache.felix.gogo.command, org.apache.felix.shell.remote, org.apache.felix.fileinstall`
