# Notification Service

Payara Server version 4.1.1.163 introduced a general Notification service in order to log events which come from other services, such as the [Health Check service](/documentation/extended-documentation/health-check-service/health-check-service.md) or the [Request Tracing service](/documentation/extended-documentation/request-tracing-service/request-tracing-service.md)

The Notification service provides the ability to disseminate notification events through various channels that are being created by other services, such as the Request Tracing and Health Check services. The Notification service is provided with a number of configurable _notifiers_, the default being a log notification mechanism which can be seen in this `domain.xml` snippet:

```
<notification-service-configuration enabled="true">
    <log-notifier-configuration enabled="true" />
</notification-service-configuration>
```


The main configuration tag `notification-service-configuration` has only one attribute, named `enabled`, which can be set to either `true` or `false`. This provides the ability to globally enable or disable all notifications to all configured notifiers.

The `<log-notifier-configuration>` tag registers a log notifier to the pub-sub model of the notification service where it subscribes to each log notification event that would get published by another service.

The Notification service can be configured through the admin console:

![Notification service admin console screenshot](/images/notification-configuration.png)


* [Asadmin Commands](asadmin-commands.md)
