---
title: Mobile Threat Defense with Microsoft Intune
description: Use Intune Mobile Threat Defense (MTD) with your Mobile Threat Defense partner to protect access to company resources based on device risk.
author: brenduns
ms.author: brenduns
ms.date: 01/26/2026
ms.topic: article
ms.reviewer: ilwu
ms.collection:
- M365-identity-device-management
- sub-mtd-apps
---

# Mobile Threat Defense integration with Intune

> [!NOTE]
>
> This article is about third-party Mobile Threat Defense vendors, for more information on Microsoft Defender for Endpoint, see [Microsoft Defender for Endpoint](../protect/microsoft-defender-with-intune.md).

Intune can integrate data from a Mobile Threat Defense (MTD) vendor as an information source for device compliance policies and device Conditional Access rules. You can use this information to help protect corporate resources like Exchange and SharePoint, by blocking access from compromised mobile devices.

Intune can use this same data as a source for unenrolled devices using Intune app protection policies. As such, admins can use this information to help protect corporate data within a [Microsoft Intune protected app](../apps/apps-supported-intune-apps.md), and issue a block or selective wipe.

## Government cloud support

Mobile Threat Defense (MTD) connectors for Android and iOS/iPadOS devices are available in the following sovereign clouds, provided that the MTD partners also support these environments. Upon logging into your tenant, you'll be able to view the available connectors in that specific environment:

- U.S. Government Community Cloud (GCC) High
- 21Vianet

Learn more about Intune and government clouds:

- [Microsoft Intune for US Government GCC High support](/enterprise-mobility-security/solutions/ems-intune-govt-service-description)
- [Microsoft Intune for US Government GCC High and DoD service description](../fundamentals/intune-govt-service-description.md)
- [Microsoft Intune operated by 21Vianet in China](../fundamentals/china.md)

## Protect corporate resources

Integrating information from MTD vendors can help you protect your corporate resources from threats that affect mobile platforms.

Typically, companies are proactive in protecting PCs from vulnerabilities and attack while mobile devices often go unmonitored and unprotected. Where mobile platforms have built-in protection such as app isolation and vetted consumer app stores, these platforms remain vulnerable to sophisticated attacks. As more employees use devices for work and to access sensitive information, the information from MTD vendors can help you protect devices and your resources from increasingly sophisticated attacks.

## Intune Mobile Threat Defense connectors

Intune uses a Mobile Threat Defense connector to create a channel of communication between Intune and your chosen MTD vendor. Intune MTD partners offer intuitive, easy to deploy applications for mobile devices. These applications actively scan and analyze threat information to share with Intune. Intune can use the data for either reporting or enforcement purposes.

For example: A connected MTD app reports to the MTD vendor that a phone on your network is currently connected to a network that is vulnerable to Man-in-the-Middle attacks. This information is categorized to an appropriate risk level of low, medium, or high. This risk level is then compared with the risk level allowances you set in Intune. Based on this comparison, access to certain resources of your choice can be revoked while the device is compromised.

### Connector status

Once you add a Mobile Threat Defense connector to your tenant, the status displays one of the following states:

| Connector status     | Definition | Device threat messages blocked?     | App Sync request messages blocked? | Certificate Sync request messages blocked? |
|--------------|-----------|------------|------------|------------|
| **Unavailable**| Connector is/was deprovisioned. The MTD partner needs to talk to Intune to provision it once more. | Yes (starting 2308) | Yes (starting 2308) | Yes (starting 2601) |
| **Not Set Up**| Connector setup isn't complete. There may be additional steps or permissions required within Intune or the MTD partner for this status to change to **Available** | Yes (starting 2309) | Yes (starting 2309) | Yes (starting 2601) |
| **Available**| Connector setup is complete. At least one platform toggle must be turned on for this status to change to **Enabled**. | No | No | No |
| **Enabled**| Connector setup is complete, and at least one platform toggle is currently turned on for this connector. | No | No | No |
| **Unresponsive**| Connector isn't responsive. If the connector status continues to be unresponsive for the days defined in **Number of days until partner is unresponsive**, Intune ignores the compliance state.| No | No | No |
| **Error**| Connector has an error code. Some MTD partners may choose to send this in an error case. | No | No | No |

## Data that Intune collects for Mobile Threat Defense

Intune can collect and share two types of inventory data with Mobile Threat Defense (MTD) partners to enhance threat analysis capabilities. Both services are opt-in; no information is shared by default. An Intune administrator must explicitly enable these features in the Mobile Threat Defense connector settings before any data is shared.

### App inventory (App Sync)

