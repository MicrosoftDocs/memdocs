---
title: "SMS_MeteredProductRule Class"
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
ms.assetid: ad9f4135-37ee-4677-aa12-b0c7d393cb16searchScope: - ConfigMgr SDK
caps.latest.revision: 8
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_MeteredProductRule Server WMI Class
The `SMS_MeteredProductRule` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in System Center Configuration Manager, that represents the rules that describe which files to meter.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_MeteredProductRule : SMS_BaseClass  
{  
      Boolean ApplyToChildSites;  
      String Comment;  
      Boolean Enabled;  
      String FileName;  
      String FileVersion;  
      UInt32 LanguageID;  
      DateTime LastUpdateTime;  
      String OriginalFileName;  
      String ProductName;  
      UInt32 RuleID;  
      String SecurityKey;  
      String SiteCode;  
      String SourceSite;  
};  
```  

## Methods  
 The `SMS_MeteredProductRule` class does not define any methods.  

## Properties  
 `ApplyToChildSites`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 `true` (default) if the rule is applied to child sites.  

 `Comment`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Comment describing the rule.  

 `Enabled`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 `true` if the rule is enabled. Data is only collected by the client if the rule is enabled.  

 `FileName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Name of the file to be metered. This property is used for matching.  

 `FileVersion`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Version of the file being metered. This property is used for matching and matches to the `FileVersion` property stored in the file version information. It can contain wildcards, such as * (match multiple characters) and ? (match a single character). An empty `FileVersion` property only matches to those executable files that have no version.  

 `LanguageID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [Subtype("Locale Id")]  

 Language ID of the rule being metered. This property matches the `Language` property stored in the file version information. If it is set to 65535, it matches any language.  

 `LastUpdateTime`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: None  

 Last time the rule definition was changed.  

 `OriginalFileName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Original file name. This property is used for matching and matches the `OriginalFileName` property stored in the file version information. Because `FileName` is the Resource Explorer name of the file and might be changed by users, `OriginalFileName` is used to ensure that the file is metered.  

 `ProductName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Name of the product being metered. This is the display name of the rule and is not used in matching.  

 `RuleID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 ID for the rule.  

 `SecurityKey`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Security key for the rule.  

 `SiteCode`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Site code of the site on which the rule runs. The rule applies to clients of this site and to the clients of child sites if `ApplyToChildSites` is set to `true`.  

 `SourceSite`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Site where the rule was created.  

## Remarks  
 Class qualifiers for this class include:  

-   Secured  

 For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

 Software metering rules instruct the Software Metering Agent which processes to monitor on the client. Your application creates a new rule by creating an instance of this class. The following properties of this class have to be provided:  

-   `ProductName`  

-   `FileName`  

-   `OriginalFileName`  

-   `FileVersion`  

-   `LanguageID`  

-   `SiteCode`  

-   `ApplyToChildSites`  

-   `Enabled`  

 The `Comment` property is optional. `OriginalFileName` can be used instead of `FileName`, both can be supplied, or `FileName` only can be supplied. If either the `FileName` value or the `OriginalFileName` value matches the file, the file is metered.  

 No other properties should be supplied.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Software Metering Server WMI Classes](../../../develop/reference/apps/software-metering-server-wmi-classes.md)
