---
title: Windows Autopilot device preparation reporting and monitoring
description: Reporting and monitoring in Windows Autopilot device preparation.
ms.service: windows-client
ms.subservice: itpro-deploy
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 05/31/2024
ms.topic: article
ms.collection:
  - M365-modern-desktop
  - m365initiative-coredeploy
  - highpri
  - tier1
  - essentials-overview
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
---

# Windows Autopilot device preparation reporting and monitoring

Out of the box reporting and monitoring with near real-time status of deployments, including applications and PowerShell scripts details and deployment time. This feature provides improved troubleshooting.

## Accessing reports and near real-time monitoring

To access Windows Autopilot device preparation reports and monitor deployments in near real-time:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. In the **Home** screen, select **Devices** in the left hand pane.

3. In the **Devices | Overview** screen, select **Monitor**.

4. In the **Devices | Monitor** screen, in the list of reports under **Report name**, select **Windows Autopilot device preparation deployments**.

5. The **Device enrollment - Autopilot deployments** screen opens. In the **Device enrollment - Autopilot deployments** screen, deployments of individual devices is shown. Each device has the following information:

    - **Device name** - the name given to the device during the deployment. Selecting this item goes to the deployment details for the device.
    - **Enrollment date** - the date and time that the device enrolled.
    - **Deployment status** - displays the current status of the deployment on the device. During deployment, the status will show **In progress**. Once deployment is complete, it will show the final outcome of the deployment as either **Success** or **Failed**.
    - **Phase** - shows the last reported phase that the deployment is at.
    - **Serial number** - the hardware serial number of the device.
    - **Deployment time** - the amount of time that the deployment took during the out of box experience (OOBE) to complete. If the deployment hasn't yet completed, it will show **In progress**.
    - **UPN** - the user that signed into the device during OOBE and that the Windows Autopilot device preparation policy was assigned to.

6. Select an individual device under **Device name**. The **Device deployment details** pane opens. The **Device deployment details** pane contains three sections:

   1. **Device** - contains information regarding the device, including:

      - **Device name** - the name given to the device during the deployment. Selecting this item goes to the device details in Intune.
      - **Deployment status** - displays the current status of the deployment on the device. During deployment, the status will show **In progress**. Once deployment is complete, it will show the final outcome of the deployment as either **Success** or **Failed**.
      - **Device ID** - the device ID of the device in Intune.
      - **Microsoft Entra device ID** - the device ID of the device in Microsoft Entra ID.
      - **Serial number** - the hardware serial number of the device.
      - **Deployment policy** - the Windows Autopilot device preparation policy the device received.
      - **Policy Version** - the version of the Windows Autopilot device preparation policy the device received. Each time a change is made and saved to the Windows Autopilot device preparation policy, the version number is incremented by one.
      - **OS version** - the version of Windows installed on the device during the deployment.

   2. **Apps** - reflects the last reported status for the applications being installed during the Windows Autopilot device preparation including the list of applications being installed. Statuses include:

      - **Installed** - application was successfully installed.
      - **In progress** - application is currently being installed.
      - **Skipped** - usually indicates that the application was selected in the Windows Autopilot device preparation policy, but wasn't assigned to the device group specified in the Windows Autopilot device preparation policy. It can also mean that the application isn't applicable to the device.
      - **Failed** - the application failed to install. Check logs for further details.

   3. **Scripts** - contains information regarding the PowerShell scripts being run during the Windows Autopilot device preparation including the list of scripts being run. Statuses include:

      - **Installed** - the PowerShell script successfully ran.
      - **In progress** - the PowerShell script is currently running.
      - **Skipped** - usually indicates that the PowerShell script was selected in the Windows Autopilot device preparation policy, but wasn't assigned to the device group specified in the Windows Autopilot device preparation policy.
      - **Failed** - the PowerShell script failed to run. Check logs for further details.
