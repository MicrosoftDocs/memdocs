---
title: "UnPackNALPath Method"
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
ms.assetid: 76960011-6155-4295-8c5c-d7181018011esearchScope: - ConfigMgr SDK
caps.latest.revision: 10
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# UnPackNALPath Method in Class SMS_NAL_Methods
The `UnPackNALPath` method, in Configuration Manager, decodes a network abstraction layer (NAL) path into its components.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 UnPackNALPath(  
     String NALPath,  
     String DisplayQualifiers[],  
     String NALType,   
     String NetworkOSPath,   
     String NetworkConnectionQualifiers[]  
);  
```  

#### Parameters  
 `NALPath`  
 Data type: `String`  

 Qualifiers: [in]  

 NAL path to be decoded.  

 `DisplayQualifiers`  
 Data type: `String` Array  

 Qualifiers: [out]  

 Qualifiers used by the Configuration Manager console. See the `DisplayQualifiers` property of [PackNALPath Method in Class SMS_NAL_Methods](../../../develop/reference/misc/packnalpath-method-in-class-sms_nal_methods.md).  

 `NALType`  
 Data type: `String`  

 Qualifiers: [out]  

 The NAL type specified by the network operating system. See the `NALType` property of [PackNALPath Method in Class SMS_NAL_Methods](../../../develop/reference/misc/packnalpath-method-in-class-sms_nal_methods.md).  

 `NetworkOSPath`  
 Data type: `String`  

 Qualifiers: [out]  

 Network operating system path. See the `NetworkOSPath` property of [PackNALPath Method in Class SMS_NAL_Methods](../../../develop/reference/misc/packnalpath-method-in-class-sms_nal_methods.md).  

 `NetworkConnectionQualifiers`  
 Data type: `String` Array  

 Qualifiers: [out]  

 Configuration Manager component-specific qualifiers. See the `NetworkConnectionQualifiers` property of [PackNALPath Method in Class SMS_NAL_Methods](../../../develop/reference/misc/packnalpath-method-in-class-sms_nal_methods.md).  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For information about handling returned errors, see [About Configuration Manager Errors](../../../develop/core/understand/about-configuration-manager-errors.md).  

## Example Code  
 The following example decodes a NAL path.  

```  
Dim clsNALMethods As SWbemObject  
Dim NALPath As String  
Dim DisplayQuals() As Variant  
Dim NALType As String  
Dim NOSPath As String  
Dim NOSQuals() As Variant  
Dim instResources As SWbemObjectSet  
Dim instResource As SWbemObject  
Dim Query As String  

Set clsNALMethods = Services.Get("SMS_NAL_Methods")  

Query = "SELECT * FROM SMS_SystemResourceList " & _  
        "WHERE RoleName=""SMS Distribution Point"" AND SiteCode=""<site code>"""  
Set instResources = Services.ExecQuery(Query, , wbemFlagForwardOnly Or wbemFlagReturnImmediately)  

For Each instResource In instResources  
    NALPath = instResource.NALPath  

    clsNALMethods.UnPackNALPath NALPath, DisplayQuals, NALType, NOSPath, NOSQuals  
    MsgBox "Path = " & NALPath & vbCrLf & _  
           "Display = " & DisplayQuals(0) & vbCrLf & _  
           "Type = " & NALType & vbCrLf & _  
           "NOSPath = " & NOSPath & vbCrLf & _  
           "NOSQual = " & NOSQuals(0)  
Next  
```  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_NAL_Methods Class](../../../develop/reference/misc/sms_nal_methods-server-wmi-class.md)   
 [PackNALPath Method in Class SMS_NAL_Methods](../../../develop/reference/misc/packnalpath-method-in-class-sms_nal_methods.md)
