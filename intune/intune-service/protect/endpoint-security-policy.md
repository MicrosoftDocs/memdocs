---
title: Manage endpoint security policies in Microsoft Intune
description: Security Administrators can use the Endpoint Security policies and profiles to focus on security configuration of devices in Microsoft Intune.
author: brenduns
ms.author: brenduns
ms.date: 12/04/2025
ms.topic: how-to
ms.collection:
- M365-identity-device-management
- highpri
- sub-secure-endpoints
ms.reviewer: laarrizz

---

# Manage device security with endpoint security policies in Microsoft Intune

As a security administrator, use Intune endpoint security policies to configure and manage security settings on your managed devices. Endpoint security policies are purpose-built security profiles that focus on specific device security scenarios, providing a streamlined approach to implementing and managing security controls across your organization.

Compared to managing security settings through device configuration policies, endpoint security policies offer several key advantages:

- **Focused security management**: Each policy type targets specific security areas (antivirus, firewall, disk encryption, etc.) without the complexity of broader device configuration profiles.
- **Security-first approach**: Purpose-built policies designed specifically for security scenarios rather than general device management.
- **Organized by security function**: Grouped by security workload (antivirus, firewall, etc.) rather than mixed with general device management settings.
- **Comprehensive monitoring**: Built-in reporting and conflict detection to ensure security policies deploy successfully.

## Understanding endpoint security policy integration

When implementing endpoint security policies alongside other Intune policy types, plan your approach to minimize configuration conflicts. All Intune policy types are treated as equal sources of device configuration settings, meaning conflicts occur when a device receives different configurations for the same setting from multiple policies.

**Common conflict scenarios**:

