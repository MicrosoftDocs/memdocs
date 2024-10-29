---
title: Create a New Administrator
titleSuffix: Configuration Manager
description: Learn how administrative assignments for a user or security group are defined by the roles and security scopes assigned to that user or security group.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: how-to
ms.assetid: b7749c61-a744-4824-b36b-6ed957d30eb3
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# How to Create a New Administrator
The administrative assignments for a user or security group are defined by the roles and security scopes assigned to that user or security group. The Windows Management Instrumentation (WMI) `SMS_Admin` class contains all the administrators defined in Configuration Manager. The security roles for an admin are in the `SMS_Admin.Roles` property and the security scopes for an admin are in the `SMS_Admin.Categories` property. Both of these properties expose an array of strings which correspond to the identifier of the role or security scope. Both properties are also marked as `lazy` and are read-only.  

> [!IMPORTANT]
>  `Lazy` properties are never retrieved with the class instance if the class instance was loaded from a query. The object must be directly accessed from WMI. Generally the WMI provider will supply a `Get` method that will accept a query path to the object.  

### To create a new administrator  

1.  Set up a connection to the SMS Provider.  

2.  Get an instance to a `SMS_Admin` WMI class that matches the desired administrator by using their identifier.  

3.  Add permissions, including category, role and secured scope.  

    > [!IMPORTANT]
    >  Category, role and secured scope are all required values.  

4.  Save the new administrator instance.  

## Example  
 The following example pulls an admin directly from WMI and displays the role and security scope identifiers:  

```c#  
public void CreateSMSAdmin(WqlConnectionManager connection, string distinguishedName, string categoryID, string roleID, int categoryTypeID)  
 {  
     // Create a new administrator instance.  
     IResultObject newSMSAdmin = connection.CreateInstance("SMS_Admin");  

     // Set the required properties.  
     // One set of example values in comments.  
    newSMSAdmin.Properties["DistinguishedName"].StringValue = distinguishedName; // "CN=<USERACCOUNT>,CN=Users,DC=<DOMAINNAME>,DC=COM"  

    // Create new permissions list.  
    List<IResultObject> permissionsObjectList = new List<IResultObject>();  

    // Add permissions.  
    IResultObject permissionObject = connection.CreateEmbeddedObjectInstance("SMS_APermission");  
    permissionObject["CategoryID"].StringValue = categoryID;             // "SMS00004" (All Users and User Groups)  
    permissionObject["RoleID"].StringValue = roleID;                     // "SMS000GR" (EndPoint Protection Manager)  
    permissionObject["CategoryTypeID"].IntegerValue = categoryTypeID;    // 1          (Collection)  
    permissionsObjectList.Add(permissionObject);  

    // Add secured scope.  
    IResultObject permissionObject2 = connection.CreateEmbeddedObjectInstance("SMS_APermission");  
    permissionObject2["CategoryID"].StringValue = "SMS00UNA";             // "SMS00UNA" (Default)  
    permissionObject2["RoleID"].StringValue = "SMS000GR";                 // "SMS000GR" (EndPoint Protection Manager)  
    permissionObject2["CategoryTypeID"].IntegerValue = 29;                // 29         (Secured Scope)  
    permissionsObjectList.Add(permissionObject2);  

    // Save the permissions list to the new administrator instance.  
     newSMSAdmin.SetArrayItems("Permissions", permissionsObjectList);  

    // Save the new administrator instance.  
     newSMSAdmin.Put();  
}  
```  

 The example method has the following parameters:  

| Parameter | Type | Description |
| --------- | ---- | ----------- |
|`connection`|-   Managed: `WqlConnectionManager`|A valid connection to the SMS Provider.|  
|`distinguishedName`|-   Managed: `String`|Like "CN=John Doe,OU=UserAccounts,DC=contoso,DC=com"|  
|`categoryID`|-   Managed: `String`|The RBA secured categories associated with this account.|  
|`CategoryTypeID`|-   Managed: `Integer`|The type of the category (collection or secured scope).|  

## Compiling the Code  
 The C# example requires:  

### Namespaces  
 Microsoft.ConfigurationManagement.ManagementProvider  

 Microsoft.ConfigurationManagement.ManagementProvider.WqlQueryEngine  

 System  

### Assembly  
 adminui.wqlqueryengine  

 microsoft.configurationmanagement.managementprovider  

 mscorlib  

## Robust Programming  
 For more information about error handling, see [About Configuration Manager Errors](../../../../develop/core/understand/about-configuration-manager-errors.md).  

## See Also  
 [SMS_Admin Server WMI Class](../../../../develop/reference/core/servers/configure/sms_admin-server-wmi-class.md)   
 [SMS_Role Server WMI Class](../../../../develop/reference/core/servers/configure/sms_role-server-wmi-class.md)   
 [SMS_SecuredCategory Server WMI Class](../../../../develop/reference/core/servers/configure/sms_securedcategory-server-wmi-class.md)
