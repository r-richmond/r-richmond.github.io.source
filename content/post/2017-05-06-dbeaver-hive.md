---
title: " Connecting to Hive with Dbeaver using Kerberos Authentication"
date: 2017-05-06
draft: false
categories : [
    "Analyst",
]
tags: ["SQL",
      "Dbeaver",
      "Hive",
      "Kerberos", ]
---

# 0) Install Dbeaver

You can find installation instructions [here](/post/dbeaver-mac/)

# 1) Download the latest drivers
You can find the latest drivers on the [Cloudera website](https://www.cloudera.com/downloads/connectors/hive/jdbc.html)

# 2) Create a folder
`mkdir ~/.dbeaver-drivers/cloudera-hive/`

# 3) Extract driver jars and move to folder

![jars_in_folder](/img/20170506_hive_jars_in_place.png)

# 4) Create New Driver in Dbeaver

  1. Navigate to Database > Driver Manager > New
  1. Add all the files from `~/.dbeaver-drivers/cloudera-hive/`
  1. Driver name: `Hive-Cloudera` (for labeling only)
  1. Class name: `com.cloudera.hive.jdbc41.HS2Driver` (at the time of this writing)
  1. Default port: `10000`
  1. URL template: `jdbc:hive2://{host}:{port}/{database};AuthMech=1;KrbRealm=FOO.BAR;KrbHostFQDN={server}; KrbServiceName=hive;KrbAuthType=2`
    * Note you need to change `FOO.BAR` to match your krb5.conf settings


# 5) Create New Connection

  1. Navigate to Database > New Connection
  1. Select Hive-Cloudera
  1. Fill in the appropriate values for host & database (I set database to default)
  1. Set server to be your KrbHostFQDN
  1. Leave your user name & password blank
  1. Test connection
  1. Press next, next, & change the name of this connection as you see fit
  1. Press finish

  Congrats you've successfully connected to hive using kerberos authentication!

# 6) Troubleshooting

If you are receiving `[Cloudera][HiveJDBCDriver](500168) Error creating login context using ticket cache: Unable to obtain Principal Name for authentication` make sure to check the following

  1. Ensure that you have the latest cryptography libraries installed
    * Java 9 includes these libraries by default
  1. That you've configured your `/etc/krb5.conf` successfully
    * If you've done this correctly you should be able to run `kinit` in terminal and create a ticket without issue
  1. For Windows adding the following lines to your dbeaver.ini may be necessary as well
    * `Djava.security.krb5.conf=c:\kerberos\krb5.ini`
    * `Djava.security.auth.login.config=c:\kerberos\jaas.conf`
      * success has been reported with the following jaas.conf file & keytab usage
      ```
    Client {
       com.sun.security.auth.module.Krb5LoginModule required
            debug=true
            doNotPrompt=true
            useKeyTab=true
            keyTab="C:\Users\{user}\krb5cc_{user}"
            useTicketCache=true
            renewTGT=true
            principal="{user}@FOO.BAR"
        ;
    };
```