- **Security baselines** can set non-default values for settings to comply with recommended configurations, while endpoint security and device configuration policies typically default to *Not configured* - mixing these approaches can create conflicts ([resolve conflicts](../protect/security-baselines-monitor.md#resolve-conflicts-for-security-baselines)).
- **Device configuration policies** managing the same settings as endpoint security policies ([resolve conflicts](../configuration/device-profile-monitor.md#view-conflicts)).
- **Multiple endpoint security policies** setting different values for the same setting ([manage conflicts](#manage-policy-conflicts)).

When conflicts occur, affected settings might fail to apply properly. Plan your policy architecture and use the linked guidance to identify and resolve conflicts.

## Available endpoint security policy types

Access endpoint security policies from **Endpoint security** > **Manage** in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

:::image type="content" source="./media/endpoint-security-policy/endpoint-security-policies.png" alt-text="Managing Endpoint security policies in the Microsoft Intune admin center":::

**[Account protection](../protect/endpoint-security-account-protection-policy.md)**  

- **Purpose**: Protect user identities and accounts through modern authentication methods
- **Platform support**: Windows
- **Available profiles**: Account protection, Local admin password solution (Windows LAPS), Local user group membership
- **Use case**: Implement passwordless authentication and credential protection

**[Antivirus](../protect/endpoint-security-antivirus-policy.md)**  

- **Purpose**: Configure and manage antivirus protection settings
- **Platform support**: Windows, macOS, Linux
- **Available profiles**: Defender Update controls, Microsoft Defender Antivirus, Microsoft Defender Antivirus exclusions, Windows Security experience, macOS Endpoint security antivirus
- **Use case**: Centrally manage Microsoft Defender Antivirus policies on Windows devices

**[App Control for Business](../protect/endpoint-security-app-control-policy.md)**  

- **Purpose**: Control which applications can run on Windows devices using [Windows Defender Application Control (WDAC)](/windows/security/application-security/application-control/windows-defender-application-control/wdac)
- **Platform support**: Windows
- **Available profiles**: Windows Defender Application Control (WDAC)
- **Use case**: Implement application allowlisting and control software execution

**[Attack surface reduction](../protect/endpoint-security-asr-policy.md)**  

- **Purpose**: Reduce potential attack vectors and system vulnerabilities
- **Platform support**: Windows
- **Available profiles**: App and browser isolation, Attack surface reduction rules, Device control,  Exploit protection, Application control
- **Use case**: Harden devices against common attack methods and techniques
- **Requirements**: Microsoft Defender Antivirus must be the primary antivirus solution

**[Disk encryption](../protect/endpoint-security-disk-encryption-policy.md)**  

- **Purpose**: Manage built-in encryption methods for data protection
- **Platform support**: Windows, macOS
- **Available profiles**: BitLocker, Personal Data Encryption (PDE), macOS FileVault
- **Use case**: Ensure data-at-rest protection with native encryption technologies

**[Endpoint detection and response](../protect/endpoint-security-edr-policy.md)**  

- **Purpose**: Configure Microsoft Defender for Endpoint integration and onboarding
- **Platform support**: Windows, macOS, Linux
- **Available profiles**: Endpoint detection and response *(For onboarding and configuration)*
- **Use case**: Enable advanced threat detection and response capabilities
- **Requirements**: Microsoft Defender for Endpoint licensing and tenant connection

**[Firewall](../protect/endpoint-security-firewall-policy.md)**  

- **Purpose**: Configure built-in firewall protection
- **Platform support**: Windows, macOS
- **Available profiles**: Windows Firewall, Windows Firewall rules, macOS Firewall
- **Use case**: Control network access and implement network segmentation

## Enhanced management features

Endpoint security policies include the following management capabilities beyond basic policy deployment:

**[Reusable settings groups](../protect/reusable-settings-groups.md)**: Create standardized configurations that can be shared across multiple policies, reducing administrative overhead and ensuring consistency. Supported by:

- **Firewall** > *Windows Firewall rules* profile (Windows platform)
- **Attack surface reduction** > *Device control* profile (Windows platform)

**[Security settings management through Microsoft Defender portal](../protect/mde-security-integration.md)**: When devices have Microsoft Defender for Endpoint but aren't enrolled with Intune, you can use select endpoint security policies (Antivirus, Attack Surface Reduction, EDR) directly from the Defender portal. This provides:

- Extended security management to devices that aren't enrolled with Intune in your environment.
- Unified policy management experience through the Defender portal.
- Consistent security controls across enrolled and non-enrolled devices.

## Role-based access control for endpoint security

Managing endpoint security policies requires appropriate Intune Role-based access control (RBAC) permissions. Understanding the current RBAC permission model is essential for proper role assignment and policy management access.

> [!NOTE]
> Intune is transitioning from using the unified *Security baselines* permission for all endpoint security workloads to granular permissions for individual policy types. This transition provides more precise access control but results in different permission requirements across policy types.

### Required RBAC permissions

Endpoint security policies use either granular permissions for specific workloads or the *Security baselines* permission. The required permission varies by policy type:

**Granular permissions** (policy-specific access):
- **Application control for Business** - Application control policies and reports
- **Attack surface reduction** - Most Attack surface reduction policies. *(See the following important note)*
- **Endpoint detection and response** - EDR policies and reports

**Security baselines permission** (unified access):
- **Antivirus** policies (all profiles)
- **Account protection** policies
- **Disk encryption** policies
- **Firewall** policies
- Some **Attack surface reduction** profiles: *App and browser isolation*, *Web protection*, *Exploit protection*, *Controlled folder access*

> [!IMPORTANT]
> For Attack surface reduction policies, check the specific profile requirements. Some profiles use the granular *Attack surface reduction* permission while others require *Security baselines* permission.

For detailed profile-specific requirements, see [Custom role considerations](#custom-role-considerations).

> [!IMPORTANT]
>
> The granular permission of *Antivirus* for endpoint security policies might be temporarily visible in some Tenants. This permission isn't released and isn't supported for use. Configurations of the Antivirus permission are ignored by Intune. When Antivirus becomes available to use as a granular permission, well announce its availability in the [What's new in Microsoft Intune](../fundamentals/whats-new.md) article.

### Built-in RBAC roles

The following Intune built-in roles provide access to endpoint security workloads:

- **Endpoint Security Manager** - Full management capabilities across all endpoint security policies.
- **Help Desk Operator** - Limited operational tasks and read access.
- **Read Only Operator** - View-only access to policies and reports.

### Custom role considerations

**Reporting access**: The *View Reports* right for Device configurations also provides access to endpoint security policy reports.

**Defender portal integration**: Security settings management through the Defender portal uses the same Intune RBAC permissions.

**[Multi Admin Approval](../fundamentals/multi-admin-approval.md)**: Role modifications might require dual administrator approval depending on your organization's governance settings.

## Create endpoint security policies

Follow this general workflow for creating endpoint security policies:

1. **Navigate to policy creation**:
   - Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
   - Go to **Endpoint security** > select the desired policy type > **Create Policy**.

2. **Configure policy basics**:
   - **Platform**: Choose the target device platform (options vary by policy type).
   - **Profile**: Select from available profiles for your chosen platform.
   - Select **Create** to continue.

3. **Complete policy configuration**:
   - **Basics**: Provide a descriptive name and optional description for the profile.
   - **Configuration settings**: Expand each group of settings and configure the settings you want to manage with this profile. When done configuring settings, select **Next**.
   - **Scope tags**: Choose **Select scope tags** to open the *Select tags* pane to assign scope tags to the profile (optional).
   - **Assignments**: Select the groups to receive this profile. See [Assign user and device profiles](../configuration/device-profile-assign.md).
   - **Review + create**: Review your configuration and select **Create** when ready. The new profile then appears in the policy list.

## Advanced policy management

### Duplicate policies

Policy duplication streamlines deployment by allowing you to copy existing configurations and modify them for different scenarios, rather than recreating complex policies from scratch.

**Common use cases for policy duplication**:

- **Environment deployment**: Copy production policies to staging or test environments.
- **Group variations**: Create similar policies for different user groups (for example, executives vs. general users with slightly different security requirements).
- **Regional customization**: Adapt policies for different geographical locations with varying compliance requirements.
- **Incremental rollouts**: Create multiple versions of the same policy for phased deployments.

**Duplication workflow**:

1. Locate the source policy in the policy list.
2. Select the ellipsis (**…**) > **Duplicate**.
3. Provide a new descriptive name and save.
4. Edit the duplicated policy to customize settings for your specific use case.
5. Configure new group assignments for the target scenario.

> [!NOTE]
> Duplicated policies retain all configuration settings and scope tags from the original policy but do not inherit assignments. You must configure new assignments and typically modify some settings to match your target scenario.

### Modify existing policies

Update policies through the Properties view:

1. Select the policy to modify.
2. Select **Edit** for each section requiring changes (*Basics*, *Assignments*, *Scope tags*, *Configuration settings*).
4. Save changes after editing a section before proceeding to the next.

## Manage policy conflicts

Prevent and resolve policy conflicts through strategic planning and monitoring:

**Prevention strategies**:
- Plan policy architecture before implementation and document which policy types manage specific settings.
- Use consistent configuration approaches across policy types.
- Apply security baselines as primary configuration sources where appropriate.

**Understanding policy boundaries**:
- **Setting overlap**: Many settings managed by endpoint security policies are also available in device configuration policies and security baselines.
- **Equal priority**: All policy types have equal precedence when Intune evaluates device configuration.
- **Conflict behavior**: When multiple policies configure the same setting with different values, the setting might fail to apply and be flagged as conflicted.

**Conflict troubleshooting workflow**:
1. **Identify conflicts**: Monitor policy deployment reports for error or conflict status flags.
2. **Verify settings**: Check which policy types target the same setting across multiple policies.
3. **Review per-setting status**: Use device-level reporting to identify which policies are applying.
4. **Check baselines**: Determine if security baselines are setting non-default values that conflict with other policies.
5. **Apply resolution**: Use policy-specific guidance to resolve conflicts systematically.

**Resolution resources**: [Troubleshoot policies and profiles in Intune](/troubleshoot/mem/intune/troubleshoot-policies-in-microsoft-intune) and [Monitor security baselines](../protect/security-baselines-monitor.md#troubleshoot-using-per-setting-status).

## Integration with Microsoft Defender for Endpoint

Many endpoint security policies have deep integration with Microsoft Defender for Endpoint, ranging from optional enhancement to essential integration. Understanding these relationships is essential for successful implementation.

### Policy-specific Defender dependencies

**Endpoint Detection and Response (EDR)**:
- **Requires integration**: Defender for Endpoint tenant connection with Intune.
- **Onboarding packages**: Uses Defender-specific onboarding configurations for each platform.
- **Core functionality**: Provides real-time attack detection and response capabilities.

**Antivirus**:
- **Cross-platform management**: Windows devices use the built-in Microsoft Defender Antivirus, while macOS devices use Microsoft Defender for Endpoint.
- **Tamper protection**: Available on Windows and macOS with Defender for Endpoint P1 or greater licenses.

**Attack Surface Reduction**:
- **Requirements**: Microsoft Defender Antivirus must be the primary antivirus solution.
- **ASR rules**: Attack surface reduction rules are native Microsoft Defender Antivirus features that integrate with Defender for Endpoint.
- **Device control**: Advanced device control policies use Defender's peripheral monitoring capabilities.

**Application Control**:
- **Managed installers**: Integration with Defender's application tagging and trust mechanisms.
- **Policy enforcement**: Uses Defender infrastructure for application control decisions.

### Defender integration benefits

- **Unified security posture**: Centralized visibility across endpoint security policies and threat detection.
- **Advanced reporting**: Combined device compliance and threat intelligence data.
- **Cross-platform management**: Consistent security policy deployment across Windows, macOS, and Linux through Defender agent.
- **Security settings management**: Manage select endpoint security policies (Antivirus, Attack Surface Reduction, EDR) on non-enrolled devices through the Defender portal. See [Microsoft Defender for Endpoint security settings management](../protect/mde-security-integration.md).

### Prerequisites for Defender integration

- **Licensing**: Microsoft Defender for Endpoint P1 or greater license.
- **Tenant connection**: Service-to-service connection between Intune and Defender for Endpoint tenants.
- **Agent deployment**: Defender for Endpoint agent installed on target devices (required for some policy types).
- **Network connectivity**: Device access to `*.dm.microsoft.com` endpoints for Defender security settings management and policy communication.

## Next steps

- [Explore the Endpoint security overview](../protect/endpoint-security.md)
- [Review security baselines for comprehensive security configurations](../protect/security-baselines.md)
- [Learn about reusable settings groups](../protect/reusable-settings-groups.md)
- [Configure Microsoft Defender for Endpoint integration](../protect/microsoft-defender-integrate.md)
- [Understand device protection strategies](../protect/device-protect.md)