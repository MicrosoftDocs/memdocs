---
description: Learn how to represent Automatic Deployment Rule (ADR) deployment settings in Configuration Manager.
title: SMS_ADRDeploymentSettings Class
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 9069bd1c-693c-4235-866c-b9376af2929c
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_ADRDeploymentSettings Server WMI Class
The `SMS_ADRDeploymentSettings` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents Automatic Deployment Rule (ADR) deployment settings.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_ADRDeploymentSettings : SMS_BaseClass  
{  
    UInt32 ActionID;  
    String AssociatedDeploymentID;  
    String CollectionID;  
    String CollectionName;  
    UInt32 DeploymentNumber;  
    String DeploymentTemplate;  
    Boolean Enabled;  
    UInt32 LocaleID;  
    String Name;  
    Sint32 RuleID;  
};  

```  

## Methods  
 The `SMS_ADRDeploymentSettings` class does not define any methods.  

## Properties  
 `ActionID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 The action ID.  

 `AssociatedDeploymentID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Deployment ID for the associated deployment.  

 `CollectionID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 The collection ID.  

 `CollectionName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 Name of collection.  

 `DeploymentNumber`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 The deployment number.  

 `DeploymentTemplate`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [not_null, lazy]  

 Deployment template XML for the auto deployment.  

 `Enabled`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 Specifies whether the deployment is enabled.  

 `LocaleID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 Locale of the auto deployment name and description fields.  

 `Name`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Name of the deployment setting.  

 `RuleID`  
 Data type: `SInt32`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 ID for the associated automatic deployment rule.  

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
