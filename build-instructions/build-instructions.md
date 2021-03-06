# Contents

* [1. Overview](#1-overwiew)
* [2. Prerequisites](#2-prerequisites)
* [3. Configuring Maven](#3-configuring-maven)
* [4. Getting the Source Code](#4-getting-the-source-code)
* [5. Building Payara Server](#5-building-payara-server)
* [6. Building Payara Micro](#6-building-payara-micro)

## 1. Overwiew

This page provides instructions on how to build the Payara Server's source code.

## 2. Prerequisites

To build and run Payara Server, your environment must be set up with the following:

* Oracle JDK 7 Update 65 or later, or Oracle JDK 8 Update 20 or later.
* Maven 3.0.3 or above
* Git
* A `JAVA_HOME` environment variable pointing to the JDK install location \(e.g. /home/user/jdk11.8.0\_45/\)
* A `PATH` environment variable that has a pointer to the Java binaries \(JAVA\_HOME/bin\)

You can also optionally add the Maven _bin_ folder to the `PATH` environment variable as well, and the documentation will assume that you have done so.

## 3. Configuring Maven

If using JDK 7, you will need to increase the heap size and _PermGen_ size to prevent the build process from running out of memory.

Create a `MAVEN_OPTS` environment variable and set it as:

```Shell
-Xmx1024m -XX:MaxPermSize=512m
```

If using JDK 8, _PermGen_ has been replaced by _Metaspace_, which can increase its maximum size on its own, so you only need to increase the heap size:

```Shell
-Xmx1024m
```

## 4. Getting the Source Code

To download the Payara Server's source code, open a terminal or Git Bash window, navigate to the directory you would like the source code to be downloaded to, and run `git clone https://github.com/payara/Payara.git`.

This will download the Payara Server's source code, and initialise git, in a directory called _Payara_.

## 5. Building Payara Server

With your Git Bash or terminal window, navigate into the downloaded _Payara_ directory, and run:

```Shell
mvn clean install
```

This will build Payara and run the integrated GlassFish unit tests. To save a bit of time, you can skip these tests by appending the _skipTests_ flag to the install command like so:

```Shell
mvn clean install -DskipTests
```

## 6. Building Payara Micro

Since 164, Payara Micro is included as part of the default build. As it depends on modules of Payara Server, it can't be built on its own. To build Payara Micro:

```Shell
mvn clean install -DskipTests
```

After the build has completed, the Payara Micro jar can be found in the target directory at:

```Shell
appserver/extras/payara-micro/payara-micro-distribution/target/
```

## Building Payara Microprofile

Payara Microprofile is built as part of Payara Micro. To build Payara Microprofile, you can run:

```Shell
mvn clean install -DskipTests
```

Payara Microprofile can be found in its target directory at:

```Shell
appserver/extras/payara-micro/payara-micro-microprofile-distributions/target
```

## Additional Build Profiles

There are a number of additional Maven build profiles:
```Shell
mvn clean install
mvn clean install -PBuildExtras
mvn clean install -PQuickBuild
```

| Payara Version |  clean install | -PBuildExtras | -PQuickBuild |
| ---- | ---- | ---- | ---- | 
| Payara Server |✓|✓|✓|
| Payara Server (Web Profile) |✓ |✓ | |
| Payara Server Multi Language |✓ |✓ | |
| Payara Server Multi Language (Web Profile) |✓ |✓ | |
| Payara Server Minimal |✓ |✓ |✓ |
| Payara Micro |✓ |✓ | |
| Payara Microprofile |✓|✓ | |
| Payara Embedded | |✓ | |
| Payara Embedded (Web Profile) | |✓ | |

To save time on builds, you can also add the flag _skipTests_:
```Shell
mvn clean install -DskipTests
```
This will cut out all build tests so will save quite a bit of time.