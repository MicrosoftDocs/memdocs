---
title: "Initiate a One-time Membership Evaluation for a Collection"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: c1733ce8-d443-4b0f-83f4-82f82d619c7c
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# How to Initiate a One-time Membership Evaluation for a Collection
### To Initiate a One-time Membership Evaluation  

1.  Set up a connection to the SMS Provider.  

2.  Get the specific collection instance by using the collection ID provided.  

3.  Refresh the collection membership using the [RequestRefresh](../../../../develop/reference/core/clients/collections/requestrefresh-method-in-class-sms_collection.md) method in the [SMS_Collection](../../../../develop/reference/core/clients/collections/sms_collection-server-wmi-class.md) class.  

## Example  
 The following example method refreshes the collection membership for a specific collection.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../../../develop/core/understand/calling-code-snippets.md).  

```vbs  
Sub RefreshCollection(connection, collectionID)    Dim collection    Set collection = connection.Get("SMS_Collection.CollectionID='" & collectionID & "'")    Call collection.RequestRefresh()End Sub  
```  

```c#  
public void RefreshCollection(WqlConnectionManager connection, string collectionID){    IResultObject collection = connection.GetInstance(string.Format("SMS_Collection.CollectionID='{0}'", collectionID));    collection.ExecuteMethod("RequestRefresh", null);}  
```  

 The example method has the following parameters:  

|Parameter|Type|Description|  
|---------------|----------|-----------------|  
|`connection`|-   Managed: `WqlConnectionManager`<br />-   VBScript: [SWbemServices](https://msdn.microsoft.com/library/aa393854.aspx)|A valid connection to the SMS Provider.|  
|`collectionID`|-   Managed: `String`<br />-   VBScript: `String`|Unique auto-generated ID containing eight characters. For more information, see the CollectionID property of [SMS_Collection Server WMI Class](../../../../develop/reference/core/clients/collections/sms_collection-server-wmi-class.md).|  

## Compiling the Code  
 The C# example requires:  

### Namespaces  
 System  

 Microsoft.ConfigurationManagement.ManagementProvider  

 Microsoft.ConfigurationManagement.ManagementProvider.WqlQueryEngine  

### Assembly  
 adminui.wqlqueryengine  

 microsoft.configurationmanagement.managementprovider  

 mscorlib  

## Robust Programming  
 For more information about error handling, see [About Configuration Manager Errors](../../../../develop/core/understand/about-configuration-manager-errors.md).  

## See Also  
 [Configuration Manager Collections](../../../../develop/core/clients/collections/collections.md)   
 [SMS_Collection Server WMI Class](../../../../develop/reference/core/clients/collections/sms_collection-server-wmi-class.md)
