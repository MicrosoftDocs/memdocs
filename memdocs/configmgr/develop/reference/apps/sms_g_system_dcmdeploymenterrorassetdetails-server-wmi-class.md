---
title: "SMS_G_SYSTEM_DCMDeploymentErrorAssetDetails Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 0d7fca8a-666e-4856-b25d-06e5bedb6d0c
author: aczechowski
ms.author: aaroncz
manager: dougeby


---
# SMS_G_SYSTEM_DCMDeploymentErrorAssetDetails Server WMI Class
The `SMS_G_SYSTEM_DCMDeploymentErrorAssetDetails` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents the asset details for a deployment error.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_G_SYSTEM_DCMDeploymentErrorAssetDetails : SMS_G_System  
{  
    UInt32 AssignmentID;  
    UInt32 BL_ID;  
    UInt32 CI_ID;  
    UInt32 ErrorCode;  
    UInt32 ErrorType;  
    UInt32 ObjectID;  
    UInt32 ObjectType;  
    UInt32 ResourceID;  
};  
```  

## Methods  
 The `SMS_G_SYSTEM_DCMDeploymentErrorAssetDetails` class does not define any methods.  

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

 `ErrorCode`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, not_null, read]  

 See [SMS_DCMDeploymentErrorAssetDetails Server WMI Class](../../../develop/reference/compliance/sms_dcmdeploymenterrorassetdetails-server-wmi-class.md).  

 `ErrorType`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, not_null, read]  

 See [SMS_DCMDeploymentErrorAssetDetails Server WMI Class](../../../develop/reference/compliance/sms_dcmdeploymenterrorassetdetails-server-wmi-class.md).  

 `ObjectID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, not_null, read]  

 See [SMS_DCMDeploymentErrorAssetDetails Server WMI Class](../../../develop/reference/compliance/sms_dcmdeploymenterrorassetdetails-server-wmi-class.md).  

 `ObjectType`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, not_null, read]  

 See [SMS_DCMDeploymentErrorAssetDetails Server WMI Class](../../../develop/reference/compliance/sms_dcmdeploymenterrorassetdetails-server-wmi-class.md).  

 `ResourceID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Unique ID, supplied by Configuration Manager, that identifies a client resource. This ID is not unique across sites.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).
