---
title: "SMS_ReportParameter Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: ab6691e4-7620-43a6-949c-4dec7e8cf871
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_ReportParameter Server WMI Class
The `SMS_ReportParameter` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a user-supplied parameter that is required to run the report.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_ReportParameter  
{  
      Boolean AllowEmpty;  
      String DefaultValue;  
      String PromptText;  
      String SampleValueSQL;  
      String VariableName;  
};  
```  

## Methods  
 The `SMS_ReportParameter` class does not define any methods.  

## Properties  
 `AllowEmpty`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 `true` if the report parameter can be unspecified by the user. The value of the `DefaultValue` property is used instead.  

 `DefaultValue`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Value to use if the report parameter is unspecified by the user. Set this property to `null` to use SQL NULL as a default. This property is only applicable if `AllowEmpty` is set to `true`.  

 `PromptText`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Text displayed to the user to request the report parameter value.  

 `SampleValueSQL`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Text of the SQL query that populates a list of sample values for the parameter.  

 `VariableName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Name of the report parameter as it appears in the SQL statement.  

## Remarks  
 Class qualifiers for this class include:  

-   Embedded  

 For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

 This class is an embedded class used only as a member of [SMS_Report Server WMI Class](../../../develop/reference/misc/sms_report-server-wmi-class.md).  

 The user-supplied parameter provided to this class is substituted for a variable in an SQL query for the report. Usually this is a value in a WHERE clause.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Reporting Server WMI Classes](../../../develop/reference/core/servers/reporting/configuration-manager-reporting-server-wmi-classes.md)   
 [SMS_Report Server WMI Class](../../../develop/reference/misc/sms_report-server-wmi-class.md)
