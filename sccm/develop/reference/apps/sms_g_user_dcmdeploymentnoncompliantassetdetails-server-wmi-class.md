---
title: "SMS_G_USER_DCMDeploymentNonCompliantAssetDetails Class"
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
ms.assetid: 6cc27c1a-0e86-4727-8809-83c850c157cbsearchScope: - ConfigMgr SDK
caps.latest.revision: 9
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_G_USER_DCMDeploymentNonCompliantAssetDetails Server WMI Class
The `SMS_G_USER_DCMDeploymentNonCompliantAssetDetails` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents non-compliant asset details for a deployment.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_G_USER_DCMDeploymentNonCompliantAssetDetails : SMS_G_User  
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
 The `SMS_G_USER_DCMDeploymentNonCompliantAssetDetails` class does not define any methods.  

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

## See Also  
 [Application Management Server WMI Classes](../../../develop/reference/apps/application-management-server-wmi-classes.md)
