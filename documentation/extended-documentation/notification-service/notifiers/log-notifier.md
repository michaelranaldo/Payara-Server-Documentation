# Log Notifier
The default output for the log notifier is the configured instance log file, which is either the `server.log` file or `cluster.log` file, depending on the instance configuration. More details on Payara Logging can be found [on the logging page](/documentation/core-documentation/logging/logging.md). The log notifier is the only notifier which is enabled by default when the notification service is activated.

## Configuration

By default, the log notifier will receive notifications from the [notification service](/documentation/extended-documentation/notification-service/notification-service.md) and outputs them to the configured logs when activated.

### Payara Configuration

The log notifier is, by default, disabled on startup. However, as the default notifier it is enabled when the [notification service](/documentation/extended-documentation/notification-service/notification-service.md) is enabled.

To enable the log notifier specifically, run the command:

```Shell
asadmin notification-log-configure --enabled=true --dynamic=true
```

## Log Configuration

To get the current configuration of the log notifier, run the command below:

```Shell
asadmin get-log-notifier-configuration
```
