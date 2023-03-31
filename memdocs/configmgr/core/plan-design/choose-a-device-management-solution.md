---
title: Choose a device management solution
titleSuffix: Configuration Manager
description: Learn about the solutions that Microsoft offers for managing PCs, servers, and devices.
ms.date: 03/30/2023
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Choose a device management solution

Microsoft offers different solutions for managing PCs, servers, and devices. These solutions are available on-premises, cloud-based, or a combination of both. Choose the solution that's right for the business requirements of your organization. Base your decision on the device platforms you need to manage and the management functionality you need.

## Overview

There are several Microsoft solutions that might work best for you in different scenarios. You don't need to choose just one.

- For a small organization, a tool like the Windows administration center may be a great fit.
- Approximately 75% of IT organizations use Configuration Manager to manage their devices.
- Microsoft Azure provides various solutions from the cloud or on-premises with Azure Arc and Azure Stack that primarily target server management.
- Microsoft Intune provides cloud management of clients.
- You can combine Configuration Manager and Intune with co-management.
- You can use [Security Management for Microsoft Defender for Endpoint (MDE)](../../../intune/protect/mde-security-integration.md) to manage security settings for devices utilizing Microsoft Defender for Endpoint.

Use the following table to help compare these management technologies:

|  | Cloud-only | Cloud-attached | On-premises | Disconnected |
|---------|---------|---------|---------|---------|
| **Hyper-V host** | Not applicable | - Azure Stack<br/> - Windows Admin Center<br/> - Security Management for MDE <br/>- Virtual Machine Manager | - Azure Stack<br/> - Windows Admin Center<br/> - Virtual Machine Manager | - Azure Stack<br/> - Windows Admin Center<br/> - Virtual Machine Manager |
| **Windows Server** | - Azure Arc <br/> - Configuration Manager<br/> - Security Management for MDE | - Azure Arc<br/> - Configuration Manager <br/> - Security Management for MDE | - Azure Arc<br/> - Configuration Manager | Configuration Manager |
| **Linux Server** | Azure Arc | Azure Arc | Azure Arc |  |
| **Windows 10/11** | - Intune<br/> - Configuration Manager<br/> - Security Management for MDE | - Intune<br/> - Configuration Manager<br/> - Security Management for MDE | - Intune<br/> - Configuration Manager<br/> - Security Management for MDE | Configuration Manager |
| **Windows 7 or 8.1** | Configuration Manager | Configuration Manager | Configuration Manager | Configuration Manager |
| **Azure Virtual Desktop** | Configuration Manager | Not applicable | Not applicable | Not applicable |

For more information, see the following articles:

- [What is Azure Stack?](/azure-stack/operator/azure-stack-overview)
- [What is Windows Admin Center?](/windows-server/manage/windows-admin-center/understand/what-is)
- [What is Virtual Machine Manager?](/system-center/vmm/overview)
- [Azure Arc products](/azure/)
- [What is Azure Virtual Desktop?](/azure/virtual-desktop/overview)
- [Security Management for Microsoft Defender for Endpoint (MDE)](../../../intune/protect/mde-security-integration.md)

For more information on the Configuration Manager and Intune solutions, continue to the next section.

## Client management

This section compares the following four client management solutions:

- [Configuration Manager client](#bkmk_sccm)
- [Co-management with Microsoft Intune](#bkmk_comanage)
- [Microsoft Exchange](#bkmk_exchange)

You can use these solutions by themselves or in combination with each other. For example, use the client-based management approach to manage the computers and servers in your organization, and also use co-management to manage internet-based laptops. By combining approaches this way, you can cover all of your device management needs.  

There are also two tables that compare the management solutions by the following factors:

- [Compare by supported platforms](#bkmk_comp1)
- [Compare by management functionality](#bkmk_comp2)

### <a name="bkmk_sccm"></a> Configuration Manager client  

This option requires installation of the Configuration Manager client on devices. It provides the most features for managing PCs, servers, and other devices in your environment.

For more information, see [Client installation methods](../clients/deploy/plan/client-installation-methods.md).  

### Security Management for Microsoft Defender for Endpoint

This options requires utilizing Microsoft Defender for Endpoint on your devices and is intended to provide security management capability in circumstances where Microsoft Intune or Microsoft Configuration Manager are not present. This uses the Microsoft Defender for Endpoint client to communicate directly with Intune and apply security management policy.

For more information, see [Security Management for Microsoft Defender for Endpoint (MDE)](../../../intune/protect/mde-security-integration.md).

### <a name="bkmk_comanage"></a> Co-management with Microsoft Intune

Co-management is one of the primary ways to attach your existing Configuration Manager deployment to the Microsoft 365 cloud. It enables you to concurrently manage Windows devices by using both Configuration Manager and Microsoft Intune. Co-management lets you cloud-attach your existing investment in Configuration Manager by adding new functionality.

For more information, see [What is co-management?](../../comanage/overview.md).  

### <a name="bkmk_exchange"></a> Microsoft Exchange  

This option uses the Exchange Server connector to connect multiple Exchange servers to Configuration Manager. It centralizes management of devices that can connect to Exchange ActiveSync. You can configure Exchange mobile device management features from the Configuration Manager console. Example features include remote device wipe and the settings control for multiple Exchange servers.

For more information, see [Manage mobile devices with Configuration Manager and Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

### <a name="bkmk_comp1"></a> Compare solutions by supported platforms  

|Platform|Configuration Manager client|On-premises MDM|Configuration Manager with Exchange| Intune |
|--------|----------------------------|---------------|-----------------------------------|--------|
|Android| | |Yes| Yes |
|iOS| | |Yes| Yes |
|macOS X|Yes| |Yes| Yes |
|Windows 10/11|Yes|Yes|Yes| Yes |
|Windows 10 Mobile| |Yes|Yes| Yes |
|Windows (previous versions)|Yes| |Yes|  |
|Windows Server|Yes| |Yes|  |
|Windows Embedded|Yes| | |  |

For a complete list of supported platforms, see the following articles:

- [Supported operating systems for clients and devices for Configuration Manager](configs/supported-operating-systems-for-clients-and-devices.md)
- [Intune supported configurations](/intune/supported-devices-browsers)

Microsoft recommends using Intune to manage Android, iOS, and Windows 10/11 mobile devices. For more information, see [What is Microsoft Intune?](/intune/what-is-intune).

### <a name="bkmk_comp2"></a> Compare solutions by management functionality  

|Management functionality|Configuration Manager client|On-premises MDM|Configuration Manager with Exchange|  
|--------|----------------------------|---------------|-----------------------------------|  
|Certificate-based mutual authentication|Yes|Yes| |
|Client installation|Yes| | |
|Support over the internet|Yes| | |
|Discovery|Yes| |Yes|
|Hardware inventory|Yes|Yes|Yes|
|Software inventory|Yes| |Yes|
|Settings|Yes|Yes|Yes|
|Software deployment|Yes|Yes| |
|Software update management|Yes| | |
|OS deployment|Yes| | |
|Block from Configuration Manager|Yes|Yes| |
|Quarantine and block from Exchange Server (and Configuration Manager)| | |Yes|
|Remote wipe| |Yes|Yes|
