---
# required metadata

title: Monitor results of your device compliance policies in Microsoft Intune
description: Use the device compliance dashboard to understand overall device compliance the per-policy and per-setting device compliance results.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 10/19/2022
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: tycast
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier1
- M365-identity-device-management
- highpri
---
# Monitor results of your Intune Device compliance policies

Compliance reports help you understand when devices fail to meet your [compliance policies](../protect/device-compliance-get-started.md) and can help you identify compliance-related issues in your organization. Using these reports, you can view information on:

- The overall compliance states of devices
- The compliance status for an individual setting
- The compliance status for an individual policy
- Drill down into individual devices to view specific settings and policies that affect the device

This article applies to:

- Android device administrator
- Android (AOSP) (*preview*)
- Android Enterprise
- iOS/iPadOS
- Linux - Ubuntu Desktop, version 20.04 LTS and 22.04 LTS
- macOS
- Windows 10 and later

## Open the compliance dashboard

Open the **Intune Device compliance dashboard**:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Devices** > **Overview** > **Compliance status** tab.

> [!IMPORTANT]
> Devices must be enrolled into Intune to receive device compliance policies.

## Dashboard overview

When the dashboard opens, you get an overview with all the compliance reports. In these reports, you can see and check for:

- Overall device compliance
- Per-policy device compliance
- Per-setting device compliance
- Threat agent status
- Device protection status

:::image type="content" source="./media/compliance-policy-monitor/idc-1.png" alt-text="Screenshot of the Microsoft Intune admin center compliance overview and the different reports.":::

As you dig in to this reporting, you can also see any specific compliance policies and settings that apply to a specific device, including the compliance state for each setting.

### Device compliance status

The **Device compliance status** chart shows the compliance states for all Intune enrolled devices. The device compliance states are kept in two different databases: Intune and Azure Active Directory.

