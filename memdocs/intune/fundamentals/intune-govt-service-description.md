---
# required metadata

title: Microsoft Intune Government Service overview
description: Learn more about the Intune government service offerings and features. This article is designed to serve as an overview of the Microsoft Intune offering for government community cloud (GCC) High and United States Department of Defense (DoD) environments.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 09/23/2024
ms.topic: article
ms.service: microsoft-intune
ms.suite: ems

# optional metadata
ms.reviewer: pfetty
ms.collection:
- tier1
- M365-identity-device-management
- highpri
---

# Microsoft Intune for US Government GCC High and DoD service description

> [!NOTE]
> This article applies to Microsoft Intune features only. If you're looking for information on other features, then go to that specific documentation. For example, for Microsoft Teams devices, go to [Teams Rooms on Windows and Android](/microsoftteams/rooms/teams-devices-feature-comparison).

The Intune U.S. government service description is as an overview of the service offering in the Government Community Cloud (GCC) High and U.S. Department of Defense (DoD) environments.

This article lists the feature differences compared to the commercial offering of Microsoft Intune.

To learn more about Intune for GCC customers, go to [EMS offers for US Government and Microsoft 365 interoperability](/enterprise-mobility-security/solutions/ems-govt-service-description#ems-offers-for-us-government-and-microsoft-365-interoperability).

> [!TIP]
> For information on the US Federal Risk and Authorization Management Program (FedRAMP) accreditation and Microsoft, go to [FedRAMP](/compliance/regulatory/offering-fedramp).

## Get started with Intune for US Government GCC High and DoD

The Intune GCC High and DoD offerings are built on the Microsoft Azure Government Cloud. This cloud is designed to interoperate with Microsoft 365 GCC High and DoD environments.

For more information about Intune, and what you can do, go to [Microsoft Intune securely manages identities, manages apps, and manages devices](what-is-intune.md). Use this documentation as your starting point for deploying and using Microsoft Intune.

Intune has two service instances:

- **Commercial service**: The commercial service is available to anyone with an Intune license and is used by most Intune customers.
- **Government cloud**: This service is also known as **GCC High** or **DoD**. This instance is a datacenter that's physically separate from the commercial instances. The datacenter is locked down and is only used by government customers who purchase the appropriate license.

These government instances are also known as **IL4** and **IL5**, where **IL** refers to Impact Level.

:::image type="content" source="./media/intune-govt-service-description/migration-public-government-cloud.png" alt-text="Screenshot that shows the Microsoft government cloud, including GCC High and DoD services, is physically separate from the public cloud and commercial cloud instances.":::

### What you need to know

- There isn't a built-in way to migrate from the commercial service to the government cloud, and vice versa. To migrate, devices need to unenroll from the current tenant, and then re-enroll to the new tenant.

  This approach is similar to unenrolling from another mobile device management (MDM) service and enrolling in Intune. For more information, go to [Deployment guide: Setup or move to Microsoft Intune](deployment-guide-intune-setup.md#currently-use-a-third-party-mdm-provider).

- In the government cloud, the Intune service instance is shared with GCC High and DoD tenants. This architecture is slightly different than other services, such as Microsoft 365 and Azure.

- GCC is the same instance as Microsoft Intune in the commercial space. Other services, like Microsoft 365, have a separate GCC instance. Intune doesn't have a separate GCC instance.

  So, when you see **GCC** in this Intune article, it refers to the commercial service. When you see **GCC High** or **DoD**, it refers to the government cloud.

  GCC instances are commonly used by state and local government customers that require extra accreditation for the cloud services they use.

## Feature differences in Intune GCC High and DoD

### Available and supported

The following features are available and supported in Microsoft GCC High and/or DoD clouds:

| Feature | Availability |
| --- | --- |
| Standard MDM features | ✅ <br/><br/> You can use app policies, device configuration profiles, compliance policies, and more. |
| Mobile Threat Defense (MTD) | ✅ <br/><br/>Mobile Threat Defense (MTD) connectors for Android and iOS/iPadOS devices with MTD vendors that **also support** the GCC High environment can be used. When you sign in to a GCC High tenant, you see the connectors that are available in these environments. |
| Microsoft Defender for Endpoint security settings management | ✅ <br/><br/> On devices onboarded to Defender but not enrolled in Intune, you can use Intune endpoint security policies to manage Defender security settings. For more information on this feature, go to [Defender for Endpoint security settings management](../protect/mde-security-integration.md). |
| Platform support | ✅ <br/><br/> You can use the same operating systems - Android, AOSP, iOS/iPadOS, Linux, macOS, and Windows. <br/><br/>- **Android (AOSP)**: There are some device restrictions. For more information, go to [Supported operating systems and browsers in Intune - AOSP](supported-devices-browsers.md#android). <br/>- **Linux**: Generally available (GA) in February 2024.|
| Remote Help | ✅ <br/><br/> Remote Help is supported in GCC on Android, macOS, and Windows devices. It's not supported in GCC High or DoD.<br/><br/> For more information on this feature, go to [Remote Help in Microsoft Intune](../fundamentals/remote-help.md). |
| Windows Autopilot device preparation | ✅ <br/><br/> Some features are available now, such as user-driven deployments, and some are still [in the planning phase](#in-the-planning-phase). For more information on the recent changes to Windows Autopilot device preparation, go to [Blog: Windows deployment with the next generation of Windows Autopilot](https://techcommunity.microsoft.com/t5/microsoft-intune-blog/windows-deployment-with-the-next-generation-of-windows-autopilot/ba-p/4148169). <br/><br/> To get started with Windows Autopilot device preparation, go to [Windows Autopilot Device Preparation overview](/autopilot/device-preparation/overview). |
| Log Analytics | ✅ <br/><br/> You can send Intune log data to Azure Storage, Event Hubs, or Log Analytics. <br/><br/> For more information on this feature, go to [Send log data to storage, event hubs, or log analytics from Intune](review-logs-using-azure-monitor.md). |
| Microsoft Intune Plan 2 </br>and Microsoft Intune Suite | For more information on these plans, go to [Use Intune Suite add-on capabilities](intune-add-ons.md). <br/><br/> The following Plan 2 features support the GCC High and DoD environements: </br>- [Microsoft Tunnel for Mobile Application Management](../protect/microsoft-tunnel-mam.md) </br>- [Firmware-over-the-air update](../protect/fota-updates-android.md) </br>- [Specialty devices management](../fundamentals/specialty-devices-with-intune.md) </br></br>  The following Microsoft Intune Suite features support the GCC High and DoD environements: </br>- [Endpoint Privilege Management](../protect/epm-overview.md) </br>- [Advanced Analytics](../../analytics/advanced-endpoint-analytics.md)  - With this release, GCC High and DoD support for Advanced Endpoint Analytics not include the [*Device query*](../../analytics/device-query.md) functionality.|

### In the planning phase

The following features are currently not available and aren't supported in GCC High and DoD clouds. Planning is underway to support these features for GCC High and DoD. If ETAs are available, then they're listed.

| Feature | Availability |
| --- | --- |
| Expedited updates | For more information on this feature, go to [Expedite Windows quality updates in Microsoft Intune](../protect/windows-10-expedite-updates.md). |
| Feature updates | For more information on this feature, go to [Feature updates for Windows in Intune](../protect/windows-10-feature-updates.md). |
| Windows Autopilot | The following features are in the planning phase: </br></br>- Customize out-of-box experience (OOBE) and rename devices during provisioning based on organizational structure </br>- Self-deploying and pre-provisioning mode </br> - More admin-specified configurations delivered before allowing desktop access. </br> - Enhanced optional desktop onboarding experience inside the Windows Company Portal app </br> - The ability to associate a device with a tenant. </br></br>For information about Windows Autopilot, go to [Windows Autopilot overview](/autopilot/overview). |

### Not available

The following features aren't available and won't be supported for GCC High and DoD:

| Feature | Availability |
| --- | --- |
| Chrome OS Connector | ❌ |
| Microsoft Store for Business | ❌ |
| On-premises Exchange Connector | ❌ |
| [TeamViewer connector](../remote-actions/teamviewer-support.md) </br>or TeamViewer feature | ❌ |

## Next steps

To learn more about Intune and how to get started, go to the [Microsoft Intune planning guide](intune-planning-guide.md).
