---
title: Windows Autopilot Enrollment Status Page 
description: Gives an overview of the Enrollment Status Page capabilities, configuration
keywords: Autopilot Plug and Forget, Windows 10
ms.technology: windows
ms.prod: w10
ms.mktglfcycl: deploy
ms.sitesec: library
ms.pagetype: deploy
ms.localizationpriority: medium
audience: itpro
author: aczechowski
ms.author: aaroncz
ms.reviewer: jubaptis
manager: dougeby
ms.date: 12/16/2020
ms.collection: M365-modern-desktop
ms.topic: conceptual
---


# Windows Autopilot Enrollment Status Page

**Applies to**

- Windows 11
- Windows 10, version 1803 and later

When a user signs into a device for the first time, the Enrollment Status Page (ESP) displays the device's configuration progress. The ESP also makes sure the device is in the expected state before the user can access the desktop for the first time.

The ESP tracks the installation of applications, security policies, certificates, and network connections.

## ESP profiles

An administrator can deploy ESP profiles to a licensed Intune user and configure specific settings within the ESP profile. A few of these settings are:
- Force the installation of specified applications.
- Allow users to collect troubleshooting logs.
- Specify what a user can do if device setup fails.

For more information, see how to set up the [Enrollment Status Page in Intune](/intune/windows-enrollment-status).  
 
![Enrollment Status Page](images/enrollment-status-page.png)
 

## More information

For more information on configuring the Enrollment Status Page, see the [Microsoft Intune documentation](/intune/windows-enrollment-status).<br>
For details about the underlying implementation, see the [FirstSyncStatus details in the DMClient CSP documentation](/windows/client-management/mdm/dmclient-csp).<br>
For more information about blocking for app installation:
- [Blocking for app installation using Enrollment Status Page](/archive/blogs/mniehaus/blocking-for-app-installation-using-enrollment-status-page).
- [Support Tip: Office C2R installation is now tracked during ESP](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Support-Tip-Office-C2R-installation-is-now-tracked-during-ESP/ba-p/295514).
