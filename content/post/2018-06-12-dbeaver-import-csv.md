---
title: "Importing a CSV into a database using DBeaver"
date: 2018-06-12
draft: false
categories : [
    "Analyst",
]
tags: ["SQL",
      "DBeaver",
      "CSV",
      ]
---

## 0) Install DBeaver

You can find installation instructions [here](/post/2017-03-26-dbeaver-mac/)

## 1) Create a folder to be used as your CSV Database

`mkdir ~/desktop/csvs`

Place the CSV you want to load into this folder

## 2) Create a CSV database connection
In the menu bar select `Database > Create a New Connection`
 & from the list of drivers select `Flat files(CSV) > CSV/DBF`

![select_driver](/img/20180612_select_driver.png)

Set the path of the connection to the folder you created earlier (the JDBC URL will auto-populate)

![configure_path](/img/20180612_configure_path.png)

Note: If you run into trouble downloading the driver navigate to the [source website](http://csvjdbc.sourceforge.net/) and download the driver manually

## 3) Connect to your target database

3.1) Navigate through your target database & schema and right click on your target table and select import table data

![import_table_data](/img/20180612_import_table_data.png)

3.2) Next select your source CSV from your CSV connection as the source container

![select_csv_table](/img/20180612_select_csv_table.png)

Note: In this example case I'm loading a test CSV into a Postgres database but this functionality works with any connection that DBeaver supports (which is basically everything)

## 4) Ensure that the mappings of each of your columns is correct

* For column names that are an exact match DBeaver will automatically map them for you
* For the remaining columns make sure to map the source columns to your desired target columns

![map_columns](/img/20180612_map_columns.png)

## 5) Complete the wizard and watch DBeaver import your data

Note: For large files it may be necessary to go get lunch but in my case 4 records doesn't take long to import :)

![data_finished](/img/20180612_data_finished.png)

## 6) Check to make sure that the data has loaded correctly

As a last optional step it is good practice to make sure that everything loaded correctly which can easily be done by running a query against your target DB

![data_in_table](/img/20180612_data_in_table.png)

## 7) Final Notes & Thoughts

* While this process takes a little bit more time to get setup than other tools setting up the CSV connection only needs to be done once
  * One side benefit of this as well is that you are now able to run SQL queries against CSVs very easily
* The only real pain point that I have run across is that if you add a new CSV file or add/delete columns in an active CSV connection you have to cancel the import wizard & refresh the CSV connection for the changes to be picked up
  * this feedback was provided in [issue 926](https://github.com/dbeaver/dbeaver/issues/926) and hopefully it will be resolved in a future update
