# JMS Notifier
The Java Message Service (JMS) API is a messaging API which can be used to enable asynchronous communication between clients. The Payara JMS notifier makes use of a JMS queue to send notification events from services such as Request Tracing and Health Check. These can then be consumed by a custom MDB or other JMS compatible client.

## Requirements

To use JMS as a notification target, you will need the following:

1. **A JMS broker**<br />_Payara Server ships with embedded OpenMQ_
2. **Payara Server Full edition**<br />_The Web edition does not come with native JMS capabilities_

If you are using Payara Server _Full_ edition, the easiest way to configure the JMS notifier is to use the embedded OpenMQ broker, as described here.

## Configuration

Configuration requires a few steps. At a high level, this means:
* Create a target JMS queue to received notifications (if none exists)
* Configure the JMS notifier to use the queue configured


1. Create a new JMS queue to receive the notification messages from the notifier:
  ![](/assets/edit-jms-destination.png)

  To make this change via the asadmin tool, use the following command which mirrors the above screenshot:

  ```Shell
  asadmin create-jms-resource --enabled=true --property=Name=notifierQueue --restype=javax.jms.queue jms/notifierQueue
  ```

2. Set the properties for the JMS Notifier:
![](/assets/jms-notifier-configuration.png)
The above example uses the embedded OpenMQ broker provided in Payara Server Full. No further configuration is needed to use it other than creating the queue.

  To make this change via the asadmin tool, use the following command which mirrors the above screenshot:

  ```Shell
  asadmin notification-jms-configure --dynamic=true --enabled=true --contextFactoryClass=com.sun.enterprise.naming.SerialInitContextFactory --target=server-config --queueName=notifierQueue --url=localhost:7676 --connectionFactoryName=jms/_defaultConnectionFactory
  ```

&nbsp;
##### Verify the Configuration
For verification purposes, it may be useful to enable a service to push notifications through the JMS notifier to demonstrate that it is working. To do this, we will also need a Message-Driven Bean (MDB) to consume the notifications and demonstrate that they are being received on the queue.


1. First, enable a service to push data through the notifier. For example, the HealthCheck service's CPU metric can be configured to push CPU metrics to a notifier every 5 seconds:
```
asadmin> healthcheck-configure --enabled=true --dynamic=true
asadmin> healthcheck-configure-service --serviceName=healthcheck-cpu --enabled=true --dynamic=true --time=5 --unit=SECONDS
```
Providing the JMS notifier is already configured, these messages will begin to be sent to the configured queue right away.

2. To Consume Messages using a JMS 2.0 compliant MDB, the following class will work for a local queue named `notifierQueue`:
```Java
@MessageDriven(activationConfig = {
    @ActivationConfigProperty(propertyName = "destinationLookup", propertyValue = "jms/notifierQueue"),
    @ActivationConfigProperty(propertyName = "destinationType", propertyValue = "javax.jms.Queue"),
    @ActivationConfigProperty(propertyName = "destination", propertyValue = "notifierQueue"),
})
public class NotificationConsumer implements MessageListener {

    @Override
    public void onMessage(Message message) {
        try {
            System.out.println("Message received: " + message.getBody(String.class));
        } catch (JMSException ex) { // ignore }
    }
}
```

3. View the result of the MessageDrivenBean's `onMessage()` command. In this example, the CPU metric of the healthcheck service was configured to notify every 5 seconds, so the result of simply printing to `System.out` is log messages similar to the following:

```Shell
[2017-02-24T14:25:02.019+0000] [Payara 4.1] [INFO] [] [fish.payara.nucleus.healthcheck.HealthCheckService] [tid: _ThreadID=151 _ThreadName=admin-thread-pool::admin-listener(9)] [timeMillis: 1487946302019] [levelValue: 800] [[
  Scheduling Health Check for task: CPUC]]

[2017-02-24T14:25:02.019+0000] [Payara 4.1] [INFO] [] [fish.payara.nucleus.healthcheck.HealthCheckService] [tid: _ThreadID=151 _ThreadName=admin-thread-pool::admin-listener(9)] [timeMillis: 1487946302019] [levelValue: 800] [[
  Payara Health Check Service Started.]]

[2017-02-24T14:25:02.376+0000] [Payara 4.1] [INFO] [] [] [tid: _ThreadID=48 _ThreadName=p: thread-pool-1; w: 3] [timeMillis: 1487946302376] [levelValue: 800] [[
  Message received: Health Check notification with severity level: INFO. (host:mike-payara, server:server, domain:domain1,instance:server)
CPUC:Health Check Result:[[status=GOOD, message='CPU%: 1.45, Time CPU used: 3 seconds 797 milliseconds'']']]]

[2017-02-24T14:25:02.380+0000] [Payara 4.1] [INFO] [] [] [tid: _ThreadID=50 _ThreadName=p: thread-pool-1; w: 5] [timeMillis: 1487946302380] [levelValue: 800] [[
  Message received: Health Check notification with severity level: SEVERE. (host:mike-payara, server:server, domain:domain1,instance:server)
CPUC:Health Check Result:[[status=CRITICAL, message='CPU%: 109.71, Time CPU used: 7 milliseconds'']']]]
```

## Asadmin Commands

#### Set the JMS notifier configuration

To set the JMS notifier configuration, the following asadmin command will reflect the configuration in the screenshot above:

```
asadmin> notification-jms-configure --dynamic=true --enabled=true \
--contextFactoryClass=com.sun.enterprise.naming.SerialInitContextFactory \
--connectionFactoryName=jms//__defaultConnectionFactory \
--queueName=notifierQueue \
--url=localhost:7676 \
--username= \
--password= \
--target=server-config \
```
#### Get the JMS notifier configuration
To get the current JMS notifier configuration using asadmin, run the command:

```
asadmin> get-jms-notifier-configuration
```

This will return the details of the current JMS notifier configuation; see below for an example:

```
Enabled     Context Factory Class                               Connection Factory Name         Queue Name     URL                  Username    Password
true        com.sun.enterprise.naming.SerialInitContextFactory  jms/__defaultConnectionFactory  notifierQueue  localhost:7676
```

## Troubleshooting
When you have correctly configured the JMS notifier, it can be used to push notifications to your configured queue. If you do not see any notifications, check the following:

* Is your MDB or other JMS client correctly configured to consume messages from the correct queue? (e.g. check for typos)
* Are the JMS queue details correctly entered in the JMS notifier configuration? (check the server.log for errors)
* Is the JMS queue available? If you have configured your own JMS broker, is it responding? If the broker is remote, check that it is reachable.
* Is the service using the notifier configured to send notifications frequently enough to observe?
* Is the service using the notifier correctly configured and also enabled?