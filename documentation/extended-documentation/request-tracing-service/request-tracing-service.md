# Request Tracing Service

The Request Tracing Service provides tracing facilities for Servlet request events. The service logs each request in detail; capturing EJB method calls and web service invocations. The service can be configured to inform the user of a threshold breach during request execution.

The service helps users to detect application slowness by logging requests that exceed a given threshold. The trace data from long-running requests gives insight to help recover from bottlenecks that may arise within an application.

The service is available in both Payara Server and Payara Micro, though configuration is different for Payara Micro.

The following types of requests are traced if the service is enabled:

 - REST (JAX-RS endpoints)
 - Servlet (handling HTTP requests)
 - SOAP Web Service Requests
 - WebSocket
 - execution of EJB timers
 - inbound JMS message hnadled by a message-driven bean
 - JBatch job is created
 - a new task is executed in a managed executor

Once a request is being traced, the Request Tracing service collects events during processing, so that it may later provide a report of what was happening and how long it took if the configured threshold is exceeded. The following events are observed and reported:

 - start/end of the request
 - an EJB method entered/exited
 - a CDI bean method entered/exited (only configured methods are observed)
 - SQL statement invocations via JDBC
 - a JTA transaction is started/finished
 - JASPIC authentication

--------------------------

* [Asadmin Commands](asadmin-commands.md)
* [Configuration](configuration.md)
