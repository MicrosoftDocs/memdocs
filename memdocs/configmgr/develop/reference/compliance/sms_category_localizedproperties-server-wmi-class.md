---
title: SMS_Category_LocalizedProperties Class
titleSuffix: Configuration Manager
description: The SMS_Category_LocalizedProperties Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that describes various localized properties for a category, for example, a product or a classification.
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 1ffc950b-4a68-4d59-8080-dc5393f71a20
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_Category_LocalizedProperties Server WMI Class
The `SMS_Category_LocalizedProperties` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that describes various localized properties for a category, for example, a product or a classification.  

## Syntax  

```  
Class SMS_Category_LocalizedProperties  
{  
      String CategoryInstanceName;  
      UInt32 LocaleID;  
};  
```  

## Methods  
 The `SMS_Category_LocalizedProperties` class does not define any methods.  

## Properties  
 `CategoryInstanceName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Display name of the category instance. The default value is "".  

 `LocaleID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 ID for the locale associated with the category instance.  

## Remarks  
 Class qualifiers for this class include:  

- Embedded  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

  Your application uses this class to create objects that are embedded by [SMS_CategoryInstance Server WMI Class](../../../develop/reference/compliance/sms_categoryinstance-server-wmi-class.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Configuration Manager Compliance Settings (DCM) Server WMI Classes](../../../develop/reference/compliance/compliance-settings-dcm-server-wmi-classes.md)   
 [SMS_CategoryInstance Server WMI Class](../../../develop/reference/compliance/sms_categoryinstance-server-wmi-class.md)
