# Advance Connection Pool Properties in Deployment Descriptors
_Payara Server and Micro 161 (4.1.1.162) onwards_

From Payara 161 (4.1.1.162), Payara Server now supports the advanced connection pool properties usually only available for connection pools created via the administration console for Datasource connection pools deployed with an application via the application deployment descriptor or datasource annotations. This means your application scoped datasources now can fully utilise Payara Server's powerful connection pool support.

## Payara Micro Support
All the advanced properties are now also supported on Payara Micro datasources deployed with your microservices application. Bringing advanced debugging and diagnostics support.

## Setting properties in the deployment descriptor
In Java EE 7 a Datasource definition can be added to a deployment descriptor of an application for example in the web.xml. To set advanced properties just add a property tag shown in the example below.

```xml
    <data-source>
     <name>java:global/ExampleDataSource</name>
     <class-name>com.mysql.jdbc.jdbc2.optional.MysqlXADataSource</class-name>
     <server-name>localhost</server-name>
     <port-number>3306</port-number>
     <database-name>mysql</database-name>
     <user>test</user>
     <password>test</password>
     <!-- Example of how to use a Payara specific custom connection pool setting -->
     <property>
         <name>fish.payara.is-connection-validation-required</name>
         <value>true</value>
     </property>
   </data-source>
```

## Setting properties via annotations.
In Java EE 7 a Datasource definition can be added to an application via annotations . To set advanced properties just add a property tag shown in the example below.
```java
@DataSourceDefinition(
    name = "java:app/MyApp/MyDS",
    className = "org.h2.jdbcx.JdbcDataSource",
    url = "jdbc:h2:mem:test",
    properties = {"fish.payara.is-connection-validation-required=true"})
    ```
    
## Full List of Properties
Each of the properties below has a corresponding field in the administration console.

|Property|Value Type|Default|Notes|
|--------|----------|-----|---|
|fish.payara.is-connection-validation-required|Boolean|false|true - Validate connections, allow server to reconnect in case of failure|
|fish.payara.connection-validation-method|String||The method of connection validation table, autocommit, meta-data, custom-validation|
|fish.payara.validation-table-name|String||The name of the table used for validation if the validation method is set to table|
|fish.payara.validation-classname|String||The name of the custom class used for validation if the validation-method is set to custom-validation|
|fish.payara.fail-all-connections|Boolean|false|Close all connections and reconnect on failure, otherwise reconnect only when used |
|fish.payara.allow-non-component-callers|Boolean|false|Enable the pool to be used by non-component callers such as Servlet Filters|
|fish.payara.validate-atmost-once-period-in-seconds|Number|0|Specifies the time interval in seconds between successive requests to validate a connection at most once. Default value is 0, which means the attribute is not enabled.|
|fish.payara.connection-leak-timeout-in-seconds|Number|0|0 implies no connection leak detection|
|fish.payara.connection-leak-reclaim|Boolean|false|If enabled, leaked connection will be reclaimed by the pool after connection leak timeout occurs|
|fish.payara.connection-creation-retry-attempts|Number|0|Number of attempts to create a new connection. 0 implies no retries|
|fish.payara.connection-creation-retry-interval-in-seconds|Number|10|Time interval between retries while attempting to create a connection. Effective when Creation Retry Attempts is greater than 0.|
|fish.payara.statement-timeout-in-seconds|Number|-1|Timeout property of a connection to enable termination of abnormally long running queries. -1 implies that it is not enabled.|
|fish.payara.lazy-connection-enlistment|Boolean|false|Enlist a resource to the transaction only when it is actually used in a method |
|fish.payara.lazy-connection-association|Boolean|false|Connections are lazily associated when an operation is performed on them|
|fish.payara.associate-with-thread|Boolean|false|When the same thread is in need of a connection, it can reuse the connection already associated with that thread|
|fish.payara.pooling|Boolean|true|When set to false, disables connection pooling for the pool|
|fish.payara.statement-cache-size|Number|0|Caching is enabled when set to a positive non-zero value (for example, 10)|
|fish.payara.match-connections|Boolean|true|Turns connection matching for the pool on or off|
|fish.payara.max-connection-usage-count|Number|0|Connections will be reused by the pool for the specified number of times, after which they will be closed. 0 implies the feature is not enabled. |
|fish.payara.wrap-jdbc-objects|Boolean|true|When set to true, application will get wrapped jdbc objects for Statement, PreparedStatement, CallableStatement, ResultSet, DatabaseMetaData|
|fish.payara.sql-trace-listeners|String||Comma-separated list of classes that implement the org.glassfish.api.jdbc.SQLTraceListener interface|
|fish.payara.ping|Boolean|false|When enabled, the pool is pinged during creation or reconfiguration to identify and warn of any erroneous values for its attributes|
|fish.payara.init-sql|String||Specify a SQL string to be executed whenever a connection is created from the pool |
|fish.payara.statement-leak-timeout-in-seconds|Number|0|0 implies no statement leak detection|
|fish.payara.statement-leak-reclaim|Boolean|false|If enabled, leaked statement will be reclaimed by the pool after statement leak timeout occurs|
|fish.payara.statement-cache-type|String|||
|fish.payara.slow-query-threshold-in-seconds|Number|-1|SQL queries that exceed this time in seconds will be logged. Any value <= 0 disables Slow Query Logging|
|fish.payara.log-jdbc-calls|Boolean|false|When set to true, all JDBC calls will be logged allowing tracing of all JDBC interactions including SQL|

## Example Datasource configuration
An example datasource configured via the web.xml and deployed with a custom SQL trace listener is shown below. this datasource is configured to also validate all connections returned from the connection pool before giving them to the application using the in-build MySQL Connection Validation class. The datasource is also configured to log any queries that exceed 5 seconds and also to log all jdbc calls.
```xml
<?xml version="1.0" encoding="UTF-8"?>

<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
	 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	 xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_3_1.xsd"
	 version="3.1">
    <session-config>
        <session-timeout>
            30
        </session-timeout>
    </session-config>
    <data-source>
     <name>java:global/ExampleDataSource</name>
     <class-name>com.mysql.jdbc.jdbc2.optional.MysqlXADataSource</class-name>
     <server-name>localhost</server-name>
     <port-number>3306</port-number>
     <database-name>mysql</database-name>
     <user>test</user>
     <password>test</password>
     <!-- Example of how to use a Payara specific custom connection pool setting -->
     <property>
         <name>fish.payara.slow-query-threshold-in-seconds</name>
         <value>5</value>
     </property>
     <property>
         <name>fish.payara.log-jdbc-calls</name>
         <value>true</value>
     </property>
     <property>
         <name>fish.payara.sql-trace-listeners</name>
         <value>fish.payara.examples.payaramicro.datasource.example.CustomSQLTracer</value>
     </property>
     <property>
         <name>fish.payara.is-connection-validation-required</name>
         <value>true</value>
     </property>
     <property>
         <name>fish.payara.connection-validation-method</name>
         <value>custom-validation</value>
     </property>
     <property>
         <name>fish.payara.validation-classname</name>
         <value>org.glassfish.api.jdbc.validation.MySQLConnectionValidation</value>
     </property>
    </data-source>
</web-app>
```
