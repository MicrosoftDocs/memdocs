---
title: "SMS_ReplicationGroup Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 66b11714-672c-4a84-80e4-8e173afee891
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_ReplicationGroup Server WMI Class
The `SMS_ReplicationGroup` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that contains replication group data.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_ReplicationGroup : SMS_BaseClass  
{  
    UInt32 ID;  
    Boolean IsPush;  
    String ReplicationGroup;  
    String ReplicationPattern;  
    UInt16 ReplicationPriority;  
    String SecurityKey;  
    UInt32 Status;  
    UInt32 SyncInterval;  
    String TransportType;  
};  
```  

## Methods  
 The following table lists the methods in the `SMS_ReplicationGroup` class.  

|Method|Description|  
|------------|-----------------|  
|[InitializeData Method in Class SMS_ReplicationGroup](../../../../../develop/reference/core/servers/configure/initializedata-method-in-class-sms_replicationgroup.md)|Reinitializes the data in a specific replication group between two specified sites.|  

## Properties  
 `ID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key]  

 Unique identifier for the replication group.  

 `IsPush`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: none  

 `true` if this is site data. `false` if this is global data.  

 `ReplicationGroup`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: none  

 Name of the replication group used in the data replication service. Each replication group contains a set of tables to be replicated together.  

 `ReplicationPattern`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: none  

 Replication pattern. Possible values are:  

|Value|Replication pattern|  
|-|-|  
|Global|The data is replicated across all primary sites and CAS in the hierarchy.|  
|Site|The data is replicated up to the CAS in the hierarchy.|  
|Global_proxy|The data is replicated to secondary sites in the hierarchy.|  

 `ReplicationPriority`  
 Data type: `UInt16`  

 Access type: Read-only  

 Qualifiers: none  

 Priority of data replication using data replication service.  

 `SecurityKey`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: none  

 Security key value for RBAC to verify that the SDK user has permission to read the instance of `SMS_ReplicationGroup`.  

 `Status`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: none  

 The current status of replicating data for tables in the replication group.  

 `SyncInterval`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: none  

 How often the data replication service checks to see if there are any changes in the tables within the replication group to be replicated.  

 `TransportType`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: none  

 Type of transportation supported by data replication service.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Configuration Manager Site Configuration Server WMI Classes](../../../../../develop/reference/core/servers/configure/site-configuration-server-wmi-classes.md)
