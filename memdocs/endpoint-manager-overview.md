---
# required metadata

title: Microsoft Endpoint Manager overview - Azure | Microsoft Docs
description: Endpoint Manager includes Intune, Configuration Manager, co-management, Desktop Analytics, Windows Autopilot, and the admin center to manage all devices, including on-premises.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 02/24/2020
ms.topic: conceptual
ms.service: 
ms.subservice: 
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: dougeby
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: get-started
ms.collection: M365-identity-device-management
---

# Microsoft Endpoint Manager overview

Microsoft Endpoint Manager helps deliver the modern workplace and modern management to keep your data secure, in the cloud and on-premises. Endpoint Manager includes the services and tools administrators use to manage and monitor mobile devices, desktop computers, virtual machines, embedded devices, and servers.

Endpoint Manager combines services device administrators may know and already be using, including Microsoft Intune, Configuration Manager with Desktop Analytics, co-management, and Windows Autopilot. These services are part of the Microsoft 365 stack to help secure access, protect data, and respond and manage risk.

## What you get

Endpoint Manager includes the following services:

- **Microsoft Intune**: Intune is a mobile device management (MDM) and mobile application management (MAM) provider for your apps and devices. It's 100% cloud-based, and lets you control features and settings on Android, Android Enterprise, iOS/iPadOS, macOS, and Windows devices. It integrates with other services, including Azure Active Directory (AD), mobile threat defenders, ADMX templates, Win32 and custom LOB apps, and more.

  As part of Endpoint Manager, use Intune to create and check for compliance, and deploy apps, features, and settings to your devices using the cloud.

  For more information, see [What is Microsoft Intune](https://docs.microsoft.com/intune/fundamentals/what-is-intune).

- **Configuration Manager**: Configuration Manager is an on-premises management solution that uses Active Directory, SQL Server, and Internet Information Services (IIS). It deploys apps and operating systems, and manages servers, desktops, and laptops. It also integrates with Intune, Windows Server Update Services (WSUS), group policy, and more.

  As part of Endpoint Manager, continue to use Configuration Manager as you always have. If you're ready to move some tasks to the cloud, consider [co-management](https://docs.microsoft.com/configmgr/comanage/).

  For more information, see [What is Configuration Manager?](https://docs.microsoft.com/configmgr/core/understand/introduction).

- **Co-management**: Co-management combines your existing on-premises Configuration Manager investment with the cloud using Intune and other Microsoft 365 cloud services.

  As part of Endpoint Manager, co-management uses cloud features, including conditional access. You keep some tasks on-premises, while running other tasks in the cloud with Intune.

  For more information, see [What is co-management?](https://docs.microsoft.com/configmgr/comanage/overview).

- **Desktop Analytics**: Desktop Analytics is a cloud-based service that integrates with Configuration Manager. It provides information on security updates, apps and devices in your organization, identifies compatibility issues, and inventories your devices.

  As part of Endpoint Manager, use Desktop Analytics to keeps on-premises apps and Windows 10 devices current.

  For more information, see [What is Desktop Analytics?](https://docs.microsoft.com/configmgr/desktop-analytics/overview).

- **Windows Autopilot**: Windows Autopilot sets up and pre-configures new devices, getting them ready for use. It's designed to simplify the lifecycle of Windows devices, for both IT and end users, from initial deployment through end of life.

  As part of Endpoint Manager, use Autopilot to preconfigure devices, and automatically enroll devices in Intune. You can also integrate Autopilot with Configuration Manager and co-management for more complex device configurations (in preview).

  For more information, see [Windows Autopilot overview](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-autopilot) and [Enroll Windows devices in Intune](https://docs.microsoft.com/intune/enrollment/enrollment-autopilot).

- **Azure AD Premium**: Azure AD is used by Endpoint Manager for devices, users, groups, dynamic groups, auto-enrollment, multi-factor authentication, and conditional access. These features are key to protecting devices, apps, and data.

  For more information, see [add users](../users-add.md), [set up auto-enrollment](../enrollment/windows-enroll.md), and [about conditional access](../protect/conditional-access.md).

  - **Endpoint Manager admin center**: The [admin center](https://devicemanagement.microsoft.com) is a one-stop web site to create policies and manage your devices. It plugs-in other key device management services, including groups, security, conditional access, and reporting. This admin center also shows devices managed by Configuration Manager and Intune (in preview).

## Choose what's right for you

There are a few ways to determine what's right for your organization. Your next steps depend on what your organization does. Consider what you're trying to achieve.

For example:

- If you constantly provision new devices, then start with Windows Autopilot.
- If you add rules and control settings for your users, apps, and devices, then start with Intune.
- If you currently use Configuration Manager to deploy apps, and want to use conditional access based on security requirements, then start with co-management.
- If you currently use Configuration Manager and are responsible for keeping Windows 10 devices up-to-date, then start with Desktop Analytics.
- If you're getting started with MDM and MAM, or use ADMX templates to control Office, Microsoft Edge, and Windows settings, then start with Intune.

You can also think of Endpoint Manager in three parts: cloud, on-premises, and cloud + on-premises:

- **Cloud**: All data is stored in Azure. And, no more data centers. This approach gives you the mobility benefits of the cloud, and the security benefits of Azure.

- **On-premises**: If you have an on-premises infrastructure that includes Configuration Manager, or aren't ready to use the cloud, then you can keep your existing systems.

- **Cloud + on-premises**: Many environments are mixed, and use a cloud-attach approach. Meaning they use a combination of cloud and on-premises. For new devices, use the benefits of Intune to access and protect data. If you use Configuration Manager, and want to move some workloads to the cloud, then co-management is a good option.

## What you need to get started

If you currently use Configuration Manager, you also get Microsoft Intune to co-manage your Windows devices. For other platforms, such as iOS/iPadOS and Android, then you'll need a separate Intune license.

In most scenarios, Microsoft 365 may be the best option, as it gives you Endpoint Manager, and Office 365.

For more information, see [Microsoft 365](https://www.microsoft.com/licensing/product-licensing/microsoft-365-enterprise).

## Next steps

[Use the power of cloud intelligence to simplify and accelerate IT and the move to a modern workplace](https://www.microsoft.com/microsoft-365/blog/2019/11/04/use-the-power-of-cloud-intelligence-to-simplify-and-accelerate-it-and-the-move-to-a-modern-workplace/)

[Microsoft Endpoint Manager](https://www.microsoft.com/microsoft-365/microsoft-endpoint-manager)

[Tutorial: Walkthrough Intune in Microsoft Endpoint Manager](https://docs.microsoft.com/intune/fundamentals/tutorial-walkthrough-endpoint-manager)

[What is Microsoft 365? learn module](https://docs.microsoft.com/learn/modules/what-is-m365/index)
