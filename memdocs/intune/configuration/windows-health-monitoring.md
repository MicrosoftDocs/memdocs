---
# required metadata

title: Create a Windows Health Monitoring profile in Microsoft Intune
description: Add a Windows Health Monitoring profile to collect endpoint analytics and software update events on Windows 10/11 devices in Microsoft Intune. Use these data to recommend software, review startup performance, and fix support issues.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 01/19/2022
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology:

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: 
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Use Windows Health Monitoring profile on Windows devices in Microsoft Intune

Microsoft can collect event data, and provide recommendations to improve performance on your Windows devices. [Endpoint Analytics](../../analytics/overview.md) analyzes this data, and can recommend software, help improve startup performance, and fix common support issues.

In Intune, you can create a Windows Health Monitoring device configuration profile to enable this data collection, and then deploy this profile to your devices.

Use this profile as part of your mobile device management (MDM) solution to optimize your Windows devices.

This feature applies to:

- Windows 11 devices enrolled in Intune
- Windows 10 version 1903 and newer devices enrolled in Intune

This article shows you how to create the profile, and enable the monitoring.

## Create the profile

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **Configuration profiles** > **Create profile**.
3. Enter the following properties:

    - **Platform**: Choose **Windows 10 and later**.
    - **Profile**: Select **Templates** > **Windows health monitoring**.

    > [!NOTE]
    >
    > If you don't see **Windows health monitoring** in the list, then:
    >
    > 1. Go to **Reports** > **Endpoint Analytics** > **Settings**.
    > 2. Select **Intune data collection policy**.

4. Select **Create**.
5. In **Basics**, enter the following properties:

    - **Name**: Enter a descriptive name for the profile. Name your policies so you can easily identify them later. For example, a good profile name is **Windows devices: Windows Health Monitoring profile**.
    - **Description**: Enter a description for the profile. This setting is optional, but recommended.

6. Select **Next**.
7. In **Configuration settings**, configure the following settings:

    - **Health monitoring**: This setting turns on health monitoring to track Windows updates and events. Your options:
      - **Not configured**: Intune doesn't change or update this setting.
      - **Enable**: Event information is collected from the devices, and sent to Microsoft for analytics and insights.
      - **Disable**: Event information isn't collected from the devices.

      [DeviceHealthMonitoring/AllowDeviceHealthMonitoring CSP](/windows/client-management/mdm/policy-csp-devicehealthmonitoring#devicehealthmonitoring-allowdevicehealthmonitoring)

    - **Scope**: Choose the event information you want collected and evaluated. Your options:
      - **Windows updates**: This option configures devices to send Windows Update data to Intune. This data is then used in a [compliance policy](../protect/windows-update-compliance-reports.md) that reports on Windows updates.
      - **Endpoint analytics**

      [DeviceHealthMonitoring/ConfigDeviceHealthMonitoringScope CSP](/windows/client-management/mdm/policy-csp-devicehealthmonitoring#devicehealthmonitoring-configdevicehealthmonitoringscope)

8. Select **Next**.

9. In **Assignments**, select the users or user group that will receive your profile. For more information on assigning profiles, see [Assign user and device profiles](device-profile-assign.md).

    Select **Next**.

10. In **Applicability Rules**, use the **Rule**, **Property**, and **Value** options to define how this profile applies within assigned groups. Intune applies the profile to devices that meet the rules you enter. For more information about applicability rules, see [Applicability rules](device-profile-create.md#applicability-rules).

    Select **Next**.

11. In **Review + create**, review your settings. When you select **Create**, your changes are saved, and the profile is assigned. The policy is also shown in the profiles list.

The next time each device checks in, the policy is applied.

## Next steps

After the [profile is assigned](device-profile-assign.md), be sure to [monitor its status](device-profile-monitor.md).

[What is Endpoint analytics](../../analytics/overview.md)
