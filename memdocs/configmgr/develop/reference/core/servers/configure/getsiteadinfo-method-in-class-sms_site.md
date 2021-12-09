---
title: "GetSiteADInfo Method"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 34cd1ffb-97f9-4177-8b1b-751203358528
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# GetSiteADInfo Method in Class SMS_Site
The `GetSiteADInfo` Windows Management Instrumentation (WMI) class method, in Configuration Manager, gets Active Directory information of site server.  

 The following syntax is simplified from Managed Object Format (MOF) code and is intended to show the definition of the method.  

## Syntax  

```  
SInt32 GetSiteADInfo(  
   String SiteCode,  
   String DCName,  
   String DCAddress,  
   String DomainName,  
   String ForestName,  
   String DCSiteName,  
   String ClientSiteName  
);  
```  

#### Parameters  
 `SiteCode`  
 Data type: `String`  

 Qualifiers: [in]  

 Site code.   

 `DCName`  
 Data type: `String`  

 Qualifiers: [out]  

 Name of the Active Directory domain controller.  

 `DCAddress`  
 Data type: `String`  

 Qualifiers: [out]  

 Domain controller address.  

 `DomainName`  
 Data type: `String`  

 Qualifiers: [out]  

 Domain name.  

 `ForestName`  
 Data type: `String`  

 Qualifiers: [out]  

 Name of the Active Directory forest.  

 `DCSiteName`  
 Data type: `String`  

 Qualifiers: [out]  

 Name of the Active Directory site where the domain controller is located.  

 `ClientSiteName`  
 Data type: `String`  

 Qualifiers: [out]  

 Name of the site that the computer belongs to.  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For information about handling returned errors, see [About Configuration Manager Errors](../../../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_Identification Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_identification-server-wmi-class.md)
