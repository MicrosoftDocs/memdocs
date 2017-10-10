---
title: "Delete Updates from a Deployment Package"
titleSuffix: "Configuration Manager"
ms.custom: ""
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.reviewer: ""
ms.suite: ""
ms.technology:
  - "configmgr-other"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to:
  - "System Center Configuration Manager (current branch)"
ms.assetid: b8a24372-4e7a-4565-8dda-96e912fd2fd4searchScope: - ConfigMgr SDK
caps.latest.revision: 8
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# How to Delete Updates from a Deployment Package
You remove updates from a software updates deployment package, in System Center Configuration Manager, by obtaining an instance of the [SMS_SoftwareUpdatesPackage](../../develop/reference/sum/sms_softwareupdatespackage-server-wmi-class.md) class and using the [RemoveContent](../../develop/reference/sum/removecontent-method-in-class-sms_softwareupdatespackage.md) method.  

### To delete updates from a software updates deployment package  

1.  Set up a connection to the SMS Provider.  

2.  Obtain an existing package object by using the `SMS_SoftwareUpdatesPackage` class.  

3.  Remove update content from the existing software updates management package by using the `RemoveContent` method.  

## Example  
 The following example method shows how to remove updates from a software updates deployment package by using the `SMS_SoftwareUpdatesPackage` class and the `RemoveContent` method.  

> [!IMPORTANT]
>  No VBScript example was included, as the `RemoveContent` method does not return from the method call on failure. This is a known issue and is being investigated.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../develop/core/understand/calling-code-snippets.md).  

 Example of the method call in C#:  

```  

// Prework for RemoveUpdatesfromSUMDeploymentPackage.  
// Define the array of Content IDs to load into the content parameters.  
int[] newArrayContentIDs2 = new int[] { 82 };  

// Load the update content parameters into an object to pass to the method.  
Dictionary<string, object> removeContentParameters = new Dictionary<string, object>();  
removeContentParameters.Add("ContentIDs", newArrayContentIDs2);  
removeContentParameters.Add("bRefreshDPs", true);  

// Call the RemoveUpdatesfromSUMDeploymentPackage method.  
RemoveUpdatesfromSUMDeploymentPackage(WMIConnection,  
                                      "ABC00001",  
                                      removeContentParameters);  

```  

```c#  

public void RemoveUpdatesfromSUMDeploymentPackage(WqlConnectionManager connection,  
                                                  string existingSUMPackageID,  
                                                  Dictionary<string, object> removeContentParameters)  
{  
    try  
    {  
        // Get the specific SUM Deployment Package to change.  
        IResultObject existingSUMDeploymentPackage = connection.GetInstance(@"SMS_SoftwareUpdatesPackage.PackageID='" + existingSUMPackageID + "'");  

        // Remove updates from the existing SUM Deployment Package using the RemoveContent method.  
        // Note: The method will throw an exception, if the method is not able to add the content.  
        IResultObject result = existingSUMDeploymentPackage.ExecuteMethod("RemoveContent", removeContentParameters);  

        // Output a success message.  
        Console.WriteLine("Removed content from the deployment package. ");  

    }  
    catch (SmsException ex)  
    {  
        Console.WriteLine("Failed to remove content from the deployment package. Error: " + ex.Message);  
        throw;  
    }  
}  

```  

 The example method has the following parameters:  

||||  
|-|-|-|  
|Parameter|Type|Description|  
|`connection`|-   Managed: `WqlConnectionManager`|A valid connection to the SMS Provider.|  
|`existingSUMPackageID`|-   Managed: `String`|The package ID for an existing software updates management package.|  
|`removecontentParameters`|-   Managed: `dictionary object`|The set of parameters (`ContentIDs`, `bRefreshDPs`) that is passed into the method and used with the `RemoveContent` method call.|  

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
 For more information about securing Configuration Manager applications, see [Securing Configuration Manager Applications](../../develop/core/understand/securing-configuration-manager-applications.md).  

## See Also  
 [System Center Configuration Manager Software Development Kit](../../develop/core/misc/system-center-configuration-manager-sdk.md)   
 [Configuration Manager Software Updates](../../develop/sum/software-updates.md)   
 [Software Updates Scheduled Deployment](../../develop/sum/software-updates-deployments.md)   
 [How to Assign a Package to a Distribution Point](../../develop/core/servers/configure/how-to-assign-a-package-to-a-distribution-point.md)   
 [SMS_SoftwareUpdatesPackage](../../develop/reference/sum/sms_softwareupdatespackage-server-wmi-class.md)   
 [RemoveContent Method in Class SMS_SoftwareUpdatesPackage](../../develop/reference/sum/removecontent-method-in-class-sms_softwareupdatespackage.md)
