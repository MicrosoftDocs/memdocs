---
# required metadata
title: Windows 365 Frontline Cloud PCs and Windows Update
titleSuffix:
description: Learn suggested Windows Update configurations for Windows 365 Frontline Cloud PCs.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 02/28/2024
ms.topic: how-to
ms.service: windows-365
ms.subservice: windows-365-enterprise
ms.localizationpriority: high
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

Windows 365 Frontline Cloud PCs rely on active hours Windows Update policies to make sure that Cloud PCs don't reboot for Windows Update during active usage. The following table lists  recommended update configurations for Frontline Cloud PCs. Make sure to use the [Filter function](create-filter.md#create-a-filter-for-all-cloud-pcs) to target the policies only to your Frontline Cloud PCs.

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
| Change notification update level | Turn off all notifications, including restart warnings |
| Deadline for feature updates | Default (Not configured) |
| Deadline for quality updates | Default (Not configured) |
| Grace Period | 2 |
| Auto-restart before deadline | No |
| [Active hours start](/windows/client-management/mdm/policy-csp-update) | Defined by IT administrator |
| [Active hours end](/windows/client-management/mdm/policy-csp-update) | Defined by IT administrator |
| Active hours max range | Defined by IT administrator |

These settings are important to make sure that users aren't disrupted by a Windows Update during their work hours.

## Automatic sync updates for Cloud PCs that haven't been turned on for seven days

The Windows 365 Service automatically powers on a Windows 365 Frontline Cloud PC if it hasn't been used and powered in the previous seven days. When the Windows 365 Frontline Cloud PC is turned on, the Windows 365 Service:

- Syncs the Cloud PC with the Windows Update service.
- Performs the Windows Update process honoring the Windows Update policy configurations set in Intune.
- Keeps the Cloud PC powered on for two hours to make sure that the Windows Update installation can complete.
- Checks for any pending reboots. If there are, the Cloud PC automatically reboots to complete any Windows Update before turning off.

This process lets the user seamlessly start using the Windows 365 Frontline Cloud PC the next time they sign in.

<!-- ########################## --> 
## Next steps

[Learn more about Windows Updates](/windows/deployment/update/get-started-updates-channels-tools).

[Windows Update policies you should set and why (blog)](https://techcommunity.microsoft.com/t5/windows-it-pro-blog/the-windows-update-policies-you-should-set-and-why/ba-p/3270914).
