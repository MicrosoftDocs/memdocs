---
title: Choose a device management solution
titleSuffix: Configuration Manager
description: Learn about the solutions that Configuration Manager offers for managing PCs, servers, and devices.
ms.date: 01/31/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 24633725-791a-4df7-8dce-2c24c1a19a03
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
---

# Choose a device management solution for Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Configuration Manager offers different solutions for managing PCs, servers, and devices. Choose the solution that's right for your organization. Base your decision on the device platforms you need to manage and the management functionality you need.  


> [!Important]  
> As of August 14, 2018, hybrid mobile device management is a [deprecated feature](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures). For more information, see [What is hybrid MDM](/sccm/mdm/understand/hybrid-mobile-device-management).<!--Intune feature 2683117-->  
<!-- SCCMDocs issue 1197 -->



## Overview

This article covers the following four device management solutions: 
- [Configuration Manager client](#bkmk_sccm)
- [On-premises mobile device management (MDM) with Configuration Manager](#bkmk_opmdm)
- [Co-management with Microsoft Intune](#bkmk_intune)
- [Microsoft Exchange](#bkmk_opmdm)

You can use these device management solutions by themselves or in combination with each other. For example, you can use the client-based management approach to manage the computers and servers in your organization, and also use co-management to manage internet-based laptops. By combining approaches this way, you can cover all of your device management needs.  

The article also includes two tables that compare the management solutions by the following factors: 
- [Compare by supported platforms](#bkmk_comp1)
- [Compare by management functionality](#bkmk_comp2)


### <a name="bkmk_sccm"></a> Configuration Manager client  

This option requires installation of the Configuration Manager client on devices. It provides the most features for managing PCs, servers, and other devices in your environment. 

For more information, see [Client installation methods](/sccm/core/clients/deploy/plan/client-installation-methods).  


### <a name="bkmk_opmdm"></a> On-premises MDM  

This option uses the device management capabilities built into Windows 10. While not as full-featured as client-based management, on-premises mobile device management provides a lighter touch approach to management. It uses on-premises Configuration Manager resources to manage devices.  

For more information, see [Manage mobile devices with on-premises infrastructure](/sccm/mdm/understand/manage-mobile-devices-with-on-premises-infrastructure).  


### <a name="bkmk_comanage"></a> Co-management with Microsoft Intune

Co-management is one of the primary ways to attach your existing Configuration Manager deployment to the Microsoft 365 cloud. It enables you to concurrently manage Windows 10 devices by using both Configuration Manager and Microsoft Intune. Co-management lets you cloud-attach your existing investment in Configuration Manager by adding new functionality. 

For more information, see [What is co-management?](/sccm/comanage/overview).  


### <a name="bkmk_exchange"></a> Microsoft Exchange  

This option uses the Exchange Server connector to connect multiple Exchange servers to Configuration Manager. This centralizes management of devices that can connect to Exchange ActiveSync. You can configure Exchange mobile device management features from the Configuration Manager console. Example features include remote device wipe and the settings control for multiple Exchange servers.

For more information, see [Manage mobile devices with Configuration Manager and Exchange](/sccm/mdm/deploy-use/manage-mobile-devices-with-exchange-activesync).  



## <a name="bkmk_comp1"></a> Compare solutions by supported platforms  

|Platform|Configuration Manager client|On-premises MDM|Configuration Manager with Exchange|  
|--------|----------------------------|---------------|-----------------------------------|  
|Android| | |Yes|  
|iOS| | |Yes|  
|Mac OS X|Yes| |Yes|  
|UNIX/Linux|Yes| |Yes|  
|Windows 10|Yes|Yes|Yes|  
|Windows 10 Mobile| |Yes|Yes|  
|Windows (previous versions)|Yes| |Yes|  
|Windows Server|Yes| |Yes|  
|Windows CE|Yes (with mobile device legacy client)| |Yes|  
|Windows Embedded|Yes| | |  
|Windows Mobile| | |Yes|  

For a complete list of supported platforms, see [Supported operating systems for clients and devices for System Center Configuration Manager](configs/supported-operating-systems-for-clients-and-devices.md).

Microsoft recommends using Intune to manage Android, iOS, and Windows 10 mobile devices. For more information, see [What is Microsoft Intune?](https://docs.microsoft.com/intune/what-is-intune)



##  <a name="bkmk_comp2"></a> Compare solutions by management functionality  

|Management functionality|Configuration Manager client|On-premises MDM|Configuration Manager with Exchange|  
|--------|----------------------------|---------------|-----------------------------------|  
|Public key infrastructure (PKI) security between the mobile device and Configuration Manager (uses mutual authentication and SSL to encrypt data transfers)|Yes|Yes| |  
|Client installation|Yes| | |  
|Support over the internet|Yes| | |  
|Discovery|Yes| |Yes|  
|Hardware inventory|Yes|Yes|Yes|  
|Software inventory|Yes| |Yes|  
|Settings|Yes|Yes|Yes|  
|Software deployment|Yes|Yes| |  
|Monitor with fallback status point|Yes| | |  
|Connections to management points|Yes|Yes| |  
|Connections to distribution points|Yes|Yes| |  
|Block from Configuration Manager|Yes|Yes| |  
|Quarantine and block from Exchange Server (and Configuration Manager)| | |Yes|  
|Remote wipe| |Yes|Yes|  


