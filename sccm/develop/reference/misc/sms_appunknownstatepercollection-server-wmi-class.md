---
title: "SMS_AppUnknownStatePerCollection Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: f95f3e04-9b31-44f8-8bfc-2657a560d780
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_AppUnknownStatePerCollection Server WMI Class
The `SMS_AppUnknownStatePerCollection` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents unknown application state per collection.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_AppUnknownStatePerCollection : SMS_BaseClass  
{  
    UInt32 AppCI;  
    String AppName;  
    UInt32 AssignmentID;  
    String AssignmentUniqueID;  
    UInt32 Category;  
    String CollectionID;  
    String CollectionName;  
    UInt32 DeploymentIntent;  
    DateTime StartTime;  
    UInt32 Total;  
};  
```  

## Methods  
 The `SMS_AppUnknownStatePerCollection` class does not define any methods.  

## Properties  
 `AppCI`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 See [SMS_AppDeploymentAssetDetails Server WMI Class](../../../develop/reference/apps/sms_appdeploymentassetdetails-server-wmi-class.md).  

 `AppName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_AppDeploymentAssetDetails Server WMI Class](../../../develop/reference/apps/sms_appdeploymentassetdetails-server-wmi-class.md).  

 `AssignmentID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, not_null, read]  

 See [SMS_AppDeploymentAssetDetails Server WMI Class](../../../develop/reference/apps/sms_appdeploymentassetdetails-server-wmi-class.md).  

 `AssignmentUniqueID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 See [SMS_AppDeploymentAssetDetails Server WMI Class](../../../develop/reference/apps/sms_appdeploymentassetdetails-server-wmi-class.md).  

 `Category`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, not_null, read]  

 Specific unknown state.   

 `CollectionID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 See [SMS_AppDeploymentAssetDetails Server WMI Class](../../../develop/reference/apps/sms_appdeploymentassetdetails-server-wmi-class.md).  

 `CollectionName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 See [SMS_AppDeploymentAssetDetails Server WMI Class](../../../develop/reference/apps/sms_appdeploymentassetdetails-server-wmi-class.md).  

 `DeploymentIntent`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_AppDeploymentAssetDetails Server WMI Class](../../../develop/reference/apps/sms_appdeploymentassetdetails-server-wmi-class.md).  

 `StartTime`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_AppDeploymentAssetDetails Server WMI Class](../../../develop/reference/apps/sms_appdeploymentassetdetails-server-wmi-class.md).  

 `Total`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Total number of resources in this state.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).
