---
title: " Connecting to Google BigQuery with DBeaver"
date: 2018-09-22
draft: false
categories : [
    "Analyst",
]
tags: ["SQL",
      "DBeaver",
      "BigQuery",
      ]
---

# 0) Install DBeaver

You can find installation instructions [here](/post/2017-03-26-dbeaver-mac/)

# 1) Download the latest drivers
You can find the latest drivers on [Google's website](https://cloud.google.com/bigquery/partners/simba-drivers/)

# 2) Create a folder to store the drivers
`mkdir ~/.dbeaver-drivers/bigquery/`

# 3) Extract driver jars and move to the folder we made earlier

![jars_in_folder](/img/20180922_bigquery_jars_in_place.png)

# 4) Create a New Driver in DBeaver

  1. Navigate to `Database > Driver Manager > New`
  1. Add all the files from `~/.dbeaver-drivers/bigquery/`
  1. Driver name: `BigQuery` (for labeling only)
  1. Class name: `com.simba.googlebigquery.jdbc42.Driver` (at the time of this writing)
  1. Default port: `443`
  1. URL template: `jdbc:bigquery://https://www.googleapis.com/bigquery/v2:443;ProjectId={server};OAuthType=0;OAuthServiceAcctEmail={user};OAuthPvtKeyPath={host};`
    * Note there are 4 different ways to connect to BigQuery using the JDBC driver. This tutorial illustrates connecting using the service account authorization method.
    * Additionally, at the time of this writing, Dbeaver only supports a couple URL template variables (e.g. server, user, host) which is why I've used the `host` variable for a path to key file rather than something like `key_path`

# 5) Create a new service account

  1. Instructions & details for creating a new service account can be found on [Google's website](https://cloud.google.com/docs/authentication/production#auth-cloud-implicit-python)
  1. Grant your desired BigQuery permissions to your new service account
  1. Download the service account key

# 6) Create a New Connection

  1. In the menu bar Navigate to `Database > New Connection`
  1. Select BigQuery
  1. Fill in the appropriate values for host, server, user
  1. Set host to the path the service account key e.g., `/Users/admin/.dbeaver_drivers/bigquery/project_name-####.json`
  1. Set server to project id for your BigQuery project
  1. Set user to the email address for the generated service account
  1. Press finish

  Congrats you've successfully connected to BigQuery using Dbeaver!

![successful connection](/img/20180922_bigquery_connection.png)

# 7) Troubleshooting

  * If you receive `[Simba][BigQueryJDBCDriver](100004) HttpTransport IO error : 403 Forbidden` make sure you've created a service account with the necessary permissions.
  * As of Dbeaver 5.2.0 Dbeaver is unable to return arrays of ints and other numerics
    * e.g., select [1, 2] as ids results in `org.jkiss.dbeaver.model.exec.DBCException: SQL Error [10140] [22003]: [Simba][JDBC](10140) Error converting value to long.`
    * You can still use
