---
author: Banreet
ms.author: banreetkaur
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: include
ms.date: 10/04/2019


---

### <a name="ki_hinv"></a> Hardware inventory reports

<!--5468413-->
If you try to run a report that relies upon hardware inventory, it returns an error. For example, a BitLocker report returns an error similar to the following message:

```
Microsoft.Reporting.WinForms.ReportServerException
An error has occurred during report processing. (rsProcessingAborted)
```

You may also see the following error in the **dataldr.log** file:

`[42S22][207][Microsoft][SQL Server Native Client 11.0][SQL Server]Invalid column name 'FileTimeStamp00'. : pOFFICE_ADDIN_DATA`

Console dashboards that rely on hardware inventory may also be affected.

This issue is because of a database schema change on specific hardware inventory tables.

#### Workaround

The workaround is to drop the pre-existing attribute from the database. The dataloader site component can then create a new attribute. Run the following SQL script on the site database server to fix the table schema:

``` SQL
IF NOT EXISTS (SELECT * FROM SYS.columns WHERE name = 'FileTimestamp00' AND object_id = OBJECT_ID('OFFICE_ADDIN_DATA'))
BEGIN
       DELETE am
       FROM AttributeMap am
       INNER JOIN GroupMap gm ON am.GroupKey=gm.GroupKey
       WHERE gm.GroupClass='MICROSOFT|OFFICE_ADDIN|1.0'
       AND am.AttributeName='FileTimeStamp'

       PRINT 'Fix OFFICE_ADDIN_DATA schema'
END
```
