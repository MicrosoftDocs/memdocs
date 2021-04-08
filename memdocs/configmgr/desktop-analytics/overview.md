---
title: Desktop Analytics
titleSuffix: Configuration Manager
description: An overview of the Desktop Analytics service integrated with Configuration Manager.
ms.date: 04/02/2021
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: overview
ms.assetid: 38b2bed2-20dd-4ce1-abc0-219343d2c4b8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
---

# What is Desktop Analytics?

Desktop Analytics is a cloud-based service that integrates with Configuration Manager. The service provides insight and intelligence for you to make more informed decisions about the update readiness of your Windows clients. It combines data from your organization with data aggregated from millions of devices connected to Microsoft cloud services.

Use Desktop Analytics with Configuration Manager to:

- Create an inventory of apps running in your organization

- Assess app compatibility with the latest Windows 10 feature updates

- Identify compatibility issues, and receive mitigation suggestions based on cloud-enabled data insights

- Create pilot groups that represent the entire application and driver estate across a minimal set of devices

- Deploy Windows 10 to pilot and production-managed devices

:::image type="content" source="media/portal-home.png" alt-text="Screenshot of the Desktop Analytics home page in the Microsoft Endpoint Manager admin center" lightbox="media/portal-home.png":::

The following video is a session from Ignite 2019, which includes more information on Desktop Analytics:

