---
title: "SMS_MonthlyUsageSummary Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 8e439e9d-7a96-4cb0-b0ff-18efd7a1f43f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_MonthlyUsageSummary Server WMI Class
The `SMS_MonthlyUsageSummary` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a monthly usage summary for a particular file.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_MonthlyUsageSummary : SMS_BaseClass  
{  
      SInt64 FileID;  
      DateTime LastUsage;  
      UInt32 MeteredUserID;  
      UInt32 ResourceID;  
      UInt32 TimeKey;  
      UInt32 TSUsageCount;  
      UInt32 UsageCount;  
      UInt32 UsageTime;  
};  
```  

## Methods  
 The `SMS_MonthlyUsageSummary` class does not define any methods.  

## Properties  
 `FileID`  
 Data type: `SInt64`  

 Access type: Read/Write  

 Qualifiers: [key]  

 File ID for the summarized file.  

 `LastUsage`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: None  

 Date and time when the metered file was last used during the month.  

 `MeteredUserID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 ID of the user of the metered file. This matches the `MeteredUserID` property in [SMS_MeteredUser Server WMI Class](../../../develop/reference/apps/sms_metereduser-server-wmi-class.md).  

 `ResourceID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 ID of the computer using the metered file. This ID matches the `ResourceId` property in [SMS_R_System Server WMI Class](../../../develop/reference/core/clients/manage/sms_r_system-server-wmi-class.md).  

 `TimeKey`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Month that the summary data represents, encoded as an integer Year*100+Month. This property also matches the time key in the [SMS_SummarizationInterval Server WMI Class](../../../develop/reference/apps/sms_summarizationinterval-server-wmi-class.md) class.  

 `TSUsageCount`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Number of times that the summarized file was used under a Terminal Services session during the month.  

 `UsageCount`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Number of times that the summarized file was used in a console session during the month.  

 `UsageTime`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Total amount of time, in seconds, that the summarized file was used during the month.  

## Remarks  
 There are no special class qualifiers for this class. For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

 This class compiles data about a file running on a particular computer by a particular user during a calendar month. `TSUsageCount` and `UsageCount` represent the number of times the summarized file was used during a month. For example, a file could have been opened in the month of May and terminated in June. In this case, both May and June have a usage count of 1 for this file although it was only started in May.  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_MeteredUser Server WMI Class](../../../develop/reference/apps/sms_metereduser-server-wmi-class.md)   
 [SMS_R_System Server WMI Class](../../../develop/reference/core/clients/manage/sms_r_system-server-wmi-class.md)   
 [SMS_SummarizationInterval Server WMI Class](../../../develop/reference/apps/sms_summarizationinterval-server-wmi-class.md)
