# New Features

* [1063/PAYARA-182 - Java EE Concurrent Context Interceptor](https://github.com/payara/Payara/pull/1063)
* [1068/PAYARA-179 - Request Tracing for inbound JMS to MDB](https://github.com/payara/Payara/pull/1068)
* [1083/PAYARA-1038 - Add Request Tracing Event for JASPIC authentication](https://github.com/payara/Payara/pull/1083)
* [1097/PAYARA-178 - JDBC Context Interceptor](https://github.com/payara/Payara/pull/1097)
* [1099/PAYARA-756 - Request tracing events for start and stop of JTA transactions](https://github.com/payara/Payara/pull/1099)
* [1101/PAYARA-181 - JBatch Context interceptor](https://github.com/payara/Payara/pull/1101)
* [1107/PAYARA-931 - Integrate Request Tracing into Payara Micro](https://github.com/payara/Payara/pull/1107)
* [1131/PAYARA-999 - Enable jars within an application deployment to be excluded from CDI scanning](https://github.com/payara/Payara/pull/1131)
* [1142/PAYARA-867 - Option to disable the servlet container initializer](https://github.com/payara/Payara/pull/1142)
* [1152/PAYARA-618 - Enable the DAS to discover Payara Micro instances](https://github.com/payara/Payara/pull/1152)

# Enhancements

* [980/PAYARA-846 - Add new improvements to payaradomain](https://github.com/payara/Payara/pull/980)
* [996/PAYARA-936 - Provide default group to role mapping](https://github.com/payara/Payara/pull/996)
* [1032/PAYARA-955 - Rolling upgrades for versioned apps](https://github.com/payara/Payara/pull/1032)
* [1034/PAYARA-824 - Disabling CDI in the deployment descriptor now overrides admin console setting](https://github.com/payara/Payara/pull/1034)
* [1053/PAYARA-733 - Add capability to output logs in JSON format](https://github.com/payara/Payara/pull/1053)
* [1076/PAYARA-1024 - Refactor Notification Service asadmin Commands for Simplicity](https://github.com/payara/Payara/pull/1076)
* [1076/PAYARA-1025 - Refactor Request Tracing asadmin Commands for simplicity](https://github.com/payara/Payara/pull/1076)
* [1082/PAYARA-1041 - Make notification service enabled by default for the log notifier](https://github.com/payara/Payara/pull/1082)
* [1102/PAYARA-1018 - Increase pool size of Managed Executor Service and Scheduled Executor Service](https://github.com/payara/Payara/pull/1102)
* [1111/PAYARA-1049 - Add a --deployDir option to do the same job as --deploymentDir in Payara Micro](https://github.com/payara/Payara/pull/1111)
* [1125/PAYARA-1107 - JCache beans created by JSR107Producer use generics](https://github.com/payara/Payara/pull/1125)
* [1126/PAYARA-1106 - Use name from CacheDefaults when injecting JCache](https://github.com/payara/Payara/pull/1126)
* [1130/PAYARA-923 - Provide option to compress log files on rotation](https://github.com/payara/Payara/pull/1130)
* [1150/PAYARA-1140 - Allow to use colon \(:\) to separate coordinates in maven deployer](https://github.com/payara/Payara/pull/1150)
* [1156/PAYARA-1071 - Admin console integration for JSON Log Formatter](https://github.com/payara/Payara/pull/1156)

# Component Upgrades

* Jersey 2.22.2
* Hazelcast 3.7.1
* Eclipselink 2.6.3
* mail 1.5.6
* btrace 1.2.3
* Jackson 2.8.1
* Grizzly 2.3.28
* Weld 2.4.0.Final

# Fixed Issues

* [668/PAYARA-947 - CDI EJB Field producers' validation fail with incompatible types](https://github.com/payara/Payara/pull/668)
* [959/PAYARA-1010 - BufferUnderflowException in case of using java 8 with lambdas](https://github.com/payara/Payara/pull/959)
* [986/PAYARA-1075 - Deployment of application fails when a resource adapter is not deployed to all instances](https://github.com/payara/Payara/pull/986)
* [1000/PAYARA-690/PAYARA-813 - Cannot find the resource bundle error message when deploying / underlying EAR applications](https://github.com/payara/Payara/pull/1000)
* [1041/PAYARA-1012 - Payara Embedded stopped working in .163 due to request tracing](https://github.com/payara/Payara/pull/1041)
* [1044/PAYARA-1129 - Perform preInvoke and postInvoke steps symmetrically in EJB BaseContainer](https://github.com/payara/Payara/pull/1044)
* [1046/PAYARA-1034 - NPE when accessing Notification Service in the admin console on a 162 domain with 163 binaries](https://github.com/payara/Payara/pull/1046)
* [1049/PAYARA-994/PAYARA-1023 - Healthcheck service can't add a new checker dynamically / NullPointerException when dynamically registering healthcheck services for the first time](https://github.com/payara/Payara/pull/1049)
* [1064/PAYARA-935 - Fix "Illegal non-string type" for request tracing, notification, healthcheck, and asadmin recorder services](https://github.com/payara/Payara/pull/1064)
* [1067/PAYARA-1035 - Request Tracing is not dynamic in domain migrated from 162 to 163](https://github.com/payara/Payara/pull/1067)
* [1075/PAYARA-993 - Update Grizzly to 2.3.26 to fix PAYARA-797](https://github.com/payara/Payara/pull/1075)
* [1076/PAYARA-1040 - Payara Micro does not force redeploy when domain.xml or rootDir is used](https://github.com/payara/Payara/pull/1076)
* [1079/PAYARA-956 - ManagedExecutorService MBean attempts to register multiple times](https://github.com/payara/Payara/pull/1079)
* [1081/PAYARA-917 - Jaspic - forward from SAM injected request tests fail](https://github.com/payara/Payara/pull/1081)
* [1084/PAYARA-988 - Asadmin command to configure hogging threads checker is missing](https://github.com/payara/Payara/pull/1084)
* [1110/PAYARA-1076 - PAYARA-1076 make LazyBootPersistence manager more null safe on misconfiguration](https://github.com/payara/Payara/pull/1110)
* [1116/PAYARA-1083 - disable and deploy commands should wait for all applications to deploy](https://github.com/payara/Payara/pull/1116)
* [1128/PAYARA-1104 - Wrong redirect of WebService endpoint to https](https://github.com/payara/Payara/pull/1128)
* [1129/PAYARA-1081 - ClassNotFoundException for JaxbAnnotationIntrospector upon first request to REST endpoint](https://github.com/payara/Payara/pull/1129)
* [1132/PAYARA-954 - Update Service descriptions to replace "GlassFish" with "Payara"](https://github.com/payara/Payara/pull/1132)
* [1136/PAYARA-1036 - @ViewScoped, @FlowScoped, @ConversationScoped not working on Payara Micro](https://github.com/payara/Payara/pull/1136)
* [1139/PAYARA-1126 - Cache Interceptors should cast to Throwable not Exception when Caching](https://github.com/payara/Payara/pull/1139)
* [1140/PAYARA-934 - aliased password cannot be replaced by the value of the alias](https://github.com/payara/Payara/pull/1140)
* [1144/PAYARA-1113 - Request Tracing does not process thresholds of less than one millisecond](https://github.com/payara/Payara/pull/1144)
* [1145/PAYARA-1130 - Comparing elapsed time to threshold should be done in nanoseconds](https://github.com/payara/Payara/pull/1145)
* [1149/PAYARA-1134 - When Payara Micro deploys a war called ROOT.war its context root is /ROOT when it should be /](https://github.com/payara/Payara/pull/1149)
* [1159/PAYARA-1127 - Unable to set ClientInfo for connection with H2 1.4.192](https://github.com/payara/Payara/pull/1159)

## Security Fixes

* [1024/PAYARA-989 - Security Issue in Payara](https://github.com/payara/Payara/pull/1024)
* [1051/PAYARA-1011 - Fix CVE-2016-5388](https://github.com/payara/Payara/pull/1051)

## Upstream Fixes

* [1052/PAYARA-1010/GLASSFISH-21510 - BufferUnderflowException in case of using java 8 with lambdas](https://github.com/payara/Payara/pull/1052)
* [1089/PAYARA-1067 - Undefined behaviour when interceptor method is overloaded in interceptor class](https://github.com/payara/Payara/pull/1089)
* [1090/PAYARA-892/GLASSFISH-20606 - create-domain assigns wrong values for JMS port](https://github.com/payara/Payara/pull/1090)
* [1123/PAYARA-1056 - Sums of thread pool statistics counters not correct](https://github.com/payara/Payara/pull/1123)
* [1157/PAYARA-1008 - Fix PWC6117: File "null" not found errors](https://github.com/payara/Payara/pull/1157)



