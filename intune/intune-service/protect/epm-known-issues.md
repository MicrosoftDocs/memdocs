---
title: Known Issues for Endpoint Privilege Management with Microsoft Intune
description: Configure policies that define how Endpoint Privilege Management functions in your tenant, and behaviors when elevating files to run in administrative context.
author: brenduns
ms.author: brenduns
ms.date: 09/10/2025
ms.topic: how-to
ms.reviewer: mikedano
ms.subservice: suite
ms.collection:
- tier 1
- M365-identity-device-management
- sub-intune-suite
---

# Known Issues for Endpoint Privilege Management

[!INCLUDE [intune-add-on-note](../includes/intune-add-on-note.md)]

[!INCLUDE [intune-epm-overview](includes/intune-epm-overview.md)]

This article lists known issues with Endpoint Privilege Management.

## Windows 10 devices might not immediately receive confirmation of support approvals

We're working to resolve a few scenarios that prevent Windows 10 devices from automatically receiving the notification that a new approval is ready for the device when you use [support approved elevations](../protect/epm-support-approved.md#about-support-approved-elevations).

## Organizations that disable User Account Control (UAC) might experience issues with Endpoint Privilege Management

Endpoint Privilege Management doesn't support UAC being explicitly disabled. Windows policy controls for UAC Prompt Behavior exist to control the behavior of UAC. If organizations take extra steps to disable UAC outside of the existing policy controls, like disabling Windows services, they might experience issues with Endpoint Privilege Management.

## Organizations that enable Administrator Protection might experience issues with Endpoint Privilege Management

Administrator Protection doesn't currently support elevations initiated from Endpoint Privilege Management. If organizations enable Administrator Protection on devices where standard users rely on Endpoint Privilege Management (EPM) to handle elevation, the elevation fails. We're working to resolve this issue in a future release.

## Organizations using Application Control for Business might experience issues running Endpoint Privilege Management

Application Control for Business policies that don't account for the EPM client components could prevent the EPM components from functioning. In order to use EPM with AppControl, ensure that your Application Control policy includes rules that allow EPM to function. For more information about troubleshooting application control, see [WDAC debugging and troubleshooting](/windows/security/application-security/application-control/windows-defender-application-control/operations/wdac-debugging-and-troubleshooting).

> [!Note]
> EPM is not included in default policies for Application Control and may require creating custom policies.

## Organizations restricting users who can sign in interactively might see issues with Endpoint Privilege Management

Endpoint Privilege Management uses an isolated account to facilitate elevations. This account requires the ability to create an interactive sign-in session. Organizations who limit the ability for users to create interactive sessions need to make changes for EPM to function properly.

## Users requesting support approval for elevation must be the primary user on the device

Endpoint Privilege Management currently requires the user requesting an elevation to be the primary user of the device. We're working to remove this limitation in a future release.

## Authoring files with a file name as one of the sole attributes for identification

File name is an attribute that can be utilized to detect an application that needs to be elevated. However, it isn't protected by the signature of the file.

File names are *highly susceptible* to change, and files that are signed with a certificate that you trust could have their name changed to be *detected* and then *elevated*, which might not be your intended behavior.

> [!IMPORTANT]
> Always ensure that rules including a file name include other attributes that provide a strong assertion to the file's identity. Attributes like file hash or properties that are included in the files signature are good indicators that the file you intend is likely the one being elevated.

## Elevation settings policies might show conflict if changed in quick succession

Endpoint Privilege Management reports status of individual settings applied using the *Elevation Settings* profile. If settings in this profile (Default elevation behavior for instance) are changed multiple times in quick succession, it might result in devices reporting a conflict or falling back to the default behavior of *Denying* the elevation. These results are a transient state and resolve without further action in less than 60 minutes. This issue will be fixed in a future release.

## Blocked files downloaded from the internet fail to elevate

Behavior exists in Windows to set an attribute on files that are downloaded directly from the internet and prevent them from executing until validated. Windows has functionality to validate the reputation of files downloaded from the internet. When a files reputation isn't validated, it might fail to elevate.

To correct this behavior, unblock the file by unblocking the file from the file properties pane. *Unblocking a file should only be done when you trust the file*.

## Network and cloud resource access limitations

Apps elevated with Endpoint Privilege Management run in an isolated security context and can't access resources that require user authentication. This includes access to network shares and cloud services like OneDrive, SharePoint, and Azure.

If access to these resources is needed, consider whether elevation is required at runtime.

## Windows devices that are "workplace joined" fail to enable Endpoint Privilege Management

Endpoint Privilege Management doesn't support devices that are workplace joined. These devices won't show success or process EPM policies (elevation settings or elevation rules) when deployed to the device.

## Rules for a network file might fail to elevate

Endpoint Privilege Management supports running files that are locally stored on disk. EPM doesn't support running files from a network location, such as a network share or mapped drive.

## Endpoint Privilege Management doesn't receive policy when I use a 'SSL-inspection' on my network infrastructure

Endpoint Privilege Management doesn't support SSL inspection, which is known as 'break and inspect'. In order to use Endpoint Privilege Management, ensure the URLs listed in the [Intune Endpoints for Endpoint Privilege Management](../fundamentals/intune-endpoints.md#microsoft-intune-endpoint-privilege-management) are exempt from inspection.

### Certain Windows functions, such as control panel items or configurations in the settings app can't be elevated with EPM

EPM can elevate Executables (.exe), Windows Installer (.msi), and PowerShell scripts (.ps1). Some functions in Windows are executed in ways that EPM can't detect and elevate. As a workaround, some of these things could be packaged as scripts and approved for elevation with EPM.

### Certificate based rules only work for valid certificates

EPM checks the certificate expiry date to ensure it hasn't passed before allowing elevation. Rules based on certificates that are expired will fail to elevate.
