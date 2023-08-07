---
# required metadata
title: Windows 365 Switch known issues
titleSuffix:
description: Learn about known issues with Windows 365 Switch, including workarounds and updated fixes.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 08/08/2023
ms.topic: troubleshooting
ms.service: windows-365
ms.subservice: 
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: elluthra
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection:
- M365-identity-device-management
- tier2
---

# Windows 365 Switch known issues

This page lists recent known issues with [Windows 365 Switch](windows-365-switch-overview.md).

## Support for only one Cloud PC

Currently, Windows 365 Switch only supports one Switch-enabled Cloud PC. The user is automatically signed into the first available Switch-supported Cloud PC from the list of Cloud PCs assigned to the user. The user can’t choose the Cloud PC that they want to sign in to.

## Limited gestures

Some gestures aren't supported in the Cloud PC, like three finger gestures to change app or four finger gesture to bring up the Task view and show the desktop. These gestures will instead get triggered on the physical device. Other than these all the usual Windows 11 gestures are supported.

## Bluetooth and hardware settings can't be managed from the Cloud PC

Cloud PCs lack hardware components like bluetooth adapters. Users can't change it from the Cloud PC Settings app or quick Settings. 

**Troubleshooting steps**:

Users must switch back to their physical device and change the settings in the Settings app.

## Reconnect button not working

If the **Reconnect** option in the disconnect message dialog is used, reconnecting might not work as expected or may result in an unusable Cloud PC session.

**Troubleshooting steps**:

Let the disconnect complete and then launch a new connection using Task view.

## Missing or extra buttons in a Cloud PC session

You might see extra buttons, or some buttons might be missing, in your Cloud PC session. For example, the Local Desktop button might not appear in Task view.

**Possible  cause:**

The user connected to their Cloud PC using another mode (like Windows 365 Boot or from the task bar) and then next connects using Windows 365 Switch, or vice versa.

**Troubleshooting steps:**

Restart the Cloud PC. 

<!-- ########################## -->
## Next steps

[Troubleshooting](troubleshooting.md)
