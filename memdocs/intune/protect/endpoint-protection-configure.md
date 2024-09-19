---
# required metadata

title: Configure Endpoint protection settings in Microsoft Intune
description: Create Endpoint protection settings when you create a macOS or Windows 10 device profile in Microsoft Intune.
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 11/14/2023
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
# optional metadata

#ROBOTS:
#audience:

ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
- endpoint-protection
- sub-secure-endpoints
ms.reviewer: mattcall
---

# Add Endpoint protection settings in Intune

With Intune, you can use device configuration profiles to manage common Endpoint protection security features on devices, including:

- Firewall
- BitLocker
- Allowing and blocking apps
- Microsoft Defender and encryption

For example, you can create an Endpoint protection profile that only allows macOS users to install apps from the Mac App Store. Or, enable Windows SmartScreen when running apps on Windows 10/11 devices.

Before you create a profile, review the following articles that detail the Endpoint protection settings Intune can manage for each supported platform:

- [macOS settings](endpoint-protection-macos.md)
- [Windows settings](endpoint-protection-windows-10.md)

## Create a device profile containing Endpoint protection settings

> [!IMPORTANT]
> The macOS endpoint protection template has been deprecated. Existing policies remain unchanged, but you can no longer create new policies using this template. We recommend using the settings catalog to create new configurations policies for FileVault, Firewall, and System Policy Control (Gatekeeper) payloads. For more information, see [macOS settings catalog](../configuration/settings-catalog.md?tabs=sc-search-filter%2Csc-reporting).  

2. Select **Devices** > **Manage devices** > **Configuration** > **Create**.

3. Enter the following properties:

    - **Platform**: Choose the platform of your devices. Your options:

        - **macOS**
        - **Windows 10 and later**

    - **Profile**: Select **Templates** > **Endpoint protection**.

4. Select **Create**.

5. In **Basics**, enter the following properties:

   - **Name**: Enter a descriptive name for the policy. Name your policies so you can easily identify them later. For example, a good policy name might include the profile type and platform.
   - **Description**: Enter a description for the policy. This setting is optional, but recommended.

   Select **Next**.

6. In **Configuration settings**, depending on the platform you chose, the settings you can configure are different. Choose your platform for detailed settings:

   - [macOS settings](endpoint-protection-macos.md)
   - [Windows settings](endpoint-protection-windows-10.md)

7. Select **Next**.

8. In **Assignments**, select the users or groups that will receive your profile. For more information on assigning profiles, see [Assign user and device profiles](../configuration/device-profile-assign.md).

   Select **Next**.

9. In **Applicability Rules**, use the **Rule**, **Property**, and **Value** options to define how this profile applies within assigned groups. Intune applies the profile to devices that meet the rules you enter. For more information about applicability rules, see [Applicability rules](../configuration/device-profile-create.md).

   Select **Next**.

10. In **Review + create**, review your settings. When you select **Create**, your changes are saved, and the profile is assigned. The policy is also shown in the profiles list.

## Add custom Firewall rules for Windows 10/11 devices

When you configure the Windows Firewall as part of a profile that includes endpoint protection rules for Windows 10/11, you can configure custom rules for Firewalls. Custom rules let you expand on the pre-defined set of Firewall rules supported for Windows devices.

When you plan for profiles with custom Firewall rules, consider the following information, which could affect how you choose to group firewall rules in your profiles:

- Each profile supports up to 150 firewall rules. When you use more than 150 rules, create additional profiles, each limited to 150 rules.

- For each profile, if a single rule fails to apply, all rules in that profile are failed and none of the rules are applied to the device.

- When a rule fails to apply, all rules in the profile are reported as failed. Intune cannot identify which individual rule failed.  

The Firewall rules that Intune can manage are detailed in the Windows [Firewall configuration service provider](/windows/client-management/mdm/firewall-csp) (CSP). To review the list of custom firewall settings for Windows devices that Intune supports, see [Custom Firewall rules](endpoint-protection-windows-10.md#firewall-rules).

### To add custom firewall rules to an Endpoint protection profile

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Devices** > **Manage devices** > **Configuration** > **Create**.

3. Enter the following properties:

    - **Platform**: Choose **Windows 10 and later**.

    - **Profile**: Select **Templates** > **Endpoint protection**.

4. Select **Create**.

5. In **Basics**, enter the following properties:

   - **Name**: Enter a descriptive name for the policy. Name your policies so you can easily identify them later. For example, a good policy name might include the profile type and platform.
   - **Description**: Enter a description for the policy. This setting is optional, but recommended.

   Select **Next**.

6. In **Configuration settings**, expand **Windows Firewall**. Next, for *Firewall rules*, select **Add** to open the **Create Rule** page.

7. Specify settings for the Firewall rule, and then select **Save** to save it. To review the available custom firewall rule options in documentation, see [Custom Firewall rules](endpoint-protection-windows-10.md#firewall-rules).

    1. The rule appears on the *Windows Firewall* page in the list of rules.
    2. To modify a rule, select the rule from the list, to open the **Edit Rule** page.
    3. To delete a rule from a profile, select the ellipsis **(…)** for the rule, and then select **Delete**.
    4. To change the order in which rules display, select the *up arrow, down arrow* icon at the top of the rule list.

   Select **Next**.

8. In **Assignments**, select the device groups that will receive this profile. For more information on assigning profiles, see [Assign user and device profiles](../configuration/device-profile-assign.md).

   Select **Next**.

9. In **Applicability Rules**, use the **Rule**, **Property**, and **Value** options to define how this profile applies within assigned groups. Intune applies the profile to devices that meet the rules you enter. For more information about applicability rules, see [Applicability rules](../configuration/device-profile-create.md).

   Select **Next**.

10. In **Review + create**, review your settings. When you select **Create**, your changes are saved, and the profile is assigned. The policy is also shown in the profiles list.

## Next steps

[Monitor the profile status](../configuration/device-profile-monitor.md).
