---
# required metadata
title: Windows 365 Frontline Cloud PCs and Windows Update
titleSuffix:
description: Learn suggested Windows Update configurations for Windows 365 Frontline Cloud PCs.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 04/06/2023
ms.topic: how-to
ms.service: windows-365
ms.subservice: 
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: gkomatsu
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection:
- M365-identity-device-management
- tier2
---

# Configure Windows Update for Windows 365 Frontline Cloud PCs

Windows 365 Frontline Cloud PCs rely on active hours Windows Update policies to make sure that Cloud PCs don't reboot for Windows Update during active usage. The following table lists  recommended update configurations for Frontline Cloud PCs. Make sure to use the Filter function to target the policies only to your Frontline Cloud PCs.

| Windows Update policy setting | Windows 365 Frontline recommendation |
| --- | --- |
| Microsoft product updates | Allow |
| Windows drivers | Allow |
| Quality update deferral period | 9 |
| Feature update deferral period | 0 |
| Upgrade Windows 10 to latest Windows 11 release | No |
| Set feature update uninstall period | 30 days |
| Servicing channel | General availability |
| Automatic update behavior | Auto install and restart at maintenance time\* |
| Restart checks | Allow |
| Option to pause updates | Disable |
| Option to check for Windows Updates | Default |
| Change notification update level | Turn off all notifications, including restart warnings\* |
| Deadline for feature updates | Default (Not configured) |
| Deadlien for quality updates | Default (Not configured) |
| Grace Period | 2 |
| Auto-restart before deadline | No |
| [Active hours start](/windows/client-management/mdm/policy-csp-update) | Defined by IT administrator |
| [Active hours end](/windows/client-management/mdm/policy-csp-update) | Defined by IT administrator |
| Active hours max range | Defined by IT administrator |

\* These settings are most important to make sure that users are not disrupted by a Windows Update during their work hours.

<!-- ########################## -->
## Next steps

[Learn more about Windows Updates](/windows/deployment/update/get-started-updates-channels-tools).
