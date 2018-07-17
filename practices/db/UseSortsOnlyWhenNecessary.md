# Use Sorts only when absolutely necessary

The most common reason for sorting is the ORDER BY clause of a SELECT statement. DB2 can avoid a physical sort if a suitable index is available.  You may in fact design an index for this very reason.  If you have such an index, you do not incur sorting costs.  

Sorts can also occur if the following SQL clauses are used: GROUP BY, DISTINCT, some JOIN methods and UNION may cause sorts. UNION without ‘ALL’ always requires a sort; the others may use an index. There may be other circumstances where a sort is used by DB2, but those mentioned above are the primary ones.

Sorting rows has several side effects, such as materialization of the result set, impact on the locking behavior, the creation of a work file and others.  Each of these side effects will result in an increase in the CPU consumption of the SQL statement.

You can reduce CPU time by avoiding a sort whenever possible.  Note that if you require the data to be returned in a certain order, then you should not depend on DB2 to perform a sort by using any of the above clauses other than ORDER BY or UNION.  In many cases DB2 can perform the requested function, such as GROUP BY, using an existing index.  In that case you should specify ORDER BY to ensure that the results are returned in the order desired.  If DB2 can return the data in the desired order by using an index instead of performing a sort, then it will and you will gain the benefits of avoiding the sort.

The following techniques can be used to avoid a sort.  

## Specify GROUP BY in the order you want results returned

The GROUP BY clause groups the rows in the result set by the criteria specified in the GROUP BY clause.  Also, the ‘group by’ should match the column order of any available composite index. The query result will have one row for each column combination specified in the GROUP BY clause.  

## Use UNION ALL instead of UNION when possible

The UNION clause allows you to specify multiple SELECT statements and merge the results into one report.  There are two variations of UNION:
•	UNION ALL – Returns ALL the rows from all the SELECT statements
•	UNION – Eliminates duplicates from the resulting set of rows

UNION is more expensive than UNION ALL because a sort is required to determine whether there are any duplicate results in the output.  Any duplicates are then removed.

If you are not concerned about whether there are any duplicates in your output, or if it is not possible to have duplicates, then you should use UNION ALL to avoid the need for a sort. You may still want to sort the results if you desire the output in a particular order, but you are eliminating the sort required by DB2 to eliminate duplicates.

## Use of DISTINCT to show a single row for each distinct value

The DISTINCT clause eliminates duplicates in your result set in order to show a distinct (unique) set of values.

You should be aware of what order you want to display your results and of what indexes are available and code your DISTINCT clause appropriately to take advantage of those indexes.  If you require that the results be in a certain order, then you should include an ORDER BY clause; DB2 will determine whether a sort is required to maintain the desired order.
