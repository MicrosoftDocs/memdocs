---
title: "SDK Libraries and Header Files"
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
ms.assetid: c3dbe6c9-31ba-48bb-b055-18a0a536e3eesearchScope: - ConfigMgr SDK
caps.latest.revision: 19
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# Configuration Manager SDK Libraries and Header Files
In System Center Configuration Manager, when you write unmanaged applications, you might have to include one or more of the following libraries, which are included with the Configuration Manager SDK. Use COM Interoperability to access COM objects from .NET Framework applications.  

|Library|Description|  
|-------------|-----------------|  
|ismifcom.dll|Contains a class wrapper for the install status MIF functions. Visual Basic and scripting programmers use this ActiveX control to create a status MIF file.<br /><br /> Visual Basic users must select the ISMIFCOM 1.0 Type Library project reference. Scripting users create this object by using "ISMIFCOM.InstallStatusMIF".|  
|Microsoft.ConfigurationManager.Messaging.dll|Contains A .NET assembly encapsulating the client SDK that has an object model and transport for communicating with Configuration Manager site server roles such as the management point.|  
|smsmsgapi.dll|Contains management point interface libraries.|  
|smsrsgen.dll|Contains the Discovery Data Record functions. This DLL must exist in the directory from where you start your application.|  
|smsrsgenctl.dll|Contains a class wrapper for the Discovery Data Record Functions. Visual Basic and scripting programmers use this control to create discovery data records.|  

> [!NOTE]
>  The library files can be found in the %Program Files%\Microsoft System Center 2012 Configuration Manager SDK\Redistributables folder.  

> [!IMPORTANT]
>  The tsmediaapi.dll file is incorrectly listed as a redistributable file in the `redist.txt` file in the % Program Files %\Microsoft System Center 2012 Configuration Manager SDK\Redistributables folder. The tsmediaapi.dll file is no longer included in the SDK.  

 You might have to include one or more of the following header files, which are included with the Configuration Manager SDK.  

|Header file|Description|  
|-----------------|-----------------|  
|Smscstat.h|Contains header information for creating status messages.|  
|Ssperrcode.h|Contains the error codes and macros that are used to evaluate an error condition that is returned from the SMS Provider.|  

> [!NOTE]
>  The header files can be found in the % Program Files %\Microsoft System Center 2012 Configuration Manager SDK\Samples\Includes folder.  

> [!IMPORTANT]
>  For more information about general System Center Configuration Manager requirements, see [Supported Configurations for Configuration Manager](http://go.microsoft.com/fwlink/p/?LinkId=248211).  

## See Also  
 [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md)   
 [Configuration Manager Client Development Requirements](../../../develop/core/reqs/client-development-requirements.md)
