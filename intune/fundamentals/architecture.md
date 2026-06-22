---
title: Microsoft Intune architecture
description: Reference architecture for a Microsoft Intune deployment, including cloud and on-premises components and Microsoft and third-party integrations.
author: paolomatarazzo
ms.author: paoloma
ms.date: 05/12/2026
ms.topic: concept-article
ms.reviewer: davidra
ms.collection:
- M365-identity-device-management
- triage
---

# Microsoft Intune architecture

This article describes the architecture of a Microsoft Intune deployment: the cloud and on-premises components and the Microsoft and third-party products Intune integrates with.

For an introduction to what Intune does, see [What is Microsoft Intune?](what-is-intune.md). For a conceptual walkthrough of how Intune manages identities, devices, and apps, see [Microsoft Intune core concepts](core-concepts.md).

:::image type="content" source="./media/architecture/intune-reference-architecture.png" alt-text="Diagram that shows Microsoft Intune in a reference architecture with Microsoft Entra, Microsoft 365, Configuration Manager, on-premises connectors, and managed endpoints." lightbox="./media/architecture/intune-reference-architecture.png" border="false":::

The diagram organizes a typical Intune deployment into seven tiers:

1. **Cloud control plane**: Microsoft-hosted Intune services.
1. **Managed endpoints**: devices that Intune manages.
1. **Endpoint family services**: Microsoft products whose primary purpose is endpoint management.
1. **Connectors and extensions**: cloud-based external services Intune integrates with.
1. **Peer integrations**: other Microsoft products that integrate with Intune.
1. **Partner ecosystem**: third-party products and services that integrate with Intune.
1. **On-premises services**: customer-operated infrastructure that integrates with the Intune cloud.

Each tier is described in the following sections.

## Cloud control plane

:::row:::
    :::column:::
        The cloud control plane is the set of Microsoft-hosted services that constitute the Intune tenant. They store configurations, deliver policy, expose programmatic interfaces, and surface the admin and user experiences.
    :::column-end:::
    :::column:::
        :::image type="content" source="media/architecture/cloud-control-plane.png" alt-text="Diagram of the cloud control plane." border="false" lightbox="media/architecture/cloud-control-plane-on.png":::
    :::column-end:::
:::row-end:::

| Component | Role |
|---|---|
| **Microsoft Intune service** | The cloud control plane that stores configurations and orchestrates policy delivery. |
| **[Microsoft Intune admin center]** | Web console for administrators. |
| **[Microsoft Graph API](/graph/intune-concept-overview)** | Public programming interface. Every admin center action is backed by a Graph API call. |
| **[Microsoft Intune Company Portal app and website](../app-management/configuration/configure-company-portal.md)** | User-facing surface that enrolls devices, surfaces required apps, and shows compliance status. |

## Managed endpoints

:::row:::
    :::column:::
        Intune supports the following platforms: Android, iOS, iPadOS, Linux, macOS, tvOS, visionOS, and Windows. Specialty scenarios include kiosks, frontline devices, and rugged hardware managed through platform-specific enrollment paths.
    :::column-end:::
    :::column:::
        :::image type="content" source="media/architecture/managed-endpoints.png" alt-text="Diagram of managed endpoints as they relate to the cloud control plane." border="false" lightbox="media/architecture/managed-endpoints-on.png":::
    :::column-end:::
:::row-end:::

Devices come under management through several modes:

- **Mobile device management (MDM)**: typical for organization-owned devices; Intune manages the entire device.
- **Mobile application management (MAM)**: typical for personal (BYOD) devices; Intune manages only work apps and data.
- **Automated enrollment** for organization-owned hardware: Windows Autopilot, Apple Automated Device Enrollment, and Android Enterprise.

For the full supported-OS matrix, see [Supported operating systems and browsers for Intune](ref-supported-platforms.md).

## Endpoint family services

:::row:::
    :::column:::
        Endpoint family services are Microsoft products whose primary purpose is endpoint management. Each specializes in a specific aspect of the endpoint lifecycle.
    :::column-end:::
    :::column:::
        :::image type="content" source="media/architecture/endpoint-family-services.png" alt-text="Diagram of endpoint family services as they relate to the cloud control plane." border="false" lightbox="media/architecture/endpoint-family-services-on.png":::
    :::column-end:::
