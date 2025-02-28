---
title: What is Endpoint analytics?
titleSuffix: Microsoft Intune
description: Overview for Endpoint analytics.
ms.date: 02/28/2025
ms.service: microsoft-intune
ms.subservice: endpoint-analytics
ms.topic: overview
author: smritib17
ms.author: smbhardwaj
manager: dougeby
#Customer intent: As an Intune or Configuration Manager admin, I want to have visibility into the end-user experience so that I can improve it.
ms.localizationpriority: high
ms.collection: highpri
---

# <a name="bkmk_overview"></a> What is Endpoint analytics?

Endpoint analytics is part of the [Microsoft Adoption Score](/microsoft-365/admin/productivity/productivity-score). These analytics give you insights for measuring how your organization is working and the quality of the experience you're delivering to your users. Endpoint analytics can help identify policies or hardware issues that might be slowing down devices and help you proactively make improvements before end-users generate a help desk ticket. For more information on the Microsoft Adoption Score and other new tools, see [New tools to help IT empower employees securely in a remote work world​](https://www.microsoft.com/en-us/microsoft-365/blog/2020/04/30/new-tools-help-it-empower-employees-securely-remote-work-world/).<!-- see MEMDocs#955, this link requires "en-us" locale -->

## Endpoint analytics overview

It's not uncommon for end users to experience long boot times or other disruptions. These disruptions can be due to a combination of:

- Legacy hardware
- Software configurations that aren't optimized for the end-user experience
- Issues caused by configuration changes and updates

These issues and other end-user experience problems persist because IT doesn't have much visibility into the end-user experience. Generally, the only visibility into these issues comes from a slow costly support channel that doesn't usually provide clear information about what needs to be optimized. It's not only IT support bearing the cost of these problems. The time information workers spend dealing with issues is also costly. Performance, reliability, and support issues that reduce user productivity can affect an organization's bottom line as well.

**Endpoint analytics** aims to improve user productivity and reduce IT support costs by providing insights into the user experience. The insights enable IT to optimize the end-user experience with proactive support and to detect regressions to the user experience by assessing the effect of configuration changes on users.

> [!IMPORTANT]
> Endpoint analytics is now available to tenants in Government cloud.

## <a name="bkmk_prereq"></a> Prerequisites

You can enroll devices via Configuration Manager or Microsoft Intune.

### <a name="bkmk_intune_prereq"></a> How to enroll devices via Intune

- Intune enrolled or co-managed devices running the following:
  - Windows 10 version 1903 or later
  - July 2021 cumulative update or later
  - Pro, Pro Education, Enterprise, or Education. Home and long-term servicing channel (LTSC) aren't supported.
