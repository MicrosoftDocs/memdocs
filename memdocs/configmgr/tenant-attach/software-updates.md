---
title: Software updates in the admin center
description: Software updates for Configuration Manager devices from the admin center
ms.date: 06/07/2022
ms.prod: configuration-manager
ms.technology: configmgr-core
author: banreet
ms.author: banreetkaur
ms.manager: apoorvseth
ms.topic: conceptual
ms.localizationpriority: high
---
# Tenant attach: Software updates in the admin center
<!--13035723-->
*Applies to: Configuration Manager (current branch)*

The **Software updates** page in the admin center displays the status of software updates status for devices. You can review updates that have successfully installed, failed, or that are assigned but not yet installed. Using the timestamp for the update status assists with troubleshooting.

## Software updates page overview

Each tenant attached device lists its applicable updates and the status of each update on the **Software updates** page. The **Software updates** page is populated with data from Configuration Manager software update scans.

:::image type="content" source="./media/13035723-software-updates-page.png" alt-text="This screenshot displays software updates page for a device." lightbox="media/13035723-software-updates-page.png":::

## Prerequisites

- All of the prerequisites for [Tenant attach: ConfigMgr client details](client-details.md).
- A minimum of Configuration Manager version 2111 with [update rollup KB12896009](../hotfix/2111/12896009.md) installed on all sites in the hierarchy.


## Display the Software updates page

To display the **Software updates** page for a device, use the following steps:

1. In a browser, navigate to [https://endpoint.microsoft.com](https://endpoint.microsoft.com).
1. Select **Devices** then **All Devices**.
1. Select a device that is synced from Configuration Manager via [tenant attach](device-sync-actions.md).
1. Select **Software updates**.

## Update details

Selecting an update from the **Software updates** page opens the details pane for the update. The details pane lists the title of the update along with its description, classification, product category, and link to technical information about the specific update. The pane also includes the status and the status time for the selected update on the selected device.

:::image type="content" source="./media/13035723-software-updates-details.png" alt-text=" Screenshot displaying the details pane for an update." lightbox="media/13035723-software-updates-details.png":::

### Software updates page options

**Searching:** Searching is enabled for every category except for **Status time**. You can search for a string of words, a single word, or a partial word. For instance, searching for the string `compliant` would display results that contain the string `compliant` which would include `non-compliant`.

:::image type="content" source="./media/13035723-software-updates-filter.png" alt-text="This screenshot shows searching a feature on software updates page." lightbox="media/13035723-software-updates-filter.png":::

**Sorting:** You can sort by any column. The default view is sorted based on the **Status time**.

**Refresh:** You can refresh to display the latest information from the on-premises server at any time.

**Paging & Caching:** Paging is fully implemented with each page having a maximum of 25 software update entries. Each time you select **Next**, the data will be retrieved from the on-premises server. Once the data is retrieved the first time, it's cached for the browser to allow for quick page loading.

**Filters:** You can filter the available software updates based on their **Status** values, **Classification** values, or both values.

**Export:** Allows you to export all your available data, across all pages, while honoring any applied search teams and filters. The data is exported to a `.csv` file.

## Update status values

The following **Status** values are used in the **Software updates** page:

- **Unknown**: The status of the update isn't known or is currently unavailable.
- **Compliant**: The update is fully compliant and assigned.
- **Non-compliant**: The update isn't compliant (this message doesn't mean there was an error though), it just means it's either an older version or unapproved.
- **Conflict detected**: There's some sort of conflict with other software on the machine causing the update to fail.
- **Error**: The update failed with an error.
- **Partial compliance**: The update is installed and partially compliant. That is, part of the software update isn't compliant.
