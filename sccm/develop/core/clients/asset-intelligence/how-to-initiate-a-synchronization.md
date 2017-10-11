---
title: "Initiate a Synchronization"
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
ms.assetid: 6b484801-89a1-4707-ac9f-46da72365fdfsearchScope: - ConfigMgr SDK
caps.latest.revision: 10
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# How to Initiate a Synchronization
The Asset Intelligence catalog can be refreshed manually, outside the normal synchronization schedule. A manual refresh is accomplished by using the [RequestCatalogUpdate](../../../../develop/reference/core/clients/asset-intelligence/requestcatalogupdate-method-in-class-sms_aiproxy.md) method on the [SMS_AIProxy Server WMI Class](../../../../develop/reference/core/clients/asset-intelligence/sms_aiproxy-server-wmi-class.md).  

> [!IMPORTANT]
>  This method can only be called once within a 12 hours period, subsequent method calls will not work.  

### Refresh the Asset Intelligence catalog  

1.  Set up a connection to the SMS Provider. For more information, see [About the SMS Provider in Configuration Manager](../../../../develop/core/understand/about-the-sms-provider-in-configuration-manager.md).  

2.  Query the SMS Provider for the [SMS_AIProxy](../../../../develop/reference/core/clients/asset-intelligence/sms_aiproxy-server-wmi-class.md) instance that you want refresh the catalog on.  

3.  Call the SMS_AIProxy class [RequestCatalogUpdate](../../../../develop/reference/core/clients/asset-intelligence/requestcatalogupdate-method-in-class-sms_aiproxy.md) method to run an action on the collection.  

## Example  
 The following example method runs the refresh on the provided server.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../../../develop/core/understand/calling-code-snippets.md).  

```vbs  
Function InitateSync(connection, serverName)    On Error Resume Next    Dim classObj: Set classObj = connection.Get("SMS_AIProxy")    Dim inParams: Set inParams = classObj.Methods_("RequestCatalogUpdate").InParameters.SpawnInstance_()    Dim outParams        inParams.Properties_.Item("ProxyName") = serverName        Set outParams = connection.ExecMethod("SMS_AIProxy", "RequestCatalogUpdate", inParams)    If Err.Number <> 0 Then         InitateSync = False    Else        InitateSync = True    End If    On Error Goto 0End Function  
```  

```c#  
public void InitateSync(WqlConnectionManager connection, string serverName){    try    {        Dictionary<string, object> inParams = new Dictionary<string, object>();        IResultObject classObj = connection.GetClassObject("SMS_AIProxy");        inParams.Add("ProxyName", serverName);        Console.WriteLine("Requesting catalog update on server " + serverName);        classObj.ExecuteMethod("RequestCatalogUpdate", inParams);    }    catch (SmsException ex)    {        Console.WriteLine(String.Format("Failed to request catalog update on server {0}. Error: {1}", serverName, ex.Message));        throw;    }}  
```  

 The example method has the following parameters:  

|Parameter|Type|Description|  
|---------------|----------|-----------------|  
|connection|Managed: `WqlConnectionManager`<br /><br /> VBScript: [SWbemServices](https://msdn.microsoft.com/library/aa393854.aspx)|A valid connection to the provider.|  
|serverName|Managed: `String`<br /><br /> VBScript: `String`|Name of the server to run the refresh on. This name maps to the `ProxyName` property of an `SMS_AIProxy` instance.|  

## Compiling the Code  
 The C# example requires:  

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
 For more information about error handling, see [About Configuration Manager Errors](../../../../develop/core/understand/about-configuration-manager-errors.md).  

## .NET Framework Security  
 For more information about securing Configuration Manager applications, see [Securing Configuration Manager Applications](../../../../develop/core/understand/securing-configuration-manager-applications.md).
