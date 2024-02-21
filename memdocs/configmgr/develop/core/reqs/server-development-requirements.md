---
title: Server Development Requirements
titleSuffix: Configuration Manager
description: The SMS Provider and associated technologies can be programmed by using managed code, VBScript, C++, and other languages.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: conceptual
ms.assetid: 186d3283-419b-417f-a168-0b7fba5ec628
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# Configuration Manager Server Development Requirements
In Configuration Manager, the SMS Provider and associated technologies can be programmed by using the following programming languages.  

## Managed Code  
 The Configuration Manager SDK provides Microsoft .NET Framework libraries for accessing the SMS Provider and also for extending the Configuration Manager console.  

> [!NOTE]
>  You can also use the System.Management namespace for accessing the SMS Provider, but this approach is not documented in the Configuration Manager SDK.  

 Programming the SMS Provider with managed code has the following requirements:  

-   Installed Configuration Manager site server  

-   Microsoft.ConfigurationManagement.ManagementProvider .NET Framework assembly.  

-   Microsoft Visual Studio   

-   Microsoft .NET Framework version 4  

### NET Framework  
 You should have version 4 of the .NET Framework installed on the development computer and on the computers you want to deploy your .NET Framework application to. To download the .NET Framework redistributable package, see [Download .NET Framework](https://dotnet.microsoft.com/download/dotnet-framework). It is also installed as part of Visual Studio.  

## Configuration Manager Console User Interface Extension  
 Programming Configuration Manager console extensions has the following requirements:  

- Installed Configuration Manager site server  

- Installed Configuration Manager console  

- Microsoft Visual Studio   

- Microsoft.ConfigurationManagement.ManagementProvider .NET Framework assembly.  

- Microsoft .NET Framework 4  

  For more information, see [About console extensions](../servers/console/about-configuration-manager-console-extension.md).  

  For specific information about deploying Configuration Manager console extensions, see [Configuration Manager Console Extension Deployment](../../../develop/core/servers/console/console-extension-deployment.md)  

## VBScript  
 You can use Windows Management Instrumentation (WMI) to access the SMS Provider.  

 The scripting samples are provided in VBScript and use WMI to access Configuration Manager. For more information, see [Objects overview](../understand/configuration-manager-objects-overview.md).  

 Programming the SMS Provider with VBScript has the following requirements:  

- Installed Configuration Manager site server  

- Windows Script Host  

  For more information about scripting with WMI, see [Windows Management Instrumentation](/windows/win32/wmisdk/wmi-start-page).  

## C++  
 C++ examples are provided for some Configuration Manager technologies where C++ is the most appropriate development language. In most cases, C++ developers should use the VBScript samples as a guide. For more information about using WMI with C++, see [Creating a WMI Application Using C++](/windows/win32/wmisdk/creating-a-wmi-application-using-c-).  

## Other Languages  
 For languages that are not based on the .NET Framework, use the VBScript samples as a starting point for accessing Configuration Manager through WMI.  

> [!IMPORTANT]
>  For more information about general Configuration Manager requirements, see [Supported configurations](../../../core/plan-design/configs/supported-configurations.md).  

## See Also  
 [Configuration Manager Client Development Requirements](../../../develop/core/reqs/client-development-requirements.md)   
 [Configuration Manager SDK Libraries and Header Files](../../../develop/core/reqs/configuration-manager-sdk-libraries-and-header-files.md)
