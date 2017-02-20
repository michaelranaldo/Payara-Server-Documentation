# Log Notifier
The default output for the notification service is the `server.log`. More details on Payara Logging can be found [here](../core-documentation/logging/logging.md).

## Configuration

By default, Payara Server will send notifications from the [Notification service](/documentation/extended-documentation/notification-service/notification-service.md) to the logs when activated.

### Payara Configuration

The log notifier is not automatically enabled when Payara starts - to enable log notifications run the command:

```Shell
asadmin notification-log-configure --enabled=true --dynamic=true
```

This will also enable the notification service. More details on specific commands for the notification service can be found [here](/documentation/extended-documentation/notification-service.md).

## Log Configuration

To get the current configuration of the log notifier, run the command below:

```Shell
asadmin get-log-notifier-configuration
```
