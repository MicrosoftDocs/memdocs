---
title: Enable Local Windows Autopilot reset in Intune
description: Enable Local Windows Autopilot reset in Intune.
ms.prod: windows-client
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 03/14/2023
ms.topic: tutorial
ms.collection: 
  - tier1
  - highpri
ms.technology: itpro-deploy
---

# Enable local Windows Autopilot reset


## Enable local Windows Autopilot reset in Intune

To create a configuration profile that enables local Windows Autopilot reset, follow the below steps:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

1. In the **Home** screen, select **Devices** in the left pane.

1. In the **Devices | Overview** screen, under **Policy**, select **Configuration Profiles**.

1. In the **Devices | Configuration profiles** screen, make sure **Profiles** is selected at the top, and then select **Create profile**.

1. In the **Create profile** window that opens:

   1. Under **Platform**, select **Windows 10 and later**.

   1. Under **Profile type**, select **Templates**.

   1. When the templates appear, under **Template name**, select **Device restrictions**. If **Device restrictions** is not visible, scroll through the **Template name** list until **Device restrictions** is visible. The list is in alphabetical order.

   1. Select **Create** to close the **Create profile** window.

1. The **Create profile** screen will open. In the **Basics** page:

   1. Next to **Name**, enter a name for the domain join profile.

   1. Next to **Description**, enter a description for the domain join profile.

   1. Select **Next**.

1. In the **Configuration settings** page:

   1. Select **General** to expand it.

   1. Under **General**, scroll down to **Autopilot Reset**.

   1. Next to **Autopilot Reset**, select **Allow**.

   1. Select **Next**.

1. In the **Assignments** page:

   1. Under **Included groups**, choose **Add groups**.

      > [!NOTE]
      >
      > Make sure to add the correct device groups under **Included groups** and not under **Excluded groups**. Accidentally adding the desired device groups under **Excluded groups** will result in those devices being excluded and they won't receive the Autopilot profile.

   1. In the **Select groups to include** window that opens, select the groups that the configuration profile should be assigned to. This device group(s) is normally the device group(s) created in the step [Create device group](autopilot-reset-device-group.md). Once done, select **Select**.

   1. Under **Included groups** > **Groups**, ensure the correct group(s) are selected, and then select **Next**.

1. In the **Applicability Rules** page, select **Next**. For the purpose of this tutorial, applicability rules is being skipped. However if applicability rules are needed, do so at this screen. For more information about scope tags, see [Applicability rules](/mem/intune/configuration/device-profile-create#applicability-rules).

1. In the **Review + Create** page, review and verify that all of the settings are set as desired, and then choose **Create** to create the domain join profile.

## More information

For more information on Windows Autopilot Reset, see the following article(s):

- [Windows Autopilot Reset](/mem/autopilot/windows-autopilot-reset)
