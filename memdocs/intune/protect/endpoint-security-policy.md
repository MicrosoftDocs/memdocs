---
# required metadata

title: Manage endpoint security policies in Microsoft Intune
description: Security Administrators can use the Endpoint Security policies and profiles to focus on security configuration of devices in Microsoft Intune. 
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 09/23/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
- highpri
- sub-secure-endpoints
ms.reviewer: laarrizz

---

# Manage device security with endpoint security policies in Microsoft Intune

As a security admin concerned with device security, use Intune endpoint security policies to manage security settings on devices. These profiles are similar in concept to a device configuration policy template or security baseline, which are logical groups of related settings. However where device configuration profiles and security baselines include a large body of diverse settings outside the scope of securing endpoints, each endpoint security profile focuses on a specific subset of device security.

When using endpoint security policies along side other policy types like security baselines or endpoint protection templates from device configuration policies, it’s important to develop a plan for using multiple policy types to minimize the risk of conflicting settings. Security baselines, device configuration policies, and endpoint security policies are all treated as equal sources of device configuration settings by Intune. A settings conflict occurs when a device receives two different configurations for a setting from multiple sources. Multiple sources can include separate policy types and multiple instances of the same policy.

When Intune evaluates policy for a device and identifies conflicting configurations for a setting, the setting that's involved can be flagged for an error or conflict and fail to apply to the device. For information that can help you manage conflicts, see the following policy and profile specific guidance:

