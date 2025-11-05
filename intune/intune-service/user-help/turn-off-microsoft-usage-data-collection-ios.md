---
title: Share Company Portal usage data with Microsoft Intune
description: Learn how to turn off Microsoft data collection in Intune Company Portal for iOS to prevent usage and diagnostic data from automatically being shared with Intune.
ms.date: 02/04/2025
ms.reviewer: esmich
---

# Share Company Portal usage data with Microsoft

When turned on, the Company Portal usage data feature shares your in-app performance and usage data with Microsoft. Sharing your Company Portal usage data helps to improve the reliability and performance of Microsoft products like Intune.

You can turn this feature on or off from the Settings app. Your organization can't change your usage data preference, and doesn't have any control over the collection of your data.

If you turn off Company Portal usage data:

* All optional telemetry and diagnostic data that's normally collected and sent to Intune will stop being sent.
* Proactive troubleshooting will no longer be possible, so you'll need to manually upload your logs to Intune if you have a problem with the device.

The usage data setting doesn't control the data that's required to run the Intune service. That data will continue to be sent to Intune but doesn't contain any personal information.

## Edit usage data preferences
Change your usage data preferences to turn usage data collection on or off.

1. Open the **Settings** app.
2. Go to **Apps** and tap **Company Portal**.
3. Switch the **Usage Data** toggle to the off position (to stop usage and diagnostic data from being sent to Intune), or to the on position (to allow usage and diagnostic data to be sent to Intune).

## Enable or disable advanced logging

The **Enable Advanced Logging** setting is available in the Intune Company Portal app for iOS/iPadOS devices. Device users can able to enable or disable advanced logging on a device. By turning on advanced logging, detailed log reports will be sent to Microsoft to troubleshoot issues. By default, the **Enable Advanced Logging** setting will be off. Device users should keep this setting off unless otherwise instructed by their organization's IT admin.

To modify this setting on an iOS/iPadOS device:
1. Open the **Settings** app.
2. Find **Company Portal**.
3. Under **Diagnostics**, turn on or off the **Enable Advanced Logging** toggle.

## Next steps

Still need help? Contact your IT support person. For contact information, check the [Company Portal website](https://go.microsoft.com/fwlink/?linkid=2010980).

