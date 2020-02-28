---
# required metadata

title: Configure endpoint protection settings in Microsoft Intune - Azure | Microsoft Docs
description: Create endpoint protection settings when you create a macOS or Windows 10 device profile in Microsoft Intune.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 11/18/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology:

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
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

## Create a device profile containing endpoint protection settings

1. Sign in to the [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Devices** > **Configuration profiles** > **Create profile**.

3. Enter a **Name** and **Description** for the endpoint protection profile.

4. From the **Platform** drop-down list, select the device platform to which you want to apply custom settings. Currently, you can choose one of the following platforms for device restriction settings:

   - **macOS**
   - **Windows 10 and later**

5. From the **Profile type** drop-down list, choose **Endpoint protection**.

6. Depending on the platform you chose, the settings you can configure are different. See:

   - [macOS settings](endpoint-protection-macos.md)
   - [Windows 10 settings](endpoint-protection-windows-10.md)

7. After you configure applicable settings, select **Create** on the **Create profile** page.

   The profile is created and appears on the profiles list page. To assign this profile to groups, see [assign device profiles](../configuration/device-profile-assign.md).

## Add custom Firewall rules for Windows 10 devices

When you configure the Microsoft Defender Firewall as part of a profile that includes endpoint protection rules for Windows 10, you can configure custom rules for Firewalls. Custom rules let you expand on the pre-defined set of Firewall rules supported for Windows 10.

When you plan for profiles with custom Firewall rules, consider the following information, which could affect how you choose to group firewall rules in your profiles:

- Each profile supports up to 150 firewall rules. When you use more than 150 rules, create additional profiles, each limited to 150 rules.

- For each profile, if a single rule fails to apply, all rules in that profile are failed and none of the rules are applied to the device.

- When a rule fails to apply, all rules in the profile are reported as failed. Intune cannot identify which individual rule failed.  

The Firewall rules that Intune can manage are detailed in the Windows [Firewall configuration service provider]( https://docs.microsoft.com/windows/client-management/mdm/firewall-csp) (CSP). To review the list of custom firewall settings for Windows 10 devices that Intune supports, see [Custom Firewall rules](endpoint-protection-windows-10.md#firewall-rules).

### To add custom firewall rules to an Endpoint protection profile

1. Sign in to the [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Devices** > **Configuration profiles** > **Create Profile**.

3. For *Platform*, select **Windows 10 and later**, and then for *Profile type* select **Endpoint protection**.

4. Select **Microsoft Defender Firewall** to open the configuration page, and then for *Firewall rules* select **Add** to open the **Create Rule** page.

5. Specify settings for the Firewall rule, and then select **OK** to save it. To review the available custom firewall rule options in documentation, see [Custom Firewall rules](endpoint-protection-windows-10.md#firewall-rules).

6. After you save the rule, it appears on the *Microsoft Defender Firewall* page in the list of rules.

7. To modify a rule, select the rule from the list, to open the **Edit Rule** page.

8. To delete a rule from a profile, select the ellipsis **(…)** for the rule, and then select **Delete**.

9. To change the order in which rules display, select the *up arrow, down arrow* icon at the top of the rule list.

## Next steps

To assign a profile to groups, see [assign device profiles](../configuration/device-profile-assign.md).
