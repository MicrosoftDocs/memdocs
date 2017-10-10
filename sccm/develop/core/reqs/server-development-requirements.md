---
title: "Server Development Requirements"
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
ms.assetid: 186d3283-419b-417f-a168-0b7fba5ec628searchScope: - ConfigMgr SDK
caps.latest.revision: 15
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# Configuration Manager Server Development Requirements
In System Center Configuration Manager, the SMS Provider and associated technologies can be programmed by using the following programming languages.  

## Managed Code  
 The Configuration Manager SDK provides Microsoft .NET Framework libraries for accessing the SMS Provider and also for extending the Configuration Manager console.  

> [!NOTE]
>  You can also use the System.Management namespace for accessing the SMS Provider, but this approach is not documented in the Configuration Manager SDK.  

 Programming the SMS Provider with managed code has the following requirements:  

-   Installed Configuration Manager site server  

-   Microsoft.ConfigurationManagement.ManagementProvider .NET Framework assembly.  

-   Microsoft Visual Studio 2010  

-   Microsoft .NET Framework version 4  

### NET Framework  
 You should have version 4 of the .NET Framework installed on the development computer and on the computers you want to deploy your .NET Framework application to. The .NET Framework redistributable package is available from the [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkID=276779). It is also installed as part of Visual Studio 2010.  

## Configuration Manager Console User Interface Extension  
 Programming Configuration Manager console extensions has the following requirements:  

-   Installed Configuration Manager site server  

-   Installed Configuration Manager console  

-   Microsoft Visual Studio 2010  

-   Microsoft.ConfigurationManagement.ManagementProvider .NET Framework assembly.  

-   Microsoft .NET Framework 4  

 For more information, see [Configuration Manager Console Extension](../../../develop/core/servers/console/console-extension.md)  

 For specific information about deploying System Center Configuration Manager console extensions, see [Configuration Manager Console Extension Deployment](../../../develop/core/servers/console/console-extension-deployment.md)  

## VBScript  
 You can use Windows Management Instrumentation (WMI) to access the SMS Provider.  

 The scripting samples are provided in VBScript and use WMI to access Configuration Manager. For more information, see [How to Use Configuration Manager Objects with WMI](../../../develop/core/understand/how-to-use-configuration-manager-objects-with-wmi.md).  

 Programming the SMS Provider with VBScript has the following requirements:  

-   Installed Configuration Manager site server  

-   Windows Script Host  

 For more information about scripting with WMI, see [Windows Management Instrumentation](http://go.microsoft.com/fwlink/?LinkID=276770).  

## C++  
 C++ examples are provided for some Configuration Manager technologies where C++ is the most appropriate development language. In most cases, C++ developers should use the VBScript samples as a guide. For more information about using WMI with C++, see [Creating a WMI Application Using C++](http://go.microsoft.com/fwlink/?LinkId=276780).  

## Other Languages  
 For languages that are not based on the .NET Framework, use the VBScript samples as a starting point for accessing Configuration Manager through WMI.  

> [!IMPORTANT]
>  For more information about general System Center Configuration Manager requirements, see [Supported Configurations for Configuration Manager](http://go.microsoft.com/fwlink/?LinkId=276781).  

## See Also  
 [Configuration Manager Client Development Requirements](../../../develop/core/reqs/client-development-requirements.md)   
 [Configuration Manager SDK Libraries and Header Files](../../../develop/core/reqs/configuration-manager-sdk-libraries-and-header-files.md)
