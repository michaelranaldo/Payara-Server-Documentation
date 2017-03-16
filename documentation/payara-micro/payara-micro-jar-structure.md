# Payara Micro JAR Structure

From Payara 4.1.1.171, Payara Micro has changed its JAR structure.

## Payara Micro Structure

The Payara Micro jar now looks like this:

```Shell
payara-micro.jar
├── fish
│   └── payara/micro/
├── META-INF
│   ├── MANIFEST.MF
│   └── maven/fish.payara.micro/payara-micro-boot/pom.xml
└── MICRO-INF
    ├── classes
    ├── deploy
    ├── domain
    ├── lib
    ├── payara-boot.properties
    ├── post-boot-commands.txt
    ├── pre-boot-commands.txt
    └── runtime
```

| File | Description|
|---|---|
|fish/payara|Payara Micro's class files|
|META-INF|Contains the Manifest, Pom, and Pom properties|
|MICRO-INF/classes|Contains classes which are added to the classpath before those in /runtime|
|MICRO-INF/deploy|Contains WAR, EAR, and EJB-JAR files for deployment.|
|MICRO-INF/domain|Contains domain.xml, default-web.xml, keystores, login.conf, logging.properties, and other files that are written to the temp file directory.|
|MICRO-INF/lib|Contains additional third party dependency jars which will be added to the classpath automatically|
|MICRO-INF/runtime|Contains the core runtime jars|
|MICRO-INF/payara-boot.properties|The System properties file containing Payara Micro runtime flags. This overrides the runtime and can be overidden by command-line arguments|
|MICRO-INF/post-boot-commands.txt|A txt file containing asadmin commands to execute post boot|
|MICRO-INF/pre-boot-commands.txt|A txt file containing asadmin commands to execute before boot|

## Nested JAR

Payara Micro now has two options for unpacking classes:

#### Unpacking to File System (`--unpack`)

By default, Payara Micro will unpack the nested JARs into a temporary directory within the directory specified by either the system property `java.io.tmpdir` or the command line argument `--unpackdir`, and then load them as classes.
This way of booting Payara Micro results in a comparable boot time to previous Payara Micro releases, but with the added advantages of avoiding class collisions and safer extensibility.
This requires no explicit command-line arguments.

#### Unpacking to Memory (`--nested`)

The other flag now available is `--nested`.
This will load the classes directly from the nested JARs to the memory without unpacking the JARs into a folder, but may slow boot.

To start Payara Micro as a nested JAR, use the `--nested` option as shown:

```Shell
java -jar payara-micro.jar --nested
```
