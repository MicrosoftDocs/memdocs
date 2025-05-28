---
title: Windows Autopilot device preparation in automatic mode for Windows 365 - Step 6 of 6 - Monitor the deployment
description: How to - Windows Autopilot device preparation in automatic mode for Windows 365 - Step 6 of 6 - Monitor the deployment.
ms.service: windows-client
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: madakeva
manager: aaroncz
ms.date: 05/29/2025
ms.topic: tutorial
ms.collection:
  - tier1
  - highpri
ms.subservice: autopilot
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
---

# Windows Autopilot device preparation in automatic mode for Windows 365: Monitor the Windows Autopilot device preparation in automatic mode for Windows 365 deployment

Windows Autopilot device preparation in automatic mode for Windows 365 steps:

- Step 1: [Set up Windows automatic Intune enrollment](automatic-automatic-enrollment.md)
- Step 2: [Create an assigned device group](automatic-device-group.md)
- Step 3: [Assign applications and PowerShell scripts to device group](automatic-assign-apps-scripts.md)
- Step 4: [Create Windows Autopilot device preparation policy](automatic-autopilot-policy.md)
- Step 5: [Create a Cloud PC provisioning policy](automatic-cloud-pc-provisioning-policy.md)

> [!div class="checklist"]
>
> - **Step 6: Monitor the deployment**

For an overview of the Windows Autopilot device preparation in automatic mode for Windows 365 workflow, see [Windows Autopilot device preparation in automatic mode for Windows 365 overview](automatic-workflow.md#workflow).

## Monitor the deployment

With other Windows Autopilot and Windows Autopilot device preparation scenarios, deployments can be "viewed" on actual devices to see the deployment progress and result. However, with Windows Autopilot device preparation in automatic mode for Windows 365, the setup and deployment of the Cloud PC is "headless" and takes place in the background where it can't be viewed. Deployments can instead be monitored through the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) including [Windows Autopilot device preparation reporting and monitoring](../../reporting-monitoring.md).

### View status of the deployment

To view status of a Windows Autopilot device preparation in automatic mode for Windows 365 deployment:

1. Sign into the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

1. In the **Home** screen, select **Devices** in the left hand pane.

1. In the **Devices | Overview** screen, under **Device onboarding**, select **Windows 365**.

1. At the top of the **Devices | Windows 365** screen, select **All Cloud PCs**.

1. The status of each Cloud PC is displayed under the **Status** column in this page. The statuses include:

    - **Provisioning** - the Cloud PC is currently being provisioned and isn't ready for use yet.

    - **Provisioned** - the Cloud PC has been successfully provisioned and is ready to be used.

    - **Failed** - the Cloud PC failed to be provisioned successfully and can't be used due to the setting **Prevent users from connection to Cloud PC upon installation failure or timeout** option enabled in the Cloud PC provisioning policy. For more information, see [Create a Cloud PC provisioning policy for use with Windows Autopilot device preparation in automatic mode for Windows 365](automatic-cloud-pc-provisioning-policy.md#create-a-cloud-pc-provisioning-policy-for-use-with-windows-autopilot-device-preparation-in-automatic-mode-for-windows-365).

    - **Provisioned with warnings** - the Cloud PC failed to be provisioned successfully but can be used due to the setting **Prevent users from connection to Cloud PC upon installation failure or timeout** option enabled in the Cloud PC provisioning policy. For more information, see [Create a Cloud PC provisioning policy for use with Windows Autopilot device preparation in automatic mode for Windows 365](automatic-cloud-pc-provisioning-policy.md#create-a-cloud-pc-provisioning-policy-for-use-with-windows-autopilot-device-preparation-in-automatic-mode-for-windows-365).

    > [!TIP]
    >
    > The Cloud PCs can be filtered based on the different statuses by selecting the appropriate status above the table.

### View details of the deployment

To view the details of a Windows Autopilot device preparation in automatic mode for Windows 365 deployment beyond just status, use [Windows Autopilot device preparation reporting and monitoring](../../reporting-monitoring.md):

[!INCLUDE [Windows Autopilot device preparation reporting and monitoring](../../includes/reporting-monitoring.md)]
