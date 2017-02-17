# Payara Micro Jar Structure
From Payara 4.1.1.171, Payara Micro has changed how its Uber-JAR is  packaged.

_In versions of Payara prior to Payara 4.1.1.171, Payara Micro used the same shaded JAR packaging as Payara Embedded. The JVM classloader handled every internal class and resource, with the Payara classloader only loading WAR files. This made Payara Micro difficult to work with as it was awkward to extend and would overwrite common dependencies between modules._

## Uber-JAR Format

Payara Micro was and still is an Uber-JAR - the only thing which has changed is how the files within the Uber-JAR are arranged. Also known as "fat JAR", an Uber-JAR is a way of packaging a Java program and its dependencies. There are a few different ways of packaging the dependencies within the Uber-JAR, each with their own pros and cons.

Before Payara 4.1.1.171 Payara Micro was a shaded JAR, in the same style as Payara Embedded. This meant that

Repackaging all classes into a single JAR file and renaming to avoid dependency clashes

_Payara Micro was and still is an Uber-JAR. This is a jar file which contains both Payara Micro and its dependencies, to make life easier. This is why you only need a computer and Java to run Payara Micro. There are a few ways of packaging Uber-JARs - previously the shaded jar apporach we had been using up to 4.1.1.171 was decided to be too unwieldy to continue using. This prompted the move to the nested JAR format._



Now only the required classes are loaded by the JVM classloader. Everything else is handled by the Payara classloader, which loads both the WAR files and the rest of the classes as nested JARs.This resulted in two new ways to load the classes into Payara Micro:


## Default Packaging

By default, Payara Micro will unpack the nested JARs into folders within the file system and then load them as classes. This is faster than previous versions of Payara Micro.

## Nested JAR

The other option is launching Payara Micro with the `--nested` flag. This will load the classes directly from the nested JARs to the memory. While this slows boot by about 15% during classloading, the nested flag optimizes the nested JARs for random access.
