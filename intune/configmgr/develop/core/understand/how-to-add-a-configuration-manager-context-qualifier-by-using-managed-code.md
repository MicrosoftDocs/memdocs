---
title: Add a Context Qualifier by Using Managed Code
titleSuffix: Configuration Manager
description: To add a context qualifier by using the managed SMS Provider, use the Context property which is a Dictionary object that holds context qualifiers.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: how-to
ms.assetid: eef96176-cbf5-4163-bb81-047c22443527
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart
---
# How to Add a Configuration Manager Context Qualifier by Using Managed Code
In Configuration Manager, to add a context qualifier by using the managed SMS Provider, use the [Context](/previous-versions/system-center/developer/cc147087(v=msdn.10)) property which is a `Dictionary` object that holds context qualifiers.

 Typically you will add your application name to the ApplicationName context qualifier, along with the computer name (MachineName) and Locale identifier (LocaleID).

### To add Configuration Manager context qualifier

1.  Set up a connection to the SMS Provider. For more information, see [How to Connect to an SMS Provider in Configuration Manager by Using Managed Code](../../../develop/core/understand/how-to-connect-to-an-sms-provider-by-using-managed-code.md)

2.  Get the [SmsNamedValuesDictionary](/previous-versions/system-center/developer/cc147435(v=msdn.10)) object from the *WqlConnectionManager* object that you get from step 1.

3.  Add the context qualifiers as required.

## Example
 The following C# example first adds a number of context qualifiers to a WQLConnectionManager object *Context* dictionary property. It then displays a list of the context qualifiers in dictionary object.

> [!NOTE]
>  **WqlConnectionManager** derives from **ConnectionManagerBase**.

 In the example, the `LocaleID` context qualifier is hard-coded to English (U.S.). If you need the locale for non-U.S. installations, you can get it from the [SMS_Identification Server WMI Class](../../../develop/reference/core/servers/configure/sms_identification-server-wmi-class.md)`LocaleID` property.

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../../develop/core/understand/calling-code-snippets.md).

```
public void AddContextQualifiers(WqlConnectionManager connection)
{
    try
    {
        connection.Context.Add("ApplicationName", "My application name");
        connection.Context.Add("MachineName","Computername");
        connection.Context.Add("LocaleID", @"MS\1033");

        foreach (KeyValuePair<string, object> namedValue in connection.Context)
        {
            Console.WriteLine(namedValue.Key);
            Console.WriteLine(namedValue.Value);
            Console.WriteLine();
        }
    }
    catch (SmsException e)
    {
        Console.WriteLine("Failed to add context qualifier : " + e.Message);
    }
}

```

 The example method has the following parameters:

|Parameter|Type|Description|
|---------------|----------|-----------------|
|`connection`|-   WqlConnectionManager|A valid connection to the SMS Provider.|

## Compiling the Code

### Namespaces
 System

 System.Collections.Generic

 System.ComponentModel

 Microsoft.ConfigurationManagement.ManagementProvider

 Microsoft.ConfigurationManagement.ManagementProvider.WqlQueryEngine

### Assembly
 microsoft.configurationmanagement.managementprovider

 adminui.wqlqueryengine

## Robust Programming
 The Configuration Manager exceptions that can be raised are [SmsConnectionException](/previous-versions/system-center/developer/cc147431(v=msdn.10)) and [SmsQueryException](/previous-versions/system-center/developer/cc147436(v=msdn.10)). These can be caught together with [SmsException](/previous-versions/system-center/developer/cc147433(v=msdn.10)).

## See Also
 [Configuration Manager Context Qualifiers](../../../develop/core/understand/context-qualifiers.md)
 [How to Connect to a Configuration Manager Provider using Managed Code](../../../develop/core/understand/how-to-connect-to-an-sms-provider-by-using-managed-code.md)
