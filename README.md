# Postgres Business Case
This project is a data analysis business case focused on addressing final business questions. It includes technical steps such as database restoration, modeling adaptation, and customized correction with automation to handle native database issues.

## Intro
Data analysis project aimed at restoring a .sql file using the 'Restore' feature in PostgreSQL via the Query Tool method. Data management is done using PowerQuery, directly connected to the PostgreSQL server. Analytics - as final step -, are delivered using MS PowerBI.

<img src="https://github.com/vinifborgess/postgresql-business-case/blob/main/Data%20Architecture.jpg"/> 

## Setup

• Before starting, ensure that you have PostgreSQL installed on your machine.

• If you have forgotten your credentials, click on the following tutorial: [password recovery tutorial].

• Download the (.sql) file: [zip file link].

## Step 1: Restoring the .sql file [database]

PostgreSQL Setup: Within the PostgreSQL environment, check the version of your application. There are various ways to do this; the easiest and safest is to connect to the generic database 'postgres'. Right-click on Query Tool, enter your credentials (if you don't know or have lost them, access them here). With the terminal open, type SELECT version();. The output of the command will include secure information about the PostgreSQL version.

This step is crucial because when you install PostgreSQL on your system, these utilities are installed in a specific directory. However, if you have more than one version of PostgreSQL installed on your system, there may be different directories for each version.

Therefore, PostgreSQL needs to know where to find these utilities so that you can use them. This is done by setting the correct binary paths for each PostgreSQL version. Binary paths are the locations of the directories where the utilities are installed.

By setting the correct binary paths, you ensure that PostgreSQL uses the correct version of the utilities for the database version you're using. This is important because each PostgreSQL version may have changes or improvements to the utilities, and using the wrong version could result in unexpected behaviors or errors.

## Step 1.1: Reviewing binary paths

In PostgreSQL, go to Files -> Preferences -> Binary Paths -> and adjust the path to the directory where PostgreSQL is installed on your machine.

For example, the directory C:\Program Files\PostgreSQL\16\bin is where the PostgreSQL 16 utilities are installed. If you have PostgreSQL 16 installed on your system, you should set the binary path to this directory in the open fields under the EDB Advanced Server Binary Path and PostgreSQL Binary Path sections.

Adjust the path according to your PostgreSQL version.

## Step 1.2: Migrating SQL Code from .txt to PostgreSQL

With the binary paths adjusted, go to the data source file (.sql) and open it with your preferred text editor. Once the file is open, press CTRL + A to select all the code, and then CTRL + C to copy it to your clipboard.

Next, go to the 'postgres' database or another of your choice, right-click on the database name, open the Query Tool, and paste the copied code from your clipboard. In other words, migrate the SQL code from the source file to the terminal.

## Step 2: Execution and Validation

• Press F5 to execute the query. After the run, the tables from the code (6) will have been successfully generated in a logical and secure manner within the 'Schemas' section of your selected database.

• The tables generated within the public schema are:

• Movements (fact);
• City_State_Country (dimension);
• Clients (dimension);
•Items (dimension);
• Product_Goals (dimension);
• Representatives (dimension);

To view and check, navigate to 'Schemas' -> public -> Tables -> and verify that the six SQL code tables have been generated. For a better understanding of the data, right-click on a table and select View/Edit Data to view the dataset.

## Step 3: Data Ingestion into the MS PowerBI Environment

MS PowerBI has an integrated connection with the project's DBMS (PostgreSQL). In Get Data, search for PostgreSQL and select the 'PostgreSQL database' option.

Since the project is being executed in a local environment, in the server tab, enter your localhost (```localhost``` or ```127.0.0.1```) and the database where the tables are hosted.

For most systems, the default Postgres user is ```postgres```, and the password is the one you set during installation. If you don't know it, click here.

## Step 4: Import and Data Management

Import all the tables into PowerQuery, the native data management environment of MS PowerBI, and click Transform Data.

If you already have the .pbix file ready, simply update the credentials following the instructions from Step 3.

## Step 5: Adjusting database errors

In the fact table (Movements), there are errors with date records when attempting to merge the separate date-related fields.


## Step 6: Data Modeling 

<img src="https://github.com/vinifborgess/postgresql-business-case/blob/main/imagem_2024-08-19_172345393.png"/>


