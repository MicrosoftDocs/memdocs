---
title: Reports for Windows quality updates policies
description: Learn about the reports available for Windows quality updates policies in Microsoft Intune.
ms.date: 03/04/2025
ms.topic: how-to
ms.reviewer: zadvor
---

# Windows update distribution report

The Windows update distribution report in Intune provide a summarized report to show the number of devices that are on each quality update level and the percentage coverage for each update across devices managed by Intune (including co-managed devices).

The report provides a drill down for each quality update that aggregates devices based on Windows feature version and the update statuses. The admins can get the list of devices that aggregate to the numbers shown in the previous two reports, which they can export and use for troubleshooting and analysis.

The report includes Intune managed and co-managed devices, and is based on the OS version updated at every device check-in. The report can slice the data based on device scope tags.

>[!NOTE]
> The Windows update distribution report can be used if you are using Update Rings, or not using any update policies in Intune.

The Windows update distribution report comprises three distinct organizational reports that function sequentially to provide insights on devices and their corresponding Windows update versions. To access this feature, navigate to **Reports** > **Windows Updates** > **Reports tab** > **Windows Update Distribution Report**.

The Windows update distribution report includes three nested reports:

- Windows quality update distribution report
- Windows quality update distribution per feature version report
- Windows quality update device version report


Select a tab to learn more about each report. 

# [**QU distribution**](#tab/distribution)

The report displays the distribution of devices against different Quality Updates (QUs) for the selected scope. It shows the counts of devices corresponding to the displayed QUs.\
Select one or more scope tags from the drop-down list to generate the report. The drop-down list shows all the scope tags the user has access to, based on the user's assigned scope tags.

:::image type="content" source="./images/reports/windows-quality-updates-page1.png" alt-text="Screen capture of the Windows quality update distribution report." lightbox="./images/reports/windows-quality-updates-page1.png":::

The report shows the number of devices under each QU level corresponding to the current month and the last 3 months from the day of reporting. The top rows typically represent the last three months, followed by other device data distributions.

**Column details**:

- **Update**: Monthly quality update version. The update format corresponds to YYYY-MM-UpdateType. For example, 2024-02-B.
  - **Older releases**: All windows devices running valid feature version (non-preview/insider) and running older than 3 months of quality update level are combined into a single entity shown as *Older releases*.
  - **Windows insider or other releases**: All those devices whose OS version does not align with the Windows generally available feature release version and not on documented QU level, are combined under *Windows insider or other releases*.
- **Update Type**: Monthly quality update type. For more information, go to [Windows monthly update explained](https://techcommunity.microsoft.com/t5/windows-it-pro-blog/windows-monthly-updates-explained/ba-p/3773544)
  - B: Security Updates (released on patch Tuesday)
  - D: Non-Security Updates (released on 4th week of month)
  - OOB: Out of band updates
- **Release Date**: Release date of the monthly quality update.
- **Devices on this update**: Number of devices where the target quality update is installed.
- **% of all devices**: Number of devices running a particular quality update represented in percentage of total managed devices in Intune.

All QUs from this page are hyperlinked:
- When you select one of the current or last 3 months quality update (B, D or OOB), the *Windows quality update distribution per feature version* report is displayed.
- When you select **Older releases**, the *Windows quality update device version* report is displayed with a list of devices that are on an older quality update level excluding insider builds and unknown builds.
- When you select **Windows insider or other releases**, the  *Windows quality update device version* report is displayed with a list of devices whose feature version is insider release, or the quality update of the device cannot be mapped to documented quality update version in Windows release information.

# [**QU distribution per feature version**](#tab/feature-version)

The report provides the distribution of devices against Windows feature releases. The distribution of devices that are eligible to receive the selected quality update shown based on the Windows feature versions that are generally available. The report aids IT administrators in making informed decisions for devices and managing devices that need attention.

:::image type="content" source="./images/reports/windows-quality-updates-page2.png" alt-text="Screen capture of the Windows quality update distribution per feature version." lightbox="./images/reports/windows-quality-updates-page2.png":::

The stacked chart displays the counts of devices that are up to date, those that need updates, and those for which the chosen quality update does not apply. Together, these counts make up the total Windows devices that Intune manages, including co-managed devices.

The table lists each supported feature version that the selected quality update affects.

Select **Columns** at the top of the table to toggle the visibility of columns, including the **Devices on this update** column, which is hidden by default. You can sort the data by the **Windows version** and **Build number** columns.

**Column details**:

- **Windows version**: Shows the Windows feature version.
- **Total devices**: Total managed devices corresponding to the Windows feature version.
- **Build Number**: Build number of the windows feature version. Devices running supported Windows feature versions that the selected quality update does not cover are marked as **Not applicable**. Devices running unsupported Windows feature versions, insider versions, or those with an unknown OS version, are grouped under one line item and marked as **Not applicable**.
- **Devices on this update or later**: Number of devices where the target quality update or later is installed.
- **Devices on this update**: Number of devices where the target quality update is installed.
- **Devices need update**: Number of devices that are applicable for the update but do not currently have it installed.
KB article: External link to target quality update's KB Article for the corresponding Windows feature version.

When you select any device count, the *Windows quality update device version* report is displayed.

# [**QU device version**](#tab/device-version)

The report presents a list of devices based on the selections from the previous 2 reports. The  criteria that you selected in the previous reports are displayed at the top of the page.\
The report offers sortable columns and search options, along with an export feature allowing high volume data to be downloaded in CSV format.

:::image type="content" source="./images/reports/windows-quality-updates-page3.png" alt-text="Screen capture of the Windows quality update device version." lightbox="./images/reports/windows-quality-updates-page3.png":::

**Column details**:

- **Device Name**: The name of the device.
- **Intune Device Id**: Intune device identifier.
- **Entra Device Id**: Microsoft Entra identifier for device.
- **Primary UPN**: Intune user identifier (email).
- **OS version**: Operating System (OS) version build number. The OS version corresponds to the Windows feature Version (For example, Windows 11 24H2) and the quality Update level (For example, 2024-08 B).
- **Windows feature version**: Windows feature version.
- **Windows quality version**: Windows quality update.
- **Managed by**: Management agent.
- **Last check-in**: Device last check-in date time

The search bar enables the search for a specific device or UPN. Select a device from the list to view the device's details.

All these reports are cached, and have an expiry time of three days, after which you must generate a new report. Select **Generate Again** to get fresh data.

