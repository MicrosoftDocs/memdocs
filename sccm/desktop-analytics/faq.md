---
title: FAQ for Desktop Analytics
titleSuffix: Configuration Manager
description: Frequently asked questions for Desktop Analytics.
ms.date: 06/10/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: e0db3311-2303-4013-a906-76b408172d3c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
---

# Desktop Analytics FAQ

> [!Note]  
> This information relates to a preview service which may be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here.  

## Windows upgrade

### Can I upgrade Windows and change architecture?

Desktop Analytics is designed to best support in-place upgrades. In-place upgrades don't support migrations from 32-bit to 64-bit architecture. If you need to migrate computers in this scenario, use the refresh scenario. Desktop Analytics insights are still valuable in this scenario, but you can ignore upgrade-specific guidance.

For more information, see [Refresh an existing computer with a new version of Windows](/sccm/osd/deploy-use/refresh-an-existing-computer-with-a-new-version-of-windows).

### Can I change from BIOS to UEFI when upgrading Windows?

Yes. For more information, see [Convert from BIOS to UEFI during an in-place upgrade](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion#convert-from-bios-to-uefi-during-an-in-place-upgrade).

### Can I use Desktop Analytics with Windows 10 LTSC?

While you can use Desktop Analytics to assist with updating devices from Windows 10 Long-Term Servicing Channel (LTSC) to Windows 10 Semi-Annual Channel, Desktop Analytics doesn't support updates to Windows 10 LTSC. This channel of Windows 10 isn't intended for broad use, and doesn't receive feature updates, so it's not a supported target with Desktop Analytics. For more information, see [Windows as a service overview](https://docs.microsoft.com/windows/deployment/update/waas-overview#long-term-servicing-channel).

### Can I reduce the amount of time it takes for data to refresh in my Desktop Analytics portal?

There are two types of data in the Desktop Analytics portal: Administrator data and diagnostic data. To refresh administrator data on-demand, open the data currency flyout and select **Apply changes**. This action immediately triggers a one-time refresh of any pending administrator changes in your workspaces. The changes propagate and are generally available within 15-60 minutes. The timing depends on the size of your workspace and the scope of pending changes. You can request an on-demand data refresh up to six times within a 24-hour period. 

All data is updated automatically once daily, even if you don't request an on-demand data refresh. There's no way to trigger an on-demand refresh of diagnostic data. For more information about the different types of data in Desktop Analytics, see [Data latency](/sccm/desktop-analytics/troubleshooting#data-latency).


## Privacy

### Can Desktop Analytics be used without a direct client connection to the Microsoft Data Management Service?

No, the entire service is powered by Windows diagnostic data, which requires that devices have this direct connectivity.

### Can I choose the data center location?

For Azure Log Analytics: Yes, when you set up Desktop Analytics and create the Log Analytics workspace.

For the Microsoft Data Management Service and Analytics Azure Storage: No, these two services are hosted in the United States.

### Where is my organization's data stored?

Windows diagnostic data from your computers is encrypted, sent to, and processed at Microsoft-managed secure data centers located in the United States. Our analysis of the Desktop Analytics-related data is then provided to you through the Desktop Analytics solution in the Azure portal. Desktop Analytics is supported in all Azure regions. Selecting an international Azure region doesn't prevent diagnostic data from being sent to and processed in Microsoft's secure data centers in the US.