- Windows devices must be Microsoft Entra joined or Microsoft Entra hybrid joined. Workplace joined or Microsoft Entra registered devices aren't supported.
- Network connectivity from devices to the Microsoft public cloud. For more information, see [endpoints](troubleshoot.md#bkmk_endpoints).
- The [Intune Service Administrator role](/mem/intune/fundamentals/role-based-access-control) is required to [start gathering data](enroll-intune.md#bkmk_onboard).
  - After the administrator selects **Start** for gathering data, other read-only roles can view the data.

### <a name="bkmk_cm_prereq"></a> How to enroll devices via Configuration Manager

- A minimum of Configuration Manager version 2002 with [KB4560496 - Update rollup for Microsoft Configuration Manager version 2002](https://support.microsoft.com/help/4560496) or later
- The Configuration Manager clients upgraded to version 2002 (including [KB4560496](https://support.microsoft.com/help/4560496)) or later
- [Microsoft Intune tenant attach](../configmgr/tenant-attach/device-sync-actions.md) enabled.
- [Enable Endpoint analytics for devices uploaded to Microsoft Intune](enroll-configmgr.md#bkmk_cm_upload).

<!-- ### Remediation scripting requirements

Whether enrolling devices via Intune or Configuration Manager, [**Remediation scripting**](../intune/fundamentals/remediations.md) has the following requirements:

- Devices must be Azure AD joined or hybrid Azure AD joined and meet one of the following conditions:
  - Is managed by Intune and runs an Enterprise, Professional, or Education edition of Windows 10 or later.
  - A [co-managed](../configmgr/comanage/overview.md) device running Windows 10, version 1903 or later. Co-managed devices on preceding versions of Windows 10 will need the [Client apps workload](../configmgr/comanage/workloads.md#client-apps) pointed to Intune (only applicable up to version 1607). -->

## Licensing Prerequisites

Devices enrolled in Endpoint analytics need a valid license for the use of Microsoft Intune. For more information, see [Microsoft Intune licensing](../intune/fundamentals/licenses.md) or [Microsoft Configuration Manager licensing](../configmgr/core/understand/learn-more-editions.md).

<!-- Remediations also requires users of the devices to have one of the following licenses:

- Windows 10/11 Enterprise E3 or E5 (included in Microsoft 365 F3, E3, or E5)
- Windows 10/11 Education A3 or A5 (included in Microsoft 365 A3 or A5)
- Windows 10/11 Virtual Desktop Access (VDA) per user -->

## Permissions

### Endpoint analytics permissions

[!INCLUDE [Endpoint analytics permissions information](includes/endpoint-analytics-rbac.md)]

### Built-in role permissions

Use the following chart to see which built-in roles already have access to endpoint analytics. For more information about roles, see [Administrator role permissions in Microsoft Entra ID](/azure/active-directory/roles/permissions-reference) and [Role-based access control (RBAC) with Microsoft Intune](../intune/fundamentals/role-based-access-control.md). <!--7567981-->

|Role name|Microsoft Entra role|Intune role|Endpoint analytics permissions|
|---|---|---|---|
|Global Administrator|Yes||Read/write|
|Intune Service Administrator|Yes||Read/write|
|School Administrator||Yes|Read/write|
|Endpoint Security Manager||Yes|Read only|
|Help Desk Operator||Yes|Read only|
|Read Only Operator||Yes|Read only|
|Reports Reader|Yes||Read only|

<!-- ### Remediations permissions

For Remediations, the user needs permissions appropriate to their role under the **Device configurations** category.  Permissions in the **Endpoint Analytics** category aren't needed if the user only uses Remediations.

An [Intune Service Administrator](/azure/active-directory/users-groups-roles/directory-assign-admin-roles#intune-service-administrator-permissions) is required to confirm licensing requirements before using Remediations for the first time. (removing this as part of moving Remediations to Intune)-->

## <a name="bkmk_endpoints"></a> Endpoints

If your environment uses a proxy server, configure your proxy server to allow the following endpoints:

### Endpoints required for Configuration Manager-managed devices

Configuration Manager-managed devices send data to Intune via the connector on the Configuration Manager role and they don't need directly access to the Microsoft public cloud.

| Endpoint  | Function  |
|-----------|-----------|
| `https://graph.windows.net` | Used to automatically retrieve settings  when attaching your hierarchy to Endpoint analytics on Configuration Manager Server role. For more information, see [Configure the proxy for a site system server](../configmgr/core/plan-design/network/proxy-server-support.md#configure-the-proxy-for-a-site-system-server). |
| `https://*.manage.microsoft.com` | Used to synch device collection and devices with Endpoint analytics on Configuration Manager Server role only. For more information, see [Configure the proxy for a site system server](../configmgr/core/plan-design/network/proxy-server-support.md#configure-the-proxy-for-a-site-system-server). |

### Endpoints required for Intune-managed devices

To enroll devices to Endpoint analytics, they need to send required functional data to Microsoft public cloud. Endpoint Analytics uses the Windows Connected User Experiences and Telemetry component (DiagTrack) to collect the data from Intune-managed devices. Make sure that the **Connected User Experiences and Telemetry** service on the device is running.

| Endpoint  | Function  |
|-----------|-----------|
| `https://*.events.data.microsoft.com` | Used by Intune-managed devices to send [required functional data](data-collection.md#bkmk_datacollection) to the Intune data collection endpoint. |

>[!Important]  
> For privacy and data integrity, Windows checks for a Microsoft SSL certificate (certificate pinning) when communicating with the required functional data sharing endpoints. SSL interception and inspection aren't possible. To use Endpoint analytics, exclude these endpoints from SSL inspection.<!-- BUG 4647542 -->

## Next steps

- [Enroll Intune managed devices](enroll-intune.md)
- [Enroll Configuration Manager managed devices](enroll-configmgr.md)