- [Device configuration profiles](../configuration/device-profile-monitor.md#view-conflicts)
- [Endpoint security profiles](#manage-conflicts)
- [Security baselines](../protect/security-baselines-monitor.md#resolve-conflicts-for-security-baselines)

## Available types of endpoint security policy

You'll find endpoint security policies under *Manage* in the **Endpoint security** node of the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

:::image type="content" source="./media/endpoint-security-policy/endpoint-security-policies.png" alt-text="Managing Endpoint security policies in the Microsoft Intune admin center":::

Following are brief descriptions of each endpoint security policy type. To learn more about them, including the available profiles for each, follow the links to content dedicated to each policy type:

- [Account protection](../protect/endpoint-security-account-protection-policy.md) - Account protection policies help you protect the identity and accounts of your users. The account protection policy is focused on settings for Windows Hello and Credential Guard, which is part of Windows identity and access management.

- [Antivirus](../protect/endpoint-security-antivirus-policy.md) - Antivirus policies help security admins focus on managing the discrete group of antivirus settings for managed devices.

- [App Control for Business (Preview)](../protect/endpoint-security-app-control-policy.md) - Manage approved apps for Windows devices with App Control for Business policy and Managed Installers for Microsoft Intune. Intune App Control for Business policies are an implementation of Windows Defender Application Control (WDAC).

- [Attack surface reduction](../protect/endpoint-security-asr-policy.md) - When Defender antivirus is in use on your Windows 10/11 devices, use Intune endpoint security policies for Attack surface reduction to manage those settings for your devices.

- [Disk encryption](../protect/endpoint-security-disk-encryption-policy.md) - Endpoint security Disk encryption profiles focus on only the settings that are relevant for a devices built-in encryption method, like FileVault, BitLocker, and Personal Data Encryption (for Windows). This focus makes it easy for security admins to manage disk or folder level encryption settings without having to navigate a host of unrelated settings.

- [Endpoint detection and response](../protect/endpoint-security-edr-policy.md) - When you integrate Microsoft Defender for Endpoint with Intune, use the endpoint security policies for endpoint detection and response (EDR) to manage the EDR settings and onboard devices to Microsoft Defender for Endpoint.

- [Firewall](../protect/endpoint-security-firewall-policy.md) - Use the endpoint security Firewall policy in Intune to configure a devices built-in firewall for devices that run macOS and Windows 10/11.

The following sections apply to all of the endpoint security policies.

## Assign role-based access controls for endpoint security policy

To manage Intune endpoint security policies, you must use an account that includes the Intune role-based access control (RBAC) permission for the policy, and specific rights related to the task you're managing.

> [!NOTE]
>
> Before June of 2024, Intune endpoint security policies were managed through rights provided by the *Security baselines* permission. Beginning in June of 2024, Intune began to release granular permissions to manage individual endpoint security workloads.
>
> Each time a new granular permission for an endpoint security workload is added to Intune, those same rights are removed from the *Security baselines* permission. If you use custom roles with the *Security baselines* permission, the new RBAC permission is assigned automatically to your custom roles with the same rights that were granted through the *Security baseline* permission. This auto-assignment ensures your admins continue to have the same permissions they have today.

### RBAC roles and permissions to manage endpoint security workloads

When you assign RBAC permission for managing aspects of endpoint security, we recommend assigning administrators the minimum permissions required to accomplish specific tasks. Each of the RBAC permissions that manage endpoint security includes the following rights, which can be individually granted or withheld when creating a [custom RBAC role](../fundamentals/create-custom-role.md):

- Assign
- Create
- Delete
- Read
- Update
- View Reports

#### Use custom RBAC roles

The following permissions include rights to endpoint security workloads:

- **Application control for Business** - Grants rights to manage [Application control](../protect/endpoint-security-account-protection-policy.md) policies and reports.

- **Attack surface reduction** - Grants rights to manage some but not all [Attack surface reduction](../protect/endpoint-security-asr-policy.md) policies and reports. For this workload, the following profiles (Templates) continue to require rights provided by the *Security baselines* permission:
  - Windows App and browser isolation
  - Windows Web protection
  - Windows Application control
  - Windows Exploit protection

- **Endpoint detection and response** - Grants rights to manage [Endpoint detection and response](../protect/endpoint-security-edr-policy.md) (EDR) policies and reports.

- **Security baselines** - Grants rights to manage all endpoint security workloads that don't have a dedicated workflow.

- **Device configurations** - The *View Reports* right for Device configurations also grants rights to view, generate, and export reports for endpoint security policies.

> [!IMPORTANT]
>
> The granular permission of *Antivirus* for endpoint security policies might be temporarily visible in some Tenants. This permission is not released and isn't supported for use. Configurations of the Antivirus permission are ignored by Intune. When Antivirus becomes available to use as a granular permission, it's availability will be announced in the [What's new in Microsoft Intune](../fundamentals/whats-new.md) article.

#### Use built-in RBAC roles

The following Intune built-in RBAC roles can also be assigned to admins to provide rights to manage some or all tasks for endpoint security workloads and reports.

- **Help Desk Operator**
- **Read Only Operator**
- **Endpoint Security Manager**

For more information about the specific permissions and rights each role includes, see [Built-in role permissions for Microsoft Intune](../fundamentals/role-based-access-control-reference.md).

### Considerations for new endpoint security permissions

When new granular permissions for endpoint security workloads are added, the new workload permission has the same permission and rights structure as the *Security baselines* permission does today. This includes management of the security policies within those workloads, which can contain overlapping settings in other types of policies like Security baseline policies or Settings catalog policies, which are governed by separate RBAC permissions.

If you use the [Defender for Endpoint security settings management](../protect/mde-security-integration.md) scenario, the same RBAC permission changes apply to the Microsoft Defender portal for security policy management.

## Create an endpoint security policy

The following procedure provides general guidance for creating endpoint security policies:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Endpoint security** and then select the type of policy you want to configure, and then select **Create Policy**. Choose from the following policy types:
   - Account protection
   - Antivirus
   - Application control (Preview)
   - Attack surface reduction
   - Disk encryption
   - Endpoint detection and response
   - Firewall

3. Enter the following properties:
   - **Platform**: Choose the platform that you're creating policy for. The available options depend on the policy type you select.
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

- Account protection
- Application Control (preview)
- Antivirus
- Attack surface reduction
- Disk encryption
- Endpoint detection and response
- Firewall

After creating the new policy, review and edit the policy to make changes to its configuration.

### To duplicate a policy

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Locate the policy that you want to copy from the policy list, and then select the ellipsis (**…**) for that line to open the *Context menu*.
3. Select **Duplicate**.
4. Provide a **New name** for the policy, and then select **Save**.

### To edit a policy

1. Select the new policy, and then select **Properties**.
2. Select Settings to expand a list of the configuration settings in the policy. You can’t modify the settings from this view, but you can review how they're configured.
3. To modify the policy, select **Edit** for each category where you want to make a change:
   - Basics
   - Assignments
   - Scope tags
   - Configuration settings
4. After making changes, select **Save** to save your edits. Edits to one category must be saved before you can introduce edits to additional categories.

## Manage conflicts

Many of the device settings that you can manage with Endpoint security policies (security policies) are also available through other policy types in Intune. These other policy types include *device configuration* policy and *security baselines*. Because settings can be managed through several different policy types or by multiple instances of the same policy type, be prepared to identify and resolve policy conflicts for devices that don't adhere to the configurations you expect.

- Security baselines can set a non-default value for a setting to comply with the recommended configuration that baseline addresses.
- Other policy types, including the endpoint security policies, set a value of *Not configured* by default. These other policy types require you to explicitly configure settings in the policy.

Regardless of the policy method, managing the same setting on the same device through multiple policy types, or through multiple instances of the same policy type can result in conflicts that should be avoided.

The information at the following links can help you identify and resolve conflicts:

- [Troubleshoot policies and profiles in Intune](/troubleshoot/mem/intune/troubleshoot-policies-in-microsoft-intune)
- [Monitor your security baselines](../protect/security-baselines-monitor.md#troubleshoot-using-per-setting-status)

## Next steps

[Manage endpoint security in Intune](../protect/endpoint-security.md)
