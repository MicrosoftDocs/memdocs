---
title: "Choose a device management solution "
titleSuffix: "Configuration Manager"
description: "Learn about the solutions that System Center Configuration Manager offers for managing PCs, servers, and devices."
ms.date: 12/08/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 24633725-791a-4df7-8dce-2c24c1a19a03
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# Choose a device management solution for System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager (also known as ConfgMgr or SCCM) offers different solutions for managing PCs, servers, and devices. You can choose the solution that's right for you, based on the device platforms you need to manage and the management functionality you need.  


##  Overview of device management solutions  
 This article covers four device management solutions: the Configuration Manager client application, on-premises Configuration Manager infrastructure, Microsoft Intune, and Exchange. The article concludes with two tables that compare the management solutions, one based on [supported mobile device platforms](#compare-device-management-solutions-based-on-supported-mobile-device-platforms), and one based on [management functionality](#compare-mobile-device-management-solutions-based-on-management-functionality).


###  Manage devices with the Configuration Manager client  

This option, which requires installation of the Configuration Manager client application on the devices, provides the most features for managing PCs, servers, and other devices in your environment. For more information, see [Client installation methods in System Center Configuration Manager](/sccm/core/clients/deploy/plan/client-installation-methods).  

###  Manage devices with on-premises Configuration Manager infrastructure  

This option uses the device management capabilities built into the operating systems of some device platforms. While not as full-featured as the client-based management, on-premises mobile device management provides a lighter touch approach to management by using on-premises Configuration Manager resources to reach and manage devices. Note that this option is currently supported only for Windows 10 PCs and Windows 10 Mobile devices.  

For more information, see [Manage mobile devices with on-premises infrastructure in System Center Configuration Manager](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).  

###  Manage devices with Microsoft Intune (hybrid)  

This option uses Microsoft Intune to enroll and manage devices, instead of using Configuration Manager on-premises resources. Even though Intune manages the devices, you access your management tasks in the Configuration Manager console. This option supports all major mobile device operating systems, including Windows 10 Mobile, Windows Phone, iOS, Mac OS X, and Android. It also provides management for Windows 8.1 and Windows 10 computers in your organization.  

For more information, see [Hybrid mobile device management (MDM) with System Center Configuration Manager and Microsoft Intune](../../mdm/understand/hybrid-mobile-device-management.md).  

###  Manage devices with Microsoft Exchange  

This option uses the Exchange Server connector to connect multiple Exchange servers to Configuration Manager. This centralizes management of devices that can connect to Exchange ActiveSync. You can configure Exchange mobile device management features, such as remote device wipe and the settings control for multiple Exchange servers, from the Configuration Manager console.  

For more information, see [Manage mobile devices with System Center Configuration Manager and Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

You can use these device management solutions by themselves or in combination with each other. For example, you can use the client-based management approach to manage the computers and servers in your organization, and also use Intune to manage mobile devices. By combining approaches this way, you can cover all of your device management needs from the Configuration Manager console.  

## Compare device management solutions based on supported mobile device platforms  

|Platform|With the Configuration Manager client|Configuration Manager with Microsoft Intune (hybrid)|On\-premises mobile device management|Configuration Manager with Exchange|  
|--------------|-------------------------------------------|-------------------------------------------------------------------|-------------------------------|-----------------------------------------|  
|Android||Yes||Yes|  
|iOS||Yes||Yes|  
|Mac OS X|Yes|||Yes|  
|UNIX/Linux|Yes|||Yes|  
|Windows 10|Yes|Yes|Yes|Yes|  
|Windows 10 Mobile||Yes|Yes|Yes|  
|Windows (previous versions)|Yes|Yes||Yes|  
|Windows CE|Yes (with mobile device legacy client)|||Yes|  
|Windows Embedded|Yes||||  
|Windows Phone||Yes||Yes|  
|Windows Server|Yes|||Yes|  

 For a complete list of supported platforms, see [Supported operating systems for clients and devices for System Center Configuration Manager](configs/supported-operating-systems-for-clients-and-devices.md).

##  <a name="bkmk_comp2"></a> Compare mobile device management solutions based on management functionality  

|Management functionality|With the Configuration Manager client|Configuration Manager with Microsoft Intune (hybrid)|On\-premises mobile device management|Configuration Manager with Exchange|  
|------------------------------|-------------------------------------------|-------------------------------------------------------------------|-------------------------------|-----------------------------------------|  
|Public key infrastructure (PKI) security between the mobile device and Configuration Manager (uses mutual authentication and SSL to encrypt data transfers)|Yes|Yes|Yes||  
|Client installation|Yes||||  
|Support over the Internet|Yes||||  
|Discovery|Yes|||Yes|  
|Hardware inventory|Yes|Yes|Yes|Yes|  
|Software inventory|Yes|||Yes|  
|Settings|Yes|Yes|Yes|Yes|  
|Software deployment|Yes|Yes|Yes||  
|Monitor with fallback status point|Yes||||  
|Connections to management points|Yes||Yes||  
|Connections to distribution points|Yes||Yes||  
|Block from Configuration Manager|Yes|Yes|Yes||  
|Quarantine and block from Exchange Server (and Configuration Manager)||||Yes|  
|Remote wipe| |Yes|Yes|Yes|  
