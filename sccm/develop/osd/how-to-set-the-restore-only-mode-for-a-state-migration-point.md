---
title: "Set the Restore-Only Mode for a State Migration Point"
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
ms.assetid: e2cb40c3-7b94-4586-a5c2-75b1ed52f571searchScope: - ConfigMgr SDK
caps.latest.revision: 11
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# How to Set the Restore-Only Mode for a State Migration Point
In System Center Configuration Manager, you configure the operating system deployment state migration point to reject new requests to store user data by setting the **SMPQuiesceState** embedded property.  

 **SMPQuiesceState** has two possible values.  

|Value|Definition|  
|-----------|----------------|  
|0|Restore-only mode is turned off.|  
|1|Restore-only mode is turned on.|  

### To set the restore only mode for a state migration point  

1.  Set up a connection to the SMS Provider. For more information, see [About the SMS Provider in Configuration Manager](../../develop/core/understand/about-the-sms-provider-in-configuration-manager.md).  

2.  Make a connection to the state migration point resources section of the site control file.  

3.  Get the embedded properties.  

4.  Update **SMPQuiesceState**.  

5.  Commit the changes to the site control file.  

## Example  
 The following example method sets the restore-only mode based on supplied value.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../develop/core/understand/calling-code-snippets.md).  

```vbs  
Sub SetRestoreOnlyMode(connection,          _  
                       context,           _  
                       siteCode,               _  
                       enableRestoreOnlyMode)  

    ' Load site control file and get SMS State Migration Point section.  
    connection.ExecMethod "SMS_SiteControlFile.Filetype=1,Sitecode=""" & siteCode & """", "Refresh", , , context  

    Query = "SELECT * FROM SMS_SCI_SysResUse " & _  
            "WHERE RoleName = 'SMS State Migration Point' " & _  
            "AND SiteCode = '" & siteCode & "'"  

    Set SCIComponentSet = connection.ExecQuery(Query, , , context)  

    ' Only one instance is returned from the query.  
    For Each SCIComponent In SCIComponentSet  

         ' Display state migration point server name.  
         wscript.echo "SMS State Migration Point Server: " & SCIComponent.NetworkOSPath                                      

        ' Loop through the array of embedded property instances.  
        For Each vProperty In SCIComponent.Props  

            ' Setting: SMPQuiesceState  
            If vProperty.PropertyName = "SMPQuiesceState" Then  
                wscript.echo " "  
                wscript.echo vProperty.PropertyName  
                wscript.echo "Current value " &  vProperty.Value                 

                ' Modify the value.  
                vProperty.Value = enableRestoreOnlyMode  
                wscript.echo "New value " & enableRestoreOnlyMode  
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
public void SetRestoreOnlyMode(  
    WqlConnectionManager connection,  
    string server,   
    string siteCode,   
    bool enableRestoreOnlyMode)  
{  
    try  
    {  
        // Get the site control file.  
        IResultObject ro = connection.GetInstance("SMS_SCI_SysResUse.FileType=2,ItemName='[\"Display=\\\\" + server + "\\\"]MSWNET:[\"SMS_SITE=" + siteCode + "\"]\\\\" + server + "\\,SMS State Migration Point',ItemType='System Resource Usage',SiteCode='" + siteCode + "'");  

        // Get the embedded properties.  
        Dictionary<string, IResultObject> embeddedProperties = ro.EmbeddedProperties;  

        // Set the restore only mode.  
        embeddedProperties["SMPQuiesceState"]["Value"].BooleanValue = enableRestoreOnlyMode;  

        ro.EmbeddedProperties = embeddedProperties;  

        // Commmit the changes.  
        ro.Put();  
    }  
    catch (SmsException e)  
    {  
        Console.WriteLine("Failed to set restore only mode" + e.Message);  
        throw;  
    }  
}  
```  

 The example method has the following parameters:  

||||  
|-|-|-|  
|Parameter|Type|Description|  
|`connection`|-   Managed: `WqlConnectionManager`<br />-   VBScript: [SWbemServices](https://msdn.microsoft.com/library/aa393854.aspx)|A valid connection to the SMS Provider.|  
|`context (VBScript)`|-   VBScript: `SWbemContext`|A valid context object. For more information, see [How to Add a Configuration Manager Context Qualifier by Using WMI](../../develop/core/understand/how-to-add-a-configuration-manager-context-qualifier-by-using-wmi.md).|  
|`server`|-   Managed: `String`<br />-   VBScript: `String`|The Configuration Manager server that the state migration point is running on.|  
|`siteCode`|-   Managed: `String`<br />-   VBScript: `String`|The Configuration Manager site code.|  
|`enableRestoreOnlyMode`|-   Managed: `Boolean`<br />-   VBScript: `Integer`|Sets the restore only mode.<br /><br /> -   Managed: `true` turns restore only mode on; otherwise `false`.<br />-   VBScript: `1` turns restore mode on; otherwise `0`.|  

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
