---
# required metadata

title: Troubleshoot email profiles in Microsoft Intune - Azure | Microsoft Docs
description: See common issues and solutions with email profiles in Microsoft Intune, including duplicate email profiles and errors on Samsung KNOX Standard Android devices.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 02/18/2020
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology:
ms.assetid: f5c944ea-32a6-48af-bb57-16d5f1f3c588
ROBOTS:

# optional metadata

#audience:
#ms.devlang:
ms.reviewer: tscott
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-classic
ms.collection: M365-identity-device-management
---

# Common issues and resolutions with email profiles in Microsoft Intune

Review some common email profile issues, and how to troubleshoot and resolve them.

## What you need to know

- Email profiles are deployed for the user who enrolled the device. To configure the email profile, Intune uses the Azure Active Directory (AD) properties in the email profile of the user during enrollment. [Add email settings to devices](email-settings-configure.md) may be a good resource.
- For Android Enterprise, deploy Gmail or Nine for Work using the managed Google Play Store. [Add Managed Google Play apps](../intune/apps/apps-add-android-for-work.md) lists the steps.
- Microsoft Outlook for iOS/iPadOS and Android don't support email profiles. Instead, deploy an app configuration policy. For more information, see [Outlook Configuration setting](../intune/apps/app-configuration-policies-outlook.md).
- Email profiles targeted to device groups (not user groups) may not be delivered to the device. When the device has a primary user, then device targeting should work. If the email profile includes user certificates, be sure to target user groups.
- Users may be repeatedly prompted to enter their password for the email profile. In this scenario, check all the certificates referenced in the email profile. If one of the certificates isn't targeted to a user, then Intune retries to deploy the email profile.

## Device already has an email profile installed

If users create an email profile before enrolling in Intune or Office 365 MDM, the email profile deployed by Intune may not work as expected:

- **iOS/iPadOS**: Intune detects an existing, duplicate email profile based on hostname and email address. The user-created email profile blocks the deployment of the Intune-created profile. This is a common problem as iOS/iPadOS users typically create an email profile, then enroll. The Company Portal app states that the user isn't compliant, and may prompt the user to remove the email profile.

  The user should remove their email profile so the Intune profile can be deployed. To prevent this issue, instruct your users to enroll, and allow Intune to deploy the email profile. Then, users can create their email profile.

- **Windows**: Intune detects an existing, duplicate email profile based on hostname and email address. Intune overwrites the existing email profile created by the user.

- **Samsung KNOX Standard**: Intune identifies a duplicate email account based on the email address, and overwrites it with the Intune profile. If the user configures that account, it's overwritten again by the Intune profile. This may cause some confusion to the user whose account configuration gets overwritten.

Samsung KNOX doesn't use hostname to identify the profile. We recommend you don't create multiple email profiles to deploy to the same email address on different hosts, as they overwrite each other.

## Error 0x87D1FDE8 for KNOX Standard device

**Issue**: After creating and deploying an Exchange Active Sync email profile for Samsung KNOX Standard for different Android devices, the **0x87D1FDE8** or **remediation failed** error shows in the device's properties > policy tab.

Review the configuration of your EAS profile for Samsung KNOX and source policy. The Samsung Notes sync option is no longer supported, and that option shouldn't be selected in your profile. Be sure devices have enough time to process the policy, up to 24 hours.

## Unable to send images from  email account

Users who have email accounts automatically configured can't send pictures or images from their devices. This scenario can happen if **Allow e-mail to be sent from third-party applications** isn't enabled.

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **Configuration profiles**.
3. Select your email profile > **Properties** > **Settings**.
4. Set the **Allow e-mail to be sent from third-party applications** setting to **Enable**.

## Next steps

Get [support help from Microsoft](../intune/fundamentals/get-support.md), or use the [community forums](https://social.technet.microsoft.com/Forums/en-US/home?category=microsoftintune).
