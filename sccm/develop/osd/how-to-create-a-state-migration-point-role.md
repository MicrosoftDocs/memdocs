---
title: "Create a State Migration Point Role"
ms.custom: ""
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.reviewer: ""
ms.suite: ""
ms.technology:
  - "configmgr-other"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to:
  - "System Center Configuration Manager (current branch)"
ms.assetid: dd3b2d67-edcb-44fb-9efc-72afef3896c9searchScope: - ConfigMgr SDK
caps.latest.revision: 11
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# How to Create a State Migration Point Role
You create the state migration point role, in System Center Configuration Manager, by creating an instance of [SMS_SCI_SysResUse Server WMI Class](../../develop/reference/core/servers/configure/sms_sci_sysresuse-server-wmi-class.md) and providing the property values in the following table.  

|Property|Description|  
|--------------|-----------------|  
|`RoleName`|Name of the role. For a state migration point, the value is SMS State Migration Point.|  
|`SiteCode`|The site code for the site.|  
|`NALPath`|The network abstraction layer (NAL) path to the state migration point. For more information, see [PackNALPath Method in Class SMS_NAL_Methods](../../develop/reference/misc/packnalpath-method-in-class-sms_nal_methods.md).|  
|`NALType`|The resource type. For a state migration point, this should be Windows NT Server.|  

 You will also need to set initial values for the following embedded properties and embedded property lists.  

|Name|Description|  
|----------|-----------------|  
|`Server Remote Name`|The server that has the state migration point. Embedded property.|  
|`SMPQuiesceState`|Sets the restore-only mode. For more information, see [How to Set the Restore-Only Mode for a State Migration Point](../../develop/osd/how-to-set-the-restore-only-mode-for-a-state-migration-point.md). Embedded property.|  
|`SMPStoreDeletionDelayTimeInMinutes`|Sets the deletion policy. For more information, see [How to Set the Deletion Policy for a State Migration Point](../../develop/osd/how-to-set-the-deletion-policy-for-a-state-migration-point.md). Embedded property.|  
|`SMPStoreDeletionCycleTimeInMinutes`|Sets the deletion policy. For more information, see [How to Set the Deletion Policy for a State Migration Point](../../develop/osd/how-to-set-the-deletion-policy-for-a-state-migration-point.md).|  
|`Directories`|Lists the state migration point folders. For more information, see [How to Add a State Migration Point Folder](../../develop/osd/how-to-add-a-state-migration-point-folder.md).|  

### To create a state migration point role  

1.  Set up a connection to the SMS Provider. For more information, see [About the SMS Provider in Configuration Manager](../../develop/core/understand/about-the-sms-provider-in-configuration-manager.md).  

2.  Create an instance of [SMS_SCI_SysResUse Server WMI Class](../../develop/reference/core/servers/configure/sms_sci_sysresuse-server-wmi-class.md).  

3.  Populate the properties listed above.  

4.  Commit the `SMS_SCI_SystResUse` object.  

## Example  
 The following example method creates a state migration point from the supplied site code and NAL path. Some helper functions are provided for writing the embedded properties and embedded property lists to the site control file.  

> [!IMPORTANT]
>  This example makes use of other state migration point code snippets to set various values. The methods `AddSmpFolder`, `SetRestoreOnlyMode`, `SetDeletionPolicy` are described in the below topics:  
>   
>  -   [How to Add a State Migration Point Folder](../../develop/osd/how-to-add-a-state-migration-point-folder.md)  
> -   [How to Set the Restore-Only Mode for a State Migration Point](../../develop/osd/how-to-set-the-restore-only-mode-for-a-state-migration-point.md)  
> -   [How to Set the Deletion Policy for a State Migration Point](../../develop/osd/how-to-set-the-deletion-policy-for-a-state-migration-point.md)  
>   
>  The methods `AddSmpFolder`, `SetRestoreOnlyMode`, `SetDeletionPolicy` must be included for the example to work. The methods are not included in the code snippets below.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../develop/core/understand/calling-code-snippets.md).  

