---
title: SMS_CIRelation Class
titleSuffix: Configuration Manager
description: Learn about the SMS_CIRelation Server Windows Management Instrumentation (WMI) Class.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 9afb280d-716b-40ae-90bb-0c543b4ac9c7
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_CIRelation Server WMI Class
The `SMS_CIRelation` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that defines the relationship between two configuration items, for example, the superseding of one item by another.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_CIRelation : SMS_BaseClass  
{  
    UInt32 FromCIID;  
    Boolean IsBroken;  
    Boolean IsVersionSpecific;  
    UInt32 Priority;  
    UInt32 RelationType;  
    UInt32 ToCIID;  
};  
```  

## Methods  
 The `SMS_CIRelation` class does not define any methods.  

## Properties  
 `FromCIID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 The ID of one of the configuration items. The value of this property usually depends on the value of `ToCIID` in the context specified by `RelationType`. For example, this property can represent a child configuration item ID (FROMCIID) that is derived from a parent configuration item ID (TOCIID).  

 The ID of a configuration item is represented by the `CI_ID` property of [SMS_ConfigurationItemLatestBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitemlatestbaseclass-server-wmi-class.md).  

 `IsBroken`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read, key]  

 `true` if the relation is broken, otherwise the value will be false.  

 `IsVersionSpecific`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None.  

 See [SMS_ConfigurationItemLatestBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitemlatestbaseclass-server-wmi-class.md).  

 `Priority`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None.  

 One App to deployment type relation (9) has priority.  

 `RelationType`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Type of relationship between configuration items. Possible values are:  

| Value | Relationship type |  
| ----- | ----------------- |  
|1|Bundled|  
|2|Required|  
|3|Prohibited|  
|4|Optional|  
|5|Derived|  
|6|Superseded|  
|7|Self|  
|8|Reference|  
|9|AppToDTReference|  
|10|AppDependence|  
|11|Intention|  
|12|Platform|  
|13|GlobalConditionReference|  
|15|ApplicationSuperSeded|  
|16|ApplicationType|  
|17|ApplicationHost|  
|18|ApplicationInstaller|  
|19|SupersedOrDependent|  
|20|VirtualEnvironmentReference|  
|21|AppDCMReference|  
|22|DeploymentTypeToPolicyTemplateReference|  
|23|CIInheritanceRelation|  

 `ToCIID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 The ID for the second configuration item that is related to the first item. The value of this property usually depends on the value of `FromCIID` in the context specified by `RelationType`. For example, this property can represent a parent configuration item ID (TOCIID) from which a child configuration item ID (FROMCIID) is derived.  

 The ID of a configuration item is represented by the `CI_ID` property of [SMS_ConfigurationItemLatestBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitemlatestbaseclass-server-wmi-class.md).  

## Remarks  
 Class qualifiers for this class include:  

- Read (read-only)  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

  This class is applicable to all types of configuration items, not just software updates. For a discussion of configuration item types, see the `CIType_ID` property of SMS_ConfigurationItemBaseClass Server WMI Class.  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [About software update deployments](../../sum/about-software-updates-deployments.md)
