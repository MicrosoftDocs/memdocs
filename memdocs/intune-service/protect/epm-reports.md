---
title: Monitor your Endpoint Privilege Management policies for Microsoft Intune
description: View reports for managed and unmanaged file elevations when you use Endpoint Privilege Management for Microsoft Intune.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 02/12/2025
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high

# optional metadata

#ROBOTS:
#audience:
 
ms.reviewer: mikedano
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier 1
- M365-identity-device-management
- sub-intune-suite
---

# Reports for Endpoint Privilege Management

[!INCLUDE [intune-add-on-note](../includes/intune-add-on-note.md)]

*Elevation reports for Endpoint Privilege Management are currently in preview.*

With Microsoft Intune **Endpoint Privilege Management (EPM)** your organization’s users can run as a standard user (without administrator rights) and complete tasks that require elevated privileges. Tasks that commonly require administrative privileges are application installs (like Microsoft 365 Applications), updating device drivers, and running certain Windows diagnostics.

Endpoint Privilege Management supports your zero-trust journey by helping your organization achieve a broad user base running with least privilege, while allowing users to still run tasks allowed by your organization to remain productive.

The information available in EPM reports depends on the *reporting scope* of a device. The reporting scope for each device is configured as part of a [Windows elevation settings policy](../protect/epm-policies.md#windows-elevation-settings-policy), and different devices can have different reporting scope configurations.

The EPM reports are available from the *Reports* tab of the *Endpoint Privilege Management* node from within the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) at **Endpoint security** > **Endpoint Privilege Management**, and select the **Reports** tab. The report data is retained for 30 days. To view a report, select from the following tiles:

- Elevation report
- Managed elevations report
- Elevation report by applications
- Elevation report by publisher
- Elevation report by user

> [!NOTE]
>
> Data is processed once every 24 hours. There may be a delay before seeing data in the elevation usage reports.

## Elevation report

The *Elevation report* displays a list view with details about all reported elevations. This list includes elevations that are managed by specific rules and elevations that are captured by default elevation setting policies. Several columns of information are available by default, including but not limited to:

- **File name** - The name of the file that received an elevation request.
- **User** - The user who requested elevation of the file.
- **Device** - The name of the device on which the file request was made.
- **Result** - Whether the elevation was successful.
- **Date and time** - When the elevation request was made.

By selecting an entry in the report, you can drill in to view more details about the elevation request and the file involved.

## Managed elevation report

The *Managed elevation report* displays the same types of detail as the *Elevation report*, but reports on only the elevations that are managed by a *Windows elevation rule policy*.

## Elevation report by applications

The *Elevation report by applications* report displays details for all managed and unmanaged elevations, aggregated by the application that elevated. Details include:

- **Internal file name**
- **File version**
- **Publisher**
- **Elevation type**
- **Elevation count**

The information in this report can help identify applications that might require elevation rules to function properly, including rules for child processes.

## Elevation report by publisher

The *Elevation report by publisher* report displays details for all managed and unmanaged elevations, aggregated by the publisher of the app that elevated. Details include:

- **Publisher**
- **Elevation type**
- **Elevation count**

The information in this report can help identify related applications and the source of applications that are run elevated in your environment.

## Elevation report by user

The *Elevation report by user* report displays details for all managed and unmanaged elevations, aggregated by the user that elevated. Details include:

- **Internal file name**
- **File version**
- **Publisher**
- **Elevation type**
- **Elevation count**

The information in this report can help identify applications on a per-user basis that might require elevation rules to function properly, including rules for child processes.

## Endpoint Privilege Management policy details

In addition to the dedicated reports, you can view basic details about EPM policies from the Policies tab of the Endpoint Privilege Management node. This node is the same location in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) where you create policies for EPM: In the admin center, go to **Endpoint security** > **Endpoint Privilege Management**, and select the **Policies** node.

## Related content

- [Guidance for creating Elevation Rules](../protect/epm-guidance-for-creating-rules.md)
- [Configure policies for Endpoint Privilege Management](../protect/epm-policies.md)
- [Approving elevation requests](../protect/epm-support-approved.md)
- [Data collection and privacy for Endpoint Privilege Management](../protect/epm-data-collection.md)
- [Deployment considerations and frequently asked questions](../protect/epm-deployment-considerations-ki.md)
