---
# required metadata

title: Microsoft Intune family of products and services
description: Microsoft Intune is a family of on-premises products and cloud services. This family includes Intune, Configuration Manager, co-management, Endpoint Analytics, Windows Autopilot, and the admin center to manage all devices, including on-premises.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 10/04/2022
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
  - highpri
  - highseo
---

# Microsoft Intune is a family of products and services

Microsoft Intune is a family of products and services. It combines services you may know and may already be using, including Microsoft Intune, Configuration Manager, co-management, Endpoint Analytics, and Windows Autopilot. These services are part of the Microsoft 365 stack to help secure access, protect data, and respond to & manage risk.

Previously, this family of products and services was known as Microsoft Endpoint Manager.

The Microsoft Intune family helps deliver the modern workplace and modern management to keep your data secure, in the cloud and on-premises. Intune includes the services and tools you use to manage and monitor mobile devices, desktop computers, virtual machines, embedded devices, and servers.

This article provides an overview of the Microsoft Intune family of products and services.

## Microsoft Intune

Intune is a cloud-native mobile device management (MDM) and mobile application management (MAM) service provider for your devices, apps, and data. It lets you control features and settings on Android, AOSP, iOS/iPadOS, macOS, and Windows client devices. With Intune, users can be productive from anywhere and on any device. It also gives admins the tools to manage users, manage devices, and manage apps securely.

It integrates with other services, including Azure Active Directory (AD), on-premises Configuration Manager, mobile threat defense (MTD) apps & services, Win32 & custom LOB apps, and more.

If you're moving to the cloud or are adopting more cloud-based services, Intune is a great place to start.

For more information, go to:

- [What is Microsoft Intune?](./intune/fundamentals/what-is-intune.md)
- [Get started with Microsoft Intune](./intune/fundamentals/get-started-with-intune.md)

## Configuration Manager and co-management

Configuration Manager is an on-premises management solution that can manage desktops, Windows servers, and laptops that are on your network or are internet-based. You can use Configuration Manager to manage data centers, apps, software updates, and operating systems.

If you're ready to move some tasks to the cloud, then consider co-management. Co-management combines your existing on-premises Configuration Manager investment with some of the cloud-based features in Intune, including using the web-based Endpoint Manager admin center.

Co-management is a great way to get started with Intune and to start moving some workloads to the cloud.

For more information, go to:

- [What is Configuration Manager?](./configmgr/core/understand/introduction.md)
- [What is co-management?](./configmgr/comanage/overview.md)
- [Tenant attach: Prerequisites](./configmgr/tenant-attach/prerequisites.md)

## Endpoint Analytics

Endpoint Analytics is a cloud-native service that provides metrics and recommendations on the health and performance of your Windows client devices.

You can get data on:

- Startup performance
- How frequently devices restart
- A list of apps that affect end-user productivity
- Recommendations on how to improve performance

This information and more is shown in the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

You can use Endpoint Analytics on devices that are managed by Intune or Configuration Manager.

For more information, go to:

- [What is Endpoint analytics?](./analytics/overview.md)
- [Endpoint analytics scores, baselines, and insights](./analytics/scores.md)
- [Tutorial: Walkthrough Intune in Microsoft Endpoint Manager](./intune/fundamentals/tutorial-walkthrough-endpoint-manager.md)

## Windows Autopilot

Windows Autopilot is a cloud-native service that sets up and pre-configures new devices, getting them ready for use. It can also reset and repurpose existing devices. It's designed to simplify the lifecycle of Windows devices from initial deployment through end of life, benefitting IT and end users.

Use Windows Autopilot to pre-configure devices, automatically join devices to Azure AD, automatically enroll the devices in Intune, customize the out of box experience (OOBE), and more. You can also integrate Windows Autopilot with Configuration Manager and co-management for more device configurations.

If you constantly provision new devices or repurpose existing devices, then use Windows Autopilot.

For more information, go to:

- [Windows Autopilot overview](./autopilot/windows-autopilot.md)
- [Enroll Windows devices in Intune](./autopilot/enrollment-autopilot.md)

## Azure Active Directory (AD)

Azure AD is a cloud-native service that's used by Intune to manage the identities of users, devices, and groups. The Intune policies you create are assigned to these users, devices, and groups. When devices are enrolled in Intune, your users sign in to their devices with their Azure AD accounts (`user@contoso.com`).

**Azure AD Premium**, which may be an extra cost, has [more features](https://azure.microsoft.com/pricing/details/active-directory/) to help protect devices, apps, and data, including dynamic groups, automatic enrollment in Intune, and conditional access.

For more information, go to:

- [Add users](./intune/fundamentals/users-add.md)
- [Set up auto-enrollment](./intune/enrollment/windows-enroll.md)
- [Learn about conditional access and Intune](./intune/protect/conditional-access.md)

## Endpoint Manager admin center

The [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) is a one-stop web site. Use the admin center to add users & groups, create & manage policies, and monitor your policies using report data. If you use Configuration Manager tenant-attach or co-management, you can see your on-premises devices and run some actions on these devices.

The admin center also plugs-in other key device management services, including:

- [**Azure AD Privileged Identity Management** to monitor access to important resources](/azure/active-directory/privileged-identity-management/pim-configure)
- [**Microsoft Tunnel** VPN gateway solution that runs on Linux](./intune/protect/microsoft-tunnel-overview.md)
- [**Mobile threat defense** partners](./intune/protect/mobile-threat-defense.md)
- [**TeamViewer** for remote administration](./intune/remote-actions/teamviewer-support.md)
- [**Windows 365** for your Windows virtual machines needs](/windows-365/overview)
- [**Windows Autopatch** to automate updates](/windows/deployment/windows-autopatch/overview/windows-autopatch-overview)

For more information, go to:

- [Tutorial: Walkthrough Intune in Microsoft Endpoint Manager](./intune/fundamentals/tutorial-walkthrough-endpoint-manager.md)

## Next steps

- [Learn more about cloud-native endpoints](./solutions/cloud-native-endpoints/cloud-native-endpoints-overview.md)
- [Microsoft 365 Feature comparison and licensing](https://www.microsoft.com/licensing/product-licensing/microsoft-365-enterprise)
- [Microsoft Intune licensing](./intune/fundamentals/licenses.md)
- [Get started with Microsoft Intune](./intune/fundamentals/get-started-with-intune.md)
