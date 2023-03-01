---
title: Export Configuration Baselines and Items
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: how-to
ms.assetid: 0599e22f-3de3-4182-bcc2-3175d91b5b58
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
description: You can export a configuration baseline or configuration item by using Configuration Manager SDK and reading the relevant SMS_ConfigurationItem instance and writing the SDMPackageXML property (string) to a file.
ms.reviewer: mstewart,aaroncz 
---
# How to Export Configuration Baselines and Configuration Items
In Configuration Manager, to export a configuration baseline or configuration item using the Configuration Manager SDK, read the relevant `SMS_ConfigurationItem` instance and write the `SDMPackageXML` property (string) to a file.  

> [!IMPORTANT]
>  The encoding of the XML file must be set to UTF-16 encoded Unicode.  

### To export Configuration Baselines and Configuration Items  

1.  Set up a connection to the SMS Provider.  

2.  Get the specific instance of [SMS_ConfigurationItem](../../develop/reference/compliance/sms_configurationitem-server-wmi-class.md) class using the unique ID of the configuration item (CI_ID).  

3.  Copy the configuration item XML (SDMPackageXML) into a variable.  

4.  Write the configuration item XML content to a file.  

## Example  
 The following code example shows how to read an instance of a configuration baseline or configuration item and then export it to a file.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../develop/core/understand/calling-code-snippets.md).  

```vbs  

Sub DCMExportBaselineOrCI(swbemServices, _  
                          pathToFile,    _  
                          configurationItemId)  

' Set required variables.  
fileContents          =    ""  
configurationItemXML  =    null  

' Get specified configuration item (configurationItemId variable).  
Set getCIInfo = swbemServices.Get("SMS_ConfigurationItem.CI_ID=" & configurationItemId )  

' Copy configuration item XML into variable.   
configurationItemXML = getCIInfo.SDMPackageXML  

Wscript.Echo configurationItemXML  

' Open file for write (Unicode option enabled by second true).  
Set FSO = CreateObject("Scripting.FileSystemObject")  
Set textFile = FSO.CreateTextFile(pathToFile, true, true)  

' Write XML content to file specified by pathToFile.       
textFile.Write configurationItemXML  
textFile.Close   

Wscript.Echo " "  
Wscript.Echo "Successfully wrote " & pathToFile  

End Sub  

```  

```c#  

public void DCMExportBaselineOrCI(WqlConnectionManager connection,  
                                  string pathToOutputFile,  
                                  string configurationItemId)  
{  

    // Set required variables.  
    string configurationItemXML = null;  

    try  
    {  
        // Get the specified configuration item (configurationItemId variable).  
        IResultObject getCIInfo = connection.GetInstance(@"SMS_ConfigurationItem.CI_ID=" + configurationItemId);  

        // Copy configuration item XML into variable.   
        configurationItemXML = getCIInfo["SDMPackageXML"].StringValue;  
    }  
    catch (SmsException ex)  
    {  
        Console.WriteLine("Failed to retrieve configuration item xml. " + "\n" + ex.Message);  
        throw;  
    }  

    StreamWriter sw = null;  
    try  
    {  
        // Open file for output.  
        sw = new StreamWriter(pathToOutputFile, false, System.Text.Encoding.Unicode);  

        // Write XML to output file.  
        sw.Write(configurationItemXML);  
    }  
    catch (Exception ex)  
    {  
        Console.WriteLine("Failed to write configuration item XML to: " + pathToOutputFile + "\n" + ex.Message);  
        throw;  
    }  
    finally  
    {  
        if (sw != null)  
        {  
            sw.Close();  
        }  
    }  

    Console.WriteLine("Wrote configuration item XML to: " + pathToOutputFile);  
}  

```  

 The example method has the following parameters:  

| Parameter | Type | Description |
| --------- | ---- | ----------- |
|`connection`|-   Managed: `WqlConnectionManager`<br />-   VBScript: [SWbemServices](/windows/win32/wmisdk/swbemservices)|A valid connection to the SMS Provider.|  
|-   pathToOutputFile<br />-   pathToFile|-   Managed: `String`<br />-   VBScript: `String`|Path to the output file.|  
|`configurationItemId`|-   Managed: `String`<br />-   VBScript: `String`|Identifier of a configuration item to export.|  

## Compiling the Code  

### Namespaces  
 System  

 System.Collections.Generic  

 System.ComponentModel  

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
 [About Configuration Baselines and Configuration Items](../../develop/compliance/about-configuration-baselines-and-configuration-items.md)   
 [Objects overview](../core/understand/configuration-manager-objects-overview.md)
 [How to Connect to a Configuration Manager Provider using Managed Code](../../develop/core/understand/how-to-connect-to-an-sms-provider-by-using-managed-code.md)   
 [How to Connect to a Configuration Manager Provider Using WMI](../../develop/core/understand/how-to-connect-to-an-sms-provider-in-configuration-manager-by-using-wmi.md)   
 [SMS_BaselineAssignment Server WMI Class](../../develop/reference/compliance/sms_baselineassignment-server-wmi-class.md)   
 [SMS_ConfigurationItem Server WMI Class](../../develop/reference/compliance/sms_configurationitem-server-wmi-class.md)
