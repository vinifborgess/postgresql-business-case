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

### 5.1 - Creation of a dCalendar for stabilization and universalization of dates for the data model.

• Creation of a dCalendar to stabilize and universalize dates for the data model based on the minimum/maximum year of entry of the database in Postgres up to the maximum recorded date. This allows that, as the data is updated in the DBMS, the dCalendar will also be updated.

### 5.2 - Solving the main date error

The error with dates involves incorrect days in months, such as having the 31st day in months with only 30 days, or the 29th day in February when it only has 28 days.

Since it is not possible to merge the original Month and Year fields and detect the correct date type directly, as this would not allow me to address the issues or identify the erroneous dates, I need to clone these columns for validation.

By creating clones of the Year and Month columns and renaming them to distinguish them from the original columns, I can perform the following steps without affecting the original data:

• Duplicate the Year and Month Columns: Rename the duplicates to differentiate them from the original columns.
• Merge the Duplicates: Combine the duplicated Year and Month columns to create a new column called MonthYear.
• Convert to Date Format: Change the MonthYear column to a date format.
• Add a Column to Identify Days in the Month: Create a new column that calculates the number of days in the month for each MonthYear, using the cloned Month and Year columns. Additionally, add a column for the Month Type to categorize the month based on the number of days.
• The logic for the Month Type column is as follows:

```
= Table.AddColumn(DaysInMonth, "Month Type", each 
    if [DaysInMonth] = 28 then "February - Non-Leap Year" 
    else if [DaysInMonth] = 29 then "February - Leap Year" 
    else if [DaysInMonth] = 30 then "Month with 30 Days" 
    else "Month with 31 Days"
)
```

This approach helps identify where corrections are needed without causing errors in the base data.

---

**Finalizing Date Corrections**

After creating the merged `MonthYear` column with the original Month and Year columns, you can use this merged column to retain the `Month Type` information, as it is based on the duplicates that match the originals.

With the `MonthYear` column now populated using the original Month and Year columns, you should avoid converting this new column to a date type. Converting it to a date with incorrect values could disrupt your logic. Instead, keep it as a string and perform a detailed analysis to identify which records have incorrect date entries.

Using the `MonthYear` column created from the duplicated columns, generate two new fixed columns: `FixedMonth` and `FixedYear`.

You can then create a stable and corrected date column by combining the Day (from the `DaysInMonth` column), the Month (from the `MonthYear` column), and the Year (from the `MonthYear` column, again based on the duplicates). 

This method allows you to fix the date accurately, as the erroneous entries typically occurred at the end of the month. By determining the number of days in each month for a given year, you generate the correct day values for the fixed date column.

Once the `Days` column is corrected, you can merge it with the `MonthYear` column generated from the duplicated Month and Year columns. This will result in a clean, stable, and new date column.

I prefer to use the duplicated `MonthYear` columns to validate potential errors against the original columns, but you can remove these duplicates after confirming that all day corrections are accurate. The main focus is ensuring the days are corrected properly.

## Step 6: Data Modeling 

<img src="https://github.com/vinifborgess/postgresql-business-case/blob/main/imagem_2024-08-19_172345393.png"/>


