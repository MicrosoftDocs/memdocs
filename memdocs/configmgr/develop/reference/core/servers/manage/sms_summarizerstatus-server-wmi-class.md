---
title: "SMS_SummarizerStatus Class"
description: "Learn how the SMS_SummarizerStatus class is an SMS Provider server class that identifies registered summarizers, without defining any specific status information."
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: eb7a44f9-409d-4c6b-9902-ef94de634fd8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_SummarizerStatus Server WMI Class
The `SMS_SummarizerStatus` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that identifies registered summarizers, without defining any specific status information.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_SummarizerStatus : SMS_BaseClass  
{  
      String GUID_ID;  
      String MessageDLL;  
      UInt32 MessageID;  
      String SiteCode;  
      UInt32 Status;  
      DateTime Updated;  
};  
```  

## Methods  
 The `SMS_SummarizerStatus` class does not define any methods.  

## Properties  
 `GUID_ID`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: [key]  

 GUID under which the summarizer is registered in the registry.  

 `MessageDLL`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: None  

 Resource DLL containing the localized name of the summarizer.  

 `MessageID`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: None  

 ID the string resource in the `MessageDLL` property that contains the localized name of the summarizer.  

 `SiteCode`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: [key]  

 Site code of the Configuration Manager site.  

 `Status`  
 Data type: `UInt32`  

 Access type: Read  

 Qualifiers: None  

 Value indicating the health of the data associated with the registered summarizer. Possible values are:  

| Value | Status |
| ----- | ------ |
|GREEN(0)|OK. There are no warning or error messages.|  
|YELLOW(1)|Warning. Warning messages were generated, but error messages were not generated. This status also indicates that the storage objects are approaching their threshold.|  
|RED(2)|Critical. There are error messages, or the storage objects have exceeded their thresholds.|  

 `Updated`  
 Data type: `DateTime`  

 Access type: Read  

 Qualifiers: None  

 Date and time when the registration was last updated.  

## Remarks  
 Class qualifiers for this class include:  

- Read (read-only)  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  
