---
title: "SMS_NAL_Methods Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: b9e16ee5-11c1-4d82-9ff4-73612137e243
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_NAL_Methods Server WMI Class
The `SMS_NAL_Methods` Windows Management Instrumentation (WMI) class, in Configuration Manager, defines and manipulates a network abstraction layer (NAL) path.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_NAL_Methods : SMS_BaseClass ();  

```  

## Methods  
 The following table lists the methods in `SMS_NAL_Methods`.  

|Method|Description|  
|------------|-----------------|  
|[PackNALPath](../../../develop/reference/misc/packnalpath-method-in-class-sms_nal_methods.md)|Encodes a NAL path from its components.|  
|[UnPackNALPath](../../../develop/reference/misc/unpacknalpath-method-in-class-sms_nal_methods.md)|Decodes a NAL path into its components.|  

## Properties  
 The `SMS_NAL_Methods` class does not define any properties.  

## Remarks  
 Class qualifiers for this class include:  

-   Abstract  

 For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Configuration Manager Supporting Classes](../../../develop/reference/misc/supporting-server-wmi-classes.md)   
 [SMS_DistributionPoint Server WMI Class](../../../develop/reference/core/servers/configure/sms_distributionpoint-server-wmi-class.md)   
 [SMS_SCI_SysResUse Server WMI Class](../../../develop/reference/core/servers/configure/sms_sci_sysresuse-server-wmi-class.md)   
 [SMS_SystemResourceList Server WMI Class](../../../develop/reference/core/servers/configure/sms_systemresourcelist-server-wmi-class.md)
