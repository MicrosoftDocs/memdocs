---
author: frankroj
ms.author: frankroj
manager: aaroncz
ms.subservice: itpro-deploy
ms.service: windows-client
ms.topic: include
ms.date: 06/11/2024
ms.localizationpriority: medium
---

<!-- This file is shared by the following articles:

pre-provisioning/azure-ad-join-autopilot-profile.md
pre-provisioning/hybrid-azure-ad-join-autopilot-profile.md
self-deploying/self-deploying-autopilot-profile.md
user-driven/azure-ad-join-autopilot-profile.md
user-driven/hybrid-azure-ad-join-autopilot-profile.md

Headings are driven by article context. -->

9. Once the options in the **Out-of-box experience (OOBE)** page are configured as desired, select **Next**.

10. In the **Assignments** page:

    1. Under **Included groups**, choose **Add groups**.

      > [!NOTE]
      >
       Make sure to add the correct device groups under **Included groups** and not under **Excluded groups**. Accidentally adding the desired device groups under **Excluded groups** prevents devices in those device groups from receiving the Autopilot profile.

    1. In the **Select groups to include** window that opens, select the groups that the Autopilot profile should be assigned to. These device groups are normally the device groups created in the previous **Create device group** step. Once done, select **Select**.

    1. Under **Included groups** > **Groups**, ensure the correct groups are selected, and then select **Next**.

11. In the **Review + Create** page, review and verify that all of the settings are set as desired, and then choose **Create** to create the Autopilot profile.
