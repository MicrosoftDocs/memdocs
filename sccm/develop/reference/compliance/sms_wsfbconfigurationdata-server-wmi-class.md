---
title: "SMS_WSfBConfigurationData Class"
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
ms.assetid: 51870eea-f043-4bd3-a3cd-a68b7471681dsearchScope: - ConfigMgr SDK
caps.latest.revision: 5
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_WSfBConfigurationData Server WMI Class
The `SMS_WSfBConfigurationData` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents Windows Store For Business configuration data.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_WSfBConfigurationData : SMS_BaseClass  
{  
    String ClientId;  
    String ContentLocation;  
    String DefaultLocale;  
    DateTime LastSuccessfulSyncTime;  
    SInt32 LastSyncStatus;  
    DateTime LastSyncTime;  
    String SelectedLocales;  
    String TenantId;  
};  

```  

## Methods  
 The `SMS_WSfBConfigurationData` class does not define any methods.  

## Properties  
 `ClientId`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: none  

 Windows Store For Business client ID.  

 `ContentLocation`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: none  

 Location of the content downloaded from the Windows Store For Business.  

 `DefaultLocale`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: none  

 The default language for the Windows Store For Business.  

 `LastSuccessfulSyncTime`  
 Data type: `DateTime`  

 Access type: Read  

 Qualifiers: none  

 The time of the last successful synchronization with Windows Store For Business.  

 `LastSyncStatus`  
 Data type: `SInt32`  

 Access type: Read  

 Qualifiers: none  

 The status of the last synchronization with Windows Store For Business.  

 `LastSyncTime`  
 Data type: `DateTime`  

 Access type: Read  

 Qualifiers: none  

 The time of the last synchronization with Windows Store For Business.  

 `SelectedLocales`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: none  

 The selected languages for Windows Store For Business.  

 `TenantId`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: [key]  

 Windows Store For Business tenant ID.  

## Remarks  
 Class qualifiers for this class include:  

-   Dynamic  

-   Read (read-only)  

-   Secured  

 For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Configuration Manager Compliance Settings (DCM) Server WMI Classes](../../../develop/reference/compliance/compliance-settings-dcm-server-wmi-classes.md)
