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

1. Once the options in the **Out-of-box experience (OOBE)** page are configured as desired, select **Next**.

1. In the **Assignments** page:

   1. Under **Included groups**, choose **Add groups**.

      > [!NOTE]
      >
      > Make sure to add the correct device groups under **Included groups** and not under **Excluded groups**. Accidentally adding the desired device groups under **Excluded groups** will result in those devices being excluded and they won't receive the Autopilot profile.

   1. In the **Select groups to include** window that opens, select the groups that the Autopilot profile should be assigned to. This device group(s) is normally the device group(s) created in the step [Create device group](self-deploying-device-group.md). Once done, select **Select**.

   1. Under **Included groups** > **Groups**, ensure the correct group(s) are selected, and then select **Next**.

1. In the **Review + Create** page, review and verify that all of the settings are set as desired, and then choose **Create** to create the Autopilot profile.
