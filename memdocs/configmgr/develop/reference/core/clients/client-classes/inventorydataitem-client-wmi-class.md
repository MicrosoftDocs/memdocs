---
title: "InventoryDataItem Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 45f7e59f-85d2-4594-9fd7-79b3e6de8c25
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# InventoryDataItem Client WMI Class
In Configuration Manager, the `InventoryDataItem` class is a client Windows Management Instrumentation (WMI) class that defines an inventory collection query.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class InventoryDataItem : SMS_InventoryAgent_Policy  
{  
      String AssocClass[];  
      InventoryDataContext Context[];  
      String DataItemID;  
      String Filter;  
      String InventoryActionID;  
      String ItemClass;  
      String Namespace;  
      String PolicyID;  
      String PolicyInstanceID;  
      UInt32 PolicyPrecedence;  
      String PolicyRuleID;  
      String PolicySource;  
      String PolicyVersion;  
      String Properties;  
      PropertyRule ReportRules[];  
      UInt32 Timeout;  
};  
```  

## Methods  
 The `InventoryDataItem` class does not define any methods.  

## Properties  
 `AssocClass`  
 Data type: `String` Array  

 Access type: Read/Write  

 Qualifiers: None  

 Reserved for future use.  

 `Context`  
 Data type: `InventoryDataContext` Array  

 Access type: Read/Write  

 Qualifiers: None  

 Optional context qualifier for the class query. For more information, see [InventoryDataContext Client WMI Class](../../../../../develop/reference/core/clients/client-classes/inventorydatacontext-client-wmi-class.md).  

 `DataItemID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [realkey]  

 Unique identifier for an [InventoryDataItem Client WMI Class](../../../../../develop/reference/core/clients/client-classes/inventorydataitem-client-wmi-class.md) object.  

 `Filter`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Class query property filter, for example, NumberOfProcessors=1 AND DomainRole=1. The Inventory Agent uses this field to build the WQL WHERE clause for the class instance query.  

 `InventoryActionID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 ID that matches the `InventoryActionID` value for an associated [InventoryAction Client WMI Class](../../../../../develop/reference/core/clients/client-classes/inventoryaction-client-wmi-class.md) object. The Inventory Agent uses this value to find the [InventoryDataItem Client WMI Class](../../../../../develop/reference/core/clients/client-classes/inventorydataitem-client-wmi-class.md) class for a particular inventory action.  

 `ItemClass`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [realkey]  

 WMI instance class to query, for example, Win32_ComputerSystem.  

 `Namespace`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [realkey]  

 WMI namespace to query, for example, \\\\\\\\.\\\root\\\cimv2.  

 `PolicyID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Unique ID of the policy.  

 `PolicyInstanceID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Unique ID of the policy instance.  

 `PolicyPrecedence`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Precedence for the policy.  

 `PolicyRuleID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Unique ID of the rule used to create the policy.  

 `PolicySource`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Source of the policy.  

 `PolicyVersion`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Version of the policy.  

 `Properties`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Class properties to query, for example, Domain, Name, and UserName. The Inventory Agent uses this property to build the WQL SELECT clause for the class instance query.  

 `ReportRules`  
 Data type: `PropertyRule` Array  

 Access type: Read/Write  

 Qualifiers: None  

 Reserved for future use.  

 `Timeout`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Maximum time that the agent waits for the `InventoryDataItem` class query to complete before canceling the query. This property overrides `DefaultTimeOut` property in the [InventoryAction Client WMI Class](../../../../../develop/reference/core/clients/client-classes/inventoryaction-client-wmi-class.md) class.  

## Remarks  
 The Inventory Agent uses each instance of this class to build a WMI query for the referenced class; for example, `SELECT Name FROM Win32_ComputerSystem WHERE  DomainRole=1`.  

 The Inventory Agent collects items returned by [InventoryDataItem Client WMI Class](../../../../../develop/reference/core/clients/client-classes/inventorydataitem-client-wmi-class.md) queries and builds a report based on the results. Each `InventoryDataItem` object contains a reference to an [InventoryAction Client WMI Class](../../../../../develop/reference/core/clients/client-classes/inventoryaction-client-wmi-class.md) object. Multiple `InventoryDataItem` queries are used to build the combined report for an `InventoryAction` object.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).  

## See Also  
 [Inventory Agent Client WMI Classes](../../../../../develop/reference/core/clients/client-classes/inventory-agent-client-wmi-classes.md)   
 [InventoryAction Client WMI Class](../../../../../develop/reference/core/clients/client-classes/inventoryaction-client-wmi-class.md)   
 [InventoryDataContext Client WMI Class](../../../../../develop/reference/core/clients/client-classes/inventorydatacontext-client-wmi-class.md)
