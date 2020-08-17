---
title: What is Endpoint analytics (preview)?
titleSuffix: Configuration Manager
description: Overview for Endpoint analytics preview.
ms.date: 08/12/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: overview
ms.assetid: b3273525-dc40-40d7-adf0-6ed8b054bd7e
author: mestew
ms.author: mstewart
manager: dougeby
#Customer intent: As an Intune or Configuration Manager admin, I want to have visibility into the end-user experience so that I can improve it.
---

# <a name="bkmk_overview"></a> What is Endpoint analytics (preview)?

Endpoint analytics is part of the [Microsoft Productivity Score](https://docs.microsoft.com/microsoft-365/admin/productivity/productivity-score). These analytics give you insights for measuring how your organization is working and the quality of the experience you're delivering to your users. Endpoint analytics can help identify policies or hardware issues that may be slowing down devices and proactively make changes without disrupting end users or generating a help desk ticket. For more information on the Microsoft Productivity Score and other new tools, see [New tools to help IT empower employees securely in a remote work world​](https://www.microsoft.com/microsoft-365/blog/2020/04/30/new-tools-help-it-empower-employees-securely-remote-work-world/).

> [!Note]  
> This information relates to a preview feature which may be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here.
>
> For more information about changes to Endpoint analytics, see [What's new in Endpoint analytics](whats-new.md).

## Endpoint analytics overview

It's not uncommon for end users to experience long boot times or other disruptions. These disruptions can be due to a combination of:

- Legacy hardware
- Software configurations that aren't optimized for the end-user experience
- Issues caused by configuration changes and updates

These issues and other end-user experience problems persist because IT doesn't have much visibility into the end-user experience. Generally, the only visibility into these issues comes from a slow costly support channel that doesn't usually provide clear information about what needs to be optimized. It's not only IT support bearing the cost of these problems. The time information workers spend dealing with issues is also costly. Performance, reliability, and support issues that reduce user productivity can have a large impact on an organization's bottom line as well.

**Endpoint analytics** aims to improve user productivity and reduce IT support costs by providing insights into the user experience. The insights enable IT to optimize the end-user experience with proactive support and to detect regressions to the user experience by assessing user impact of configuration changes.

This initial release, focuses on three things:

- [**Recommended software**](recommended-software.md): Recommendations for providing the best user experience
- [**Proactive remediation scripting**](proactive-remediations.md): Fix common support issues before end-users notice issues
- [**Start up performance**](startup-performance.md): Help IT get users from power-on to productivity quickly without lengthy boot and sign in delays

This release is just the beginning. We'll be rapidly rolling out new insights for other key user-experiences soon after initial release. For more information about changes to Endpoint analytics, see [What's new in Endpoint analytics](whats-new.md).

## <a name="bkmk_prereq"></a> Prerequisites

For this preview, you can enroll devices via Configuration Manager or Microsoft Intune.

### <a name="bkmk_intune_prereq"></a> To enroll devices via Intune, this preview requires:
- Intune enrolled or co-managed devices running Windows 10 Pro, Windows 10 Pro Education, Windows 10 Enterprise, or Windows 10 Education. Windows 10 Home isn't supported.
   - Startup performance insights are only available for devices running version 1903 or later of Windows 10 Enterprise or Windows 10 Education. Windows 10 Pro and Windows 10 long-term servicing channel (LTSC) aren't supported.
- Windows 10 devices must be Azure AD joined or hybrid Azure AD joined. Workplace joined or Azure AD registered devices aren't supported.
- Network connectivity from devices to the Microsoft public cloud. For more information, see [endpoints](troubleshoot.md#bkmk_endpoints).
- The [Intune Service Administrator role](https://docs.microsoft.com/intune/fundamentals/role-based-access-control) is required to [start gathering data](enroll-intune.md#bkmk_onboard).
   - By clicking **Start**, you agree to and acknowledge that your customer data may be stored outside the location you selected when you provisioned your Microsoft Intune tenant.
   - After clicking **Start** for gathering data, other read-only roles can view the data.

### <a name="bkmk_cm_prereq"></a> To enroll devices via Configuration Manager, this preview requires:
- Configuration Manager version 2002 or newer
- Clients upgraded to version 2002 or newer
- [Microsoft Endpoint Manager tenant attach](../configmgr/tenant-attach/device-sync-actions.md) enabled.
- [Enable Endpoint analytics for devices uploaded to Microsoft Endpoint Manager](enroll-configmgr.md#bkmk_cm_upload).

### <a name="bkmk_prs_prereq"></a> Proactive remediation scripting requires:
Whether enrolling devices via Intune or Configuration Manager, [**Proactive remediation scripting**](proactive-remediations.md#bkmk_prs) has the following requirements:
- Devices must be Azure AD joined or hybrid Azure AD joined and meet one of the following conditions:
  - A Windows 10 Enterprise, Professional, or Education device that is managed by Intune.
  - A [co-managed](../configmgr/comanage/overview.md) device running Windows 10, version 1903 or later. Co-managed devices on preceding versions of Windows 10 will need the [Client apps workload](../configmgr/comanage/workloads.md#client-apps) pointed to Intune (only applicable up to version 1607).

## Licensing Prerequisites

Endpoint analytics is included in the following plans:

- [Enterprise Mobility + Security E3](https://www.microsoftvolumelicensing.com/ProductResults.aspx?doc=Product%20Terms,OST&fid=51) or higher
- [Microsoft 365 Enterprise E3](https://www.microsoft.com/en-us/microsoft-365/enterprise?rtc=1) or higher.

Proactive remediations also require one of the following licenses for the managed devices:
- Windows 10 Enterprise E3 or E5 (included in Microsoft 365 F3, E3, or E5)
- Windows 10 Education A3 or A5 (included in Microsoft 365 A3 or A5)
- Windows Virtual Desktop Access E3 or E5

## Permissions

### Endpoint analytics permissions

The following permissions are used for Endpoint analytics:
- **Read** under the **Device configurations** category.
- **Read** under the **Organization** category. <!--temporary for pp-->
- Permissions appropriate to the user's role under the **Endpoint Analytics** category.

A read-only user would only need the **Read** permission under both the **Device configurations** and **Endpoint Analytics** categories. An Intune administrator would typically need all permissions.

### Proactive remediations permissions

For Proactive remediations, the user needs permissions appropriate to their role under the **Device configurations** category.  Permissions in the **Endpoint Analytics** category aren't needed if the user only uses Proactive remediations.

An [Intune Service Administrator](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles#intune-service-administrator-permissions) is required to confirm licensing requirements before using proactive remediations for the first time.

## <a name="bkmk_endpoints"></a> Endpoints

If your environment uses a proxy server, configure your proxy server to allow the following endpoints:

### Endpoints required for Configuration Manager-managed devices

Configuration Manager-managed devices send data to Intune via the connector on the Configuration Manager role and they don't need directly access to the Microsoft public cloud.

| Endpoint  | Function  |
|-----------|-----------|
| `https://graph.windows.net` | Used to automatically retrieve settings  when attaching your hierarchy to Endpoint analytics on Configuration Manager Server role. For more information, see [Configure the proxy for a site system server](../configmgr/core/plan-design/network/proxy-server-support.md#configure-the-proxy-for-a-site-system-server). |
| `https://*.manage.microsoft.com` | Used to synch device collection and devices with Endpoint analytics on Configuration Manager Server role only. For more information, see [Configure the proxy for a site system server](../configmgr/core/plan-design/network/proxy-server-support.md#configure-the-proxy-for-a-site-system-server). |

### Endpoints required for Intune-managed devices

To enroll devices to Endpoint analytics, they need to send required functional data to Microsoft public cloud. Endpoint Analytics uses the Windows 10 and Windows Server Connected User Experiences and Telemetry component (DiagTrack) to collect the data from Intune-managed devices. Make sure that the **Connected User Experiences and Telemetry** service on the device is running.

| Endpoint  | Function  |
|-----------|-----------|
| `https://*.events.data.microsoft.com` | Used by Intune-managed devices to send [required functional data](data-collection.md#bkmk_datacollection) to the Intune data collection endpoint. |

> [!Important]  
> For privacy and data integrity, Windows checks for a Microsoft SSL certificate (certificate pinning) when communicating with the required functional data sharing endpoints. SSL interception and inspection aren't possible. To use Endpoint analytics, exclude these endpoints from SSL inspection.<!-- BUG 4647542 -->

## Next steps

- [Enroll Intune managed devices](enroll-intune.md)
- [Enroll Configuration Manager managed devices](enroll-configmgr.md)
