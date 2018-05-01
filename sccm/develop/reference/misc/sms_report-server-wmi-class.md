---
title: "SMS_Report Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: cec44169-1614-4518-8bfd-2db83f0526fa
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_Report Server WMI Class
The `SMS_Report` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a fully defined report that can be run by Configuration Manager Reports.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_Report : SMS_BaseClass  
{  
      String Category;  
      String Comment;  
      UInt32 DrillThroughColumns[];  
      UInt32 DrillThroughReportID;  
      ref:SMS_Report DrillThroughReportPath;  
      String DrillThroughURL;  
      String GraphCaption;  
      UInt32 GraphType;  
      UInt32 GraphXCol;  
      UInt32 GraphYCol;  
      Boolean MachineDetail;  
      Boolean MachineSource;  
      String Name;  
      UInt32 NumPrompts;  
      UInt32 RefreshInterval;  
      String ReportGUID;  
      UInt32 ReportID;  
      SMS_ReportParameter ReportParams[];  
      String SecurityKey;  
      String SQLQuery;  
      Boolean StatusMessageDetailSource;  
      Boolean UnicodeData;  
      String XColLabel;  
      String YColLabel;  
};  
```  

## Methods  
 The following table shows the methods in `SMS_Report`.  

|Method|Description|  
|------------|-----------------|  
|[GetReportPointInfo Method in Class SMS_Report](../../../develop/reference/misc/getreportpointinfo-method-in-class-sms_report.md)|Gets report point information.|  
|[ValidateQuery Method in Class SMS_Report](../../../develop/reference/misc/validatequery-method-in-class-sms_report.md)|Verifies that a report query is a valid SQL statement and performs the same level of validation that occurs when the report is saved.|  

## Properties  
 `Category`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Category to be used in the Configuration Manager console to filter the list of reports and to provide a report hierarchy. The default value is "".  

 `Comment`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Further description of the report to be displayed on the property page for the report in the Configuration Manager console.  

 `DrillThroughColumns`  
 Data type: `UInt32` Array  

 Access type: Read/Write  

 Qualifiers: None  

 Integers indicating the columns to use as the parameters of the destination report when drilling through on a particular row. If this property is not applicable, set it to `null` or an empty array.  

 `DrillThroughReportID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Report ID to link to each row of the report. Selected columns from the originating report are used as parameters to the destination report. Set this property to `null` if there is no drill-through destination for the report.  

 This property can be set to a report object path to support references to other reports in the same MOF file as the originating report.  

 `DrillThroughReportPath`  
 Data type: `SMS_Report REF`  

 Access type: Read Only  

 Qualifiers: [lazy]  

 Relative path of the WMI object representing the destination report to which the originating report will drill through. When defining multiple reports in a MOF file that link together, set this property to the path alias from the previously defined drill-through report.  

 `DrillThroughURL`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 The URL of the drill-through report.  

 `GraphCaption`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Caption for the report graph. If there is no graph, set this property to `null`.  

 `GraphType`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Type of report graph. Set this property to `null` if no graph is available.  

 `GraphXCol`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Column number to use for the X axis of the graph. Set this property to `null` if it is not applicable.  

 `GraphYCol`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Column number to use for the Y axis of the graph. Set this property to `null` if it is not applicable.  

 `MachineDetail`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 `true` if the report is a computer detail report, having one parameter that represents the Name0 column of the report. The default value is `false`.  

 `MachineSource`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 `true` if this report drills through to the computer details page. The `DrillThroughColumns` property should contain a single index representing the Name0 column of the report. The default value is `false`.  

 `Name`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Report name to display in the Configuration Manager console and on the report itself.  

 `NumPrompts`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 The number of report prompts allowed in the console.  

 `RefreshInterval`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [Range("0-60")]  

 The interval, in seconds, that should elapse before the report is automatically rerun and the page is refreshed. Possible values are 0 (default) through 60. Set this property to 0 if the page should not be automatically refreshed.  

 `ReportGUID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [unique]  

 GUID for the report.  

 `ReportID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Unique automatically generated number that identifies the report.  

 `ReportParams`  
 Data type: `SMS_ReportParameter` Array  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 [SMS_ReportParameter Server WMI Class](../../../develop/reference/misc/sms_reportparameter-server-wmi-class.md) objects that define the user-supplied parameters to the report. Set this property to `null` or an empty array if there are no parameters.  

 `SecurityKey`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [unique]  

 Unique automatically generated key used as the security identifier for the [SMS_UserInstancePermissions Server WMI Class](../../../develop/reference/misc/sms_userinstancepermissions-server-wmi-class.md) class.  

 `SQLQuery`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [lazy, large]  

 Text of the SQL query that produces the result set of the report.  

 `StatusMessageDetailSource`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 `true` if the source of the status message is detailed. The default value is `false`.  

 `UnicodeData`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 `true` if the report includes Unicode data. The default value is `false`.  

 `XColLabel`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Caption for the X axis of the graph. Set this property to `null` if it is not applicable.  

 `YColLabel`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Caption for the Y axis of the graph. Set this property to `null` if it is not applicable.  

## Remarks  
 Class qualifiers for this class include:  

-   Secured  

 For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Reporting Server WMI Classes](../../../develop/reference/core/servers/reporting/configuration-manager-reporting-server-wmi-classes.md)
