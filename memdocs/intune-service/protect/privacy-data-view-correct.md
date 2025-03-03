---
# required metadata

title: View and correct personal data collected by Intune
titleSuffix: Microsoft Intune
description: Learn how to view and correct personal data that's been collected by Intune.
keywords:
author: Smritib17
ms.author: smbhardwaj
manager: dougeby
ms.date: 04/08/2022
ms.topic: article
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.assetid: 1ba77bc7-505e-4eca-a49e-dcdaa75d0043

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: angerobe
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
- privacy
- sub-data-privacy
---

# View and correct personal data

Based on their access permissions, Intune admins can view some personal data that's been collected by Intune but can't change that data. Only end users can change their device's personal data that has been collected by Intune.

[!INCLUDE [GDPR-related guidance](../includes/gdpr-dsr-and-stp-note.md)]

## View personal data

Admins can see end user personal information in various Nodes of the Intune UI in the Microsoft Intune admin center. The following articles explain what information admins do and don't have access to:

- [See device details](../remote-actions/device-inventory.md) in Intune explains how you can review details about an end user's device.
- [Monitor app information and assignments](../apps/apps-monitor.md) explains how to see details about apps installed on an end user's device.
- The [What information can my company see when I enroll my device? article](../user-help/what-info-can-your-company-see-when-you-enroll-your-device-in-intune.md) gives end users a list of data that their company can and can't see. It's best to clearly tell your users what kind of data you're collecting and why you're collecting it. This article can be the first step in that transparency.

### Who can view the data?

Microsoft uses strict controls to govern access to customer data, granting the lowest level of access required to complete key tasks and revoking access when it's no longer needed.

You can secure and control access to end user personal data by using role-based administration control (RBAC). For more information, see [RBAC with Microsoft Intune](../fundamentals/role-based-access-control.md).

You can learn more about Microsoft data practices by reading the Online Services Terms and [Microsoft Online Services Privacy Statement](https://go.microsoft.com/fwlink/p/?linkid=131004&clcid=0x409). 

## Correct end user personal data

Admins can't update device or app specific information. If an end user wants to correct any personal data (like the device name), they must do so directly on their device. Such changes are synchronized the next time they connect to Intune.


## Next steps

Find out how to [audit, export, or delete](privacy-data-audit-export-delete.md) personal data in Intune.