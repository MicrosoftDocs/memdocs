---
title: "SMS_MAMStoreApplication Class"
titleSuffix: "Configuration Manager"
description: "The SMS_MAMStoreApplication WMI class is an SMS Provider server class that represents mobile application management store application lists."
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 2f1e23a4-4a19-4502-b14f-2f7ab3c78417
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_MAMStoreApplication Server WMI Class
The `SMS_MAMStoreApplication` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents mobile application management (MAM) store application lists.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_MAMStoreApplication : SMS_BaseClass  
{  
     String IdentityIdentifier;  
     Boolean IsManagedBrowser;  
     String MAMSDKVersion;  
     Boolean PinToProfile;  
     UInt32 StoreIdentifier;  
     String StoreApplicationIdentifier;  
};  

```  

## Methods  
 The `SMS_MAMStoreApplication` class does not define any methods.  

## Properties  
 `IdentityIdentifier`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Identity identifier.  

 `IsManagedBrowser`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read]  

 True if managed browser MAM application.  

 `MAMSDKVersion`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Version of the MAM SDK.  

 `PinToProfile`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read]  

 True if this application pin to profile.  

 `StoreIdentifier`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Store identifier.  

 `StoreApplicationIdentifier`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Store application identifier.  

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
