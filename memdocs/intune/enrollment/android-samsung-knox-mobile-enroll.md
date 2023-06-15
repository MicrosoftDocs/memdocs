---
# required metadata

title: Automatically enroll Android devices using Samsung's Knox Mobile Enrollment
titleSuffix: Microsoft Intune
description: Learn how to enroll Android devices using Samsung KME
keywords:
author: Lenewsad
ms.author: lanewsad
manager:
ms.date: 03/03/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology:
ms.assetid: 30df0f9e-6e9e-4d75-a722-3819e33d480d

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: chmaguir
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: seodec18
ms.collection:
- tier2
- M365-identity-device-management
---

# Automatically enroll Android devices by using Samsung's Knox Mobile Enrollment

This topic helps you set up Intune for enrolling supported Android devices using Samsung Knox Mobile Enrollment (KME). Using Intune with Samsung KME, you can enroll large numbers of company-owned Android devices when end users turn on their devices for the first time and connect to a WiFi or cellular network. Also, devices can be enrolled using Bluetooth or NFC when using the Knox Deployment App.

To enable Intune enrollment using Samsung KME, you use both the Intune and Samsung Knox portals in this order:

1. In the Knox portal:
    1. [Create an MDM profile](#create-mdm-profile)
    2. [Add devices](#add-devices)
    3. [Assign an MDM profile to the devices](#assign-an-mdm-profile-to-devices)
2. In the Knox portal, [configure end user sign in](#configure-how-end-users-sign-in).
3. [Distribute the devices](#distribute-devices).


A list of device identifiers (serial numbers and IMEIs) is automatically added to the Knox Portal when purchasing devices from authorized resellers participating in the Knox Deployment Program.


## Prerequisites

To enroll into Intune using KME, you must first register your company on the Samsung Knox portal by following these steps:
1. [Make sure KME is available in your country/region](https://www.samsungknox.com/en/solutions/it-solutions/knox-configure/available-countries): KME is available in over 55 countries/regions. Ensure that your country/region of deployment is supported.

2. [Supported devices](https://www.samsungknox.com/en/knox-platform/supported-devices/2.4+): KME is available on all Samsung devices with a minimum of Knox 2.4 for Android enrollment and a minimum of Knox 2.8 for Android enterprise enrollment.

3. [Network requirements](https://docs.samsungknox.com/KME-Getting-Started/Content/firewall_exceptions.htm): Make sure that the necessary firewall and network access rules are permitted on your network.

4. [Register for a Samsung account](https://www2.samsungknox.com/en/user/register): A Samsung account is needed to register and enable KME and manage all Knox Enterprise entitlements in a single place.

5. Registration Review: After your profile is completed and submitted, Samsung reviews your application and either approves it immediately or puts it in a pending review status for further follow-up. After your account is approved, you can continue to further steps.

## Create MDM profile

When your company is successfully registered, you can create your MDM profile for Microsoft Intune in the Knox portal using the information below. You can create MDM profiles for both Android and Android enterprise in the Knox portal.
- To create an Android MDM profile, select **Device Admin** as the profile type in the Knox Portal. 
- To create an Android Enterprise MDM profile, select **Device Owner** as the profile type in the Knox Portal.  

### For Android device administrator

| MDM Profile Fields| Required? | Values | 
|-------------------|-----------|-------| 
|Profile Name       | Yes       |Enter a profile name of your choice. |
|Description        | No        |Enter text describing the Profile. |
|MDM Information     | Yes        |Choose **Server URI not required for my MDM**.| 
|MDM Agent APK      | Yes       |https://aka.ms/intune_kme| 
|Custom JSON        | No        |Leave this blank. |
|Skip Setup wizard  | No        |Choose this option to skip standard device setup prompts for the end user.|
|Allow End User to Cancel Enrollment | No | Choose this option to allow users to cancel KME.|
| Privacy Policy, EULAs and Terms of Service | No | Leave this blank. |
| Support contact details | Yes | Choose Edit to update your contact details |
|Associate a Knox license with this profile | No | Leave this option unselected. Enrolling to Intune using KME doesn't require a Knox license.|

### For Android Enterprise

For step-by-step guidance, see the [Samsung's Create Profile](https://docs.samsungknox.com/KME-Getting-Started/Content/create-profiles.htm) instructions.

| MDM Profile Fields| Required? | Values |
|-------------------|-----------|-------|
|Profile Name       | Yes       |Enter a profile name of your choice.|
|Description        | No        |Enter text describing the Profile.|
|Pick your MDM | Yes | Choose Microsoft Intune. |
|MDM Agent APK      | Yes       |https://aka.ms/intune_kme_deviceowner|
|MDM Server URI     | No        |Leave this blank.|
|Custom JSON Data        | Yes*        |{"com.google.android.apps.work.clouddpc.EXTRA_ENROLLMENT_TOKEN": "Enter Intune enrollment token string"}. Learn how to create an enrollment token for [dedicated devices](android-kiosk-enroll.md) and [fully managed devices](android-fully-managed-enroll.md). |
|Dual DAR | No | Leave this blank.|
|QR code for enrollment | No | You can add a QR code to speed enrollment.|
|System applications | Yes | Choose the **Leave all system apps enabled** option to ensure all apps are enabled and available to the profile. If this option isn't selected, only a limited set of system apps displays in the device's apps tray. Apps such as the Email app remain hidden. |
|Privacy Policy, EULAs and Terms of Service | No | Leave this blank.|
|Company Name | Yes | This name will display during device enrollment. |

\* This field is not required to complete profile creation in the Knox portal. However, Intune does require this field to be filled in so that the profile can successfully enroll the device in Intune.

## Add devices

To assign MDM Profiles to devices, supported Samsung Knox devices must be added to the Knox Portal using one of the following methods:
- **Using Samsung-Approved Reseller(s):** Use this method if you're purchasing devices from one of the Samsung-approved resellers. Resellers can auto-upload devices for you when approved. [Visit the Samsung Knox Enrollment User Guide to learn how to add resellers](https://docs.samsungknox.com/KME-Getting-Started/Content/Register_resellers.htm).

- **Using the Knox Deployment App (KDA):** Use this method if you have existing devices that need to be enrolled using KME. You can either use Bluetooth or NFC to add devices to the Knox Portal using this method. [Visit the Samsung Knox Enrollment User Guide to learn about using the KDA](https://docs.samsungknox.com/admin/knox-mobile-enrollment/about-kda.htm).

## Assign an MDM profile to devices
You must assign an MDM profile to added devices in the Knox Portal before they can be enrolled. [Visit the Samsung Knox Enrollment User Guide to learn about device configuration](https://docs.samsungknox.com/KME-Getting-Started/Content/configure-devices.htm).

## Configure how end users sign in

For devices enrolled in Intune using KME for Android, you can configure how an end user signs in as follows:

- **Without user name association:** In the Knox Portal under **Device details**, leave the **User ID** and **Password** fields blank for the added devices. This option requires the end user to enter both user name and password when enrolling to Intune.

- **With user name association:** In the Knox Portal under **Device details**, provide a **User ID** (such as a user name for the assigned user or a [Device Enrollment Manager](device-enrollment-manager-enroll.md) account) for the added devices. This option prepopulates the user name and requires the end user to enter a password when enrolling to Intune.

> [!NOTE]
>
>User association only applies to Android device administrator enrollment. When user association is defined, only the associated user can enroll the device using KME. This is true even after a factory reset of the device. When no user association is defined in the Knox portal, any user with a valid Intune license can enroll the device using KME.
>For Android Enterprise fully managed devices, even if user association is defined, it will not be passed to the device or tie the device to the user.
>

## Distribute devices

After creating and assigning an MDM profile, associating a user name, and identifying the devices as corporate-owned in Intune, you can distribute devices to users.

Still need help? Check out the complete [KME User Guide](https://docs.samsungknox.com/KME-Getting-Started/Content/get-started.htm).

## Frequently asked questions

- **Device Owner support:** Intune supports enrolling Dedicated and Fully Managed devices by using the KME portal. Other Android enterprise device owner modes will be supported as they become available in Intune.

- **Work profile support:** KME is a corporate device enrollment method and devices enrolled in Android personally-owned work profile ensure work and personal data are separate on personal devices. Device enrollment to personally-owned work profile using KME is not a supported scenario in Intune.

- **Factory reset to enroll to Android enterprise:** If repurposing devices that have already been set up, devices need to be factory reset when enrolling to Android Enterprise.

- **Updates using Google Play account:** Google Play account isn't necessary for enrolling the device to Microsoft Intune. But, for Android device administrator enrollments, future updates to the Intune Company Portal app may require a Google Play account on the device. Google Play account isn't required when enrolling to Google Device Owner.

- **"Password" field is ignored:** If the **password** field is populated in **Device details** in the Knox Portal, it's ignored by the Intune Company Portal app during Android enrollment. The end user must enter a password on the device to complete device enrollment.


## Getting support
Learn more about [how to get support for Samsung KME](https://docs.samsungknox.com/KME-Getting-Started/Content/to-get-kme-support.htm).


