---
title: "Add a Context Qualifier by Using WMI"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: how-to
ms.assetid: 7e6d8d4e-2454-40a3-9df7-649681f47dfe
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# How to Add a Configuration Manager Context Qualifier by Using WMI
In Configuration Manager, you add context qualifiers to a connection ([SWbemServices](/windows/win32/wmisdk/swbemservices)) or object ([SWbemObject](/windows/win32/wmisdk/swbemobject)) by creating a [SWbemNamedValueSet](/windows/win32/wmisdk/swbemnamedvalueset) value set to hold the context qualifiers. You then provide the [SWbemNamedValueSet](/windows/win32/wmisdk/swbemnamedvalueset) value set as a parameter to connection and object methods.  

 in Configuration Manager, you can provide your application name (ApplicationName), computer name (MachineName) and locale identifier (LocaleID).  

 In most cases, context qualifiers are not required. The main exception is accessing the site control file where they are needed to set up session information. For more information, see [About the Configuration Manager Site Control File](../../../develop/core/understand/about-the-configuration-manager-site-control-file.md).  

### To add a Configuration Manager context qualifier  

1.  Set up a connection to the SMS Provider. For more information, see [SMS Provider fundamentals](sms-provider-fundamentals.md).  

2.  Create a [WbemScripting.SWbemNamedValueSet](/windows/win32/wmisdk/swbemnamedvalueset) object and add the desired context qualifiers.  

3.  Use the [SWbemNamedValue](/windows/win32/wmisdk/swbemnamedvalue) value set you created in step two to pass context qualifiers to connection and object manipulation calls.  

## Example  
 The following VBScript example creates a [SWbemNamedValueSet](/windows/win32/wmisdk/swbemnamedvalueset) value set and adds the supplied context qualifiers. The following code example demonstrates how to call the method for use in an [SMS_Package](../../../develop/reference/core/servers/configure/sms_package-server-wmi-class.md) package object **Put** method call. For more information about Configuration Manager objects, see [Objects overview](configuration-manager-objects-overview.md).  

 `Dim context`  

 `Set context = CreateContextQualifiers("My application" , "My Computer" , "MS\1033")`  

 `package.Put_ , context`  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../../develop/core/understand/calling-code-snippets.md).  

```vbs  

Function CreateContextQualifiers(applicationName, machineName, localeID)  
    On Error Resume next  
    Dim smsContext  

    set smsContext = CreateObject("WbemScripting.SWbemNamedValueSet")  

    ' Add the context qualifiers to the set.  
    smsContext.Add "LocaleID", localeID  
    smsContext.Add "MachineName", machineName  
    smsContext.Add "ApplicationName", applicationName  

    Set CreateContextQualifiers = smsContext  

      If Err.Number<>0 Then  
        WScript.Echo Err.Description  
        CreateContextQualifiers = null  
        Exit Function  
    End If  
End Function  
```  

 The example method has the following parameters:  

|Parameter|Type|Description|  
|---------------|----------|-----------------|  
|`applicationName`|-   `String`|The ApplicationName context qualifier.|  
|`machineName`|-   `String`|The computer name qualifier.|  
|`localeID`|-   `String`|The locale identifier. For example, MS\1033 is English (U.S.). If you need the locale for non-U.S. installations, you can get it from the [SMS_Identification Server WMI Class](../../../develop/reference/core/servers/configure/sms_identification-server-wmi-class.md)`LocaleID` property.|  

## Compiling the Code  
 This VBScript example requires:  

## Robust Programming  
 For more information about error handling, see [About Configuration Manager Errors](../../../develop/core/understand/about-configuration-manager-errors.md).  

## .NET Framework Security  
 For more information about securing Configuration Manager applications, see [Configuration Manager role-based administration](../../../develop/core/servers/configure/role-based-administration.md).  

## See Also  
 [About the Configuration Manager Site Control File](../../../develop/core/understand/about-the-configuration-manager-site-control-file.md)   
 [Objects overview](configuration-manager-objects-overview.md)
 [Configuration Manager Context Qualifiers](../../../develop/core/understand/context-qualifiers.md)   
 [How to Connect to an SMS Provider in Configuration Manager by Using WMI](../../../develop/core/understand/how-to-connect-to-an-sms-provider-in-configuration-manager-by-using-wmi.md)   
 [Windows Management Instrumentation](/windows/win32/wmisdk/wmi-start-page)
