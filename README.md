# INFO7210_DWBI_Assignment2
CourseName: Data Warehousing and Business Intelligence, Professor: Vincent Lattauda 
In computing, extract, transform, load (ETL) is the general procedure of copying data from one or more sources into a destination system which represents the data differently from the source. The term comes from the three basic steps needed: extracting (selecting and exporting) data from the source, transforming the way the data is represented to the form expected by the destination, and loading (reading or importing) the transformed data into the destination system.

In this assignment very basic and simple ETL process has been carried out. The source/destination are limited to OLE DB and Flat File(.txt here) types only. The steps are: 

Step 1: Extracting the data
An SSIS package was created to extract(export) the ‘Employee’ table in AdventureWorks2014 database in a comma-separated .txt file (Flat file). 
The source (SQL Server file) was connected to the package using OLE DB Connection Manager. The destination (Flat File) was connected using Flat File Connection Manager and the columns were mapped.
The package was deployed and as seen below, the debugging was successful, and the 290 rows of data were exported in a Employee_table.txt file.

Step 2 : Creating the Staging Area
Transformation of data demands a stage area where the transformations are performed before loading the data into a warehouse. This is the reason we need a staging table to transform and make the data load-ready.
A staging table was created in SQL with similar schema as the original source but less restrictive with constraints relieved for some variables which do not make the data nonsensical as the goal here is to enter as much data as possible.  
Now this table will be used as the destination in Step 3 to load our data in from the Flat file we created in Step 1.

Step 3: Loading the Data to Stage Area
Here the a Data Flow Task is built to load the data from the Flat File Source to a OLE DB Connection. As the source is Flat File, all the variables are of ‘string’ data type and though the datatype conversion from string to numeric etc is taken care by the SSIS task, it does not support Unicode to non-unicode conversions. Hence, there was one more step added in the Data Flow task which is ‘Data Type Transformation’. Once the data conversion is done, the data is to be loaded in OLE DB Destination which in this case is ‘stage’ table created in Step 2. 
The package was deployed. The process was successful and 290 rows of data was loaded successfully in the stage table as seen below:
