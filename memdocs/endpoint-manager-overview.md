---
# required metadata

title: Microsoft Endpoint Manager overview
description: Endpoint Manager includes Intune, Configuration Manager, co-management, Desktop Analytics, Windows Autopilot, and the admin center to manage all devices, including on-premises.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 10/03/2022
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

Microsoft Endpoint Manager referred to the products and services that focused on endpoint management. This family of products and services is now called Microsoft Intune.

The Microsoft Intune family helps deliver the modern workplace and modern management to keep your data secure, in the cloud and on-premises. Intune includes the services and tools you use to manage and monitor mobile devices, desktop computers, virtual machines, embedded devices, and servers.

Intune combines services you may know and already be using, including Microsoft Intune, Configuration Manager, Endpoint Analytics, co-management, and Windows Autopilot. These services are part of the Microsoft 365 stack to help secure access, protect data, respond to risk, and manage risk.

This articles provides an overview of the Microsoft Intune family of products and services.

## Microsoft Intune

Intune is a cloud-based service mobile device management (MDM) and mobile application management (MAM) provider for your devices, apps, and data. It lets you control features and settings on Android, Android Enterprise, AOSP, iOS/iPadOS, macOS, and Windows client devices. With Intune, users can be productive from anywhere and on any device. It also gives admins the tools to manage users, manage devices, and manage apps.

It integrates with other services, including Azure Active Directory (AD), on-premises Configuration Manager, mobile threat defense (MTD) apps & services, Win32 & custom LOB apps, and more.

If you are moving to the cloud or adopting more cloud-based services, Intune is a great place to start.

For more information, go to:

- [What is Microsoft Intune?](/intune/fundamentals/what-is-intune)
- [Get started with Microsoft Intune](/intune/fundamentals/get-started-with-intune)

## Configuration Manager and co-management

Configuration Manager is an on-premises management solution that can manage desktops, servers, and laptops that are on your network or are internet-based. You can use Configuration Manager to manage data centers, deploy apps, software updates, and operating systems.

If you're ready to move some tasks to the cloud, then consider co-management. Co-management combines your existing on-premises Configuration Manager investment with some of the cloud-based features in Intune, including using the web-based Endpoint Manager admin center.

Co-management is a great way to get started with Intune and to start moving some workloads to the cloud.

For more information, go to:

- [What is Configuration Manager?](/configmgr/core/understand/introduction)
- [What is co-management?](/configmgr/comanage/overview)
- [Tenant attach: Prerequisites](/configmgr/tenant-attach/prerequisites)

## Endpoint Analytics

Endpoint Analytics is a cloud-based service that provides metrics and recommendations on the health and performance of your Windows client devices. This information is shown in the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

For example, you can get data on startup performance, how frequently devices restart, get a list of apps that affect end-user productivity, and get recommendations on how to improve performance.

You can use Endpoint Analytics on devices that are managed by Intune or Configuration Manager.

For more information, go to:

- [What is Endpoint analytics?](/mem/analytics/overview)
- [Endpoint analytics scores, baselines, and insights](/mem/analytics/scores)

## Windows Autopilot

Windows Autopilot is a cloud-based services that sets up and pre-configures new devices, getting them ready for use. It's designed to simplify the lifecycle of Windows devices, for both IT and end users, from initial deployment through end of life.

Use Windows Autopilot to pre-configure devices, and automatically enroll devices in Intune. You can also integrate Windows Autopilot with Configuration Manager and co-management for more complex device configurations.

For more information, go to:

- [Windows Autopilot overview](/windows/deployment/windows-autopilot/windows-autopilot)
- [Enroll Windows devices in Intune](./autopilot/enrollment-autopilot.md)

## Azure Active Directory (AD)

Azure AD is used for identity of devices, users, groups, and multi-factor authentication (MFA). **Azure AD Premium**, which may be an additional cost, has [additional features](https://azure.microsoft.com/pricing/details/active-directory/) to help protect devices, apps, and data, including dynamic groups, auto-enrollment, and conditional access.

For more information, go to [add users](./intune/fundamentals/users-add.md), [set up auto-enrollment](./intune/enrollment/windows-enroll.md), and [about conditional access](./intune/protect/conditional-access.md).

## Endpoint Manager admin center

The [admin center](https://go.microsoft.com/fwlink/?linkid=2109431) is a one-stop web site to create policies and manage your devices. It plugs-in other key device management services, including groups, security, conditional access, and reporting. This admin center also shows devices managed by Configuration Manager and Intune.

## Choose what's right for you

There are a few ways to determine what's right for your organization. Your next steps depend on what your organization does. Consider what you're trying to achieve.

For example:

- If you constantly provision new devices, then use Windows Autopilot.
- If you add rules and control settings for your users, apps, and devices, then use Intune.
- If you currently use Configuration Manager to deploy apps, and want to use conditional access based on security requirements, then use co-management.
- If you currently use Configuration Manager and are responsible for keeping Windows 10/11 devices up-to-date, then use Endpoint Analytics.
- If you're getting started with MDM and MAM, or use ADMX templates to control Office, Microsoft Edge, and Windows settings, then use Intune.

You can also think of Intune in three parts: cloud, on-premises, and cloud + on-premises:

- **Cloud**: All data is stored in Azure. And, no more data centers. This approach gives you the mobility benefits of the cloud, and the security benefits of Azure.

- **On-premises**: If you have an on-premises infrastructure that includes Configuration Manager, or aren't ready to use the cloud, then keep your existing systems.

- **Cloud + on-premises**: Many environments are mixed, and use a cloud-attach approach. Meaning, they use a combination of cloud and on-premises. For new devices, use the benefits of Intune to access and protect data. If you use Configuration Manager, connect to the cloud for additional functionality and analytics. If you want to move some workloads to the cloud, then co-management is a good option.

## What you need to get started

Intune is a solution platform that unifies several technologies. The services are licensed according to their individual licenses terms. For more information, go to the [product licensing terms](https://www.microsoft.com/licensing/product-licensing/products).

If you currently use Configuration Manager, you also get Microsoft Intune to co-manage your Windows devices. For other platforms, such as iOS/iPadOS and Android, then you'll need a separate Intune license.

In most scenarios, Microsoft 365 may be the best option, as it gives you Intune and Office. For more information, go to [Microsoft 365](https://www.microsoft.com/licensing/product-licensing/microsoft-365-enterprise).

## Next steps

[Use the power of cloud intelligence to simplify and accelerate IT and the move to a modern workplace](https://www.microsoft.com/microsoft-365/blog/2019/11/04/use-the-power-of-cloud-intelligence-to-simplify-and-accelerate-it-and-the-move-to-a-modern-workplace/)

[Tutorial: Walkthrough Intune in Microsoft Endpoint Manager](/intune/fundamentals/tutorial-walkthrough-endpoint-manager)

[What is Microsoft 365?](/training/modules/what-is-m365/index)