```c#  
public void CreateSmpRole(  
     WqlConnectionManager connection,  
     string serverName,  
     string siteCode,  
     string nalPath)  
{  
    try  
    {  
        // Create the state migration point resource object.  
        IResultObject smpRole = connection.CreateInstance("SMS_SCI_SysResUse");  
        smpRole["RoleName"].StringValue = "SMS State Migration Point";  

        // Set the state migration point properties.  
        smpRole["SiteCode"].StringValue = siteCode;  
        smpRole["NALPath"].StringValue = nalPath;  
        smpRole["NALType"].StringValue = "Windows NT Server";  

        // Create the embedded property and property lists.  
        this.WriteScfEmbeddedProperty(smpRole, "Server Remote Name", 0, serverName, string.Empty);  
        this.WriteScfEmbeddedProperty(smpRole, "SMPQuiesceState", 1, string.Empty, string.Empty);  
        this.WriteScfEmbeddedProperty(smpRole, "SMPStoreDeletionDelayTimeInMinutes", 0, string.Empty, string.Empty);  
        this.WriteScfEmbeddedProperty(smpRole, "SMPStoreDeletionCycleTimeInMinutes", 0, string.Empty, string.Empty);  
        this.WriteScfEmbeddedPropertyList(smpRole, "Directories", null);  

        // Commit the site role.  
        smpRole.Put();  

        // Use SDK snippets to populate some values.  
        this.AddSmpFolder(connection, @"C:\temp", 100, 10, 1, serverName, siteCode);  
        this.SetRestoreOnlyMode(connection, serverName, siteCode, true);  
        this.SetDeletionPolicy(connection, serverName, siteCode, 10);  
    }  
    catch (SmsException e)  
    {  
        Console.WriteLine("Failed to create the state migration point: " + e.Message);  
        throw;  
    }  
}  
public void WriteScfEmbeddedPropertyList(  
    IResultObject resource,  
    string propertyListName,  
    string[] values  
    )  

    // Create an embedded property list for the supplied resource.  
{  
    Dictionary<string, IResultObject> EmbeddedPropertyList = resource.EmbeddedPropertyLists;  

    // Get the property list, or create it.   
    IResultObject ropl;  
    if (EmbeddedPropertyList.ContainsKey(propertyListName))  
    {  
        ropl = EmbeddedPropertyList[propertyListName];  
    }  
    else  
    {  
        ConnectionManagerBase connection = resource.ConnectionManager;  
        ropl = connection.CreateEmbeddedObjectInstance("SMS_EmbeddedPropertyList");  
        EmbeddedPropertyList.Add(propertyListName, ropl);  
    }  

    // Set the property list properties.  
    ropl["PropertyListName"].StringValue = propertyListName;  
    ropl["Values"].StringArrayValue = values;  
    resource.EmbeddedPropertyLists = EmbeddedPropertyList;  
}  

public void WriteScfEmbeddedProperty(  
    IResultObject resource,  
    string propertyName,  
    int value,  
    string value1,  
    string value2)  
{  
    // Properties  
    // Server remote name  
    Dictionary<string, IResultObject> EmbeddedProperties = resource.EmbeddedProperties;  

    // Get the property, or create it.  
    IResultObject ro;  
    if (EmbeddedProperties.ContainsKey(propertyName))  
    {  
        ro = EmbeddedProperties[propertyName];  
    }  
    else  
    {  
        ConnectionManagerBase connection = resource.ConnectionManager;  
        ro = connection.CreateEmbeddedObjectInstance("SMS_EmbeddedProperty");  
        EmbeddedProperties.Add(propertyName, ro);  
    }  

    ro["PropertyName"].StringValue = propertyName;  
    ro["Value"].IntegerValue = value;  
    ro["Value1"].StringValue = value1;  
    ro["Value2"].StringValue = value2;  

    resource.EmbeddedProperties = EmbeddedProperties;  
}  

```  

 The example method has the following parameters:  

||||  
|-|-|-|  
|Parameter|Type|Description|  
|`connection`|Managed: `WqlConnectionManager`|A valid connection to the SMS Provider.|  
|`serverName`|Managed: `String`|The Configuration Manager server that the state migration point is running on.|  
|`siteCode`|Managed: `String`|The Configuration Manager site code.|  
|`nalPath`|Managed: `String`|The NAL path to the state migration point. For example, `["Display=\\SERVERNAME\"]MSWNET:["SMS_SITE=SITECODE"]\\SERVERNAME\`|  

## Compiling the Code  
 The C# example has the following compilation requirements:  

### Namespaces  
 System  

 System.Collections.Generic  

 System.Text  

 Microsoft.ConfigurationManagement.ManagementProvider  

 Microsoft.ConfigurationManagement.ManagementProvider.WqlQueryEngine  

### Assembly  
 microsoft.configurationmanagement.managementprovider  

 adminui.wqlqueryengine  

## Robust Programming  
 For more information about error handling, see [About Configuration Manager Errors](../../develop/core/understand/about-configuration-manager-errors.md).  

## .NET Framework Security  
 For more information about securing Configuration Manager applications, see [Securing Configuration Manager Applications](../../develop/core/understand/securing-configuration-manager-applications.md).  

## See Also  
 [SMS_SCI_SysResUse Server WMI Class](../../develop/reference/core/servers/configure/sms_sci_sysresuse-server-wmi-class.md)   
 [PackNALPath Method in Class SMS_NAL_Methods](../../develop/reference/misc/packnalpath-method-in-class-sms_nal_methods.md)   
 [About Operating System Deployment Site Role Configuration](../../develop/osd/about-operating-system-deployment-site-role-configuration.md)   
 [Configuration Manager Operating System Deployment](../../develop/osd/operating-system-deployment.md)   
 [Configuration Manager Programming Fundamentals](../../develop/core/understand/configuration-manager-programming-fundamentals.md)   
 [Operating System Deployment Site Role Configuration](../../develop/osd/operating-system-deployment-site-role-configuration.md)   
 [How to Add a State Migration Point Folder](../../develop/osd/how-to-add-a-state-migration-point-folder.md)   
 [How to Set the Deletion Policy for a State Migration Point](../../develop/osd/how-to-set-the-deletion-policy-for-a-state-migration-point.md)   
 [How to Set the Restore-Only Mode for a State Migration Point](../../develop/osd/how-to-set-the-restore-only-mode-for-a-state-migration-point.md)   
 [How to Read and Write to the Configuration Manager Site Control File by Using Managed Code](../../develop/core/understand/how-to-read-and-write-to-the-site-control-file-by-using-managed-code.md)   
 [How to Read and Write to the Configuration Manager Site Control File by Using WMI](../../develop/core/understand/how-to-read-and-write-to-the-site-control-file-by-using-wmi.md)
