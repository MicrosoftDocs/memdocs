---
title: "Create a Deployment Template"
titleSuffix: "Configuration Manager"
description: "Create a software updates deployment template in Configuration Manager by creating an instance of the SMS_Template class and populating the properties."
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: how-to
ms.assetid: 552c2251-8c97-4596-bcc0-71558ce8c532
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# How to Create a Deployment Template
You create a software updates deployment template, in Configuration Manager, by creating an instance of the `SMS_Template` class and populating the properties.  

### To create a deployment template  

1.  Set up a connection to the SMS Provider.  

2.  Create the new template object by using the `SMS_Template` class.  

3.  Populate the new template properties.  

4.  Save the new template and properties.  

## Example  
 The following example method shows how to create a software updates deployment template by using the `SMS_Template` class and class properties.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../develop/core/understand/calling-code-snippets.md).  

> [!NOTE]
> In the following code examples, the template settings are passed into the method by using a string variable called deploymentTemplateSettings. The template settings are stored in an XML structure.  

VB Template Setting Example (one long string):  

```xml
deploymentTemplateSettings = "<TemplateDescription xmlns:xsi=""http://www.w3.org/2001/XMLSchema-instance"" xmlns:xsd=""http://www.w3.org/2001/XMLSchema""> <CollectionId>SMS00001</CollectionId> <IncludeSub>true</IncludeSub> <AttendedInstall>true</AttendedInstall> <UTC>true</UTC> <Duration>2</Duration> <DurationUnits>Weeks</DurationUnits> <SuppressServers>Unchecked</SuppressServers> <SuppressWorkstations>Unchecked</SuppressWorkstations> <AllowRestart>false</AllowRestart> <Deploy2003>true</Deploy2003> <CollectImmediately>false</CollectImmediately> <LocalDPOption>DownloadAndInstall</LocalDPOption> <RemoteDPOption>DownloadAndInstall</RemoteDPOption> <DisableMomAlert>false</DisableMomAlert> <GenerateMomAlert>false</GenerateMomAlert> <UseRemoteDP>false</UseRemoteDP> <UseUnprotectedDP>false</UseUnprotectedDP> </TemplateDescription>"  
```

C# Template Setting Example (the same template settings and still passed as a string, but the XML structure is more obvious):  

```xml
string deploymentTemplateSettings =   
  @"<TemplateDescription xmlns:xsi=""http://www.w3.org/2001/XMLSchema-instance"" xmlns:xsd=""http://www.w3.org/2001/XMLSchema"">  
  <CollectionId>SMS00001</CollectionId>  
  <IncludeSub>true</IncludeSub>  
  <AttendedInstall>true</AttendedInstall>  
  <UTC>true</UTC>  
  <Duration>2</Duration>  
  <DurationUnits>Weeks</DurationUnits>  
  <SuppressServers>Unchecked</SuppressServers>  
  <SuppressWorkstations>Unchecked</SuppressWorkstations>  
  <AllowRestart>false</AllowRestart>  
  <Deploy2003>true</Deploy2003>  
  <CollectImmediately>false</CollectImmediately>  
  <LocalDPOption>DownloadAndInstall</LocalDPOption>  
  <RemoteDPOption>DownloadAndInstall</RemoteDPOption>  
  <DisableMomAlert>false</DisableMomAlert>  
  <GenerateMomAlert>false</GenerateMomAlert>  
  <UseRemoteDP>false</UseRemoteDP>  
  <UseUnprotectedDP>false</UseUnprotectedDP>  
  </TemplateDescription>";  
```  

```vbs  

Sub CreateSUMDeploymentTemplate(connection,              _  
                                 newTemplateName,         _  
                                 newTemplateDescription,  _  
                                 newTemplateSettings,     _  
                                 newTemplateType)                 

    ' Create the new Template object.  
    Set newSUMTemplate = connection.Get("SMS_Template").SpawnInstance_  

    ' Populate the SMS_Template properties.  
    ' Note: The template name (newTemplateName) must be unique.  
    newSUMTemplate.Name = newTemplateName  
    newSUMTemplate.Description = newTemplateDescription  
    newSUMTemplate.Data = newTemplateSettings  
    newSUMTemplate.Type = newTemplateType  

    ' Save the new template and properties.  
    newSUMTemplate.Put_   

    ' Output the new template name.  
    Wscript.Echo "Created new template: " & newTemplateName                    

 End Sub  

```  