:::row-end:::



| Service | What it does | When to use |
|---|---|---|
| **[Windows Autopilot](/autopilot/overview)** | Cloud-based provisioning for new and existing Windows devices, with options for user-driven, self-deploying (zero-touch), pre-provisioning, and reset | Shipping devices directly from OEM to end users, or repurposing existing devices at scale |
| **[Windows 365](/windows-365/enterprise/overview)** | Cloud-hosted Windows desktops (Cloud PCs) | Remote workers, BYOD, contractors, regulated workloads |
| **[Windows Autopatch](/windows/deployment/windows-autopatch/overview/windows-autopatch-overview)** | Managed update service for Windows, Microsoft 365 Apps for enterprise, Microsoft Edge, Microsoft Teams, and device drivers and firmware | Reducing manual update administration |
| **[Endpoint analytics](../endpoint-analytics/index.md)** | Telemetry and recommendations on device health and performance | Identifying performance issues and reducing help-desk volume |

## Connectors and extensions

:::row:::
    :::column:::
        Connectors and extensions are cloud-based external services that Intune integrates with. They have no on-premises footprint. Intune communicates with them over the internet.
    :::column-end:::
    :::column:::
        :::image type="content" source="media/architecture/connectors-and-extensions.png" alt-text="Diagram of connectors and extensions as they relate to the cloud control plane." border="false" lightbox="media/architecture/connectors-and-extensions-on.png":::
    :::column-end:::
:::row-end:::

| Connector | Role |
|---|---|
| **[Microsoft Cloud PKI](../cloud-pki/index.md)** | Cloud-hosted PKI that issues, renews, and revokes SCEP certificates for Intune-managed devices without requiring on-premises AD CS, NDES, or the certificate connector. Supports a fully cloud-hosted hierarchy or anchoring to your existing private root (BYOCA). |
| **[Apple Business / VPP](../app-management/deployment/manage-vpp-apple.md)** | Token-based integration for Apple app delivery. |
| **[Apple Push Notification service (APNs)](../device-enrollment/apple/create-mdm-push-certificate.md)** | Required for Apple device management. |
| **[Managed Google Play](../app-management/deployment/add-managed-google-play.md)** | Android Enterprise app catalog. |
| **[Microsoft Store](../app-management/deployment/add-microsoft-store.md)** | Built-in catalog for Windows apps. |

## Peer integrations

:::row:::
    :::column:::
        Peer integrations are Microsoft products that work alongside Intune. They have their own primary purpose; integration with Intune is one of many uses.
    :::column-end:::
    :::column:::
        :::image type="content" source="media/architecture/peer-integrations.png" alt-text="Diagram of peer integrations as they relate to the cloud control plane." border="false" lightbox="media/architecture/peer-integrations-on.png":::
    :::column-end:::
:::row-end:::

| Product | Role |
|---|---|
| **[Microsoft 365 apps](../app-management/deployment/add-microsoft-365-windows.md)** | Deployed to managed endpoints via Intune. |
| **[Endpoint security in Microsoft Defender](../device-security/microsoft-defender/configure-integration.md)** | Feeds real-time device risk signals into Intune compliance evaluation and Conditional Access decisions. Also serves as a mobile threat defense (MTD) source for iOS, iPadOS and Android. |
| **[Copilot in Intune](../copilot/index.md)** | Microsoft Security Copilot capabilities surfaced inside the Microsoft Intune admin center. |
| **[Microsoft Purview](/purview/device-onboarding-mdm)** | Sensitivity labels and endpoint data loss prevention (DLP) policies that apply to data on Intune-managed devices. |

## Partner ecosystem

:::row:::
    :::column:::
        The partner ecosystem includes third-party products and services that integrate with Intune through documented APIs, connectors, or configuration patterns.
    :::column-end:::
    :::column:::
        :::image type="content" source="media/architecture/partner-ecosystem.png" alt-text="Diagram of the partner ecosystem as it relates to the cloud control plane." border="false" lightbox="media/architecture/partner-ecosystem-on.png":::
    :::column-end:::
