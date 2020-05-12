---
title: Troubleshooting iOS/iPadOS device enrollment problems in Microsoft Intune
titleSuffix: Microsoft Intune
description: Suggestions for troubleshooting some of the most common problems when you enroll iOS/iPadOS devices in Intune.
keywords:
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 11/18/2019
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: medium
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: mghadial
#ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Troubleshoot iOS/iPadOS device enrollment problems in Microsoft Intune

This article helps Intune administrators understand and troubleshoot problems when enrolling iOS/iPadOS devices in Intune.

## Prerequisites

Before you start troubleshooting, it's important to collect some basic information. This information can help you better understand the problem and reduce the time to find a resolution.

Collect the following information about the problem:

- What is the exact error message?
- Where do you see the error message?
- When did the problem start? Has enrollment ever worked?
- What platform (Android, iOS/iPadOS, Windows) has the problem?
- How many users are affected? Are all users affected or just some?
- How many devices are affected? Are all devices affected or just some?
- What is the MDM authority?
- How is enrollment being performed? Is it "Bring your own device" (BYOD) or Apple Automated Device Enrollment (ADE) with enrollment profiles?

## Error messages

### Profile Installation Failed. A Network Error Has Occurred.

**Cause:** There's an unspecified problem with iOS/iPadOS on the device.

#### Resolution