> [!IMPORTANT]
> Intune follows the device check-in schedule for all compliance evaluations on the device. [Learn more about the device check-in schedule](../configuration/device-profile-troubleshoot.md#how-long-does-it-take-for-devices-to-get-a-policy-profile-or-app-after-they-are-assigned).

Descriptions of the different device compliance policy states:

- **Compliant**: The device successfully applied one or more device compliance policy settings.

- **In-grace period:** *(This status isn’t supported by Linux)* The device is targeted with one or more device compliance policy settings. But, the user hasn't applied the policies yet. This status means the device is not-compliant, but it's in the grace period defined by the admin.

  - Learn more about [Actions for noncompliant devices](actions-for-noncompliance.md).

- **Not evaluated**: *(This status isn’t supported by Linux)* An initial state for newly enrolled devices. Other possible reasons for this state include:

  - Devices that aren't assigned a compliance policy and don't have a trigger to check for compliance
  - Devices that haven't checked in since the compliance policy was last updated
  - Devices not associated to a specific user, such as:
    - iOS/iPadOS devices purchased through Apple's Device Enrollment Program (DEP) that don't have user affinity
    - Android kiosk or Android Enterprise dedicated devices
  - Devices enrolled with a device enrollment manager (DEM) account

- **Not-compliant:** The device failed to apply one or more device compliance policy settings. Or, the user hasn't complied with the policies.

- **Device not synced:** *(This status isn’t supported by Linux)* The device failed to report its device compliance policy status because one of the following reasons:

  - **Unknown**: The device is offline or failed to communicate with Intune or Azure AD for other reasons.
  - **Error**: The device failed to communicate with Intune and Azure AD, and received an error message with the reason.

- **Checking status**: *(Applies only to Linux)* Intune is currently evaluating the devices compliance your organization’s policies.

> [!IMPORTANT]
> Devices that are enrolled into Intune, but not targeted by any device compliance policies are included in this report under the **Compliant** bucket.

#### Device behavior with a compliance setting in Error state

When a setting for a compliance policy returns a value of **Error**, the compliance state of the device remains unchanged for up to seven days to allow time for the compliance calculation to complete correctly for that setting. Within those seven days, the device's existing compliance status continues to apply until the compliance policy setting evaluates as **Compliant** or **Not compliant**. If a setting still has a status of **Error** after seven days, the device becomes **Not compliant** immediately. Grace periods don't apply to compliance policies with a setting in an **Error** state.

##### Examples:

- A device is initially marked **Compliant**, but then a setting in one of the compliance policies targeted to the device reports **Error**. After three days, compliance evaluation completes successfully and the setting now reports **Not compliant**. The user can continue to use the device to access Conditional Access-protected resources within the first three days after the setting states changes to **Error**, but once the setting returns **Not compliant**, the device is marked **Not compliant** and this access is removed until the device becomes **Compliant** again.

- A device is initially marked **Compliant**, but then a setting in one of the compliance policies targeted to the device reports **Error**. After three days, compliance evaluation completes successfully, the setting returns **Compliant**, and the device's compliance status becomes **Compliant**. The user is able to continue to access Conditional Access protected resources without interruption.

- A device is initially marked **Compliant**, but then a setting in one of the compliance policies targeted to the device reports **Error**. The user is able to access Conditional Access protected resources for seven days, but after seven days, the compliance setting still returns **Error**. At this point, the device becomes Not compliant immediately and the user loses access to the protected resources until the device becomes **Compliant**, even if there's a grace period set for the applicable compliance policy.

- A device is initially marked **Not compliant**, but then a setting in one of the compliance policies targeted to the device reports Error. After three days, compliance evaluation completes successfully, the setting returns **Compliant**, and the device's compliance status becomes **Compliant**. The user is prevented from accessing Conditional Access protected resources for the first three days (while the setting returns **Error**). Once the setting returns **Compliant** and the device is marked **Compliant**, the user can begin to access protected resources on the device.

#### Drill down for more details

In the **Device compliance status** chart, select a status. For example, select the **Not compliant** status:

:::image type="content" source="./media/compliance-policy-monitor/select-not-compliant-status.png" alt-text="Screenshot that shows Choose the not compliant status.":::

That action opens the **Device compliance** window and displays devices in a **Device status** chart. The chart shows you more details on the devices in that state, including operating system platform, last check-in date, and more.

:::image type="content" source="./media/compliance-policy-monitor/drill-down-details.png" alt-text="Dashboard image shows more details on the device in that specific state.":::

If you want to see all the devices owned by a specific user, you can also filter the chart report by typing the user's e-mail.

> [!TIP]
> If no user is signed in to the device, the device with the targeted device compliance policy will send a compliance report back to Intune showing **System Account** as the user principal name. This happens because a device compliance policy was targeted to either a group of users or devices, and no user was signed into the device at the time the compliance policy was evaluated.
>
> Additionally, if there are multiple users signed into the same device, and coincidentally the device is targeted with a compliance policy that is scoped to cover all users that are currently signed in the device, the compliance report might show the same device multiple times as every user signed into the device has to evaluate the device compliance policy and report it back to Intune.


> [!NOTE]
> Be aware that when assigning a compliance policy to a device group, when a user is signed in it will cause two compliance evaluations: one for the user and the one for the System account. In this scenario, the **System Account** evaluation could fail, causing the device to be **"Not compliant"**. To prevent this behavior:
>
> - For devices with a user signed in - assign the compliance policy to a User group.
> - For devices without a user signed in - assign the compliance policy to a Device group.

#### Filter and columns

:::image type="content" source="./media/compliance-policy-monitor/filter-columns.png" alt-text="Select Filter and Column to change the results in the chart.":::

When you select the **Filter** button, the filter fly-out opens with more options, including the **Compliance** state, **Jailbroken** devices, and more. **Apply** the filter to update the results.

Use the **Columns** property to add or remove columns from the chart output. For example, **User principal name** may show the email address registered on the device. **Apply** the columns to update the results.

#### Device details

In the **Device details** chart, select a specific device, and then select **Device compliance**:

:::image type="content" source="./media/compliance-policy-monitor/see-policies-applied-specific-device.png" alt-text="Choose a specific device, and then Device Compliance to see the compliance policies applied.":::

Intune displays more details on the device compliance policy settings applied on that device. When you select the specific policy, it shows all the settings in the policy.

### Devices without compliance

On the *Compliance status* page, next to the *Policy compliance* chart, you can select the **Devices without compliance policy** tile to view information about devices that don't have any compliance policies assigned:

:::image type="content" source="./media/compliance-policy-monitor/devices-without-policies.png" alt-text="See devices without any compliance policies.":::

When you select the tile, it shows all devices without a compliance policy. It also shows the user of the device, the policy deployment status, and the device model.

> [!TIP]  
> In public preview, there is a new organizational report that identifies all devices in your tenant that have not been assigned a compliance report. See [Devices without compliance policy (preview) (Organizational)](../fundamentals/reports.md#devices-without-compliance-policy-preview-organizational).

#### What you need to know

- With the **Mark devices with no compliance policy assigned as** security setting, it's important to identify devices without a compliance policy. Then you can assign at least one compliance policy to them.

  The security setting is configurable in the Microsoft Intune admin center. Go to **Devices** > **Compliance policies** > **Compliance policy settings**. Then, set **Mark devices with no compliance policy assigned as** to **Compliant** or **Not compliant**.

- Users who are assigned a compliance policy of any type aren't shown in the report, regardless of device platform. For example, if you've assigned a Windows compliance policy to a user with an Android device, the device doesn't show up in the report. However, Intune considers that Android device not compliant. To avoid issues, we recommend that you create policies for each device platform and deploy them to all users.

### Per-policy device compliance

The **Policy compliance** chart shows you the policies, and how many devices are compliant and noncompliant.

:::image type="content" source="./media/compliance-policy-monitor/idc-8.png" alt-text="See a list of the policies, and how many compliant vs noncompliant devices for that policy.":::

### Setting compliance

The **Setting compliance** chart shows you all device compliance policy settings from all compliance policies, the platforms the policy settings are applied, and the number of noncompliant devices.

:::image type="content" source="./media/compliance-policy-monitor/idc-10.png" alt-text="See a list of all the settings in the different policies.":::

## View compliance reports

In addition to using the charts on *Compliance status*, you can go to **Reports** > **Device compliance**.

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Devices** > **Monitor**, and then from below **Compliance** select the report you want to view. Some of the available compliance reports include:

   - Device compliance
   - Noncompliant devices
   - Devices without compliance policy
   - Setting compliance
   - Policy compliance
   - Noncompliant policies (preview)
   - Windows health attestation report
   - Threat agent status

For more information about reports, see [Intune reports](../fundamentals/reports.md)

## View status of device policies

You can check the different states of your policies, by platform. For example, you have a macOS compliance policy. You want to see the devices that are impacted by this policy, and know if there are conflicts or failures.

This feature is included in the device status reporting:

1. Select **Devices** > **Compliance policies** > **Policies**. A list of policies is shown, including the platform, if the policy is assigned, and more details.
2. Select a policy > **Overview**. In this view, the policy assignment includes the following statuses:

    - **Succeeded**: Policy is applied
    - **Error**: The policy failed to apply. The message typically displays with an error code that links to an explanation.
    - **Conflict**: Two settings are applied to the same device, and Intune can't sort out the conflict. An administrator should review.
    - **Pending**: The device hasn't checked in with Intune to receive the policy yet.
    - **Not applicable**: The device can't receive the policy. For example, the policy updates a setting specific to iOS 11.1, but the device is using iOS 10.

3. To see details on the devices using this policy, select one of the statuses. For example, select **Succeeded**. In the next window, specific device details, including the device name and deployment status are listed.

## How Intune resolves policy conflicts

Policy conflicts can occur when multiple Intune policies are applied to a device. If the policy settings overlap, Intune resolves any conflicts by using the following rules:

- If the conflict is between settings from an Intune configuration policy and a compliance policy, the settings in the compliance policy take precedence over the settings in the configuration policy. This result happens even if the settings in the configuration policy are more secure.

- If you have deployed multiple compliance policies, Intune uses the most secure of these policies.

To learn more about conflict resolution for policies, see [If multiple policies are assigned to the same user or device, how do I know which settings gets applied?](../configuration/device-profile-troubleshoot.md#if-multiple-policies-are-assigned-to-the-same-user-or-device-how-do-i-know-which-settings-gets-applied).

## Next steps

[Compliance policies overview](device-compliance-get-started.md)