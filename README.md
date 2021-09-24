# geometry_columns-for-MS-SQLServer

SQL procedures and command to automatically update a geometry_columns table. It it used by QGIS to reduce the amount of initial queries to inspect the database for spatial tables or views

You have to check the "Only look in the geometry_columns meta data table" in the MS SQL-Server connection details for QGIS to optimize its search 

There are 2 files:
- run_once.sql: SQL to execute once in SQL Manager (or likewise) for each database to install 2 stored procedures and create table dbo.geometry_columns
- run_when_spatial_tables_or_views_added.sql: SQL to run in SQL Manager (or likewise) every time you add or remove a spatial table or view

TODO: 
- Find original Stack-Exchange entries where part of the code orignated and aknowledge in readme 
- Change content of run_when_spatial_tables_or_views_added.sql to a stored procedure
- Extend existing run_once stored procedures with function to evaluate spatial extends of the specific table/view and update relevant QGIS specific columns with information