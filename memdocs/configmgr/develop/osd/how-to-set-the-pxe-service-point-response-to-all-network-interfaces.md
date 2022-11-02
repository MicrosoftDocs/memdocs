---
title: Set the PXE Service Point Response to All Network Interfaces
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: how-to
ms.assetid: 9ef702dc-1d13-4c4a-99d8-a5503628fde1
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
description: Learn how to set the PXE service point response to all network interfaces by setting the BindPolicy embedded property.
ms.reviewer: mstewart,aaroncz 
---
# How to Set the PXE Service Point Response to All Network Interfaces
In Configuration Manager, you set the operating system deployment PXE service point response to network interfaces by setting the `BindPolicy` embedded property.  

 `BindPolicy` has the following possible values.  

|Value|Description|  
|-----------|-----------------|  
|0|Responds to PXE requests on all network interfaces.|  
|1|Responds to requests on specific network interfaces.|  

 If `BindPolicy` is set to respond to specific network interfaces (1), you must add the media access control (MAC) addresses for the required network interfaces by using the `BindExcept` list. If `BindExcept` is not populated, PXE will not respond to any requests. For more information see, [How to Set the PXE Service Point Response for a Specific Network Interface](../../develop/osd/how-to-set-the-pxe-service-point-response-for-a-specific-network-interface.md).  

### To set the PXE response to network interfaces  

1.  Set up a connection to the SMS Provider. For more information, see [SMS Provider fundamentals](../core/understand/sms-provider-fundamentals.md).  

2.  Make a connection to the distribution point instance with PXE enabled.  

3.  Get the embedded properties.  

4.  Update the `BindPolicy` embedded property.  

5.  Commit the changes to the site control file.  

## Example  
 The following example method sets the PXE service point response to a network interface. If `respondToSpecificInterface` is set to `1` you must set the `BindExcept` list to specify the network interfaces that can respond. For more information, see [How to Set the PXE Service Point Response for a Specific Network Interface](../../develop/osd/how-to-set-the-pxe-service-point-response-for-a-specific-network-interface.md).  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../develop/core/understand/calling-code-snippets.md).  

```c#  
public void SetNetworkInterface(WqlConnectionManager connection,                                  string siteCode,                                  string serverName,                                  string respondToSpecificInterface){    try    {        //Connect to distribution point instance.                        IResultObject siteRole = connection.GetInstance("SMS_SCI_SysResUse.FileType=2,ItemName=\"[\\\"Display=\\\\\\\\" + serverName + "\\\\\\\"]MSWNET:[\\\"SMS_SITE=" + siteCode + "\\\"]\\\\\\\\" + serverName + "\\\\,SMS Distribution Point\",ItemType=\"System Resource Usage\",SiteCode=" + "\"" + siteCode + "\"");        // Create temporary copy of the embedded properties.        Dictionary<string, IResultObject> embeddedProperties = siteRole.EmbeddedProperties;        // Enumerate through the embedded properties and makes changes as needed.        foreach (KeyValuePair<string, IResultObject> kvp in siteRole.EmbeddedProperties)        {            // Setting: BindPolicy            if (kvp.Value.PropertyList["PropertyName"] == "BindPolicy")            {                // Get current property value.                Console.WriteLine();                Console.WriteLine("Property: {0}", kvp.Value.PropertyList["PropertyName"]);                Console.WriteLine("Current value: {0}", kvp.Value.PropertyList["Value"]);                // Change value.                embeddedProperties["BindPolicy"]["Value"].StringValue = respondToSpecificInterface;                Console.WriteLine("Setting the {0} value to {1}.", kvp.Value.PropertyList["PropertyName"], respondToSpecificInterface);            }        }        // Store the settings that have changed.        siteRole.EmbeddedProperties = embeddedProperties;        // Save the settings.         siteRole.Put();    }    catch (SmsException ex)    {        Console.WriteLine();        Console.WriteLine("Failed. Error: " + ex.InnerException.Message);    }}  
```  

 The example method has the following parameters:  

|Parameter|Type|Description|
|-|-|-|
|`connection`|Managed: `WqlConnectionManager`|A valid connection to the SMS Provider.|  
|`siteCode`|Managed: `String`|The Configuration Manager site code.|  
|`serverName`|Managed: `String`|The server name. For example, `"SERVER1.DOMAIN1.COM"`.|  
|`respondToSpecficInterface`|Managed: `String`|The value to set which network interfaces will respond to PXE requests.<br /><br /> -   0 - Responds to PXE requests on all network interfaces.<br />-   1 - Responds to requests on specific network interfaces.|  

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
 For more information about securing Configuration Manager applications, see [Configuration Manager role-based administration](../../develop/core/servers/configure/role-based-administration.md).  

## See Also  
 [About OS deployment site role configuration](about-operating-system-deployment-site-role-configuration.md)
 [How to Set the PXE Service Point Response for a Specific Network Interface](../../develop/osd/how-to-set-the-pxe-service-point-response-for-a-specific-network-interface.md)   
 [How to Read and Write to the Configuration Manager Site Control File by Using Managed Code](../../develop/core/understand/how-to-read-and-write-to-the-site-control-file-by-using-managed-code.md)   
 [How to Read and Write to the Configuration Manager Site Control File by Using WMI](../../develop/core/understand/how-to-read-and-write-to-the-site-control-file-by-using-wmi.md)
