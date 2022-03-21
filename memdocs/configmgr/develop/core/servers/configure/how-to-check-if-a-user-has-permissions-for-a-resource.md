---
title: "Check if a User Has Permissions for a Resource"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: how-to
ms.assetid: 648585e5-c6e8-465b-aefe-d3f9cf7091a9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# How to Check if a User Has Permissions for a Resource
In Configuration Manager, you can check whether a user has permission for a resource using the `GetCollectionsWithResourcePermissions` method in the `SMS_RbacSecuredObject` class.  

### To check if a user has permissions for a resource  

1.  Create a dictionary object to pass object name and permissions to check for to the [GetCollectionsWithResourcePermissions Method in Class SMS_RbacSecuredObject](../../../../develop/reference/core/servers/configure/getcollectionswithresourcepermissions-method-in-class-sms_rbacsecuredobject.md).  

2.  Call the [GetCollectionsWithResourcePermissions Method in Class SMS_RbacSecuredObject](../../../../develop/reference/core/servers/configure/getcollectionswithresourcepermissions-method-in-class-sms_rbacsecuredobject.md), passing in the dictionary object.  

3.  The method returns `true`, if the user has the permissions.  

## Example  
 The following example checks to see if the user has resource permissions.  

```c#  
public bool CheckUserPermissions(ConnectionManagerBase connectionManager, string resourceID)  
{  
    bool result = false;  
    int iId = 0;  
    IResultObject outParams = null;  
    if (int.TryParse(resourceID, out iId) == false)  
    {  
        throw new ArgumentException("Invalid resource ID");  
    }  
    //ControlAMT permissions.  
    int controlAMT = 0x1000000;  
    try  
    {  
        Dictionary<string, object> inParams = new Dictionary<string, object>();  
        inParams["Permissions"] = controlAMT;  
        inParams["ResourceID"] = iId;  
        outParams = connectionManager.ExecuteMethod("SMS_RbacSecuredObject", "GetCollectionsWithResourcePermissions", inParams);  
        if (outParams != null)  
        {  
            //If the return value equals 0 and the array is not empty, the user has the resource permissions.  
            if (outParams["ReturnValue"].IntegerValue == 0 && outParams["CollectionIDs"].StringArrayValue.Length != 0)  
            {  
                result = true;  
            }  
        }  
    }  
    finally  
    {  
        if (outParams != null)  
        {  
             outParams.Dispose();  
        }  
    }  
    return result;  
}  

```  

 The example method has the following parameters:  

| Parameter | Type | Description |
| --------- | ---- | ----------- |
|`connection`|-   Managed: `connectionManager`|A valid connection to the SMS Provider.|  
|`resourceID`|`String`|Unique ID, supplied by Configuration Manager, for the resource.|  

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
