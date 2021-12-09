---
title: "Class and Property Qualifiers"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 836a5204-4439-4fbd-a5d2-0b7796ae24ae
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# Configuration Manager Class and Property Qualifiers
The following table shows the qualifiers that are specific to Microsoft Configuration Manager.  

|Qualifier|Description|  
|---------------|-----------------|  
|`Bits` (property)|A bit position of a Boolean flag in a bit field.|  
|`Embedded` (class)|A textual description that indicates that the class is used as an embedded object. Individual instances of embedded classes cannot be created.|  
|`Enumeration` (property)|A list of valid string names for a discrete enumeration.|  
|`Lazy` (property)|A property that is returned only for a `GetObject` operation (that is, omitted from the result class instance for an enumeration or a query).|  
|`Range` (property)|A range of permitted values for a string or integer that has the following format:<br /><br /> `<Low Value>-<High Value>`|  
|`ResID` (class or property)|**Important:**  This qualifier is not used in Configuration Manager. <br /><br /> A string identifier in a resource DLL that contains the localized class or property name. The `ResID` qualifiers always used with `ResDLL`.|  
|`ResIDValueLookup`|**Important:**  This qualifier is not used in Configuration Manager. <br /><br /> A qualifier that assists in the translation of an enumeration property to a localized string representation found in a DLL. To use this qualifier, query `SMS_ResIDValueLookup` with the `ResIDValueLookup` value and the property value (`IntLookupValue` for integers and `StringLookupValue` for strings). The `ResDLL` property of the resulting `ResIDValueLookup` instance will contain the resource DLL name containing the localized string, and the `ResID` property will be set to the string ID in the DLL.|  
|`ResDLL` (class/property)|**Important:**  This qualifier is not used in Configuration Manager. <br /><br /> The name of the resource DLL that contains the localized class property name.|  
|`Secured` (class)|An indicator that a class requires special rights to read or manipulate.|  
|`SecurityVerbs` (instance)|**Important:**  This qualifier is not used in Configuration Manager. This functionality has been superseded by the role-based administration security model. <br /><br /> A bit field used on instances of secured objects to describe the rights that a requesting user has on the object. The meanings of the bits are the same as those found in the `AvailableInstancePermissions` property of the `SMS_SecuredObject` class.|  
|`SizeLimit` (property)|The size limit of the data, which depends on the property data type:<br /><br /> `<low length>-<high length>`<br /><br /> or<br /><br /> `<specific length>`|  

## See Also  
 [Configuration Manager SDK](../../../develop/core/misc/system-center-configuration-manager-sdk.md)   
 [Configuration Manager Reference](../../../develop/reference/configuration-manager-reference.md)
