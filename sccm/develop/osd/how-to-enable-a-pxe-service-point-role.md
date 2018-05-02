---
title: "Enable a PXE Service Point Role"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 340ab144-d2e3-475b-9a1b-e3346c2be551
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# How to Enable a PXE Service Point Role
You enable the PXE Service Point role, in System Center Configuration Manager, by getting an instance of a specific distribution point and setting the `IsPXE` value to `1`.  

### To enable a PXE service point role  

1.  Set up a connection to the SMS Provider. For more information see, [About the SMS Provider in Configuration Manager](../../develop/core/understand/about-the-sms-provider-in-configuration-manager.md).  

2.  Get an instance of a specific distribution point.  

3.  Set the `IsPXE` embedded property to `1`.  

4.  Save the distribution point instance.  

## Example  
 The following example method enables a PXE service point.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../develop/core/understand/calling-code-snippets.md).  

```c#  
public void EnablePXE(WqlConnectionManager connection,                      string siteCode,                      string serverName){    try    {        //Connect to distribution point instance.                        IResultObject siteRole = connection.GetInstance("SMS_SCI_SysResUse.FileType=2,ItemName=\"[\\\"Display=\\\\\\\\" + serverName + "\\\\\\\"]MSWNET:[\\\"SMS_SITE=" + siteCode + "\\\"]\\\\\\\\" + serverName + "\\\\,SMS Distribution Point\",ItemType=\"System Resource Usage\",SiteCode=" + "\"" + siteCode + "\"");        // Create temporary copy of the embedded properties.        Dictionary<string, IResultObject> embeddedProperties = siteRole.EmbeddedProperties;        // Enumerate through the embedded properties and makes changes as needed.        foreach (KeyValuePair<string, IResultObject> kvp in siteRole.EmbeddedProperties)        {            // Setting: IsPXE            if (kvp.Value.PropertyList["PropertyName"] == "IsPXE")            {                // Get current property value.                Console.WriteLine();                Console.WriteLine("Property: {0}", kvp.Value.PropertyList["PropertyName"]);                Console.WriteLine("Current value: {0} (0 not enabled, 1 enabled)", kvp.Value.PropertyList["Value"]);                // Change value to enable PXE (1 enabled, 0 not enabled).                 embeddedProperties["IsPXE"]["Value"].StringValue = "1";                Console.WriteLine("Setting the {0} value to {1}.", kvp.Value.PropertyList["PropertyName"], "1");            }        }        // Store the settings that have changed.        siteRole.EmbeddedProperties = embeddedProperties;        // Save the settings.         siteRole.Put();    }    catch (SmsException ex)    {        Console.WriteLine();        Console.WriteLine("Failed. Error: " + ex.InnerException.Message);    }}   
```  

 The example method has the following parameters:  

||||  
|-|-|-|  
|Parameter|Type|Description|  
|`connection`|Managed: `WqlConnectionManager`|A valid connection to the SMS Provider.|  
|`siteCode`|Managed: `String`|The Configuration Manager site code.|  
|`serverName`|Managed: `String`|The server name. For example, `"SERVER1.DOMAIN1.COM"`|  

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
 [SMS_SCI_SysResUse Server WMI Class](../../develop/reference/core/servers/configure/sms_sci_sysresuse-server-wmi-class.md)   
 [PackNALPath Method in Class SMS_NAL_Methods](../../develop/reference/misc/packnalpath-method-in-class-sms_nal_methods.md)   
 [About Operating System Deployment Site Role Configuration](../../develop/osd/about-operating-system-deployment-site-role-configuration.md)   
 [Configuration Manager Operating System Deployment](../../develop/osd/operating-system-deployment.md)   
 [Configuration Manager Programming Fundamentals](../../develop/core/understand/configuration-manager-programming-fundamentals.md)   
 [Operating System Deployment Site Role Configuration](../../develop/osd/operating-system-deployment-site-role-configuration.md)   
 [How to Set the Response Delay for a PXE Service Point](../../develop/osd/how-to-set-the-response-delay-for-a-pxe-service-point.md)   
 [How to Set the PXE Service Point Response to All Network Interfaces](../../develop/osd/how-to-set-the-pxe-service-point-response-to-all-network-interfaces.md)   
 [How to Set the PXE Service Point Response to PXE Requests](../../develop/osd/how-to-set-the-pxe-service-point-response-to-pxe-requests.md)   
 [How to Read and Write to the Configuration Manager Site Control File by Using Managed Code](../../develop/core/understand/how-to-read-and-write-to-the-site-control-file-by-using-managed-code.md)   
 [How to Read and Write to the Configuration Manager Site Control File by Using WMI](../../develop/core/understand/how-to-read-and-write-to-the-site-control-file-by-using-wmi.md)
