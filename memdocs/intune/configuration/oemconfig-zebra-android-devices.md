---
# required metadata

title: Deploy many OEMConfig profiles to Zebra devices using Microsoft Intune - Azure | Microsoft Docs
description: Use Microsoft Intune to create and deploy multiple OEMConfig device configuration profiles on Zebra devices running Android Enterprise. Use Zebra actions and steps to order your profiles.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/12/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority:
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: jieyan
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Deploy multiple OEMConfig profiles to Zebra devices in Microsoft Intune

In Microsoft Intune, use OEMConfig to customize OEM-specific settings for Android Enterprise devices. These settings are specific to the device manufacturer, and deployed using configuration profiles in Intune.

On Zebra devices, you can deploy or assign multiple profiles to the same device. Existing OEMConfig profiles can use this feature the next time the devices sync with Intune.

This feature applies to:

- Zebra devices running Android Enterprise

To learn more about OEMConfig, including what it does, and how to use it, see [OEMConfig configuration profile](android-oem-configuration-overview.md).

This article describes deploying OEMConfig multiple profiles to Zebra devices, describes ordering, and using the reporting features in Microsoft Intune.

## Prerequisites

Create an [OEMConfig configuration profile](android-oem-configuration-overview.md).

## Use multiple profiles

On Zebra devices, you can have many profiles on each device simultaneously. This feature allows you to split your Zebra OEMConfig settings into smaller profiles. For example, you could have one baseline profile that affects all devices, and then additional profiles for certain devices that configure settings specific to those use cases.

Zebra’s OEMConfig schema also uses **Actions**. Actions are operations that run on the device. They don’t configure any settings. Use these actions to trigger a file download, clear the clipboard, and more. For a full list of the supported actions, see [Zebra’s documentation](https://techdocs.zebra.com/oemconfig/10-0/about/) (opens Zebra's web site).

For example, you create a Zebra OEMConfig profile that applies some settings to the device. Another Zebra OEMConfig profile includes an action that clears the clipboard. You assign the first profile to a Zebra devices group. Later, you need to clear the clipboard on those devices. You assign the second profile to the same devices group, without changing the first profile. The device clipboard gets cleared without resending or affecting the configuration settings created in the first profile.

In another example, you assigned an OEMConfig profile that configured some Zebra device settings. Recently, users are reporting issues with a specific application, and you want to clear the app's cache. Create a new OEMConfig profile that includes only the “clear cache” action. Assign the profile to the devices that need it.

## Ordering

With multiple profiles on each device, the order that profiles are deployed isn’t guaranteed. This behavior is a Google Play limitation. To run operations in sequence, you can use [Zebra's Transaction Step feature](https://techdocs.zebra.com/oemconfig/10-0/mc/) (opens Zebra's web site). Let's look at an example.

Let's say you want to turn on Bluetooth for all newly-enrolled Zebra devices before configuring another setting on the same devices.

You create two profiles:

- **Profile 1**: Turns on Bluetooth. This profile is assigned on Monday to the **All Devices** group.
- **Profile 2**: Configures the other setting. This profile is assigned on Tuesday to the **All Devices** group.

On Wednesday, you enroll 10 new Zebra devices with Intune. Profile 1 and Profile 2 are assigned to the **All Devices** group. After the new devices sync with Intune, they receive the profiles. These devices may get Profile 2 before Profile 1.

The better way to accomplish your goal is to use the **Steps** feature in Zebra’s schema to confirm that operations run in sequence. In this case, you create one profile that has two Transaction Steps. The first step includes Bluetooth settings, and the second step configures the other setting. When Zebra’s OEMConfig app receives the profile, it runs the steps in order.

For more information, see [Zebra's transaction steps](https://techdocs.zebra.com/oemconfig/10-0/mc/) (opens Zebra's web site).

## Enhanced reporting

You deploy a profile, and it’s executed by the Zebra OEMConfig app on the device. The Zebra OEMConfig app reports the profile status to Intune. In the Endpoint Manager admin center, you can see the status of deployed OEMConfig profiles, and any errors or warnings.

1. Open the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select your Zebra OEMConfig profile > **Monitor** > **Device status**. This option shows the devices that have your OEMConfig profile assigned.
3. Select a device > **Device configuration** > Select your Zebra OEMConfig profile. This option shows the profile settings that succeeded or failed.

    Select a failed row. Details are shown that have more information on why it failed.

## Next steps

- Learn more about [OEMConfig configuration profiles](android-oem-configuration-overview.md).
- On Android device administrator, configure [Mobility Extensions (MX)](android-zebra-mx-overview.md).
- [Monitor the profile status](device-profile-monitor.md).
