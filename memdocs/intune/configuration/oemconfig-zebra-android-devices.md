---
# required metadata

title: Deploy OEMConfig profiles to Zebra devices using Microsoft Intune
description: Use Microsoft Intune to create and deploy multiple OEMConfig device configuration profiles on Zebra devices running Android Enterprise. Use Zebra actions and steps to order your profiles.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 06/27/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: Low
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: akritis
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
---

# Deploy OEMConfig profiles to Zebra devices in Microsoft Intune

In Microsoft Intune, use OEMConfig to customize OEM-specific settings for Android Enterprise devices. These settings are specific to the device manufacturer, and deployed using configuration profiles in Intune.

Depending on the OEMCOnfig app you're using, on Zebra devices, you can deploy or assign profiles to the same device. Existing OEMConfig profiles can use this feature the next time the devices sync with Intune.

This feature applies to:

- Zebra devices running Android Enterprise

To learn more about OEMConfig, including what it does, and how to use it, go to [OEMConfig configuration profile](android-oem-configuration-overview.md).

This article describes deploying OEMConfig multiple profiles to Zebra devices, describes ordering, and using the reporting features in Microsoft Intune.

## Prerequisites

- Create an [OEMConfig configuration profile](android-oem-configuration-overview.md). Review the [Before you begin](android-oem-configuration-overview.md#before-you-begin) section for important information, as there's a 500 KB file size limit and other important information.
- Zebra devices don't support Android 12.

## OEMConfig apps for Zebra devices

To manage Zebra devices, there are two versions of the OEMConfig app:

| OEMConfig app | Supported Android versions | Multiple profile support |
| --- | --- | --- |
| **Zebra OEMConfig Powered by MX** (new app) | - Android 13 and later <br/> - Android 11 | ❌ This new app aligns closely with Google's standards. It's suggested to deploy one profile with all the required configuration settings.<br/><br/>If you use multiple OEMConfig profiles, then don't configure the same top parent group or bundle in multiple profiles. It can cause conflicts. For more important information, go to [OEMConfig overview - Before you begin](android-oem-configuration-overview.md#before-you-begin) <br/><br/>For more information on the new **Zebra OEMConfig Powered by MX** app, go to [New Zebra OEMConfig app for Android](https://techcommunity.microsoft.com/t5/intune-customer-success/new-zebra-oemconfig-app-for-android-11-and-later/ba-p/3846730). |
| **Legacy Zebra OEMConfig** | - Android 11 and earlier | ✅ You can split your Zebra OEMConfig settings into smaller profiles. For example, create a baseline profile that affects all devices. Then, create more profiles that configure settings specific to a device. |

## Multiple profiles using the Legacy Zebra OEMConfig app

Zebra's OEMConfig schema also uses **Actions**. Actions are operations that run on the device. They don't configure any settings. Use these actions to trigger a file download, clear the clipboard, and more. For a full list of the supported actions, go to [Zebra's documentation](https://techdocs.zebra.com/oemconfig/) (opens Zebra's web site).

For example, you create a Zebra OEMConfig profile that applies some settings to the device. Another Zebra OEMConfig profile includes an action that clears the clipboard. You assign the first profile to a Zebra devices group. Later, you need to clear the clipboard on those devices. You assign the second profile to the same devices group, without changing the first profile. The device clipboard gets cleared without resending or affecting the configuration settings created in the first profile.

In another example, you assigned an OEMConfig profile that configured some Zebra device settings. Recently, users are reporting issues with a specific application, and you want to clear the app's cache. Create a new OEMConfig profile that includes only the "clear cache" action. Assign the profile to the devices that need it.

Multiple profiles take longer to deploy than a single profile. If the speed of delivery of policy to the device is important, you should group settings into the smallest number of profiles possible. 

## Ordering

With multiple profiles on each device, the order that profiles are deployed isn't guaranteed. This behavior is a Google Play limitation. To run operations in sequence, you can use [Zebra's Transaction Step feature](https://techdocs.zebra.com/oemconfig/11-4/mc/#transactionsteps) (opens Zebra's web site). 

To summarize, if order matters, use [Zebra's Transaction Step feature](https://techdocs.zebra.com/oemconfig/11-4/mc/#transactionsteps) (opens Zebra's web site). If order doesn't matter, use multiple Intune profiles. 

Let's look at some examples:

- You want to turn on Bluetooth for all newly enrolled Zebra devices before configuring any other setting on these devices. To run operations in sequence, use the **Steps** feature in Zebra's schema.

  Create one Intune profile that has two Transaction Steps. The first step includes Bluetooth settings, and the second step configures the other setting. When Zebra's OEMConfig app receives the profile, it runs the steps in order.

  For more information, go to [Zebra's transaction steps](https://techdocs.zebra.com/oemconfig/11-4/mc/#transactionsteps) (opens Zebra's web site).

- You want all Zebra devices to display time in 24-hour format. For some of these devices, you want to turn off the camera. The time and camera settings don't depend on each other.

  Create two Intune profiles:

  - **Profile 1**: Displays the time in 24-hour format. On Monday, this profile is assigned to the **All Zebra AE devices** group.
  - **Profile 2**: Turns off the camera. On Tuesday, this profile is assigned to the **Zebra AE factory devices** group.

  On Wednesday, you enroll 10 new Zebra devices with Intune. Profile 1 and Profile 2 are assigned. After the new devices sync with Intune, they receive the profiles. The devices can get Profile 2 before getting Profile 1.

## Enhanced reporting

When you deploy the Intune profile, the Zebra OEMConfig app on the device executes the configurations in your profile. The Zebra OEMConfig app also reports the profile status to Intune.

In the Intune admin center, you can view the status of deployed OEMConfig profiles, and any errors or warnings.

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select your Zebra OEMConfig profile > **Monitor** > **Device status**. This option shows the devices that have your OEMConfig profile assigned.
3. Select a device > **Device configuration** > Select your Zebra OEMConfig profile. This option shows the profile settings that succeeded or failed.

    Select a failed row. Details are shown that have more information on why it failed.

## Related articles

- Learn more about [OEMConfig configuration profiles](android-oem-configuration-overview.md).
- On Android device administrator, configure [Mobility Extensions (MX)](android-zebra-mx-overview.md).
- [Monitor the profile status](device-profile-monitor.md).
