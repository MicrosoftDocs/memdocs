---
title: Create queries
titleSuffix: Configuration Manager
description: Discover how to create and import queries in Configuration Manager. Includes example queries and tips.
ms.date: 04/27/2021
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.author: gokarthi
author: gowdhamankarthikeyan
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# Create queries in Configuration Manager

*Applies to: Configuration Manager (current branch)*

This article describes how to create and import queries in Configuration Manager.  

##  <a name="BKMK_Create"></a> Create a query  
 Use this procedure to create a query in Configuration Manager.  

1.  In the Configuration Manager console, select **Monitoring**.  

2.  In the **Monitoring** workspace, select **Queries**. On the **Home** tab, in the **Create** group, select **Create Query**.  

3.  On the **General** tab of the **Create Query Wizard**, specify a unique name and, optionally, a comment for the query.  

4.  If you want to import an existing query to use as a basis for the new query, select **Import Query Statement**. In the **Browse Query** dialog box, select a query that you want to import, and then select **OK**.  

5.  In the **Object Type** list, select the type of object that you want the query to return. This table describes some examples of the types of objects you can search for:  

    |Object type|Description|  
    |-----------------|-----------------|  
    |**System Resource**|Use to search for typical system attributes, like the NetBIOS name of a device, the client version, the client IP address, and Active Directory Domain Services information.|  
    |**User Resource**|Use to search for typical user information, like user names, user group names, and security group names.|  
    |**Deployment**|Use to search for typical attributes of a deployment, like the deployment name, the schedule, and the collection that it was deployed to.|  

6.  Select **Edit Query Statement** to open the &lt;Query Name\> **Statement Properties** dialog box.  

