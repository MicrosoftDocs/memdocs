---
title: "Set the PXE Service Point Response for a Specific Network Interface"
titleSuffix: "Configuration Manager"
description: "Creates a copy of the current boot image source .wim file and updates the copy with the most current operating system deployment binaries."
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: how-to
ms.assetid: fdfdbb2d-50d9-4f01-a1aa-a07aae85629d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# How to Set the PXE Service Point Response for a Specific Network Interface
In Configuration Manager, you set the operating system deployment to respond to a specific set of network addresses by adding the required media access control (MAC) addresses to the `BindExcept` embedded property list. You must also set the `BindPolicy` embedded property to 1. This specifies that PXE requests are accepted on specified network address only. For more information about setting `BindPolicy`, see [How to Set the PXE Service Point Response to All Network Interfaces](../../develop/osd/how-to-set-the-pxe-service-point-response-to-all-network-interfaces.md).  

### To set the response for a specific network interface  

1.  Set up a connection to the SMS Provider. For more information, see [SMS Provider fundamentals](../core/understand/sms-provider-fundamentals.md).  

2.  Make a connection to the PXE service point resources section of the site control file.  

3.  Get the `BindExcept` embedded property list.  

4.  Add the MAC addresses to the `BindExcept` embedded property list.  

5.  Commit the changes to the site control file.  

## Example  
 The following example method adds a supplied MAC address to the list of MAC address that are responded to.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../develop/core/understand/calling-code-snippets.md).  

```c#  
public void SetNetworkInterface(WqlConnectionManager connection,                                string siteCode,                                string serverName,                                string macAddress){    try    {        //Connect to distribution point instance.                        IResultObject siteRole = connection.GetInstance("SMS_SCI_SysResUse.FileType=2,ItemName=\"[\\\"Display=\\\\\\\\" + serverName + "\\\\\\\"]MSWNET:[\\\"SMS_SITE=" + siteCode + "\\\"]\\\\\\\\" + serverName + "\\\\,SMS Distribution Point\",ItemType=\"System Resource Usage\",SiteCode=" + "\"" + siteCode + "\"");        // Create temporary copy of the embedded properties.        Dictionary<string, IResultObject> embeddedPropertyLists = siteRole.EmbeddedPropertyLists;        // Get current mac addresses.        string[] macAddresses = embeddedPropertyLists["BindExcept"]["Values"].StringArrayValue;        //Convert to list.        List<string> addressList = new List<string>();        foreach (string address in macAddresses)        {            addressList.Add(address);        }        // Add the new mac address to the list.        addressList.Add(macAddress);        // Add the new mac address to the list.        embeddedPropertyLists["BindExcept"]["Values"].StringArrayValue = addressList.ToArray();        siteRole.EmbeddedPropertyLists = embeddedPropertyLists;        // Save the settings.         siteRole.Put();    }    catch (SmsException ex)    {        Console.WriteLine();        Console.WriteLine("Failed. Error: " + ex.InnerException.Message);    }}  
```  

 The example method has the following parameters:  

|Parameter|Type|Description|
|-|-|-|
|`connection`|-   Managed:  `WqlConnectionManager`|A valid connection to the SMS Provider.|  
|`serverName`|-   Managed: `String`|The Configuration Manager server.|  
|`siteCode`|-   Managed: `String`|The Configuration Manager site code.|  
|`macAddress`|-   Managed: `String`|The MAC address to be added in the following format:<br /><br /> 00:11:22:33:44:55|  

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
 [How to Read and Write to the Configuration Manager Site Control File by Using Managed Code](../../develop/core/understand/how-to-read-and-write-to-the-site-control-file-by-using-managed-code.md)   
 [How to Read and Write to the Configuration Manager Site Control File by Using WMI](../../develop/core/understand/how-to-read-and-write-to-the-site-control-file-by-using-wmi.md)
