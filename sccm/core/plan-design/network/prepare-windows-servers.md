---
title: "Prepare Windows Servers"
titleSuffix: "Configuration Manager"
description: "Ensure that a computer meets prerequisites for use as a site server or a site system server for System Center Configuration Manager."
ms.custom: na
ms.date: 2/14/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 2aca914f-641e-4bc8-98d4-bbf0a2a5276f
caps.latest.revision: 10
caps.handback.revision: 0
author: mstewart
ms.author: mstewart
manager: angrobe

---
# Prepare Windows Servers to support System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Before you can use a Windows computer as a site system server for System Center Configuration Manager, the computer must meet the prerequisites for its intended use as a site server or site system server.  

-   These prerequisites often include one or more Windows features or roles, which are enabled by using the computers Server Manager.  

-   Because the method to enable Windows features and roles differs among operating systems, refer to the documentation for your operating system for detailed information about how to set up the operating system that you use.  

The information in this article provides an overview of the types of Windows configurations that are required to support Configuration Manager site systems. For configuration details for specific site system roles, see [Site and site system prerequisites](/sccm/core/plan-design/configs/site-and-site-system-prerequisites).

##  <a name="BKMK_WinFeatures"></a> Windows features and roles  
 When you set up Windows features and roles on a computer, you might be required to reboot the computer to complete that configuration. Therefore, it's a good idea to identify computers that will host specific site system roles before you install a Configuration Manager site or site system server.
### Features  
 The following Windows features are required on certain site system servers and should be set up before you install a site system role on that computer.  

-   **.NET Framework**: Including  

    -   ASP.NET  
    -   HTTP Activation  
    -   Non-HTTP Activation  
    -   Windows Communication Foundation (WCF) Services  

    Different site system roles require different versions of .NET Framework.  

    Because .NET Framework 4.0 and later is not backward compatible to replace 3.5 and earlier versions, when different versions are listed as required, plan to enable each version on the same computer.  

-   **Background Intelligent Transfer Services (BITS)**: Management points require BITS (and automatically selected options) to support communication with managed devices.  

-   **BranchCache**: Distribution points can be set up with BranchCache to support clients that use BranchCache.  

-   **Data Deduplication**: Distribution points can be set up with and benefit from data deduplication.  

-   **Remote Differential Compression (RDC)**: Each computer that hosts a site server or a distribution point requires RDC.   
    RDC is used to generate package signatures and perform signature comparisons.  

### Roles  
 The following Windows roles are required to support specific functionality, like software updates and operating system deployments, while IIS is required by the most common site system roles.  

 -   **Network Device Enrollment Service** (under Active Directory Certificate Services):  This Windows role is a prerequisite to use Certificate Profiles in Configuration Manager.  

 -   **Web server (IIS)**: Including:  
    -   Common HTTP Features >  
        -   HTTP Redirection  
    -   Application Development >  
        -   .NET Extensibility  
        -   ASP.NET  
        -   ISAPI Extensions  
        -   ISAPI Filters  
    -   Management Tools >  
        -   IIS 6 Management Compatibility  
        -   IIS 6 Metabase Compatibility  
        -   IIS 6 Windows Management Instrumentation (WMI) Compatibility  
    -   Security >  
        -   Request Filtering  
        -   Windows Authentication  

 The following site system roles use one or more of the listed IIS configurations:  
    -   Application Catalog web service point  
    -   Application Catalog website point  
    -   Distribution point  
    -   Enrollment point  
    -   Enrollment proxy point  
    -   Fallback status point  
    -   Management point  
    -   Software update point  
    -   State migration point     

    The minimum version of IIS that is required is the version that is supplied with the operating system of the site server.  

    In addition to these IIS configurations, you might need to set up [IIS Request Filtering for distribution points](#BKMK_IISFiltering).  

-   **Windows Deployment Services**: This role is used with Operating System Deployment.  
-   **Windows Server Update Services**: This role is required when you will deploy software updates.  

##  <a name="BKMK_IISFiltering"></a> IIS Request Filtering for distribution points  
 By default, IIS uses Request Filtering to block several file name extensions and folder locations from access by HTTP or HTTPS communication. On a distribution point, this prevents clients from downloading packages that have blocked extensions or folder locations.  

 When your package source files have extensions that are blocked in IIS by your Request Filtering configuration, you must set up Request Filtering to allow them. This is done by [editing the Request Filtering Feature](https://technet.microsoft.com/library/hh831621.aspx) in the IIS Manager on your distribution point computers.  

 Additionally, the following file name extensions are used by Configuration Manager for packages and applications. Make sure that your Request Filtering configurations do not block these file extensions:  

-   .PCK  
-   .PKG  
-   .STA  
-   .TAR  

For example, source files for a software deployment might include a folder named **bin** or have a file that has the **.mdb** file name extension.  

-   By default, IIS Request Filtering blocks access to these elements (**bin** is blocked as a Hidden Segment and **.mdb** is blocked as a File Name Extension).  

-   When you use the default IIS configuration on a distribution point, clients that use BITS fail to download this software deployment from the distribution point and indicate that they are waiting for content.  

-   To let the clients download this content, on each applicable distribution point, edit **Request Filtering** in IIS Manager to allow access to the file extensions and folders that are in the packages and applications that you deploy.  

> [!IMPORTANT]  
>  Edits to the Request Filter can increase the attack surface of the computer.  
>   
>  -   Edits that you make at the server level apply to all websites on the server.  
> -   Edits that you make to individual websites apply to only that website.  
>   
>  The security best practice is to run Configuration Manager on a dedicated web server. If you must run other applications on the web server, use a custom website for Configuration Manager. For information, see [Websites for site system servers in System Center Configuration Manager](../../../core/plan-design/network/websites-for-site-system-servers.md).  

## HTTP verbs
**Management points:** To ensure that clients can successfully communicate with a management point, on the management point server ensure the following HTTP verbs are allowed:  
 - GET
 - POST
 - CCM_POST
 - HEAD
 - PROPFIND

**Distribution points:** Distribution points require that the following HTTP verbs as allowed:
 - GET
 - HEAD
 - PROPFIND

For information about how to configure Request Filtering, see [Configure Request Filtering in IIS](https://technet.microsoft.com/library/hh831621.aspx#Verbs) on TechNet or similar documentation that applies to the version of Windows Server that hosts your management point.
