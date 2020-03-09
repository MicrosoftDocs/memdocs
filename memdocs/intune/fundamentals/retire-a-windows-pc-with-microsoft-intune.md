---
# required metadata

title: Retire a Windows PC 
titleSuffix: Microsoft Intune
description: How to retire an Intune-managed Windows PC.
keywords:
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 01/01/2018
ms.topic: archived
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: medium
ms.technology:
ms.assetid: 5c916182-d99c-44c5-a779-3f596f261c40

# optional metadata

#audience:

ms.reviewer: owenyen
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-classic-keep
ms.collection: M365-identity-device-management
---

# Retire a Windows PC

[!INCLUDE [classic-portal](../includes/classic-portal.md)]

Use the following steps to retire desktops that you are managing as PCs by running the Intune software client on them. When you retire a PC, it removes it from Intune management. You cannot wipe a PC from Intune to set it back to its original factory settings.

1. In the [Microsoft Intune administration console](https://manage.microsoft.com/), choose **Groups** &gt; **All Devices** (or another group that contains the PC you want to retire).

2. Select the devices you want to retire, and then choose **Retire/Wipe**.

To re-enroll a PC into Intune, reinstall the software client on the PC using guidance in [Install the Windows PC client with Microsoft Intune](install-the-windows-pc-client-with-microsoft-intune.md).

If a PC cannot connect to Intune, a message is displayed in the **Dashboard** workspace.

When you retire a PC:

- It is removed from the Intune management and inventory, and the license associated with the PC is made available for re-use. Retire/Wipe removes the Intune software client but does not remove apps or data from the PC. This retirement does not perform a full wipe on the PC.

- Its status no longer displays in the Intune console.

- Intune removes the software client from the PC. If the PC is not connected to the Intune service, the software client will be removed next time it connects.

- Microsoft Intune Endpoint Protection is removed from the PC. If the PC has another endpoint application installed and it is disabled, that application can be re-enabled after Microsoft Intune Endpoint Protection is removed to ensure that your PC are protected.

- Any policies are removed from the PC and the values that were set by the policy will be changed.

- The PC no longer receives software updates or malware definition updates from the Intune service.

- Depending on how they are configured, retired PC can continue to receive updates by using Windows Server Update Services, Windows Update, or Microsoft Update.

    > [!IMPORTANT]
    > If the client software was installed by using a Group Policy Object (GPO), you must remove the Group Policy Object (GPO) before you can remove the client software to prevent the software from being reinstalled.

    If the Endpoint Protection client fails to uninstall, read [Troubleshoot Endpoint Protection](/intune/troubleshoot-endpoint-protection-in-microsoft-intune) for more help.

## See also

[Common Windows PC management tasks with the Intune software client](common-windows-pc-management-tasks-with-the-microsoft-intune-computer-client.md)
