---
title: "SMS_ReportDashboard Class"
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
ms.assetid: 4ce1e635-f5ee-4bca-9932-eb97b7c84341searchScope: - ConfigMgr SDK
caps.latest.revision: 6
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_ReportDashboard Server WMI Class
The `SMS_ReportDashboard` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a collection of reports tiled across and displayed as a single page in Web reports.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_ReportDashboard : SMS_BaseClass  
{  
      UInt32 ColumnCount;  
      String Comment;  
      UInt32 DashboardID;  
      String Name;  
      UInt32 ReportIDs[];  
      UInt32 RowVerticalLimit;  
};  
```  

## Methods  
 The `SMS_ReportDashboard` class does not define any methods.  

## Properties  
 `ColumnCount`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Number of reports tiled horizontally across the dashboard.  

 `Comment`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 User-assigned additional information to display on the property page for the dashboard.  

 `DashboardID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Unique automatically generated ID for the dashboard.  

 `Name`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 User-assigned display name. This property is unique for the site.  

 `ReportIDs`  
 Data type: `UInt32` Array  

 Access type: Read/Write  

 Qualifiers: None  

 Report IDs specifying the reports that comprise the dashboard. Reports are listed in row-major order, from left to right and top to bottom. Missing reports should be included with NULL or blank IDs.  

 This property also accepts the object paths of report objects to support aliased references to reports defined in the same MOF file as the dashboard.  

 `RowVerticalLimit`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Vertical height, in pixels, of a tiled dashboard row. Set this property to NULL if there is no limit.  

## Remarks  
 There are no special class qualifiers for this class. For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Reporting Server WMI Classes](../../../develop/reference/core/servers/reporting/configuration-manager-reporting-server-wmi-classes.md)
