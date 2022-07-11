---
title: Tenant attach - Device timeline
titleSuffix: Configuration Manager
description: View the timeline for Configuration Manager devices from the admin center.
ms.date: 01/25/2022
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-core
manager: dougeby
author: mestew
ms.author: mstewart
ms.localizationpriority: high
---

# <a name="bkmk_timeline"></a> Tenant attach: Device timeline in the admin center
<!--CM7141381, IN7552762 pubpreview Sept 8, 2020, GA 2201-->
*Applies to: Configuration Manager (current branch)*

Microsoft Endpoint Manager is an integrated solution for managing all of your devices. Microsoft brings together Configuration Manager and Intune into a single console called **Microsoft Endpoint Manager admin center**. When Configuration Manager synchronizes a device to Microsoft Endpoint Manager through tenant attach, you can see a timeline of events. This timeline shows past activity on the device that can help you troubleshoot problems.

## Prerequisites

The following items are needed to use the timeline from the admin center:

- All of the prerequisites for [Tenant attach: ConfigMgr client details](client-details.md#prerequisites).
- Enable Endpoint analytics data collection in Configuration Manager:
   1. In the Configuration Manager console, go to **Administration** > **Client Settings** > **Default Client Settings**.
   1. Right-click and select **Properties** then select the **Computer Agent** settings.
   1. Set **Enable Endpoint analytics data collection** to **Yes**.
      - Only events collected after the client receives this policy will be visible in the admin center. Events prior to receiving the policy won't be accessible.

## Permissions

The user account needs the following permissions:

- The **Read** permission for the device's **Collection** in Configuration Manager.
- The **Read Resource** permission under **Collection** in Configuration Manager.
- The **Notify Resource** permission under **Collection** in Configuration Manager. <!--7984188-->
- An [Intune role](../../intune/fundamentals/role-based-access-control.md) assigned to the user <!--7980141-->

## Generate events

Devices send events once a day to the admin center. Only events collected after the client receives the **Enable Endpoint analytics data collection** policy are visible in the admin center. Generate test events easily by installing an application or an update from Configuration Manager, or restart the device. Events are kept for 30 days. Use the [chart](#collected-events) to view events that are collected.

## Collected events

|Event name|Provider name|Event ID|
|---|---|---|
|Application Error|Application Error|1000|
|Application Hang|Application Hang|1002|
|Kernel Crash|Microsoft-Windows-WER-SystemErrorReporting|1001|
|Application Crash|Windows Error Reporting|1001|
|Windows Update Agent – Update Installation|Microsoft-Windows-WindowsUpdateClient|19|
|Unknown Shutdown|Boot|0|
|Initiated Shutdown|Boot|1074|
|Abnormal Shutdown|Boot|41|
|Boundary Group Change|Microsoft-ConfigMgr|20000|
|Application Deployment|Microsoft-ConfigMgr|20001|
|Configuration Manager – Update Installation|Microsoft-ConfigMgr|20002|
|Firmware version change|Microsoft-ConfigMgr|20003|
|Configuration Manager Reboot request|Microsoft-ConfigMgr|20005|
|Client repair|Microsoft-ConfigMgr|20006|
|State resync|Microsoft-ConfigMgr|20007|
|Inventory resync|Microsoft-ConfigMgr|20008|

## View the timeline

1. In a browser, navigate to [https://endpoint.microsoft.com](https://endpoint.microsoft.com).
1. Select **Devices** then **All Devices**.
1. Select a device that is synced from Configuration Manager via [tenant attach](device-sync-actions.md).
1. Select **Timeline**. By default, you're shown events from the last 24 hours.
   - Use the **Filter** button to change the **Time range**, **Event levels**, and **Provider name**.
   - If you select on an event, you'll see the detailed message for it.
   - Select **Sync** to fetch the recent data generated on client. The device sends events once a day to the admin center by default. <!--7984188-->
   - Select **Refresh** to reload the page and to see newly collected events.

   :::image type="content" source="./media/7141381-timeline.png" alt-text="Timeline of events for a device" lightbox="./media/7141381-timeline.png":::

## Known issues
<!--9114968, 9102454-->
You will receive a time out error if the following condition applies:

- You're opening **Timeline** for the very first time after restarting SMSExecutive on the service connection point's on-premises server. 

To work around the issue, reload the **Timeline** page.

## Next steps

[Troubleshoot the device timeline](troubleshoot-timeline.md)
