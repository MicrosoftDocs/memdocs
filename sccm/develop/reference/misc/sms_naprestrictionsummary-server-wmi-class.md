---
title: "SMS_NAPRestrictionSummary Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 0fa61bee-8ef6-41d0-ac55-7397f9240f8b
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_NAPRestrictionSummary Server WMI Class
The `SMS_NAPRestrictionSummary` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a Network Access Protection (NAP) restriction summary.  

> [!NOTE]
>  This class requires a high level of permissions to enumerate.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_NAPRestrictionSummary : SMS_BaseClass  
{  
      String ArticleID;  
      String BulletinID;  
      UInt32 CI_ID;  
      String CI_UniqueID;  
      UInt32 Last30DaysCount;  
      UInt32 Last7DaysCount;  
      UInt32 LastDayCount;  
      DateTime LastSummaryTime;  
      String LocalizedDisplayName;  
      String LocalizedInformativeURL;  
      UInt32 LocalizedPropertyLocaleID;  
};  
```  

## Methods  
 The `SMS_NAPRestrictionSummary` class does not define any methods.  

## Properties  
 `ArticleID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Knowledge base article ID for the configuration item associated with the NAP restriction.  

 `BulletinID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Bulletin ID for security updates released by Microsoft for the configuration item associated with the NAP restriction.  

 `CI_ID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 The unique ID of the configuration item associated with the NAP restriction. This ID is unique for the site.  

 `CI_UniqueID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [unique]  

 The unique ID of the configuration item associated with the NAP restriction. This ID is unique across sites.  

 `Last30DaysCount`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 The number of computers restricted in the last 30 days.  

 `Last7DaysCount`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 The number of computers restricted in the last 7 days.  

 `LastDayCount`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 The number of computers restricted in the last 24 hours.  

 `LastSummaryTime`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read]  

 The last time the summary task was run to get the cumulative counts.  

 `LocalizedDisplayName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Localized title of the NAP update.  

 `LocalizedInformativeURL`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Localized URL of information about the NAP update.  

 `LocalizedPropertyLocaleID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 ID of the locale for retrieved localized properties.  

## Remarks  
 Class qualifiers for this class include:  

- Read (read-only)  

- Secured  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [NAP Server WMI Classes](../../../develop/reference/misc/nap-server-wmi-classes.md)
