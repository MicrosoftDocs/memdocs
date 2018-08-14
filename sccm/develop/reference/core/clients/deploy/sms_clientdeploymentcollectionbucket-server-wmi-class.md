---
title: "SMS_ClientDeploymentCollectionBucket Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: bf1d205a-d474-457b-b451-9c8f5afb7c23
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_ClientDeploymentCollectionBucket Server WMI Class
The  `SMS_ClientDeploymentCollectionBucket` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a client deployment collection bucket that is used to display the localized name in the client deployment detail view.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_ClientDeploymentCollectionBucket: SMS_BaseClass  
{  
    UInt32 BaselineType;      
    String Bucket;  
    String CollectionID;  
    String CollectionName;  
    UInt32 FeatureType;  
};  

```  

## Methods  
 The  `SMS_ClientDeploymentCollectionBucket`  class does not define any methods.  

## Properties  
 `BaselineType`  
 Data type: `UInt32`  

 Access type: Read  

 Qualifiers: [key]  

 The baseline type. Possible values are:  

|||  
|-|-|  
|1|Product Baseline|  
|2|Staging Baseline|  

 `Bucket`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: [key]  

 The client deployment status bucket. Possible values are:  

|Value|
|-|  
|CDUnknown|  
|CDFullCompliant|  
|CDInProgress|  
|CDNotCompliant|  
|CDCriticalError|  

 `CollectionID`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: [key]  

 The ID of the collection.  

 `CollectionName`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: none  

 The name of the collection.  

 `FeatureType`  
 Data type: `UInt32`  

 Access type: Read  

 Qualifiers: [key]  

 The feature type. Possible values are:  

|||  
|-|-|  
|3|Client Deployment|  

## Remarks  
 Class qualifiers for this class include:  

-   Dynamic  

-   Read (read-only)  

 For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Configuration Manager Client Deployment Server WMI Classes](../../../../../develop/reference/core/clients/deploy/client-deployment-server-wmi-classes.md)
