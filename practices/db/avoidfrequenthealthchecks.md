# Avoid Frequent health checks



Use error/exception handling routines
and SQL code check rather than frequent health checks.  



 



For example, executing a ‘Select’ against
the DB2 catalog (example: ‘SELECT 1 FROM SYIBM.SYSDUMMY1’ every 30 seconds or
every minute may help indicate if the RDBMS itself is up, but may not warn you
appropriately of any specific application database related issues, and
furthermore, if the ‘Select’ is not coded appropriately in terms of isolation
level (meaning not explicitly coded ‘For Read Only’), then you may unknowingly
create page locks on rows within the database, when you did not want to.



 



Better example: ‘SELECT 1 FROM SYIBM.SYSDUMMY1
**FOR READ ONLY WITH UR**’



 



Nonetheless, having your application code check for
errors instead, can be more timely and specific to the database you are
actually referencing.



 



You may also consult with your Dev-Ops analyst(s)
to leverage any new non-intrusive health checks they may have been developing.
