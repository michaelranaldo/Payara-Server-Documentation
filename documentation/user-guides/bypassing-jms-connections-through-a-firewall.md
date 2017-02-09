# Bypassing JMS Connections through a Firewall

A common scenario when using the JMS service with Payara Server is to have the Message broker and a remote client separated by a firewall. To solve this impediment, there are 2 options to establish a successful connection between them:

1. Configure a secure connection using the `httpjms` or `httpsjms` connection services of the broker so the connection is correctly tunneled using a proxy servlet.

2. Bypass the Message Queue Port Mapper and explicitly assign a static port address to the desired connection service, and configure the firewall to allow connections to this static port.

The second approach is usually **recommended** in most cases: Tunneling through a secure connection going through the firewall can significantly increase message processing time, so it's better to bypass the connection instead.

## Configuring a static port for the Message Queue Port Mapper

To assign the static port number to a connection service, determine which connection service and protocol you are using to establish connections with the broker and set the appropriate configuration property according to the following table:

| Connection Service | Protocol | Configuration Property |
| :--- | :--- | :--- |
| _jms_ | TCP | `imq.jms.tcp.port` |
| _ssljms_ | TLS | `imq.ssljms.tls.port` |
| _admin_ | TCP | `imq.admin.tcp.port` |
| _ssladmin_ | TLS | `imq.ssladmin.tls.port` |

To correctly assign this configuration property, you need to determine the type of configuration mode Payara Server is using for the JMS connection service: EMBEDDED, LOCAL or REMOTE.

### How to set the property in EMBEDDED mode

On **EMBEDDED** mode, the OpenMQ broker is executed as part of the same JVM process the application server is running \(Only works with Payara Server Full Edition\). Considering this, the configuration property must be set as part of the JVM settings of the domain. To configure the JMS service using the respective `asadmin` command you can do this:

```
./asadmin create-jvm-options --target=server-config -Dimq.jms.tcp.port=10234
```

Where _10234_ is the static port set up in the firewall.

### How to set the property in LOCAL mode

On **LOCAL **mode, the OpenMQ broker is executed in a separate JVM process from the application server's. To set the configuration property correctly, is recommended to set it as part of the start arguments the server uses to start the broker at domain startup. To configure the JMS service using the respective `asadmin` command you can do this:

```
./asadmin set configs.config.server-config.jms-service.start-args=-Dimq.jms.tcp.port=10234

```

Where _10234_ is the static port set up in the firewall.

### How to set the property in REMOTE mode

On **REMOTE** mode, the OpenMQ broker is completely independent from the Payara Server installation. Since it's the responsability of a third party to configure and manage the lifecyle of the broker, the property must be configured directly on it instead of the server/domain. 

The recommended way to do this is to pass the property as a start argument (_JVM_ argument, along with other arguments for memory, GC, etc.) when manually starting the broker. To configure the JMS service using the `imqbrokerd` utility you can do this:

```
./imqbrokerd -varhome ${MQ_HOME}/data/imq -name mq_server -port 7676 -vmargs "-Dimq.jms.tcp.port=10234 -Xms256 -Xmx256m -XX:+UseG1GC"
```

Where _10234_ is the static port set up in the firewall.