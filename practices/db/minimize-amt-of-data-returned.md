# Minimize Amount of Data Returned to Your Program

The cost of database I/O and the cost to move data from the buffer pool to your program contribute greatly to the overall cost of application programs.  Reducing the cost of any activity associated with returning data to your application program can result in reduced elapsed and CPU times.  Following are some techniques to reduce the cost of returning data to your program.

## Select only the columns you need

DB2 for z/OS database I/O generally occurs at the page level, which means that even though you may only need one row, DB2 will need to access the entire page of data that contains that row.  The data is read from DASD into the appropriate buffer pool, unless the data already resides in the buffer pool.

The database I/O cost is the same regardless of how many columns you select.  In other words, DB2 will return all the rows on the page into the buffer pool, and will return the data for all the columns in those rows.

Once the data is in the buffer pool, there is a subsequent CPU cost to move the data from the buffer pool to your program’s working storage for each column selected.  The cost is not the same for selecting all the columns as opposed to selecting a small subset of columns.  Use of ‘SELECT *’ is almost always forbidden since a) it’s inefficient and it may be rare that we ever need to retrieve all columns and b) if the table structure were to change you may receive unexpected results in your application logic and processing.

## Don’t select data you already know

The SELECT statement returns one or more rows of data that matches the criteria specified in the WHERE clause.  Here is a sample SELECT statement to return some data from the CLIENT_T table for a DRV_LIC_NO of 'CDL123456789abcdefgh':

```
SELECT DRV_LIC_NO, COM_FST_NM, COM_LST_NM, D_STATE_C
FROM cwsns1.client_t 
WHERE DRV_LIC_NO = 'CDL123456789abcdefgh'
WITH UR
```

In this particular example, the value for the column DRV_LIC_NO is supplied in the WHERE clause.  There is no need to include the same column in the SELECT list because you already know what the value will be for that column.

There is no savings in database I/O cost by excluding the column from your SELECT list, since DB2 has to read the page of data in which the row resides, but there is a savings in the cost to move data from the buffer pool to your program’s storage area.




## Don’t read from tables that you’ve already read

There are times when programs will need to read data from more than one table.  For example, to retrieve information about a userid, including their staff person, you will need to select data from the USERID_T and the STFPERST tables.  
If, after reading the data from the STFPERST table, a program needs to read data from another table, for example GVR_ENTC from the CWS_OFFT table, there is no need to re-select data from the USERID_T table as you already have that information in your program’s storage area.  You can use the same identifier key value from the USERID_T table to select from the CWS_OFFT table.  

Even though it is likely that the row would already exist in the buffer pool since it was previously selected, there is no need to incur the cost of DB2 checking to see if the row is in the buffer pool.

Another example of reading from tables that you’ve already read is where you have made the initial SELECT statement efficient by selecting only the columns you need, but then turn around and issue a second SELECT statement against the same table to select more columns.  In that case it would be more efficient to select all the columns you need up front.
