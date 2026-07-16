---
title: Microsoft Intune Government Service overview
description: Learn more about the Intune government service offerings and features. This article is designed to serve as an overview of the Microsoft Intune offering for government community cloud (GCC) High and United States Department of Defense (DoD) environments.
ms.date: 06/04/2026
ms.topic: concept-article
ms.reviewer: acabello
---

# Microsoft Intune for US Government GCC High and DoD service description

> [!NOTE]
> This article applies to Microsoft Intune features only. If you're looking for information on other features, then go to that specific documentation. For example, for Microsoft Teams devices, see [Teams Rooms on Windows and Android](/microsoftteams/rooms/teams-devices-feature-comparison).

The Intune U.S. government service description is as an overview of the service offering in the Government Community Cloud (GCC) High and U.S. Department of Defense (DoD) environments.

This article lists the feature differences compared to the commercial offering of [Microsoft Intune](what-is-intune.md). To learn more about Intune for GCC customers, see [EMS offers for US Government and Microsoft 365 interoperability](/enterprise-mobility-security/solutions/ems-govt-service-description#ems-offers-for-us-government-and-microsoft-365-interoperability).

## Intune commercial and government instances

The Intune GCC High and DoD offerings are built on the Microsoft Azure Government Cloud. This cloud is designed to interoperate with Microsoft 365 GCC High and DoD environments.

Intune has two service instances:

- **Commercial service**: The commercial service is available to anyone with an Intune license and is used by most Intune customers.
- **Government cloud**: This service is also known as **GCC High** or **DoD**. This instance is a datacenter that's physically separate from the commercial instances. The datacenter is locked down and is only used by government customers who purchase the appropriate license.

These government instances are also known as **IL4** and **IL5**, where **IL** refers to Impact Level.

- In the government cloud, the Intune service instance is shared with GCC High and DoD tenants. This architecture is slightly different than other services, such as Microsoft 365 and Azure.

- GCC is the same instance as Microsoft Intune in the commercial space. Other services, like Microsoft 365, have a separate GCC instance. Intune doesn't have a separate GCC instance.

  So, when you see **GCC** in this Intune article, it refers to the commercial service. When you see **GCC High** or **DoD**, it refers to the government cloud.

  GCC instances are commonly used by state and local government customers that require extra accreditation for the cloud services they use.

## Enroll in government tenant

:::image type="content" source="./media/government-service/migration-public-government-cloud.png" alt-text="Screenshot that shows the Microsoft government cloud, including GCC High and DoD services, is physically separate from the public cloud and commercial cloud instances.":::

If your resources are in a commercial tenant and you want to move to the government cloud, the devices need to unenroll from the current tenant, and then re-enroll in the new tenant. There isn't a built-in way to migrate from the commercial service to the government cloud, and vice versa.

This process is similar to unenrolling from another mobile device management (MDM) service and enrolling in Intune. For more information, see [Deployment guide: Setup or move to Microsoft Intune](setup-migration.md#currently-use-a-third-party-mdm-provider).

Administrators can get help locking down their Intune tenants using the Secure Technical Implementation Guide (STIG). To get guidance from the `cyber.mil` website, see the [STIGs Document Library](https://public.cyber.mil/stigs/downloads/?_dl_facet_stigs=mdm-emm) (opens the `public.cyber.mil` website).

## Compliance and certifications

Intune is Common Criteria certified and is on the National Information Assurance Partnership (NIAP) Product Compliance List (PCL). To see the certification materials, see [NIAP - Product Details](https://www.niap-ccevs.org/products/11298).

For information on the US Federal Risk and Authorization Management Program (FedRAMP) accreditation and Microsoft, see [FedRAMP](/compliance/regulatory/offering-fedramp).

## Supported Intune features in GCC High and DoD

The following features are available and supported in Microsoft GCC High and/or DoD clouds:

| Feature | Availability |
|--|--|
| Log Analytics | You can send Intune log data to Azure Storage, Event Hubs, or Log Analytics. <br/><br/> For more information on this feature, see [Send log data to storage, event hubs, or log analytics from Intune](../governance/integrate-azure-monitor.md). |
| Microsoft Defender for Endpoint security settings management | On devices onboarded to Defender but not enrolled in Intune, you can use Intune endpoint security policies to manage Defender security settings. <br/><br/>This support extends to the US Government Community Cloud (GCC), US Government Community High (GCC High), and Department of Defense (DoD) environments. <br/><br/>For more information on this feature, see [Defender for Endpoint security settings management](../device-security/microsoft-defender/security-settings-management.md). |
| Microsoft Intune advanced capabilities | The following Intune advanced capabilities support the GCC High and DoD environments:</br>- [Advanced Analytics](../advanced-analytics/index.md) </br>- [Endpoint Privilege Management](../epm/overview.md) </br>- [Enterprise Application Management (EAM)](../app-management/deployment/enterprise-app-management.md) </br>- [Firmware-over-the-air update](../device-updates/android/manage-fota.md) </br>- [Microsoft Tunnel for Mobile Application Management](../device-security/microsoft-tunnel/mam.md) </br>- [Specialty devices management](../device-management/specialty-devices.md)|
| Mobile Threat Defense (MTD) | Mobile Threat Defense (MTD) connectors for Android and iOS/iPadOS devices with MTD vendors that **also support** the GCC High environment can be used. When you sign in to a GCC High tenant, you see the connectors that are available in these environments. |
| Platform support | You can use the same operating systems - Android, Android Open Source Project (AOSP), iOS/iPadOS, Linux, macOS, and Windows. <br/><br/>- **Android (AOSP)**: There are some device restrictions. For more information, see [Supported operating systems and browsers in Intune - AOSP](ref-supported-platforms.md#android). <br/>- **Linux**: Generally available. |
| Standard MDM features | You can use app policies, device configuration profiles, compliance policies, and more. |
| Windows Autopilot device preparation | Some features are available now, such as user-driven deployments, and some are still [in the planning phase](#intune-features-planned-for-gcc-high-and-dod). For more information about Windows Autopilot solutions, see [Compare Windows Autopilot device preparation and Windows Autopilot](/autopilot/device-preparation/compare). <br/><br/> To get started with Windows Autopilot device preparation, see [Windows Autopilot Device Preparation overview](/autopilot/device-preparation/overview). |

## Intune features planned for GCC High and DoD

The following features are currently not available and aren't supported in GCC High and DoD clouds. Planning is started to support these features for GCC High and DoD environments. If ETAs are available, then they're listed.

| Feature | Feature documentation |
| --- | --- |
| **Advanced capabilities** | [Cloud PKI](../cloud-pki/index.md) (GCC High only) |
| &nbsp; | [Remote Help](../remote-help/index.md) |
| **Autopatch and updates** | [Windows Autopatch](/windows/deployment/windows-autopatch/overview/windows-autopatch-overview) |
| &nbsp; | [Feature updates for Windows in Intune](../device-updates/windows/manage-feature-updates.md) |
| &nbsp; | [Quality updates for Windows in Intune](../device-updates/windows/manage-quality-updates.md) |
| &nbsp; | [Expedite updates for Windows in Intune](../device-updates/windows/configure-expedite-policy.md) |
| &nbsp; | [Driver updates for Windows in Intune](../device-updates/windows/configure-driver-update-policy.md) |
| &nbsp; | [Delivery Optimization for Win32 Apps](/windows/deployment/do/waas-delivery-optimization) |
| **BIOS and DFCI** | [BIOS configuration profiles for Windows in Intune](../device-configuration/templates/configure-bios-windows.md) |
| &nbsp; | [Device Firmware Configuration Interface (DFCI) Management](/autopilot/dfci-management) |
| **Security Copilot** | [What is Microsoft Security Copilot?](/copilot/security/microsoft-security-copilot) |
| **Windows Device Health Attestation (DHA)** | [Device Health Attestation](/windows-server/security/device-health-attestation) |
| **[Windows Autopilot device preparation](/autopilot/device-preparation/overview)** | Customize out-of-box experience (OOBE) and rename devices during provisioning based on organizational structure |
| &nbsp; | Self-deploying and pre-provisioning mode |
| &nbsp; | More admin-specified configurations delivered before allowing desktop access |
| &nbsp; | Enhanced optional desktop onboarding experience inside the Windows Company Portal app |
| &nbsp; | The ability to associate a device with a tenant. Provisioning modes which require Windows Autopilot registration are not supported. |

## Intune features not available in GCC High and DoD

The following features aren't available and there's currently no planning to support these features for GCC High and DoD environments:

| Feature | Availability |
| --- | --- |
| [App and driver compatibility reports for Windows updates](../device-updates/windows/monitor-compatibility.md) | n/a |
| [Apple Managed account federation](/entra/external-id/customers/how-to-apple-federation-customers) | n/a |
| [Chrome Enterprise Connector](../device-enrollment/configure-chrome-enterprise-connector.md) | n/a |
| [eSIM cellular support on Windows](../device-configuration/templates/configure-esim-download-server.md) | n/a |
| [Intune PowerBI connector for DWH](/power-query/connectors/) | n/a |
| [Microsoft Connected Cache for Enterprise and Education](/windows/deployment/do/mcc-ent-edu-overview) | n/a |
| [Microsoft Store for Business](/windows/configuration/store/?tabs=intune) | n/a |
| On-premises Exchange Connector | n/a |
| [Reports for feature update policies](../device-updates/windows/monitor-feature-updates.md) | n/a |
| [ServiceNow connector](../device-management/tools/setup-servicenow.md) | n/a |
| [TeamViewer connector (legacy)](../device-management/tools/teamviewer-legacy.md) and [TeamViewer integration](../device-management/tools/setup-teamviewer.md) | n/a |
| [Windows Autopilot](/autopilot/overview) | n/a |
| [Windows Backup for Organizations](/windows/configuration/windows-backup/?tabs=intune) | n/a |
| [Windows Diagnostic Data processor configuration](/windows/privacy/configure-windows-diagnostic-data-in-your-organization#enable-windows-diagnostic-data-processor-configuration) | n/a |
| [Windows Enterprise multi-session remote desktops (AVD)](../solutions/azure-virtual-desktop-multi-session.md) | n/a |
| [Windows Subscription Activation](/windows/deployment/windows-subscription-activation?pivots=windows-11) | n/a |

## Related content

- [Microsoft Intune planning guide](planning-guide.md)
- [Microsoft Intune licensing](licensing.md)
