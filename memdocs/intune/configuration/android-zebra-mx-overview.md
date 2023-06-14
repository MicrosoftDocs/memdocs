---
# required metadata

title: Use Zebra Mobility Extensions on Android devices in Microsoft Intune
description: Use Microsoft Intune to manage and use Zebra devices running Android with Zebra Mobility Extensions (MX). See all the steps, including install the Company Portal app, sideload the app, assign device administrator role, create a StageNow profile, and more.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 09/07/2022
ms.topic: how-to
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
ms.collection:
- tier2
- M365-identity-device-management
---

# Use and manage Zebra devices with Zebra Mobility Extensions in Microsoft Intune

Intune includes a rich set of features, including managing apps and configuring device settings. These built-in features and settings manage Android devices manufactured by Zebra Technologies, also known as "Zebra devices".

On Android devices, use Zebra's **Mobility Extensions (MX)** profiles to customize or add more Zebra-specific settings.

This feature applies to:

- Android device administrator

For Android Enterprise devices, use [OEMConfig](android-oem-configuration-overview.md).

Your company may use Zebra devices for retail, on the factory floor, and more. For example, you're a retailer and your environment includes thousands of Zebra mobile devices used by sales associates. Intune can help manage these devices as part of your mobile device management (MDM) solution.

Using Intune, you can enroll Zebra devices to deploy your line-of-business apps to the devices. "Device configuration" profiles let you create MX profiles to manage your Zebra-specific settings.

This article shows you how to use Zebra Mobility Extensions (MX) on Zebra devices in Microsoft Intune.

> [!NOTE]
> By default, the Zebra MX APIs aren't locked down on devices. Before a device enrolls in Intune, it's possible the device can be compromised in a malicious manner. When the device is in a clean state, we suggest you lock down MX APIs using Access Manager (AccessMgr). For example, you can choose that only the Company Portal app and apps you trust are allowed to call MX APIs.
>
> For more information, see [Locking down your device](https://developer.zebra.com/community/home/blog/2017/04/11/locking-down-your-device) on Zebra's web site.

## Before you begin

- Be sure you have the latest version of the StageNow desktop app from Zebra Technologies.
- Be sure to check [Zebra's full MX feature matrix](http://techdocs.zebra.com/mx/compatibility) (opens Zebra's web site). Confirm the profiles you create are compatible with the device's MX version, OS version, and model.
- Certain devices, such as TC20/25 devices, don't support all of the available MX features in StageNow. Be sure to check [Zebra's feature matrix](http://techdocs.zebra.com/mx/tc2x/) (opens Zebra's web site) for updated support info.

## Step 1: Install the latest Company Portal app

On the device, open the Google Play store. Download and install the Intune Company Portal app from Microsoft. When installed from Google Play, the Company Portal app gets updates and fixes automatically.

If Google Play isn't available, download the [Microsoft Intune Company Portal for Android](https://www.microsoft.com/download/details.aspx?id=49140) (opens another Microsoft website), and [sideload it](#sideload-the-company-portal-app) (in this article). When installed this way, the app doesn't receive updates or fixes automatically. Be sure to regularly update and patch the app manually.

### Sideload the Company Portal app

"Sideloading" is when you don't use Google Play to install an app. To sideload the Company Portal app, use StageNow.

The following steps provide an overview. For specific details, see Zebra's documentation. [Enroll in an MDM using StageNow](https://techdocs.zebra.com/stagenow/5-7/Profiles/enrollmdm/) (opens Zebra's web site) may be a good resource.

1. In StageNow, create a profile for **Enroll in an MDM**.
2. In **Deployment**, choose to download the MDM agent file.
3. Set the **Support App** and **Download Configuration** steps to **No**.
4. In **Download MDM**, select **Transfer/Copy File**. Add the source and destination of the Company Portal Android package (APK).
5. In **Launch MDM**, leave the default values as-is. Add the following details:

    - **Package Name**: `com.microsoft.windowsintune.companyportal`
    - **Class Name**: `com.microsoft.windowsintune.companyportal.views.SplashActivity`

Continue to publish the profile, and consume it with the StageNow app on the device. The Company Portal app is installed and opened on the device.

