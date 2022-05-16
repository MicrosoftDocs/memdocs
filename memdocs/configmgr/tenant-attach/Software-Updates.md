---
title: Software Updates in the admin center
titleSuffix: Intune
description: Release notes for ConfigMgr Software Updates in the Microsoft Endpoint Manager admin center
ms.date: 05/12/2022
ms.service: microsoft-intune
author: banreet
ms.author: banreetkaur
ms.manager: apoorvseth
ms.topic : include
---
# <a name="SoftwareUpdates_releasenotes"></a>Software Updates in the admin center


Software updates page displays the status for software updates on a device. You can review updates that have successfully installed, failed, and are assigned but not yet installed. Using the timestamp for the update status assists with troubleshooting.

You can select Devices, followed by All Devices to open Device Explorer (DEX). You can then view the software updates for a device that is synced from Configuration Manager via tenant attach.

:::image type="content" source="/media/Softwareupdates_releasenotes_1.png" alt-text="This screenshot displays All devices page. Select any tenant attached device from here.":::

## Overview of Software Updates Page

For any tenant attached device the software updates page will look as follows:

:::image type="content" source="/media/Softwareupdates_releasenotes_2.png" alt-text="This screenshot displays software updates page for a device.":::

### Features available on Software Updates page

**Searching:** Searching is enabled for every category except for Status time. You can search by subwords and the complete words. For instance, searching "English" would yield all results, which have the word "English" or "English" + other words in them.

:::image type="content" source="/media/Softwareupdates_releasenotes_3.png" alt-text="This screenshot shows searching a feature on software updates page.":::

**Sorting:** You can sort by any category. The default view is sorted based on the Status time.

**Refresh:** You can refresh to see live updates from the on-prem server at any time.

**Paging & Caching:** Paging is fully implemented with each page having a maximum of 25 software update entries. Each time you click 'Next', the data will be pulled from the on-prem server. Once it's pulled the first time, it's cached on the browser and will therefore load immediately.

**Filters:** You can filter the available software updates based on their Status or their Classification values, or both.

**Status Messages:** The messages that can appear are:

1. **Unknown** - this status message means that the status of a certain update isn't known or is currently unavailable.
2. **Compliant** - this status message means that the update is fully compliant and assigned
3. **Non-compliant** - the update isn't compliant (this message doesn't mean there was an error though), it just means it's either an older version or unapproved
4. **Conflict detected** - this status message means that there's some sort of conflict with other software on the machine causing the update to fail
5. **Error** - this status message means that the update failed due to an error
6. **Partial compliance** - this status message means that the update is installed and partially compliant with where it should be (that is, part of the software isn't compliant)

**Export:** Exporting will allow you to export all your available data, across all pages, while honoring the search and filters applied (if any).  Click on 'Download’ button on the Export dialog box. The data will be exported in the form of a .csv file.

**Details of an update:** the details of an update can be found in the detail pane that opens on the right of the screen after clicking an update

:::image type="content" source="/media/Softwareupdates_releasenotes_4.png" alt-text="This screenshot displays the details of an update.":::
