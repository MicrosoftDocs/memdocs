---
title: "Connect to an SMS Provider by Using Managed Code"
titleSuffix: "Configuration Manager"
description: "To connect to an SMS Provider, use WqlConnectionManager.Connect."
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: how-to
ms.assetid: 2a435561-01b7-45d5-b7cf-89fc1845025f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# How to Connect to an SMS Provider in Configuration Manager by Using Managed Code
To connect to an SMS Provider, use **WqlConnectionManager.Connect**. After it is connected, **WqlConnectionManager.Connect** has methods to query, create, delete, and otherwise use Configuration Manager Windows Management Instrumentation (WMI) objects.  

> [!NOTE]
>  **WqlConnectionManager.Connect** is a WMI-specific derivation of [ConnectionManagerBase](/previous-versions/system-center/developer/cc147366(v=msdn.10)).  

 If you are connecting to a local SMS Provider, you do not supply user credentials. If you are connecting to a remote SMS Provider, you do not need to supply user credentials if the if the current user/computer context has permissions on the remote SMS Provider.  

 If you do not have access privileges on the remote SMS Provider, or if you want to use a different user account, then you must supply user credentials for a user account that has access privileges.  

 **WQLConnectionManager.Connection** requires a [SmsNamedValuesDictionary](/previous-versions/system-center/developer/cc147435(v=msdn.10)) object. This can be used to store cached information such as the computer name.  

 It is pre-populated with a number of values that can be used in your application.  

|Value|Description.|  
|-----------|------------------|  
|ProviderLocation|The provider location. For example,<br /><br /> \\\\<ComputerName\>\ROOT\sms:SMS_ProviderLocation.SiteCode="XXX".|  
|ProviderMachineName|The provider computer. For example, \\\ComputerName.|  
|Connection|The connection path. For example, \\\ComputerName\root\sms\site_XXX.|  
|ConnectedSiteCode|The site code for the Configuration Manager site that the connection is connected to. For example, XXX.|  
|ServerName|The computer name, for example, COMPUTERNAME.|  
|SiteName|The Configuration Manager site code. For example, Central Site.|  
|ConnectedServerVersion|Ther version for the connected server. For example, 4.00.5830.0000|  
|BuildNumber|The Configuration Manager installation build number. For example, 5830.|  

> [!NOTE]
>  The [SmsNamedValuesDictionary](/previous-versions/system-center/developer/cc147435(v=msdn.10)) object is not the context qualifier information passed to the provider. For more information, see [How to Add a Configuration Manager Context Qualifier by Using Managed Code](../../../develop/core/understand/how-to-add-a-configuration-manager-context-qualifier-by-using-managed-code.md).  

### To connect to the SMS Provider  

1.  Create a [SmsNamedValuesDictionaryObject](/previous-versions/system-center/developer/cc147435(v=msdn.10)).  

2.  Create an instance of the **WqlConnectionManager** class and call the *[Connect]* method passing the server name, and if the server name is remote, the user name and password.  

3.  Use the **WqlConnectionManager** object to connect to the provider.  

## Example  
 The following example method connects to the SMS Provider on a local or remote computer. If `servername` is remote, the method uses the supplied user name and password to connect to the remote computer. If you want to use the current user context, for the remote connection, change the code so that it does not pass the user name and password. If the connection is successful, a **WqlConnectionManager** object is returned.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../../develop/core/understand/calling-code-snippets.md).  

```  
public WqlConnectionManager Connect(string serverName, string userName, string userPassword)  
{  
    try  
    {  
        SmsNamedValuesDictionary namedValues = new SmsNamedValuesDictionary();  
        WqlConnectionManager connection = new WqlConnectionManager(namedValues);  

        if (System.Net.Dns.GetHostName().ToUpper() == serverName.ToUpper())  
        {  
            // Connect to local computer.  
            connection.Connect(serverName);  
        }  
        else  
        {  
            // Connect to remote computer.  
            connection.Connect(serverName, userName, userPassword);  
        }  

        return connection;  
    }  
    catch (SmsException e)  
    {  
        Console.WriteLine("Failed to Connect. Error: " + e.Message);  
        return null;  
    }  
    catch (UnauthorizedAccessException e)  
    {  
        Console.WriteLine("Failed to authenticate. Error:" + e.Message);  
        return null;  
    }  
}  

```  

## Compiling the Code  

### Namespaces  
 System  

 System.Collections.Generic  

 System.ComponentModel  

 Microsoft.ConfigurationManagement.ManagementProvider  

 Microsoft.ConfigurationManagement.ManagementProvider.WqlQueryEngine  

 Microsoft.ManagementConsole  

### Assembly  
 microsoft.configurationmanagement.managementprovider  

 adminui.wqlqueryengine  

 Microsoft.ManagementConsole  

## Robust Programming  
 The Configuration Manager exceptions that can be raised are [SmsConnectionException](/previous-versions/system-center/developer/cc147431(v=msdn.10)) and [SmsQueryException](/previous-versions/system-center/developer/cc147436(v=msdn.10)). These can be caught together with [SmsException](/previous-versions/system-center/developer/cc147433(v=msdn.10)).  

## .NET Framework Security  
 [UnauthorizedAccessException](/dotnet/api/system.unauthorizedaccessexception) is raised when the wrong credentials are passed to **WqlConnectionManager.Connect**.  

## See Also  
 [SMS Provider fundamentals](sms-provider-fundamentals.md)
 [How to Add a Configuration Manager Context Qualifier Using Managed Code](../../../develop/core/understand/how-to-add-a-configuration-manager-context-qualifier-by-using-managed-code.md)   
 [Objects overview](configuration-manager-objects-overview.md)
