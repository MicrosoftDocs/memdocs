---
title: "How to Create a Software Metering Rule"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: how-to
ms.assetid: 9929aeac-7f48-4151-b228-d66be910a9c8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth
description: "You can create a software metering rule in Configuration Manager by creating an instance of the SMS_MeteredProductRule class and populating the properties."

---
# How to Create a Software Metering Rule
You create a software metering rule, in Configuration Manager, by creating an instance of the `SMS_MeteredProductRule` class and populating the properties.  

### To create software metering rule  

1.  Set up a connection to the SMS Provider.  

2.  Create the new software metering rule object by using the `SMS_MeteredProductRule` class.  

3.  Populate the new software metering rule properties.  

4.  Save the new software metering rule and properties.  

## Example  
 The following example method shows how to create a software metering rule by creating an instance of the `SMS_MeteredProductRule` class and populating the properties.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../develop/core/understand/calling-code-snippets.md).  

```vb

Sub CreateSWMRule(connection,              _  
                  newProductName,          _  
                  newFileName,             _  
                  newOriginalFileName,     _  
                  newFileVersion,          _  
                  newLanguageID,           _  
                  newSiteCode,             _  
                  newApplyToChildSites)                 

    ' Create the new MeteredProductRule object.   
    Set newSWMRule = connection.Get("SMS_MeteredProductRule").SpawnInstance_  

    ' Populate the SMS_MeteredProductRule properties.  
    newSWMRule.ProductName= newProductName  
    newSWMRule.FileName = newFileName  
    newSWMRule.OriginalFileName =  newOriginalFileName  
    newSWMRule.FileVersion = newFileVersion  
    newSWMRule.LanguageID = newLanguageID  
    newSWMRule.SiteCode = newSiteCode  
    newSWMRule.ApplyToChildSites = newApplyToChildSites  

    ' Save the new rule and properties.  
    newSWMRule.Put_   

    ' Output new rule name.  
    Wscript.Echo "Created new SWM Rule: " & newProductName                    

End Sub  
```  

```c#  

public void CreateSWMRule(WqlConnectionManager connection,  
                          string newProductName,  
                          string newFileName,  
                          string newOriginalFileName,  
                          string newFileVersion,  
                          int newLanguageID,  
                          string newSiteCode,  
                          bool newApplyToChildSites)  
{  
    try  
    {  
        // Create the new SMS_AuthorizationList object.  
        IResultObject newSWMRule = connection.CreateInstance("SMS_MeteredProductRule");  

        // Populate the new SMS_MeteredProductRule object properties.  
        newSWMRule["ProductName"].StringValue = newProductName;  
        newSWMRule["FileName"].StringValue = newFileName;  
        newSWMRule["OriginalFileName"].StringValue = newOriginalFileName;  
        newSWMRule["FileVersion"].StringValue = newFileVersion;  
        newSWMRule["LanguageID"].IntegerValue = newLanguageID;  
        newSWMRule["SiteCode"].StringValue = newSiteCode;  
        newSWMRule["ApplyToChildSites"].BooleanValue = newApplyToChildSites;  

        // Save changes.  
        newSWMRule.Put();  

        Console.WriteLine();  
        Console.WriteLine("Created new SWM Rule: " + newProductName);  
    }  

    catch (SmsException ex)  
    {  
        Console.WriteLine("Failed to create SWM rule. Error: " + ex.Message);  
        throw;  
    }  
}  

```  

 The example method has the following parameters:  

|Parameter|Type|Description|  
|----|----|----|
|`connection`|-   Managed: `WqlConnectionManager`<br />-   VBScript: `SWbemServices`|A valid connection to the SMS Provider.|  
|`newProductName`|-   Managed: `String`<br />-   VBScript: `String`|The new product name.|  
|`newFileName`|-   Managed: `String`<br />-   VBScript: `String`|The new file name.|  
|`newOriginalFileName`|-   Managed: `String`<br />-   VBScript: `String`|The new original file name.|  
|`newFileVersion`|-   Managed: `String`<br />-   VBScript: `String`|The new file version.|  
|`newLanguageID`|-   Managed: `Integer`<br />-   VBScript: `Integer`|The new language ID.|  
|`newSiteCode`|-   Managed: `String`<br />-   VBScript: `String`|The new site code.|  
|`newApplyToChildSites`|-   Managed: `Boolean`<br />-   VBScript: `Boolean`|Determines whether the rule will apply to child sites.|  

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
