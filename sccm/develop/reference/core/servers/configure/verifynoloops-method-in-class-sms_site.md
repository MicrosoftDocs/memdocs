---
title: "VerifyNoLoops Method"
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
ms.assetid: 1abbb982-f594-4ccb-87c4-906154245644searchScope: - ConfigMgr SDK
caps.latest.revision: 6
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# VerifyNoLoops Method in Class SMS_Site
The `VerifyNoLoops` Windows Management Instrumentation (WMI) class method, in Configuration Manager, determines if the insertion of a site in the Configuration Manager hierarchy at a specific point will result in a recursive loop of the sites.  

 The following syntax is simplified from Managed Object Format (MOF) code and is intended to show the definition of the method.  

## Syntax  

```  
SInt32 VerifyNoLoops(  
     String CentralSiteCode,  
     String TargetSiteCode,  
     String ParentSiteCode,  
     Boolean Result  
);  
```  

#### Parameters  
 `CentralSiteCode`  
 Data type: `String`  

 Qualifiers: [in, SizeLimit("3")]  

 Not used.  

 `TargetSiteCode`  
 Data type: `String`  

 Qualifiers: [in, SizeLimit("3")]  

 Site code of the child site to insert.  

 `ParentSiteCode`  
 Data type: `String`  

 Qualifiers: [in, SizeLimit("3")]  

 Site code of the site that will be the parent of the target site.  

 `Result`  
 Data type: `Boolean`  

 Qualifiers: [out]  

 `true` if no loop is formed by inserting the new site in the Configuration Manager hierarchy  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For information about handling returned errors, see [About Configuration Manager Errors](../../../../../develop/core/understand/about-configuration-manager-errors.md).  

## Example Code  
 The following example shows how to call the `VerifyNoLoops` method.  

```  
Dim Site As SWbemObject  
Dim NoLoop As Boolean  

Set Site = GetObject("winmgmts:root\sms\site_<sitecode>:SMS_Site")  
Site.VerifyNoLoops "", "<child sitecode>", "<parent sitecode>", NoLoop  

MsgBox "NoLoop = " & NoLoop  
```  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_Site Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_site-server-wmi-class.md)
