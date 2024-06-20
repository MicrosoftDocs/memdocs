---
title: Add a State Migration Point Folder
titleSuffix: Configuration Manager
description: Add an operating system deployment state migration point folder by adding the folder description to the Directories embedded property list.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: how-to
ms.assetid: 95b399e5-47fd-4519-a30e-c220ebdb5c95
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# How to Add a State Migration Point Folder
In Configuration Manager, you add an operating system deployment state migration point folder by adding the folder description to the `Directories` embedded property list.  

 The folder description is a string that defines the following information.  

|Value|Description|  
|-----------|-----------------|  
|`Directory`|The name of the folder.|  
|`MaxClients`|The maximum number of clients supported.|  
|`MinDiskSpace`|The minimum disk space required.|  
|`MinDiskSpaceUnit`|The minimum disk space units.<br /><br /> 1 - MB<br /><br /> 2 - GB<br /><br /> 3 - Percentage|  

### To add a state migration point folder  

1.  Set up a connection to the SMS Provider. For more information, see [SMS Provider fundamentals](../core/understand/sms-provider-fundamentals.md).  

2.  Make a connection to the state migration point resources section of the site control file.  

3.  Get the `Directories` embedded properties list.  

4.  Update the `Directories` embedded property with new folder.  

5.  Commit the changes to the site control file.  

## Example  
 The following example method adds a new folder to the state migration point.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../develop/core/understand/calling-code-snippets.md).  

```vbs  
Sub AddSmpFolder( connection, _  
    context,              _  
    directory,            _  
     maxClients,          _  
     minDiskSpace,        _  
     minDiskSpaceUnit,    _  
    siteCode)  

    Dim InParams  
    Dim smpSettings  
    Dim found  

     ' Format the directories string.  
     smpSettings = "Directory=" + directory + ";MaxClients=" + _  
     CStr(maxClients) + ";MinDiskSpace=" + CStr(minDiskSpace) + _  
     ";MinDiskSpaceUnit=" + CStr(minDiskSpaceUnit) + ";"  

     Set InParams = connection.Get("SMS_SiteControlFile").Methods_("RefreshSCF").InParameters.SpawnInstance_  
InParams.SiteCode = siteCode  
connection.ExecMethod "SMS_SiteControlFile", "RefreshSCF", InParams, , context  

    Query = "SELECT * FROM SMS_SCI_SysResUse " & _  
            "WHERE RoleName = 'SMS State Migration Point' " & _  
            "AND SiteCode = '" & siteCode & "'"  

    found = false  

    Set SCIComponentSet = connection.ExecQuery(Query, , , context)  

    For Each SCIComponent In SCIComponentSet  
        For Each vProperty in SCIComponent.PropLists  

            WScript.Echo vProperty.PropertyListName  

            if   vProperty.PropertyListName = "Directories" Then  

                Dim  directories  
                Dim i  

                found = true  

                ' Resize the array to accommodate the new directory.  
                ReDim  directories(UBound (vProperty.Values)+1)  

                for i  = 0 to UBound(vProperty.Values)   
                    directories(i) = vProperty.Values(i)  
                Next  

                directories(ubound (directories))= smpSettings  
                vProperty.Values = directories                  

            End If    

        Next    

              ' Update the component in your copy of the site control file. Get the path  
             ' to the updated object, which could be used later to retrieve the instance.  
             Set SCICompPath = SCIComponent.Put_( , context)  
    Next  

    ' Commit the change to the actual site control file.  
    Set InParams = connection.Get("SMS_SiteControlFile").Methods_("CommitSCF").InParameters.SpawnInstance_  
    InParams.SiteCode = siteCode  
   connection.ExecMethod "SMS_SiteControlFile", "CommitSCF", InParams, , context  

 End Sub  
```  

```c#  
public void AddSmpFolder(  
    WqlConnectionManager connection,  
    string directory,  
    int maxClients,  
    int minDiskSpace,  
    int minDiskSpaceUnit,  
    string serverName,  
    string siteCode)  
{  
    try  
    {  
        // Set up folder string.  
        string smpSettings = "Directory=" +   
            directory +   
            ";MaxClients=" +   
            maxClients.ToString(CultureInfo.InvariantCulture) +  
            ";MinDiskSpace=" +   
            minDiskSpace.ToString(CultureInfo.InvariantCulture) +   
            ";MinDiskSpaceUnit=" +   
            minDiskSpaceUnit.ToString(CultureInfo.InvariantCulture) +  
            ";";  

        // Get state migration point properties from site control file.  
        IResultObject ro = connection.GetInstance(  
            "SMS_SCI_SysResUse.FileType=2,ItemName='[\"Display=\\\\" +  
            serverName +   
            "\\\"]MSWNET:[\"SMS_SITE=" +   
            siteCode + "\"]\\\\" +   
            serverName +  
            "\\,SMS State Migration Point',ItemType='System Resource Usage',SiteCode='" +  
            siteCode +   
            "'"  
            );  

        // Get directories.  
        Dictionary<string, IResultObject> embeddedPropertyLists = ro.EmbeddedPropertyLists;  

        string[] directories = embeddedPropertyLists["Directories"]["Values"].StringArrayValue; // Current directories.  

        List<string> directoriesList = new List<string>(); // convert to list.  
        foreach (string directoryName in directories)  
        {  
            directoriesList.Add(directoryName);  
        }  

        directoriesList.Add(smpSettings);  

        // Update the embedded property list.  
        embeddedPropertyLists["Directories"]["Values"].StringArrayValue = directoriesList.ToArray();  

        ro.EmbeddedPropertyLists = embeddedPropertyLists;  

        // Commit changes.  
        ro.Put();  
    }  
    catch (SmsException e)  
    {  
        Console.WriteLine("failed to update SMP settings" + e.Message);  
        throw;  
    }  
}  

```  

 The example method has the following parameters:  

| Parameter | Type | Description |
| --------- | ---- | ----------- |
|`connection`|-   Managed: `WqlConnectionManager`<br />-   VBScript: [SWbemServices](/windows/win32/wmisdk/swbemservices)|A valid connection to the SMS Provider.|  
|`context (VBScript)`|-   VBScript: `SWbemContext`|A valid context object. For more information, see [How to Add a Configuration Manager Context Qualifier by Using WMI](../../develop/core/understand/how-to-add-a-configuration-manager-context-qualifier-by-using-wmi.md).|  
|`directory`|-   Managed: `String`<br />-   VBScript: `String`|The folder to be added.|  
|`maxClients`|-   Managed: `Integer`<br />-   VBScript: `Integer`|The maximum number of supported clients.|  
|`minDiskSpace`|-   Managed: `Integer`<br />-   VBScript: `Integer`|The minimum disk space.|  
|`minDiskSpaceUnit`|-   Managed: `Integer`<br />-   VBScript: `Integer`|The minimum disk space unit.|  
|`serverName`|-   Managed: `String`<br />-   VBScript: `String`|The Configuration Manager server that the state migration point is running on.|  
|`siteCode`|-   Managed: `String`<br />-   VBScript: `String`|The site code for the site that is running the state migration point site role.|  

## Compiling the Code  
 The C# example has the following compilation requirements:  

### Namespaces  
 System  

 System.Collections.Generic  

 System.Text  

 Microsoft.ConfigurationManagement.ManagementProvider  

 Microsoft.ConfigurationManagement.ManagementProvider.WqlQueryEngine  

 System.Globalization  

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
