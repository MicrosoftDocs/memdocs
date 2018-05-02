---
title: "SMS_DCMDeploymentCompliantAssetDetails Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 3f694e79-24c2-4c18-b4b9-095fa12df1e8
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_DCMDeploymentCompliantAssetDetails Server WMI Class
The `SMS_DCMDeploymentCompliantAssetDetails` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents compliant asset details for a deployment.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_DCMDeploymentCompliantAssetDetails : SMS_BaseClass  
{  
    UInt32 AssetID;  
    String AssetName;  
    UInt32 AssetType;  
    UInt32 AssignmentID;  
    String AssignmentUniqueID;  
    UInt32 BL_ID;  
    String BLName;  
    UInt32 BLRevision;  
    UInt32 CI_ID;  
    String CIName;  
    UInt32 ClientType;  
    Boolean IsMachineAssignedToUser;  
    Boolean IsMachineChangesPersisted;  
    Boolean IsVM;  
    UInt32 Revision;  
    UInt32 StatusType;  
    String TargetCollectionID;  
    String VMHostName;  
};  
```  

## Methods  
 The `SMS_DCMDeploymentCompliantAssetDetails` class does not define any methods.  

## Properties  
 `AssetID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 The ID of the asset.  

 `AssetName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key, not_null, read]  

 Name of the asset.  

 `AssetType`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [enumeration, not_null, read]  

 Type of the asset. Possible values are:  

|||  
|-|-|  
|0|USER|  
|1|MACHINE|  

 `AssignmentID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, not_null, read]  

 The ID of the configuration item assignment. This ID is unique only for the site.  

 `AssignmentUniqueID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 The unique ID of the configuration item assignment. This ID is unique across sites.  

 `BL_ID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, not_null, read]  

 Identifier of the baseline deployed using this assignment.  

 `BLName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Name of the baseline deployed using this assignment.  

 `BLRevision`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Baseline version that is deployed using this assignment.  

 `CI_ID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, not_null, read]  

 The unique ID of the configuration item. This ID is unique only for the site.  

 `CIName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 The name of the configuration item.  

 `ClientType`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [enumeration, read]  

 Type of client. Possible values are:  

|||  
|-|-|  
|1|WINDOWS_CLIENT|  
|2|WINDOWS_MOBILE|  

 `IsMachineAssignedToUser`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read]  

 `true` if the computer is assigned to a user.  

 `IsMachineChangesPersisted`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read]  

 `true` if the virtual machine changes are persisted.  

 `IsVM`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read]  

 `true` if this is a virtual machine.  

 `Revision`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Revision number for the configuration item.  

 `StatusType`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, not_null, read]  

 Status of the deployment to the targeted asset. Possible values are:  

|||  
|-|-|  
|1|Success|  
|2|InProgress|  
|4|Unknown|  

 `TargetCollectionID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 The ID of the collection to which the assignment is targeted.  

 `VMHostName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Virtual machine host name.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).
