---
title: "Enable Unknown Computer Support for a PXE Service Point"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: fbabd2ed-c3ee-48f0-8d9d-7d0c48f69af6
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# How to Enable Unknown Computer Support for a PXE Service Point
In System Center Configuration Manager, you set the operating system deployment PXE service point response to incoming PXE requests from unknown computers by setting the **SupportUnknownMachines** embedded property.  

 **SupportUnknownMachines** has the following possible values.  

|Value|Description|  
|-----------|-----------------|  
|0|The PXE service point does not respond to PXE requests from unknown computers.|  
|1|The PXE service point responds to requests from unknown computers.|  

### To set the PXE service point response to PXE requests from unknown computers  

1.  Set up a connection to the SMS Provider. For more information, see [About the SMS Provider in Configuration Manager](../../develop/core/understand/about-the-sms-provider-in-configuration-manager.md).  

2.  Make a connection to the distribution point instance with PXE enabled.  

3.  Get the embedded properties.  

4.  Update the **SupportUnknownMachines** embedded property.  

5.  Commit the changes to the site control file.  

## Example  
 The following example method sets the response for a PXE request based on the supplied `String` value (`allowResponse`).  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../develop/core/understand/calling-code-snippets.md).  

```c#  
public void EnablePXE(WqlConnectionManager connection,                      string siteCode,                      string serverName,                      string allowResponse){    try    {        //Connect to distribution point instance.                        IResultObject siteRole = connection.GetInstance("SMS_SCI_SysResUse.FileType=2,ItemName=\"[\\\"Display=\\\\\\\\" + serverName + "\\\\\\\"]MSWNET:[\\\"SMS_SITE=" + siteCode + "\\\"]\\\\\\\\" + serverName + "\\\\,SMS Distribution Point\",ItemType=\"System Resource Usage\",SiteCode=" + "\"" + siteCode + "\"");        // Create temporary copy of the embedded properties.        Dictionary<string, IResultObject> embeddedProperties = siteRole.EmbeddedProperties;        // Enumerate through the embedded properties and makes changes as needed.        foreach (KeyValuePair<string, IResultObject> kvp in siteRole.EmbeddedProperties)        {            // Setting: SupportUnknownMachines            if (kvp.Value.PropertyList["PropertyName"] == "SupportUnknownMachines")            {                // Get current property value.                Console.WriteLine();                Console.WriteLine("Property: {0}", kvp.Value.PropertyList["PropertyName"]);                Console.WriteLine("Current value: {0}", kvp.Value.PropertyList["Value"]);                // Change value.                embeddedProperties["SupportUnknownMachines"]["Value"].StringValue = allowResponse;                Console.WriteLine("Setting the {0} value to {1}.", kvp.Value.PropertyList["PropertyName"], allowResponse);            }        }        // Store the settings that have changed.        siteRole.EmbeddedProperties = embeddedProperties;        // Save the settings.         siteRole.Put();    }    catch (SmsException ex)    {        Console.WriteLine();        Console.WriteLine("Failed. Error: " + ex.InnerException.Message);    }}  
```  

 The example method has the following parameters:  

||||  
|-|-|-|  
|Parameter|Type|Description|  
|`connection`|Managed: `WqlConnectionManager`|A valid connection to the SMS Provider.|  
|`siteCode`|Managed: `String`|The Configuration Manager site code.|  
|`serverName`|Managed: `String`|The server name. For example, `"SERVER1.DOMAIN1.COM"`.|  
|`allowResponse`|Managed: `String`|The value to set whether the PXE service point will respond to unknown computers.<br /><br /> -   0 - The PXE service point does not respond to PXE requests from unknown computers.<br />-   1 - The PXE service point responds to requests from unknown computers.|  

## Compiling the Code  
 The C# example has the following compilation requirements:  

### Namespaces  
 System  

 System.Collections.Generic  

 System.Text  

 Microsoft.ConfigurationManagement.ManagementProvider  

 Microsoft.ConfigurationManagement.ManagementProvider.WqlQueryEngine  

### Assembly  
 microsoft.configurationmanagement.managementprovider  

 adminui.wqlqueryengine  

## Robust Programming  
 For more information about error handling, see [About Configuration Manager Errors](../../develop/core/understand/about-configuration-manager-errors.md).  

## .NET Framework Security  
 For more information about securing Configuration Manager applications, see [Securing Configuration Manager Applications](../../develop/core/understand/securing-configuration-manager-applications.md).  

## See Also  
 [About Operating System Deployment Site Role Configuration](../../develop/osd/about-operating-system-deployment-site-role-configuration.md)   
 [Configuration Manager Operating System Deployment](../../develop/osd/operating-system-deployment.md)   
 [Configuration Manager Programming Fundamentals](../../develop/core/understand/configuration-manager-programming-fundamentals.md)   
 [Operating System Deployment Site Role Configuration](../../develop/osd/operating-system-deployment-site-role-configuration.md)   
 [How to Read and Write to the Configuration Manager Site Control File by Using Managed Code](../../develop/core/understand/how-to-read-and-write-to-the-site-control-file-by-using-managed-code.md)   
 [How to Read and Write to the Configuration Manager Site Control File by Using WMI](../../develop/core/understand/how-to-read-and-write-to-the-site-control-file-by-using-wmi.md)
