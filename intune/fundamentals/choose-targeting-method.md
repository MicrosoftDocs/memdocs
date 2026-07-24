---
title: Choose the right targeting method in Microsoft Intune
description: Learn when to use assignment filters, dynamic groups, static groups, virtual groups, and enrollment time grouping for device and user targeting in Microsoft Intune.
author: matt-call
ms.author: mattcall
ms.date: 06/30/2026
ms.topic: concept-article
ms.reviewer: mattcall
ms.collection:
- M365-identity-device-management
---

# Choose the right targeting method in Microsoft Intune

Microsoft Intune supports several methods for targeting devices and users with policies and apps. Each method has different strengths, evaluation characteristics, and use cases. Choosing the right method — or combination of methods — helps ensure policies and apps reach the right devices at the right time.

This article describes the available targeting constructs and helps you choose the right approach for your environment.

## Key concepts

Before choosing a targeting method, understand the principles that guide effective targeting in Intune:

| Principle | Description |
|---|---|
| **Start broad, refine narrow** | Instead of building many narrow groups to match each policy, start with the broadest applicable audience and use assignment filters to refine which devices receive the policy. This strategy reduces group sprawl and simplifies management. |
| **Groups define scope, filters define targeting** | Groups answer *"who is the audience?"*. Assignment filters answer *"which devices in that audience actually receive this policy?"* Combining both concerns into groups alone leads to many nearly-identical groups that are difficult to manage. |
| **One group, many policies** | You don't need a 1:1 relationship between groups and policies. A single broad group can serve multiple policy assignments. Applicability of the workload or assignment filters can ensure the policies only go to applicable users and devices. |
| **Group membership is identity, not policy intent** | Groups should describe *what a device is* or *what a user is* in a way that's meaningful across your organization — not *what policy it should get*. If only Intune reads a group, evaluate whether an assignment filter can replace the group. |
| **Evaluate at check-in vs. evaluate on change** | Groups and filters use different evaluation models. Group membership is processed when device or user attributes change reflecting the current state of the directory. Filters evaluate at every device check-in against the device's properties at that moment. Choose based on whether you need membership that other services can read (groups) or precise, check-in-time targeting for Intune (filters). |

## Targeting methods overview

Intune targeting is built on two layers: **group types** that define *who* or *what* is in scope, and **Intune targeting features** that refine *how* and *when* policies reach those devices.

### Group types

| Group type | What it does | Best for |
|---|---|---|
| **Virtual groups** | Built-in *All users* and *All devices* groups maintained by Intune | Broad policies that apply to everyone or every device |
| **Static groups** | Manually managed security groups with fixed membership | Fixed, known sets of users or devices that don't change frequently |
| **Dynamic groups** | Groups with rule-based membership evaluated by Microsoft Entra ID | Cross-workload targeting (Conditional Access, licensing), Autopilot, user-based grouping |

Static and dynamic groups are Microsoft Entra security groups — any service that consumes group membership (Conditional Access, licensing, SharePoint, Exchange) can use them. Virtual groups are Intune-managed and always current without requiring additional processing.

### Intune targeting features

| Construct | What it does | Best for |
|---|---|---|
| **Assignment filters** | Intune-evaluated rules applied on top of group assignments | Device property targeting for Intune policies — evaluated at check-in without depending on group membership processing |
| **Enrollment time grouping** | Adds devices to a security group during enrollment | Fast group-based policy delivery during enrollment without waiting for dynamic group membership processing |

These are unique to Intune. Assignment filters and enrollment time grouping extend what you can do with groups — they don't replace groups, but they solve specific gaps in speed and precision that groups alone can't address.

## Group types

### Virtual groups

Intune provides built-in virtual groups for *All users* and *All devices*. These groups are always current — they don't require processing to update membership.

Virtual groups are most effective when combined with Intune targeting features:

- **Virtual group + assignment filter** — Assign a policy to *All devices*, then apply a filter to narrow scope to specific device properties (like OS type, manufacturer, or ownership). The filter evaluates at check-in without depending on group membership processing.

**Use when:**

- A policy or app should reach all users or all devices
- You want a broad target that you refine with assignment filters to achieve precise device-level targeting

### Static groups

Static security groups have manually managed membership. An administrator adds or removes members directly.

Static groups can also be combined with Intune targeting features:

