---
title: "Importing a CSV into a database using DBeaver"
date: 2018-06-12
draft: false
categories : [
    "Analyst",
]
tags: ["SQL",
      "Dbeaver",
      "CSV",
      ]
---

## 0) Install DBeaver

You can find installation instructions [here](/post/2017-03-26-dbeaver-mac/)

## 1) Create a folder to be used as your CSV Database

`mkdir ~/desktop/csvs`

Place the CSV you want to load into this folder

## 2) Create a CSV database connection
In the menubar select `Database > Create a New Connection`
 & from the list of drivers select `Flat files(CSV) > CSV/DBF`

![select_driver](/img/20180612_select_driver.png)

Set the path of the connection to the folder you created earlier (the JDBC URL will auto-populate)

![configure_path](/img/20180612_configure_path.png)

Note: If you run into trouble downloading the driver navigate to the [source website](http://csvjdbc.sourceforge.net/) and download the driver manually

## 3) Connect to your target database

3.1) Navigate through your target database & schema and right click on your target table and select import table data

![import_table_data](/img/20180612_import_table_data.png)

3.2) Next select your target CSV as the source container

![select_csv_table](/img/20180612_select_csv_table.png)

Note: In this example case I'm loading a test CSV into a Postgres database but this functionality works with any connection that DBeaver supports (which is basically everything)

## 4) Ensure that the mappings of each of your columns is correct

* For columns that are exact match DBeaver will map them correctly for you
* For the remaining columns make sure to map the source columns to your desired target columns

![map_columns](/img/20180612_map_columns.png)

## 5) Complete the wizard and watch DBeaver import your data

Note: For large files it may be necessary to go get lunch but in my case 4 records doesn't take long to import :)

![data_finished](/img/20180612_data_finished.png)

## 6) Check to make sure that the data has finished loading

As a last optional step it is good practice to make sure that everything loaded correctly which you can see here

![data_in_table](/img/20180612_data_in_table.png)

## 7) Final Notes & Thoughts

* While this process takes a little bit more time to get setup than other tools the setup part is only a one time pain
* After setting this up you are also able to easily query CSVs using SQL within the best SQL IDE on the market :)
  * Simply use the CSV connection like any other connection
* The only real pain point that I have run across is that if you add a new CSV file or add/delete columns in an active CSV connection you have to restart the import wizard & refresh the CSV connection for the changes to be picked up
  * this feedback was provided in [issue 926](https://github.com/dbeaver/dbeaver/issues/926) hopefully it is resolved in a future update
