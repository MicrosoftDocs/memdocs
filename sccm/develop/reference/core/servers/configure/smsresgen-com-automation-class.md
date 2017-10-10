---
title: "SMSResGen COM Automation Class"
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
ms.assetid: 98b96b3e-3689-4cec-8617-597c2c850f19searchScope: - ConfigMgr SDK
caps.latest.revision: 11
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMSResGen COM Automation Class
The `SMSResGen` COM class, in Configuration Manager, is used to create data discovery records (DDRs).  

## Methods  

|Name|Description|  
|----------|-----------------|  
|[ISMSResGen Interface](../../../../../develop/reference/core/servers/configure/ismsresgen-interface.md)|Defines the data discovery record methods.|  

## Remarks  
 `SMSResGen` is found in SMSResGenCtl.dll. Use the [ISMSResGen Interface](../../../../../develop/reference/core/servers/configure/ismsresgen-interface.md) interface to create and use DDRs.  

> [!IMPORTANT]
>  The SMSResGenCtl.dll file is part of the downloadable SDK.  

 Because the `SMSResGen` control is not thread safe, do not try to create more than one instance of this class.  

> [!IMPORTANT]
>  The function `DDRSendToSMS`, available in previous releases of the SDK and in versions of `SMSRsGen.dll`/`SMSResGenCtl.dll`, has been deprecated and should not be used with Configuration Manager.  

 The CLSID for `SMSResGen` is 19352BAD-BEE0-4193-95C4-588B6C5DBCD1.  

## Requirements  

### Runtime Requirements  
 smsrsgenctl.dll  

 smsrsgen.dll  

 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [ISMSResGen Interface](../../../../../develop/reference/core/servers/configure/ismsresgen-interface.md)
