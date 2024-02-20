---
title: Delete a Software Metering Rule
titleSuffix: Configuration Manager
description: Delete a software metering rule by loading the instance of the rule identified by the software metering rule ID, and calling the delete method.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: how-to
ms.assetid: 26421f68-0708-4c5a-a0a3-f3a399ed9b8e
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# How to Delete a Software Metering Rule
You delete a software metering rule, in Configuration Manager, by loading the instance of the software metering rule that is identified by the software metering rule ID and calling the delete method.  

### To delete a software metering rule  

1.  Set up a connection to the SMS Provider.  

2.  Load the software metering rule object by using the [SMS_MeteredProductRule](../../develop/reference/apps/sms_meteredproductrule-server-wmi-class.md) class and a known software metering rule ID.  

3.  Delete the software metering rule by using the delete method.  

## Example  
 The following example method shows how to delete a software metering rule by loading an instance of the software metering rule that is identified by the software metering rule ID and calling the delete method.  

> [!IMPORTANT]
>  The rule ID corresponds to the value stored in the property `RuleID`. The Configuration Manager console displays a **Rule ID** column, which actually corresponds to the value stored in the property `SecurityID`.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../develop/core/understand/calling-code-snippets.md).  

```vbs  

' Delete a software metering rule.  
 Sub DeleteSWMRule(connection,                  _  
                   existingSWMRuleID)                           

    ' Get an existing software metering rule to delete.   
    Set existingSWMRule = connection.Get("SMS_MeteredProductRule.RuleID='" & existingSWMRuleID & "'")    

    ' Get file name for output.  
    fileName = existingSWMRule.FileName  

    ' Delete the software metering rule.  
    existingSWMRule.Delete_  

    ' Output a success message.  
    Wscript.Echo "Deleted SWM rule: " & existingSWMRuleID  
    Wscript.Echo "Rule name: " & fileName  

 End Sub  
```  

```c#  

public void DeleteSWMRule(WqlConnectionManager connection,  
                          string existingSWMRuleID)  
{  
    try  
    {  
        // Get the specific SWM Rule to delete.  

        IResultObject existingSWMRule = connection.GetInstance(@"SMS_MeteredProductRule.RuleID='" + existingSWMRuleID + "'");  

        // Get file name for output message.  
        string fileName = existingSWMRule["FileName"].StringValue;  

        // Delete the software metering rule.  
        existingSWMRule.Delete();  

        // Output a success message.  
        Console.WriteLine("Deleted SWM rule: " + existingSWMRuleID);  
        Console.WriteLine("Rule name: " + fileName);  
    }  

    catch (SmsException ex)  
    {  
        Console.WriteLine("Failed to delete the software metering rule. Error: " + ex.Message);  
        throw;  
    }  
}  

```  

 The example method has the following parameters:  

| Parameter | Type | Description |
| --------- | ---- | ----------- |
|`connection`|-   Managed: `WqlConnectionManager`<br />-   VBScript: [SWbemServices](/windows/win32/wmisdk/swbemservices)|A valid connection to the SMS Provider.|  
|`existingSWMRuleID`|-   Managed: `String`<br />-   VBScript: `String`|Identifies a specific software metering rule. In this case, identifies the specific software metering rule that will be deleted.|  

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
 For more information about error handling, see [About Configuration Manager Errors](../../develop/core/understand/about-configuration-manager-errors.md).  

## .NET Framework Security  
 For more information about securing Configuration Manager applications, see [Configuration Manager role-based administration](../../develop/core/servers/configure/role-based-administration.md).  

## See Also  
 [Configuration Manager Software Development Kit](../../develop/core/misc/system-center-configuration-manager-sdk.md)   
 [SMS_MeteredProductRule Server WMI Class](../../develop/reference/apps/sms_meteredproductrule-server-wmi-class.md)
