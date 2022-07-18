---
title: "SMS_CategoryInstance Class"
titleSuffix: "Configuration Manager"
description: "An SMS Provider server class that represents a category instance for replicating information about a category, for example, a product or a classification, to all child sites."
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 1564111c-d22b-407f-8299-e42f13179d50
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_CategoryInstance Server WMI Class
The `SMS_CategoryInstance` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a category instance used to replicate information about a category, for example, a product or a classification, to all child sites. This class is used in settings management monitoring.  

## Syntax  

```  
Class SMS_CategoryInstance : SMS_CategoryInstanceBase  
{  
      String CategoryInstance_UniqueID;  
      UInt32 CategoryInstanceID;  
      String CategoryTypeName;  
      String LocalizedCategoryInstanceName;  
      SMS_Category_LocalizedProperties LocalizedInformation[];  
      UInt32 LocalizedPropertyLocaleID;  
      UInt32 ParentCategoryInstanceID;  
      String SourceSite;  
};  
```  

## Methods  
 The `SMS_CategoryInstance` class does not define any methods.  

## Properties  
 `CategoryInstance_UniqueID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [unique, SizeLimit("512")  

 See [SMS_CategoryInstanceBase Server WMI Class](../../../develop/reference/compliance/sms_categoryinstancebase-server-wmi-class.md).  

 `CategoryInstanceID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 See [SMS_CategoryInstanceBase Server WMI Class](../../../develop/reference/compliance/sms_categoryinstancebase-server-wmi-class.md).  

 `CategoryTypeName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_CategoryInstanceBase Server WMI Class](../../../develop/reference/compliance/sms_categoryinstancebase-server-wmi-class.md).  

 `LocalizedCategoryInstanceName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_CategoryInstanceBase Server WMI Class](../../../develop/reference/compliance/sms_categoryinstancebase-server-wmi-class.md).  

 `LocalizedInformation`  
 Data type: `SMS_Category_LocalizedProperties` Array  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 See [SMS_CategoryInstanceBase Server WMI Class](../../../develop/reference/compliance/sms_categoryinstancebase-server-wmi-class.md).  

 `LocalizedPropertyLocaleID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_CategoryInstanceBase Server WMI Class](../../../develop/reference/compliance/sms_categoryinstancebase-server-wmi-class.md).  

 `ParentCategoryInstanceID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_CategoryInstanceBase Server WMI Class](../../../develop/reference/compliance/sms_categoryinstancebase-server-wmi-class.md).  

 `SourceSite`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_CategoryInstanceBase Server WMI Class](../../../develop/reference/compliance/sms_categoryinstancebase-server-wmi-class.md).  

## Remarks  
 Class qualifiers for this class include:  

- Secured  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

  To use this class, the application creates an `SMS_CategoryInstance` object and sets the properties, as required, for the particular baseline configuration item.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Configuration Manager Compliance Settings (DCM) Server WMI Classes](../../../develop/reference/compliance/compliance-settings-dcm-server-wmi-classes.md)   
 [SMS_CategoryInstanceBase Server WMI Class](../../../develop/reference/compliance/sms_categoryinstancebase-server-wmi-class.md)   
 [SMS_BaselineAssignment Server WMI Class](../../../develop/reference/compliance/sms_baselineassignment-server-wmi-class.md)   
 [SMS_ConfigurationBaselineInfo Server WMI Class](../../../develop/reference/compliance/sms_configurationbaselineinfo-server-wmi-class.md)
