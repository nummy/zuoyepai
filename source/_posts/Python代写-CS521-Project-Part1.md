---
title: 'Python代写: CS521_Project Part1'
date: 2019-01-04 16:48:29
tags: 
- Python
categories:
- Python代写
---

### Purpose

This assignment is the first of a mini project where you are going to demonstrate your understanding of the modules of this class.
The mini project is about building a small ETL program in python. Each part will focus on different portions / stages of the ETL process.

### Assignment Background

Summarizing your acquired knowledge from modules 1-4, we are going to focus on the E part of the ETL process. For reference, ETL stands for Extract, Transform, Load. We are going to focus here on Extract.
Assignment Statement

•   Read CSV files – You may use the csv module and its methods for this project.  Please see https://docs.python.org/3.5/library/csv.html for more information.
•   Load the content of the CSV files into usable records
•   Use polymorphism to hold data
•   Use inheritance to process data
 
### Requirements:

To extract the raw data (row) into a usable format that can be relied upon by the rest of your application, we will define the concept of a record.

1.  Create class: AbstractRecord
a.  This class will contain 1 (instance) member: name
2.  Create a record class for each of the files you want to load.  When a record is referenced in the requirements, we are referring to one of the following records:
BaseballStatRecord or StockStatRecord.
And including the following functionality:
a.  inherit the AbstractRecord
b.  have an initializer method that takes the data you want to load as arguments:
For stocks:
•   Stock symbol (ticker)→ this should be stored in the “name” member
•   Company name (company_name)
•   Exchange country (exchange_country)
•   Stock Price (price)
•   Exchange Rate (exchange_rate)
•   Shares Outstanding (shares_outstanding)
•   Net Income (net_income)
•   Market Value in USD (market_value_usd) – This value is calculated in step 4e
•   Price/Earnings Ratio (pe_ratio) – This step is calculated in step 4e
c.  for baseball
•   player name → this should be stored in the “name” member
•   salary
•   G (Games played)
•   AVG (which is the batting average)
d.  For each record type, override __str__() (https://docs.python.org/3/reference/datamodel.html#object.__str__ ) to return a string of the form: “<name of the record type> ( <value1>, <value2>,  <...> )” using “str.format”.
For floats please only display 2 decimal numbers (2 numbers after the comma) for monetary values and 3 decimal places for batting average.  It may be easier for you to work with USD.

To load the data we are going to need a CSV reader.

3.  Create 1 AbstractCSVReader class
a.  The class should have an initializer method taking the path to the file to be read
b.  The class should have the method: row_to_record(row)
•   Where “row” is a row from the CSV as a dictionary
•   This method should be implemented by simply raising NotImplementedError.
c.  The class should have the method: load() that returns a list of records. Load should:
i.  Use “with” to open the CSV files
ii. read each row from the file into a dictionary: keys are the column names and values are the matching values (see https://docs.python.org/3/library/csv.html#csv.DictReader )
iii.    call the row_to_record method and send the row as a parameter
iv. handle the BadData exception raised by  row_to_record by skipping the record – For more on BadData Exception see step 5
v.  If no exception is raised: then the record should be added to the list of records.
vi. Once all records are loaded into the list, returns the list.
4.  Create a CSV reader class for each of the files you want to load 
i.e. BaseballCSVReader and StocksCSVReader
a.  The class should inherit the AbstractCSVReader
b.  Each class should implement its own row_to_record method. The input is a dictionary of unvalidated data, it should validate the data, parse it, create new record and return the record created. 
c.  The validation depends on your concrete record:
•   Validation fails for any row that is missing any piece of information
•   Validation fails if the name (symbol or player name) is empty
•   Validation fails if any of the numbers (int or float) cannot be parsed (watch out of the division by zero!!)
d.  If validation fails: this method should raise a BadData exception (requirement #5)
e.  StocksCSVReader should have two calculations using the extracted records:
•   market_value_usd  = Price * ExchangeRate * SharesOutstanding
•   pe_ratio = Price / NetIncome{}
5.  Create a BadData custom exception to handle record creation errors
6.  From your main section ( https://docs.python.org/3/library/__main__.html )
a.  load the CSV (e.g.  BaseballCSVReader('path to my CSV').load())
b.  Print each record to the console. You are to use: print(record)
