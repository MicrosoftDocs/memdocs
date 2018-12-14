---
title: "SMS_AISoftwareList Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: d00d2f8e-5c03-4f71-8c0f-79445be73374
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_AISoftwareList Server WMI Class
The `SMS_AISoftwareList` Windows Management Instrumentation (WMI) class, in System Center Configuration Manager, contains all the known software titles in the Asset Intelligence catalog.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_AISoftwareList : SMS_BaseClass   
{   
      uint32 CategoryID;   
      string CategoryName;   
      string CommonName;   
      string CommonPublisher;   
      string CommonVersion;   
      uint32 Count; (obsolete in SP1)   
      uint32 FamilyID;   
      string FamilyName;   
      string OfficialCategoryName;   
      string OfficialFamilyName;   
      string SoftwareCode; (obsolete in SP1)  
      uint32 SoftwareCount;   
      string SoftwareID; (obsolete in SP1)  
      string SoftwareKey;   
      string SoftwarePropertiesHash; (obsolete in SP1)  
      uint32 State;   
      uint32 Tag1ID;   
      string Tag1Name;   
      uint32 Tag2ID;   
      string Tag2Name;   
      uint32 Tag3ID;   
      string Tag3Name;   
};  
```  

## Methods  
 The following table lists the methods in the `SMS_AISoftwareList` class.  

|Method|Description|  
|------------|-----------------|  
|[AddSoftwareHashData Method in Class SMS_AISoftwareList](../../../../../develop/reference/core/clients/asset-intelligence/addsoftwarehashdata-method-in-class-sms_aisoftwarelist.md)|Adds the `SoftwarePropertiesHash` from `SoftwareCode` and `Title`.|  
|[GetCategorizationRequestText Method in Class SMS_AISoftwareList](../../../../../develop/reference/core/clients/asset-intelligence/getcategorizationrequesttext-method-in-class-sms_aisoftwarelist.md)|Retrieves the categorization XML that is used in requesting categorization from System Center Online.|  
|[GetSummary Method in Class SMS_AISoftwareList](../../../../../develop/reference/core/clients/asset-intelligence/getsummary-method-in-class-sms_aisoftwarelist.md)|Retrieves a summary of all class instances based on the `State` property of the class.|  
|[ResolveConflict Method in Class SMS_AISoftwareList](../../../../../develop/reference/core/clients/asset-intelligence/resolveconflict-method-in-class-sms_aisoftwarelist.md)|Resolves the conflict through the Resolution parameter whose values are:<br />1 - Keep local edit and discard latest update from Microsoft.<br />2 - Revert local edit and replace it with latest update from Microsoft.<br />All other values are ignored.|  
|[SetCategorizationRequest Method in Class SMS_AISoftwareList](../../../../../develop/reference/core/clients/asset-intelligence/setcategorizationrequest-method-in-class-sms_aisoftwarelist.md)|Submits a request to System Center Online for software categorization.|  

## Properties  
 `CategoryID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Refers to a [SMS_AICategory Server WMI Class](../../../../../develop/reference/core/clients/asset-intelligence/sms_aicategory-server-wmi-class.md) instance.  

 `CategoryName`  
 Data type: `String`  

 Access type: Read Only  

 Qualifiers: None  

 Category name identified by the `CategoryID` property.  

 `CommonName`  
 Data type: `String`  

 Access type: Read Only  

 Qualifiers: None  

 Software title, as it is commonly known.  

 `CommonPublisher`  
 Data type: `String`  

 Access type: Read Only  

 Qualifiers: None  

 Publisher of the software title, as it is commonly known.  

 `CommonVersion`  
 Data type: `String`  

 Access type: Read Only  

 Qualifiers: None  

 Version of the software title, as it is commonly known.  

 `Count`  
 Data type: `UInt32`  

 Access type: Read Only  

 Qualifiers: None  

 This method/property has been removed or deprecated in System Center Configuration Manager SP1. Use `SoftwareCount` instead.  

 This information applies to System Center 2012 Configuration Manager SP1 or later, and System Center 2012 R2 Configuration Manager or later.  

 `FamilyID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Refers to a [SMS_AICategory Server WMI Class](../../../../../develop/reference/core/clients/asset-intelligence/sms_aicategory-server-wmi-class.md) instance.  

 `FamilyName`  
 Data type: `String`  

 Access type: Read Only  

 Qualifiers: None  

 Family name identified by the `FamilyID` property.  

 `OfficialCategoryName`  
 Data type: `String`  

 Access type: Read Only  

 Qualifiers: None  

 The `CategoryID` property can be changed, which alters what the `CategoryName` property contains. This is the original name of the category before any changes have occurred.  

 `OfficialFamilyName`  
 Data type: `String`  

 Access type: Read Only  

 Qualifiers: None  

 The `FamilyID` property can be changed, which alters what the `FamilyName` property contains. This is the original name of the family before any changes have occurred.  

 `SoftwareCode`  
 Data type: `String`  

 Access type: Read Only  

 Qualifiers: None  

 Identifier of the software title, defined by the publisher of the software title.  

 `SoftwareCount`  
 Data type: `UInt32`  

 Access type: Read Only  

 Qualifiers: [read]  

 Count of the software title.  

 This information applies to System Center 2012 Configuration Manager SP1 or later, and System Center 2012 R2 Configuration Manager or later.  

 `SoftwareID`  
 Data type: `String`  

 Access type: Read Only  

 Qualifiers: None  

 A Microsoft generated GUID identifying this software title.  

 This method/property has been removed or deprecated in System Center Configuration Manager SP1.  

 `SoftwareKey`  
 Data type: `String`  

 Access type: Read Only  

 Qualifiers: [key, read]  

 A Microsoft generated key identifying this software title.  

 This information applies to System Center 2012 Configuration Manager SP1 or later, and System Center 2012 R2 Configuration Manager or later.  

 `SoftwarePropertiesHash`  
 Data type: `String`  

 Access type: Read Only  

 Qualifiers: key  

 An automatically generated hash composed of the Name, Publisher, and Version of the software title.  

 This method/property has been removed or deprecated in System Center Configuration Manager SP1.  

 `State`  
 Data type: `UInt32`  

 Access type: Read Only  

 Qualifiers: None  

 Status of this software record.  

|Value|Description|  
|-----------|-----------------|  
|0|Validated, category is defined by Microsoft through System Center Online.|  
|1|User-defined, category was defined or has been changed by a user.|  
|2|Pending, the software is pending categorization by Microsoft through System Center Online.|  
|3|Updatable, the software category can be updated by the user.|  
|4|Uncategorized, the software has not been categorized by Microsoft or the user.|  

 `Tag1ID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Refers to a [SMS_AICategory Server WMI Class](../../../../../develop/reference/core/clients/asset-intelligence/sms_aicategory-server-wmi-class.md) instance.  

 `Tag1Name`  
 Data type: `String`  

 Access type: Read Only  

 Qualifiers: None  

 Tag name identified by the `CategoryID` property.  

 `Tag2ID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Refers to a [SMS_AICategory Server WMI Class](../../../../../develop/reference/core/clients/asset-intelligence/sms_aicategory-server-wmi-class.md) instance.  

 `Tag2Name`  
 Data type: `String`  

 Access type: Read Only  

 Qualifiers: None  

 Tag name identified by the `CategoryID` property.  

 `Tag3ID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Refers to a [SMS_AICategory Server WMI Class](../../../../../develop/reference/core/clients/asset-intelligence/sms_aicategory-server-wmi-class.md) instance.  

 `Tag3Name`  
 Data type: `String`  

 Access type: Read Only  

 Qualifiers: None  

 Tag name identified by the `CategoryID` property.  

## Remarks  
 Class qualifiers for this class include:  

- DisplayName("AI Software List Table")  

- Dynamic  

- Provider("ExtnProv")  

- Secured  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For information about handling returned errors, see [About Configuration Manager Errors](../../../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Configuration Manager Asset Intelligence](../../../../../develop/core/clients/asset-intelligence/asset-intelligence.md)
