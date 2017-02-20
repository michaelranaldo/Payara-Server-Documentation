# JavaMail
A JavaMail session resource represents a mail session within the JavaMail API.
JavaMail sessions configured here can be referred to by their JNDI name.

## Configuration

### From the Admin Console

JavaMail sessions are added from the `Resources` tab on the left pane of the Admin Console. Select `New` on the `Sessions` table to create a new JavaMail session.

  ![](/assets/admin-console-javamail-location.png)

Fill in the required fields. The example below shows configuring a mail host with an address of `mail.payara.fish`, where mail will be sent from the address `payara@payara.fish`. You must ensure that you have added in your authentication details here.

  ![](/assets/admin-console-email-notifier-configuration.png)

### From asadmin

JavaMail sessions can be created directly from asadmin. The command `create-javamail-resource` creates a new JavaMail session and accepts the `mail host`, `mail user`, and `from address` as command-line arguments. To properly configure the email notifier, StartTLS must also be enabled, along with SMTP authentication, and the mail password. These are passed as colon separated arguments of the `--property` command-line argument.

The command below demonstrates this, using the same configuration as pictured above:

```Shell
asadmin create-javamail-resource --mailhost mail.payara.fish --mailuser payara --fromaddress payara@payara.fish --property mail-smtp-starttls-enable=true:mail-smtp-auth=true:mail-smtp-password=password mail/EmailNotifications
```
