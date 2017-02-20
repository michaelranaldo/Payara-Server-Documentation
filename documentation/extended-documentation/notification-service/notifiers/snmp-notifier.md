# SNMP Notifier

#### Getting SNMP Configuration

To get the current SNMP configuration using asadmin, run the command:

```Shell
asadmin get-snmp-notifier-configuration
```

This will return the details of the current SNMP configuration; see below for an example:

```Shell
Enabled    Community    OID                  Version   Host        Port
true       example      .1.3.6.1.2.1.1.8     v2c       127.0.0.1   162
```
