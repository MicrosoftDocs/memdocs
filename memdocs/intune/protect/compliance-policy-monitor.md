---
# required metadata

title: Monitor results of your device compliance policies in Microsoft Intune
description: Use the device compliance dashboard to understand overall device compliance the per-policy and per-setting device compliance results.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 08/21/2023
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

Intune includes the following options for reviewing device compliance details:

- Device compliance status dashboard
- Policy-based device compliance reports
- Organizational and operational compliance reports

## Important concepts for device compliance policies and status results

When viewing compliance status details and reports, be aware of the following important details that can affect how a device's compliance status is reported:

- Devices must be enrolled into Intune to receive device compliance policies.

- Intune follows the device check-in schedule for all compliance evaluations on the device. [Learn more about the device check-in schedule](../configuration/device-profile-troubleshoot.md#policy-refresh-intervals).

- The tenant-wide [compliance policy settings](../protect/device-compliance-get-started.md#compliance-policy-settings) include the setting **Mark devices with no compliance policy assigned as**. By default, this setting marks the devices that haven't been assigned a compliance policy as *Compliant*. If it's important for your organization to identify devices that aren't assigned a compliance policy, consider editing this setting.

- At times a device might send a compliance report back to Intune that shows **System Account** as the user principal name. This result can happen when a compliance policy targets a group of users or devices and is evaluated at a time when there's no user is signed into the device.

- Similarly, when a compliance policy is assigned to a *device* group and evaluated while a user is signed in, there are two compliance evaluations: one for the user and the one for the devices System account. In this scenario, the *System Account* evaluation can fail, causing the device to be **Not compliant**. To prevent this behavior:

  - For devices with a user signed in - assign the compliance policy to a User group.
  - For devices without a user signed in - assign the compliance policy to a Device group.

- When there are multiple users signed into the same device, and that device is assigned a compliance policy that is scoped to all users that are currently signed in the device, compliance runs for each of those users. This can result in compliance reports showing multiple entries for the device where each entry indicates a different user name.

- Users of a device type who are assigned a compliance policy for a different device type than they use aren't shown in reports. For example, if you've assigned a Windows compliance policy to a user with an Android device, that compliance policy doesn't run on the user's Android device and the devices previous compliance state remains unchanged.

## Device compliance dashboard

The device compliance dashboard is found in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by navigating to **Devices** > **Overview** and then selecting the **Compliance status** tab. The *Compliance status* tab is a dashboard with several tiles that present high-level summaries for the following compliance report details:

- [Device compliance status](#device-compliance-status)
- [Devices without compliance](#devices-without-compliance)
- [Policy compliance](#policy-compliance)
- [Setting compliance](#setting-compliance)

:::image type="content" source="./media/compliance-policy-monitor/compliance-status-tab.png" alt-text="Image of the Intune admin center that shows the charts available on the Compliance status tab.":::

### Device compliance status

The **Device compliance status** tile displays the compliance states for all Intune enrolled devices.
If you select this tile, Intune displays the **Noncompliant devices** report that can also be found under the **Devices** > **Monitor** node of the admin center.

The tile displays a count of devices for each of the following categories:

- **Compliant**: The device successfully applied one or more device compliance policy settings.

- **In-grace period**: The device is targeted with one or more device compliance policy settings but isn't yet compliant to all of them. Often this is due to users not applying compliant configurations, like meeting password complexity requirements. Devices with this status are noncompliant, but in the grace period defined by the admin.

 Learn more about [Actions for noncompliant devices](../protect/actions-for-noncompliance.md).

- **Not evaluated**: An initial state for newly enrolled devices. Other possible reasons for this state include:
  - Devices that aren't assigned a compliance policy and don't have a trigger to check for compliance.
  - Devices that haven't checked in since the compliance policy was last updated.
  - Devices not associated to a specific user, such as:
    - iOS/iPadOS devices purchased through Apple's Device Enrollment Program (DEP) that don't have user affinity.
    - Android kiosk or Android Enterprise dedicated devices.
  - Devices enrolled with a device enrollment manager (DEM) account.

- **Not compliant**: The device failed to apply one or more device compliance policy settings, or the user hasn't complied with the policies.

### Policy compliance

The **Policy compliance** tile displays the list of compliance policies that are assigned to devices, and the count of compliant and noncompliant devices for each policy.

:::image type="content" source="./media/compliance-policy-monitor/idc-8.png" alt-text="Screen shot that shows the list of policies and how many devices are compliant or noncompliant for each policy.":::

You can select a policy from this tile to open a Policy Compliance view that provides more details about that policy.

> [!TIP]
> We recommend using the newer [Policy compliance (preview)](../fundamentals/reports.md#policy-compliance-preview) report that replaces this view and includes improved capabilities. Eventually, the older report version will be retired.

### Devices without compliance

The **Devices without compliance policy** tile displays a count of devices that don't have any compliance policies assigned. The tile name is often truncated in the admin center view as this tile displays only a count of devices:

:::image type="content" source="./media/compliance-policy-monitor/devices-without-compliance-policy-tile.png" alt-text="Image of the Devices without compliance policy tile.":::

If you select this tile, Intune displays a *Device status* view that lists each device that doesn’t have a compliance policy. This view includes the *Device* name, the *User Principal Name* associated with the device, the devices compliance *Status*, and the *Device model*.

> [!TIP]  
> Intune includes an organizational report that identifies all devices in your tenant that have not been assigned a compliance policy. See [Devices without compliance policy (Organizational)](../fundamentals/reports.md#devices-without-compliance-policy-organizational).

### Setting compliance

The **Setting compliance** tile displays all the device compliance policy settings from all compliance policies, the platforms the policy settings apply to, and the number of noncompliant devices. At least one device must report a status for a setting before the setting is visible in this view.

Screenshot that shows the list of policies and how many devices are compliant or noncompliant for each policy
:::image type="content" source="./media/compliance-policy-monitor/idc-10.png" alt-text="Screen shot that shows the list of all the settings from all compliance policies.":::

You can select an individual setting to open a setting detail view that provides more information about devices that report status for that setting.

> [!TIP]
> We recommend using the newer [Setting compliance (preview)](../fundamentals/reports.md#settings-compliance-preview) report that replaces this report and includes improved capabilities. Eventually, this older report version will be retired.

## Policy-based device compliance reports

Each compliance policy you create directly supports compliance reporting. To view the reports for an individual policy, in the admin center go to **Devices** > **Compliance Policies** > **Policies**, and then select the policy for which you want to view its report details.

By default, when you select a policy Intune opens the Monitor tab for that policy, where Intune displays:

- **Device status** - A simple bar chart that identifies the basic compliance status for devices that receive this policy.
- **View report** - A button you can select that opens the device status report where you can view deeper details about device compliance to this policy.
- **Per-setting status** - A tile you can select that opens the per-setting status report for this policy.

:::image type="content" source="./media/compliance-policy-monitor/select-compliance-policy.png" alt-text="View of the Intune admin center after selecting a compliance policy. ":::

> [!TIP]
> After navigating to the *Monitor* tab of the *Compliance policies* > *Policies* node, you can select the **Properties** tab.
>
> On the Properties tab you’ll see essential details about the policy like the policies name and platform type, as well as the configuration of each setting in that policy. On this tab you can choose to edit different details for the policy including the settings configurations, policy assignments, and more.

### Device status

The *Device status* summary is the default view that’s available when you select a compliance policy. This summary is a simple chart that presents a count of devices that report a specific device compliance status. The horizontal bar is divided into colors from the available categories in proportion to the count of devices in each category. In the preceding screen capture, all devices are compliant. As a result, the representational bar is entirely green.

Before a device is represented in this chart view, the device must check in with Intune to receive the policy, process it, and successfully report back its status. This process can take up to 24 hours when the device is online.

Details in the Device status chart include:

- **Compliant** - The device successfully applied one or more device compliance policy settings.
- **Noncompliant** - The device configuration has failed to meet one or more device compliance policy settings.
- **Others** - The device is in a state that is neither compliant or noncompliant with the settings in this policy, such as *Error* or *Not evaluated*.
- **Total** - The total number of devices that have received this policy and reported in.

To view more details, you can select the **View report** button.

### View report

When you select the *View report* button on the device status view of a policy, Intune displays a more detailed view of the device status for that policy.

:::image type="content" source="./media/compliance-policy-monitor/view-report-for-compliance-policy.png" alt-text="View of the detailed device status report, after selecting the View report button in the Intune admin center.":::

By default, the report view displays details for the following, though you can add more columns of detail can to the view:

- **Device name** - The name of the device as it appears when viewing Devices and creating groups.
- **Logged in user**
- **Policy compliance status** - This status identifies if the device is compliant to this policy, but doesn't represent a device's compliance for any other compliance policies. A device could still be considered noncompliant by Intune should it be noncompliant to a different policy.
- **Device Id** - The device's Intune Device ID.
- **OS** - The operating system of the device, like *Windows*, or *Android*.
- **Last contacted** - The last day and time that this device made contact with the Intune service.

In this report view:

- Each column can be sorted alphabetically.
- You can configure *Filters* and specify a *Search* string to refine the reports results. Search looks through all displayed columns.

 For example, in the previous policy report view, when we enter a search string of **st1** which appears in both the *Device name* and *Logged in user* columns. The resulting view displays both devices that contain *st1* as well as each device associated with the user with *st1* in their user name:

 :::image type="content" source="./media/compliance-policy-monitor/filtered-search-results.png" alt-text="A screen capture that shows filtered search results for the device status report view.":::

### Per-setting status

After selecting a compliance policy, you can select the *Per-setting status* tile to open the device compliance per-setting status view for that policy. This view displays the settings that the policy configures with columns for the various status conditions that can be reported. For each setting, each status column displays a count of devices that report that status.

The following image displays a per-setting view of a policy for Android devices. This policy includes one setting and was deployed to four devices, all of which are compliant to that setting. In this view, you can sort by selecting a column, or using search:

:::image type="content" source="./media/compliance-policy-monitor/view-report-for-per-setting-status.png" alt-text="Screen shot that shows the detailed per-setting status report, after selecting the View report button in the Intune admin center.":::

From the per-setting view, you can select the device count from any status column to open a view with more details for that specific setting and status. The following image displays the results of having selected the number **4** from the **Compliant devices** column"

:::image type="content" source="./media/compliance-policy-monitor/per-status-drill-in.png" alt-text="Screen shot that displays the results of drilling into a per-setting status result to view details for devices that have reported that status.":::

In the screenshot we see there are four entries for the selected setting, with each entry representing a distinct device. This count of devices matches the initial count on the initial per-status view.

We can also see that one device, which has a name that starts with **st1**, has been flagged in the *Device compliance* column as being **Not compliant**. This result is worth examining more closely:

- The details in the Device compliance column represent a device's overall compliance status, and not necessarily a device's compliance with this policy or this setting from this policy.
- We can be assured that this device is compliant to how this setting is configured in this policy because we're viewing a list of devices that reported as being compliant to the settings for this policy.
- This result indicates that the device is failing compliance against some other policy.

Because this drill-in view doesn’t support a deeper drill through, you must use the other compliance reports that are available to determine which policy and setting the device is reporting as noncompliant.

#### Device behavior with a compliance setting in Error state

When a setting for a compliance policy returns a value of **Error**, the compliance state of the device remains unchanged for up to seven days to allow time for the compliance calculation to complete correctly for that setting. Within those seven days, the device's existing compliance status continues to apply until the compliance policy setting evaluates as **Compliant** or **Not compliant**. If a setting still has a status of **Error** after seven days, the device becomes **Not compliant** immediately.

**Examples**:

- A device is initially marked **Compliant**, but then a setting in one of the compliance policies targeted to the device reports **Error**. After three days, compliance evaluation completes successfully and the setting now reports **Not compliant**. The user can continue to use the device to access Conditional Access-protected resources within the first three days after the setting states changes to **Error**, but once the setting returns **Not compliant**, the device is marked **Not compliant** and this access is removed until the device becomes **Compliant** again.

- A device is initially marked **Compliant**, but then a setting in one of the compliance policies targeted to the device reports **Error**. After three days, compliance evaluation completes successfully, the setting returns **Compliant**, and the device's compliance status becomes **Compliant**. The user is able to continue to access Conditional Access protected resources without interruption.

- A device is initially marked **Compliant**, but then a setting in one of the compliance policies targeted to the device reports **Error**. The user is able to access Conditional Access protected resources for seven days, but after seven days, the compliance setting still returns **Error**. At this point, the device becomes Not compliant immediately and the user loses access to the protected resources until the device becomes **Compliant**, even if there's a grace period set for the applicable compliance policy.

- A device is initially marked **Not compliant**, but then a setting in one of the compliance policies targeted to the device reports Error. After three days, compliance evaluation completes successfully, the setting returns **Compliant**, and the device's compliance status becomes **Compliant**. The user is prevented from accessing Conditional Access protected resources for the first three days (while the setting returns **Error**). Once the setting returns **Compliant** and the device is marked **Compliant**, the user can begin to access protected resources on the device.

## Organizational and operational compliance reports

In addition to reports that are available through individual compliance policies, you can view reports for device compliance that focus on the settings in your compliance policies that list all the devices that are noncompliant, and that provide insights to compliance trends.

To view these reports, open the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Reports** > **Device compliance**, and select the **Reports** tab.

For more information about these reports, see [Device compliance reports](../fundamentals/reports.md#device-compliance-reports) in the **Intune reports** article.

## Other compliance reports

In addition to reports from the *Compliance status* tab and from the *Reports* node of the admin center, the following older compliance reports are available. The following reports are  found under the *Compliance* category in the admin center at **Devices** > **Monitor**:

- Noncompliant devices
- Setting compliance – This report version remains available but will be deprecated as there is an updated version with enhanced capabilities. See the updated report at [Setting compliance (preview)](../fundamentals/reports.md#settings-compliance-preview)
- Policy compliance – This report version remains available but will be deprecated as there is an updated version with enhanced capabilities.  [Policy compliance (preview)](../fundamentals/reports.md#policy-compliance-preview)
- Policy noncompliance
- Windows health attestation report

## How Intune resolves policy conflicts

Policy conflicts can occur when multiple Intune policies are applied to a device. If the policy settings overlap, Intune resolves any conflicts by using the following rules:

- If the conflict is between settings from an Intune configuration policy and a compliance policy, the settings in the compliance policy take precedence over the settings in the configuration policy. This result happens even if the settings in the configuration policy are more secure.

- If you have deployed multiple compliance policies, Intune uses the most secure of these policies.

To learn more about conflict resolution for policies, see [Compliance and device configuration policies that conflict](../configuration/device-profile-troubleshoot.md#compliance-and-device-configuration-policies-that-conflict).

## Next steps

[Compliance policies overview](device-compliance-get-started.md)