---
title: "AddContent Method"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 09bf18d9-4e97-42ee-bb5c-a87d2556449d
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# AddContent Method in Class SMS_ContentPackage
The `AddContent` Windows Management Instrumentation (WMI) class method, in Configuration Manager, adds content to the [SMS_ContentPackage Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_contentpackage-server-wmi-class.md) content package.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
sint32 AddContent (  
     string ContentID[],  
     uint32 ContentVersion[]  
     string ContentSource[],  
     uint32 ContentFlags[]  
     uint32 ContentType[],  
     string RelatedContentID[]  
);  
```  

#### Parameters  
 `ContentID`  
 Data type: `string` Array  

 Qualifiers: `[in]`  

 Identifier of the content.  

 `ContentVersion`  
 Data type: `UInt32` Array  

 Qualifiers: `[in]`  

 Version of the content.  

 `ContentSource`  
 Data type: `String` Array  

 Qualifiers: `[in]`  

 Specifies the source location where content files are stored.  

 `ContentFlags`  
 Data type: `UInt32` Array  

 Qualifiers: `[in]`  

 This specifies additional attributes for the content instance.  

|||  
|-|-|  
|8|DOWNLOAD_ON_DEMAND_FROM_LOCAL_DP|  
|12|DOWNLOAD_FROM_LOCAL_DISPPOINT|  
|13|DOWNLOAD_LOCAL_PARTIALDOWNLOADTOLOCAL|  
|14|DOWNLOAD_FROM_REMOTE_DISPPOINT|  
|15|DOWNLOAD_REMOTE_PARTIALDOWNLOADTOLOCAL|  
|16|DOWNLOAD_ENABLE_PEER_CACHING|  
|17|DP_NO_FALLBACK_UNPROTECTED|  
|24|DO_NOT_DOWNLOAD|  
|25|PERSIST_IN_CACHE|  

 `ContentType`  
 Data type: `UInt32` Array  

 Qualifiers: `[in]`  

 Specifies the type of content.  

 `RelatedContentID`  
 Data type: `string` Array  

 Qualifiers: `[in]`  

 Specifies the related content associated with this content.  

## Return Values  
 An  `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For more information about handling returned errors, see [About Configuration Manager Errors](../../../../../develop/core/understand/about-configuration-manager-errors.md).  

## Remarks  
 The input parameters are a parallel array for each content element.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_Application Server WMI Class](../../../../../develop/reference/apps/sms_application-server-wmi-class.md)   
 [Application Model Server WMI Classes](../../../../../develop/reference/apps/application-management-server-wmi-classes.md)