**App Sync for iOS/iPadOS devices** allows MTD partners to request metadata about applications installed on enrolled devices. When enabled, inventories from both corporate and personally owned iOS/iPadOS devices are sent to your MTD service provider during device check-in intervals.

**Data shared includes:**
- App ID
- App Version
- App Short Version
- App Name
- App Bundle Size
- App Dynamic Size
- Whether the app is ad-hoc code-signed (starting 2309)
- Whether the app is installed from the app store (starting 2309)
- Whether the app is a beta app (installed via TestFlight) (starting 2309)
- Whether the app is a device-based volume purchased app (starting 2309)
- Whether the app is validated or not
- Whether the app is managed or not

### Certificate inventory (Certificate Sync)

**Certificate Sync for iOS/iPadOS devices** allows supported MTD partners to request information about certificates installed on enrolled devices. When enabled, certificate inventories from both corporate and personally owned iOS/iPadOS devices are sent to your MTD service provider during device check-in intervals.

**Data shared includes:**  
- Account ID
- Entra ID Device ID
- Device Owner
- Certificate List
  - Common Name
  - Data
  - Is Identity

**Certificate Sync is supported by the following Mobile Threat Defense partners:**  
- Zimperium

## Sample scenarios for enrolled devices using device compliance policies

When a device is considered infected by the Mobile Threat Defense solution:

![Image showing a Mobile Threat Defense infected device](./media/mobile-threat-defense/MTD-image-1.png)

Access is granted when the device is remediated:

![Image showing a Mobile Threat Defense Access granted](./media/mobile-threat-defense/MTD-image-2.png)

## Sample scenarios for unenrolled devices using Intune app protection policies

When a device is considered infected by the Mobile Threat Defense solution:  
![Image that shows a Mobile Threat Defense infected device](./media/mobile-threat-defense/MTD-image-3.png)

Access is granted when the device is remediated:  
![Image showing a Mobile Threat Defense access granted](./media/mobile-threat-defense/MTD-image-4.png)

> [!NOTE]
> We recommend using one Mobile Threat Defense vendor per tenant per platform.
>
> For Device Compliance, you can use multiple Mobile Defense vendors with a single Intune tenant. However, when two or more vendors are configured for use for the same platform, all devices that run that platform must install each MTD app and scan for threats. Failure to submit a scan from any configured app results in the device being marked as non-compliant.
>
> This recommendation does not apply to Microsoft Defender for Endpoint. You can use Defender for Endpoint with a third-party MTD app and check compliance separately by deploying different compliance policies to different groups.

## Mobile Threat Defense partners

Learn how to protect access to company resource based on device, network, and application risk with:

- [Better Mobile](better-mobile-threat-defense-connector.md) - *(Android, iOS/iPadOS)*
- [BlackBerry Protect Mobile](blackberry-mobile-threat-defense-connector.md) - *(Android, iOS/iPadOS)*
- [Check Point Harmony Mobile](checkpoint-sandblast-mobile-mobile-threat-defense-connector.md) - *(Android, iOS/iPadOS)*
- [CrowdStrike Falcon for Mobile](crowdstrike-falcon-defense-connector.md) - *(Android, iOS/iPadOS)*
- [iVerify Enterprise](iverify-mobile-threat-defense-connector.md) - *(Android, iOS/iPadOS)*
- [Jamf Mobile Threat Defense](jamf-mtd-connector.md) - *(Android, iOS/iPadOS)*
- [Lookout for Work](lookout-mobile-threat-defense-connector.md) - *(Android, iOS/iPadOS)*
- [Microsoft Defender for Endpoint](../protect/microsoft-defender-with-intune.md) - *(Android, iOS/iPadOS, Windows)*
- [Pradeo](pradeo-mobile-threat-defense-connector.md) - *(Android, iOS/iPadOS)*
- [SentinelOne](Sentinelone-mobile-threat-defense-connector.md) - *(Android, iOS/iPadOS)*
- [Sophos Mobile](sophos-mtd-connector.md) - *(Android, iOS/iPadOS)*
- [Symantec Endpoint Protection Mobile](skycure-mobile-threat-defense-connector.md) - *(Android, iOS/iPadOS)*
- [Trellix Mobile Security](trellix-mobile-threat-defense-connector.md) - *(Android, iOS/iPadOS)*
- [Trend Micro Mobile Security as a Service](trend-micro-mobile-threat-defense-connector.md) - *(Android, iOS/iPadOS)*
- [Windows Security Center](../apps/protect-mam-windows.md) - *(Windows)* - *For information about the Windows versions that support this connector, see [Data protection for Windows MAM](../apps/protect-mam-windows.md).*
- [Zimperium](zimperium-mobile-threat-defense-connector.md) - *(Android, iOS/iPadOS)*
