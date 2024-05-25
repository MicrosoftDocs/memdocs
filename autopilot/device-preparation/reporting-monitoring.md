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

5. The **Device enrollment - Autopilot deployments** screen opens. In the **Device enrollment - Autopilot deployments** screen, deployments of individual devices is shown. Select an individual device under **Device name** opens

6. The **Device deployment details** pane opens. The **Device deployment details** pane contains three sections:

   1. **Device** - Contains information regarding the device, including:

      1. **Device name** - the name given to the device during the deployment. Selecting this item goes to the device details in Intune.
      2. **Deployment status** - displays the current status of the deployment on the device including if the deployment was a **Success** or **Failed**.
      3. **Device ID** - the device ID of the device in Intune.
      4. **Microsoft Entra device ID** - the device ID of the device In Microsoft Entra ID.
      5. **Serial number** - the hardware serial number of the device.
      6. **Deployment policy** - the device preparation policy the device received.
      7. **Policy Version**
      8. **OS version** - the version of Windows installed on the device during the deployment.

   2. **Apps**

   3. **Scripts**
