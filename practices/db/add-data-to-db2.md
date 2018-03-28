# Adding Data to DB2

Data needed for testing or other uses can be added to the DB2 databases in the lower-order (development) environments. 

In general, test cases should try to create their own data, and clean up when done, in order to reduce the possibility of test data pollution. However there will be cases when adding new data is required. Given this, its recommended to add new data for your specific testing, and not re-use existing data.

By following the steps described at the [DB2data github repo](https://github.com/ca-cwds/db2data) you can get data added to the DB2 Docker container (for local development). This data will also be manually added to the DB2 mainframe baseline image. 
The goal of this process is that when the DBs are refreshed, all environments will be reset to an identical image will contain what teams need for testing.   

## NOTE ## 
In some cases, you will not know how to construct the queries needed to correctly add data to CWS/CMS DB2 database. In this case, you will need to work with the DB2 DBAs. The steps are:
+ You (developer) work with a legacy SME to use the legacy app to add data needed. Once you confirm that the data can be added, contact the DBAs
+ The DBAs can prep the mainframe to capture sql logs. Then your legacy SME will repeat the steps to add needed data to the legacy. 
+ When done, the DBA can extract the captured SQL for you, and you can follow the [process described above](https://github.com/ca-cwds/db2data) for adding SQL to the DB2 Docker container via liquibase. 
