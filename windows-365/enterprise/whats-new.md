---
# required metadata
title: What's new in Windows 365 Enterprise
titleSuffix:
description: Find out what's new in Windows 365 Enterprise
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 03/03/2022
ms.topic: reference
ms.service: cloudpc
ms.subservice:
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: traceyadams
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
---

# What's new in Windows 365 Enterprise

Learn what new features are available in Windows 365 Enterprise.

> [!Note]
> Each monthly update may take up to a week to rollout to all customers.

<!-- Common categories:  
### App management
### Device configuration
### Device provisioning
### Device management
### Device security
### Intune apps
### Monitor and troubleshoot
### Role-based access control
### Scripts
-->

<!-- ########################## -->
## Week of February 28, 2022 (Service release 2202)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

#### Point-in-time restore (preview)<!--37063579-->

Administrators and users can now restore a Cloud PC to a state from a previous point in time. Multiple near-term and long-term restore points are available. For more information, see [Point-in-time restore for Windows 365 Enterprise](restore-overview.md).

#### Higher Cloud PC screen resolution option (preview)<!--38301718 -->

Cloud PC users can now choose a higher screen resolution when they connect to their Cloud PC from https://windows365.microsoft.com.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Documentation

#### New documentation article: Windows 365 approved partners

We’ve published a new help documentation article. For more information, see [Windows 365 approved partners](../partners.md).

<!-- ########################## -->
## Week of February 14, 2022

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Documentation

#### New documentation article: Windows 365 identity and authentication

