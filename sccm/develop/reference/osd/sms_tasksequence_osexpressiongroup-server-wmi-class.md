---
title: "SMS_TaskSequence_OSExpressionGroup Class"
titleSuffix: "Configuration Manager"
ms.custom: ""
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.reviewer: ""
ms.suite: ""
ms.technology:
  - "configmgr-other"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to:
  - "System Center Configuration Manager (current branch)"
ms.assetid: 1d399a59-c2e6-44ae-a0d2-032f2f6e022asearchScope: - ConfigMgr SDK
caps.latest.revision: 14
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_TaskSequence_OSExpressionGroup Server WMI Class
The `SMS_TaskSequence_OSExpressionGroup` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents an evaluation of a single operating system platform in a task sequence. An object of this type is always contained by an [SMS_TaskSequence_OSConditionGroup Server WMI Class](../../../develop/reference/osd/sms_tasksequence_osconditiongroup-server-wmi-class.md) object.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_TaskSequence_OSExpressionGroup : SMS_TaskSequence_ConditionOperator  
{  
      String Name;  
      SMS_TaskSequence_WMIConditionExpression Operands[];  
      String OperatorType;  
      String PlatformArchKey;  
      String PlatformMaxVerKey;  
      String PlatformMinVerKey;  
      String PlatformTypeKey;  
};  
```  

## Methods  
 The `SMS_TaskSequence_OSExpressionGroup` class does not define any methods.  

## Properties  
 `Name`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Optional. The name of an operating system, for example, "Windows XP SP2". The default value is "". See the `DisplayText` property for `SMS_SupportedPlatforms`.  

 `Operands`  
 Data type: `SMS_TaskSequence_WMIConditionExpression`Array  

 Access type: Read/Write  

 Qualifiers: [Not_NULL]  

 See [SMS_TaskSequence_ConditionOperator Server WMI Class](../../../develop/reference/osd/sms_tasksequence_conditionoperator-server-wmi-class.md).  

 Each element of this property is an [SMS_TaskSequence_WMIConditionExpression Server WMI Class](../../../develop/reference/osd/sms_tasksequence_wmiconditionexpression-server-wmi-class.md) object that matches the WQL query for the `SMS_SupportedPlatforms` Server WMI Class object indexed by the platform keys. The expressions are typically built from the WQL query stored in the `Condition` property of `SMS_SupportedPlatforms`. There must be at least one [SMS_TaskSequence_WMIConditionExpression Server WMI Class](../../../develop/reference/osd/sms_tasksequence_wmiconditionexpression-server-wmi-class.md) contained by the [SMS_TaskSequence_OSExpressionGroup Server WMI Class](../../../develop/reference/osd/sms_tasksequence_osexpressiongroup-server-wmi-class.md).  

 `OperatorType`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [Not_NULL]  

 See [SMS_TaskSequence_ConditionOperator Server WMI Class](../../../develop/reference/osd/sms_tasksequence_conditionoperator-server-wmi-class.md).  

 The only operator type supported by this class is "and".  

 `PlatformArchKey`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [Not_Null]  

 Platform key that maps to the `OSPlatform` property for `SMS_SupportedPlatforms` objects. For more information, see the Remarks section later in this topic.  

 `PlatformMaxVerKey`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [Not_Null]  

 Platform key that maps to the `OSMaxVersion` property for `SMS_SupportedPlatforms` objects. For more information, see the Remarks section later in this topic.  

 `PlatformMinVerKey`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [Not_Null]  

 Platform key that maps to the `OSMinVersion` property for SMS_SupportedPlatforms objects. For more information, see the Remarks section later in this topic.  

 `PlatformTypeKey`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [Not_Null]  

 Platform key that maps to the `OSName` property for `SMS_SupportedPlatforms` objects. For more information, see the Remarks section later in this topic.  

## Remarks  
 There are no class qualifiers for this class. For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

 The platform strings specified by `PlatformArchKey`, `PlatformMaxVerKey`, `PlatformMinVerKey`, and `PlatformTypeKey` are used to index the corresponding `SMS_SupportedPlatforms` object instance for the expression.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Operating System Deployment Server WMI Classes](../../../develop/reference/osd/operating-system-deployment-server-wmi-classes.md)   
 [SMS_TaskSequence_ConditionOperator Server WMI Class](../../../develop/reference/osd/sms_tasksequence_conditionoperator-server-wmi-class.md)   
 [SMS_SupportedPlatforms Server WMI Class](../../../develop/reference/core/servers/configure/sms_supportedplatforms-server-wmi-class.md)   
 [SMS_TaskSequence_WMIConditionExpression Server WMI Class](../../../develop/reference/osd/sms_tasksequence_wmiconditionexpression-server-wmi-class.md)
