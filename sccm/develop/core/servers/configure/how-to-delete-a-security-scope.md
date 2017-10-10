---
title: "Delete a Security Scope"
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
ms.assetid: 87238a9a-7f58-4d27-92a2-569c37387decsearchScope: - ConfigMgr SDK
caps.latest.revision: 10
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# How to Delete a Security Scope
The following example shows how to delete a security scope in System Center Configuration Manager by using the `SMS_SecuredCategory` class.  

### To delete a security scope  

1.  Set up a connection to the SMS Provider.  

2.  Load the existing security scope by using the `SMS_SecuredCategory` WMI class  

3.  Delete the security scope by using the delete method.  

## Example  
 The following example deletes a security scope by identifier:  

```vbs  
Sub DeleteSecurityScope(connection, scopeId)  
    Dim scope  
    ' Get the existing scope by identifier.  
    Set scope = connection.Get("SMS_SecuredCategory.CategoryID='" & scopeId & "'")  

    ' Make sure we are allowed to delete this scope.  
    If (scope.IsBuiltIn) Then  
        Err.Raise 1, "DeleteSecurityScope", "Deleting a built-in security scope is not allowed."  
    Else  
        scope.Delete_  
    End If  
End Sub  
```  

```c#  
public void DeleteSecurityScope(WqlConnectionManager connection, string scopeId)  
{  
    // Get the existing scope by identifier.  
    IResultObject secScope = connection.GetInstance("SMS_SecuredCategory.CategoryID='" + scopeId + "'");  

    // Make sure we are allowed to delete this scope.  
    if (secScope.Properties["IsBuiltIn"].BooleanValue == true)  
        throw new System.Exception("Deleting a built-in security scope is not allowed.");  
    else  
        secScope.Delete();  
}  
```  

 The example method has the following parameters:  

||||  
|-|-|-|  
|Parameter|Type|Description|  
|`connection`|-   Managed: `WqlConnectionManager`<br />-   VBScript: [SWbemServices](https://msdn.microsoft.com/library/aa393854.aspx)|A valid connection to the SMS Provider.|  
|`scopeId`|`String`|The identifier of the security scope to delete.|  

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
 [How to Create a New Security Scope](../../../../develop/core/servers/configure/how-to-create-a-new-security-scope.md)   
 [How to Associate an Object with a Security Scope](../../../../develop/core/servers/configure/how-to-associate-an-object-with-a-security-scope.md)   
 [How to Remove an Object Association with a Security Scope](../../../../develop/core/servers/configure/how-to-remove-an-object-association-with-a-security-scope.md)   
 [SMS_SecuredCategory Server WMI Class](../../../../develop/reference/core/servers/configure/sms_securedcategory-server-wmi-class.md)
