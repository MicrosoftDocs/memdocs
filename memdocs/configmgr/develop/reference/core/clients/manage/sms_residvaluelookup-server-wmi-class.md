---
title: "SMS_ResIDValueLookup Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: b4e19017-3d4a-48aa-a569-16a1a3aa9fd1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_ResIDValueLookup Server WMI Class
The `SMS_ResIDValueLookup` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that maps integers to localized text strings found in a resource DLL.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_ResIDValueLookup   
{  
     String LookupName;  
     UInt32 IntLookupValue;  
     String StringLookupValue;  
     String ResDLL;  
     UInt32 ResID;  
};  
```  

## Methods  
 The `SMS_ResIDValueLookup` class does not define any methods.  

## Properties  
 `LookupName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Name specified in the ResIDValueLookup property qualifier.  

 `IntLookupValue`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Value from the property to be localized. Specify a value for this property if the data type of the property to be localized is an integer. The default value is 0.  

 `StringLookupValue`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Value from the property to be localized. Specify a value for this property if the data type of the property to be localized is a string. The default value is "".  

 `ResDLL`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Resource DLL name from which to retrieve a localized string. The default value is "".  

 `ResID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Resource ID from which to retrieve the localized string. The default value is 0.  

## Remarks  
 Class qualifiers for this class include:  

- Static  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

  The Configuration Manager console uses this class to convert enumerated property values into localized text strings. The console uses the ResIDValueLookup qualifier value and the property value of the class instance to look up the location of the localized string.  

  For example, to get the location of the localized string for the `Priority` property of [SMS_Package Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_package-server-wmi-class.md), the property must contain a ResIDValueLookup property qualifier:  

1. Get the property value.  

2. Either query `SMS_ResIDValueLookup` or get the object directly by specifying the full path. The query and the object path are as follows.  

   ```  
   SELECT * FROM SMS_ResIDValueLookup  
   WHERE LookupName = < property qualifier value>  
   AND IntLookupValue = <property value>  

   SMS_ResIDValueLookup.IntLookupValue=<property value>,LookupName="<qualifier value>",StringLookupValue=""  
   ```  

   When you have the location and resource identifier, you can use the `LoadString` Win32 function to return the localized text string for the Priority value.  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  
