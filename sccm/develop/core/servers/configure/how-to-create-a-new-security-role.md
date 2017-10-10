---
title: "Create a New Security Role"
titleSuffix: "Configuration Manager"
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
ms.assetid: a97841c0-5cab-4a84-a480-3a2eb60d706asearchScope: - ConfigMgr SDK
caps.latest.revision: 6
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# How to Create a New Security Role
The administrative assignments for a user or security group are defined by the roles and security scopes assigned to that user or security group. The Windows Management Instrumentation (WMI)`SMS_Admin` class contains all the administrators defined in Configuration Manager. The security roles for an admin are in the `SMS_Admin.Roles` property and the security scopes for an admin are in the `SMS_Admin.Categories` property. Both of these properties expose an array of strings which correspond to the identifier of the role or security scope. Both properties are also marked as `lazy` and are read-only.  

> [!IMPORTANT]
>  `Lazy` properties are never retrieved with the class instance if the class instance was loaded from a query. The object must be directly accessed from WMI. Generally the WMI provider will supply a `Get` method that will accept a query path to the object.  

### To create a new Security Role  

1.  Set up a connection to the SMS Provider.  

2.  Create an instance of the `SMS_Role` WMI class.  

3.  Set the required properties, including a new role name and the original security role to copy.  

4.  Get an instance of the original `SMS_Role` WMI class.  

5.  Copy the role permissions from the original security role to the new security role. This is similar to the Admin Console functionality when creating a new security role and not strictly required to create the security role.  

6.  Save the new security role.  

## Example  
 The following example creates a new security role:  

```c#  
public void CreateRole(WqlConnectionManager connection, string roleName, string originalRoleID)  
{  
    // Create a new security role instance.  
    IResultObject newRole = connection.CreateInstance("SMS_Role");  

    // Set the required properties.  
    // Note: RoleDescription is not required, but convenient.  
    newRole.Properties["RoleName"].StringValue = roleName;  
    newRole.Properties["CopiedFromID"].StringValue = originalRoleID;  
    newRole.Properties["RoleDescription"].StringValue = roleName + " Description";  

    // Get the original role instance.  
    IResultObject originalRole = connection.GetInstance(@"SMS_Role.RoleID='" + originalRoleID + "'");  

    // Copy the original role permissions to the new security role.  
    newRole.SetArrayItems("Operations", originalRole.GetArrayItems("Operations"));  

    // Save the new security role.  
    newRole.Put();  
}  

```  

 The example method has the following parameters:  

||||  
|-|-|-|  
|Parameter|Type|Description|  
|`connection`|-   Managed: `WqlConnectionManager`|A valid connection to the SMS Provider.|  
|roleName|-   Managed: `String`|A name for the new role.|  
|`originalRoleID`|-   Managed: `String`|The identifier of the original security role.|  

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
