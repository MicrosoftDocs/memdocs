---
description: Learn how to report user-defined informational, warning, and error status messages, on the site server using methods defined in the SMS_StatusMessage class.
title: Report User-Defined Status Messages
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: how-to
ms.assetid: c32d4de0-4d09-4c2e-ad83-d3f690a3be63
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# How to Report User-Defined Status Messages
In Configuration Manager, you can report user-defined informational, warning, and error status messages, on the site server, by using the following methods that are defined in the `SMS_StatusMessage` class:  

|Method|Description|  
|------------|-----------------|  
|`RaiseErrorStatusMsg`|Raises an error status message.|  
|`RaiseWarningStatusMsg`|Raises a warning status message.|  
|`RaiseInformationalStatusMsg`|Raises an informational status message.|  

### To report a user defined status message by using WMI  

1.  Set up a connection to the SMS Provider. For more information, see [SMS Provider fundamentals](../../understand/sms-provider-fundamentals.md).  

2.  Call the `SMS_StatusMessage` class method that is appropriate for the type of status message you want to raise.  

## Example  
 The following example raises an error message. It also defines an attribute identifier and attribute values for a package. For more information about attributes, see [SMS_StatMsgAttributes Server WMI Class](../../../../develop/reference/core/servers/manage/sms_statmsgattributes-server-wmi-class.md).  

 In the example, the `LocaleID` property is hard-coded to English (U.S.). If you need the locale for non-U.S. installations, you can get it from the [SMS_Identification Server WMI Class](../../../../develop/reference/core/servers/configure/sms_identification-server-wmi-class.md)`LocaleID` property.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../../../develop/core/understand/calling-code-snippets.md).  

```vbs  
Sub RaiseErrorStatusMessage(connection)  

    Dim smsContext  
    Dim statusMessageParameters  
    Dim inParams  
    Dim statusMessageClass  

    Set smsContext = CreateObject("WbemScripting.SWbemNamedValueSet")  

    ' Add the context qualifiers to the set.  
    smsContext.Add "LocaleID", "MS\1033"  
    smsContext.Add "MachineName", "MyComputerName"  
    smsContext.Add "ApplicationName", "MyApplication"  

   ' Obtain the class definition object of a SMS_Status Message object.  
    Set statusMessageClass = connection.Get("SMS_StatusMessage")  

    ' Set up the in parameter.  
    Set inParams = statusMessageClass.Methods_("RaiseErrorStatusMsg").InParameters.SpawnInstance_  
    inParams.MessageText = "This is an error message"  
    inParams.MessageType = 768  
    inParams.AttrIDs = Array(400)  
    inParams.AttrValues = Array("MyPackageID")  

    Call connection.ExecMethod( "SMS_StatusMessage", "RaiseErrorStatusMsg", inParams,,smsContext)  
    If Err.Number<>0 Then  
        Wscript.Echo "Couldn't run method"  
        Exit Sub  
    End If  

 End Sub  
```  

```c#  
public void RaiseErrorStatusMessage(WqlConnectionManager connection)  
{  
    try  
    {  
        Dictionary<string, object> StatusMessageParameters = new Dictionary<string, object>();  

        connection.Context.Add("ApplicationName", "MyApplication");  
        connection.Context.Add("MachineName", "MyComputerName");  
        connection.Context.Add("LocaleID", @"MS\1033");  

        // Add the parameters.  
        StatusMessageParameters.Add("MessageText", "This is an error message");  
        StatusMessageParameters.Add("MessageType", 768);  
        StatusMessageParameters.Add("AttrIDs", new int[] { 400 });  
        StatusMessageParameters.Add("AttrValues", new string[] { "MyPackageID" });  

        // Call the method.  
        connection.ExecuteMethod("SMS_StatusMessage", "RaiseErrorStatusMsg", StatusMessageParameters);  

    }  
    catch (SmsException ex)  
    {  
        Console.WriteLine("Failed to raise error status message: ", ex.Message);  
        throw;  
    }  
}  
```  

 The example method has the following parameters:  

|Parameter|Type|Description|  
|---------------|----------|-----------------|  
|`connection`|-   Managed: [WqlConnectionManager](../../understand/managed-sms-provider-fundamentals-in-configuration-manager.md#wqlconnectionmanager)<br />-   VBScript: [SWbemServices](/windows/win32/wmisdk/swbemservices)|A valid connection to the SMS Provider. For more information, see [SMS Provider fundamentals](../../understand/sms-provider-fundamentals.md).|  

## Compiling the Code  
 This C# example requires:  

### Namespaces  
 System  

 System.Collections.Generic  

 System.Text  

 Microsoft.ConfigurationManagement.ManagementProvider  

 Microsoft.ConfigurationManagement.ManagementProvider.WqlQueryEngine  

### Assembly  
 adminui.wqlqueryengine  

 microsoft.configurationmanagement.managementprovider  

## Robust Programming  
 For more information about error handling, see [About Configuration Manager Errors](../../../../develop/core/understand/about-configuration-manager-errors.md).  

## .NET Framework Security  
 For more information about securing Configuration Manager applications, see [Configuration Manager role-based administration](../../../../develop/core/servers/configure/role-based-administration.md).  

## See Also  
 [About status messages](about-configuration-manager-status-messages.md)
 [SMS_StatusMessage Server WMI Class](../../../../develop/reference/core/servers/manage/sms_statusmessage-server-wmi-class.md)   
 [How To Delete Status Messages](../../../../develop/core/servers/manage/how-to-delete-status-messages.md)
