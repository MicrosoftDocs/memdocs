---
title: "SMS_Query Class"
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
ms.assetid: 92214631-1cd5-45ac-a7d9-f49c32530be0searchScope: - ConfigMgr SDK
caps.latest.revision: 13
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_Query Server WMI Class
The `SMS_Query` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in System Center Configuration Manager, that serves as a container for predefined queries.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_Query : SMS_BaseClass  
{  
   String Comments;  
   String Expression;  
   String LimitToCollectionID;  
   String LocalizedCategoryInstanceNames[];  
   String Name;  
   String QueryID;  
   String ResultAliasNames[];  
   String ResultColumnsNames[];  
   String TargetClassName;  
};  
```  

## Methods  
 The following table lists the methods in `SMS_Query`.  

|Method|Description|  
|------------|-----------------|  
|[CreateCCRs Method in Class SMS_Query](../../../../../develop/reference/core/clients/manage/createccrs-method-in-class-sms_query.md)|Generates client configuration requests (CCRs) for the query.|  
|[FindResourceSite Method in Class SMS_Query](../../../../../develop/reference/core/clients/manage/findresourcesite-method-in-class-sms_query.md)|Gets site code information for resources from SQL.|  

## Properties  
 `Comments`  
 Data type: **String**  

 Access type: Read/Write  

 Qualifiers: None  

 Comments to document the query. The default value is "".  

 `Expression`  
 Data type: **String**  

 Access type: Read/Write  

 Qualifiers: None  

 WMI Query Language (WQL) text for the query. The default value is "".  

 `LimitToCollectionID`  
 Data type: **String**  

 Access type: Read/Write  

 Qualifiers: None  

 ID of a collection. This ID is used to limit the query results to resources that are members of the collection.  

 `LocalizedCategoryInstanceNames`  
 Data type: **String** Array  

 Access type: Read  

 Qualifiers: None  

 Localized names of the categories to which the resource belongs.  

 `Name`  
 Data type: **String**  

 Access type: Read/Write  

 Qualifiers: None  

 Name of the query as shown in the Configuration Manager console. The default value is "".  

 `QueryID`  
 Data type: **String**  

 Access type: Read-only  

 Qualifiers: [read, key]  

 Unique auto-generated ID for the query.  

 `ResultAliasNames`  
 Data type: **String** Array  

 Access type: Read-only  

 Qualifiers: None  

 If you specify an alias in the query expression, this array will be filled with the aliases.  

 `ResultColumnsNames`  
 Data type: **String** Array  

 Access type: Read-only  

 Qualifiers: None  

 If you specify an alias in the query expression, this array will be filled with the resulting alias columns names.  

 `TargetClassName`  
 Data type: **String**  

 Access type: Read/Write  

 Qualifiers: None  

 Name of the target class, found in the FROM clause of the query. The default value is "".  

 This name is arbitrary for queries that perform a JOIN operation. The Configuration Manager console uses this property for display purposes to give the user an idea of the data that the query retrieves.  

## Remarks  
 Class qualifiers for this class include:  

-   Secured  

-   DisplayName("Query")  

 For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

 You can use `SMS_Query` to persist valid queries that can be used later in an application or that can be run from the System Center Configuration Manager console.  

 Instances of this class with the `TargetClassName` property set to an [SMS_StatusMessage Server WMI Class](../../../../../develop/reference/core/servers/manage/sms_statusmessage-server-wmi-class.md) object appear in the System Status node in the System Center Configuration Manager console. All other instances appear in the Queries node.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Resource Management Server WMI Classes](../../../../../develop/reference/core/clients/manage/configuration-manager-resource-management-server-wmi-classes.md)   
 [SMS_Collection Server WMI Class](../../../../../develop/reference/core/clients/collections/sms_collection-server-wmi-class.md)   
 [SMS_StatusMessage Server WMI Class](../../../../../develop/reference/core/servers/manage/sms_statusmessage-server-wmi-class.md)
