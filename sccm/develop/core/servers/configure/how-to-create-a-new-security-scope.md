---
title: "Create a New Security Scope"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: ccf65b5f-d1bc-4deb-babd-93dc48a9517b
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# How to Create a New Security Scope
Creating a security scope in System Center Configuration Manager is simple. All security scopes are defined by the `SMS_SecuredCategory` Windows Management Instrumentation (WMI) class. Only two properties are required when you are creating a new security scope, the name and description.  

### To create a new security scope  

1.  Set up a connection to the SMS Provider.  

2.  Create an instance of the `SMS_SecuredCategory` WMI class  

3.  Set the `CategoryName` and `CategoryDescription` properties.  

4.  Save the security scope.  

## Example  
 The following example creates a new security scope:  

```vbs  
Sub CreateSecurityScope(connection, scopeName, scopeDescription)  

    Dim scope  

    ' Create a new security scope instance.  
    Set scope = connection.Get("SMS_SecuredCategory").SpawnInstance_()  

    ' Set the required properties.  
    scope.CategoryName = scopeName    scope.CategoryDescription = scopeDescription  

    ' Save the security scope.  
    scope.Put_  

End Sub  
```  

```c#  
public void CreateSecurityScope(WqlConnectionManager connection, string scopeName, string scopeDescription)  
{  
    // Create a new security scope instance.  
    IResultObject secScope = connection.CreateInstance("SMS_SecuredCategory");  

    // Set the required properties.  
    secScope.Properties["CategoryName"].StringValue = scopeName;  
    secScope.Properties["CategoryDescription"].StringValue = scopeDescription;  

    // Save the security scope.  
    secScope.Put();  
}  
```  

 The example method has the following parameters:  

||||  
|-|-|-|  
|Parameter|Type|Description|  
|`connection`|-   Managed: `WqlConnectionManager`<br />-   VBScript: [SWbemServices](https://msdn.microsoft.com/library/aa393854.aspx)|A valid connection to the SMS Provider.|  
|`scopeName`|`String`|The name of security scope.|  
|`scopeDescription`|`String`|The description of security scope.|  

## Compiling the Code  
 The C# example requires:  

### Namespaces  
 Microsoft.ConfigurationManagement.ManagementProvider  

 Microsoft.ConfigurationManagement.ManagementProvider.WqlQueryEngine  

### Assembly  
 adminui.wqlqueryengine  

 microsoft.configurationmanagement.managementprovider  

## Robust Programming  
 For more information about error handling, see [About Configuration Manager Errors](../../../../develop/core/understand/about-configuration-manager-errors.md).  

## See Also  
 [Security Scope Management](../../../../develop/core/servers/configure/security-scope-management.md)   
 [How to Delete a Security Scope](../../../../develop/core/servers/configure/how-to-delete-a-security-scope.md)   
 [How to Associate an Object with a Security Scope](../../../../develop/core/servers/configure/how-to-associate-an-object-with-a-security-scope.md)   
 [How to Remove an Object Association with a Security Scope](../../../../develop/core/servers/configure/how-to-remove-an-object-association-with-a-security-scope.md)   
 [SMS_SecuredCategory Server WMI Class](../../../../develop/reference/core/servers/configure/sms_securedcategory-server-wmi-class.md)
