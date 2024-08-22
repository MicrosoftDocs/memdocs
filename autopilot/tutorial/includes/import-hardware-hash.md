---
author: frankroj
ms.author: frankroj
manager: aaroncz
ms.subservice: itpro-autopilot
ms.service: windows-client
ms.topic: include
ms.date: 06/28/2024
ms.localizationpriority: medium
---

<!-- This file is shared by the following articles:

includes/register-autopilot-device.md
existing-devices/register-device.md

Headings are driven by article context. -->

Several of the methods in the previous section on obtaining the hardware hash when manually registering devices as Autopilot devices produces a CSV file that contains the hardware hash of the device. This CSV file with the hardware hash needs to be imported into Intune to register the device as an Autopilot device.

After the CSV file is created, it can be imported into Intune via the following steps:

1. Sign into the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

1. In the **Home** screen, select **Devices** in the left hand pane.

1. In the **Devices | Overview** screen, under **By platform**, select **Windows**.

1. In the **Windows | Windows devices** screen, under **Device onboarding**, select **Enrollment**.

1. In the **Windows | Windows enrollment** screen, under **Windows Autopilot**, select **Devices**.

1. In the **Windows Autopilot devices** screen that opens, select **Import**.

   1. In the **Add Autopilot devices** window that opens:

      1. Under **Specify the path to the list you want to import.**, select the blue file folder.

      1. Browse to the CSV file obtained using one of the above methods to obtain the hardware hash of a device.

      1. After selecting the CSV file, verify that the correct CSV file is selected under **Specify the path to the list you want to import.**, and then select **Import**. Selecting **Import** closes the **Add Autopilot devices** window. Importing can take several minutes.

   1. After the import is complete, select **Sync**.

      A message displays saying that the sync is in progress. The sync process might take a few minutes to complete, depending on how many devices are being synchronized.

      > [!NOTE]
      >
      > If another sync is attempted within 10 minutes after initiating a sync, an error will be displayed. Syncs can only occur once every 10 minutes. To attempt a sync again, wait at least 10 minutes before trying again.

   1. Select **Refresh** to refresh the view. The newly imported devices should display within a few minutes. If the devices aren't yet displayed, wait a few minutes, and then select **Refresh** again.
