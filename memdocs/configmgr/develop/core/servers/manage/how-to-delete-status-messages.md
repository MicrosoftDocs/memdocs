---
title: Delete Status Messages
titleSuffix: Configuration Manager
description: In Configuration Manager, you delete status messages by calling the SMS_StatusMessage class DeleteByID method and supplying an array of status message RecordID identifiers.
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: how-to
ms.assetid: 883d80f4-a623-4d5e-9b98-84f62f068205
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# How to Delete Status Messages
In Configuration Manager, you delete status messages by calling the `SMS_StatusMessage` class `DeleteByID` method and supplying an array of status message `RecordID` identifiers. Alternatively, you can call the `SMS_StatusMessage` class `DeleteByQuery` method and supply a WQL query that identifies the status messages to be deleted.  

### To delete a status message  

1.  Set up a connection to the SMS Provider. For more information, see [SMS Provider fundamentals](../../understand/sms-provider-fundamentals.md).  

2.  Call the `SMS_StatusMessage` class `DeleteByID` method with an array of record identifiers for the status messages to be deleted.  

## Example  
 The following example deletes a single status message identified by the `recordId` identifier.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../../../develop/core/understand/calling-code-snippets.md).  

```vbs  
Sub DeleteStatusMessage(connection, recordId)  

    Dim inParams  
    Dim outParams  
    Dim statusMessageClass  

    On Error Resume Next  

    ' Obtain the class definition object of a SMS_StatusMessage object.  
    Set statusMessageClass = connection.Get("SMS_StatusMessage")  

    If Err.Number<>0 Then  
        Wscript.Echo "Couldn't get status message class"  
        Exit Sub  
    End If  

    ' Set up the in parameter.  
    Set inParams = statusMessageClass.Methods_("DeleteByID").InParameters.SpawnInstance_  
    inParams.RecordIDs = Array(recordId)  
    If Err.Number<>0 Then  
        Wscript.Echo "Couldn't get in parameters object"  
        Exit Sub  
    End If  

    ' Call the method.  
    Set outParams = _  
        connection.ExecMethod( "SMS_StatusMessage", "DeleteByID", inParams)  
    If Err.Number<>0 Then  
        Wscript.Echo "Couldn't run method"  
        Exit Sub  
    End If  

    WScript.Echo CStr(outParams.ReturnValue) + " record(s) deleted"  

  End Sub  
```  

```c#  
public void DeleteStatusMessage(WqlConnectionManager connection, Int64 recordId)  
{  
    try  
    {  
        Dictionary<string, object> StatusMessageParameters = new Dictionary<string, object>();  

         // Add the parameters.  
        StatusMessageParameters.Add("RecordIDs", new Int64[] { recordId });  

        // Call the method.  
        IResultObject result = connection.ExecuteMethod("SMS_StatusMessage", "DeleteByID", StatusMessageParameters);  

        Console.WriteLine (result["ReturnValue"].IntegerValue + " record(s) deleted");  

   }  
    catch (SmsException ex)  
    {  
        Console.WriteLine("Failed to delete error message: ", ex.Message);  
        throw;  
    }  
}  

```  

 The example method has the following parameters:  

|Parameter|Type|Description|  
|---------------|----------|-----------------|  
|`Connection`|-   Managed: [WqlConnectionManager](../../understand/managed-sms-provider-fundamentals-in-configuration-manager.md#wqlconnectionmanager)<br />-   VBScript: [SWbemServices](/windows/win32/wmisdk/swbemservices)|A valid connection to the SMS Provider. For more information, see [SMS Provider fundamentals](../../understand/sms-provider-fundamentals.md).|  
|`recordId`|-   Managed: `Integer`<br />-   VBScript: `Integer`|The status message identifier. This is `SMS_StatusMessage` object `RecordID` property for the status message to be deleted.|  

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
 [How to Report User-Defined Status Messages Using WMI](../../../../develop/core/servers/manage/how-to-report-user-defined-status-messages.md)
