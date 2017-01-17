---
title: "Create queries | Microsoft Docs"
description: "Discover how to create and import queries in System Center Configuration Manager. Includes example queries and tips."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 868049d3-3209-47ec-b34a-9cc26941893a
caps.latest.revision: 5
caps.handback.revision: 0
author: robstackmsftms.author: robstackmanager: angrobe

---
# How to create queries in System Center Configuration Manager*Applies to: System Center Configuration Manager (Current Branch)*
You can use this topic to help you create or import queries in System Center Configuration Manager.  

##  <a name="BKMK_Create"></a> How to create queries  
 Use this procedure to help you create queries in Configuration Manager.  

#### To create a query  

1.  In the Configuration Manager console, choose **Monitoring**.  

2.  In the **Monitoring** workspace, choose **Queries**. Then, on the **Home** tab, in the **Create** group, choose **Create Query**.  

3.  On the **General** tab of the **Create Query Wizard**, specify a unique name and an optional comment for the query.  

4.  If you want to import an existing query to use as a basis for the new query, choose **Import Query Statement**. In the **Browse Query** dialog box, select an existing query that you want to import, and then choose **OK**.  

5.  In the **Object Type** list, select the type of object that you want the query to return. The following table describes some examples of the type of object you can search for:  

    |Object type|Description|  
    |-----------------|-----------------|  
    |**System Resource**|Use to search for typical system attributes, such as the NetBIOS name of a device, the client version, the client IP address, and Active Directory Domain Services information.|  
    |**User Resource**|Use to search for typical user information, such as user names, user group names, and security group names.|  
    |**Deployment**|Use to search for typical attributes of a deployment, such as the deployment name, the schedule, and the collection that it was deployed to.|  

6.  Choose **Edit Query Statement** to open the *&lt;Query Name\>* **Statement Properties** dialog box.  

