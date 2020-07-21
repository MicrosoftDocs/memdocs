---
# required metadata

title: Troubleshoot email profiles in Microsoft Intune - Azure | Microsoft Docs
description: See common issues and solutions with email profiles in Microsoft Intune, including duplicate email profiles and errors on Samsung KNOX Standard Android devices.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 07/20/2020
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology:
ms.assetid: f5c944ea-32a6-48af-bb57-16d5f1f3c588
ROBOTS:

# optional metadata

#audience:

ms.reviewer: tscott
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-classic
ms.collection: M365-identity-device-management
---

# Common issues and resolutions with email profiles in Microsoft Intune

Review some common email profile issues, and how to troubleshoot and resolve them.

## Users are repeatedly prompted to enter their password

Users are repeatedly prompted to enter their password for the email profile. If certificates are used to authenticate and authorize the user, check the assignments of all the certificate profiles. Typically, these certificate profiles are assigned to user groups, not device groups. If one of the certificate profiles isn't targeted to a user, then Intune keeps retrying to deploy the email profile.

If the email profile chain is assigned to user groups, be sure your certificate profiles are also assigned to user groups.

## Profiles deployed to device groups show errors and latency

Email profiles are typically assigned to user groups. There may be some cases when they're assigned to device groups.

- For example, you want to deploy a certificate-based email profile to only Surface devices, not desktops. In this scenario, device groups might make sense. Know that these devices may show as not compliant, may return errors, and may not get your email profiles immediately.

  In this example, you create the email profile, and assign the profile to device groups. The device restarts, and there's a delay before a user signs in. During this delay, your PKCS certificate profile, which is assigned to user groups, is deployed. Since there's no user yet, the PKCS certificate profile causes the device to be not compliant. The Event Viewer may also show errors on the device.

  To get compliant, the user signs in to the device, and syncs with Intune to receive the policies. Users can resync manually, or wait for the next sync.

- For example, you're using dynamic groups. If Azure AD doesn't update the dynamic groups immediately, then these devices may show as uncompliant.

In these scenarios, you decide if it's more important to use device groups, or more important to show all policies as compliant.

## Device already has an email profile installed

If users create an email profile before enrolling in Intune or Office 365 MDM, the email profile deployed by Intune may not work as expected:

- **iOS/iPadOS**: Intune detects an existing, duplicate email profile based on hostname and email address. The user-created email profile blocks the deployment of the Intune-created profile. This scenario is a common problem as iOS/iPadOS users typically create an email profile, then enroll. The Company Portal app states that the user isn't compliant, and may prompt the user to remove the email profile.

  The user should remove their email profile so the Intune profile can be deployed. To prevent this issue, instruct your users to enroll, and allow Intune to deploy the email profile. Then, users can create their email profile.

- **Windows**: Intune detects an existing, duplicate email profile based on hostname and email address. Intune overwrites the existing email profile created by the user.

- **Samsung KNOX Standard**: Intune identifies a duplicate email account based on the email address, and overwrites it with the Intune profile. If the user configures that account, it's overwritten again by the Intune profile. This behavior may cause some confusion to the user whose account configuration gets overwritten.

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

Get [support help from Microsoft](../fundamentals/get-support.md), or use the [community forums](https://social.technet.microsoft.com/Forums/en-US/home?category=microsoftintune).
