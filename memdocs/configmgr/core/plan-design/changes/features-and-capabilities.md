---
title: Features and capabilities
titleSuffix: Configuration Manager
description: Learn about the primary management capabilities of Configuration Manager.
ms.date: 07/15/2021
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: overview
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz
---

# Features and capabilities of Configuration Manager

*Applies to: Configuration Manager (current branch)*

This article summarizes the primary management features of Configuration Manager. Each feature has its own prerequisites, and how you use each might influence the design and implementation of your Configuration Manager hierarchy. For example, if you want to deploy software updates to devices in your hierarchy, you need a software update point site system role.

## Co-management

Co-management is one of the primary ways to attach your existing Configuration Manager deployment to the Microsoft 365 cloud. It enables you to concurrently manage Windows devices by using both Configuration Manager and Microsoft Intune. Co-management lets you cloud-attach your existing investment in Configuration Manager by adding new functionality like conditional access. For more information, see [What is co-management](../../../comanage/overview.md)?

## Cloud-attached management

Use features like the cloud management gateway and Microsoft Entra ID to manage internet-based clients.

For more information, see the following articles:

- [Cloud management gateway overview](../../clients/manage/cmg/overview.md)
- [Plan for Microsoft Entra ID](../security/plan-for-security.md#azure-active-directory)
- [Azure services](../../servers/deploy/configure/azure-services-wizard.md)

## Real-time management

Use CMPivot to immediately query online devices, then filter and group the data for deeper insights. Also use the Configuration Manager console to manage and deploy Windows PowerShell scripts to clients. For more information, see [CMPivot](../../servers/manage/cmpivot.md) and [Create and run PowerShell scripts](../../../apps/deploy-use/create-deploy-scripts.md).

## Application management

Helps you create, manage, deploy, and monitor applications to a range of different devices that you manage. Deploy, update, and manage Microsoft 365 Apps from the Configuration Manager console. Additionally, Configuration Manager integrates with the Microsoft Store for Business and Education to deliver cloud-based apps. For more information, see [Introduction to application management](../../../apps/understand/introduction-to-application-management.md).

## OS deployment

Deploy an in-place upgrade of Windows, or capture and deploy OS images. Image deployment can use PXE, multicast, or bootable media. It can also help redeploy existing devices using Windows Autopilot. For more information, see [Introduction to OS deployment](../../../osd/understand/introduction-to-operating-system-deployment.md).

## Software updates

Manage, deploy, and monitor software updates in the organization. Integrate with Windows Delivery Optimization and other peer caching technologies to help control network usage. For more information, see [Introduction to software updates](../../../sum/understand/software-updates-introduction.md).

## Company resource access

Lets you give users in your organization access to data and applications from remote locations. This feature includes Wi-Fi, VPN, email, and certificate profiles. For more information, see [Protect data and site infrastructure](../../../protect/understand/protect-data-and-site-infrastructure.md).

## Compliance settings

Helps you to assess, track, and remediate the configuration compliance of client devices in the organization. Additionally, you can use compliance settings to configure a range of features and security settings on devices you manage. For more information, see [Ensure device compliance](../../../compliance/understand/ensure-device-compliance.md).

## Endpoint Protection

Provides security, antimalware, and Windows Firewall management for computers in your organization. This area includes management and integration with the following Windows Defender suite features:

- Windows Defender Antivirus
- Microsoft Defender for Endpoint
- Windows Defender Exploit Guard
- Windows Defender Application Guard
- Windows Defender Application Control
- Windows Defender Firewall

For more information, see [Endpoint Protection](../../../protect/deploy-use/endpoint-protection.md).

## Inventory

Helps you identify and monitor assets.

### Hardware inventory

Collects detailed information about the hardware of devices in your organization. For more information, see [Introduction to hardware inventory](../../clients/manage/inventory/introduction-to-hardware-inventory.md).

### Software inventory

Collects and reports information about the files that are stored on client computers in your organization. For more information, see [Introduction to software inventory](../../clients/manage/inventory/introduction-to-software-inventory.md).

### Asset Intelligence

Provides tools to collect inventory data and monitor software license usage in your organization. For more information, see [Introduction to Asset Intelligence](../../clients/manage/asset-intelligence/introduction-to-asset-intelligence.md).

## On-premises mobile device management

Enrolls and manages devices by using the on-premises Configuration Manager infrastructure with the management functionality built into the device platforms. (Typical management uses a separately installed Configuration Manager client.) This feature currently supports managing Windows 10 Enterprise and Windows 10 Mobile devices. For more information, see [Manage mobile devices with on-premises infrastructure](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).

## Power management

Manage and monitor the power consumption of client computers in the organization. Configure power plans, and use Wake-on-LAN to do maintenance outside of business hours. For more information, see [Introduction to power management](../../clients/manage/power/introduction-to-power-management.md).

## Remote control

Provides tools to remotely administer client computers from the Configuration Manager console. For more information, see [Introduction to remote control](../../clients/manage/remote-control/introduction-to-remote-control.md).

## Reporting

Use the advanced reporting capabilities of SQL Server Reporting Services from the Configuration Manager console. This feature provides hundreds of default reports. For more information, see [Introduction to reporting](../../servers/manage/introduction-to-reporting.md).

## Software metering

Monitor and collect software usage data from Configuration Manager clients. You can use this data to determine whether software is used after it's installed. For more information, see [Monitor app usage with software metering](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).

## Next steps

For more information about how to plan and install Configuration Manager to support these management capabilities in your environment, see [Get ready for Configuration Manager](../get-ready.md).
