---
title: SMS_SiteAndSubsites Class
titleSuffix: Configuration Manager
description: The SMS_SiteAndSubsites WMI class reads the current site and child site information.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: a0d97ac9-83c1-42cd-a385-903efab4c0e9
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_SiteAndSubsites Server WMI Class
The `SMS_SiteAndSubsites` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that reads the current site and child site information.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_SiteAndSubsites : SMS_BaseClass  
{  
    String ServerName;  
    String SiteCode;  
    String SiteName;  
    String Version;  
};  
```  

## Methods  
 The `SMS_SiteAndSubsites` class does not define any methods.  

## Properties  
 `ServerName`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: [none]  

 The server name of the site Configuration Manager is installed on.  

 `SiteCode`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: [key, sizelimit("3")]  

 The three letter site code for the site.  

 `SiteName`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: [none]  

 The name of the site.  

 `Version`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: [none]  

 The Configuration Manager version of the current site.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
