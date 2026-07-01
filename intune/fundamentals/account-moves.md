---
title: Microsoft Intune Account Moves Overview
description: Learn what an Intune account move is, why moves happen, and how the process affects your tenant before, during, and after the maintenance window.
ms.topic: concept-article
ms.custom: msecd-doc-authoring-1012
ms.date: 05/21/2026
robots: NOINDEX, NOFOLLOW
---

# Microsoft Intune account moves overview

An Intune account move is a managed migration that relocates your tenant's Intune customer data at rest from one geographic datacenter region to another. The move preserves your Intune policies, profiles, device enrollments, app management state, and service configuration.

When your organization first provisions Microsoft Intune, Intune hosts customer data in the geography that best aligns with the country or region value in your Microsoft Entra directory. As Intune grows, Microsoft might add new geographies or datacenters. Existing tenants don't automatically move when new capacity becomes available. An account move is how the tenant's Intune customer data transfers to a different geographic datacenter region.

An account move isn't a tenant-to-tenant migration. Your tenant, users, groups, device records, policies, and management relationships stay in place. The move changes where Intune customer data is stored at rest.

## Why account moves happen

Account moves can be initiated by a customer or by Microsoft.

| Move type | Why it happens | How it's coordinated |
|---|---|---|
| Customer-requested move | Your organization needs Intune customer data to reside in a different geography, such as for data residency, regulatory, or business alignment requirements. | Contact Microsoft support. Support helps determine eligibility, explain limitations, and coordinate the move date. |
| Microsoft-initiated move | Microsoft moves tenants to optimize service performance, balance scale units, or improve regional service operations. | Microsoft provides advance notice before the scheduled move. Downtime for Microsoft-initiated moves is governed by Intune service commitments. |

## How the account move process works

The account move process uses four stages. Most data is copied before the maintenance window, which reduces the amount of data that must move while the service is in read-only mode.

### :::image type="icon" source="media/account-moves/practice-move.svg" border="false":::&nbsp;Stage 0: Practice move

> Microsoft performs a dry-run migration to the destination region weeks before the scheduled move. This isolated practice move validates the process and helps estimate downtime. It doesn't affect your production tenant.

### :::image type="icon" source="media/account-moves/pre-move.svg" border="false":::&nbsp;Stage 1: Pre-move

> About 24 hours before the maintenance window, most tenant data is copied to the destination region in the background. Intune stays operational during this stage.

### :::image type="icon" source="media/account-moves/downtime-move.svg" border="false":::&nbsp;Stage 2: Downtime move

> During the maintenance window, Intune enters a temporary read-only state. Recently changed data from the previous period transfers to the destination region.

### :::image type="icon" source="media/account-moves/validation.svg" border="false":::&nbsp;Stage 3: Validation

> Microsoft validates data integrity and service readiness, then restores normal Intune service operations.
## Before the move

Before the account move, Microsoft or Microsoft support coordinates timing with your organization. For Microsoft-initiated moves, you will receive at least 5 business days' notice ahead of the scheduled move date, however we typically try to provide at least a month's notice to help you plan.

Use the preparation period to review expected limitations, communicate the maintenance window, and avoid changes that could overlap with the move.

### How the move affects your organization

The maintenance window affects the Microsoft Intune admin center and Intune for Education. During downtime, these portals are read-only and administrators can't make changes. Your Intune account moves to a new tenant data location, and some features need preparation or follow-up after the move.

Review the following areas before the move if your organization uses them:

- Windows Autopilot
- Policy reporting data
- All devices list
- Intune Data Warehouse API

### Preparation checklist

