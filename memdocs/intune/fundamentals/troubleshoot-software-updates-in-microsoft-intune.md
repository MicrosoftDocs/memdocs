---
# required metadata

title: Troubleshoot software updates in Microsoft Intune - Azure | Microsoft Docs
description: Solve software update problems in Microsoft Intune.
keywords:
author: Brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/29/2019
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: medium
ms.technology:
ms.assetid: d17b70f4-17b4-4d89-88fd-70fa4f34fbea
ROBOTS: 

# optional metadata

#audience:
#ms.devlang:
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-classic
ms.collection: M365-identity-device-management
---

# Troubleshoot software updates in Microsoft Intune

Help solve software update problems in Microsoft Intune. To see a list of the error codes and descriptions, go to [Software update agent error codes in Microsoft Intune](../intune/protect/software-update-agent-error-codes.md).

## Windows 7 devices with many superseded updates stop reporting to Intune

Microsoft Intune clients may experience one or more of the following symptoms:

- Devices suddenly stop reporting to Intune.  
- Devices experience high CPU utilization.
- Applications install slowly when installed through Intune.
- The Microsoft Intune Center shows the following error: `An error occurred while updating your computer. Error found: Code 0x800705b4`.
- The Intune Admin Console > Groups > All Devices > status shows: `One or more agents that are installed on this computer have errors. The information for this computer may not be accurate or up-to-date.`

This problem can occur if superseded updates (updates are replaced by another update) haven't been declined for an extended period. During certain processes, such as installing an application, Windows checks all superseded updates in sequence so that the updates and their successors are correctly mapped. If the list of superseded updates gets too large, this checking task may cause high CPU utilization because of the processing load and time required. This issue primarily affects Windows 7 devices because of the large number of superseded updates that are available for Windows 7. Newer operating systems may not have as many available superseded updates, and may not be susceptible to this issue.

**Resolution**

1. Sign in to [Intune](https://go.microsoft.com/fwlink/?linkid=2090973).
2. Select **Software Updates**.
3. Decline all superseded updates that may apply to Windows 7 or to applications, such as Microsoft Office, that were installed on the affected clients.
4. Restart the affected clients.

If you're running Windows 7, be sure the following update is installed:[3050265 Windows Update Client for Windows 7: June 2015](https://support.microsoft.com/kb/3050265).

## Next steps

Get [support help from Microsoft](get-support.md), or use the [community forums](https://social.technet.microsoft.com/Forums/en-US/home?category=microsoftintune).