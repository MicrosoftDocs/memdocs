---
title: "SMS_AppUnknownStatePerClient Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: cc02c9dc-9bc4-4ab5-a39d-12a76b93ad6d
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_AppUnknownStatePerClient Server WMI Class
The `SMS_AppUnknownStatePerClient` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents unknown application state per client.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_AppUnknownStatePerClient : SMS_BaseClass  
{  
    UInt32 AppCI;  
    String AppName;  
    UInt32 AssignmentID;  
    String AssignmentUniqueID;  
    UInt32 Category;  
    String CollectionID;  
    String CollectionName;  
    UInt32 DeploymentIntent;  
    String MachineName;  
    DateTime StartTime;  
    String UserName;  
};  
```  

## Methods  
 The `SMS_AppUnknownStatePerClient` class does not define any methods.  

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

 Qualifiers: [read]  

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

 `MachineName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key, not_null, read]  

 See [SMS_AppDeploymentAssetDetails Server WMI Class](../../../develop/reference/apps/sms_appdeploymentassetdetails-server-wmi-class.md).  

 `StartTime`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_AppDeploymentAssetDetails Server WMI Class](../../../develop/reference/apps/sms_appdeploymentassetdetails-server-wmi-class.md).  

 `UserName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key, not_null, read]  

 See [SMS_AppDeploymentAssetDetails Server WMI Class](../../../develop/reference/apps/sms_appdeploymentassetdetails-server-wmi-class.md).  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).
