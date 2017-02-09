# Deploying an Application Programmatically from a Maven Repository

## Deploying an Artefact Using Maven Coordinates
To deploy an application programmatically directly from a Maven repository, you will need to add a Maven GAV coordinate. This can be done using `addDeployFromGAV()` method. This method accepts a comma separated string denoting a maven artefact's _groupId_, _artifactId_, and _version_ attributes.

```Java
import fish.payara.micro.PayaraMicro;
import fish.payara.micro.BootstrapException;

public class EmbeddedPayara 
{
    public static void main(String[] args) throws BootstrapException 
    {
       PayaraMicro.getInstance().addDeployFromGAV("fish.payara.testing,clusterjsp,1.1").bootStrap();
    }
}
```

## Specifying Additional Maven Repositories
By default, Payara Micro will only search for artefacts in the Maven Central repository. If you wish to search additional repositories, you can add them to the list of repositories to search with the `addRepoUrl()` method:

```Java
import fish.payara.micro.PayaraMicro;
import fish.payara.micro.BootstrapException;

public class EmbeddedPayara 
{
    public static void main(String[] args) throws BootstrapException 
    {
       PayaraMicro.getInstance().addRepoUrl("https://raw.github.com/Pandrex247/Payara_PatchedProjects/Payara-Maven-Deployer");
       PayaraMicro.getInstance().addDeployFromGAV("fish.payara.testing,clusterjsp,1.1").bootStrap();
    }
}
```

To search through multiple additional repositories, you can simply call the `addRepoUrl` method, using commas to separate URLs:

```Java
import fish.payara.micro.PayaraMicro;
import fish.payara.micro.BootstrapException;

public class EmbeddedPayara 
{
    public static void main(String[] args) throws BootstrapException 
    {
       PayaraMicro micro = PayaraMicro.getInstance();
       micro.addRepoUrl("https://raw.github.com/Pandrex247/Payara_PatchedProjects/Payara-Maven-Deployer", "https://maven.java.net/content/repositories/promoted/");
       micro.addDeployFromGAV("fish.payara.testing,clusterjsp,1.1");
       micro.bootStrap();
    }
}
```

## Deploying Multiple Applications from a Maven Repository
Similar to when deploying multiples applications from the command line, you must call the `addDeployFromGAV` method for each application you wish to deploy directly from a Maven repository.

For example, to deploy two applications:

```Java
import fish.payara.micro.PayaraMicro;
import fish.payara.micro.BootstrapException;

public class EmbeddedPayara 
{
    public static void main(String[] args) throws BootstrapException 
    {
       PayaraMicro micro = PayaraMicro.getInstance();
       micro.addDeployFromGAV("fish.payara.testing,clusterjsp,1.1");
       micro.addDeployFromGAV("fish.payara.testing,clusterjsp,1.2");
       micro.bootStrap();
    }
}
```

