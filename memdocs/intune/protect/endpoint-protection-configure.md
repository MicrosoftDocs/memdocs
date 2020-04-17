---
# required metadata

title: Configure endpoint protection settings in Microsoft Intune - Azure | Microsoft Docs
description: Create endpoint protection settings when you create a macOS or Windows 10 device profile in Microsoft Intune.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/24/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology:

# optional metadata

#ROBOTS:
#audience:

ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
mr.reviewer: karthib
---

# Add endpoint protection settings in Intune

With Intune, you can use device configuration profiles to manage common endpoint protection security features on devices, including:

- Firewall
- BitLocker
- Allowing and blocking apps
- Microsoft Defender and encryption

For example, you can create an endpoint protection profile that only allows macOS users to install apps from the Mac App Store. Or, enable Windows SmartScreen when running apps on Windows 10 devices.

Before you create a profile, review the following articles that detail the endpoint protection settings Intune can manage for each supported platform:

- [macOS settings](endpoint-protection-macos.md)
- [Windows 10 settings](endpoint-protection-windows-10.md)

> [!NOTE]
> The Intune user interface (UI) is updating to a full screen experience, and may take several weeks. Until your tenant receives this update, you will have a slightly different workflow when you create or edit settings described in this article.

## Create a device profile containing endpoint protection settings

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Devices** > **Configuration profiles** > **Create profile**.

3. Enter the following properties:

    - **Platform**: Choose the platform of your devices. Your options:

        - **macOS**
        - **Windows 10 and later**

    - **Profile**: Select **Endpoint protection**.

4. Select **Create**.
5. In **Basics**, enter the following properties:

   - **Name**: Enter a descriptive name for the policy. Name your policies so you can easily identify them later. For example, a good policy name might include the profile type and platform.

   - **Description**: Enter a description for the policy. This setting is optional, but recommended.

6. Select **Next**.

7. In **Configuration settings**, depending on the platform you chose, the settings you can configure are different. Choose your platform for detailed settings:

   - [macOS settings](endpoint-protection-macos.md)
   - [Windows 10 settings](endpoint-protection-windows-10.md)

8. Select **Next**.
9. In **Scope tags** (optional), assign a tag to filter the profile to specific IT groups, such as `US-NC IT Team` or `JohnGlenn_ITDepartment`. For more information about scope tags, see [Use RBAC and scope tags for distributed IT](../fundamentals/scope-tags.md).

    Select **Next**.

10. In **Assignments**, select the users or groups that will receive your profile. For more information on assigning profiles, see [Assign user and device profiles](../configuration/device-profile-assign.md).

    Select **Next**.

11. In **Review + create**, review your settings. When you select **Create**, your changes are saved, and the profile is assigned. The policy is also shown in the profiles list.

## Add custom Firewall rules for Windows 10 devices

When you configure the Microsoft Defender Firewall as part of a profile that includes endpoint protection rules for Windows 10, you can configure custom rules for Firewalls. Custom rules let you expand on the pre-defined set of Firewall rules supported for Windows 10.

When you plan for profiles with custom Firewall rules, consider the following information, which could affect how you choose to group firewall rules in your profiles:

- Each profile supports up to 150 firewall rules. When you use more than 150 rules, create additional profiles, each limited to 150 rules.

- For each profile, if a single rule fails to apply, all rules in that profile are failed and none of the rules are applied to the device.

- When a rule fails to apply, all rules in the profile are reported as failed. Intune cannot identify which individual rule failed.  

The Firewall rules that Intune can manage are detailed in the Windows [Firewall configuration service provider](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp) (CSP). To review the list of custom firewall settings for Windows 10 devices that Intune supports, see [Custom Firewall rules](endpoint-protection-windows-10.md#firewall-rules).

### To add custom firewall rules to an Endpoint protection profile

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Devices** > **Configuration profiles** > **Create Profile**.

3. For *Platform*, select **Windows 10 and later**, and then for *Profile* select **Endpoint protection**.

    Select **Create**.

4. Enter a **Name** for your profile > **Next**.
5. In **Configuration settings**, select **Microsoft Defender Firewall**. For *Firewall rules*, select **Add** to open the **Create Rule** page.

6. Specify settings for the Firewall rule, and then select **OK** to save it. To review the available custom firewall rule options in documentation, see [Custom Firewall rules](endpoint-protection-windows-10.md#firewall-rules).

    1. The rule appears on the *Microsoft Defender Firewall* page in the list of rules.
    2. To modify a rule, select the rule from the list, to open the **Edit Rule** page.
    3. To delete a rule from a profile, select the ellipsis **(…)** for the rule, and then select **Delete**.
    4. To change the order in which rules display, select the *up arrow, down arrow* icon at the top of the rule list.

7. Select **Next** until you get to **Review + create**. When you select **Create**, your changes are saved and the profile is assigned. The policy is also shown in the profiles list.

## Next steps

The profile is created, but it may not be doing anything yet. Next, [assign the profile](../configuration/device-profile-assign.md) and [monitor its status](../configuration/device-profile-monitor.md).
