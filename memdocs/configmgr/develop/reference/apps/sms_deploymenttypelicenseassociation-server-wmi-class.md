---
title: "SMS_DeploymentTypeLicenseAssociation Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: f401795b-30b7-43f9-be66-0d3658c2e316
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth
description: Learn about the simplified syntax, methods, properties, and requirements of the SMS_DeploymentTypeLicenseAssociation server class.

---
# SMS_DeploymentTypeLicenseAssociation Server WMI Class
The `SMS_DeploymentTypeLicenseAssociation` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a license association for a deployment type.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_DeploymentTypeLicenseAssociation : SMS_BaseClass  
{  
    UInt32 ID;  
    String LicenseID;  
    String DTModelName;  
    Boolean IsEnabled;  
};  

```  

## Methods  
 The following table lists the methods in the `SMS_DeploymentTypeLicenseAssociation` class.  

|Method|Description|  
|------------|-----------------|  
|[AddLicense Method in Class SMS_DeploymentTypeLicenseAssociation](../../../develop/reference/apps/addlicense-method-in-class-sms_deploymenttypelicenseassociation.md)|Adds license information to an application deployment type.|  

## Properties  
 `ID`  
 Data type: `UInt32`  

 Access type: Read  

 Qualifiers: [key]  

 The ID of the deployment type.  

 `LicenseID`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: none  

 The ID of the license.  

 `DTModelName`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: none  

 The deployment type model name.  

 `IsEnabled`  
 Data type: `Boolean`  

 Access type: Read  

 Qualifiers: none  

 Indicates whether the association is enabled.  

## Remarks  
 Class qualifiers for this class include:  

- Dynamic  

- Read (read-only)  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  
