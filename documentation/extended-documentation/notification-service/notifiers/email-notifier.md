# Email Notifier
Receiving notifications via email is still a powerful way to drive automated systems and receive remote prompts.

Payara Server is now able to direct notifications from the [Notification service](/documentation/extended-documentation/notification-service/notification-service.md) to a single given email address.

## Requirements
To use an email address as a notification target you must have a valid email address, and the smtp address for your email host.

## Configuration
At a high level, the steps to configure the email notifier are:
1. Within Payara create a JavaMail Session
- Create the notifier using either the asadmin command or the Admin Console

### JavaMail Configuration
If you don't already have a JavaMail session set up, you will need one to send the notifications. The steps to create a new JavaMail session in Payara are as follows:

#### From the Admin Console

1. JavaMail sessions are added from the `Resources` tab on the left pane of the Admin Console. Select `New` on the `Sessions` table to create a new JavaMail session.

  ![](/assets/admin-console-javamail-location.png)

- Fill in the required fields. The example below shows configuring a mail host with an address of `mail.payara.fish`, where mail will be sent from the service from the address `payara@payara.fish`. You must ensure that you have added in your authentication details here.

  ![](/assets/admin-console-email-notifier-configuration.png)

- Once you have 
#### Using asadmin Commands

```Shell
asadmin create-javamail-resource --mailhost mail.payara.fish --mailuser _mailuser_ --fromaddress _fromaddress_ --property mail-smtp-starttls-enable=true:mail-smtp-auth=true:mail-smtp-password=_password_ mail/EmailNotifications
```