:::row-end:::

| Category | Description and examples |
|---|---|
| **[Mobile threat defense (MTD) partners](../device-security/mobile-threat-defense/overview.md)** | Third-party services that feed device risk signals into Intune. Examples: Lookout, Zimperium, Check Point. Endpoint security in Microsoft Defender is also an MTD source: see [Peer integrations](#peer-integrations). |
| **[Device compliance partners](../device-security/compliance/third-party-partners.md)** | Non-Intune MDMs that become the MDM authority for assigned user groups and report device compliance state into Microsoft Entra ID for Intune Conditional Access. Supported on Android, iOS, iPadOS, and macOS. Examples: Jamf Pro, Ivanti EPMM, BlackBerry UEM, Omnissa Workspace ONE, Kandji, SOTI MobiControl. |
| **IT service management (ITSM) partners** | Incident and asset integration. Examples: [ServiceNow](../device-management/tools/setup-servicenow.md), Jira. |
| **Remote support partners** | Remote control and assistance. Example: [TeamViewer](../device-management/tools/setup-teamviewer.md). |
| **Device vendor portals** | Vendor-specific management for specialty hardware. Examples: [Surface Management Portal](/surface/surface-management-portal), Lenovo, Intel vPro. |
| **Network access control (NAC) partners** | Network-tier access enforcement. Examples: Cisco ISE, Aruba ClearPass. |

## On-premises services

:::row:::
    :::column:::
        On-premises services are customer-operated infrastructure that runs on your network and integrates with the Intune cloud control plane.
    :::column-end:::
    :::column:::
        :::image type="content" source="media/architecture/on-premises-services.png" alt-text="Diagram of on-premises services as they relate to the cloud control plane." border="false" lightbox="media/architecture/on-premises-services-on.png":::
    :::column-end:::
:::row-end:::

| Component | Role |
|---|---|
| **[Microsoft Tunnel Gateway](../device-security/microsoft-tunnel/overview.md)** | VPN gateway for iOS, iPadOS and Android Enterprise devices and apps. Runs in a container on Linux. |
| **[Certificate Connector for Microsoft Intune](certificates/connector/overview.md)** | Bridges Intune to your on-premises certificate services to issue SCEP and PKCS certificates, import PFX certificates for S/MIME, and revoke certificates. |
| **[Microsoft Configuration Manager](../configmgr/core/understand/introduction.md)** | On-premises peer to Intune for Windows clients and servers. Integrates with Intune through co-management and tenant attach. See [Co-management and tenant attach](#co-management-and-tenant-attach). |

### Co-management and tenant attach

Microsoft Configuration Manager is the on-premises peer to Intune for Windows clients and servers. It manages desktops, Windows servers, and laptops on your network or connected over the internet via cloud management gateway. Configuration Manager and Intune integrate through:

- **[Co-management](../configmgr/comanage/overview.md)**: lets Configuration Manager and Intune both manage Windows clients. You move workloads to the cloud at your own pace.
- **[Tenant attach](../configmgr/tenant-attach/prerequisites.md)**: brings Configuration Manager-managed devices into the Intune admin center for visibility, remote actions, cloud-based reporting, endpoint security policy authoring (Antivirus, ASR), CMPivot, PowerShell scripts, application installs, and a unified device timeline.

By using co-management and tenant attach, organizations that already run Configuration Manager can add Intune capabilities without rebuilding their environment.

## Related content

- [What is Microsoft Intune?](what-is-intune.md)
- [Microsoft Intune core concepts](core-concepts.md)
- [Network endpoints for Microsoft Intune](endpoints.md)
- [Common ways to deploy Microsoft Intune](deploy-setup-step-1.md)
- [Cloud-native endpoints](../solutions/cloud-native-endpoints/overview.md)
- [Microsoft Intune advanced capabilities](advanced-capabilities.md)
- [Passwordless authentication with Microsoft Intune](../solutions/passwordless.md)

<!--links-->

[Microsoft Intune admin center]: https://go.microsoft.com/fwlink/?linkid=2109431