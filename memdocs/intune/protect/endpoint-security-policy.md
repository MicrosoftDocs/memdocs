---
# required metadata

title: Manage endpoint security policies in Microsoft Intune | Microsoft Docs
description: Learn how Security Administrators can use the Endpoint Security policies and profiles to focus on security configuration of devices in Microsoft Endpoint Manager. 
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 12/18/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
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
ms.reviewer: mattsha

---

# Manage device security with endpoint security policies in Microsoft Intune

As a security admin, use the security policies from the *Endpoint security* of Intune to configure device security without the overhead of navigating the larger body and range of settings found in device configuration profiles and security baselines.

Each policy type supports one or more profiles. Profiles are where you configure settings and can group settings for different platforms, or for different areas of focus in the larger policy area.

You'll find these policies under *Manage* in the **Endpoint security** node of the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

![Manage policies](./media/endpoint-security-policy/endpoint-security-policies.png)

Following are brief descriptions of each endpoint security policy type. To learn more about them, including the available profiles for each, follow the links to content dedicated to each policy type:

- [Antivirus](../protect/endpoint-security-antivirus-policy.md) - Antivirus policies help security admins focus on managing the discrete group of antivirus settings for managed devices. To use Antivirus policy, integrate Intune with Microsoft Defender for Endpoint as a Mobile Threat Defense solution.

- [Disk encryption](../protect/endpoint-security-disk-encryption-policy.md) - Endpoint security Disk encryption profiles focus on only the settings that are relevant for a devices built-in encryption method, like FileVault or BitLocker. This focus makes it easy for security admins to manage disk encryption settings without having to navigate a host of unrelated settings.

- [Firewall](../protect/endpoint-security-firewall-policy.md) - Use the endpoint security Firewall policy in Intune to configure a devices built-in firewall for devices that run macOS and Windows 10. 

- [Endpoint detection and response](../protect/endpoint-security-edr-policy.md) - When you integrate Microsoft Defender for Endpoint with Intune, use the endpoint security policies for endpoint detection and response (EDR) to manage the EDR settings and onboard devices to Microsoft Defender for Endpoint.

- [Attack surface reduction](../protect/endpoint-security-asr-policy.md) - When Defender antivirus is in use on your Windows 10 devices, use Intune endpoint security policies for Attack surface reduction to manage those settings for your devices.

- [Account protection](../protect/endpoint-security-account-protection-policy.md) - Account protection policies help you protect the identity and accounts of your users. The account protection policy is focused on settings for  Windows Hello and Credential Guard, which is part of Windows identity and access management.

The following sections apply to all of the endpoint security policies.

## Create an endpoint security policy

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Endpoint security** and then select the type of policy you want to configure, and then select **Create Policy**. Choose from the following policy types:
   - Antivirus
   - Disk encryption
   - Firewall
   - Endpoint detection and response
   - Attack surface reduction
   - Account protection

3. Enter the following properties:
   - **Platform**: Choose the platform that you're creating policy for. The available options depend on the policy type you selected:
     - macOS
     - Windows 10 and later
   - **Profile**: Choose from the available profiles for the platform you selected. For information about the profiles, see the dedicated section in this article for your chosen policy type.

4. Select **Create**.

5. On the **Basics** page, enter a name and description for the profile, then choose **Next**.

6. On the **Configuration settings** page, expand each group of settings, and configure the settings you want to manage with this profile.

   When your done configuring settings, select **Next**.

7. On the **Scope tags** page, choose **Select scope tags** to open the *Select tags* pane to assign scope tags to the profile.
  
   Select **Next** to continue.

8. On the **Assignments** page, select the groups that will receive this profile. For more information on assigning profiles, see [Assign user and device profiles](../configuration/device-profile-assign.md).

   Select **Next**.

9. On the **Review + create** page, when you're done, choose **Create**. The new profile is displayed in the list when you select the policy type for the profile you created.

## Duplicate a policy

Endpoint security policies support duplication to create a copy of the original policy. A scenario when duplicating a policy is useful, is if you need to assign similar policies to different groups but don't want to manually recreate the entire policy. Instead, you can duplicate the original policy and then introduce only the changes the new policy requires. You might only change a specific setting and the group the policy is assigned to.

When creating a duplicate, you'll give the copy a new name. The copy is made with the same setting configurations and scope tags as the original, but won't have any assignments. You'll need to edit the new policy later to create assignments.  

The following policy types support duplication:

- Antivirus
- Disk encryption
- Firewall
- Endpoint detection and response
- Attack surface reduction
- Account protection

After creating the new policy, review and edit the policy to make changes to its configuration.

### To duplicate a policy

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select the policy that you want to copy. Next, select **Duplicate** or select the ellipsis (**…**) to the right of the policy and select **Duplicate**.
3. Provide a **New name** for the policy, and then select **Save**.

### To edit a policy

1. Select the new policy, and then select **Properties**.
2. Select Settings to expand a list of the configuration settings in the policy. You can’t modify the settings from this view, but you can review how they're configured.
3. To modify the policy, select **Edit** for each category where you want to make a change:
   - Basics
   - Assignments
   - Scope tags
   - Configuration settings
4. After you’ve made changes, select **Save** to save your edits.  Edits to one category must be saved before you can introduce edits to additional categories.

## Manage conflicts

Many of the device settings that you can manage with Endpoint security policies (security policies) you can manage through other policy types in Intune. These other policy types include *device configuration* policy and *security baselines*. Because you can manage a setting with several different policy types or multiple instances of the same policy type, be prepared to identify and resolve policy conflicts should a device not adhere to the configurations you expect.

- Security baselines can set a non-default value for a setting to comply with the recommended configuration that baseline addresses.
- Other policy types, including the endpoint security policies, set a value of *Not configured* by default. These other policy types require you to explicitly configure settings in the policy.

Regardless of the policy method, managing the same setting on the same device through multiple policy types, or through multiple instances of the same policy type can result in conflicts that should be avoided.

The information at the following links can help you identify and resolve conflicts:

- [Troubleshoot policies and profiles in Intune](/troubleshoot/mem/intune/troubleshoot-policies-in-microsoft-intune)
- [Monitor your security baselines](../protect/security-baselines-monitor.md#troubleshoot-using-per-setting-status)

## Next steps

[Manage endpoint security in Intune](../protect/endpoint-security.md)