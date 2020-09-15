POSTGRES - using SQL Shell

enter path (in Windows 10): <<Environment Variables... -> New... >>>
C:\Program Files\PostgreSQL\12\bin

start command line in bash = psql -U postgres

or start a database already made = psql 'database_name'

to create the database = CREATE DATABASE test;  
to connect to a database = \c test  
to list all databases = \l  
to list relations = \d  
                  = \d users  
to quit SQL Shell = \q  
to show where database is stored = show data_directory;  
to see all the run-time parameters = show all;  

