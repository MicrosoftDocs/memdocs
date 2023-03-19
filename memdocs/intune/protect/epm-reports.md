---
title: Monitor your Endpoint Privilege Management policies for Microsoft Intune
description: View reports for managed and unmanaged file elevations when you use Endpoint Privilege Management for Microsoft Intune.
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

# Reports for Endpoint Privilege Management 

<!-- [!INCLUDE [intune-add-on-note](../includes/intune-add-on-note.md)] -->
> [!NOTE]  
> This capability is in public preview and available to use without a license. After public preview, it will be available as an Intune add-on. For more information, see [Use Intune Suite add-on capabilities](../fundamentals/intune-add-ons.md).

Microsoft Intune Endpoint Privilege Management (EPM) allows your organization’s users to run as a standard user (without administrator rights) and complete tasks that require elevated privileges. Tasks that commonly require administrative privileges are application installs (like Microsoft 365 Applications), updating device drivers, and running certain Windows diagnostics. Endpoint Privilege Management supports your zero-trust journey by helping your organization achieve a broad user base running with least privilege, while allowing users to still run tasks allowed by your organization to remain productive.

The information available in EPM reports depends on a devices *reporting scope*. The reporting scope for each device is configured as part of a [Windows elevation settings policy](../protect/epm-policies.md#windows-elevation-settings-policy), and different devices can have different reporting scope configurations.

The following EPM reports are available from the *Reports* tab of the *Endpoint Privilege Management* node, that you can access from within the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by going to **Endpoint security** > **Endpoint Privilege Management**, and selecting the **Reports** tab:

- Elevation report
- Managed elevations report

## Elevation report

The *Elevation report* displays a list view with details about all reported elevations. This includes elevations that are managed by specific rules and those that are not defined by rules but are captured by default elevation setting policies. Several columns of information are available by default, including but not limited to: 

- **File name** - The name of the file that received an elevation request.
- **User** - The user who requested elevation of the file.
- **Device** - The name of the device on which the file request was made.
- **Result** - Whether or not the elevation was successful.
- **Date and time** - When the elevation request was made.

By selecting an entry in the report, you can drill in to view more details about the elevation request and the file involved.

## Managed elevation report

The *Managed elevation report* displays the same types of detail as the *Elevation report*, but is limited to reporting on elevations that are managed by a *Windows elevation rule policy*.

## Endpoint Privilege Management policy details

In addition to the dedicated reports, you can view basic details about EPM policies from the Policies tab of the Endpoint Privilege Management node. This is the same location in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) where you create policies for EPM: In the  admin center, go to **Endpoint security** > **Endpoint Privilege Management**, and select the **Policies** node.

## Next steps

[Learn about Endpoint Privilege Management](../protect/epm-overview.md)

[Data collection for Endpoint Privilege Management](../protect/epm-data-collection.md)