> [!div class="checklist"]
>
> - Review the scheduled move window and communicate the expected impact to IT administrators, help desk teams, and affected stakeholders.
> - Review service-specific limitations that apply to your environment.
> - Update network and firewall rules if needed. For Intune endpoints, see [Network endpoints for Microsoft Intune](endpoints.md).
> - If you use Windows Autopilot enrollment for hybrid Microsoft Entra joined devices, plan to [reinstall the Intune Connector for Active Directory](/autopilot/windows-autopilot-hybrid#install-the-intune-connector-for-active-directory) after the maintenance window is complete.
> - Avoid deploying new policies, profiles, app assignments, enrollments, or configuration changes during the move window.
> - Avoid scheduling Windows feature update deployments during the move window because reporting and monitoring data might be affected.

> [!NOTE]
> Move timing can vary by tenant size and complexity. The expected downtime for many organizations is about two to four hours, but larger environments can take longer.

## During the move

During the maintenance window, Intune is temporarily in a read-only state. Administrators can view existing configuration in the Intune admin center, but write operations and new management actions are paused. Existing devices continue to operate with their last received policies.

| Scenario | Experience during the move |
|---|---|
| Microsoft Intune admin center | The admin center is in read-only mode. Sign-in succeeds, and you can view and navigate blades. Actions that create, update, or delete Intune data aren't available. |
| Intune for Education portal | Users see an account maintenance message. No further actions are allowed until the move is complete. |
| Company Portal sign-in and usage | Sign-in succeeds, and users can open the app. Some features fail, including device sync and actions that modify a device, such as rename, retire, or wipe. |
| Device check-in | MDM device check-ins are blocked. Features that depend on check-in can be affected, including app installation; VPN, Wi-Fi, and certificate provisioning; policy delivery; and device compliance state updates. |
| Mobile application management (MAM) | New app enrollments, MAM policy updates, and MAM check-ins fail. Data sharing across managed apps might fail. Users can continue to launch and use apps. |
| New enrollments (MDM and MAM) | New MDM and MAM enrollment attempts fail during the maintenance window. |
| Microsoft Entra ID updates | Changes such as account updates, new users, licensing updates, and group membership changes don't immediately reflect in Intune workloads. This delay can affect group-assigned policy delivery, license-based enrollment, and Device Enrollment Manager user management. |

## After the move

After validation completes, normal Intune service operations resume. Device management, enrollment, policy deployment, app management, and admin center write access are restored. Your configurations, policies, enrollments, and management relationships are preserved.

Some reporting data can take more time to repopulate in the destination region. The duration depends on the report type and tenant size.

| Scenario | Experience after the move |
|---|---|
| Microsoft Entra ID changes | Recent Microsoft Entra changes might take more time to reflect in Intune. The duration depends on the number of users and groups in the directory. |
| MAM for iOS and Android | For devices that already have MAM apps or policies, delivery of new policies or changes to existing policies can be delayed for up to 30 minutes. Enrollment of new MAM apps on these devices can be delayed for up to 12 hours. Apps protected by Mobile Threat Defense app protection policy can be prevented from launching for up to 30 minutes. Apps protected by Conditional Access might not be able to sign in or access resources for up to 30 minutes, depending on configuration. MAM check-in and enrollment on devices with no existing MAM apps should work as expected. |
| Data warehouse reports and trend charts | Some reports that access the data warehouse can appear empty after migration. These reports are restored within 48 hours. |
| Intune Data Warehouse API | Update the Data Warehouse API URL to use the new tenant location. For more information, see [Move your Intune Data Warehouse account data](../developer/data-warehouse/move-account-data.md). |
| Operational and aggregate reporting data | Some device and user operational reports and aggregate charts are reset and regenerate as devices check in after the move. These reports include status data for mobile app configuration profiles, device configuration profiles, device compliance policies, software updates, advanced threat protection, resource access profiles such as Wi-Fi, certificates, and VPN, and terms and conditions acceptance. |
| Organizational reports | Organizational reports, including device compliance reports in the Intune admin center and setting error reports in Intune for Education, regenerate after the move. |
| All devices list and troubleshooting data | It can take up to 72 hours after downtime ends for enrolled devices to appear in the All devices list. Troubleshooting data can also take up to 72 hours to fully repopulate. |
| Windows Autopilot for hybrid Microsoft Entra joined devices | After the maintenance window is complete, reinstall the Intune Connector for Active Directory if you use Windows Autopilot enrollment for hybrid Microsoft Entra joined devices. |
| Windows feature updates | If a Windows feature update deployment runs during the migration window, incoming reporting and monitoring data can be lost during that time. Avoid active Windows feature update deployments during an account move. |

## Impact summary

| Phase | Typical duration | Customer impact |
|---|---|---|
| Advance notice | For Microsoft initiated moves, at minimum a 5-business day notice with exact downtime details. | Time to prepare, communicate internally, and avoid conflicting changes. |
| Pre-move | About 24 hours before the move. | No customer impact. Intune stays operational while data is copied in the background. |
| Maintenance window | About two to four hours for many tenants; varies by tenant size. | Read-only mode. New enrollments, device check-ins, policy writes, app assignment changes, and configuration changes are paused. |
| Post-move | Immediate service restoration; some reporting can take 24 to 72 hours. | Normal service operations resume. Some reports repopulate gradually. |

## Verify your data location

After the move completes, verify your tenant's data location in the Microsoft Intune admin center. Go to **Tenant administration** > **Tenant status**, and review the tenant data location.

## Frequently asked questions

### Will I lose any data?

No. Intune customer data, policies, configurations, and device management relationships are migrated. Some non-critical reporting data can repopulate after the move.

### Do I need to re-enroll devices?

No. Device enrollments and management relationships are preserved through the move.

### How do I request an account move?

Contact Microsoft support. Support can help determine eligibility, coordinate timing, and explain environment-specific limitations.

### Can a move be rolled back?

If an issue occurs during the move, Microsoft can roll back to the original state and reschedule the move. Microsoft coordinates next steps and any required customer communication.

## Related content

- [Data storage and processing in Intune](../privacy/data-handling/data-storage-processing.md)
- [Migration guide: Set up or move to Microsoft Intune](setup-migration.md)
- [Microsoft Intune planning guide](planning-guide.md)
