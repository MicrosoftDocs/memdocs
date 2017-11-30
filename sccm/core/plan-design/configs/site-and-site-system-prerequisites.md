---
title: "Site prerequisites"
titleSuffix: "Configuration Manager"
description: "Learn how to configure a Windows computer as a System Center Configuration Manager site system server."
ms.custom: na
ms.date: 8/25/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1392797b-76cb-46b4-a3e4-8f349ccaa078
caps.latest.revision: 5
author: mstewart
ms.author: mstewart
manager: angrobe
---
# Site and site system prerequisites for System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*


 Windows-based computers require specific configurations to support their use as System Center Configuration Manager site system servers.  

 
 For some products, like Windows Server Update Services (WSUS) for the software update point, you need to refer to the product documentation to identify additional prerequisites and limitations for use of that product. Only configurations that directly apply for use with Configuration Manager are included here.   

> [!NOTE]  
>  In January 2016, support expired for the .NET Framework 4.0, 4.5, and 4.5.1. For more information, see [Microsoft .NET Framework Support Lifecycle Policy FAQ](https://support.microsoft.com/gp/framework_faq?WT.mc_id=azurebg_email_Trans_943_NET452_Update) at support.microsoft.com.  

## <a name="bkmk_generalprerewq"></a> General site server requirements and limitations
**The following apply to all site system servers:**

-   Each site system server must use a 64-bit operating system. The only exception to this is the distribution point site system role, which you can install on some 32-bit operating systems.  

-   Site systems are not supported on Server Core installations of any operating system. An exception to this is that Server Core installations are supported for the distribution point site system role, without PXE or multicast support.  

-   After a site system server is installed, it's not supported to change:  

    -   The domain name of the domain where the site system computer is located (also called a **domain rename**).  

    -   The domain membership of the computer.  

    -   The name of the computer.  

  If you must change any of these, you must first remove the site system role from the computer and then reinstall the role after the change is complete. If this affects the site server computer, you must uninstall the site and then reinstall the site after the change is complete.  

-   Site system roles are not supported on an instance of a Windows Server cluster. The only exception to this is the site database server.  

-   It's not supported to change the startup type or "Log on as" settings for any Configuration Manager service. If you do this, you might prevent key services from running correctly.  

##  <a name="bkmk_2012Prereq"></a> Prerequisites for Windows Server 2012 and later operating systems  
###  <a name="bkmk_2012sspreq"></a> Site server: central administration site and primary site  
  **Windows Server roles and features:**  

-   .NET Framework 3.5 SP1 (or later)  

-   .NET Framework 4.5.2  

-   Remote Differential Compression  

**Windows ADK:**  

-   Before you install or upgrade a central administration site or primary site, you must install the version of the Windows Assessment and Deployment Kit (ADK) that the version of Configuration Manager you're installing or upgrading to requires. See [Windows 10 ADK](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-adk) in the Support for Windows 10 as a client topic.  

-   For more information about this requirement, see [Infrastructure requirements for operating system deployment](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment).  

**Visual C++ Redistributable:**  

-   Configuration Manager installs the Microsoft Visual C++ 2013 Redistributable Package on each computer that installs a site server.  

-   Central administration sites and primary sites require both the x86 and x64 versions of the applicable Redistributable file.  

###  <a name="bkmk_2012secpreq"></a> Site server: secondary site  
**Windows Server roles and features:**  

-   .NET Framework 3.5 SP1 (or later)  

-   .NET Framework 4.5.2  

-   Remote Differential Compression  

**Visual C++ Redistributable:**  

-   Configuration Manager installs the Microsoft Visual C++ 2013 Redistributable Package on each computer that installs a site server.  

-   Secondary sites require only the x64 version.  

**Default site system roles:**  

-   By default, a secondary site installs a **management point** and a **distribution point**.  

-   Ensure that the secondary site server meets the prerequisites for these site system roles.  

###  <a name="bkmk_2012dbpreq"></a> Database server  
**Remote Registry service:**  

-   During installation of the Configuration Manager site, you must enable the Remote Registry service on the computer that will host the site database.  

**SQL Server:**  

-   Before you install a central administration site or primary site, you must install a supported version of SQL Server to host the site database.  

-   Before you install a secondary site, you can install a supported version of SQL Server.  

-   If you choose to have Configuration Manager install SQL Server Express as part of the secondary site installation, ensure that the computer meets the requirements to run SQL Server Express.  

###  <a name="bkmk_2012smsprovpreq"></a> SMS Provider server  
**Windows ADK:**  

-   The computer where you install an instance of the SMS Provider must have the required version of the Windows ADK that the version of Configuration Manager you're installing or upgrading to requires. See [Windows 10 ADK](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-adk) in the Support for Windows 10 as a client topic.

-   For more information about this requirement, see [Infrastructure requirements for operating system deployment](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment).  

###  <a name="bkmk_2012acwspreq"></a> Application Catalog website point  
**Windows Server roles and features:**  

-   .NET Framework 3.5 SP1 (or later)  

-   .NET Framework 4.5.2:  

    -   ASP.NET 4.5  

**IIS configuration:**  

-   Common HTTP Features:  

    -   Default Document  

    -   Static Content  

-   Application Development:  

    -   ASP.NET 3.5 (and automatically selected options)  

    -   ASP.NET 4.5 (and automatically selected options)  

    -   .NET Extensibility 3.5  

    -   .NET Extensibility 4.5  

-   Security:  

    -   Windows Authentication  

-   IIS 6 Management Compatibility:  

    -   IIS 6 Metabase Compatibility  

###  <a name="bkmk_2012ACwsitepreq"></a> Application Catalog web service point  
**Windows Server roles and features:**  

-   .NET Framework 3.5 SP1 (or later)  

-   .NET Framework 4.5.2:  

    -   ASP.NET 4.5:  

        -   HTTP Activation (and automatically selected options)  

**IIS configuration:**  

-   Common HTTP Features:  

    -   Default Document  

-   IIS 6 Management Compatibility:  

    -   IIS 6 Metabase Compatibility  

-   Application Development:  

    -   ASP.NET 3.5 (and automatically selected options)  

    -   .NET Extensibility 3.5  

    -   ASP.NET 4.5 (and automatically selected options)  

    -   .NET Extensibility 4.5  

**Computer memory:**  

-   The computer that hosts this site system role must have a minimum of 5% of the computer's available memory free to enable the site system role to process requests.  

-   When this site system role is co-located with another site system role that has this same requirement, this memory requirement for the computer doesn't increase, but remains at a minimum of 5%.  

###  <a name="bkmk_2012AIpreq"></a> Asset Intelligence synchronization point  
**Windows Server roles and features:**  

-   .NET Framework 4.5.2  

###  <a name="bkmk_2012crppreq"></a> Certificate registration point  
**Windows Server roles and features:**  

-   .NET Framework 4.5.2:  

    -   HTTP Activation  

**IIS configuration:**  

-   Application Development:  

    -   ASP.NET 3.5 (and automatically selected options)  

    -   ASP.NET 4.5 (and automatically selected options)  

-   IIS 6 Management Compatibility:  

    -   IIS 6 Metabase Compatibility  

    -   IIS 6 WMI Compatibility  

###  <a name="bkmk_2012dppreq"></a> Distribution point  
**Windows Server roles and features:**  

-   Remote Differential Compression  

**IIS configuration:**  

-   Application Development:  

    -   ISAPI Extensions  

-   Security:  

    -   Windows Authentication  

-   IIS 6 Management Compatibility:  

    -   IIS 6 Metabase Compatibility  

    -   IIS 6 WMI Compatibility  

**PowerShell:**  

-   On Windows Server 2012 or later, PowerShell 3.0 or 4.0 is required before you install the distribution point.  

**Visual C++ Redistributable:**  

-   Configuration Manager installs the Microsoft Visual C++ 2013 Redistributable Package on each computer that hosts a distribution point.  

-   The version that is installed depends on the computer's platform (x86 or x64).  

**Microsoft Azure:**  

-   You can use a cloud service in Microsoft Azure to host a distribution point.  

**To support PXE or multicast:**  

-   Install and configure the Windows Deployment Services (WDS) Windows Server role.  

    > [!NOTE]  
    >  WDS installs and configures automatically when you configure a distribution point to support PXE or multicast on a server that runs Windows Server 2012 or later.  

> [!NOTE]  
> The distribution point site system role doesn't require Background Intelligent Transfer Service (BITS). When BITS is configured on the distribution point computer, BITS on the distribution point computer isn't used to facilitate the download of content by clients that use BITS.  

###  <a name="bkmk_2012EPPpreq"></a> Endpoint Protection point  
**Windows Server roles and features:**  

-   .NET Framework 3.5 SP1 (or later)  

###  <a name="bkmk_2012Enrollpreq"></a> Enrollment point  
**Windows Server roles and features:**  

-   .NET Framework 3.5 (or later)  

-   .NET Framework 4.5.2:  

     When this site system role installs, Configuration Manager automatically installs the .NET Framework 4.5.2. This installation can place the server into a reboot pending state. When a reboot is pending for the .NET Framework, .NET applications might fail until after the server reboots and the installation finishes.  

    -   HTTP Activation (and automatically selected options)  

    -   ASP.NET 4.5  


**IIS configuration:**  

-   Common HTTP Features:  

    -   Default Document  

-   Application Development:  

    -   ASP.NET 3.5 (and automatically selected options)  

    -   .NET Extensibility 3.5  

    -   ASP.NET 4.5 (and automatically selected options)  

    -   .NET Extensibility 4.5  

-   IIS 6 Management Compatibility:  

    -   IIS 6 Metabase Compatibility  

**Computer memory:**  

-   The computer that hosts this site system role must have a minimum of 5% of the computer's available memory free to enable the site system role to process requests.  

-   When this site system role is co-located with another site system role that has this same requirement, this memory requirement for the computer doesn't increase, but remains at a minimum of 5%.  

###  <a name="bkmk_2012EnrollProxpreq"></a> Enrollment proxy point  
**Windows Server roles and features:**  

-   .NET Framework 3.5 (or later)  

-   .NET Framework 4.5.2  

     When this site system role installs, Configuration Manager automatically installs the .NET Framework 4.5.2. This installation can place the server into a reboot pending state. When a reboot is pending for the .NET Framework, .NET applications might fail until after the server reboots and the installation completes.  

**IIS configuration:**  

-   Common HTTP Features:  

    -   Default Document  

    -   Static Content  

-   Application Development:  

    -   ASP.NET 3.5 (and automatically selected options)  

    -   ASP.NET 4.5 (and automatically selected options)  

    -   .NET Extensibility 3.5  

    -   .NET Extensibility 4.5  

-   Security:  

    -   Windows Authentication  

-   IIS 6 Management Compatibility:  

    -   IIS 6 Metabase Compatibility  

**Computer memory:**  

-   The computer that hosts this site system role must have a minimum of 5% of the computer's available memory free to enable the site system role to process requests.  

-   When this site system role is co-located with another site system role that has this same requirement, this memory requirement for the computer doesn't increase, but remains at a minimum of 5%.  

###  <a name="bkmk_2012FSPpreq"></a> Fallback status point  
The default IIS configuration is required with the following additions:  

-   IIS 6 Management Compatibility:  

    -   IIS 6 Metabase Compatibility  

###  <a name="bkmk_2012MPpreq"></a> Management point  
**Windows Server roles and features:**  

-   .NET Framework 4.5.2  

-   BITS Server Extensions (and automatically selected options) or Background Intelligent Transfer Services (BITS) (and automatically selected options)  

**IIS configuration:**  

-   Application Development:  

    -   ISAPI Extensions  

-   Security:  

    -   Windows Authentication  

-   IIS 6 Management Compatibility:  

    -   IIS 6 Metabase Compatibility  

    -   IIS 6 WMI Compatibility  

###  <a name="bkmk_2012RSpoint"></a> Reporting services point  
**Windows Server roles and features:**  

-   .NET Framework 4.5.2  

**SQL Server Reporting Services:**  

-   You must install and configure at least one instance of SQL Server to support SQL Server Reporting Services before installing the reporting services point.  

-   The instance that you use for SQL Server Reporting Services can be the same instance you use for the site database.  

-   Additionally, the instance that you use can be shared with other System Center products as long as the other System Center products don't have restrictions for sharing the instance of SQL Server.  

###  <a name="bkmk_SCPpreq"></a> Service connection point  
**Windows Server roles and features:**  

-   .NET Framework 4.5.2  

     When this site system role installs, Configuration Manager automatically installs the .NET Framework 4.5.2. This installation can place the server into a reboot pending state. When a reboot is pending for the .NET Framework, .NET applications might fail until after the server reboots and the installation finishes.  

**Visual C++ Redistributable:**  

-   Configuration Manager installs the Microsoft Visual C++ 2013 Redistributable Package on each computer that hosts a distribution point.  

-   The site system role requires the x64 version.  

###  <a name="bkmk_2012SUPpreq"></a> Software update point  
**Windows Server roles and features:**  

-   .NET Framework 3.5 SP1 (or later)  

-   .NET Framework 4.5.2  

The default IIS configuration is required.

**Windows Server Update Services:**  

-   You must install the Windows server role Windows Server Update Services on a computer before installing a software update point.  

-   For more information, see [Plan for software updates in System Center Configuration Manager](../../../sum/plan-design/plan-for-software-updates.md).  

### State migration point  
The default IIS configuration is required.  

##  <a name="bkmk_2008"></a> Prerequisites for Windows Server 2008 R2 and Windows Server 2008  
Windows Server 2008 and Windows Server 2008 R2 are now in extended support and are no longer in mainstream support, as detailed by the [Microsoft Support Lifecycle](https://support.microsoft.com/lifecycle). For more information about future support for these operating systems as site system servers with Configuration Manager, see [Removed and deprecated features for System Center Configuration Manager](../../../core/plan-design/changes/removed-and-deprecated-features.md).  

**The following applies to all .NET Framework requirements:**  

-   Install the full version of the .NET Framework before you install the site system roles. For example, see the [Microsoft .NET Framework 4 (Stand-Alone Installer)](http://go.microsoft.com/fwlink/p/?LinkId=193048). The .NET Framework 4 Client Profile is insufficient for this requirement.  

**The following applies to all Windows Communication Foundation (WCF) activation requirements:**  

-   You can configure WCF activation as part of the .NET Framework Windows feature on the site system server. For example, on Windows Server 2008 R2, run the **Add Features Wizard** to install additional features on the server. On the **Select Features** page, expand **NET Framework 3.5.1 Features**, expand **WCF Activation**, and then check the boxes for both **HTTP Activation** and **Non-HTTP Activation** to enable these options.  

###  <a name="bkmk_2008sspreq"></a> Site server: central administration site and primary site  
**.NET Framework:**  

-   .NET Framework 3.5 SP1 (or later)  

-   .NET Framework 4.5.2  

**Windows feature:**  

-   Remote Differential Compression  

**Windows ADK:**  

-   Before you install or upgrade a central administration site or primary site, you must install the version of Windows ADK that the version of Configuration Manager you're installing or upgrading to requires.  See [Windows 10 ADK](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-adk) in the Support for Windows 10 as a client topic.  

-   For more information about this requirement, see [Infrastructure requirements for operating system deployment](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment).  

**Visual C++ Redistributable:**  

-   Configuration Manager installs the Microsoft Visual C++ 2013 Redistributable Package on each computer that installs a site server.  

-   Central administration sites and primary sites require both the x86 and x64 versions of the applicable Redistributable file.  

###  <a name="bkmk_2008secpreq"></a> Site server: secondary site  
**.NET Framework:**  

-   .NET Framework 3.5 SP1 (or later)  

-   .NET Framework 4.5.2  

**Visual C++ Redistributable:**  

-   Configuration Manager installs the Microsoft Visual C++ 2013 Redistributable Package on each computer that installs a site server.  

-   Secondary sites require only the x64 version.  

**Default site system roles:**  

-   By default, a secondary site installs a **management point** and a **distribution point**.  

-   Ensure that the secondary site server meets the prerequisites for these site system roles.  

###  <a name="bkmk_2008dbpreq"></a> Database server  
**Remote Registry service:**  

-   During installation of the Configuration Manager site, you must enable the Remote Registry service on the computer that will host the site database.  

**SQL Server:**  

-   Before you install a central administration site or primary site, you must install a supported version of SQL Server to host the site database.  

-   Before you install a secondary site, you can install a supported version of SQL Server.  

-   If you choose to have Configuration Manager install SQL Server Express as part of the secondary site installation, ensure that the computer meets the requirements to run SQL Server Express.  

###  <a name="bkmk_2008smsprovpreq"></a> SMS Provider server  
**Windows ADK:**  

-   The computer where you install an instance of the SMS Provider must have the required version of the Windows ADK that the version of Configuration Manager you're installing or upgrading to requires. See [Windows 10 ADK](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-adk) in the Support for Windows 10 as a client topic.  

-   For more information about this requirement, see [Infrastructure requirements for operating system deployment](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment).  

###  <a name="bkmk_2008acwspreq"></a> Application Catalog website point  
**.NET Framework:**  

-   .NET Framework 4.5.2  

**IIS configuration:**

The default IIS configuration is required with the following additions:  

-   Common HTTP Features:  

    -   Static Content  

    -   Default Document  

-   Application Development:  

    -   ASP.NET (and automatically selected options)  

         In some scenarios, such as when IIS is installed or reconfigured after the .NET Framework version 4.5.2 is installed, you must explicitly enable ASP.NET version 4.5. For example, on a 64-bit computer that runs the .NET Framework version 4.0.30319, run the following command: **%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet_regiis.exe -i -enable**  

-   Security:  

    -   Windows Authentication  

-   IIS 6 Management Compatibility:  

    -   IIS 6 Metabase Compatibility  

###  <a name="bkmk_2008ACwsitepreq"></a> Application Catalog web service point  
**.NET Framework:**  

-   .NET Framework 3.5 SP1 (or later)  

-   .NET Framework 4.5.2  

**Windows Communication Foundation (WCF) activation:**  

-   HTTP Activation  

-   Non-HTTP Activation  

**IIS configuration:**

The default IIS configuration is required with the following additions:  

-   Application Development:  

    -   ASP.NET (and automatically selected options)  

         In some scenarios, such as when IIS is installed or reconfigured after the .NET Framework version 4.5.2 is installed, you must explicitly enable ASP.NET version 4.5. For example, on a 64-bit computer that runs the .NET Framework version 4.0.30319, run the following command: **%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet_regiis.exe -i -enable**  

-   IIS 6 Management Compatibility:  

    -   IIS 6 Metabase Compatibility  

**Computer memory:**  

-   The computer that hosts this site system role must have a minimum of 5% of the computer's available memory free to enable the site system role to process requests.  

-   When this site system role is co-located with another site system role that has this same requirement, this memory requirement for the computer doesn't increase, but remains at a minimum of 5%.  

###  <a name="bkmk_2008AIpreq"></a> Asset Intelligence synchronization point  
**.NET Framework:**  

-   .NET Framework 4.5.2  

###  <a name="bkmk_2008crppreq"></a> Certificate registration point  
**.NET Framework:**  

-   .NET Framework 4.5.2  

-   HTTP Activation  

**IIS configuration:**

The default IIS configuration is required with the following additions:  

-   IIS 6 Management Compatibility:  

    -   IIS 6 Metabase Compatibility  

    -   IIS 6 WMI Compatibility  

###  <a name="bkmk_2008dppreq"></a> Distribution point  
**IIS configuration:**

You can use the default IIS configuration or a custom configuration. To use a custom IIS configuration, you must enable the following options for IIS:  

-   Application Development:  

    -   ISAPI Extensions  

-   Security:  

    -   Windows Authentication  

-   IIS 6 Management Compatibility:  

    -   IIS 6 Metabase Compatibility  

    -   IIS 6 WMI Compatibility  

When you use a custom IIS configuration, you can remove options that aren't required, such as the following:  

-   Common HTTP Features:  

    -   HTTP Redirection  

-   IIS Management Scripts and Tools  

**Windows feature:**  

-   Remote Differential Compression  

**Visual C++ Redistributable:**  

-   Configuration Manager installs the Microsoft Visual C++ 2013 Redistributable Package on each computer that hosts a distribution point.  

-   The version that is installed depends on the computer's platform (x86 or x64).  

**Microsoft Azure:**  

-   You can use a cloud service in Azure to host a distribution point.  

**To support PXE or multicast:**  

-   Install and configure the Windows Deployment Services (WDS) Windows Server role.  

    > [!NOTE]  
    >  WDS installs and configures automatically when you configure a distribution point to support PXE or multicast on a server that runs Windows Server 2012 or later.  

> [!NOTE]  
> The distribution point site system role doesn't require Background Intelligent Transfer Service (BITS). When BITS is configured on the distribution point computer, BITS on the distribution point computer isn't used to facilitate the download of content by clients that use BITS.  


###  <a name="bkmk_2008EPPpreq"></a> Endpoint Protection point  
**.NET Framework:**  

-   .NET Framework 3.5 SP1 (or later)  

###  <a name="bkmk_2008Enrollpreq"></a> Enrollment point  
**.NET Framework:**  

-   .NET Framework 4.5.2  

     When this site system role installs, if the server doesn't already have a supported version of the .NET Framework installed, Configuration Manager automatically installs the .NET Framework 4.5.2. This installation can place the server into a reboot pending state. When a reboot is pending for the .NET Framework, .NET applications might fail until after the server reboots and the installation finishes.  

**Windows Communication Foundation (WCF) activation:**  

-   HTTP Activation  

-   Non-HTTP Activation  

**IIS configuration:**

The default IIS configuration is required with the following additions:  

-   Application Development:  

    -   ASP.NET (and automatically selected options)  

         In some scenarios, such as when IIS is installed or reconfigured after the .NET Framework version 4.5.2 is installed, you must explicitly enable ASP.NET version 4.5. For example, on a 64-bit computer that runs the .NET Framework version 4.0.30319, run the following command: **%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet_regiis.exe -i -enable**  

**Computer memory:**  

-   The computer that hosts this site system role must have a minimum of 5% of the computer's available memory free to enable the site system role to process requests.  

-   When this site system role is co-located with another site system role that has this same requirement, this memory requirement for the computer doesn't increase, but remains at a minimum of 5%.  

###  <a name="bkmk_2008EnrollProxpreq"></a> Enrollment proxy point  
**.NET Framework:**  

-   .NET Framework 4.5.2  

     When this site system role installs, if the server doesn't already have a supported version of the .NET Framework installed, Configuration Manager automatically installs the .NET Framework 4.5.2. This installation can place the server into a reboot pending state. When a reboot is pending for the .NET Framework, .NET applications might fail until after the server reboots and the installation finishes.  

**Windows Communication Foundation (WCF) activation:**  

-   HTTP Activation  

-   Non-HTTP Activation  

**IIS configuration:**

The default IIS configuration is required with the following additions:  

-   Application Development:  

    -   ASP.NET (and automatically selected options)  

         In some scenarios, such as when IIS is installed or reconfigured after the .NET Framework version 4.5.2 is installed, you must explicitly enable ASP.NET version 4.5. For example, on a 64-bit computer that runs the .NET Framework version 4.0.30319, run the following command: **%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet_regiis.exe -i -enable**  

**Computer memory:**  

-   The computer that hosts this site system role must have a minimum of 5% of the computer's available memory free to enable the site system role to process requests.  

-   When this site system role is co-located with another site system role that has this same requirement, this memory requirement for the computer doesn't increase, but remains at a minimum of 5%.  

###  <a name="bkmk_2008FSPpreq"></a> Fallback status point  
**IIS configuration:**

The default IIS configuration is required with the following additions:  

-   IIS 6 Management Compatibility:  

    -   IIS 6 Metabase Compatibility  

###  <a name="bkmk_2008MPpreq"></a> Management point  
**.NET Framework:**  

-   .NET Framework 4.5.2  

**IIS configuration:**

You can use the default IIS configuration or a custom configuration. Each management point that you enable to support mobile devices requires the additional IIS configuration for ASP.NET (and its automatically selected options).

In some scenarios, such as when IIS is installed or reconfigured after the .NET Framework version 4.5.2 is installed, you must explicitly enable ASP.NET version 4.5. For example, on a 64-bit computer that runs the .NET Framework version 4.0.30319, run the following command: **%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet_regiis.exe -i -enable**  


To use a custom IIS configuration, you must enable the following options for IIS:  

-   Application Development:  

    -   ISAPI Extensions  

-   Security:  

    -   Windows Authentication  

-   IIS 6 Management Compatibility:  

    -   IIS 6 Metabase Compatibility  

    -   IIS 6 WMI Compatibility  


When you use a custom IIS configuration, you can remove options that aren't required, such as the following:  

-   Common HTTP Features:  

    -   HTTP Redirection  

-   IIS Management Scripts and Tools  

**Windows feature:**  

-   BITS Server Extensions (and automatically selected options), or Background Intelligent Transfer Services (BITS) (and automatically selected options)  

###  <a name="bkmk_2008RSpoint"></a> Reporting services point  
**.NET Framework:**  

-   .NET Framework 4.5.2  

**SQL Server Reporting Services:**  

-   You must install and configure at least one instance of SQL Server to support SQL Server Reporting Services before installing the reporting services point.  

-   The instance that you use for SQL Server Reporting Services can be the same instance you use for the site database.  

-   Additionally, the instance that you use can be shared with other System Center products as long as the other System Center products don't have restrictions for sharing the instance of SQL Server.  

###  <a name="bkmk_2008SCPpreq"></a> Service connection point  
**.NET Framework:**  

-   .NET Framework 4.5.2  

     When this site system role installs, if the server doesn't already have a supported version of the .NET Framework installed, Configuration Manager automatically installs the .NET Framework 4.5.2. This installation can place the server into a reboot pending state. When a reboot is pending for the .NET Framework, .NET applications might fail until after the server reboots and the installation finishes.  

**Visual C++ Redistributable:**  

-   Configuration Manager installs the Microsoft Visual C++ 2013 Redistributable Package on each computer that hosts a distribution point.  

-   The site system role requires the x64 version.  

###  <a name="bkmk_2008SUPpreq"></a> Software update point  
**.NET Framework:**  

-   .NET Framework 3.5 SP1 (or later)  

-   .NET Framework 4.5.2  

**IIS configuration:**

The default IIS configuration is required.  

**Windows Server Update Services:**  

-   You must install the Windows Server role Windows Server Update Services on a computer before installing a software update point.  

-   For more information, see [Plan for software updates in System Center Configuration Manager](../../../sum/plan-design/plan-for-software-updates.md).

###  <a name="bkmk_2008SMPpreq"></a> State migration point  
**IIS configuration:**

The default IIS configuration is required.  