- **Static group + assignment filter** — Assign a policy to a static group (like a department or pilot ring), then apply a filter to further narrow which devices in that group receive the policy.
- **Static group + enrollment time grouping** — Use a static group as the target for enrollment time grouping. Devices are added to the group during enrollment, enabling fast policy delivery on first check-in.

**Use when:**

- You have a fixed set of users or devices (like a pilot group or executive team)
- You need group membership for cross-workload scenarios but the population is small and stable

### Dynamic groups

Dynamic groups use rule-based membership that's evaluated and updated by Microsoft Entra ID. They're the standard mechanism for organizing users and devices across the Microsoft 365 ecosystem — any service that reads group membership (Conditional Access, licensing, SharePoint, Exchange) consumes dynamic groups.

After a device enrolls or a user attribute changes, the group membership requires additional processing before the change is reflected.

**Use when:**

- **Cross-workload scenarios** — Conditional Access policies, group-based licensing, SharePoint access, Exchange Online policies, or any Microsoft 365 service that requires group membership
- **Autopilot targeting** — Autopilot deployment profiles must be assigned to groups. Devices must be group members before enrollment begins
- **User-based grouping** — Grouping users by department, location, job title, or other user attributes

> [!NOTE]
> If your dynamic device group is only consumed by Intune (not Conditional Access, licensing, or other services), evaluate whether an assignment filter can achieve the same targeting. Filters support many of the same device properties — including `enrollmentProfileName` — and evaluate at check-in without depending on group membership processing.

Dynamic groups can also be combined with assignment filters:

- **Dynamic group + assignment filter** — Assign a policy to a dynamic group, then apply a filter to further refine which devices in that group receive the policy. approach is useful when the group serves cross-workload purposes but you need more precise Intune targeting within the group.

  **Example:** Your organization uses a dynamic group for all corporate-owned Windows devices because Conditional Access policies require that group membership. Within Intune, you assign a configuration profile to that group and apply an assignment filter to target only devices running Windows 11 24H2 or later. The group handles Conditional Access scope, while the filter handles Intune-specific version targeting — without creating a second group.

**Best practices for dynamic groups:**

- **Keep rules simple** — Use direct property comparisons with `-eq` or `-startsWith` and a small number of conditions. Simpler rules evaluate faster and are easier to troubleshoot.
- **Avoid `memberOf`** — Transitive group lookups add significant processing complexity and are a common source of unexpected membership results.
- **Audit attribute write permissions** — If a dynamic group controls access to sensitive resources (Conditional Access, licensing), the security of that access depends on who can modify the attributes referenced in the rule.
- **Ensure devices have clean, accurate attributes** — Dynamic group membership depends on the properties written to the device object. Stale or missing values lead to unexpected membership.

For detailed guidance on rule syntax and writing efficient rules, go to:

