---
title: "Server Runtime Requirements"
titleSuffix: "Configuration Manager"
ms.date: "3/14/2017"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 567e9945-ad60-4d10-8f67-edc4b31ee914
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# Configuration Manager Server Runtime Requirements
Microsoft System Center Configuration Manager server applications that are developed by using the Configuration Manager SDK, have the following runtime requirements.  

## Managed Code  

-   A supported version of Windows Server as defined in [Supported operating systems for System Center Configuration Manager site system servers](https://docs.microsoft.com/en-us/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers). For more information, see [General Requirements](#general-requirements).

-   Installed Configuration Manager site server  

-   Microsoft.ConfigurationManagement.ManagementProvider .NET Framework assembly  

-   Microsoft .NET Framework version 4  

## Configuration Manager Console User Interface Extension  
 Programming System Center Configuration Manager console extensions has the following requirements:  

- Installed Configuration Manager site server  

- Installed Configuration Manager console  

- .NET Framework 4.0  

  For more information, see [Configuration Manager Console Extension](../../../develop/core/servers/console/console-extension.md)  

## VBScript  

-   Installed Configuration Manager site server  

-   Windows Script Host  

## Windows 64-Bit Support  
 A 32-bit compiled application that uses Configuration Manager SDK interfaces to access Configuration Manager client or Configuration Manager server functionality works when it runs in 32-bit emulation on a 64-bit Windows operating system. However, a 64-bit compiled application that uses Configuration Manager SDK interfaces that access 32-bit Configuration Manager client or Configuration Manager server functionality does not work. Similarly, Configuration Manager SDK scripts do not work when the scripting host is a native 64-bit application. A Configuration Manager SDK script does work if it is called from within a 32-bit scripting host.  

## General Requirements  

> [!IMPORTANT]
>  For more information about general System Center Configuration Manager requirements, see [Supported configurations for System Center Configuration Manager](https://docs.microsoft.com/en-us/sccm/core/plan-design/configs/supported-configurations).  

## See Also  
 [Configuration Manager Console Extension](../../../develop/core/servers/console/console-extension.md)   
 [Configuration Manager Client Development Requirements](../../../develop/core/reqs/client-development-requirements.md)   
 [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md)
