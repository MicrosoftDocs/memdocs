---
description: Learn how to use Configuration Manager SMS_AutoDeployment Windows Management Instrumentation (WMI) class to represent an automatic deployment.
title: SMS_AutoDeployment Class
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: fd4929f6-441f-4589-8325-3c0aff129fb1
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_AutoDeployment Server WMI Class
The  `SMS_AutoDeployment` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents an automatic deployment.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_AutoDeployment :  SMS_BaseClass  
{  
    Boolean AutoDeploymentEnabled;  
    SInt32 AutoDeploymentID;  
    String AutoDeploymentProperties;  
    String CollectionID;  
    String ContentTemplate;  
    String Description;  
    String DeploymentTemplate;  
    Boolean IsServicingPlan;  
    SInt32 LastErrorCode;  
    DateTime LastErrorTime;  
    DateTime LastRunTime;  
    UInt32 LocaleID;  
    String Name;  
    String Schedule;  
    String UpdateRuleXML;  
};  

```  

## Methods  
 The following table lists the methods in the `SMS_AutoDeployment` class.  

|Method|Description|  
|------------|-----------------|  
|[EvaluateAllAutoDeployment Method in Class SMS_AutoDeployment](../../../develop/reference/sum/evaluateallautodeployment-method-in-class-sms_autodeployment.md)|Evaluates all automatic deployments.|  
|[EvaluateAutoDeployment Method in Class SMS_AutoDeployment](../../../develop/reference/sum/evaluateautodeployment-method-in-class-sms_autodeployment.md)|Evaluates an automatic deployment.|  

## Properties  
 `AutoDeploymentEnabled`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 Specifies whether the automatic deployment is enabled. The default value is `true`.  

 `AutoDeploymentID`  
 Data type: `SInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 The automatic deployment ID.  

 `AutoDeploymentProperties`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [not_null, lazy]  

 Automatic deployment properties in XML format.  

 `CollectionID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 The ID of the target collection. This value is needed as a security key.  

 `ContentTemplate`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [not_null, lazy]  

 The content template XML for the automatic deployment.  

 `Description`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 A description for the automatic deployment.  

 `DeploymentTemplate`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [not_null, lazy]  

 The deployment template XML for the automatic deployment.  

 `IsServicingPlan`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 Specifies whether the automatic deployment rule  is a servicing plan. The  default value is `true`.  

 `LastErrorCode`  
 Data type: `SInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 The last error encountered when processing the automatic deployment rule failed. The default value is 0.  

 `LastErrorTime`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read]  

 The last time that an error was encountered.  

 `LastRunTime`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read]  

 The last time that  the automatic deployment was processed.  

 `LocaleID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 The locale of the automatic deployment name or description fields.  

 `Name`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 Name for the automatic deployment.  

 `Schedule`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Schedule for the automatic deployment.  

 `UpdateRuleXML`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [not_null, lazy]  

 Update rule XML for the automatic deployment.  

## Remarks  
 Class qualifiers for this class include:  

- Dynamic  

- Secured  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  
