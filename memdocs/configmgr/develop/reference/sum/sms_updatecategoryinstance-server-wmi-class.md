---
title: "SMS_UpdateCategoryInstance Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: bc441b19-52b2-4004-9af3-f37a5e0529dd
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_UpdateCategoryInstance Server WMI Class
The `SMS_UpdateCategoryInstance` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a software-update-specific `SMS_CategoryInstance Server WMI Class` object available on the site.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_UpdateCategoryInstance : SMS_CategoryInstanceBase  
{  
      Boolean AllowSubscription;  
      String CategoryInstance_UniqueID;  
      UInt32 CategoryInstanceID;  
      String CategoryTypeName;  
      Boolean IsSubscribed;  
      String LocalizedCategoryInstanceName;  
      SMS_Category_LocalizedProperties LocalizedInformation[];  
      UInt32 LocalizedPropertyLocaleID;  
      UInt32 ParentCategoryInstanceID;  
      String SourceSite;  
};  
```  

## Methods  
 The `SMS_UpdateCategoryInstance` class does not define any methods.  

> [!WARNING]
>  The `ResendObjectToAllSites Method in Class SMS_UpdateCategoryInstance` has been deprecated in Configuration Manager.  

## Properties  
 `AllowSubscription`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read]  

 `true` if the category instance is enabled for subscription to the category metadata from the software update source. The default value is `false`. For more information, see [SMS_SoftwareUpdateSource Server WMI Class](../../../develop/reference/sum/sms_softwareupdatesource-server-wmi-class.md).  

> [!NOTE]
>  Not all categories can be marked for subscription.  

 `CategoryInstance_UniqueID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [unique, SizeLimit("512")  

 See [SMS_CategoryInstanceBase Server WMI Class](../../../develop/reference/compliance/sms_categoryinstancebase-server-wmi-class.md).  

 `CategoryInstanceID`  
 Data type: `UInt``3``2`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 See [SMS_CategoryInstanceBase Server WMI Class](../../../develop/reference/compliance/sms_categoryinstancebase-server-wmi-class.md).  

 `CategoryTypeName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_CategoryInstanceBase Server WMI Class](../../../develop/reference/compliance/sms_categoryinstancebase-server-wmi-class.md).  

 `IsSubscribed`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [read]  

 `true` if the category instance allows subscription. The default value is `false`. Set this property to `true` only if the `AllowSubscription` property is set to `true`.  

 `LocalizedCategoryInstanceName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_CategoryInstanceBase Server WMI Class](../../../develop/reference/compliance/sms_categoryinstancebase-server-wmi-class.md).  

 `LocalizedInformation`  
 Data type: `SMS_Category_LocalizedProperties Array` Access type: Read/Write  

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

- Read (read-only)  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

  Your application uses the `SMS_UpdateCategoryInstance` class after creating or modifying a software update deployment using [SMS_UpdatesAssignment Server WMI Class](../../../develop/reference/sum/sms_updatesassignment-server-wmi-class.md). The application can use [SMS_CIAllCategories Server WMI Class](../../../develop/reference/sum/sms_ciallcategories-server-wmi-class.md) to query for all categories associated with the software updates configuration item or for all configuration items associated with a category.  

  To use this class, the application obtains an `SMS_SoftwareUpdateSource` object and sets the properties as required for the particular software update and the source.  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_CIAllCategories Server WMI Class](../../../develop/reference/sum/sms_ciallcategories-server-wmi-class.md)   
 [About software update deployments](../../sum/about-software-updates-deployments.md)
