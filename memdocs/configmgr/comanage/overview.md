---
title: Co-management for Windows devices
titleSuffix: Configuration Manager
description: Learn how to concurrently manage Windows 10 or later devices by using both Configuration Manager and Microsoft Intune.
author: gowdhamankarthikeyan
ms.author: gokarthi
manager: apoorvseth
ms.date: 03/21/2022
ms.topic: overview
ms.subservice: co-management
ms.service: configuration-manager
#Customer intent: As an IT Pro, I want to enable co-management so that Configuration Manager is cloud-attached to Microsoft Intune.
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# What is co-management?

<!-- 1350871 -->
Co-management is one of the primary ways to attach your existing Configuration Manager deployment to the Microsoft 365 cloud. It helps you unlock more cloud-powered capabilities like conditional access.

Co-management enables you to concurrently manage Windows 10 or later devices by using both Configuration Manager and Microsoft Intune. It lets you cloud-attach your existing investment in Configuration Manager by adding new functionality. By using co-management, you have the flexibility to use the technology solution that works best for your organization.

When a Windows device has the Configuration Manager client and is enrolled to Intune, you get the benefits of both services. You control which workloads, if any, you switch the authority from Configuration Manager to Intune. Configuration Manager continues to manage all other workloads, including those workloads that you don't switch to Intune, and all other features of Configuration Manager that co-management doesn't support.

You're also able to pilot a workload with a separate collection of devices. Piloting allows you to test the Intune functionality with a subset of devices before switching a larger group.

:::image type="content" source="media/co-management-overview.svg" alt-text="Overview diagram of co-management." lightbox="media/co-management-overview.svg":::

