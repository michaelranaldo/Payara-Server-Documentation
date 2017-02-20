# JMS notifier

#### Getting JMS Notifier Configuration

To get the current JMS notifier configuration using asadmin, run the command:

```Shell
asadmin get-jms-notifier-configuration
```

This will return the details of the current JMS notifier configuration; see below for an example:

```Shell
Enabled     Context     Factory Class     Connection     Factory Name     Queue Name    URL                  Username    Password
true        ex_context  ex_factory        ex_connection  ex_factory_name  ex_queue      example.payara.fish  payara      password
```
