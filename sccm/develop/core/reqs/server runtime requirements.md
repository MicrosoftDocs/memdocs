---
title: "Server Runtime Requirements | Microsoft Docs"
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
ms.assetid: 567e9945-ad60-4d10-8f67-edc4b31ee914
caps.latest.revision: 11
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# Configuration Manager Server Runtime Requirements
Microsoft System Center Configuration Manager server applications that are developed by using the Configuration Manager SDK, have the following runtime requirements.  

## Managed Code  

-   Supported Windows Server 2008 operating systems for site server installation  

-   Installed Configuration Manager site server  

-   Microsoft.ConfigurationManagement.ManagementProvider .NET Framework assembly  

-   Microsoft .NET Framework version 4  

## Configuration Manager Console User Interface Extension  
 Programming System Center Configuration Manager console extensions has the following requirements:  

-   Installed Configuration Manager site server  

-   Installed Configuration Manager console  

-   .NET Framework 4.0  

 For more information, see [Configuration Manager Console Extension](../../../develop/core/servers/console/console extension.md)  

## VBScript  

-   Installed Configuration Manager site server  

-   Windows Script Host  

## Windows 64-Bit Support  
 A 32-bit compiled application that uses Configuration Manager SDK interfaces to access Configuration Manager client or Configuration Manager server functionality works when it runs in 32-bit emulation on a 64-bit Windows operating system. However, a 64-bit compiled application that uses Configuration Manager SDK interfaces that access 32-bit Configuration Manager client or Configuration Manager server functionality does not work. Similarly, Configuration Manager SDK scripts do not work when the scripting host is a native 64-bit application. A Configuration Manager SDK script does work if it is called from within a 32-bit scripting host.  

## General Requirements  

> [!IMPORTANT]
>  For more information about general System Center Configuration Manager requirements, see [Supported Configurations for Configuration Manager](http://go.microsoft.com/fwlink/p/?LinkId=248211).  

## See Also  
 [Configuration Manager Console Extension](../../../develop/core/servers/console/console extension.md)   
 [Configuration Manager Client Development Requirements](../../../develop/core/reqs/client development requirements.md)   
 [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server development requirements.md)
