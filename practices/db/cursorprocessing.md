# Cursor Processing

DB2 has a mechanism called a cursor. Using a cursor is like keeping your finger on a particular line of text on a printed page. In DB2, an application program uses a cursor to point to one or more rows in a set of rows that are retrieved from a table. You can also use a cursor to retrieve rows from a result set that is returned by a stored procedure.

Cursor processing involves four steps: declaring, opening, fetching and closing the cursor.

1. The DECLARE statement doesn’t execute any DB2 code, it just defines (or declares) the SELECT statement for the cursor.


2. The OPEN statement will result in the SELECT statement being executed. At OPEN time, the results will either be materialized into a work file or DB2 will read enough data to allow your program to fetch the results without having to wait for synchronous I/O. Whether or not DB2 materializes the result set depends on whether DB2 needs to read the entire result set before returning a single row to the program (likely because of some sorting or merging of multiple tables required) or whether DB2 can return data a set of rows at a time (likely because no ordering is required and data can be returned to the program in the order it is accessed from the table).


3. The FETCH statement retrieves (fetches) a single row from the set of rows returned by the cursor (either from the base table or from the work file).


4. The CLOSE statement informs DB2 that the program no longer will fetch any more rows from the cursor. The CLOSE statement may be issued after you fetch al the rows or after you have fetched all the rows you desire to read.


Following are some application development practices that you should follow when using cursors in DB2 programs.

## When and when not to use a cursor

A cursor is a valuable construct for returning multiple rows to an application program. Since the program can only deal with one row at a time, a cursor can be used to allow a program to loop through logic which issues a FETCH statement to return one row at a time to the program.

A cursor is required if you want to be able to return more than one row to your program from a single SQL statement. A cursor is not required if you know your query can only return one row or if you only want one row returned and you don’t care which row if multiple rows match the criteria specified in the WHERE clause.

**If you know your query can only return one row, then you should code a singleton SELECT statement instead of using a cursor. There is no need to use a cursor.

Similarly, if you want to retrieve a single address for a client and you don’t know whether there is more than one address in existence for that client, you can use the FETCH FIRST 1 ROW ONLY clause to avoid the need for a cursor. This ensures that only one row is returned to your program, therefore eliminating the need for a cursor.

There are two other techniques that are sometimes used to return a single row when more than one could qualify. Neither of these techniques is recommended because they incur additional overhead or do not guarantee the results will be as expected.

Declaring a cursor and then closing it after returning one row – This technique is not recommended because it incurs the overhead of opening and closing a cursor in addition to selecting a row. The more efficient technique is to use FETCH FIRST 1 ROW ONLY.

Coding a singleton SELECT and handling SQLCODE -811 as an SQLCODE 0 – If you code a singleton SELECT statement and DB2 returns more than one row, the SQL statement will receive SQLCODE -811. Although programs are often coded in this manner (to handle the -811), and the data in the working storage variables are then evaluated as if the data was returned correctly, there is no guarantee that this behavior will provide you with a valid result and it is therefore not recommended.

## When to define a cursor WITH HOLD

A cursor can be defined WITH HOLD or WITHOUT HOLD. The default is WITHOUT HOLD. Cursors that are declared WITH HOLD are kept open across a commit. This technique is often used for on-line applications that display a number of rows per screen and then allow the user to scroll to the next or previous set of rows. Declaring the cursor WITH HOLD eliminates the need for the application to include repositioning logic to handle the scrolling.

Declaring a cursor WITH HOLD may cause claims to be held on DB2 objects for a longer period of time. How long the claims are held depends on whether or not DB2 needs to materialize the result set at the time the cursor is opened.

If the cursor does not materialize, the claims on the base DB2 objects held by the cursor WITH HOLD will be held until the first commit after the cursor is closed.

If the cursor does materialize, the claims on the base DB2 objects held by the cursor WITH HOLD will be released by the first commit following materialization (OPEN CURSOR). This is because the data from the base DB2 objects is read into a work file when the OPEN CURSOR is executed. The cursor will continue to hold claims on the work file, but all locks and claims on the base objects are released. Since utilities are never run on the work files, these claims do not threaten concurrency and availability requirements.

The following criteria should be used to decide when it is appropriate to code WITH HOLD on a cursor:

• If you are certain that the cursor will always materialize, you should leave the WITH HOLD clause on the cursor.


• If the cursor does not materialize, and is easy and inexpensive to reposition, you should consider removing the WITH HOLD from the cursor and reopening it after each commit.


• If the cursor does not materialize, but the repositioning logic is expensive, there are some techniques to improve the performance of the repositioning so that the WITH HOLD clause can be removed. These techniques are described in the topic “Cursors WITH HOLD” in chapter 12 of the IBM redbook “DB2 UDB for z/OS: Application Design for High Performance and Availability”, SG24-7134.


• If the cost of the cursor repositioning cannot be reduced to an acceptable level, the WITH HOLD should be left on the cursor to maintain position. Be aware of the effect of the WITH HOLD clause on lock and claim retention, and schedule the process at a time when it will not be in contention with utilities that require drains (e.g. database Reorgs) or in contention with other applications.


• In a distributed environment, using a WITH HOLD cursor will prevent efficient thread pooling. See the topic “Thread reuse in a distributed environment” in chapter 11 of the IBM redbook “DB2 UDB for z/OS: Application Design for High Performance and Availability”, SG24-7134.

