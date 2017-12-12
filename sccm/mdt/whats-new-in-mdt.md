---

title: "What’s new in MDT 2013 Guide"
titleSuffix: "Microsoft Deployment Toolkit"
description: "Learn about the Microsoft Deployment Toolkit 2013."
ms.date:  09/09/2016
ms.prod: configuration-manager
ms.technology:
  - configmgr-osd
ms.topic: article
ms.assetid:  17466fa9-1a26-4dd8-a36f-c0c68fa1984c

author: aczechowski  
ms.author: aaroncz 
manager: angrobe

---



# What's new in Microsoft Deployment Toolkit (MDT) 2013 Guide
Microsoft Deployment Toolkit (MDT) 2013 is the next version of the Microsoft Solution Accelerator for operating system and application deployment. The purpose of this guide is to explain the changes in MDT 2013 from MDT 2012 Update 1.  

 This guide specifically discusses the MDT 2013 release and assumes familiarity with previous MDT version concepts, features, and capabilities.  

> [!NOTE]   
>  In this document, *Windows* applies to the Windows 8.1, Windows 8, Windows 7, Windows Server 2012 R2, Windows Server 2012, and Windows Server 2008 R2 operating systems unless otherwise noted. MDT does not support ARM processor–based versions of Windows. Similarly, *MDT* refers to MDT 2013 unless otherwise stated.  

## What’s New in This Release  
 MDT includes several improvements that adds new features and improves your user experience with MDT. In addition, this release of MDT includes many other small enhancements and bug fixes that are not listed below.  

### Support for Upgrading from Previous Versions of MDT  
 MDT supports upgrading from MDT 2012 Update 1.  

> [!NOTE]   
>  Create a backup of the existing MDT infrastructure before attempting an upgrade.  

### Support for Windows 8.1 and Windows Server 2012 R2  
 You can use MDT to deploy the Windows 8.1 and Windows Server 2012 R2 operating systems using the LTI, ZTI, and UDI deployment methods. Roles and features specific to Windows 8.1 and Windows Server 2012 R2 are available in the role list.  

### Support for the Windows ADK for Windows 8.1  
 MDT supports the use of the Windows ADK for Windows 8.1 to deploy operating systems. The Windows ADK for Windows 8.1 includes the Deployment Tools such as the Deployment Image Servicing and Management (DISM) tool, the Windows Pre-installation Environment (Windows PE) and the User State Migration Tool (USMT).  

### Support for System Center 2012 R2 Configuration Manager  
 ZTI and UDI deployment methods in MDT support integration with System Center 2012 R2 Configuration Manager, including new capabilities such as multiple Network Access Accounts.  

### Improved Deployment to x86-based Computers that Use the UEFI Standard  
 Unified Extensible Firmware Interface (UEFI) is a specification that defines a software interface between an operating system and platform firmware. UEFI is a more secure replacement for the older basic input/output system (BIOS) firmware interface present in some personal computers, which is vulnerable to malware that performs attacks during the boot or power on self-test processes.  

 By default, MDT creates the appropriate partitions to support computers running UEFI. MDT supports UEFI versions from 2.0 up to 2.3.1. UEFI 2.3.1 is a newer version of UEFI that will be used on Windows 8 logo–compliant computers.  

 For more information about UEFI support in MDT, see the section, "Deploy to Computers with UEFI", in the MDT document *Using the Microsoft Deployment Toolkit*.  

## What’s Been Removed from This Release?  
 This release of MDT does not include the following features that existed in previous versions of MDT:  

-   Deployment of Windows 8.1 Preview  

-   Deployment of Windows Server 2012 R2 Preview  

-   ZTI with  

    -   System Center Configuration Manager 2007  

    -   System Center 2012 Configuration Manager  

    -   System Center 2012 Configuration Manager SP1  

    -   System Center 2012 R2 Configuration Manager Preview  

-   Use of the Windows ADK for Windows 8  

-   Use of the Windows AIK for Windows 7  

-   Deployment of Windows XP or Windows Server 2003  

-   Deployment of Windows Vista or Windows Server 2008  

-   Out-of-box Group Policy objects (GPOs) from Security Compliance Manager (SCM). Tools and GPOs must be installed with SCM before they can be used in MDT.  

## Operating System Support in This Release  
The following table lists the operating system support that LTI and ZTI deployments provide in this release of MDT.  

|||||  
|-|-|-|-|  
|Operating system|LTI|ZTI|UDI|  
|Windows 8.1|●|●|●|  
|Windows Server 2012 R2|●|●||  
|Windows 8|●|●|●|  
|Windows Server 2012|●|●||  
|Windows 7|●|●|●|  
|Windows Server 2008 R2|●|●||  
|Windows PE version 5.0|●|●|●|  

 ● = supported  

## Windows ADK Support  
 The following table lists the Windows ADK and Windows AIK support that LTI, ZTI, and UDI deployments provide in MDT.  

|||||  
|-|-|-|-|  
|Windows ADK|LTI|ZTI|UDI|  
|Windows ADK for Windows 8.1|●|●|●|  

 ● = supported  

## Microsoft .NET Framework and Windows PowerShell Support  
The following table lists the versions of the Microsoft .NET Framework and Windows PowerShell that are supported by MDT by Windows operating system version.  


||||  
|-|-|-|  
|Windows version|.NET|PowerShell|  
|Windows 8.1|4.0|3.0|  
|Windows Server 2012 R2|4.0|3.0|  
|Windows 8|4.0|3.0|  
|Windows Server 2012|4.0|3.0|  
|Windows 7|3.5 with SP1|2.0|  
|Windows Server 2008 R2|3.5 with SP1|2.0|
