---
# required metadata

title: Troubleshoot policies in Microsoft Intune - Azure | Microsoft Docs
description: See how to use the built-in troubleshoot feature, and read about Common problems or issues and their resolutions when using compliance policies and configuration profiles in Microsoft Intune
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/13/2020
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology:
ms.assetid: 99fb6db6-21c5-46cd-980d-50f063ab8ab8
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

# Troubleshoot policies and profiles and in Intune

Microsoft Intune includes some built-in troubleshooting features. Use these features to help troubleshoot compliance policies and configuration profiles in your environment.

This article lists some common troubleshooting techniques, and describes some issues you may experience.

## Check tenant status

Check the [Tenant Status](../fundamentals/tenant-status.md) and confirm the subscription is Active. You can also view details for active incidents and advisories that may impact your policy or profile deployment.

## Use built-in troubleshooting

1. In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Troubleshooting + support**:

    :::image type="content" source="./media/troubleshoot-policies-in-microsoft-intune/help-and-support-troubleshoot.png" alt-text="In Endpoint Management admin center and Intune, go to Troubleshooting and support.":::

2. Choose **Select user** > select the user having an issue > **Select**.
3. Confirm that **Intune License** and **Account Status** both show green checks:

    :::image type="content" source="./media/troubleshoot-policies-in-microsoft-intune/account-status-intune-license-show-green.png" alt-text="In Intune, select the user and confirm Account status and Intune license show green checks marks for the status.":::

    **Helpful links**:

    - [Assign licenses so users can enroll devices](../fundamentals/licenses-assign.md)
    - [Add users to Intune](../fundamentals/users-add.md)

