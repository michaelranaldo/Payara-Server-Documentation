# Payara Micro Jar Structure

From Payara 4.1.1.171, Payara Micro has changed its JAR structure.

## Uber-JAR Structure
There are a number of ways to structure an Uber-JAR - a jar file which contains both a project and all its dependencies. Previously, Payara Micro inherited the shaded jar format of Payara Embedded, where dependencies which shared packages were _shaded_ and renamed if they were not unique and all JARs were unpacked, then packed within a single JAR. The JVM classloader handled all of the internal classes and resources, with the Payara classloader only handling WAR files.

This made Payara Micro awkward to work with, and lead to dependency issues.

### Nested JAR

To make Payara Micro easier to work with and increase its future extensibility, Payara Micro now uses a nested JAR format using code from Springboot. This has changed both the classloader and its behaviour. The Payara classloader now handles the majority of internal classes and resources (leaving only a few essential classes to the JVM classloader) and  there are now two options for unpacking classes:

#### Default Packaging

By default, Payara Micro will unpack the nested JARs into folders within the file system and then load them as classes. This is  faster to boot than previous versions of Payara Micro.

#### `--nested`

The other option now available is launching Payara Micro with the `--nested` flag. This will load the classes directly from the nested JARs to the memory. While this slows boot by approximately 13%, the nested flag optimizes the nested JARs for random access.
