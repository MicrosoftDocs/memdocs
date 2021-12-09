---
title: "InventoryAction Client WMI Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 74ac1a03-44e0-477f-b5da-5e74e004a1e9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# InventoryAction Client WMI Class
In Configuration Manager, the `InventoryAction` class is a client Windows Management Instrumentation (WMI) class that associates a set of queries with reporting details, tying together the item to report and the destination of the report.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class InventoryAction : SMS_InventoryAgent_Policy  
{  
      UInt32 DefaultTimeout;  
      String Description;  
      String InventoryActionID;  
      String InventoryActionLastUpdateTime;  
      String PolicyID;  
      String PolicyInstanceID;  
      UInt32 PolicyPrecedence;  
      String PolicyRuleID;  
      String PolicySource;  
      String PolicyVersion;  
      String ReportDestination;  
      UInt32 ReportTimeout;  
      String ReportType;  
};  
```  

## Methods  
 The `InventoryAction` class does not define any methods.  

## Properties  
 `DefaultTimeout`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Maximum time, by default, that the agent waits for each `InventoryDataItem` class query before canceling the query. The individual `InventoryDataItem` instances can override this default timeout.  

 `Description`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Text field that describes the inventory action. Possible values are:  

- Hardware  

- Software  

- Discovery  

  `InventoryActionID`  
  Data type: `String`  

  Access type: Read/Write  

  Qualifiers: [realkey]  

  Unique ID for the inventory action. Possible values are:  

| Inventory Action ID type | Value |
| ------------------------ | ----- |
|Discovery|{00000000-0000-0000-0000-000000000003}|  
|Hardware Inventory|{00000000-0000-0000-0000-000000000001}|  
|Software Inventory|{00000000-0000-0000-0000-000000000002}|  
|SoftwareFileCollection|{00000000-0000-0000-0000-000000000010}|  
|IDMIF collection|{00000000-0000-0000-0000-000000000011}|  

 `InventoryActionLastUpdateTime`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Timestamp of the last update to the InventoryAction instance.  

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

 Qualifiers: Key  

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

 `ReportDestination`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Destination address for the generated report.  

 `ReportTimeout`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Maximum time that the client messaging framework attempts to transmit the report if the destination endpoint is unreachable.  

 `ReportType`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Type of inventory report. Possible values are:  

| Value | Description |
| ----- | ----------- |
|Full|Report contains all instances collected by the associated `InventoryDataItem` queries.|  
|Delta|Report contains instances that have changed since the last report|  
|Resync|Report contains instances in full report and also is triggered by a site policy resynchronization request|  

## Remarks  
 Three predefined inventory actions are provided through the site policy: hardware inventory, data discovery, and software inventory. For each of these inventory actions, the Inventory Agent generates a report by using the associated [InventoryDataItem Client WMI Class](../../../../../develop/reference/core/clients/client-classes/inventorydataitem-client-wmi-class.md) queries and sends the generated report to the specified destination.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).  

## See Also  
 [Inventory Agent Client WMI Classes](../../../../../develop/reference/core/clients/client-classes/inventory-agent-client-wmi-classes.md)   
 [InventoryDataItem Client WMI Class](../../../../../develop/reference/core/clients/client-classes/inventorydataitem-client-wmi-class.md)