> [!TIP]
> For more information on StageNow, and what it does, see [StageNow Android device staging](https://www.zebra.com/us/en/products/software/mobile-computers/mobile-app-utilities/stagenow.html) (opens Zebra's web site).

## Step 2: Confirm the Company Portal app has device administrator role

The Company Portal app requires Device Administrator to manage Android devices. To activate the Device Administrator role, some Zebra devices include a user interface (UI) on the device. If the device includes a UI, the Company Portal app prompts the end user to grant Device Administrator during [enrollment](#step-3-enroll-the-device-in-to-intune) (in this article).

If a UI isn't available, use the **DevAdmin Manager** in StageNow to create a profile that manually grants Device Administrator to the Company Portal app.

The following steps provide an overview. For specific details, see Zebra's documentation. 
[Set battery swap mode as device administrator](https://zebratechnologies.force.com/s/article/Set-Battery-Swap-Mode-as-Device-Administrator-using-StageNow-Tool) (opens Zebra's website) may be a good resource.

1. In StageNow, create a profile and select **Xpert Mode**.
2. Add **DevAdmin Manager** to the profile.
3. Set **Device Administration Action** to **Turn On as Device Administrator**.
4. Set **Device Admin Package Name** to `com.microsoft.windowsintune.companyportal`.
5. Set **Device Admin Class Name** to `com.microsoft.omadm.client.PolicyManagerReceiver`.

Continue to publish the profile, and consume it with the StageNow app on the device. The Company Portal app is granted the Device Administrator role.

## Step 3: Enroll the device in to Intune

After completing the first two steps, the Company Portal app is installed on the device. The device is ready to be enrolled in to Intune.

[Enroll Android devices](/mem/intune/fundamentals/deployment-guide-enrollment-android) lists the steps. If you have many Zebra devices, you may want to use a [device enrollment manager (DEM) account](../enrollment/device-enrollment-manager-enroll.md). Using a DEM account also removes the option to unenroll from the Company Portal app, so that users can't unenroll the device as easily.

## Step 4: Create a device management profile in StageNow

Use StageNow to create a profile that configures the settings you want to manage on the device. For specific details, see Zebra's documentation. [Profiles](https://techdocs.zebra.com/stagenow/5-7/stagingprofiles/) (opens Zebra's website) may be a good resource.

When you create the profile in StageNow, on the last step, select **Export to MDM**. This step generates an XML file. Save this file. You need it in a later step.

- It's recommended to test the profile before you deploy it to devices in your organization. To test, in the last step when creating profiles with StageNow on your computer, use the **Test** options. Then, consume the StageNow-generated file with the StageNow app on the device.

  The StageNow app on the device shows logs generated when you test the profile. [Use StageNow logs on Zebra devices running Android in Intune](android-zebra-mx-logs-troubleshoot.md) has information on using StageNow logs to understand errors.

- If you reference apps, update packages, or update other files in your StageNow profile, you want the device to get these updates. To get the updates, the device must connect to the StageNow deployment server when the profile is applied. 

  Or, you can use built-in features in Intune to get these changes, including:

  - App management features to [add](../apps/apps-add.md), [deploy](../apps/apps-deploy.md), update, and [monitor](../apps/apps-monitor.md) apps.
  - Manage [system and app updates](device-restrictions-android-for-work.md#fully-managed-dedicated-and-corporate-owned-work-profile) on devices running Android Enterprise

After you test the file, the next step is to deploy the profile to devices using Intune.

- You can deploy one or multiple MX profiles to a device.
- You can also export multiple StageNow profiles, and combine the settings into a single XML file. Then, upload the XML file to Intune to deploy to your devices.

  > [!WARNING]
  > 
  > - If multiple MX profiles are targeted to the same group, and configure the same property, there will be conflicts on the device.
  > - If the same property is configured multiple times in a single MX profile, the last configuration wins.

## Step 5: Create a profile in Intune

In Intune, create a device configuration profile:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **Configuration profiles** > **Create profile**.
3. Enter the following properties:

    - **Platform**: Select **Android device administrator**.
    - **Profile**: Select **MX profile (Zebra only)**.

4. Select **Create**.
5. In **Basics**, enter the following properties:

    - **Name**: Enter a descriptive name for the new profile.
    - **Description**: Enter a description for the profile. This setting is optional, but recommended.

6. Select **Next**.
7. In **Configuration settings** > **Choose a valid Zebra MX XML file**, add the XML profile file [you exported from StageNow](#step-4-create-a-device-management-profile-in-stagenow) (in this article).

    When done, select **Next**.

    > [!TIP]
    > For security reasons, you won't see the profile XML text after you save it. The text is encrypted, and you only see asterisks (`****`). For your reference, it's recommended to save copies of the MX profiles before you add them to Intune.

8. In **Scope tags** (optional) > **Select scope tags**, choose your scope tags to assign to the profile. For more information, see [Use RBAC and scope tags for distributed IT](../fundamentals/scope-tags.md).

    Select **Next**.

9. In **Assignments**, select the groups that will receive this profile. For more information on assigning profiles, see [Assign user and device profiles](device-profile-assign.md).

    Select **Next**.

10. In **Review + create**, when you're done, choose **Create**. The profile is created, and shown in the list.

    You can also [monitor its status](device-profile-monitor.md).

The next time the device checks for configuration updates, the MX profile is deployed to the device. Devices sync with Intune when devices enroll, and then approximately every 8 hours. You can also [force a sync in Intune](../remote-actions/device-sync.md). Or, on the device, open the **Company Portal app** > **Settings** > **Sync**.

## Update a Zebra MX configuration after it's assigned

To update the MX-specific configuration of a Zebra device, you can: 

- Create an updated StageNow XML file, edit the existing Intune MX profile, and upload the new StageNow XML file. This new file overwrites the previous policy in the profile, and replaces the previous configuration.
- Create a new StageNow XML file that configures different settings, create a new Intune MX profile, upload the new StageNow XML file, and assign it to the same group. Multiple profiles are deployed. If the new profile configures settings that already exist in existing profiles, conflicts will occur.

## Next steps

- [Assign the profile](device-profile-assign.md) and [monitor its status](device-profile-monitor.md).
- [Use StageNow logs to troubleshoot Zebra devices](android-zebra-mx-logs-troubleshoot.md).
