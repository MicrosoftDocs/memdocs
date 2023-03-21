---
title: Deployment considerations for Endpoint Privilege Management
description: A list of deployment considerations and frequently asked questions for customers deploying Microsoft Intune Endpoint Privilege Management
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/23/2023
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology:

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
---

# Deployment Considerations and frequently asked questions for Endpoint Privilege Management

<!-- [!INCLUDE [intune-add-on-note](../includes/intune-add-on-note.md)] -->

> [!NOTE]  
> This capability is in public preview and available to use without a license. After public preview, it will be available as an Intune add-on. For more information, see [Use Intune Suite add-on capabilities](../fundamentals/intune-add-ons.md).

Microsoft Intune Endpoint Privilege Management (EPM) allows your organization’s users to run as a standard user (without administrator rights) and complete tasks that require elevated privileges.

Tasks that commonly require administrative privileges are application installs (like Microsoft 365 Applications), updating device drivers, and running certain Windows diagnostics.

Endpoint Privilege Management supports your zero-trust journey by helping your organization achieve a broad user base running with least privilege, while allowing users to still run tasks allowed by your organization to remain productive.

The following sections of this article discuss deployment considerations and frequently asked questions for EPM.

Applies to:

- Windows 10
- Windows 11

## Deployment considerations for Endpoint Privilege Management

### Authoring files with a file name as one of the sole attributes for identification

File name is an attribute that can be utilized to detect an application that needs to be elevated. However, it is not protected by the signature of the file.

This means that file names are *highly susceptible* to change, and files signed by a certificate that you trust could have their name changed to be *detected* and subsequently *elevated* which may not be your intended behavior.

> [!IMPORTANT]
> Always ensure that rules including a file name include other attributes that provide a strong assertion to the file's identity. Attributes like file hash or properties that are included in the files signature are good indicators that the file you intend is likely the one being elevated.

### Blocked files downloaded from the internet fail to elevate

Behavior exists in Windows to set an attribute on files that are downloaded directly from the internet and prevent them from executing until validated. Windows has functionality to validate the reputation of files downloaded from the internet. When a files reputation isn't validated it might fail to elevate. To correct this behavior, unblock the file by unblocking the file from the file properties pane. *This should only be done when you trust the file*.

### Certificate rules defined with a file path may fail to elevate

When defining a certificate rule with a file path, Endpoint Privilege Management may fail to elevate files signed by the certificate as the administrator intended. To work around this issue, supply a file name in addition to the file path. This will be fixed in a future release.

### Certificate rules defined as Issuing Certificate Authority may not allow elevation

When defining a certificate rule and specifying the certificate as an 'Issuing CA', EPM may not allow elevation when the certificate is properly part of the certificate chain. To work around this issue, specify the publisher certificate of the file instead. This will be fixed in a future release.

### On Windows 11, 'Run with elevated access' is shown under 'show more options' when I right-click on a file

Windows 11 introduced a new paradigm for right-click context menus. EPM currently shows under the 'show more options' selection from that menu. This will be fixed in a future release.

### When creating rules for a network file, elevation fails to occur

Endpoint Privilege Management supports executing files that are locally stored on disk. Executing files from a network share isn't allowed.

### Endpoint Privilege Management does not receive policy when I use a 'SSL-inspection' on my network infrastructure

Endpoint Privilege Management does not support SSL inspection (commonly referred to as 'break and inspect'). In order to use Endpoint Privilege Management, ensure the URL's listed in the [Intune Endpoints for Endpoint Privilege Management](../fundamentals/intune-endpoints.md#microsoft-intune-endpoint-privilege-management) are exempt from inspection.

## Frequently asked questions

### What happens when someone with administrative privileges uses a device that is enabled for EPM?

Endpoint Privilege Management doesn’t manage elevation requests by users that have administrative permissions on a device. There might be instances where an administrator launches a file that has an elevation rule (specifically an automatic elevation rule) that's defined on the device. This application launches as it normally does for the administrator.

### What files can be elevated to administrator?

Endpoint Privilege Management supports executable files. Microsoft is currently working on extending support for additional file types (MSI, etc.) and providing an easy method to elevate common operating system tasks.

### Why doesn't 'Run with elevated access" show on start menu items?

Certain items that reside in the start menu or taskbar have a curated right-click menu and the EPM right-click context menu is not able to be added to those menus. We are planning to fix this in a future release.

### Some applications and shortcuts fail to elevate when command-line parameters are present

Certain command line compositions can cause elevations to fail on the client. This will be fixed in future release.

### Can I launch multiple files as elevated with the "Run with elevated access" right-click context menu?

Only one file can be elevated at a time. To launch multiple files elevated, right-click each file individually and select *Run with elevated access*.

## Next steps

- [Learn about Endpoint Privilege Management](../protect/epm-overview.md)
- [Guidance for creating Elevation Rules](../protect/epm-guidance-for-creating-rules.md)
- [Configure policies for Endpoint Privilege Management](../protect/epm-policies.md)
- [Reports for Endpoint Privilege Management](../protect/epm-policies.md)
- [Data collection and privacy for Endpoint Privilege Management](../protect/epm-data-collection.md)
