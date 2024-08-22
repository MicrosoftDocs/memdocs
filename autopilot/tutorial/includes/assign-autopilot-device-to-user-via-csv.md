---
author: frankroj
ms.author: frankroj
manager: aaroncz
ms.subservice: itpro-autopilot
ms.service: windows-client
ms.topic: include
ms.date: 06/19/2024
ms.localizationpriority: medium
---

<!-- This file is shared by the following articles:

pre-provisioning/azure-ad-join-assign-device-to-user.md
pre-provisioning/hybrid-azure-ad-join-assign-device-to-user.md
user-driven/azure-ad-join-assign-device-to-user.md
user-driven/hybrid-azure-ad-join-assign-device-to-user.md

Headings are driven by article context. -->

A user can be manually assigned to a Windows Autopilot device in the Windows Autopilot device's properties. However, a user can also be assigned to the Autopilot device when the device was initially imported into Autopilot as an Autopilot device. Assigning a user when the device is imported as an Autopilot device can be done by editing the hardware hash CSV file and adding the **Assigned User** column after the **Hardware Hash** column. The user's User Principal Name (UPN) should then be added as a value under the **Assigned User** column.

> [!IMPORTANT]
>
> Use a plain-text editor such as **Notepad** to edit the CSV file. Don't use Microsoft Excel. Editing the CSV file in Excel doesn't generate a proper usable file for importing into Intune.

For more information on editing the CSV file to add an assigned user to the Autopilot device, see [Manually register devices with Windows Autopilot: Ensure that the CSV file meets requirements](../../add-devices.md#ensure-that-the-csv-file-meets-requirements).
