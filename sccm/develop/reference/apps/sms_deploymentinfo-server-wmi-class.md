---
title: "SMS_DeploymentInfo Class"
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
ms.assetid: 0fd6b2bb-50f6-440e-a603-937d0b37dd97searchScope: - ConfigMgr SDK
caps.latest.revision: 9
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_DeploymentInfo Server WMI Class
The `SMS_DeploymentInfo` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents information for all types of deployment.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_DeploymentInfo : SMS_BaseClass  
{  
    String CollectionID;  
    String CollectionName;  
    String DeploymentID;  
    UInt32 DeploymentIntent;   
    String DeploymentName;  
    UInt32 DeploymentType;  
    UInt32 DeploymentTypeID;  
    String TargetID;  
    String TargetName;  
    UInt32 TargetSecurityTypeID;  
    String TargetSubName;  
};  
```  

## Methods  
 The following table lists the methods in the `SMS_DeploymentInfo` class.  

|Method|Description|  
|------------|-----------------|  
|[GetDeployments Method in Class SMS_Deployment_Info](../../../develop/reference/apps/getdeployments-method-in-class-sms_deployment_info.md)|Gets advertisement identifier or Assignment identifier and related type for a deployment that is deployed to the specified resource.|  

## Properties  
 `CollectionID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Existing collection to which the advertisement is targeted.  

 `CollectionName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Name of the collection to which the advertisement is advertising.  

 `DeploymentID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Unique auto-generated key.  

 `DeploymentIntent`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Purpose of the deployment.  

 `DeploymentName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Plain-text name of the deployment (advertisement/assignment).  

 `DeploymentType`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Deployment type.  

 `DeploymentTypeID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [enumeration, key]  

 Type identifier of the deployment.  

 `TargetID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Unique identifier of the target. For package, it is package ID, for a configuration item, it is the Unique_ID.  

 `TargetName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Package name, if the target is a package. Application name, if it is application. Update name, if it is update.  

 `TargetSecurityTypeID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Security type identifier of the deployment.  For example, if it is package, this value is 2.  

 `TargetSubName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Program name if it is package, otherwise leave this value is empty.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).