> [!NOTE]
> When you concurrently manage devices with both Configuration Manager and Microsoft Intune, this configuration is called *co-management*. When you manage devices with Configuration Manager and enroll to a third-party MDM service, this configuration is called *coexistence*. Having two management authorities for a single device can be challenging if not properly orchestrated between the two. With co-management, Configuration Manager and Intune balance the [workloads](#workloads) to make sure there are no conflicts. This interaction doesn't exist with third-party services, so there are limitations with the management capabilities of coexistence. For more information, see [Third-party MDM coexistence with Configuration Manager](coexistence.md).

## Paths to co-management

There are two main paths to reach to co-management:

- **Existing Configuration Manager clients**: You have Windows 10 or later devices that are already Configuration Manager clients. You set up hybrid Microsoft Entra ID, and enroll them into Intune.

- **New internet-based devices**: You have new Windows 10 or later devices that join Microsoft Entra ID and automatically enroll to Intune. You install the Configuration Manager client to reach a co-management state.

For more information on the paths, see [Paths to co-management](quickstart-paths.md).

## Benefits

When you enroll existing Configuration Manager clients in co-management, you gain the following immediate value:

- Conditional access with device compliance

- Intune-based remote actions, for example: restart, remote control, or factory reset

- Centralized visibility of device health

- Link users, devices, and apps with Microsoft Entra ID

- Modern provisioning with Windows Autopilot

- Remote actions

For more information on this immediate value from co-management, see the quickstarts series to [Cloud connect with co-management](quickstarts.md).

Co-management also enables you to orchestrate with Intune for several workloads. For more information, see the [Workloads](#workloads) section.

> [!NOTE]
> Co-management by itself isn't a solution to manage remotely connected Windows systems. The Configuration Manager client still needs to communicate with its assigned site. To manage remotely connected Windows systems with Configuration Manager, enable a [cloud management gateway (CMG)](../core/clients/manage/cmg/overview.md). A CMG isn't required for co-management, and co-management isn't required with a CMG, but they can be used together.

## Prerequisites

Co-management has these prerequisites in the following areas:

- [Licensing](#licensing)
- [Configuration Manager](#configuration-manager)
- [Microsoft Entra ID](#azure-ad) (Microsoft Entra ID)
- [Microsoft Intune](#intune)
- [Windows](#windows)
- [Permissions and roles](#permissions-and-roles)

### Licensing

- Microsoft Entra ID P1 or P2

    > [!NOTE]
    > An Enterprise Mobility + Security (EMS) subscription includes both Microsoft Entra ID P1 or P2 and Microsoft Intune.

- At least one Intune license for you as the administrator to access the Microsoft Intune admin center.

    > [!TIP]
    > Make sure you assign an Intune license to the account that you use to sign in to your tenant. Otherwise, sign in fails with the error message *An unanticipated error occurred*.<!-- MEMDocs#691 -->
    >
    > You may not need to purchase and assign individual Intune or EMS licenses to your users. For more information, see the [Product and licensing FAQ](../core/understand/product-and-licensing-faq.yml#what-changes-with-licensing-for-co-management-in-the-microsoft-intune-family-of-products-).

### Configuration Manager

Co-management requires a supported version of Configuration Manager current branch.

You can connect multiple Configuration Manager instances to a single Intune tenant.<!--1357944-->

Enabling co-management itself doesn't require that you onboard your site with Microsoft Entra ID. For the [second path scenario](#paths-to-co-management), internet-based Configuration Manager clients require the [cloud management gateway](../core/clients/manage/cmg/overview.md) (CMG). The CMG requires the site is [onboarded to Microsoft Entra ID for cloud management](../core/servers/deploy/configure/azure-services-wizard.md).

<a name='azure-ad'></a>

### Microsoft Entra ID

- Windows devices must be connected to Microsoft Entra ID. They can be either of the following types:

  - [Microsoft Entra hybrid joined](/azure/active-directory/devices/concept-azure-ad-join-hybrid), where the device is joined to your on-premises Active Directory and registered with your Microsoft Entra ID.

    > [!NOTE]
    > Devices that are only registered with Microsoft Entra ID aren't supported with co-management. This configuration is sometimes referred to as _workplace joined_. They need to be either joined to Microsoft Entra ID or Microsoft Entra hybrid joined. For more information, see [Handling devices with Microsoft Entra registered state](/azure/active-directory/devices/hybrid-azuread-join-plan#handling-devices-with-azure-ad-registered-state).<!-- 9342566 -->

  - [Microsoft Entra joined](/azure/active-directory/devices/azureadjoin-plan) only. This type is sometimes referred to as _cloud domain-joined_.)<!--SCCMDocs issue 605-->

> [!TIP]
> As we talk with our customers that are using Microsoft Intune to deploy, manage, and secure their client devices, we often get questions regarding co-managing devices and Microsoft Entra hybrid joined devices. Many customers confuse these two topics. Co-management is a management option, while Microsoft Entra ID is an identity option. For more information, see [Understanding hybrid Microsoft Entra ID and co-management scenarios](https://techcommunity.microsoft.com/t5/microsoft-endpoint-manager-blog/understanding-hybrid-azure-ad-join-and-co-management/ba-p/2221201). This blog post aims to clarify Microsoft Entra hybrid join and co-management, how they work together, but aren't the same thing.

### Intune

- [Set up Intune](../../intune/fundamentals/deployment-plan-setup.md)

- [Enable Windows automatic enrollment](../../intune/enrollment/windows-enroll.md#enable-windows-automatic-enrollment)

### Windows

Update your devices to an [Intune supported version of Windows 11 or Windows 10](../../intune/fundamentals/supported-devices-browsers.md). For more information, see [Adopting Windows as a service](../core/understand/configuration-manager-and-windows-as-service.md#windows-as-a-service).

### Permissions and roles

<!--SCCMDocs issue #667-->
| Action | Role needed |
|----|----|
| Set up a cloud management gateway in Configuration Manager | Azure **Subscription Manager** |
| Create Microsoft Entra apps from Configuration Manager | Microsoft Entra ID **Global Administrator** |
| Import Azure apps in Configuration Manager | Configuration Manager **Full Administrator**<br>No other Azure roles needed |
| Enable co-management in Configuration Manager | A Microsoft Entra user<br>Configuration Manager **Full Administrator** with **All** scope rights.<!--SCCMDoc issue 626--> |

For more information about Azure roles, see [Understand the different roles](/azure/role-based-access-control/rbac-and-directory-admin-roles).

For more information about Configuration Manager roles, see [Fundamentals of role-based administration](../core/understand/fundamentals-of-role-based-administration.md).

## Workloads

You don't have to switch the workloads, or you can do them individually when you're ready. Configuration Manager continues to manage all other workloads, including those workloads that you don't switch to Intune, and all other features of Configuration Manager that co-management doesn't support.

Co-management supports the following workloads:

- Compliance policies

- Windows Update policies

- Resource access policies

- Endpoint Protection

- Device configuration

- Office Click-to-Run apps

- Client apps

For more information, see [Workloads](workloads.md).

## Monitor co-management

The co-management dashboard helps you review machines that are co-managed in your environment. The graphs can help identify devices that might need attention.

:::image type="content" source="media/co-management-dashboard.png" alt-text="Screenshot of the co-management dashboard.":::

For more information, see [How to monitor co-management](how-to-monitor.md).

## Next steps

- [Learn more about immediate value and getting started with co-management](quickstarts.md)

- [Tutorial: Enable co-management for existing Configuration Manager clients](tutorial-co-manage-clients.md)
