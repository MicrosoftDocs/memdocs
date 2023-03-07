---
author: frankroj
ms.author: frankroj
manager: aaroncz
ms.technology: itpro-deploy
ms.prod: windows-client
ms.topic: include
ms.date: 02/23/2023
ms.localizationpriority: medium
---

<!-- This file is shared by the assign-autopilot-device-to-user-via-csv.md articles. Headings are driven by article context. -->

Instead of manually assigning a user to an Autopilot device in the Autopilot device's properties, a user can be assigned to the Autopilot device when the device was initially imported into Autopilot as an Autopilot device. Assigning a user when the device is imported as an Autopilot device can be done by editing the hardware hash CSV file and adding the **Assigned User** column after the **Hardware Hash** column. The user's User Principal Name (UPN) should then be added as a value under the **Assigned User** column.

> [!IMPORTANT]
>
> Use a plain-text editor such as **Notepad** to edit the CSV file. Don't use Microsoft Excel. Editing the CSV file in Excel won't generate a proper usable file for importing into Intune.

For more information on editing the CSV file to add an assigned user to the Autopilot device, see the following article:

[Manually register devices with Windows Autopilot: Ensure that the CSV file meets requirements](/mem/autopilot/add-devices#ensure-that-the-csv-file-meets-requirements)