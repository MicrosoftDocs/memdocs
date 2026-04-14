---
title: iVerify Enterprise Mobile Threat Defense with Intune
description: Set up iVerify Enterprise Mobile Security with Microsoft Intune to control mobile device access to your corporate resources.
author: brenduns
ms.author: brenduns
ms.date: 12/02/2025
ms.topic: how-to
ms.reviewer: ilwu
ms.collection:
- M365-identity-device-management
- sub-mtd-apps
---

# Use iVerify Enterprise with Microsoft Intune

You can use iVerify Enterprise as a Mobile Threat Defense and Endpoint Detection and Response
(EDR) solution that integrates seamlessly with Microsoft Intune. Risk is assessed based on comprehensive, real-time telemetry collected from devices running the iVerify app.

You can configure Conditional Access policies based on the iVerify risk assessment, enabled through Intune device compliance policies. These policies automatically allow or block noncompliant devices from accessing corporate resources based on detected threats and vulnerabilities.

## Prerequisites

Before setting up the iVerify Enterprise connector, ensure you have the following subscriptions:

- Microsoft Entra ID P1
- Microsoft Intune Plan 1 subscription
- iVerify Enterprise subscription. See the [iVerify Enterprise website](https://iverify.io/products/enterprise-protection)

## Supported platforms

The iVerify Enterprise connector supports the following device platforms:

- Android 9.0 and later
- iOS/iPadOS 15.0 and later

Devices must run the iVerify Enterprise app:

- [Apple Store](https://apps.apple.com/us/app/iverify-enterprise/id6677005195)
- [Google Play](https://play.google.com/store/apps/details?id=com.trailofbits.iverify.orgs&utm_source=na_Med)


## Integrate iVerify Enterprise with Intune to help protect your company resources

The integration of iVerify Enterprise with Microsoft Intune ensures corporate resources are accessed only by safe, secure and compliant mobile devices. The iVerify app captures deep real-time system and log telemetry to detect both advanced and common threats, including operating system exploitation, malicious applications, and network-level risks. 

iVerify streams telemetry to its cloud for rapid risk assessment, reporting a definitive risk score to Intune using the Intune Mobile Threat Defense connector for iVerify. This updates device compliance. If a threat is detected, the device is marked noncompliant, and your Conditional Access policies block access to sensitive resources. The iVerify app then guides users to remediation, quickly restoring compliance and access while protecting the enterprise.

For step-by-step guidance to set up and integrate iVerify with Intune, see the iVerify documentation at [Connecting iVerify Enterprise with Microsoft Intune](https://edr.iverify.io/docs/iverify-portal-guide/Integrations/intune-mtd). To access iVerify content, you must sign in to your iVerify subscription.

## Common scenarios:

Here are some common scenarios:

### Control access based on threats to the operating system

When iVerify detects a threat to the operating system, such as a zero-click attack or device rooting, you can block device access until the threat is resolved. This includes:

- Connecting to corporate email
- Syncing corporate files with the OneDrive for Work app
- Accessing company Line-of-Business (LOB) apps
- Blocking access to corporate networks

:::image type="content" source="./media/iverify-mobile-threat-defense-connector/iverify-malicious-access-blocked.png" alt-text="Diagram of product flow for blocking threats to the device operating system."::: 

 ### Control access based on threats from malicious applications

When an application behaves in a malicious way, such as stealing credentials or accessing sensitive APIs, you can block device access until the threat is resolved.

:::image type="content" source="./media/iverify-mobile-threat-defense-connector/iverify-malicious-apps-blocked.png" alt-text="Diagram of product flow for blocking access due to malicious apps.":::

### Control access based on network threats

You can detect threats like Man-in-the-Middle (MiTM) attacks, malicious SSL certificates, or malicious cellular networks and protect access to corporate data based on the device's network security risk.

:::image type="content" source="./media/iverify-mobile-threat-defense-connector/iverify-network-wifi-blocked.png" alt-text="Diagram of product flow for blocking access to the organizations files due to an alert.":::

## Related content

- [Mobile Threat Defense with Microsoft Intune](mobile-threat-defense.md) 
- [Create device compliance policy for Mobile Threat Protection](mtd-device-compliance-policy-create.md)
- [Enable mobile threat connectors in Intune](mtd-connector-enable.md)