7.  On the **General** tab of the &lt;Query Name\> **Statement Properties** dialog box, specify the attributes that the query returns and how they should be displayed. Select the **New** icon to add a new attribute. You can also select **Show Query Language** to enter or edit the query directly in WMI Query Language (WQL). For examples of WMI queries, see the [Example WQL queries](#BKMK_Example) section in this article.

    - You can use the following reference documentation to help you construct your own WQL queries:  
       - [WQL (SQL for WMI)](/windows/win32/wmisdk/wql-sql-for-wmi)  
       - [WHERE Clause](/windows/win32/wmisdk/where-clause)  
       - [WQL Operators](/windows/win32/wmisdk/wql-operators)  
    - Starting in Configuration Manager 2010, you can preview the results when you're creating or editing a query for collection membership. In the **Query Statement Properties**, select the green triangle to show the **Query Results Preview** window. Select **Stop** if you want to stop a long running query. <!--7380401-->

8.  On the **Criteria** tab of the &lt;Query Name\> **Statement Properties** dialog box, specify criteria that are used to refine the results of the query. For example, you could return only resources that have a site code of **XYZ**. You can configure multiple criteria for a query.  

    > [!IMPORTANT]  
    > If you create a query that contains no criteria, the query will return all devices in the **All Systems** collection.  

9. On the **Joins** tab of the &lt;Query Name\> **Statement Properties** dialog box, you can combine data from two different attributes into your query results. Although Configuration Manager automatically creates query joins when you choose different attributes for your query result, the **Joins** tab provides more advanced options. Configuration Manager supports these attribute classes:  

    |Join type|Description|  
    |---------------|-----------------|  
    |Inner|Displays only matching results. Always used by joins that are created automatically.|  
    |Left|Displays all results for the base attribute and only the matching results for the join attribute.|  
    |Right|Displays all results for the join attribute and only the matching results for the base attribute.|  
    |Full|Displays all results for both the base attribute and the join attribute.|  

     For more information about how to use join operations, see the SQL Server documentation.  

10. Select **OK** to close the &lt;Query Name\> **Statement Properties** dialog box.  

11. On the **General** tab of the **Create Query Wizard**, specify that the results of the query aren't limited to the members of a collection, that they are limited to the members of a specified collection, or that a prompt for a collection appears each time the query is run.  

12. Complete the wizard to create the query. The new query appears in the **Queries** node in the **Monitoring** workspace.  

##  <a name="BKMK_Import"></a> Import a query  
 Use this procedure to import a query into Configuration Manager. For information about how to export queries, see [How to manage queries](../../../core/servers/manage/manage-queries.md).  

1.  In the Configuration Manager console, select **Monitoring**.  

2.  In the **Monitoring** workspace, select **Queries**. On the **Home** tab, in the **Create** group, select **Import Objects**.  

3.  On the **MOF File Name** page of the **Import Objects Wizard**, select **Browse** to select the Managed Object Format (MOF) file that contains the query that you want to import.  

4.  Review the information about the query to be imported and then complete the wizard. The new query appears on the **Queries** node in the **Monitoring** workspace.  

##  <a name="BKMK_Example"></a> Example WQL queries

This section contains example WQL queries that you can use in your hierarchy or modify for other purposes. To use these queries, select **Show Query Language** in the **Query Statement Properties** dialog box. Then copy and paste the query into the **Query Statement** field.  

> [!TIP]  
> Use the wildcard character `%` to signify any string of characters. For example, `%Visio%` returns Microsoft Office Visio 2010.  

### Computers that run Windows 10

Use the following query to return the NetBIOS name and operating system version of all computers that run Windows 10.  

``` WQL
select SMS_R_System.NetbiosName,  
SMS_R_System.OperatingSystemNameandVersion from
SMS_R_System where
SMS_R_System.OperatingSystemNameandVersion like "%Workstation 10%"  
```  

### Computers with a specific software package installed  

Use the following query to return the NetBIOS name and software package name of all computers that have a specific software package installed. This example returns all computers with a version of Microsoft Visio installed. Replace `Microsoft%Visio%` with the software package that you want to query for.  

> [!TIP]  
> This query searches for the software package by using the names that are displayed in the programs list in Windows Control Panel.  

``` WQL
select SMS_R_System.NetbiosName,
SMS_G_System_ADD_REMOVE_PROGRAMS.DisplayName from
SMS_R_System inner join SMS_G_System_ADD_REMOVE_PROGRAMS on
SMS_G_System_ADD_REMOVE_PROGRAMS.ResourceId =
SMS_R_System.ResourceId where
SMS_G_System_ADD_REMOVE_PROGRAMS.DisplayName like "Microsoft%Visio%"  
```  

### Computers in a specific Active Directory Domain Services organizational unit

Use the following query to return the NetBIOS name and organizational unit (OU) name of all computers in a specified OU. Replace the text `OU Name` with the name of the OU that you want to query for.  

``` WQL
select SMS_R_System.NetbiosName,
SMS_R_System.SystemOUName from
SMS_R_System where
SMS_R_System.SystemOUName = "OU Name"  
```  

### Computers with a specific NetBIOS name

Use the following query to return the NetBIOS name of all computers that begin with a specific string of characters. In this example, the query returns all computers with a NetBIOS name that begins with `ABC`.  

``` WQL
select SMS_R_System.NetbiosName from
SMS_R_System where SMS_R_System.NetbiosName like "ABC%"  
```  

###  <a name="BKMK_DeviceType"></a> Devices of a specific type

Device types are stored in the Configuration Manager database under the resource class **sms_r_system** and the attribute name **AgentEdition**. Use this query to retrieve only the devices that match the agent edition of the device type that you specify:  

``` WQL
Select SMS_R_System.ClientEdition from SMS_R_System where SMS_R_System.ClientEdition = <Device ID>  
```  

Use one of these values for &lt;Device ID\>:  

|Device type|Value of AgentEdition|  
|-----------------|---------------------------|  
|Windows desktop or laptop computer|0|  
|Windows ARM-based device (running Windows RT)|1|  
|Windows Mobile 6.5|2|  
|Nokia Symbian|3|  
|Windows Phone|4|  
|Mac computer|5|  
|Windows Embedded|7|  
|Intel system on a chip|12|  
|Microsoft HoloLens (MDM)|15|
|Microsoft Surface Hub (MDM)|16|

> [!NOTE]
> Values that aren't listed in this table are associated with devices that are no longer supported.

<!-- old, unsupported values
|Windows CE|6|
|iOS|8|  
|iPad|9|  
|iPod touch|10|  
|Android|11|  
|Unix and Linux servers|13|  
|Apple macOS (MDM)|14|
|Android for Work|17|
 -->

For example, if you want to return only Mac computers, use this query:  

``` WQL
Select SMS_R_System.ClientEdition from SMS_R_System where SMS_R_System.ClientEdition = 5  
```  

###  <a name="bkmk_comgmt"></a> Devices that are co-managed

```WQL
select SMS_R_SYSTEM.ResourceID, SMS_R_SYSTEM.ResourceType, SMS_R_SYSTEM.Name,
SMS_R_SYSTEM.SMSUniqueIdentifier, SMS_R_SYSTEM.ResourceDomainORWorkgroup, SMS_R_SYSTEM.Client
from SMS_R_System
inner join SMS_Client_ComanagementState on SMS_Client_ComanagementState.ResourceId = SMS_R_System.ResourceId 
where SMS_Client_ComanagementState.ComgmtPolicyPresent = 1 AND SMS_Client_ComanagementState.MDMEnrolled = 1 AND MDMProvisioned = 1
```

## Next steps

[How to manage queries](manage-queries.md)
