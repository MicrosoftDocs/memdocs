---
# required metadata

title: Create a Windows Network Boundary profile in Microsoft Intune
description: Add a Windows Network Boundary profile to add trusted sites, trusted domains, IPv4 and IPv6 ranges, and proxy servers on Windows 10/11 devices in Microsoft Intune. Sites in this boundary are trusted by Microsoft Defender Application Guard in Microsoft Edge.
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

ms.reviewer: mikedano
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
---

# Use a network boundary to add trusted sites on Windows devices in Microsoft Intune

When using Microsoft Defender Application Guard and Microsoft Edge, you can protect your environment from sites that aren't trusted by your organization. This feature is called a network boundary. It allows you to add network domains, IPV4 and IPv6 ranges, proxy servers, and more to your network boundary. Items in this boundary are trusted.

In Intune, you can create a network boundary profile, and deploy the profile to your devices.

For more information on using Microsoft Defender Application Guard in Intune, see [Windows client settings to protect devices using Intune](../protect/endpoint-protection-windows-10.md#microsoft-defender-application-guard).

This feature applies to:

- Windows 11 devices enrolled in Intune
- Windows 10 devices enrolled in Intune

This article shows you how to create the profile, and add trusted sites.

## Before you begin

This feature uses the [NetworkIsolation CSP](/windows/client-management/mdm/policy-csp-networkisolation).

## Create the profile

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **Configuration profiles** > **Create profile**.
3. Enter the following properties:

    - **Platform**: Select **Windows 10 and later**.
    - **Profile**: Select **Templates** > **Network boundary**.

4. Select **Create**.
5. In **Basics**, enter the following properties:

    - **Name**: Enter a descriptive name for the profile. Name your policies so you can easily identify them later. For example, a good profile name is **Windows devices: Network boundary profile**.
    - **Description**: Enter a description for the profile. This setting is optional, but recommended.

6. Select **Next**.
7. In **Configuration settings**, configure the following settings:

    - **Boundary type**: This setting creates an isolated network boundary. Sites in this boundary are considered trusted by Microsoft Defender Application Guard. Your options:
      - **IPv4 range**: Enter a comma-separated list of IPv4 ranges of devices in your network. Data from these devices is considered part of your organization, and is protected. These locations are considered a safe destination for organization data to be shared to.
      - **IPv6 range**: Enter a comma-separated list of IPv6 ranges of devices in your network. Data from these devices is considered part of your organization, and is protected. These locations are considered a safe destination for organization data to be shared to.
      - **Cloud resources**: Enter a pipe-separated list of organization resource domains hosted in the cloud that you want protected.
      - **Network domains**: Enter a comma-separated list of domains that create the boundaries. Data from any of these domains is sent to a device, is considered organization data, and is protected. These locations are considered a safe destination for organization data to be shared to. For example, enter `contoso.sharepoint.com, contoso.com`.
      - **Proxy servers**: Enter a comma-separated list of proxy servers. Any proxy server in this list is at the internet-level, and not internal to the organization. For example, enter `157.54.14.28, 157.54.11.118, 10.202.14.167, 157.53.14.163, 157.69.210.59`.
      - **Internal proxy servers**: Enter a comma-separated list of internal proxy servers. The proxies are used when adding **Cloud resources**. They force traffic to the matched cloud resources. For example, enter `157.54.14.28, 157.54.11.118, 10.202.14.167, 157.53.14.163, 157.69.210.59`.
      - **Neutral resources**: Enter a list of domain names that can be used for work resources or personal resources.

    - **Value**: Enter your list.
    - **Auto detection of other enterprise proxy servers**: **Disable** prevents devices from automatically detecting proxy servers that aren't in the list. The devices accept the configured list of proxies. When set to **Not configured** (default), Intune doesn't change or update this setting.
    - **Auto detection of other enterprise IP ranges**: **Disable** prevents devices from automatically detecting IP ranges that aren't in the list. The devices accept the configured list of IP ranges. When set to **Not configured** (default), Intune doesn't change or update this setting.

8. Select **Next**.

9. In **Scope tags** (optional), assign a tag to filter the profile to specific IT groups, such as `US-NC IT Team` or `JohnGlenn_ITDepartment`. For more information about scope tags, see [Use RBAC and scope tags for distributed IT](../fundamentals/scope-tags.md).

    Select **Next**.

10. In **Assignments**, select the users or user group that will receive your profile. For more information on assigning profiles, see [Assign user and device profiles](device-profile-assign.md).

    Select **Next**.

11. In **Review + create**, review your settings. When you select **Create**, your changes are saved, and the profile is assigned. The policy is also shown in the profiles list.

The next time each device checks in, the policy is applied.

## Next steps

After the [profile is assigned](device-profile-assign.md), be sure to [monitor its status](device-profile-monitor.md).

[Microsoft Defender Application Guard overview](/windows/security/threat-protection/microsoft-defender-application-guard/md-app-guard-overview)
