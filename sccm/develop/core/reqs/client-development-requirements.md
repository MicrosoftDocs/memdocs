---
title: "Client Development Requirements"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 7114139b-9615-4057-9a60-afa877346b2d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
---
# Configuration Manager Client Development Requirements
The Configuration Manager client can be programmed by using the following programming languages.  

## Managed Code  
 If you are programming the Configuration Manager client by using managed code, you use the System.Management namespace and, where applicable, you use COM Interoperability to access the Configuration Manager automation objects.  

### NET Framework  
 You should have version 4.0 of the Microsoft .NET Framework installed on the development computer and on the computers you want to deploy your .NET Framework application to. The .NET Framework redistributable package is available from the [Microsoft Download Center](https://go.microsoft.com/fwlink/?LinkID=276779). It is also installed as part of Visual Studio 2010.  

## VBScript  
 You can use VBScript to access the Configuration Manager client WMI namespaces. The client also has a number of COM automation objects that you can use.  

 For more information about scripting with WMI, see [Windows Management Instrumentation](https://go.microsoft.com/fwlink/?LinkID=276770).  

## C++  
 C++ examples are provided for some Configuration Manager technologies where C++ is the most appropriate development language. In most cases, C++ developers should use the VBScript samples as a guide. For more information about using WMI with C++, see [Creating a WMI Application Using C++](https://go.microsoft.com/fwlink/?LinkID=276780).  

## Other Languages  
 For languages that are not based on .NET Framework, use the VBScript samples as a starting point for accessing Configuration Manager through WMI.  

> [!IMPORTANT]
>  For more information about general Configuration Manager requirements, see [Supported Configurations for Configuration Manager](https://go.microsoft.com/fwlink/p/?LinkId=248211).  

## See Also  
 [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md)   
 [Configuration Manager SDK Libraries and Header Files](../../../develop/core/reqs/configuration-manager-sdk-libraries-and-header-files.md)
