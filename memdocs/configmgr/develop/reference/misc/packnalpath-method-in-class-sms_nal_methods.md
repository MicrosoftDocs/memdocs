---
title: PackNALPath Method
titleSuffix: Configuration Manager
description: Encode a network abstraction layer (NAL) path from its components. A NAL path is an abstract representation of a network path or a user account.
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: bd0d9061-a06f-4dbc-b9b4-8f103bf954fe
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# PackNALPath Method in Class SMS_NAL_Methods
The `PackNALPath` method, in Configuration Manager, encodes a network abstraction layer (NAL) path from its components. A NAL path is an abstract representation of a network path or a user account.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 PackNALPath(  
     String DisplayQualifiers[],  
     String NALType,   
     String NetworkOSPath,   
     String NetworkConnectionQualifiers[],  
     String NALPath  
);  
```  

#### Parameters  
 `DisplayQualifiers`  
 Data type: `String` Array  

 Qualifiers: [in]  

 Qualifiers that are used by the Configuration Manager console. The possible values are: Display=\<path, group, or user>. The value that you specify for the path must be the same as the value that you specify for `NetworkOSPath`. For path formats, see `NetworkOSPath` formats later in this topic.  

 `NALType`  
 Data type: `String`  

 Qualifiers: [in]  

 The NAL type specified by the network operating system. Possible values are:  

| Value | NAL type |
| ----- | -------- |
|GENERIC|All providers accept this account specification. Use this value only when you specify a user or group name.|  
|MSWNET|Windows NT.|  

 `NetworkOSPath`  
 Data type: `String`  

 Qualifiers: [in]  

 The network operating system path. Possible values are:  

|Provider|NetworkOSPath|  
|--------------|---------------------|  
|Windows NT user names|\<domain>\\<user name\>|  
|Windows NT group names|\<domain>\group=\<group name>|  
|Generic group names|GROUP=\<group name>|  
|Windows NT (UNC) computer names|\\\\<computer name\>|  
|Windows NT (UNC) share names|\\\\<computer name\>\\<share name\>|  

 `NetworkConnectionQualifiers`  
 Data type: `String` Array  

 Qualifiers: [in]  

 Optional. Configuration Manager component-specific qualifiers. The possible values are: SMS_SITE=\<site code> [Preferred]. SMS_SITE identifies the site to which the path belongs. Preferred is optional and identifies the path to use when multiple paths are specified.  

 `NALPath`  
 Data type: `String`  

 Qualifiers: [out]  

 Encoded NAL path.  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For information about handling returned errors, see [About Configuration Manager Errors](../../../develop/core/understand/about-configuration-manager-errors.md).  

## Example Code  
 The following example encodes a NAL path for an MSWNET network operating system.  

```  
Dim clsNALMethods As SWbemObject  
Dim NALPath As String  

Set clsNALMethods = Services.Get("SMS_NAL_Methods")  
clsNALMethods.PackNALPath Array("Display=\\<server>"), "MSWNET", _  
"\\<server>", Array("SMS_SITE=<site code>"), NALPath  
```  

## Remarks  
 Your application uses this method when creating a distribution point or defining system resources in the site control file programmatically. The method is not used to create a NAL path of an existing distribution point for an [SMS_DistributionPoint Server WMI Class](../../../develop/reference/core/servers/configure/sms_distributionpoint-server-wmi-class.md) object. To determine the NAL path for an existing distribution point, the application should query the [SMS_SystemResourceList Server WMI Class](../../../develop/reference/core/servers/configure/sms_systemresourcelist-server-wmi-class.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_NAL_Methods Class](../../../develop/reference/misc/sms_nal_methods-server-wmi-class.md)   
 [UnPackNALPath Method in Class SMS_NAL_Methods](../../../develop/reference/misc/unpacknalpath-method-in-class-sms_nal_methods.md)   
 [SMS_DistributionPoint Server WMI Class](../../../develop/reference/core/servers/configure/sms_distributionpoint-server-wmi-class.md)   
 [SMS_SystemResourceList Server WMI Class](../../../develop/reference/core/servers/configure/sms_systemresourcelist-server-wmi-class.md)
