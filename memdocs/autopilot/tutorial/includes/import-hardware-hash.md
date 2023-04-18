---
author: frankroj
ms.author: frankroj
manager: aaroncz
ms.technology: itpro-deploy
ms.prod: windows-client
ms.topic: include
ms.date: 04/14/2023
ms.localizationpriority: medium
---

<!-- This file is shared by the following articles:

register-autopilot-device.md
register-device.md

Headings are driven by article context. -->

Several of the above methods on obtaining the hardware hash when manually registering devices as Autopilot devices produces a CSV file that contains the hardware hash of the device. This CSV file with the hardware hash needs to be imported into Intune to register the device as an Autopilot device.

After the CSV file has been created, it can be imported into Intune via the following steps:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

1. In the **Home** screen, select **Devices** in the left pane.

1. In the **Devices | Overview** screen, under **By platform**, select **Windows**.

1. In the **Windows | Windows enrollment** screen, select **Windows enrollment**

1. Under **Windows Autopilot Deployment Program**, select **Devices**.

1. In the **Windows Autopilot devices** screen that opens, select **Import**.

   1. In the **Add Windows Autopilot devices** window that opens:

      1. Under **Specify the path to the list you want to import.**, select the blue file folder.

      1. Browse to the CSV file obtained using one of the above methods to obtain the hardware hash of a device.

      1. After selecting the CSV file, verify that the correct CSV file is selected under **Specify the path to the list you want to import.**, and then select **Import** to close the **Add Windows Autopilot devices** window. Importing can take several minutes.

   1. After the import is complete, select **Sync**.

      A message displays saying that the sync is in progress. The sync process might take a few minutes to complete, depending on how many devices are being synchronized.

      > [!NOTE]
      >
      > If another sync is attempted within 10 minutes after initiating a sync, an error will be displayed. Syncs can only occur once every 10 minutes. To attempt a sync again, wait at least 10 minutes before trying again.

   1. Select **Refresh** to refresh the view. The newly imported devices should display within a few minutes. If the devices aren't yet displayed, wait a few minutes, and then select **Refresh** again.