```c#  

public void CreateSUMDeploymentTemplate(WqlConnectionManager connection,  
                                        string newTemplateName,   
                                        string newTemplateDescription,  
                                        string newTemplateSettings,  
                                        int newTemplateType)  
{  
    try  
    {  
        // Create the template object.  
        IResultObject newSUMTemplate = connection.CreateInstance("SMS_Template");  

        // Populate the new template properties.  
        // Note: The template name (newTemplateName) must be unique.  
        newSUMTemplate["Name"].StringValue = newTemplateName;  
        newSUMTemplate["Description"].StringValue = newTemplateDescription;  
        newSUMTemplate["Data"].StringValue = newTemplateSettings;  
        newSUMTemplate["Type"].IntegerValue = newTemplateType;  

        // Save the new template and the new template properties.  
        newSUMTemplate.Put();  

        // Output the new template name.  
        Console.WriteLine("Created template: " + newTemplateName);  
    }  

    catch (SmsException ex)  
    {  
        Console.WriteLine("Failed to create template. Error: " + ex.Message);  
        throw;  
    }  
}  

```  

 This example method has the following parameters:  

|Parameter|Type|Description|
|---------|----|-----------|
|`connection`|-   Managed: `WqlConnectionManager`<br />-   VBScript: [SWbemServices](/windows/win32/wmisdk/swbemservices)|A valid connection to the SMS Provider.|  
|`newTemplateName`|-   Managed: `String`<br />-   VBScript: `String`|The new template name. The template name must be unique.|  
|`newTemplateDescription`|-   Managed: `String`<br />-   VBScript: `String`|The description for the new template.|  
|`newTemplateSettings`|-   Managed: `String`<br />-   VBScript: `String`|The new template settings. The settings are in an XML structure, stored as a string.<br /><br /> <ul><li>**CollectionId**<br /><br />     The collection for the software update deployment.<br /><br /> <ul><li>A valid collection ID.</li></ul></li><li>**IncludeSub**<br /><br />     Include members of subcollections.<br /><br /> <ul><li>`true`</li><li>`false`</li></ul></li><li>**AttendedInstall**<br /><br />     Display software update notifications on clients (false will suppress notifications).<br /><br /> <ul><li>`true`</li><li>`false`</li></ul></li><li>**UTC**<br /><br />     Use Coordinated Universal Time (UTC) instead of client local time.<br /><br /> <ul><li>`true`</li><li>`false`</li></ul></li><li>**Duration**<br /><br />     Duration of the deployment.<br /><br /> <ul><li>1-24 (hours)</li><li>1-365 (days)</li><li>1-4 (weeks)</li><li>1-12 (months)</li></ul></li><li>**DurationUnits**<br /><br />     Duration units.<br /><br /> <ul><li>hours</li><li>days</li><li>weeks</li><li>months</li></ul></li><li>**SuppressServers**<br /><br />     Suppress the system restart on servers.<br /><br /> <ul><li>Checked</li><li>Unchecked</li></ul></li><li>**SuppressWorkstations**<br /><br />     Suppress the system restart on workstations.<br /><br /> <ul><li>Checked</li><li>Unchecked</li></ul></li><li>**AllowRestart**<br /><br />     Allow system restart outside of maintenance windows (for both servers and workstations).<br /><br /> <ul><li>`true`</li><li>`false`</li></ul></li><li>**Deploy2003**<br /><br />     Deploy software updates to SMS 2003 clients.<br /><br /> <ul><li>`true`</li><li>`false`</li></ul></li><li>**CollectImmediately** (SMS 2003 client specific)<br /><br />     Collect hardware inventory immediately after installing software updates.<br /><br /> <ul><li>`true`</li><li>`false`</li></ul></li><li>**LocalDPOption** (SMS 2003 client specific)<br /><br />     Specify whether to download the update source files before running the installation when a distribution point is available locally.<br /><br /> <ul><li>DownloadAndInstall</li><li>InstallFromDP</li></ul></li><li>**RemoteDPOption** (SMS 2003 client specific)<br /><br />     Specify whether to download the update source files before running the installation when no distribution point is available locally.<br /><br /> <ul><li>DownloadAndInstall</li><li>InstallFromDP</li></ul></li><li>**DisableMomAlert**<br /><br />     Disable Operations Manager alerts while software updates run.<br /><br /> <ul><li>`true`</li><li>`false`</li></ul></li><li>**GenerateMomAlert**<br /><br />     Generate Operations Manager alert when a software update installation fails.<br /><br /> <ul><li>`true`</li><li>`false`</li></ul></li><li>**UseRemoteDP**<br /><br />     Download software updates from use a remote distribution point (even when a client is connected within a slow or unreliable network boundary).<br /><br /> <ul><li>`true`</li><li>`false`</li></ul></li><li>**UseUnprotectedDP**<br /><br />     Download software updates from a unprotected distribution point (when updates are not available from any protected distribution point).<br /><br /> <ul><li>`true`</li><li>`false`</li></ul></li></ul>|  
|`newTemplateType`|-   Managed: `Integer`<br />-   VBScript: `Integer`|The new template type. Currently the only possible value is:<br /><br /> -   `0` (SUM_DEPLOYMENT)|  

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
 [About software update deployments](about-software-updates-deployments.md)
 [How to Assign a Package to a Distribution Point](../../develop/core/servers/configure/how-to-assign-a-package-to-a-distribution-point.md)   
 [SMS_Template](../../develop/reference/sum/sms_template-server-wmi-class.md)
