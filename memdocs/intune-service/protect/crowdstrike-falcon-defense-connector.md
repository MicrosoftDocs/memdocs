---
# required metadata

title: Use CrowdStrike Falcon for Mobile with Microsoft Intune
titleSuffix: Microsoft Intune
description: How to set up CrowdStrike Falcon Threat Defense with Microsoft Intune control mobile device access to your corporate resources.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 02/12/2025
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.assetid:
# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier3
- M365-identity-device-management
- sub-mtd-apps
---

# CrowdStrike Falcon for Mobile connector with Microsoft Intune

You can control mobile device access to corporate resources using Conditional Access based on risk assessment conducted by CrowdStrike Falcon for Mobile. CrowdStrike Falcon is a mobile threat defense solution that integrates with Microsoft Intune. Risk is assessed based on telemetry collected from devices running the CrowdStrike Falcon app.

You can configure Conditional Access policies based on CrowdStrike Falcon for Mobile risk assessment enabled through Intune device compliance policies. These policies can  allow or block noncompliant devices to access corporate resources based on detected threats.

## Prerequisites

- Microsoft Entra ID P1

- Microsoft Intune Plan 1 subscription

- CrowdStrike Falcon for Mobile subscription.  
  See the [CrowdStrike Falcon for Mobile](https://www.crowdstrike.com/products/endpoint-security/falcon-for-mobile/) website.

## Supported platforms

- **Android 9.0 and later**

- **iOS 15.0 and later**

## How do Intune and CrowdStrike Falcon for Mobile help protect your company resources?

CrowdStrike Falcon app for Android and iOS/iPadOS captures available telemetry for the file system, network stack, device, and applications. The captured telemetry data is then sent to the CrowdStrike Falcon for Mobile cloud service to assess the device's risk for mobile threats.

The Intune device compliance policy includes a rule for CrowdStrike Falcon for Mobile Threat Defense, which is based on the CrowdStrike Falcon for Mobile risk assessment. When this rule is enabled, Intune evaluates device compliance with the policy that you enabled. If the device is found noncompliant, users are blocked access to corporate resources like Exchange Online and SharePoint Online. Users also receive guidance from the CrowdStrike Falcon  app installed in their devices to resolve the issue and regain access to corporate resources.

Here are some common scenarios:

### Control access based on threats from malicious apps

When malicious apps such as malware are detected on devices, you can block devices until the threat is resolved:

- Connecting to corporate e-mail

- Syncing corporate files with the OneDrive for Work app

- Accessing company apps

*Block when malicious apps are detected:*

:::image type="content" source="./media/crowdstrike-falcon-defense-connector/crowdstrike-malicious-apps-blocked.png" alt-text="Product flow for blocking access due to malicious apps.":::

*Access granted on remediation:*

:::image type="content" source="./media/crowdstrike-falcon-defense-connector/crowdstrike-malicious-apps-unblocked.png" alt-text="Product flow for granting access when malicious apps are remediated.":::

### Control access based on threat to network

Detect threats like **Man-in-the-middle** in network, and protect access to Wi-Fi networks based on the device risk.

*Block network access through Wi-Fi:*

:::image type="content" source="./media/crowdstrike-falcon-defense-connector/crowdstrike-network-wifi-blocked.png" alt-text="Product flow for blocking access through Wi-Fi due to an alert.":::

*Access granted on remediation:*

:::image type="content" source="./media/crowdstrike-falcon-defense-connector/crowdstrike-network-wifi-unblocked.png" alt-text=" Product flow for granting access through Wi-Fi after the alert is remediated.":::

### Control access to SharePoint Online based on threat to network

Detect threats like **Man-in-the-middle** in network, and prevent synchronization of corporate files based on the device risk.

*Block SharePoint Online when network threats are detected:*

:::image type="content" source="./media/crowdstrike-falcon-defense-connector/crowdstrike-network-spo-blocked.png" alt-text="Product flow for blocking access to the organizations files due to an alert.":::

*Access granted on remediation:*

:::image type="content" source="./media/crowdstrike-falcon-defense-connector/crowdstrike-network-spo-unblocked.png" alt-text="Product flow for granting access to the organizations files after the alert is remediated.":::

## Related content

- [Integrate CrowdStrike Falcon for Mobile with Intune](crowdstrike-falcon-mtd-connector-integration.md)

- [Set up CrowdStrike Falcon app](mtd-apps-ios-app-configuration-policy-add-assign.md)

- [Create CrowdStrike Falcon for Mobile device compliance policy](mtd-device-compliance-policy-create.md)

- [Enable CrowdStrike Falcon for the Mobile Threat Defence connector](mtd-connector-enable.md)
