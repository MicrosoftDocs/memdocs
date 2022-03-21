---
title: "Enumerate Administrative Assignments"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: how-to
ms.assetid: e1d7ac85-f3ab-4b9f-9017-9a7b5769b365
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# How to Enumerate the Administrative Assignments for a User or Security Group
The administrative assignments for a user or security group are defined by the roles and security scopes assigned to that user or security group. The Windows Management Instrumentation (WMI) `SMS_Admin` class contains all the administrators defined in Configuration Manager. The security roles for an admin are in the `SMS_Admin.Roles` property and the security scopes for an admin are in the `SMS_Admin.Categories` property. Both of these properties expose an array of strings which correspond to the identifier of the role or security scope. Both properties are also marked as `lazy` and are read-only.  

> [!IMPORTANT]
>  `Lazy` properties are never retrieved with the class instance if the class instance was loaded from a query. The object must be directly accessed from WMI. Generally the WMI provider will supply a `Get` method that will accept a query path to the object.  

 To determine whether an administrator references a user account or a security group, check the `SMS_Admin.AccountType` property. This property value will be one or zero. Zero means that the account is a user, and one means the account is a security group.  

### To read the roles and security scopes of an administrator  

1.  Set up a connection to the SMS Provider.  

2.  Get an instance to a `SMS_Admin` WMI class that matches the desired administrator by using their identifier.  

3.  Read the `Roles` and `Categories` properties.  

## Example  
 The following example pulls an admin directly from WMI and displays the role and security scope identifiers:  

```vbs  
Sub PrintAdminScopesAndRoles(connection, adminId)  
    Dim admin  
    Dim item  
    On Error Resume Next  
    set admin = Nothing  
    Set admin = connection.Get("SMS_Admin.AdminID=" & CStr(adminId))  
    On Error Goto 0  
    If (Not admin Is Nothing) Then  
        WScript.Echo "Reading Admin: " + admin.LogonName  
        WScript.Echo ""  
        WScript.Echo " == Roles (" + CStr(UBound(admin.Roles) + 1) + ") =="  
        For Each item In admin.Roles  
            WScript.Echo " = " + item  
        Next  
        WScript.Echo ""  
        WScript.Echo " == Security Scopes (" + CStr(UBound(admin.Categories) + 1) + ") =="  
        For Each item In admin.Categories  
            WScript.Echo " = " + item  
        Next  
    Else  
        WScript.Echo "Admin with id " + CStr(adminId) + " not found."  
    End If  
End Sub  

```  

```c#  
public void PrintAdminScopesAndRoles(WqlConnectionManager connection, int adminId)  
{  
    IResultObject admin = null;  
    try  
    {  
        admin = connection.GetInstance("SMS_Admin.AdminID=" + adminId.ToString());  
    }  
    catch (Exception) { }  
    if (admin != null)  
    {  
        Console.WriteLine("Reading Admin: " + admin["LogonName"].StringValue);  
        Console.WriteLine("");  
        Console.WriteLine(String.Format("== Roles ({0}) ==", admin["Roles"].StringArrayValue.Length.ToString()));  
        foreach (var item in admin["Roles"].StringArrayValue)            Console.WriteLine("= " + item);  
            Console.WriteLine("");  
            Console.WriteLine(String.Format("== Security Scopes ({0}) ==", admin["Categories"].StringArrayValue.Length.ToString()));  
        foreach (var item in admin["Categories"].StringArrayValue)  
            Console.WriteLine("= " + item);  
    }  
    else  
        Console.WriteLine("Admin with id " + adminId.ToString() + " not found.");  
}  

```  

 The example method has the following parameters:  

| Parameter | Type | Description |
| --------- | ---- | ----------- |
|`connection`|-   Managed: `WqlConnectionManager`<br />-   VBScript: [SWbemServices](/windows/win32/wmisdk/swbemservices)|A valid connection to the SMS Provider.|  
|`adminId`|`Integer`|The admin identifier.|  

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
