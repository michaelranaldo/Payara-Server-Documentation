# Notification Service
#### Command Reference


## `notification-configure`

**Usage:** `asadmin> notification-configure --enabled=true --dynamic=true`  

**Aim:** Enables or disables the service.


#### Command Options:

| Option | Type | Description | Default | Mandatory |
|--------|------|-------------|---------|-----------|
| `--enabled=true` | Boolean | Enables or disables the service | False | No |
| `--dynamic=true` | Boolean | When set to true, applies the changes without a restart. Otherwise a restart is required. | False | No |

The argument `--dynamic=true` is necessary to turn on the service for a running server, otherwise the change would only be applied after a server restart.

#### Example:
```
asadmin> notification-configure \
--enabled=true \
--dynamic=true
```

##`notifier-list-services`
**Usage:** `asadmin> notifier-list-services`

**Aim:** Lists available notifiers to use with the service. These can then be configured individually or referenced by other service commands, for example the [`requesttracing-configure-notifier`](/documentation/extended-documentation/request-tracing-service/asadmin-commands.md#requesttracing-configure-notifier) command.


#### Command Options
There are no options for this command

#### Example
In order to configure the notifier for request tracing, for example, the asadmin command to list available notifiers should be run first:

```
> asadmin notifier-list-services
```

which will give the following output:

> ```
> Available Notifier Services:
>         service-log
> 
> Command notifier-list-services executed successfully.
> ```

By providing a notifier service with its name, it’s possible to assign it to another service, like the Request Tracing service. The command named `requesttracing-configure-notifier` adds a logger notifier to request tracing by enabling it as follows:
```
asadmin> requesttracing-configure-notifier
    --notifierName="service-log" \
    --notifierEnabled=true \
    --dynamic=true
```

## `notification-configure-notifier`
**Usage:** `asadmin> notification-configure-notifier --notifierName=${name} --notifierEnabled=true --dynamic=true`

**Aim:** Enables or disables an individual notifier for the notification service to use.

#### Command Options:

| Option | Type | Description | Default | Mandatory |
|--------|------|-------------|---------|-----------|
| `--notifierName=${name}` | String | The name of the notifier to configure | - | Yes |
| `--notifierEnabled=true` | Boolean | Enables or disables the service | False | No |
| `--dynamic=true` | Boolean | When set to true, applies the changes without a restart. Otherwise a restart is required. | False | No |

#### Example:
```
asadmin> notification-configure-notifier \
--notifierName=service-log \
--notifierEnabled=true \
--dynamic=true
```

## `get-notification-configuration`

**Usage:** `asadmin> get-notification-configuration`

**Aim:** This command can be used to list the details of the Notification Service.

#### Command Options:

There are no options for this command.

#### Example:
```
asadmin> get-notification-configuration
```

will give output similar to the following:

> ```
> Enabled  Notifier Enabled  Notifier Name  
> false    false             service-log    
> Command get-notification-configuration executed successfully.
> ```

## `set-notification-configuration`

**Usage:** `asadmin> set-notification-configuration --enabled=true --dynamic=true --notifierName="service-log" --notifierEnabled=true --notifierDynamic=true`

**Aim:** This command can be used to set all configuration of the Notification Service at once. It effectively wraps `notification-configure` and `notification-configure-notifier` in one command.

#### Command Options:

| Option | Type | Description | Default | Mandatory |
|--------|------|-------------|---------|-----------|
| `--enabled=true` | Boolean | Enables or disables the service | False | No |
| `--dynamic=true` | Boolean | When set to true, applies the changes without a restart. Otherwise a restart is required. | False | No |
| `--notifierName` | String | The name of the notifier to use | `service-log` | Yes |
| `--notifierEnabled` | Boolean | Enables or disables notifications | false | Yes | 
| `--notifierDynamic=true` | Boolean | When set to true, applies the changes without a restart. Otherwise a restart is required. | false | No |

####Example:
```
asadmin> set-requesttracing-configuration
    --enabled=true \
    --dynamic=true
    --notifierName="service-log" \
    --notifierEnabled=true \
    --notifierDynamic=true
```