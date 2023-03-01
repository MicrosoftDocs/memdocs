---
# required metadata

title: Endpoint Management at Microsoft
description: Microsoft Intune is a family of on-premises products and cloud services. This family includes Intune, Configuration Manager, co-management, Endpoint Analytics, Windows Autopilot, and the admin center to manage all devices, including on-premises.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 02/28/2023
ms.topic: overview
ms.service: mem
ms.subservice: fundamentals
ms.localizationpriority: high
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:
ms.reviewer: dougeby
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: 
  - get-started
  - intro-overview
ms.collection:
  - M365-identity-device-management
  - tier1
---

# Endpoint management at Microsoft

This article provides an overview of endpoint management solutions at Microsoft.

## Microsoft Intune

Microsoft Intune is a family of products and services. The Intune family includes:

- Microsoft Intune service
- Configuration Manager and co-management
- Endpoint Analytics
- Windows Autopilot
- Intune admin center

These products and services offer a cloud-based unified endpoint management solution. It simplifies management across multiple operating systems, cloud, on-premises, mobile, desktop, and virtualized endpoints. It also:

- **Supports data protection on company-owned and bring your own devices** through non-intrusive mobile application management.
- Empowers organizations to **provide data protection and endpoint compliance** that support a Zero Trust security model.
- Brings together **device visibility, endpoint security, and data-driven insights** to increase IT efficiency. In hybrid work environments, admin tasks and end user experiences are improved.

Intune integrates with other services, including Azure Active Directory (AD), on-premises Configuration Manager, mobile threat defense (MTD) apps & services, Win32 & custom LOB apps, and more.

If you're moving to the cloud or are adopting more cloud-based services, Intune is a great place to start.

For more information, go to:

- [What is Microsoft Intune?](./intune/fundamentals/what-is-intune.md)
- [Get started with Microsoft Intune](./intune/fundamentals/get-started-with-intune.md)

## Configuration Manager and co-management

Configuration Manager is an on-premises management solution that can manage desktops, Windows servers, and laptops that are on your network or are internet-based. You can use Configuration Manager to manage data centers, apps, software updates, and operating systems.

To benefit from all that's happening in Microsoft Intune, connect to the cloud with co-management. Co-management combines your existing on-premises Configuration Manager investment with some of the cloud-based features in Intune, including using the web-based Microsoft Intune admin center.

Co-management is a great way to get started with Intune and to start moving some workloads to the cloud.

For more information, go to:

- [What is Configuration Manager?](./configmgr/core/understand/introduction.md)
- [What is co-management?](./configmgr/comanage/overview.md)
- [Tenant attach: Prerequisites](./configmgr/tenant-attach/prerequisites.md)

## Endpoint analytics

Endpoint analytics is a cloud-native service that provides metrics and recommendations on the health and performance of your Windows client devices. If you use Configuration Manager, you can benefit from Endpoint Analytics insights by connecting to the cloud.

You can get data on:

- Startup performance
- How frequently devices restart
- A list of apps that affect end-user productivity
- Recommendations on how to improve performance

This information and more is shown in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

You can use Endpoint Analytics on devices that are managed with Intune or Configuration Manager connected to the cloud.

For more information, go to:

- [What is Endpoint analytics?](./analytics/overview.md)
- [Endpoint analytics scores, baselines, and insights](./analytics/scores.md)
- [Tutorial: Walkthrough the Microsoft Intune admin center](./intune/fundamentals/tutorial-walkthrough-endpoint-manager.md)
- [Quickstart - Enroll Configuration Manager devices](./analytics/enroll-configmgr.md)

## Windows Autopilot

Windows Autopilot is a cloud-native service that sets up and pre-configures new devices, getting them ready for use. It can also reset and repurpose existing devices. It's designed to simplify the lifecycle of Windows devices from initial deployment through end of life, benefitting IT and end users.

Use Windows Autopilot to pre-configure devices, automatically join devices to Azure AD, automatically enroll the devices in Intune, customize the out of box experience (OOBE), and more. You can also integrate Windows Autopilot with Configuration Manager and co-management for more device configurations.

If you constantly provision new devices or repurpose existing devices, then use Windows Autopilot.

For more information, go to:

- [Windows Autopilot overview](./autopilot/windows-autopilot.md)
- [Enroll Windows devices in Intune](./autopilot/enrollment-autopilot.md)

## Azure Active Directory (AD)

Azure Active Directory (Azure AD) is a cloud-native service that's used by Intune to manage the identities of users, devices, and groups. The Intune policies you create are assigned to these users, devices, and groups. When devices are enrolled in Intune, your users sign in to their devices with their Azure AD accounts (`user@contoso.com`).

**Azure AD Premium**, which may be an extra cost, has [more features](https://azure.microsoft.com/pricing/details/active-directory/) to help protect devices, apps, and data, including dynamic groups, automatic enrollment in Intune, and conditional access.

For more information, go to:

- [Add users](./intune/fundamentals/users-add.md)
- [Set up auto-enrollment](./intune/enrollment/windows-enroll.md)
- [Learn about conditional access and Intune](./intune/protect/conditional-access.md)

## Intune admin center

The [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) is a one-stop web site. Use the admin center to add users & groups, create & manage policies, and monitor your policies using report data. If you use Configuration Manager tenant-attach or co-management, you can see your on-premises devices and run some actions on these devices.

The admin center also plugs-in other key device management services, including:

- [**Azure AD Privileged Identity Management** to monitor access to important resources](/azure/active-directory/privileged-identity-management/pim-configure)
- [**Microsoft Tunnel** VPN gateway solution that runs on Linux](./intune/protect/microsoft-tunnel-overview.md)
- [**Mobile threat defense** partners](./intune/protect/mobile-threat-defense.md)
- [**Remote Help** for remote assistance](./intune/remote-actions/remote-help.md)
- [**TeamViewer** for remote administration](./intune/remote-actions/teamviewer-support.md)
- [**Windows 365** for your Windows virtual machines](/windows-365/overview)
- [**Windows Autopatch** to automate updates](/windows/deployment/windows-autopatch/overview/windows-autopatch-overview)

## Next steps

- [Learn more about cloud-native endpoints](./solutions/cloud-native-endpoints/cloud-native-endpoints-overview.md)
- [Microsoft 365 Feature comparison and licensing](https://www.microsoft.com/licensing/product-licensing/microsoft-365-enterprise)
- [Microsoft Intune licensing](./intune/fundamentals/licenses.md)
- [Get started with Microsoft Intune](./intune/fundamentals/get-started-with-intune.md)
