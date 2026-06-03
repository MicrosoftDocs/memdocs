---
title: Microsoft Intune Government Service overview
description: Learn more about the Intune government service offerings and features. This article is designed to serve as an overview of the Microsoft Intune offering for government community cloud (GCC) High and United States Department of Defense (DoD) environments.
author: MandiOhlinger
ms.author: mandia
ms.date: 06/03/2026
ms.topic: concept-article
ms.reviewer: pfetty
ms.collection:
- M365-identity-device-management
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

:::image type="content" source="./media/government-service/migration-public-government-cloud.png" alt-text="Screenshot that shows the Microsoft government cloud, including GCC High and DoD services, is physically separate from the public cloud and commercial cloud instances.":::

### What you need to know

- There isn't a built-in way to migrate from the commercial service to the government cloud, and vice versa. To migrate, devices need to unenroll from the current tenant, and then re-enroll to the new tenant.

  This approach is similar to unenrolling from another mobile device management (MDM) service and enrolling in Intune. For more information, go to [Deployment guide: Setup or move to Microsoft Intune](setup-migration.md#currently-use-a-third-party-mdm-provider).

- In the government cloud, the Intune service instance is shared with GCC High and DoD tenants. This architecture is slightly different than other services, such as Microsoft 365 and Azure.

- GCC is the same instance as Microsoft Intune in the commercial space. Other services, like Microsoft 365, have a separate GCC instance. Intune doesn't have a separate GCC instance.

  So, when you see **GCC** in this Intune article, it refers to the commercial service. When you see **GCC High** or **DoD**, it refers to the government cloud.

  GCC instances are commonly used by state and local government customers that require extra accreditation for the cloud services they use.

- Intune is now Common Criteria certified and is on the National Information Assurance Partnership (NIAP) Product Compliance List (PCL).

  To see the certification materials, go to [NIAP - Product Details](https://www.niap-ccevs.org/products/11298).

- Administrators can get help locking down their Intune tenants using the Secure Technical Implementation Guide (STIG).

  To get guidance from the `cyber.mil` website, go to the [STIGs Document Library](https://public.cyber.mil/stigs/downloads/?_dl_facet_stigs=mdm-emm) (opens the `public.cyber.mil` website).

## Feature differences in Intune GCC High and DoD

### Available and supported

The following features are available and supported in Microsoft GCC High and/or DoD clouds:

| Feature | Availability |
| --- | --- |
| Standard MDM features | ✅ <br/><br/> You can use app policies, device configuration profiles, compliance policies, and more. |
| Mobile Threat Defense (MTD) | ✅ <br/><br/>Mobile Threat Defense (MTD) connectors for Android and iOS/iPadOS devices with MTD vendors that **also support** the GCC High environment can be used. When you sign in to a GCC High tenant, you see the connectors that are available in these environments. |
| Microsoft Defender for Endpoint security settings management | ✅ <br/><br/> On devices onboarded to Defender but not enrolled in Intune, you can use Intune endpoint security policies to manage Defender security settings. <br/><br/>This support extends to the US Government Community Cloud (GCC), US Government Community High (GCC High), and Department of Defense (DoD) environments. <br/><br/>For more information on this feature, go to [Defender for Endpoint security settings management](../device-security/microsoft-defender/security-settings-management.md). |
| Platform support | ✅ <br/><br/> You can use the same operating systems - Android, Android Open Source Project (AOSP), iOS/iPadOS, Linux, macOS, and Windows. <br/><br/>- **Android (AOSP)**: There are some device restrictions. For more information, go to [Supported operating systems and browsers in Intune - AOSP](ref-supported-platforms.md#android). <br/>- **Linux**: Generally available (GA) in February 2024.|
| Windows Autopilot device preparation | ✅ <br/><br/> Some features are available now, such as user-driven deployments, and some are still [in the planning phase](#in-the-planning-phase). For more information about Windows Autopilot solutions, go to [Compare Windows Autopilot device preparation and Windows Autopilot](/autopilot/device-preparation/compare). <br/><br/> To get started with Windows Autopilot device preparation, go to [Windows Autopilot Device Preparation overview](/autopilot/device-preparation/overview). |
| Log Analytics | ✅ <br/><br/> You can send Intune log data to Azure Storage, Event Hubs, or Log Analytics. <br/><br/> For more information on this feature, go to [Send log data to storage, event hubs, or log analytics from Intune](../governance/integrate-azure-monitor.md). |
| Microsoft Intune Plan 2 </br>and Microsoft Intune Suite | For more information on these plans, go to [Microsoft Intune advanced capabilities](advanced-capabilities.md). <br/><br/> The following Plan 2 features support the GCC High and DoD environments: </br>- [Microsoft Tunnel for Mobile Application Management](../device-security/microsoft-tunnel/mam.md) </br>- [Firmware-over-the-air update](../device-updates/android/manage-fota.md) </br>- [Specialty devices management](../device-management/specialty-devices.md) </br></br>  The following Microsoft Intune Suite features support the GCC High and DoD environments: </br>- [Endpoint Privilege Management](../epm/overview.md) </br>- [Advanced Analytics](../advanced-analytics/index.md)|

### In the planning phase

The following features are currently not available and aren't supported in GCC High and DoD clouds. Planning is underway to support these features for GCC High and DoD environments. If ETAs are available, then they're listed.

| Feature | Availability |
| --- | --- |
| Windows Autopatch | For more information on this feature, go to [What is Windows Autopatch](/windows/deployment/windows-autopatch/overview/windows-autopatch-overview). |
| Feature updates | For more information on this feature, go to [Feature updates for Windows in Intune](../device-updates/windows/manage-feature-updates.md). |
| Quality updates | For more information on this feature, go to [Manage Windows quality updates](../device-updates/windows/manage-quality-updates.md)
| Expedite updates | For more information on this feature, go to [Windows quality updates in Microsoft Intune](../device-updates/windows/configure-expedite-policy.md). |
| Driver updates | For more information on this feature, go to [Configure Windows driver update policies](../device-updates/windows/configure-driver-update-policy.md). |
| Windows Autopilot device preparation | The following features are in the planning phase: - Customize out-of-box experience (OOBE) and rename devices during provisioning based on organizational structure - Self-deploying and pre-provisioning mode - More admin-specified configurations delivered before allowing desktop access. - Enhanced optional desktop onboarding experience inside the Windows Company Portal app - The ability to associate a device with a tenant. Provisioning modes which require Windows Autopilot registration are not supported. To get started with Windows Autopilot device preparation, go to [Windows Autopilot Device Preparation overview](/autopilot/device-preparation/overview). |
| Delivery Optimization for Win32 Apps | For more information on the Delivery Optimization feature in Windows, go to [What is Delivery Optimization?](/windows/deployment/do/waas-delivery-optimization). |
| Windows Device Health Attestation (DHA) | For more information on Device Health Attestation, go to [Device Health Attestation](/windows-server/security/device-health-attestation) |
| BIOS configuration policies on Windows | For more information on this feature, go to [Use BIOS configuration profiles on Windows devices in Microsoft Intune](../device-configuration/templates/configure-bios-windows.md). |
| Device firmware configuration interface (DFCI) | For more information on this feature, go to [Device Firmware Configuration Interface (DFCI) Management](/autopilot/dfci-management). |
| Enterprise Application Management | For more information on this feature, go to [Microsoft Enterprise Application Management (EAM)](../app-management/deployment/enterprise-app-management.md). | 
| Remote Help | For more information on this feature go to [Use Remote Help with Microsoft Intune](../remote-help/index.md). |
| Cloud PKI (GCC High only) | For more information on this feature go to [Overview of Microsoft Cloud PKI for Microsoft Intune](../cloud-pki/index.md) |
| Security Copilot | For more information on this feature go to [What is Microsoft Security Copilot?](/copilot/security/microsoft-security-copilot) |

### Not available

The following features aren't available and there's currently no planning underway to support these features for GCC High and DoD environments:

| Feature | Availability |
| --- | --- |
| [Apple Managed account federation](/entra/external-id/customers/how-to-apple-federation-customers) | ❌ |
| [Chrome Enterprise Connector](../device-enrollment/configure-chrome-enterprise-connector.md) | ❌ |
| [Windows Autopilot](/autopilot/overview) | ❌ |
| [Windows Enterprise multi-session remote desktops (AVD)](../solutions/azure-virtual-desktop-multi-session.md) | ❌ |
| [Windows Diagnostic Data processor configuration](/windows/privacy/configure-windows-diagnostic-data-in-your-organization#enable-windows-diagnostic-data-processor-configuration) | ❌ |
| [App and driver compatibility reports for Windows updates](../device-updates/windows/monitor-compatibility.md) | ❌ |
| [Reports for feature update policies](../device-updates/windows/monitor-feature-updates.md) | ❌ |
| [Windows Backup for Organizations](/windows/configuration/windows-backup/?tabs=intune) | ❌ |
| [eSIM cellular support on Windows](../device-configuration/templates/configure-esim-download-server.md) | ❌ |
| [Windows Subscription Activation](/windows/deployment/windows-subscription-activation?pivots=windows-11) | ❌ |
| [Microsoft Store for Business](/windows/configuration/store/?tabs=intune) | ❌ |
| [Microsoft Connected Cache for Enterprise and Education](/windows/deployment/do/mcc-ent-edu-overview) | ❌ |
| [ServiceNow connector](../device-management/tools/setup-servicenow.md) | ❌ |
| [TeamViewer connector (legacy)](../device-management/tools/teamviewer-legacy.md) and [TeamViewer integration](../device-management/tools/setup-teamviewer.md) | ❌ |
| [Intune PowerBI connector for DWH](/power-query/connectors/) | ❌ |
| [On-premises Exchange Connector] | ❌ |

## Next steps

To learn more about Intune and how to get started, go to the [Microsoft Intune planning guide](planning-guide.md).
