---
title: Check if a User Has Permissions for an Object
titleSuffix: Configuration Manager
description: In Configuration Manager, you can check for object permissions using the UserHasPermissions Method in Class SMS_RbacSecuredObject.
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: how-to
ms.assetid: c249e680-0275-4d8a-a3f5-39643b40a8b7
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# How to Check if a User Has Permissions for an Object
In Configuration Manager, you can check for object permissions using the [UserHasPermissions Method in Class SMS_RbacSecuredObject](../../../../develop/reference/core/servers/configure/userhaspermissions-method-in-class-sms_rbacsecuredobject.md).  

### To check if a user has permissions for an object  

1.  Create a dictionary object to pass object name and permissions to check for to the [UserHasPermissions Method in Class SMS_RbacSecuredObject](../../../../develop/reference/core/servers/configure/userhaspermissions-method-in-class-sms_rbacsecuredobject.md).  

2.  Call the [UserHasPermissions Method in Class SMS_RbacSecuredObject](../../../../develop/reference/core/servers/configure/userhaspermissions-method-in-class-sms_rbacsecuredobject.md), passing in the dictionary object.  

3.  The method returns `true`, if the user has the permissions.  

## Example  
 The following example checks to see if the user has the indicated permissions:  

```c#  
public static bool UserHasPermissions(ConnectionManagerBase connectionManager, string objectName, int permissions, out int currentPermissions)  
{  
    if (connectionManager == null)  
    {  
        throw new ArgumentNullException("connectionManager");  
    }  
    if (string.IsNullOrEmpty(objectName) == true)  
    {  
        throw new ArgumentException("The parameter 'objectName' cannot be null or an empty string", "objectName");  
    }  
    IResultObject outParams = null;  
    try  
    {  
        Dictionary<string, object> inParams = new Dictionary<string, object>();  
        inParams["ObjectPath"] = objectName;  
        inParams["Permissions"] = permissions;  
        outParams = connectionManager.ExecuteMethod("SMS_RbacSecuredObject", "UserHasPermissions", inParams);  
       if (outParams != null)  
       {  
            currentPermissions = outParams["Permissions"].IntegerValue;  
            return outParams["ReturnValue"].BooleanValue;  
       }  
    }  
    finally  
    {  
        if (outParams != null)  
        {  
            outParams.Dispose();  
        }  
    }  
    currentPermissions = 0;  
    return false;  
}  

```  

 The example method has the following parameters:  

| Parameter | Type | Description |
| --------- | ---- | ----------- |
|`connectionManager`|-   Managed: `connectionManager`|A valid connection to the SMS Provider.|  
|`objectName`|`String`|Name of the object.|  
|permissions|Integer|The permissions.|  
|currentPermissions|Integer|The current permissions.|  

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