4. Under **Devices**, find the device having an issue. Review the different columns:

    - **Managed**: For a device to receive compliance or configuration policies, this property must show **MDM** or **EAS/MDM**.

        - If **Managed** isn't set to **MDM** or **EAS/MDM**, then the device isn't enrolled. It doesn't receive compliance or configuration policies until it's enrolled.

        - App protection policies (mobile application management) don't require devices to be enrolled. For more information, see [create and assign app protection policies](../apps/app-protection-policies.md).

    - **Azure AD Join Type**: Should be set to **Workplace** or **AzureAD**.
 
        - If this column is **Not Registered**, there may be an issue with enrollment. Typically, unenrolling and re-enrolling the device resolves this state.

    - **Intune compliant**: Should be **Yes**. If **No** is shown, there may be an issue with compliance policies, or the device isn't connecting to the Intune service. For example, the device may be turned off, or may not have a network connection. Eventually, the device becomes non-compliant, possibly after 30 days.

        For more information, see [get started with device compliance policies](../protect/device-compliance-get-started.md).

    - **Azure AD compliant**: Should be **Yes**. If **No** is shown, there may be an issue with compliance policies, or the device isn't connecting to the Intune service. For example, the device may be turned off, or may not have a network connection. Eventually, the device becomes non-compliant, possibly after 30 days.

        For more information, see [get started with device compliance policies](../protect/device-compliance-get-started.md).

    - **Last check in**: Should be a recent time and date. By default, Intune devices check in every 8 hours.

        - If **Last check in** is more than 24 hours, there may be an issue with the device. A device that can't check in can't receive your policies from Intune.

        - To force check-in:
            - On the Android device, open the Company Portal app > **Devices** > Choose the device from list > **Check Device Settings**.
            - On the iOS/iPadOS device, open the Company portal app > **Devices** > Choose the device from list > **Check Settings**.

        - On a Windows device, open **Settings** > **Accounts** > **Access Work or School** > Select the account or MDM enrollment > **Info** > **Sync**.

    - Select the device to see policy-specific information.

        **Device Compliance** shows the states of compliance policies assigned to the device.

        **Device Configuration** shows the states of configuration policies assigned to the device.

        If the expected policies aren't shown under **Device Compliance** or **Device Configuration**, then the policies aren't targeted correctly. Open the policy, and assign the policy to this user or device.

        **Policy states**:

        - **Not Applicable**: This policy isn't supported on this platform. For example, iOS/iPadOS policies don't work on Android. Samsung KNOX policies don't work on Windows devices.
        - **Conflict**: There's an existing setting on the device that Intune can't override. Or, you deployed two policies with the same setting using different values.
        - **Pending**: The device hasn't checked into Intune to get the policy. Or, the device received the policy but hasn't reported the status to Intune.
        - **Errors**: Look up errors and possible resolutions at [Troubleshoot company resource access problems](../fundamentals/troubleshoot-company-resource-access-problems.md).

        **Helpful links**: 

        - [Ways to deploy device compliance policies](../protect/device-compliance-get-started.md#ways-to-deploy-device-compliance-policies)
        - [Monitor device compliance policies](../protect/compliance-policy-monitor.md)

## You're unsure if a profile is correctly applied

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **All devices** > select the device > **Device configuration**. 

    Every device lists its profiles. Each profile has a **Status**. The status applies when all of the assigned profiles, including hardware and OS restrictions and requirements, are considered together. Possible statuses include:

    - **Conforms**: The device received the profile and reports to Intune that it conforms to the setting.

    - **Not applicable**: The profile setting isn't applicable. For example, email settings for iOS/iPadOS devices don't apply to an Android device.

    - **Pending**: The profile is sent to the device, but hasn't reported the status to Intune. For example, encryption on Android requires the user to enable encryption, and might show as pending.

**Helpful link**: [Monitor configuration device profiles](../configuration/device-profile-monitor.md)

> [!NOTE]
> When two policies with different levels of restriction apply to the same device or user, the more restrictive policy applies.

## Policy troubleshooting resources

- [Troubleshooting iOS/iPadOS or Android policies not applying to devices](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Support-tip-Troubleshooting-iOS-or-Android-policies-not-applying/ba-p/280154) (opens another Microsoft site)
- [Troubleshooting Windows 10 Intune policy failures](https://blogs.technet.microsoft.com/configmgrdogs/2018/08/09/troubleshooting-windows-10-intune-policy-failures/) (opens a blog)
- [Troubleshoot CSP custom settings for Windows 10](https://support.microsoft.com/en-us/help/4055338/troubleshoot-csp-setting-windows-10-computer-intune) (opens another Microsoft site)
- [Windows 10 Group Policy vs Intune MDM policy](https://blogs.technet.microsoft.com/cbernier/2018/04/02/windows-10-group-policy-vs-intune-mdm-policy-who-wins/) (opens another Microsoft site)

## Alert: Saving of Access Rules to Exchange has Failed

**Issue**: You receive the alert **Saving of Access Rules to Exchange has Failed**  in the admin console.

If you create policies in the Exchange On-Premises Policy workspace (Admin console), but are using Office 365, then the configured policy settings aren't enforced by Intune. In the alert, note the policy source. Under the Exchange On-premises Policy workspace, delete the legacy rules. The legacy rules are Global Exchange rules within Intune for on-premises Exchange, and aren't relevant to Office 365. Then, create new policy for Office 365.

[Troubleshoot the Intune on-premises Exchange connector](../protect/troubleshoot-exchange-connector.md) may be a good resource.

## Can't change security policies for enrolled devices

Windows Phone devices don't allow security policies set using MDM or EAS to be reduced in security once you've set them. For example, you set a **Minimum number of character password** to 8, and then try to reduce it to 4. The more restrictive policy is applied to the device.

Windows 10 devices may not remove security policies when you unassign the policy (stop deployment). You may need to leave the policy assigned, and then change the security settings back to the default values.

Depending on the device platform, if you want to change the policy to a less secure value, you may need to reset the security policies.

For example, in Windows 8.1, on the desktop, swipe in from right to open the **Charms** bar. Choose **Settings** > **Control Panel** > **User Accounts**. On the left, select **Reset Security Policies** link, and choose **Reset Policies**.

Other platforms, such as Android, iOS/iPadOS, and Windows Phone 8.1, may need to be retired and re-enrolled to apply a less restrictive policy.

[Troubleshoot device enrollment](../enrollment/troubleshoot-device-enrollment-in-intune.md) may be a good resource.

## PCs using the Intune software client - classic portal

> [!NOTE]
> This section applies to the classic portal. 

### Microsoft Intune policy-related errors in policyplatform.log

For Windows PCs managed with the Intune software client, policy errors in the `policyplatform.log` file may be from non-default settings in the Windows User Account Control (UAC) on the device. Some non-default UAC settings can affect Microsoft Intune client installations and policy execution.

#### Resolve UAC issues

1. Retire the computer. See [Remove devices](../remote-actions/devices-wipe.md).

2. Wait 20 minutes for the client software to be removed.

    > [!NOTE]
    > Don't attempt to remove the client from Programs and Features.

3. On the start menu, type **UAC** to open the User Account Control settings.

4. Move the notification slider to the default setting.

### ERROR: Cannot obtain the value from the computer, 0x80041013

Occurs if the time on the local system is out of sync by five minutes or more. If the time on the local computer is out of sync, secure transactions fail because the time stamps are invalid.

To resolve this issue, set the local system time as close as possible to Internet time. Or, set it to the time on the domain controllers on the network.

## Next steps

[Common issues and resolutions with email profiles](../configuration/troubleshoot-email-profiles-in-microsoft-intune.md)

Get [support help from Microsoft](../fundamentals/get-support.md), or use the [community forums](https://social.technet.microsoft.com/Forums/en-US/home?category=microsoftintune).