- [Manage rules for dynamic membership groups in Microsoft Entra ID](/entra/identity/users/groups-dynamic-membership)
- [Create simpler and faster rules for dynamic membership groups](/entra/identity/users/groups-dynamic-rule-more-efficient)
- [Understand and manage dynamic group processing](/entra/identity/users/manage-dynamic-group#optimize-rule-efficiency)

## Intune targeting features

### Assignment filters

Assignment filters are Intune-evaluated rules that refine which devices receive a policy or app. Filters are applied on top of a group assignment and evaluate device properties directly at check-in without depending on group membership processing.

**Use when:**

- You're targeting **Intune policies or apps** based on device properties (OS version, manufacturer, model, ownership, device category)
- You want evaluation **directly at device check-in** without requiring group membership processing
- You want to combine broad group assignments (like *All devices*) with precise device-level targeting
- You want to **include or exclude** specific devices from a policy assigned to a broad group

**Common scenarios:**

- Deploy a compliance policy to all corporate-owned Windows devices
- Exclude a specific device manufacturer from a configuration profile
- Target devices running a specific OS version for an app deployment
- Narrow a policy assigned to *All devices* to only iOS devices owned by the organization

> [!NOTE]
> Assignment filters are not a replacement for groups in every scenario. Filters can't be used for:
> - **Autopilot profile assignment** — devices must be group members before enrollment begins
> - **Conditional Access, licensing, or SharePoint** — these services require Entra group membership
> - **Workloads that don't support filters** — verify filter support for your specific policy or app type before designing around it

### Enrollment time grouping

Enrollment time grouping adds devices to a specified security group during enrollment rather than after. This feature allows apps and policies assigned to that group to be delivered earlier in the enrollment flow — in many cases on the first check-in — without waiting for group membership to process. Actual delivery timing depends on the workload, platform, assignment type, and enrollment method.

**Use when:**

- You need group membership to be available during enrollment for fast policy delivery
- You're using [enrollment methods that support enrollment time grouping](../device-enrollment/setup-time-grouping.md#requirements)
- You need the group for cross-workload scenarios (like Conditional Access) and also need fast enrollment-time delivery

**Don't use when:**

- An assignment filter can achieve the same targeting — if the policy is Intune-only and you're targeting based on device properties available at check-in (OS, manufacturer, ownership), a filter is simpler and doesn't require group management
- You don't need the group for any other purpose — enrollment time grouping creates real Entra security group memberships that persist after enrollment. If no other service reads that group, you're adding management overhead without benefit
- The enrollment method doesn't support it — only specific enrollment flows support enrollment time grouping. Verify your enrollment method is in the [supported list](../device-enrollment/setup-time-grouping.md#requirements) before designing around it

For more information, go to [Enrollment time grouping in Microsoft Intune](../device-enrollment/setup-time-grouping.md).

## Choosing the right approach

For most Intune environments, the best approach combines multiple methods:

1. **Start with broad groups** — Use virtual groups, static groups, or dynamic groups as your base assignment targets. Choose the broadest appropriate base group for your organization — but account for each group type's evaluation timing and cross-workload requirements.
2. **Refine targeting based on device attributes** — Use assignment filters when the policy is Intune-only. Use dynamic groups when the attribute-based membership is needed across workloads (Conditional Access, licensing, Autopilot).
3. **Use enrollment time grouping** to remove the wait for group membership processing during enrollment, so policies are delivered on the first check-in.

> [!CAUTION]
> Broad assignments are powerful but carry risk. Before assigning high-impact policies to *All devices* with a filter, validate the filter against a pilot group first. A misconfigured or deleted filter on a broad assignment can affect every device in scope. Use staged rollout rings and monitor assignment reporting before expanding to production.

### When a dynamic group can become a filter

If you have dynamic device groups that use simple property rules and are only consumed by Intune — not Conditional Access, licensing, or other services — you can simplify your targeting by replacing those groups with assignment filters. The intent isn't about removing all dynamic groups. It's about removing unnecessary group processing overhead for groups that don't serve cross-workload purposes.

The following table shows common dynamic group rules and their equivalent assignment filter syntax:

| Dynamic group rule | Equivalent assignment filter | Notes |
|---|---|---|
| `device.deviceOSType -eq "Windows"` | `operatingSystemSKU -eq "Windows"` | OS type targeting |
| `device.deviceManufacturer -eq "Microsoft"` | `manufacturer -eq "Microsoft Corporation"` | Manufacturer targeting |
| `device.deviceModel -startsWith "Surface"` | `model -startsWith "Surface"` | Model targeting |
| `device.deviceOwnership -eq "Company"` | `deviceOwnership -eq "Corporate"` | Ownership targeting |
| `device.deviceCategory -eq "Engineering"` | `deviceCategory -eq "Engineering"` | Device category targeting |

> [!NOTE]
> Property names and values may differ slightly between dynamic group rules and assignment filter syntax. Verify the exact property names and supported values in [Supported device properties when creating filters](./filters/ref-device-properties.md).

> [!IMPORTANT]
> Don't remove dynamic groups that are used by services outside of Intune (Conditional Access, licensing, SharePoint). Those services can't consume assignment filters — they require group membership. Only simplify groups that exist solely for Intune policy targeting.

> [!TIP]
> Targeting decisions also impact performance — especially in large environments. For guidance on group reuse, avoiding common anti-patterns, and understanding sync behavior, go to [Performance recommendations for grouping, targeting, and filtering](./filters/performance-recommendations.md).

## Related articles

- [Use assignment filters to assign your apps, policies, and profiles in Microsoft Intune](./filters/overview.md)
- [Supported device properties when creating filters](./filters/ref-device-properties.md)
- [Performance recommendations for grouping, targeting, and filtering](./filters/performance-recommendations.md)
- [Use groups to organize users and devices for Microsoft Intune](./tenant-administration/add-groups.md)
- [Enrollment time grouping in Microsoft Intune](../device-enrollment/setup-time-grouping.md)
