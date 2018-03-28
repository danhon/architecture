# Upgrading CWS CARES to new DB2 schema version

When the current CWS/CMS system is upgraded to support new release functionality, CWS-CARES needs to test and ensure the changes have been reviewed and are addressed in CARES. 
 
**Steps**
+ IBM releases a new version of CWS/CMS DB2
+ CWS-CARES upgrades all environments to new version of DB as soon as it is convenient for IBM 
+ We will test our application using the new version and work to identify any errors

Around Code Freeze Time (2 weeks before Go-Live)
+ CWS-CARES will keep our staging at the current (old) release of DB2. This will allow us to support current (old) system still in production 
+ During the week after the release (Go-Live weekend) of the new DB into CWS-CMS production, CARES will work with IBM to update our staging to the new version of DB2
