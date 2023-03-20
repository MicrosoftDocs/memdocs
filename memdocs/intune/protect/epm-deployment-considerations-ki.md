---
title: Deployment considerations for Endpoint Privilege Management
description: A list of deployment considerations and frequently asked questions for customers deploying Microsoft Intune Endpoint Privilege Management
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/20/2023
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

<!-- Deployment Considerations -->

## Frequently asked questions

### What happens when someone with administrative privileges uses a device that is enabled for EPM?

Endpoint Privilege Management doesn’t manage elevation requests by users that have administrative permissions on a device. There might be instances where an administrator launches a file that has an elevation rule (specifically an automatic elevation rule) that's defined on the device. This application launches as it normally does for the administrator.

### What files can be elevated to administrator?

Endpoint Privilege Management supports executable files. Microsoft is currently working on extending support for additional file types (MSI, etc.) and providing an easy method to elevate common operating system tasks.

## Next steps

- [Learn about Endpoint Privilege Management](../protect/epm-overview.md)
- [Guidance for creating Elevation Rules](../protect/epm-guidance-for-creating-rules.md)
- [Configure policies for Endpoint Privilege Management](../protect/epm-policies.md)
- [Reports for Endpoint Privilege Management](../protect/epm-policies.md)
- [Data collection and privacy for Endpoint Privilege Management](../protect/epm-data-collection.md)
