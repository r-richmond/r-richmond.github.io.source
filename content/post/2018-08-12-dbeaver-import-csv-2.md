---
title: "Importing a CSV into a database using DBeaver Part 2"
date: 2018-08-12
draft: false
categories : [
    "Analyst",
]
tags: ["SQL",
      "DBeaver",
      "CSV",
      ]
---

## Forward

This is a followup to my previous [post](/post/2018-06-12-dbeaver-import-csv/). My previous post demonstrated how to import a CSV using Dbeaver's database to database export & import feature. As of version 5.1.5 Dbeaver introduced a direct CSV option for importing CSVs.

## 0) Install DBeaver

You can find installation instructions [here](/post/2017-03-26-dbeaver-mac/)

## 1) Connect to your target database

1.1) Navigate through your target database & schema and right click on your target table and select import table data

![import_table_data](/img/20180612_import_table_data.png)

1.2) Next select CSV from the list

![select_csv_option](/img/20180812_select_csv_option.png)

1.3) Select your CSV file for upload

![select_csv_table](/img/20180812_select_csv_file.png)

## 2) Ensure that the mappings of each of your columns is correct

* For column names that are an exact match DBeaver will automatically map them for you
* For the remaining columns make sure to map the source columns to your desired target columns

![map_columns](/img/20180812_map_columns.png)

## 3) Complete the wizard and watch DBeaver import your data

Note: For large files it may be necessary to go get lunch but in my case 4 records doesn't take long to import :)

![data_finished](/img/20180612_data_finished.png)

## 4) Check to make sure that the data has loaded correctly

As a last optional step it is good practice to make sure that everything loaded correctly which can easily be done by running a query against your target DB

![data_in_table](/img/20180612_data_in_table.png)
