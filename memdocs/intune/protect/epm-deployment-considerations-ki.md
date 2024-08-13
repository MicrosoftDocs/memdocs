---
title: Deployment considerations for Endpoint Privilege Management
description: A list of deployment considerations and frequently asked questions for customers deploying Microsoft Intune Endpoint Privilege Management
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 06/18/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high

# optional metadata

#ROBOTS:
#audience:
 
ms.reviewer: mattcall
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier 1
- M365-identity-device-management
- sub-intune-suite
---

# Deployment Considerations and frequently asked questions for Endpoint Privilege Management

[!INCLUDE [intune-add-on-note](../includes/intune-add-on-note.md)]

With Microsoft Intune **Endpoint Privilege Management (EPM)** your organization’s users can run as a standard user (without administrator rights) and complete tasks that require elevated privileges. Tasks that commonly require administrative privileges are application installs (like Microsoft 365 Applications), updating device drivers, and running certain Windows diagnostics.

Endpoint Privilege Management supports your zero-trust journey by helping your organization achieve a broad user base running with least privilege, while allowing users to still run tasks allowed by your organization to remain productive.

The following sections of this article discuss deployment considerations and frequently asked questions for EPM.

Applies to:

- Windows 10
- Windows 11

## Deployment considerations for Endpoint Privilege Management

### Windows 10 devices might not immediately receive confirmation of support approvals

We're working to resolve a few scenarios that prevent Windows 10 devices from automatically receiving the notification that a new approval is ready for the device when you use [support approved elevations](../protect/epm-support-approved.md#about-support-approved-elevations). We're working with the owner to resolve this as quickly as possible.

### Organization that disable User Account Control (UAC) might experience issues with Endpoint Privilege Management

Endpoint Privilege Management doesn't support UAC being explicitly disabled. Windows policy controls for UAC Prompt Behavior exist to control the behavior of UAC. If organizations take extra steps to disable UAC outside of the existing policy controls, like disabling Windows services, they might experience issues with Endpoint Privilege Management.

### Organizations use Application Control for Business might experience issues running Endpoint Privilege Management

Application Control for Business policies that don't account for the EPM client components could prevent the EPM components from functioning. In order to use EPM with AppControl, ensure that your Application Control policy includes rules that allow EPM to function. For more information about troubleshooting application control, see [WDAC debugging and troubleshooting](/windows/security/application-security/application-control/windows-defender-application-control/operations/wdac-debugging-and-troubleshooting).

> [!Note]
> EPM is not included in default policies for Application Control and may require creating custom policies.

### Organizations restricting users who can sign in interactively might see issues with Endpoint Privilege Management

Endpoint Privilege Management uses an isolated account to facilitate elevations. This account requires the ability to create an interactive logon session. Organizations who limit the ability for users to create interactive sessions need to make changes for EPM to function properly.

### Users requesting support approval for elevation must be the primary user on the device

Endpoint Privilege Management currently requires the user requesting an elevation to be the primary user of the device. We're working to remove this limitation in a future release.

### Authoring files with a file name as one of the sole attributes for identification

File name is an attribute that can be utilized to detect an application that needs to be elevated. However, it isn't protected by the signature of the file.

File names are *highly susceptible* to change, and files that are signed with a certificate that you trust could have their name changed to be *detected* and subsequently *elevated* which might not be your intended behavior.

> [!IMPORTANT]
> Always ensure that rules including a file name include other attributes that provide a strong assertion to the file's identity. Attributes like file hash or properties that are included in the files signature are good indicators that the file you intend is likely the one being elevated.

### Elevation settings policies might show conflict if changed in quick succession

Endpoint Privilege Management reports status of individual settings applied using the *Elevation Settings* profile. If settings in this profile (Default elevation behavior for instance) are changed multiple times in quick succession, it might result device reporting conflict or falling back to the default behavior of *Denying* the elevation. This is a transient state and resolves without further action (in less than 60 minutes). This issue will be fixed in a future release.

### Blocked files downloaded from the internet fail to elevate

Behavior exists in Windows to set an attribute on files that are downloaded directly from the internet and prevent them from executing until validated. Windows has functionality to validate the reputation of files downloaded from the internet. When a files reputation isn't validated, it might fail to elevate. 

To correct this behavior, unblock the file by unblocking the file from the file properties pane. *Unblocking a file should only be done when you trust the file*.

### Windows devices that are "workplace joined" fail to enable Endpoint Privilege Management

Devices that are workplace joined aren't supported by Endpoint Privilege Management. These devices won't show success or process EPM policies (elevation settings or elevation rules) when deployed to the device.

### Rules for a network file might fail to elevate

Endpoint Privilege Management supports executing files that are locally stored on disk. Executing files from a network location, such as a network share or mapped drive, is not supported.

### Endpoint Privilege Management doesn't receive policy when I use a 'SSL-inspection' on my network infrastructure

Endpoint Privilege Management doesn't support SSL inspection, which is known as 'break and inspect'. In order to use Endpoint Privilege Management, ensure the URLs listed in the [Intune Endpoints for Endpoint Privilege Management](../fundamentals/intune-endpoints.md#microsoft-intune-endpoint-privilege-management) are exempt from inspection.

## Frequently asked questions

### Why is my virtual device not onboarding to Endpoint Privilege Management?

Currently, Endpoint Privilege Management isn't supported with Azure Virtual Desktop. This issue will be fixed in future release.

Support for Windows 365 (Cloud PCs) was added in September 2023.

### Why is my elevation settings policy showing error/not applicable?

The elevation settings policy controls the enablement of EPM and the configuration of the client side components. When this policy is in error or shows not applicable, it indicates the device had an issue enabling EPM. The two most common reasons are missing the [required Windows updates](../protect/epm-overview.md#requirements) or failure to communicate with required [Intune Endpoints for Endpoint Privilege Management](../fundamentals/intune-endpoints.md#microsoft-intune-endpoint-privilege-management).

### What happens when someone with administrative privileges uses a device that is enabled for EPM?

Endpoint Privilege Management doesn’t manage elevation requests by users that have administrative permissions on a device. There might be instances where an administrator launches a file that has an elevation rule (specifically an automatic elevation rule) that's defined on the device. This application launches as it normally does for the administrator and an event for an unmanaged elevation will be generated by EPM.

### What files can be elevated to administrator?

Endpoint Privilege Management supports executable files including those with the `.msi` extension and `.ps1` PowerShell scripts.

### Why doesn't 'Run with elevated access" show on start menu items?

Certain items that reside in the start menu or taskbar have a curated right-click menu and the EPM right-click context menu isn't able to be added to those menus. We plan to fix this issue in a future release.

### Can I launch multiple files as elevated with the "Run with elevated access" right-click context menu?

Only one file can be elevated at a time. To launch multiple files elevated, right-click each file individually and select *Run with elevated access*.

## Next steps

- [Learn about Endpoint Privilege Management](../protect/epm-overview.md)
- [Guidance for creating Elevation Rules](../protect/epm-guidance-for-creating-rules.md)
- [Configure policies for Endpoint Privilege Management](../protect/epm-policies.md)
- [Reports for Endpoint Privilege Management](../protect/epm-reports.md)
- [Data collection and privacy for Endpoint Privilege Management](../protect/epm-data-collection.md)
