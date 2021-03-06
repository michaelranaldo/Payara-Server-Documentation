# Core Documentation

JACC stands for Java Authentication Contract for Containers. It's defined in [JSR 115](https://jcp.org/en/jsr/detail?id=115) and all Java EE complaint servers are mandated to provide a default JACC Policy.

## How to install a custom JACC provider

Having coded a JACC provider, the first thing to register it is to make the classes available for the server. For that purpose, you need to put the implementation JAR, with all its dependencies, under `[payara_home]/lib`. So for example, if Payara Server is installed under `/opt/payara`, your JAR should reside under `/opt/payara/lib`. That way it will be part of Payara's global classpath on boot.

The next thing to do is to tell Payara you want to use that specific JACC provider. For that purpose, you have to execute the following commands in the `asadmin` CLI:
create-jacc-provider --policyConfigurationFactoryProvider=com.example.CustomPolicyConfigurationFactory --policyProvider=com.example.CustomPolicy --target=server-config custom-provider
set configs.config.server-config.security-service.jacc=custom-provider

```Shell
create-jacc-provider --policyConfigurationFactoryProvider=com.example.CustomPolicyConfigurationFactory --policyProvider=com.example.CustomPolicy --target=server-config custom-provider
set configs.config.server-config.security-service.jacc=custom-provider
```

These will result in the following domain.xml snippet to be added:

```xml
<security-service jacc="custom-provider">
    <jacc-provider policy-provider="com.example.CustomPolicy" name="custom-provider" policy-configuration-factory-provider="com.example.CustomPolicyConfigurationFactory"></jacc-provider>
    <!-- More providers can be defined -->
</security-service>
```

As you can derive from the XML excerpt, more JACC providers can be defined (by default, `simple` and `default` are already defined), but only one will be used at runtime, specified by the `jacc` attribute on the `security-service` element.
