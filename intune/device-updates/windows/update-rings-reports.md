---
title: Use Windows Update for Business reports for Windows Updates in Microsoft Intune
description: Use Windows Update for Business reports to view data for Windows Updates you deploy with Intune.
ms.date: 03/04/2025
ms.topic: how-to
ms.reviewer: zadvor
---

# Reports for update rings policies

Intune offers integrated report views for the Windows update ring policies you deploy. These views display details about the update ring deployment and status. To access reports, in the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) go to **Devices** > **By platform** > **Windows** > **Manage updates** > **Windows updates** > **Update rings** tab > and select an update ring policy.  Intune displays details similar to the following for the selected policy:

:::image type="content" source="./images/update-rings/default-policy-view.png" alt-text="Screen capture of the default view for Update rings policy." lightbox="./images/update-rings/default-policy-view.png":::

On the policy page view:

- **Device and user check-in status**: The default report view for this policy. This default view includes a high-level bar chart that displays a count of devices reporting four status values for this policy, and a color bar that visually represents the percentage of devices reporting each status by color. This view displays the following four status results for the policy:
  - Succeeded
  - Error
  - Conflict
  - Not applicable

- **View report**: This button opens a more detailed report view for *Device and user check-in status*. The detailed report view includes a chart and color bar similar to that from the preceding high-level view, but reports one the additional status of **In progress**.

  This view also includes device specific details that include:
  - Device name
  - Logged in user
  - Check-in status
  - Last report modification time

  :::image type="content" source="./images/reports/report-view-details.png" alt-text="Screen capture that shows details available from the View report action.":::

  From this report view, you can select a device to drill in to view the list of the settings in the policy, and the status of the selected device for each of those settings. Additional drill-in is available by selecting a setting to open the *Setting details*. The *Setting details* display the name of the setting, the devices status (State) for that setting, and a list of profiles that manage the setting and that are assigned to the device. This is useful to help identify the source of a settings conflict.

- **Two additional report tiles**: You can select the tiles for the following reports to view additional details:

  - **Device assignment status**: This report shows all the devices that are targeted by the policy, including devices in a pending policy assignment state.

    For this report, you can select one or more status details you are interested in, and then select *Generate report* to update the view with only that information. In this following image, we have generated a report that displays only the devices that were successfully assigned this policy:

    :::image type="content" source="./images/reports/successful-assignment-view.png" alt-text="Image of the results of the Assignment status report.":::

    This report supports drilling in to view the list of settings, with subsequent drill-in as seen in for the full report view available from the *View report* button.

  - **Per setting status**: View the configuration status of each setting for this policy across all devices and users. This view present a simple view of each setting in the policy, and the count of assigned devices that have success, error, or conflict. This report view doesn't support drilling in for additional detail.
