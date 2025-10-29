---
title: Monitor your Endpoint Privilege Management policies for Microsoft Intune
description: View reports for managed and unmanaged file elevations when you use Endpoint Privilege Management for Microsoft Intune.
author: brenduns
ms.author: brenduns
ms.date: 10/20/2025
ms.topic: how-to
ms.reviewer: mikedano
ms.subservice: suite
ms.collection:
- tier 1
- M365-identity-device-management
- sub-intune-suite
---

# Reports for Endpoint Privilege Management

[!INCLUDE [intune-add-on-note](../includes/intune-add-on-note.md)]

*Elevation reports for Endpoint Privilege Management are currently in preview.*

[!INCLUDE [intune-epm-overview](includes/intune-epm-overview.md)]

The information available in Endpoint Privilege Management (EPM) reports depends on the *reporting scope* of a device. The reporting scope for each device is configured as part of a [Windows elevation settings policy](../protect/epm-elevation-settings.md), and different devices can have different reporting scope configurations.

EPM reports are found within the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) at **Endpoint security** > **Endpoint Privilege Management**, and available through the Overview tab and the Reports tab. The [**Overview** tab](#overview-dashboard) is a readiness dashboard for moving admin users to standard users. The [**Reports**](#available-reports) tab presents several report tiles for different aspects of EPM, which also help power the readiness dashboard. EPM report data is retained for 30 days. 

The following reports are available from the Report tab:

- [Elevation report](#elevation-report)
- [Managed elevations report](#managed-elevations-report)
- [Elevation report by applications](#elevation-report-by-applications)
- [Elevation report by publisher](#elevation-report-by-publisher)
- [Elevation report by user](#elevation-report-by-user)

> [!NOTE]
>
> Data is processed once every 24 hours. There might be a delay before seeing data in the elevation usage reports.

## Overview dashboard

The EPM Overview tab provides a dashboard that can help you assess your organization's readiness in migrating your local admin user accounts to standard users, securely and efficiently. Information tiles on this dashboard include details pulled from the last 48 hours for the following file and elevation activities:

- **Users who have only unmanaged file elevations**. This tile identifies the count of users who are running files in an elevated context that aren't managed by EPM. This information can help you create policies to close gaps in your EPM coverage.

- **Users who have both managed and unmanaged file elevations**. This tile can help you identify how to refine elevation settings policy to help audit file elevations and begin to move them into a managed state.

- **User with only managed elevations**. The information provided by this tile helps identify those users who might be ready to run without admin permissions assigned to their user account. To remove local admin permissions, you can deploy account protection policies to manage the local user group membership.

- **Frequently unmanaged elevations**. A list of the files with the most unmanaged elevation requests in the current snapshot period. This list can help you identify files that either are unmanaged or might need refined elevation rules or have existing elevation rules applied to additional users.

- **Frequently approved by support**. Use this information to understand files that currently require support approval to elevate but might be candidates for a non-support approved elevation rule. Moving such files to more direct elevation rules can reduce friction for your users.

- **Frequently denied elevations**. View the files that most frequently are denied, which can help identify new files that require elevation rules.

Finally, at the bottom of the dashboard you can view **Elevation trends**.

## Available reports

The following sections briefly describe each report tile found on the *Reports* tab for Endpoint Privilege Management.

### Elevation report

The *Elevation report* displays a list view with details about all reported elevations. This list includes elevations that are managed by specific rules and elevations that are captured by default elevation setting policies. Several columns of information are available by default, including but not limited to:

- **File name** - The name of the file that received an elevation request.
- **User** - The user who requested elevation of the file.
- **Device** - The name of the device on which the file request was made.
- **Result** - Whether the elevation was successful.
- **Date and time** - When the elevation request was made.

By selecting an entry in the report, you can drill in to view more details about the elevation request and the file involved.

### Managed elevations report

The *Managed elevation report* displays the same types of detail as the *Elevation report*, but reports on only the elevations that are managed by a *Windows elevation rule policy*.

### Elevation report by applications

The *Elevation report by applications* report displays details for all managed and unmanaged elevations, aggregated by the application that elevated. Details include:

- **Internal file name**
- **File version**
- **Publisher**
- **Elevation type**
- **Elevation count**

The information in this report can help identify applications that might require elevation rules to function properly, including rules for child processes.

### Elevation report by publisher

The *Elevation report by publisher* report displays details for all managed and unmanaged elevations, aggregated by the publisher of the app that elevated. Details include:

- **Publisher**
- **Elevation type**
- **Elevation count**

The information in this report can help identify related applications and the source of applications that are run elevated in your environment.

### Elevation report by user

The *Elevation report by user* report displays details for all managed and unmanaged elevations, aggregated by the user that elevated. Details include:

- **Internal file name**
- **File version**
- **Publisher**
- **Elevation type**
- **Elevation count**

The information in this report can help identify applications on a per-user basis that might require elevation rules to function properly, including rules for child processes.

### Endpoint Privilege Management policy details

In addition to the dedicated reports, you can view basic details about EPM policies from the Policies tab of the Endpoint Privilege Management node. This node is the same location in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) where you create policies for EPM: In the admin center, go to **Endpoint security** > **Endpoint Privilege Management**, and select the **Policies** node.
