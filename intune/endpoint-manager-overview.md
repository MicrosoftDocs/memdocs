---
# required metadata

title: Endpoint management services and solutions at Microsoft
description: Microsoft Intune is a family of on-premises products and cloud services. It includes Intune, Configuration Manager, co-management, Endpoint Analytics, Windows Autopilot, and the admin center to manage cloud devices and on on-premises.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 08/20/2024
ms.topic: overview
ms.service: microsoft-intune
ms.subservice:
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

:::image type="content" source="./media/endpoint-management-microsoft.png" alt-text="Endpoint management for Microsoft includes Microsoft Intune, Windows Autopilot, and Endpoint analytics. It integrates with Microsoft Entra ID, on-premises Configuration Manager, mobile threat defense partners, Security Copilot, and Microsoft 365 apps." lightbox="./media/endpoint-management-microsoft.png":::

## Microsoft Intune

Microsoft Intune is a family of products and services. The Intune family includes:

- Microsoft Intune service
- Configuration Manager and co-management
- Endpoint Analytics
- Windows Autopilot
- Intune admin center

These products and services offer a **cloud-based unified endpoint management** solution. It simplifies management across multiple operating systems, cloud, on-premises, mobile, desktop, and virtualized endpoints. It also:

- Uses the Intune service for **cloud-native mobile device management (MDM) and mobile application management (MAM)**. End users and devices only need internet access; no need for on-premises infrastructure.
- **Supports data protection on company-owned and bring your own devices** through nonintrusive mobile application management.
- Empowers organizations to **provide data protection and endpoint compliance** that support a Zero Trust security model.
- Brings together **device visibility, endpoint security, and data-driven insights** to increase IT efficiency. In hybrid work environments, admin tasks and end user experiences are improved.

Intune integrates with other services, including Microsoft Entra, on-premises Configuration Manager, mobile threat defense (MTD) apps & services, Win32 & custom LOB apps, and more.

If you're moving to the cloud or are adopting more cloud-based services, then use Intune.

For more information, go to:

- [What is Microsoft Intune?](./intune-service/fundamentals/what-is-intune.md)
- [Get started with Microsoft Intune](./intune-service/fundamentals/get-started-with-intune.md)

## Configuration Manager and co-management

Configuration Manager is an on-premises management solution that uses Active Directory and Group Policy Objects (GPOs). It can **manage desktops, Windows servers, and laptops** that are on your network or are internet-based. You can use Configuration Manager to manage data centers, apps, software updates, and operating systems.

To benefit from everything that's happening in Microsoft Intune, connect your Configuration Manager to the cloud with co-management. Co-management combines your existing on-premises Configuration Manager investment with some of the cloud-based features in Intune, including using the web-based Microsoft Intune admin center.

Co-management is a great way to get started with cloud-based device management, and to start moving some workloads to the cloud.

For more information, go to:

- [What is Configuration Manager?](./configmgr/core/understand/introduction.md)
- [What is co-management?](./configmgr/comanage/overview.md)
- [Tenant attach: Prerequisites](./configmgr/tenant-attach/prerequisites.md)

## Intune Suite

The Intune Suite is a collection of add-on features that are available in Intune. The suite includes features that **expand device management capabilities**, including:

- Remote help for secure help desk connections
- Microsoft Tunnel VPN for mobile application management of devices that aren't enrolled in Intune
- Endpoint Privilege Management (EPM) so standard nonadmin users can complete tasks that require elevated privileges
- Support for specialty devices, like AR/VR headsets, large smart-screen devices, and select conference room meeting devices

The suite and its individual features are available as add-ons to your existing licenses and are also licensed individually.

There's also a free trial to help you determine if these features can help your organization.

For more information, go to:

- [Intune Suite add-on capabilities](./intune-service/fundamentals/intune-add-ons.md)

## Intune admin center

The [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) is a **one-stop web site**. Use the admin center to add users & groups, create & manage policies, and monitor your policies using report data. If you use Configuration Manager tenant-attach or co-management, you can see your on-premises devices and run some actions on these devices.

The admin center also plugs-in other key device management services, including:

- [**Microsoft Entra Privileged Identity Management** to monitor access to important resources](/azure/active-directory/privileged-identity-management/pim-configure)
- [**Microsoft Tunnel** VPN gateway solution that runs on Linux](./intune-service/protect/microsoft-tunnel-overview.md)
- [**Mobile threat defense** partners](./intune-service/protect/mobile-threat-defense.md)
- [**Remote Help** for remote assistance](/mem/intune-service/fundamentals/remote-help)
- [**TeamViewer** for remote administration](./intune-service/remote-actions/teamviewer-support.md)
- [**Windows 365** for your Windows virtual machines](/windows-365/overview)
- [**Windows Autopatch** to automate updates](/windows/deployment/windows-autopatch/overview/windows-autopatch-overview)

## Microsoft Entra ID

