---
title: "SMS_ReportViewSchema Class"
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
ms.assetid: c5531c2d-1eb5-488f-be7f-75232e334db9searchScope: - ConfigMgr SDK
caps.latest.revision: 8
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_ReportViewSchema Server WMI Class
The `SMS_ReportViewSchema` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in System Center Configuration Manager, that represents the views and columns that are available for building a report.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_ReportViewSchema : SMS_BaseClass  
{  
      Boolean IsStringType;  
      String ViewColumnName;  
      String ViewName;  
};  
```  

## Methods  
 The following table shows the methods in `SMS_ReportViewSchema`.  

|Method|Description|  
|------------|-----------------|  
|[GetSampleValues Method in Class SMS_ReportViewSchema](../../../../../develop/reference/core/servers/reporting/getsamplevalues-method-in-class-sms_reportviewschema.md)|Gets sample values for a report view schema.|  

## Properties  
 `IsStringType`  
 Data type: `Boolean`  

 Access type: Read Only  

 Qualifiers: None  

 `true` if the values of the column are strings.  

 `ViewColumnName`  
 Data type: `String`  

 Access type: Read Only  

 Qualifiers: [key]  

 Name of a column in the view.  

 `ViewName`  
 Data type: `String`  

 Access type: Read Only  

 Qualifiers: [key]  

 Name of a view.  

## Remarks  
 There are no special class qualifiers for this class. For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Configuration Manager Reporting Server WMI Classes](../../../../../develop/reference/core/servers/reporting/configuration-manager-reporting-server-wmi-classes.md)
