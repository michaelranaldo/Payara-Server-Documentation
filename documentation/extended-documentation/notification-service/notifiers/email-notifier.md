# Email Notifier
Receiving notifications via email is still a powerful way to drive automated systems and receive remote prompts.

Payara Server is now able to direct notifications from the [Notification service](/documentation/extended-documentation/notification-service/notification-service.md) to a single given email address.

## Requirements
To use an email address as a notification target you must have a valid email address, and the smtp address for your email host.

## Configuration
At a high level, the steps to configure the email notifier are:

1. Within Payara create a JavaMail Session
1. Create the notifier using either the asadmin command or the Admin Console.

### Email Notifier Configuration
If you don't already have a JavaMail session set up, you will need one to send the notifications. Instructions on setting up a JavaMail session can be found [here](/documentation/core-documentation/javamail.md).

The steps to create an Email Notifier in Payara Server are as follows:

The email notifier is enabled from the Notification tab of your instance configuration. Here the jndiName of the JavaMail session and the intended address are entered. The email notifier supports a single email address.

  ![](/assets/admin-console-email-notifier-configuration-2.png)

Mirroring the above screenshot for the Admin Console, to set up an email notifier using asadmin commands:

````Shell
asadmin notification-email-configure --jndiName=emailNotifier --to=notifications@payara.fish --enabled=true --dynamic=true
````

To check the currently applied configuration from asadmin, run the command:
```Shell
asadmin get-email-notifier-configuration
```

This will return the current configuration, whether it is enabled, the "to" address, and the JNDI name of the JavaMail session in use.
