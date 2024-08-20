---
# required metadata

title: Mobile Threat Defense with Microsoft Intune
titleSuffix: Microsoft Intune
description: Use Intune Mobile Threat Defense (MTD) with your Mobile Threat Defense partner to protect access to company resources based on device risk.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 08/21/2024
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.assetid: ac77b590-a7ec-45a0-9516-ebf5243b6210

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: demerson
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
- sub-mtd-apps
---

# Mobile Threat Defense integration with Intune

> [!NOTE]
>
> This article is about third-party Mobile Threat Defense vendors, for more information on Microsoft Defender for Endpoint, see [Microsoft Defender for Endpoint](../protect/advanced-threat-protection.md).

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

| Connector status     | Definition | Device threat messages blocked?     | AppSync request messages blocked? |
|--------------|-----------|------------|------------|
| **Unavailable**| Connector is/was deprovisioned. The MTD partner needs to talk to Intune to provision it once more. | Yes (starting 2308) | Yes (starting 2308) |
| **Not Set Up**| Connector setup isn't complete. There may be additional steps or permissions required within Intune or the MTD partner for this status to change to **Available** | Yes (starting 2309) | Yes (starting 2309) |
| **Available**| Connector setup is complete. At least one platform toggle must be turned on for this status to change to **Enabled**. | No | No |
| **Enabled**| Connector setup is complete, and at least one platform toggle is currently turned on for this connector. | No | No |
| **Unresponsive**| Connector isn't responsive. If the connector status continues to be unresponsive for the days defined in **Number of days until partner is unresponsive**, Intune ignores the compliance state.| No | No |
| **Error**| Connector has an error code. Some MTD partners may choose to send this in an error case. | No | No |

## Data that Intune collects for Mobile Threat Defense

If enabled, Intune collects app inventory information from both personal and corporate-owned devices and makes it available for MTD providers to fetch, such as Lookout for Work. You can collect an app inventory from the users of iOS devices.

This service is opt-in; no app inventory information is shared by default. An Intune administrator must enable **App Sync for iOS devices** in the Mobile Threat Defense connector settings before any app inventory information is shared.

**App inventory**  
If you enable App Sync for iOS/iPadOS devices, inventories from both corporate and personally owned iOS/iPadOS devices are sent to your MTD service provider. Data in the app inventory includes:

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

## Sample scenarios for enrolled devices using device compliance policies

When a device is considered infected by the Mobile Threat Defense solution:

![Image showing a Mobile Threat Defense infected device](./media/mobile-threat-defense/MTD-image-1.png)

Access is granted when the device is remediated:

![Image showing a Mobile Threat Defense Access granted](./media/mobile-threat-defense/MTD-image-2.png)

## Sample scenarios for unenrolled devices using Intune app protection policies

When a device is considered infected by the Mobile Threat Defense solution:<br>
![Image that shows a Mobile Threat Defense infected device](./media/mobile-threat-defense/MTD-image-3.png)

Access is granted when the device is remediated:<br>
![Image showing a Mobile Threat Defense access granted](./media/mobile-threat-defense/MTD-image-4.png)

> [!NOTE]
> We recommend using one Mobile Threat Defense vendor per tenant per platform.
>
> For Device Compliance, you can use multiple Mobile Defense vendors with a single Intune tenant. However, when two or more vendors are configured for use for the same platform, all devices that run that platform must install each MTD app and scan for threats. Failure to submit a scan from any configured app results in the device being marked as non-compliant.
>
> This recommendation does not apply to Microsoft Defender for Endpoint. You can use Defender for Endpoint with a third-party MTD app and check compliance separately by deploying different compliance policies to different groups.

## Mobile Threat Defense partners

Learn how to protect access to company resource based on device, network, and application risk with:

- [Better Mobile](better-mobile-threat-defense-connector.md)
- [BlackBerry Protect Mobile](blackberry-mobile-threat-defense-connector.md)
- [Check Point Harmony Mobile](checkpoint-sandblast-mobile-mobile-threat-defense-connector.md)
- [CrowdStrike Falcon for Mobile](crowdstrike-falcon-defense-connector.md)
- [Jamf Mobile Threat Defense](jamf-mtd-connector.md)
- [Lookout for Work](lookout-mobile-threat-defense-connector.md)
- [Microsoft Defender for Endpoint](../protect/advanced-threat-protection.md)
- [Pradeo](pradeo-mobile-threat-defense-connector.md)
- [SentinelOne](Sentinelone-mobile-threat-defense-connector.md)
- [Sophos Mobile](sophos-mtd-connector.md)
- [Symantec Endpoint Protection Mobile](skycure-mobile-threat-defense-connector.md)
- [Trellix Mobile Security](trellix-mobile-threat-defense-connector.md)
- [Trend Micro Mobile Security as a Service](trend-micro-mobile-threat-defense-connector.md)
- [Windows Security Center](../apps/protect-mam-windows.md) *(Supports integration with Windows MAM)*
- [Zimperium](zimperium-mobile-threat-defense-connector.md)