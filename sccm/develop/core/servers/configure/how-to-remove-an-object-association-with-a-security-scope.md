---
title: "Remove an Object Association with a Security Scope"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: b6be1a0c-58ba-4949-a78a-d09ab322293c
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# How to Remove an Object Association with a Security Scope
Removing a security scope from an object instance is as simple as deleting the Windows Management Instrumentation (WMI)`SMS_SecuredCategoryMembership` class instance. However, object instances must have at least one security scope associated with them. The last object instance can never be removed. Every object is created with the `Default` security scope, and if all other security scopes are to be removed from an object instance, the `Default` should be added to it before removal.  

> [!IMPORTANT]
>  You must have administrative rights to the scope and the object you are removing it from. If you do not have the correct permissions, removing a scope from that object instance will fail. Removing the last scope from an object will be unsuccessful and will fail.  

> [!TIP]
>  To remove multiple objects to a scope, use the [RemoveMemberships Method in Class SMS_SecuredCategoryMembership](../../../../develop/reference/core/servers/configure/removememberships-method-in-class-sms_securedcategorymembership.md).  

### To remove a security scope from an object  

1.  Set up a connection to the SMS Provider.  

2.  Determine the object’s key property identifier.  

3.  Determine the object type identifier.  

4.  Determine the scope identifier.  

5.  Find an instance of the `SMS_SecuredCategoryMembership` WMI class that matches the .  

6.  Delete the instance.  

## Example  
 The following code example removes a scope identifier from a package:  

```vbs  
Sub RemoveObjectScope(connection, scopeId, objectKey, objectTypeId)  

    Dim assignment  

    ' Find the existing scope assignement that matches our parameters.  
    Set assignment = connection.Get("SMS_SecuredCategoryMembership.CategoryID='" & scopeId & "',ObjectKey='" & objectKey & "',ObjectTypeId=" & objectTypeId)  

    If (assignment Is Nothing) Then  
        Err.Raise 1, "RemoveObjectScope", "Unable to find matching scope, object, and object type."  
    Else  
        assignment.Delete_  
    End If  
End Sub  
```  

```c#  
public void RemoveObjectScope(WqlConnectionManager connection, string scopeId, string objectKey, int objectTypeId)  
{  
    // Find the existing scope assignement that matches our parameters.  
     IResultObject assignment = connection.GetInstance("SMS_SecuredCategoryMembership.CategoryID='" + scopeId + "',ObjectKey='" + objectKey + "',ObjectTypeID=" + objectTypeId.ToString());  

   // Make sure we found the scope.  
    if (assignment == null)  
        throw new System.Exception("Unable to find matching scope, object, and object type.");  
    else  
        assignment.Delete();  
}  
```  

 The example method has the following parameters:  

||||  
|-|-|-|  
|Parameter|Type|Description|  
|`connection`|-   Managed: `WqlConnectionManager`<br />-   VBScript: [SWbemServices](https://msdn.microsoft.com/library/aa393854.aspx)|A valid connection to the SMS Provider.|  
|`scopeId`|`String`|The identifier of the security scope.|  
|objectKey|`String`|The key property value of the object.|  
|objectTypeId|`Integer`|The type identifier of the object referenced in the `objectKey` parameter.|  

## Compiling the Code  
 The C# example requires:  

### Namespaces  
 Microsoft.ConfigurationManagement.ManagementProvider  

 Microsoft.ConfigurationManagement.ManagementProvider.WqlQueryEngine  

### Assembly  
 adminui.wqlqueryengine  

 microsoft.configurationmanagement.managementprovider  

## See Also  
 [SMS_SecuredCategoryMembership Server WMI Class](../../../../develop/reference/core/servers/configure/sms_securedcategorymembership-server-wmi-class.md)   
 [How to Create a New Security Scope](../../../../develop/core/servers/configure/how-to-create-a-new-security-scope.md)   
 [How to Delete a Security Scope](../../../../develop/core/servers/configure/how-to-delete-a-security-scope.md)   
 [How to Associate an Object with a Security Scope](../../../../develop/core/servers/configure/how-to-associate-an-object-with-a-security-scope.md)   
 [SMS_SecuredCategory Server WMI Class](../../../../develop/reference/core/servers/configure/sms_securedcategory-server-wmi-class.md)
