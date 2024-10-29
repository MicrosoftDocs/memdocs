---
title: SMS_G_SYSTEM_DCMDeploymentNonCompliantAssetDetails Class
description: Learn how to use the SMS_G_SYSTEM_DCMDeploymentNonCompliantAssetDetails class in Configuration Manager to set non-compliant asset details for a deployment.
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: c85cfe8c-5a8b-470b-b781-3421d4177bb7
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_G_SYSTEM_DCMDeploymentNonCompliantAssetDetails Server WMI Class
The `SMS_G_SYSTEM_DCMDeploymentNonCompliantAssetDetails` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents non-compliant asset details for a deployment.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_G_SYSTEM_DCMDeploymentNonCompliantAssetDetails : SMS_G_System  
{  
    UInt32 AssignmentID;  
    UInt32 BL_ID;  
    UInt32 CI_ID;  
    UInt32 ResourceID;  
    UInt32 Rule_ID;  
    UInt32 RuleSubState;  
};  
```  

## Methods  
 The `SMS_G_SYSTEM_DCMDeploymentNonCompliantAssetDetails` class does not define any methods.  

## Properties  
 `AssignmentID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, not_null, read]  

 See [SMS_DCMDeploymentErrorAssetDetails Server WMI Class](../../../develop/reference/compliance/sms_dcmdeploymenterrorassetdetails-server-wmi-class.md).  

 `BL_ID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, not_null, read]  

 See [SMS_DCMDeploymentErrorAssetDetails Server WMI Class](../../../develop/reference/compliance/sms_dcmdeploymenterrorassetdetails-server-wmi-class.md).  

 `CI_ID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, not_null, read]  

 See [SMS_DCMDeploymentErrorAssetDetails Server WMI Class](../../../develop/reference/compliance/sms_dcmdeploymenterrorassetdetails-server-wmi-class.md).  

 `ResourceID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Unique ID, supplied by Configuration Manager, that identifies a client resource. This ID is not unique across sites.  

 `Rule_ID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, not_null, read]  

 Rule ID.  

 `RuleSubState`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, not_null, read]  

 Rule sub-status type.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  
