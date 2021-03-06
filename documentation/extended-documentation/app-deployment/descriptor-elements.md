# Elements of the Deployment Descriptor Files
This page is a reference for extra elements added to either the `glassfish-application.xml` or the `glassfish-web.xml` files in Payara Server.

### `classloading-delegate`
With this option, the libraries included in the EAR assembly will override libraries included in Payara Server distribution. 
For more information about how Payara Server loads the required classes and libraries, see the [Classloading](../classloading.md) section.

### `enable-implicit-cdi`

In a WAR file, it is possible to set the property `bean-discovery-mode` equal to `none` to turn off implicit scanning of the archive for bean defining annotations, as defined by CDI 1.1. This has been made available as part of the CDI 1.1 specification; the default value of this setting is defined as `annotated` in the specification, so the archive is scanned for any bean-defining annotations.

In the `glassfish-application.xml` deployment descriptor for an EAR file, the property `enable-implicit-cdi` can be set to `false` to achieve the same goal for all modules inside the EAR assembly. The default value is `true`, in line with the default value for WAR files.

If implicit CDI scanning causes problems for an EAR assembly, the value `false` will disable implicit CDI scanning for all CDI modules inside the EAR assembly:

```xml
<glassfish-application>
  <enable-implicit-cdi>false</enable-implicit-cdi>
</glassfish-application>
```

**Note**:  
When implicit CDI is controlled by using either the `enable-implicit-cdi` property in the `glassfish-application.xml` or the attribute `bean-discovery-mode="none"` from the `beans.xml` file in a WAR, the admin console checkbox ***is ignored***.

The default behaviour of the admin console is for the "Implicit CDI" checkbox to be enabled, but this will **not** override the application configuration.

### `scanning-exclude` and `scanning-include`
Modern WAR and EAR files very often include a number of 3rd party JARs. In situations where some JARs require CDI scanning and others may break if scanned, these can now be explicitly included or excluded from scanning.

Both the `glassfish-application.xml` and the `glassfish-web.xml` files support the following directives:

```xml
<scanning-exclude>*</scanning-exclude>
<scanning-include>ejba*</scanning-include>
<scanning-include>conflicting-web-library</scanning-include>
```

In the above example, all JARs will be excluded by default, then all JARs beginning with `ejba` will be scanned, along with the JAR named `conflicting-web-library`.

## `container-initializer-enabled`

This property configures whether to enable or disable the calling of `ServletContainerInitializer` component classes defined in JAR files bundled inside the WAR assembly.

For performance considerations, you can explicitly disable the servlet container initializer by setting the `container-initializer-enabled` element to `false`. This can help deployment in web applications that cause conflicts with a custom bootstrapping process or depend on external libraries.

The default value for this configuration element is `true`.

## `default-role-mapping`

With this property, you can set whether to enable the default group to role mappings for your application's security settings. This element is set up as a `property` element with a `Boolean` value attribute like this:

```xml
<property name="default-role-mapping" value="true">
  <description>Enable default group to role mapping</description>
</property>
```

Enabling the default group to role mappings will cause all named groups in the application's linked security realm to be mapped to a role of the same name. This will save you the time of having to redefine the same roles and map them to the realm groups each time they are modified.

This will have the same effect as executing the following asadmin command:

```sh
asadmin set configs.config.server-config.security-service.activate-default-principal-to-role-mapping=true
```

Except it's effect will only limit itself to the application instead of all applications deployed on the server. This setting is configured by default to `true` on the [production-ready-domain](../production-ready-domain.md)

The default value of this property is `false`. This property can be set in the `glassfish-web.xml`, `glassfish-ejb-jar.xml` and `glassfish-application.xml` deployment descriptors.

In an EAR assembly, only the property set in the `glassfish-application.xml` will take effect and any set in the `glassfish-web.xml` and `glassfish-ejb-jar.xml` will be ignored. Setting this configuration property in any of these files will always take precedence over any setting configured on the server.
