---
# required metadata

title: View hardware and software inventory for Windows PCs 
titleSuffix: Microsoft Intune
description: How to view hardware and software information about Windows desktops that you manage as PCs with the Intune software client.
keywords:
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 06/26/2019
ms.topic: archived
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: medium
ms.technology:
ms.assetid: 3c10f4c9-520b-4864-92fc-a45a9f640ad4

# optional metadata

#audience:

ms.reviewer: owenyen
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-classic-keep
ms.collection: M365-identity-device-management
---

# View hardware and software inventory for Windows PCs

[!INCLUDE [classic-portal](../includes/classic-portal.md)]

> [!NOTE]
> The information in this topic applies only to Windows desktops that you are managing as PCs by using the Intune software client. If you want to view inventory for Windows PCs enrolled as mobile devices, see [View device details in Intune](../remote-actions/device-inventory.md).

Intune collects detailed information about the hardware and software for desktops you manage as PCs by using the Intune software client. Use the information in the following procedures to learn how to create:

- A report that lists information about the hardware capabilities of PCs you manage.

- A report that lists the software installed on each PC.

- How to refresh a PC's inventory to ensure that the data in the report is current.

## To display information about PCs you manage

1. In the [Microsoft Intune administration console](https://manage.microsoft.com/), choose **Reports** &gt; **Computer Inventory Reports**.

2. On the **Create New Report** page, accept the default values or customize them to filter the results that will be returned by the report. For example, you could select that only PCs that run Windows 8.1 are displayed in the report.

3. Choose **View Report** to open the **Computer Inventory Report** in a new window.

    You can sort the report by any of the columns, like **Name**, **Chassis Type** or **Manufacturer** by selecting each column heading.

## To display software installed on PCs you manage

1. In the [Microsoft Intune administration console](https://manage.microsoft.com/), choose **Reports** &gt; **Detected Software Reports**.

2. On the **Create New Report** page, accept the default values or customize them to filter the results that will be returned by the report. For example, you could select that only software published by Microsoft will be displayed in the report.

3. Choose **View Report** to open the **Detected Software Report** in a new window.

    You can sort the report by any of the columns, like **Name**, **Publisher** or **Category** by selecting each column heading. You can expand the updates in the list to show more detail (such as the PCs on which it is installed) by choosing the directional arrow next to the list item.

## To refresh computer inventory to ensure it is current

1. In the [Microsoft Intune administration console](https://manage.microsoft.com/), choose **Groups** &gt; **All Devices** (or another group that contains the PC for which you want to refresh inventory).

2. Select a PC, or press and hold **Ctrl** to select multiple PCs.

3. On the taskbar, choose **Remote Tasks** &gt; **Refresh Inventory**.

4. To view the task status, choose **Remote Tasks** in the bottom right corner of the page.

    The **Task Status** dialog box displays showing current remote tasks, task status, device name, and any reported errors, and provides a link to troubleshooting information.

## See also

[Common Windows PC management tasks with the Intune software client](common-windows-pc-management-tasks-with-the-microsoft-intune-computer-client.md)
