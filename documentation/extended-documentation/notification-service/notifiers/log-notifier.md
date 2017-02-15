# Log Notifier
The default output for the notification service is the `server.log`. More details on Payara Logging can be found [here](../core-documentation/logging/logging.md).

## Configuration

Payara Server by default will send notifications from the [Notification service](/documentation/extended-documentation/notification-service/notification-service.md) to the logs when activated.

## Log Configuration

To get the current configuration of the log notifier, run the command below:

```Shell
asadmin get-log-notifier-configuration
```
