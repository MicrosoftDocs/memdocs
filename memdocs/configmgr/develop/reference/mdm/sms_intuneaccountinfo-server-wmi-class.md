---
title: SMS_IntuneAccountInfo Class
titleSuffix: Configuration Manager
description: In Configuration Manager, the SMS_IntuneAccountInfo WMI class is an SMS Provider server class that represents Microsoft Intune account information.
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: e9582b73-ef71-4cf6-963b-31ecf8dced26
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_IntuneAccountInfo Server WMI Class
The `SMS_IntuneAccountInfo` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents Microsoft Intune account information.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_IntuneAccountInfo : SMS_BaseClass  
{  
    String AADTenantID;  
    String IntuneAccountID;  
    Datetime LastUpdateTime;  
};  

```  

## Methods  
 The `SMS_IntuneAccountInfo` class does not define any methods.  

## Properties  
 `AADTenantID`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: none  

 The GUID of the Azure Active Directory account.  

 `IntuneAccountID`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: [key]  

 The GUID of the Microsoft Intune account.  

 `LastUpdateTime`  
 Data type: `DateTime`  

 Access type: Read  

 Qualifiers: none  

 The last date and time that the account was updated.  

## Remarks  
 Class qualifiers for this class include:  

- Dynamic  

- Read (read-only)  

- Secured  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  