7.  On the **General** tab in the *&lt;Query Name\>* **Statement Properties** dialog box, specify the attributes that this query returns and how they are to be displayed. Choose the **New** icon to add a new attribute. You can also choose **Show Query Language** to enter or edit the query directly in WMI Query Language (WQL). For examples of WMI queries, see the [Example WQL queries](#BKMK_Example) section in this topic.  

    > [!TIP]  
    > You can use the following MSDN reference documentation to help you construct your own WQL queries:  
    >   
    > -   [WQL (SQL for WMI)](http://go.microsoft.com/fwlink/p/?LinkId=256653)  
    > -   [WHERE Clause](http://go.microsoft.com/fwlink/p/?LinkId=256654)  
    > -   [WQL Operators](http://go.microsoft.com/fwlink/p/?LinkId=256655)  

8.  On the **Criteria** tab of the *&lt;Query Name\>* **Statement Properties** dialog box, specify criteria that are used to refine the results of the query. For example, you could return only resources that have a site code of **XYZ** in the query results. You can configure multiple criteria for a query.  

    > [!IMPORTANT]  
    > If you create a query that contains no criteria, the query will return all devices in the **All Systems** collection.  

9. On the **Joins** tab in the *&lt;Query Name\>* **Statement Properties** dialog box, you can combine data from two different attributes into your query results. Although Configuration Manager automatically creates query joins when you choose different attributes for your query result, the **Joins** tab provides more advanced options. The attribute classes that System Center 2012 Configuration Manager supports are shown in the following table:  

    |Join type|Description|  
    |---------------|-----------------|  
    |Inner|Displays only matching results—always used by joins that are created automatically.|  
    |Left|Displays all results for the base attribute and only the matching results for the join attribute.|  
    |Right|Displays all the results for the join attribute and only the matching results for the base attribute.|  
    |Full|Displays all the results for both the base attribute and the join attribute.|  

     For more information about how to use join operations, see your SQL Server documentation.  

10. Choose **OK** to close the *&lt;Query Name\>* **Statement Properties** dialog box.  

11. On the **General** tab of the **Create Query Wizard**, specify whether the results of this query aren't limited to the members of a collection, whether they are limited to the members of a specified collection, or whether there is a prompt for a collection each time the query is run.  

12. Complete the wizard to create the query. The new query is displayed in the **Queries** node in the **Monitoring** workspace.  

##  <a name="BKMK_Import"></a> How to import queries  
 Use this procedure to help you import a query into Configuration Manager. For information about how to export queries, see [How to manage queries in System Center Configuration Manager](../../../core/servers/manage/manage-queries.md).  

#### To import a query  

1.  In the Configuration Manager console, choose **Monitoring**.  

2.  In the **Monitoring** workspace, choose **Queries**. On the **Home** tab, in the **Create** group, choose **Import Objects**.  

3.  On the **MOF File Name** page of the **Import Objects Wizard**, choose **Browse** to select the Managed Object Format (MOF) file that contains the query that you want to import.  

4.  Review information about the query to be imported and then complete the wizard. The new query is displayed on the **Queries** node in the **Monitoring** workspace.  

##  <a name="BKMK_Example"></a> Example WQL queries

This section contains example WMI queries that you can use in your hierarchy or modify for other purposes. To use these queries, choose **Show Query Language** in the **Query Statement Properties** dialog box. Then, copy and paste the query into the **Query Statement** field.  

> [!TIP]  
> Use the wildcard character `%` to signify any string of characters. For example, `%Visio%` returns Microsoft Office Visio 2010.  

### Computers that run Windows 7

Use the following query to return the NetBIOS name and operating system version of all computers that run Windows 7.  

> [!TIP]  
> To return computers that run Windows Server 2008 R2, change `%Workstation 6.1%` to `%Server 6.1%`.  

```  
select SMS_R_System.NetbiosName,  
SMS_R_System.OperatingSystemNameandVersion from    
SMS_R_System where   
SMS_R_System.OperatingSystemNameandVersion like "%Workstation 6.1%"  
```  

### Computers with a specific software package installed  

Use the following query to return the NetBIOS name and software package name of all computers that have a specific software package installed. This example displays all computers with a version of Microsoft Visio installed. Replace `%Visio%` with the software package that you want to query for.  

> [!TIP]  
> This query searches for the software package by using the names that are displayed in the programs list in Windows Control Panel.  

```  
select SMS_R_System.NetbiosName,   
SMS_G_System_ADD_REMOVE_PROGRAMS.DisplayName from    
SMS_R_System inner join SMS_G_System_ADD_REMOVE_PROGRAMS on   
SMS_G_System_ADD_REMOVE_PROGRAMS.ResourceId =   
SMS_R_System.ResourceId where   
SMS_G_System_ADD_REMOVE_PROGRAMS.DisplayName like "%Visio%"  
```  

### Computers that are in a specific Active Directory Domain Services organizational unit

Use the following query to return the NetBIOS name and organizational unit (OU) name of all computers in a specified OU. Replace the text `OU Name` with the name of the OU that you want to query for.  

```  
select SMS_R_System.NetbiosName,   
SMS_R_System.SystemOUName from    
SMS_R_System where   
SMS_R_System.SystemOUName = "OU Name"  
```  

### Computers with a specific NetBIOS name

Use the following query to return the NetBIOS name of all computers that begin with a specific string of characters. In this example, the query returns all computers with a NetBIOS name that begins with `ABC`.  

```  
select SMS_R_System.NetbiosName from    
SMS_R_System where SMS_R_System.NetbiosName like "ABC%"  
```  

###  <a name="BKMK_DeviceType"></a> Devices of a specific type

Device types are stored in the Configuration Manager database under the resource class **sms_r_system** and the attribute name **AgentEdition**. Use the following query to retrieve only the devices that match the agent edition of the device type that you specify:  

```  
Select SMS_R_System.ClientEdition from SMS_R_System where SMS_R_System.ClientEdition = <Device ID>  
```  

Use one of the following values for *&lt;Device ID\>*:  

|Device type|Value of AgentEdition|  
|-----------------|---------------------------|  
|Windows desktop or laptop computer|0|  
|Windows ARM-based device (running Windows RT)|1|  
|Windows Mobile 6.5|2|  
|Nokia Symbian|3|  
|Windows Phone|4|  
|Mac computer|5|  
|Windows CE|6|  
|Windows Embedded|7|  
|iOS|8|  
|iPad|9|  
|iPod Touch|10|  
|Android|11|  
|Intel System-on-a-Chip|12|  
|Unix and Linux servers|13|  

 For example, if you want the query to return only Mac computers, use the following query:  

```  
Select SMS_R_System.ClientEdition from SMS_R_System where SMS_R_System.ClientEdition = 5  
```  

## See also  
 [Operations and maintenance for queries in System Center Configuration Manager](../../../core/servers/manage/operations-and-maintenance-for-queries.md)
