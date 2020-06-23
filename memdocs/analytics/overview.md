---
title: What is Endpoint analytics (preview)?
titleSuffix: Configuration Manager
description: Overview for Endpoint analytics preview.
ms.date: 06/25/2020
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

> [!Note]  
> This information relates to a preview feature which may be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here. 
>
> For more information about changes to Endpoint analytics, see [What's new in Endpoint analytics](whats-new.md).

## Endpoint analytics overview

It's not uncommon for end users to experience long boot times or other disruptions. These disruptions can be due to a combination of:

- Legacy hardware
- Software configurations that aren't optimized for the end-user experience
- Issues caused by configuration changes and updates

These issues and other end-user experience problems persist because IT doesn't have much visibility into the end-user experience. Generally, the only visibility into these issues come from a slow costly support channel that doesn't usually provide clear information about what needs to be optimized. It's not only IT support bearing the cost of these problems. The time information workers spend dealing with issues is also costly. Performance, reliability, and support issues that reduce user productivity can have a large impact on an organization's bottom line as well.

**Endpoint analytics** aims to improve user productivity and reduce IT support costs by providing insights into the user experience. The insights enable IT to optimize the end-user experience with proactive support and to detect regressions to the user experience by assessing user impact of configuration changes.

This initial release, focuses on three things:

- [**Recommended software**](recommended-software.md): Recommendations for providing the best user experience
- [**Proactive remediation scripting**](proactive-remediations.md): Fix common support issues before end-users notice issues
- [**Start up performance**](startup-performance.md): Help IT get users from power-on to productivity quickly without lengthy boot and sign in delays

This release is just the beginning. We'll be rapidly rolling out new insights for other key user-experiences soon after initial release. For more information about changes to Endpoint analytics, see [What's new in Endpoint analytics](whats-new.md).

## <a name="bkmk_prereq"></a> Prerequisties

For this preview, you can enroll devices via Configuration Manager or Microsoft Intune.

### <a name="bkmk_uea__intune_prereq"></a> To enroll devices via Intune, this preview requires:
- Intune enrolled devices running Windows 10
- Startup performance insights are only available for devices running version 1903 or later of Windows 10 Enterprise (Home and Pro editions aren't currently supported), and the devices must be Azure AD joined or hybrid Azure AD joined. Workplace joined machines aren't currently supported.
- Network connectivity from devices to the Microsoft public cloud. For more information, see [endpoints](trobleshoot.md#bkmk_uea_endpoints).
- The [Intune Service Administrator role](https://docs.microsoft.com/intune/fundamentals/role-based-access-control) is required to [start gathering data](enroll-intune.md#bkmk_uea_start).
   - By clicking **Start**, you agree to and acknowledge that your customer data may be stored outside the location you selected when you provisioned your Microsoft Intune tenant.
   - After clicking **Start** for gathering data, other read-only roles can view the data.

### <a name="bkmk_uea__cm_prereq"></a> To enroll devices via Configuration Manager, this preview requires:
- Configuration Manager version 2002 or newer
- Clients upgraded to version 2002 or newer
- [Microsoft Endpoint Manager tenant attach](../configmgr/tenant-attach/device-sync-actions.md) enabled.

### <a name="bkmk_uea__prs_prereq"></a> Proactive remediation scripting requires:
Whether enrolling devices via Intune or Configuration Manager, [**Proactive remediation scripting**](proactive-remediations.md#bkmk_uea_prs) has the following requirements:
- Devices must be must be Azure AD joined or hybrid Azure AD joined and meet one of the following conditions:
- A Windows 10 Enterprise, Professional, or Education device that is managed by Intune
- A [co-managed](../configmgr/comanage/overview.md) device running Windows 10 Enterprise, version 1607 or later with the [Client apps workload](../configmgr/comanage/workloads.md#client-apps) pointed to Intune.
- A [co-managed](../configmgr/comanage/overview.md) device running Windows 10 Enterprise, version 1903 or later with the [Client apps workload](../configmgr/comanage/workloads.md#client-apps) pointed to Configuration Manager.

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


## Next steps

- [Enroll Intune managed devices](enroll-intune.md)
- [Enroll Configuration Manager managed devices](enroll-configmgr.md)
