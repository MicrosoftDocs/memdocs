---
title: "SMS_AppDTDeploymentSummary Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: e577ce4f-2653-41a3-b405-606d059c00f1
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_AppDTDeploymentSummary Server WMI Class
The `SMS_AppDTDeploymentSummary` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents the deployment type-level summary of application deployment.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_AppDTDeploymentSummary : SMS_BaseClass  
{  
    UInt32 AppCI;  
    String AppModelName;  
    UInt32 AssignmentID;  
    String AssignmentUniqueID;  
    String CollectionID;  
    String CollectionName;  
    UInt32 DeploymentIntent;  
    DateTime DeploymentTime;  
    String Description;  
    UInt32 DTCI;  
    String DTModelName;  
    DateTime ModificationTime;  
    SInt32 NumberAlreadyPresent;  
    SInt32 NumberErrors;  
    SInt32 NumberInProgress;  
    SInt32 NumberInstalled;  
    SInt32 NumberReqsNotMet;  
    DateTime SummarizationTime;  
    String Technology;  
};  
```  

## Methods  
 The `SMS_AppDTDeploymentSummary` class does not define any methods.  

## Properties  
 `AppCI`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 See [SMS_AppDeploymentAssetDetails Server WMI Class](../../../develop/reference/apps/sms_appdeploymentassetdetails-server-wmi-class.md).  

 `AppModelName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Model Name of the application.  

 `AssignmentID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 See [SMS_AppDeploymentAssetDetails Server WMI Class](../../../develop/reference/apps/sms_appdeploymentassetdetails-server-wmi-class.md).  

 `AssignmentUniqueID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 See [SMS_AppDeploymentAssetDetails Server WMI Class](../../../develop/reference/apps/sms_appdeploymentassetdetails-server-wmi-class.md).  

 `CollectionID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 See [SMS_AppDeploymentAssetDetails Server WMI Class](../../../develop/reference/apps/sms_appdeploymentassetdetails-server-wmi-class.md).The ID of the collection to which the deployment was deployed.  

 `CollectionName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 See [SMS_AppDeploymentAssetDetails Server WMI Class](../../../develop/reference/apps/sms_appdeploymentassetdetails-server-wmi-class.md).  

 `DeploymentIntent`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 See [SMS_AppDeploymentAssetDetails Server WMI Class](../../../develop/reference/apps/sms_appdeploymentassetdetails-server-wmi-class.md).  

 `DeploymentTime`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: none  

 Time the deployment was created.  

 `Description`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Description of the deployment type.  

 `DTCI`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 See [SMS_AppDeploymentAssetDetails Server WMI Class](../../../develop/reference/apps/sms_appdeploymentassetdetails-server-wmi-class.md).  

 `DTModelName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Model name of the deployment type.  

 `ModificationTime`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: none  

 Time that the deployment type was last modified.  

 `NumberAlreadyPresent`  
 Data type: `SInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Number of clients that have this deployment type installed.  

 `NumberErrors`  
 Data type: `SInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Number of clients that return an error during an installation.  

 `NumberInProgress`  
 Data type: `SInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Number of clients that have this deployment type installation in progress.  

 `NumberInstalled`  
 Data type: `SInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Number of clients that have this deployment type installed.  

 `NumberReqsNotMet`  
 Data type: `SInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Number of clients that do not meet the requirements of this deployment type.  

 `SummarizationTime`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: none  

 Time when summarization occurs.  

 `Technology`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 See [SMS_AppDeploymentAssetDetails Server WMI Class](../../../develop/reference/apps/sms_appdeploymentassetdetails-server-wmi-class.md).  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Application Management Server WMI Classes](../../../develop/reference/apps/application-management-server-wmi-classes.md)