> [!VIDEO https://medius.studios.ms/Embed/Video-nc/IG19-BRK3085]

[Using Desktop Analytics and Configuration Manager to reduce Windows TCO through data-driven insights for management, servicing, and support](https://myignite.microsoft.com/archives/IG19-BRK3085)

Skip to 10:00 for an in-depth demo.

> [!NOTE]
> Desktop Analytics is a successor of Windows Analytics, which retired on January 31, 2020.
>
> The capabilities of Windows Analytics are combined in the Desktop Analytics service. Desktop Analytics is also more tightly integrated with Configuration Manager. For more information, see the [FAQ for Windows Analytics customers](faq.md#existing-windows-analytics-customers).

## Benefits

Many customers have challenges with getting and staying current with Windows 10. The primary challenge is testing applications. This process is typically manual. It's time-consuming for IT administrators and application owners to continually analyze existing applications. Then remediate any issues that arise.

Desktop Analytics provides the following benefits:

- **Device and software inventory**: Inventory of key factors such as apps and versions of Windows.

- **Pilot identification**: Identification of the smallest set of devices that provide the widest coverage of factors. It focuses on the factors that are most important to a pilot of Windows upgrades and updates. Making sure the pilot is more successful allows you to continue more quickly and confidently to broad deployments in production.

- **Issue identification**: Using aggregated market data along with data from your environment, the service predicts potential issues to getting and staying current with Windows. It then suggests potential mitigations.

- **Configuration Manager integration**: The service cloud-enables your existing on-premises infrastructure. Use this data and analysis to deploy and manage Windows on your devices.

## Prerequisites

To use Desktop Analytics, make sure your environment meets the following prerequisites.

### Technical

- An active global Azure subscription, with [global administrator](/azure/active-directory/users-groups-roles/directory-assign-admin-roles#company-administrator-permissions) permissions. [Microsoft Accounts](/windows/security/identity-protection/access-control/microsoft-accounts) aren't supported.

  > [!IMPORTANT]
  > Desktop Analytics is a Windows service hosted in Azure global that utilizes Windows diagnostic data. While Desktop Analytics is an Azure global service that's available to US government customers, it doesn't meet [US Government Community Compliance (GCC)](/office365/servicedescriptions/office-365-platform-service-description/office-365-us-government/gcc#us-government-community-compliance) attributes. For a list of compliance offerings for Microsoft products and services, see the [Microsoft Trust Center](/microsoft-365/compliance/offering-home). Desktop Analytics isn't available for GCC High or US Department of Defense (DOD) customers. The use of Azure Government subscriptions to host Desktop Analytics workspaces isn't supported.

  - **Workspace owner** permissions to **Set up your workspace**, and the following Azure Active Directory (Azure AD) roles:

    - [**Desktop Analytics Administrator**](/azure/active-directory/users-groups-roles/directory-assign-admin-roles#desktop-analytics-administrator-permissions)

    - To use an existing workspace or create a new workspace in an existing resource group: [**Log Analytics Contributor**](/azure/role-based-access-control/built-in-roles#log-analytics-contributor) and [**User Access Administrator**](/azure/role-based-access-control/built-in-roles#user-access-administrator) on the resource group.

    - To create a workspace in a new resource group: [**Owner**](/azure/role-based-access-control/built-in-roles#owner), or [**Contributor**](/azure/role-based-access-control/built-in-roles#contributor) and [**User Access Administrator**](/azure/role-based-access-control/built-in-roles#user-access-administrator) permissions on the subscription.

  - To access the portal after onboarding: [**Desktop Analytics Administrator**](/azure/active-directory/users-groups-roles/directory-assign-admin-roles#desktop-analytics-administrator-permissions) and [**Owner**](/azure/role-based-access-control/built-in-roles#owner) roles, or [**Contributor**](/azure/role-based-access-control/built-in-roles#contributor) permissions on the Log Analytics workspace.

- A supported version of Configuration Manager.

  - [**Full Administrator**](../core/understand/fundamentals-of-role-based-administration.md#bkmk_Planroles) role in Configuration Manager

  > [!NOTE]
  > Desktop Analytics supports multiple Configuration Manager hierarchies reporting to a single Azure AD tenant.<!-- 4814075 --> If you have multiple hierarchies in your environment, you have the following options:
  >
  > - Use different Commercial IDs and Azure AD tenants.
  > - Configure both hierarchies to use the same Commercial ID to share the Azure AD tenant and Desktop Analytics instance. Use [different apps](connect-configmgr.md#bkmk_connect) for connecting each hierarchy. It may take up to 30 days after you disconnect a hiearchy for the portal to reflect changes.

- Devices running Windows 7, Windows 8.1, or Windows 10

  - Install the latest updates. For more information, see [Update devices](enroll-devices.md#update-devices).

  - Managed with a supported version of the Configuration Manager client.

  - Starting in version 2010, you can use Configuration Manager to enroll Windows 10 Enterprise long-term servicing channel (LTSC) 2019 devices to Desktop Analytics. Once you enroll these devices, you can evaluate them in your deployment plans to shift from LTSC to the semi-annual servicing channel.<!--6107649-->
  
    > [!NOTE]
    > Desktop Analytics only supports the Windows 10 Enterprise LTSC 2019, which is equivalent to Windows 10, version 1809. It doesn't support Windows 10 Enterprise 2015 LTSB (version 1507) or Windows 10 Enterprise 2016 LTSB (version 1607).

    In Configuration Manager version 2006 and earlier, Desktop Analytics doesn't support upgrades to or from Windows 10 LTSC. For more information, see [Windows as a service overview](/windows/deployment/update/waas-overview#long-term-servicing-channel).

  > [!NOTE]
  > Desktop Analytics is designed to best support the in-place upgrade scenario. If you need to make major changes, such as from 32-bit to 64-bit architecture, use an imaging scenario. Desktop Analytics insights are still valuable in these classic OS deployment scenarios, but you can ignore the in-place upgrade specific guidance. For more information, see [Scenarios to deploy enterprise operating systems with Configuration Manager](../osd/deploy-use/scenarios-to-deploy-enterprise-operating-systems.md).

- Windows diagnostics data. For more information, see the following articles:

  - [Diagnostic data levels](enable-data-sharing.md#diagnostic-data-levels)

  - [Desktop Analytics privacy](privacy.md)

- Network connectivity from devices to the Microsoft public cloud. For more information, see [Internet endpoints to enable data sharing](enable-data-sharing.md#endpoints).

> [!IMPORTANT]
> Microsoft has a strong commitment to providing the tools and resources that put you in control of your privacy. As a result, Microsoft doesn't collect the following data from devices located in European countries (European Economic Area [EEA], Switzerland, and the United Kingdom):
>
> - Windows diagnostic data from Windows 8.1 devices
> - App usage data for Windows 7

### Licensing and costs

- An active global Azure subscription.

  > [!NOTE]
  > Most of the equivalent subscriptions for Configuration Manager also include Azure AD. For example, see [Microsoft 365 plans](https://www.microsoft.com/microsoft-365/compare-all-microsoft-365-plans) and [Enterprise Mobility + Security licensing](https://www.microsoft.com/licensing/product-licensing/enterprise-mobility-security).

- Devices enrolled in Desktop Analytics need a valid Configuration Manager license. For more information, see [Configuration Manager licensing](../core/understand/product-and-licensing-faq.md).

- Users of the device need one of the following licenses:

  - Windows 10 Enterprise E3 or E5 (included in Microsoft 365 F3, E3, or E5)

  - Windows 10 Education A3 or A5 (included in Microsoft 365 A3 or A5)

  - Windows Virtual Desktop Access E3 or E5

> [!NOTE]
> Beyond the cost of these license subscriptions, there's no additional cost for using Desktop Analytics within Azure Log Analytics. The data types ingested by Desktop Analytics are free from any Log Analytics data ingestion and retention charges. As non-billable data types, this data is also not subject to any Log Analytics daily data ingestion cap. For more information, see [Log Analytics usage and costs](/azure/azure-monitor/platform/manage-cost-storage).
>
> If you use another Azure solution that uses the same Log Analytics workspace, you may be charged for devices. For example, Azure Security Center. To make sure you’re not billed for Desktop Analytics devices, use a separate Log Analytics workspace for these other billed solutions.<!-- MEMDocs #590 -->

## Next steps

The following tutorial provides a step-by-step guide to getting started with Desktop Analytics in Configuration Manager:
  
> [!div class="nextstepaction"]
> [Deploy Windows 10 to pilot](tutorial-windows10.md)
