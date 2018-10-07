---
title: " Connecting to Google BigQuery with DBeaver"
date: 2018-10-07
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

You can find installation instructions [here](/post/2017-03-26-dbeaver-mac/).
Make sure to install version 5.2.2 or later. If you haven't updated to 5.2.2 or later you may use this [post](/post/2018-09-22-dbeaver-bigquery/)
as a guide for connecting to BigQuery.

# 1) Create a new service account

  1. Instructions & details for creating a new service account can be found on [Google's website](https://cloud.google.com/docs/authentication/production#auth-cloud-implicit-python)
  1. Grant your desired BigQuery permissions to your new service account
  1. Download the service account key

# 2) Create a new connection

  1. In the menu bar navigate to `Database > New Connection`
  1. Select BigQuery & press next
  1. Fill in project with the name of your BigQuery Project
      * Optional, add additional projects in the subsequent field
  1. Select service-based
  1. Fill in the name of the service account ex: `bigquery-demo@project_name.iam.gserviceaccount.com`
  1. Fill in the path to the service key downloaded earlier
  1. Press finish

Congrats you've successfully connected to BigQuery using Dbeaver!

# 7) Troubleshooting

  * If you receive
  `[Simba][BigQueryJDBCDriver](100004) HttpTransport IO error : 403 Forbidden` make sure you've created a service account with the necessary permissions.
