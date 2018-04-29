---
title: "CCM_PowerManagementClientOptoutSetting Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 2341f440-5c3b-414d-9321-1e9f367758f4
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# CCM_PowerManagementClientOptoutSetting Client WMI Class
The `CCM_PowerManagementClientOptoutSetting` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents the settings that allow users to exclude their device from power management.   

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class CCM_PowerManagementClientOptoutSetting :    
{  
    Boolean AdminAllowOptout;  
    Boolean EffectiveClientOptOut;  
    Boolean IsClientOptOut;  
};  
```  

## Methods  
 The `CCM_PowerManagementClientOptoutSetting` class does not define any methods.  

## Properties  
 `AdminAllowOptOut`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` if the Admin allows users to exclude their device from power management.    

 `EffectiveClientOptOut`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` if the result of AdminAllowOptOut and IsClientOptOut is ClientOptOut.    

 `IsClientOptOut`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` if the user has excluded their device from power management.    

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