We’ve published a new help documentation article. For more information, see [Windows 365 identity and authentication](identity-authentication.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

#### Support for Azure AD joined Cloud PCs<!-- 35060203 36751258-->

Windows 365 Enterprise now supports Cloud PCs that are Azure AD joined. These devices can run in either:

- A Microsoft-hosted network:
  - You don’t need to bring any Azure infrastructure
  - You don't need to create an on-premises network connection.
- Your own network (using an on-premises network connection)

#### Configure installed language and region for provisioning Cloud PCs<!--37095808 -->

When creating a provisioning policy, admins can now configure the installed language and region for new Cloud PCs. Previously, Cloud PCs were only created with English (United States). For more information, see [Provide users a localized Windows experience](provide-localized-windows-experience.md)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Monitor and troubleshoot

#### Use Collect diagnostics to collect additional details from Windows 365 devices through Intune remote actions<!--37678745 -->

Intune’s remote action to Collect diagnostics now collects additional details from Windows 365 Cloud PCs.

The new details for Windows 365 Cloud PCs include the following registry data:

- HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Terminal Server\AddIns\WebRTC Redirector
- HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Teams\

To learn more about the **Collect diagnostics** remote action, see [Collect diagnostics from a Windows device](/mem/intune/remote-actions/collect-diagnostics).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Provisioning

#### New supported Azure regions: US Central and German West Central<!--37678838 -->

Two new Azure regions are now for Windows 365 Cloud PC provisioning: US Central and German West Central.

For more information about supported Azure regions, see [Supported Azure regions for Cloud PC provisioning](requirements.md#supported-azure-regions-for-cloud-pc-provisioning).

<!-- ########################## -->
## Week of January 17, 2022

#### New documentation article: Optimize Cisco Webex on a Windows 365 Cloud PC<!--37106382-->

We’ve published a new help documentation article. For more information, see [Optimize Cisco Webex on a Windows 365 Cloud PC](cisco-webex-support.md).

<!-- ########################## -->
## Week of January 10, 2022

#### New documentation: Data encryption in Windows 365<!--36626607-->

We've added information to the help documentation about encryption for Windows 365 Cloud PCs. For more information, see [Data encryption in Windows 365](encryption.md).

<!-- ########################## -->
## Week of January 3, 2022

#### New documentation: Gallery image update cycle<!--36626607-->

We've added information to the help documentation about the update cycle for Windows 365 Cloud PC gallery images. For more information, see [Gallery image update cycle](device-images.md#gallery-image-update-cycle).

<!-- ########################## -->
## Week of December 13, 2021

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

#### Cloud PCs in grace period count towards active Cloud PC license usage<!-- 37017463-->

Cloud PCs that are in grace period now count towards your active Cloud PC license usage. This makes sure that your organization’s active Cloud PC allocation matches the total available licenses in your tenant.

For more information about grace period, see [Device management overview](device-management-overview.md) and [End grace period](end-grace-period.md).

<!-- ########################## -->
## Week of November 29, 2021 (Service release 2111)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

#### Operating system end of support status for Cloud PCs<!--36852572 -->

The **Provisioning policies** page has a new column: **Image status**. It tells you if the device image for each provisioning policy uses an operating system (OS) that is supported by Microsoft Windows security and other updates. For more information, see [Lifecycle policies and end of support for Cloud PC OS](end-of-support.md).

#### New documentation article: Optimize Zoom on a Windows 365 Cloud PC<!--37106382-->

We’ve published a new help documentation article. For more information, see [Optimize Zoom on a Windows 365 Cloud PC](zoom-support.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device security

#### Two new security baseline settings for Windows 11 Cloud PCs<!--36989243 -->

Windows 365 Enterprise now supports the following Windows 11 security baseline settings:

- **Tamper Protection**: Helps protect Cloud PCs from bad actors bypassing security features like anti-virus protection.

- **Script Scanning**: Helps identify possible threats by intercepting scripts and scanning them before they’re run.

For more information about the security baseline updates for Windows 11, see [Windows 11 Security baseline](https://techcommunity.microsoft.com/t5/microsoft-security-baselines/windows-11-security-baseline/ba-p/2810772). For more information about setting security baselines for Cloud PCs, see [Deploy security baselines](deploy-security-baselines.md).

<!-- ########################## -->
## Week of November 1, 2021 (Service release 2110)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

#### Improved user interface for online access to Cloud PCs<!--36735456 -->

The user interface on [windows365.microsoft.com](https://windows365.microsoft.com) has been improved with:

- Faster load times.
- Higher performance reliability.
- Local resource settings (printer, microphone, clipboard).
- Alternative keyboard settings.
- Edit settings in-session.
- Accessibility support.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Provisioning

#### Provisioning maximum timeout changed to five hours<!--36461463-->

To improve reliability, the maximum provisioning timeout has been changed to five hours.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Role-based access control

#### Custom Windows 365 RBAC roles in public preview<!--36222579  -->

Custom Windows 365 role-based access control (RBAC) roles are now available in the Microsoft Endpoint Manager admin center. You can mix-and-match Windows 365 permissions to create custom roles for your organization's needs. You can also create both Windows 365 and Intune custom roles and give granular admin permissions to admins for both services. For more information, see [Custom roles](role-based-access.md#custom-roles-public-preview).

<!-- ########################## -->
## Week of October 11, 2021 (Service release 2109)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

#### Resize support for preview and trial licenses<!--36228235-->

If you have a combination of paid and free trial licenses, the Resize remote action will use your paid licenses first. When those run out, it will use your trial licenses. For more information, see [Resize a Cloud PC](resize-cloud-pc.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device provisioning

#### Health check improvement<!--36461502-->

The **DNS can resolve Active Directory domain** health check has been improved. A new step has been added to look for the following Azure Active Directory DNS record. If it can’t be found, the check fails.

_ldap._tcp.yourDomain.com -type SRV

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Role-based access control

#### Windows 365 Administrator role<!--5827123-->

The Windows 365 Administrator role is now available for admins by using role assignment in the Microsoft Endpoint Manager Admin Center and Azure Active Directory (Azure AD) for Windows. With this role, admins can broadly manage Windows 365 Enterprise Cloud PCs, users, devices, and groups. This new role is in addition to the other existing roles that Windows 365 currently supports: Azure AD Global Admin, Intune Admin, and Cloud PC granular roles in Microsoft Endpoint Manager. For more information, see [Role-based access control](role-based-access.md).

<!-- ########################## -->
## Week of October 4, 2021
<!-- vvvvvvvvvvvvvvvvvvvvvv -->

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

#### Support for Windows 11<!--35091970 -->

Windows 365 Enterprise now supports Windows 11 as a Cloud PC operating system.

Windows 11 Cloud PCs require Generation 2 (Gen2) virtual machines. For information about converting existing Generation 1 custom device images to Gen2, see [Convert an existing custom device image to a generation 2 virtual machine](device-images-convert-generation-2.md).

## Week of September 13, 2021
<!-- vvvvvvvvvvvvvvvvvvvvvv -->

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

#### New PowerShell script for installing languages on custom device images<!--35726116-->

The [Windows365LanguagesInstaller PowerShell script]( https://www.powershellgallery.com/packages/Windows365LanguagesInstaller) can install 38 additional languages on your custom device images. For more information, see [Provide a localized Windows experience](provide-localized-windows-experience.md#add-languages-to-windows-using-a-script-and-capture-the-image).

<!-- ########################## -->
## Week of September 6, 2021 (Service release 2108)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

#### End grace period option<!--34841603-->

Certain conditions put a Cloud PC into a seven-day grace period. At the end of this time the Cloud PC will be deprovisioned and user will lose access.

You can now immediately end the grace period for individual Cloud PCs. By ending the grace period manually, you won’t have to wait the full seven days to remove user access from the Cloud PC.

For more information on grace periods, see [End grace period](end-grace-period.md).

<!-- ########################## -->
## Week of August 30, 2021

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Monitor and troubleshoot

#### Resource performance report in Endpoint Analytics<!-- 32978343 -->

Endpoint analytics has a new report named **Resource performance**. The **Resource performance report** includes metrics for CPU and RAM performance on Cloud PCs. For more information, see [Resource performance report](report-resource-performance.md).

#### Remoting connection report in Endpoint Analytics<!-- 33039368 -->

Endpoint analytics has a new report named **Remoting connection report**. This report includes the following metrics:

- **Cloud PC Sign in time (sec)** provides the total time users take to connect to the cloud PC.
- **Round Trip Time (ms)** provides insights on the speed and reliability of network connections from the user location.

For more information, see [Remoting connection report](report-remoting-connection.md).

<!-- ########################## -->
## Week of August 2, 2021

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
<!--### Feature area alpha-->

### Windows 365 now generally available<!--10393594 -->

Windows 365 is a new service from Microsoft that automatically creates Cloud PCs for your end users. Cloud PCs are a new hybrid personal computing category that use both the power of the cloud and the accessing device to provide a full and personalized Windows virtual machine. Admins can use Microsoft Endpoint Manager to define the configurations and applications that are provisioned for each user’s Cloud PC. End users can access their Cloud PC from any device and any location. Windows 365 stores the end user’s Cloud PC and data in the cloud, not on the device, providing a secure experience.

For more information about Windows 365, see [Windows 365](https://www.microsoft.com/windows-365?rtc=1).

<!-- ########################## -->
## Next steps

For details about Windows 365 licensing, see [Windows 365 pricing](https://www.microsoft.com/windows-365/enterprise/compare-plans-pricing).
