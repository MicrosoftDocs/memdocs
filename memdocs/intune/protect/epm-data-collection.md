---
title: Review the data that Endpoint Privilege Management collects when used with Microsoft Intune
description: View details about the type of data Endpoint Privilege Management can collect and store when used with Microsoft Intune.
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

# Data collection and privacy for Endpoint Privilege Management

<!-- [!INCLUDE [intune-add-on-note](../includes/intune-add-on-note.md)] -->
> [!NOTE]  
> This capability is in public preview and available to use without a license. After public preview, it will be available as an Intune add-on. For more information, see [Use Intune Suite add-on capabilities](../fundamentals/intune-add-ons.md).

Microsoft Intune Endpoint Privilege Management (EPM) allows your organization’s users to run as a standard user (without administrator rights) and complete tasks that require elevated privileges. Tasks that commonly require administrative privileges are application installs (like Microsoft 365 Applications), updating device drivers, and running certain Windows diagnostics. Endpoint Privilege Management supports your zero-trust journey by helping your organization achieve a broad user base running with least privilege, while allowing users to still run tasks allowed by your organization to remain productive.

The following sections of this article discuss requirements to use EPM, provide a functional overview of how this capability works, and introduce important concepts for EPM.

Applies to:

- Windows 10
- Windows 11

## Overview of data collection

Endpoint Privilege Management (EPM) collects data to support elevation usage scenarios and to provide diagnostic intelligence to Microsoft. The data collected is generally related to elevation activities that occur on a device, such as metadata about the file or user completing the elevation, as well the device that completed the elevation.

## Diagnostic Data

Diagnostic data is event data that is used by Microsoft to monitor the health of the client side components that provide the capability to elevate as a standard user.

### Diagnostic data collected

<!-- Insert Diagnostic Data collection Table-->

## Usage Data

Usage data is elevation data this is used by customers to determine what elevations have occurred in their environment. This data is stored with your Intune infrastructure and is used to populate the elevation reports. When configuring *reporting scope* you have the ability to configure what scope of data is collected. You can chose between none, only elevations completed by EPM, or all elevations that take place on a device.

### Usage data collected

<!-- Insert Usage Data collection table here -->

## Next steps
[Learn about Endpoint Privilege Management](../protect/epm-overview.md)