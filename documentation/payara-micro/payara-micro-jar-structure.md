# Payara Micro Jar Structure

From Payara 4.1.1.171, Payara Micro has changed its JAR structure.

## Uber-JAR Structure
There are a number of ways to structure an Uber-JAR - a jar file which contains both a project and all its dependencies. Previously, Payara Micro inherited the shaded jar format of Payara Embedded, where dependencies which shared packages were _shaded_ and renamed if they were not unique and all JARs were unpacked, then packed within a single JAR. The JVM classloader handled all of the internal classes and resources, with the Payara classloader only handling WAR files.

### Nested JAR

Payara Micro now uses a nested JAR format using code from Spring Boot. The Payara classloader now handles the majority of internal classes and resources (leaving only a few essential classes to the JVM classloader) and  there are now two options for unpacking classes:

#### Default - Unpacking to File System (`--unpack`)

By default, Payara Micro will unpack the nested JARs into a temporary directory within the directory specific by the system property `java.io.tmpdir` and then load them as classes. This is  faster to boot than previous versions of Payara Micro. This requires no explicit command-line arguments.

#### Unpacking to Memory (`--nested`)

The other flag now available is `--nested`. This will load the classes directly from the nested JARs to the memory, but may slow boot.

To start Payara Micro as a nested JAR, use the `--nested` option as shown:

```Shell
java -jar payara-micro.jar --nested
```
