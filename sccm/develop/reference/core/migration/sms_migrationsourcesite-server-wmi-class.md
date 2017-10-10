---
title: "SMS_MigrationSourceSite Class"
ms.custom: ""
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.reviewer: ""
ms.suite: ""
ms.technology:
  - "configmgr-other"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to:
  - "System Center Configuration Manager (current branch)"
ms.assetid: ff844187-e53f-4325-a3ed-7e906baa32cfsearchScope: - ConfigMgr SDK
caps.latest.revision: 15
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_MigrationSourceSite Server WMI Class
The `SMS_MigrationSourceSite` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a site in the source hierarchy.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_MigrationSourceSite : SMS_BaseClass  
{  
    String FQDN;  
    Boolean IsCentral;  
    Boolean IsConfigured;  
    Boolean IsDecommissioned;  
    Boolean IsDeleted;  
    String ParentSiteCode;  
    String ParentSiteServer;  
    String SiteCode;  
    UInt32 SiteID;  
    UInt32 SiteType;  
    String SourceSiteFQDN;  
    String Version;  
};  
```  

## Methods  
 The `SMS_MigrationSourceSite` class does not define any methods.  

## Properties  
 `FQDN`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: none  

 FQDN of the source Site Server (deprecated).  

 `IsCentral`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: none  

 `true` if the source site is a central site.  

 `IsConfigured`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: none  

 `true` if the source site is configured.  

 `IsDecommissioned`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: none  

 `true` if the site has stopped gathering data.  

 `IsDeleted`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: none  

 `true` if the source site is deleted.  

 `ParentSiteCode`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: none  

 The site code of the parent site of the source site.  

 `ParentSiteServer`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: none  

 The site server name of the parent site of the source site.  

 `SiteCode`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: none  

 The source site code.  

 `SiteID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key]  

 The source site ID.  

 `SiteType`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [enumeration]  

 See [SMS_SCI_SiteDefinition Server WMI Class](../../../../develop/reference/core/servers/configure/sms_sci_sitedefinition-server-wmi-class.md).  

 `SourceSiteFQDN`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: none  

 The FQDN of the source site server.  

 `Version`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: none  

 The version of the source site.  

 This information applies to System Center 2012 Configuration Manager SP1 or later, and System Center 2012 R2 Configuration Manager or later.  

## Remarks  
 All of the instances are gathered from the Configuration Manager database, except for the first one which is created when you specify the source hierarchy.Each instance carries basic information for the source site, such as the parent site code, the site type and the FQDN of the site.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../develop/core/reqs/server-development-requirements.md).