1. To prevent data loss in the following steps (restoring iOS/iPadOS deletes all data on the device), make sure to back up your data.
2. Put the device in recovery mode and then restore it. Make sure that you set it up as a new device. For more information about how to restore iOS/iPadOS devices, see [https://support.apple.com/HT201263](https://support.apple.com/HT201263).
3. Re-enroll the device.

### Profile Installation Failed. Connection to the server could not be established.

**Cause:** Your Intune tenant is configured to only allow corporate-owned devices. 

#### Resolution
1. Sign in to the Azure portal.
2. Select **More Services**, search for Intune, and then select **Intune**.
3. Select **Device enrollment** > **Enrollment restrictions**.
4. Under **Device Type Restrictions**, select the restriction that you want to set > **Properties** > **Select platforms** > select **Allow** for **iOS**, and then click **OK**.
5. Select **Configure platforms**, select **Allow** for personally owned iOS/iPadOS devices, and then click **OK**.
6. Re-enroll the device.

**Cause:** The necessary CNAME records in DNS don't exist.

#### Resolution
Create CNAME DNS resource records for your company's domain. For example, if your company's domain is contoso.com, create a CNAME in DNS that redirects EnterpriseEnrollment.contoso.com to EnterpriseEnrollment-s.manage.microsoft.com.

Although creating CNAME DNS entries is optional, CNAME records make enrollment easier for users. If no enrollment CNAME record is found, users are prompted to manually enter the MDM server name, enrollment.manage.microsoft.com.

If there's more than one verified domain, create a CNAME record for each domain. The CNAME resource records must contain the following information:

|TYPE|Host name|Points to|TTL|
|------|------|------|------|
|CNAME|EnterpriseEnrollment.company_domain.com|EnterpriseEnrollment-s.manage.microsoft.com|1 Hr|
|CNAME|EnterpriseRegistration.company_domain.com|EnterpriseRegistration.windows.net|1 Hr|

If your company uses multiple domains for user credentials, create CNAME records for each domain.

> [!NOTE]
> Changes to DNS records might take up to 72 hours to propagate. You can't verify the DNS change in Intune until the DNS record propagates.

**Cause:** You enroll a device that was previously enrolled with a different user account, and the previous user was not appropriately removed from Intune.

#### Resolution
1. Cancel any current profile installation.
2. Open [https://portal.manage.microsoft.com](https://portal.manage.microsoft.com) in Safari.
3. Re-enroll the device.

> [!NOTE]
> If enrollment still fails, remove cookies in Safari (don't block cookies), then re-enroll the device.

**Cause:** The device is already enrolled with another MDM provider.

#### Resolution
1. Open **Settings** on the iOS/iPadOS device, go to **General > Device Management**.
2. Remove any existing management profile.
3. Re-enroll the device.

**Cause:** The user who is trying to enroll the device does not have a Microsoft Intune license.

#### Resolution
1. Go to the [Office 365 Admin Center](https://admin.microsoft.com), and then choose **Users > Active Users**.
2. Select the user account that you want to assign an Intune user license to, and then choose **Product licenses > Edit**.
3. Switch the toggle to the **On** position for the license that you want to assign to this user, and then choose **Save**.
4. Re-enroll the device.

### This Service is not supported. No Enrollment Policy.

**Cause**: An Apple MDM push certificate isn't configured in Intune, or the certificate is invalid. 

#### Resolution

- If the MDM push certificate isn't configured, follow the steps in [Get an Apple MDM push certificate](apple-mdm-push-certificate-get.md#steps-to-get-your-certificate).
- If the MDM push certificate is invalid, follow the steps in [Renew Apple MDM push certificate](apple-mdm-push-certificate-get.md#renew-apple-mdm-push-certificate).

### Company Portal Temporarily Unavailable. The Company Portal app encountered a problem. If the problem persists, contact your system administrator.

**Cause:** The Company Portal app is out of date or corrupted.

#### Resolution
1. Remove the Company Portal app from the device.
2. Download and install the **Microsoft Intune Company Portal** app from **App Store**.
3. Re-enroll the device.
 > [!NOTE]
    > This error can also occur if the user is attempting to enroll more devices than device enrollment is configured to allow. Follow
    the resolutions steps for **Device Cap Reached** below if these steps do not resolve the issue.

### Device Cap Reached

**Cause:** The user tries to enroll more devices than the device enrollment limit.

#### Resolution
1. In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), choose **Devices** > **All Devices**, and check the number of devices the user has enrolled.
    > [!NOTE]
    > You should also have the affected user logon to the [Intune user portal](https://portal.manage.microsoft.com/) and check devices that have enrolled. There may be devices that appear in the [Intune user portal](https://portal.manage.microsoft.com/) but not in the [Intune admin portal](https://portal.azure.com/?Microsoft_Intune=1&Microsoft_Intune_DeviceSettings=true&Microsoft_Intune_Enrollment=true&Microsoft_Intune_Apps=true&Microsoft_Intune_Devices=true#blade/Microsoft_Intune_DeviceSettings/ExtensionLandingBlade/overview), such devices also count toward the device enrollment limit.
2. In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), choose **Devices** > **Enrollment restrictions** > check the device enrollment limit. By default, the limit is set to 15. 
3. If the number of devices enrolled has reached the limit, remove unnecessary devices, or increase the device enrollment limit. Because every enrolled device consumes an Intune license, we recommend that you always remove unnecessary devices first.
4. Re-enroll the device.

### Workplace Join failed

**Cause:** The Company Portal app is out of date or corrupted.  

#### Resolution
1. Remove the Company Portal app from the device.
2. Download and install the **Microsoft Intune Company Portal** app from **App Store**.
3. Re-enroll the device.

### User License Type Invalid

**Cause:** The user who is trying to enroll the device does not have a valid Intune license.

#### Resolution
1. Go to the [Microsoft 365 admin center](https://admin.microsoft.com), and then choose **Users** > **Active Users**.
2. Select the affected user account > **Product licenses** > **Edit**.
3. Verify that a valid Intune license is assigned to this user.
4. Re-enroll the device.

### User Name Not Recognized. This user account is not authorized to use Microsoft Intune. Contact your system administrator if you think you have received this message in error.

**Cause:** The user who is trying to enroll the device does not have a valid Intune license.

1. Go to the [Microsoft 365 admin center](https://admin.microsoft.com), and then choose **Users** > **Active Users**.
2. Select the affected user account, and then choose **Product licenses** > **Edit**.
3. Verify that a valid Intune license is assigned to this user.
4. Re-enroll the device.

### Profile Installation Failed. The new MDM payload does not match the old payload.

**Cause:** A management profile is already installed on the device.

#### Resolution

1. Open **Settings** on the iOS/iPadOS device > **General** > **Device Management**.
2. Tap the existing management profile, and tap **Remove Management**.
3. Re-enroll the device.

### NoEnrollmentPolicy

**Cause:** The Apple Push Notification Service (APNs) certificate is missing, invalid, or expired.

#### Resolution
Verify that a valid APNs certificate is added to Intune. For more information, see [Set up iOS/iPadOS enrollment](ios-enroll.md).

### AccountNotOnboarded

**Cause:** There's a problem with the Apple Push Notification service (APNs) certificate configured in Intune.

#### Resolution
Renew the APNs certificate, and then re-enroll the device.

> [!IMPORTANT]
> Make sure that you renew the APNs certificate. Don't replace the APNs certificate. If you replace the certificate, you have to re-enroll all iOS/iPadOS devices in Intune. 

- To renew the APNs certificate in Intune standalone, see [Renew Apple MDM push certificate](apple-mdm-push-certificate-get.md#renew-apple-mdm-push-certificate).
- To renew the APNs certificate in Office 365, see [Create an APNs Certificate for iOS/iPadOS devices](https://support.office.com/article/Create-an-APNs-Certificate-for-iOS-devices-522b43f4-a2ff-46f6-962a-dd4f47e546a7).

### XPC_TYPE_ERROR Connection invalid

When you turn on a ADE-managed device that is assigned an enrollment profile, enrollment fails, and you receive the following error message:

```
asciidoc
mobileassetd[83] <Notice>: 0x1a49aebc0 Client connection: XPC_TYPE_ERROR Connection invalid <error: 0x1a49aebc0> { count = 1, transaction: 0, voucher = 0x0, contents = "XPCErrorDescription" => <string: 0x1a49aee18> { length = 18, contents = "Connection invalid" } }
iPhone mobileassetd[83] <Notice>: Client connection invalid (Connection invalid); terminating connection
iPhone com.apple.accessibility.AccessibilityUIServer(MobileAsset)[288] <Notice>: [MobileAssetError:29] Unable to copy asset information from https://mesu.apple.com/assets/ for asset type com.apple.MobileAsset.VoiceServices.CombinedVocalizerVoices
iPhone mobileassetd[83] <Notice>: 0x1a49aebc0 Client connection: XPC_TYPE_ERROR Connection invalid <error: 0x1a49aebc0> { count = 1, transaction: 0, voucher = 0x0, contents = "XPCErrorDescription" => <string: 0x1a49aee18> { length = 18, contents = "Connection invalid" }
```

**Cause:** There's a connection issue between the device and the Apple ADE service.

#### Resolution
Fix the connection issue, or use a different network connection to enroll the device. You may also have to contact Apple if the issue persists.


## Other issues

### ADE enrollment doesn't start
When you turn on a ADE-managed device that is assigned an enrollment profile, the Intune enrollment process isn't initiated.

**Cause:** The enrollment profile is created before the ADE token is uploaded to Intune.

#### Resolution

1. Edit the enrollment profile. You can make any change to the profile. The purpose is to update the modification time of the profile.
2. Synchronize ADE-managed devices: In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), choose **Devices** > **iOS** > **iOS enrollment** > **Enrollment program tokens** > choose a token > **Sync now**. A sync request is sent to Apple.

### ADE enrollment stuck at user login
When you turn on a ADE-managed device that is assigned an enrollment profile, the initial setup sticks after you enter credentials.

**Cause:** Multi-Factor authentication (MFA) is enabled. Currently MFA doesn't work during enrollment on ADE devices.

#### Resolution
Disable MFA, and then re-enroll the device.


## Next steps

- [Troubleshoot device enrollment in Intune](troubleshoot-device-enrollment-in-intune.md)
- [Ask a question on the Intune forum](https://social.technet.microsoft.com/Forums/%7Blang-locale%7D/home?category=microsoftintune&filter=alltypes&sort=lastpostdesc)
- [Check the Microsoft Intune Support Team Blog](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/bg-p/IntuneCustomerSuccess)
- [Check the Microsoft Enterprise Mobility and Security Blog](https://techcommunity.microsoft.com/t5/Azure-Active-Directory-Identity/Announcing-the-public-preview-of-Azure-AD-group-based-license/ba-p/245210)
