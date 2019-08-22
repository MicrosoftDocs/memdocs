---
title: Updates in Desktop Analytics
titleSuffix: Configuration Manager
description: Learn about security and feature updates in Desktop Analytics.
ms.date: 08/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 14ae894c-26fb-4fe3-b51d-e80700122df4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
---

# Updates in Desktop Analytics

> [!Note]  
> This information relates to a preview service which may be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here.  

In the Desktop Analytics portal, view the status of security and feature updates. Select these nodes in the Monitor group of the Desktop Analytics main menu. These nodes give you insights into the status of these updates in your environment.


## Security updates

To review the current status of security updates, select **Security updates** in the **Monitor** section of Desktop Analytics:

![Security updates node of Desktop Analytics](media/security-updates.png)

This view summarizes *security* updates for devices that are running Windows 10. Devices in the bar chart are categorized by the following labels:

#### Latest

Devices are running the latest security update for that version and channel.

#### Latest-1

Devices are running a security update one version older than the latest available update on that channel.

#### Older

Devices are running a security update older than Latest-1.

#### Not measured

Desktop Analytics hasn't assessed the device. This state includes devices running Windows 7, Windows 8.1, or Windows 10 devices registered for the Windows Insider Program.  

If a Windows 10 device is *not authenticated* with a Microsoft account, Windows doesn't report this data. This authentication is typically completed as part of the Windows Setup out-of-box-experience (OOBE).<!-- 5148153 -->


## Feature updates

To review the current status of feature updates, select **Feature updates** in the **Monitor** section of Desktop Analytics:

![Feature updates node of Desktop Analytics](media/feature-updates.png)

This view summarizes *feature* updates for devices that are running Windows 10.

For more information on service periods, see [Windows lifecycle fact sheet](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet).  

Devices in the bar chart are categorized by the following labels:

#### In service

Devices are running the latest feature update for that version and channel.  

#### Near end of service

Devices are running a feature update that's within 90 days of reaching end of service.

#### End of service

Devices are running a feature update that's past the end of service date. For details about end of service dates, see [Windows lifecycle fact sheet](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet).

#### Not measured

Desktop Analytics hasn't assessed the device. This state includes devices running Windows 7, Windows 8.1, or Windows 10 devices registered for the Windows Insider Program.

If a Windows 10 device is *not authenticated* with a Microsoft account, Windows doesn't report this data. This authentication is typically completed as part of the Windows Setup out-of-box-experience (OOBE).<!-- 5148153 -->


## Next steps

- [Learn about Desktop Analytics assets](/sccm/desktop-analytics/about-assets): devices, drivers, and apps  

- [Learn about deployment plans](/sccm/desktop-analytics/about-deployment-plans)  
