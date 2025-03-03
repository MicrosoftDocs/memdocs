---
# required metadata

title: Create a Windows Health Monitoring profile in Microsoft Intune
description: Add a Windows Health Monitoring profile to collect endpoint analytics and software update events on Windows 10/11 devices in Microsoft Intune. Use this data to recommend software, review startup performance, and fix support issues.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 02/19/2025
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
# optional metadata

#ROBOTS:
#audience:

ms.reviewer: 
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
---

# Use Windows Health Monitoring profile on Windows devices in Microsoft Intune

Microsoft can collect event data, and provide recommendations to improve performance on your Windows devices. [Endpoint Analytics](../../analytics/overview.md) analyzes this data, and can recommend software, help improve startup performance, and fix common support issues.

In Intune, you can create a Windows Health Monitoring device configuration profile to enable this data collection, and then deploy this profile to your devices.

To help optimize your Windows devices, use this profile as part of your mobile device management (MDM) solution.

This feature applies to:

- Windows 11 devices enrolled in Intune
- Windows 10 version 1903 and newer devices enrolled in Intune

This article shows you how to create the profile, and enable the monitoring.

## Before you begin

- Endpoint Analytics has its own prerequisites. For more information, including enrollment requirements, go to [What is Endpoint analytics?](../../analytics/overview.md).
- If you use co-management, then to use this profile, the Device Configuration workload must be in Intune. For more information on these features, go to [What is co-management?](../../configmgr/comanage/overview.md) and [Switch Configuration Manager workloads to Intune](../../configmgr/comanage/how-to-switch-workloads.md).
- [!INCLUDE [minimum-rbac-role-policy-profile-manager](../includes/minimum-rbac-role-policy-profile-manager.md)]

## Create the profile

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy**.
3. Enter the following properties:

    - **Platform**: Select **Windows 10 and later**.
    - **Profile type**: Select **Templates** > **Windows health monitoring**.

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

    - **Health monitoring**: This setting turns on health monitoring to track events. Your options:
      - **Not configured**: Intune doesn't change or update this setting.
      - **Enable**: Event information is collected from the devices, and sent to Microsoft for analytics and insights.
      - **Disable**: Event information isn't collected from the devices.

      [DeviceHealthMonitoring/AllowDeviceHealthMonitoring CSP](/windows/client-management/mdm/policy-csp-devicehealthmonitoring#allowdevicehealthmonitoring)

    - **Scope**: Choose the event information you want collected and evaluated. Your option:
      - **Endpoint analytics**

      [DeviceHealthMonitoring/ConfigDeviceHealthMonitoringScope CSP](/windows/client-management/mdm/policy-csp-devicehealthmonitoring#configdevicehealthmonitoringscope)

8. Select **Next**.

9. In **Assignments**, select the devices or device groups that will receive your profile. For more information on assigning profiles, go to [Assign user and device profiles](device-profile-assign.md).

    Select **Next**.

10. In **Applicability Rules**, use the **Rule**, **Property**, and **Value** options to define how this profile applies within assigned groups. Intune applies the profile to devices that meet the rules you enter. For more information about applicability rules, go to [Applicability rules](device-profile-create.md#applicability-rules).

    Select **Next**.

11. In **Review + create**, review your settings. When you select **Create**, your changes are saved, and the profile is assigned. The policy is also shown in the profiles list.

The next time each device checks in, the policy is applied.

## Related content

- After the [profile is assigned](device-profile-assign.md), be sure to [monitor its status](device-profile-monitor.md).
- [What is Endpoint analytics](../../analytics/overview.md)