Microsoft Entra ID, previously known as Azure Active Directory (Azure AD), is a cloud-native service that's used by Intune to **manage the identities of users, devices, and groups**. The Intune policies you create are assigned to these users, devices, and groups. When devices are enrolled in Intune, your users sign in to their devices with their Microsoft Entra accounts (`user@contoso.com`).

**Microsoft Entra** has [different license plans that include more features](https://www.microsoft.com/security/business/microsoft-entra-pricing) to help protect devices, apps, and data, including dynamic groups, automatic enrollment in Intune, and Conditional Access.

For more information, go to:

- [Add users](./intune-service/fundamentals/users-add.md)
- [Set up auto enrollment](./intune-service/enrollment/windows-enroll.md)
- [Learn about Conditional Access and Intune](./intune-service/protect/conditional-access.md)

## Windows Autopilot

Windows Autopilot is a cloud-native service that **sets up and preconfigures devices**, getting them ready for use. It can also reset and repurpose existing devices. Windows Autopilot is designed to simplify the lifecycle of Windows devices from initial deployment through end of life, which benefits IT and end users.

Use Windows Autopilot to preconfigure devices, automatically join devices to Microsoft Entra, automatically enroll the devices in Intune, customize the out of box experience (OOBE), and more. You can also integrate Windows Autopilot with Configuration Manager and co-management for more device configurations.

If you constantly provision new devices or repurpose existing devices, then use Windows Autopilot.

For more information, go to:

- [Get an overview of Windows Autopilot](/autopilot/overview)
- [Enroll Windows devices in Intune](/autopilot/enrollment-autopilot)

## Microsoft Copilot in Intune

[Microsoft Copilot in Intune](./intune-service/copilot/copilot-intune-overview.md) is a **cloud-native service that uses AI to get information quickly**. Intune has capabilities that are powered by [Microsoft Copilot for Security](/copilot/security/microsoft-security-copilot). These capabilities access your Intune data, and can:

- Help you manage your policies and settings.
- Understand your security posture.
- Troubleshoot device issues.
- Create Kusto Query Language (KQL) queries.

For more information, go to [Microsoft Copilot in Intune](./intune-service/copilot/copilot-intune-overview.md).

## Windows 365

Windows 365 Cloud PCs are **virtual machines that are hosted in the cloud-native Windows 365 service**. They're accessible from anywhere and from any device that has internet access. Cloud PCs include a Windows desktop experience and are associated with a user.

You enroll and manage these devices with Intune, just like any other device. On these Cloud PCs, you can use Intune to deploy apps, configure settings, install updates, and more.

If you have remote workers, want to provide a secure way for your users to access corporate resources, and/or looking for a way to provide a Windows desktop experience, then Windows 365 is a great solution.

For more information, go to:

- [Windows 365 Cloud PC overview - Enterprise](/windows-365/enterprise/overview)
- [Windows 365 Cloud PC overview - Business](/windows-365/business/)

## Windows Autopatch

Windows Autopatch is a cloud-native service that **automates patching** of Windows devices and Microsoft 365 apps, including Microsoft Teams & Microsoft Edge. To use Windows Autopatch, devices must be enrolled in Intune or managed using co-management (Intune + Configuration Manager).

When you're planning your update strategy, you can use the update policies in Intune, or use Windows Autopatch. Intune gives more granular control, including when updates are installed. Windows Autopatch automatically applies updates as soon as they're available and lets admins focus on other tasks.

For more information, go to:

- [Windows Autopatch overview](/windows/deployment/windows-autopatch/overview/windows-autopatch-overview)
- [Windows Autopatch prerequisites](/windows/deployment/windows-autopatch/prepare/windows-autopatch-prerequisites)
- [Windows Autopatch FAQ](/windows/deployment/windows-autopatch/overview/windows-autopatch-faq)

## Endpoint analytics

Endpoint analytics is a cloud-native service that provides **metrics and recommendations on the health and performance** of your Windows client devices. If you use Configuration Manager, you can benefit from Endpoint Analytics insights by connecting to the cloud.

You can get data on:

- Startup performance
- Device restart frequencies
- A list of apps that affect end-user productivity
- Recommendations on how to improve performance

This information and more is shown in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

You can use Endpoint Analytics on devices that are managed with Intune or Configuration Manager connected to the cloud.

For more information, go to:

- [What is Endpoint analytics?](./analytics/overview.md)
- [Endpoint analytics scores, baselines, and insights](./analytics/scores.md)
- [Tutorial: Walkthrough the Microsoft Intune admin center](./intune-service/fundamentals/tutorial-walkthrough-endpoint-manager.md)
- [Quickstart - Enroll Configuration Manager devices](./analytics/enroll-configmgr.md)

## Learn more

- [Learn more about cloud-native endpoints](./solutions/cloud-native-endpoints/cloud-native-endpoints-overview.md)
- [Compare Microsoft 365 features and licensing](https://www.microsoft.com/licensing/product-licensing/microsoft-365-enterprise)
- [Learn more about Microsoft Intune licensing](./intune-service/fundamentals/licenses.md)
- [Get started with Microsoft Intune](./intune-service/fundamentals/get-started-with-intune.md)
