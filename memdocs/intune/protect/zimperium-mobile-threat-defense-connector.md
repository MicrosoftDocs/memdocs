---
# required metadata

title: Zimperium MTD connector with Intune
titleSuffix: Intune on Azure
description: Learn about integrating Intune with Zimperium Mobile Threat Defense to control mobile device access to your corporate resources.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 02/21/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology:
ms.assetid: 975d8d84-792a-41ad-925a-4a7f1ae4dcaf

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: heenamac
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Zimperium Mobile Threat Defense connector with Intune

You can control mobile device access to corporate resources using Conditional Access based on risk assessment conducted by Zimperium, a Mobile Threat Defense (MTD) solution that integrates with Microsoft Intune. Risk is assessed based on telemetry collected from devices running the Zimperium app.

You can configure Conditional Access policies based on Zimperium risk assessment enabled through Intune device compliance policies for enrolled devices, which you can use to allow or block noncompliant devices to access corporate resources based on detected threats. For unenrolled devices, you can use app protection policies to enforce a block or selective wipe based on detected threats.

## How do Intune and Zimperium help protect your company resources?

Zimperium app for Android and iOS/iPadOS captures file system, network stack, device, and application telemetry where available, then sends the telemetry data to the Zimperium cloud service to assess the device's risk for mobile threats.

The Intune device compliance policy includes a rule for Zimperium Mobile Threat Defense, which is based on the Zimperium risk assessment. When this rule is enabled, Intune evaluates device compliance with the policy that you enabled. If the device is found noncompliant, users are blocked access to corporate resources like Exchange Online and SharePoint Online. Users also receive guidance from the Zimperium app installed in their devices to resolve the issue and regain access to corporate resources.

## Sample scenarios

See below a few scenarios when integrating Zimperium with Intune:

### Control access based on threats from malicious apps

When malicious apps such as malware are detected on devices, you can block devices until the threat is resolved:

- Connecting to corporate e-mail

- Syncing corporate files with the OneDrive for Work app

- Accessing company apps

**Block when malicious apps are detected:**

![Conceptual image of Malicious apps detected](./media/zimperium-mobile-threat-defense-connector/Maliciousapps_blocked_Zimperium.png)

**Access granted on remediation:**

![Conceptual image of access granted after remediation](./media/zimperium-mobile-threat-defense-connector/maliciousapps_unblocked_Zimperium.png)

### Control access based on threat to network

Detect threats like **Man-in-the-middle** in network, and protect access to Wi-Fi networks based on the device risk.

**Block network access through Wi-Fi:**

![Block network access through Wi-Fi](./media/zimperium-mobile-threat-defense-connector/network_wifi_blocked_Zimperium.png)

**Access granted on remediation:**

![Access granted on remediation](./media/zimperium-mobile-threat-defense-connector/network_wifi_unblocked_Zimperium.png)

### Control access to SharePoint Online based on threat to network

Detect threats like **Man-in-the-middle** in network, and prevent synchronization of corporate files based on the device risk.

**Block SharePoint Online when network threats are detected:**

![Block SharePoint Online when network threats are detected](./media/zimperium-mobile-threat-defense-connector/network_spo_blocked_Zimperium.png)

**Access granted on remediation:**

![Access granted on remediation for Sharepoint example](./media/zimperium-mobile-threat-defense-connector/network_spo_unblocked_Zimperium.png)

## Supported platforms

- **Android 4.1 and later**

- **iOS 8 and later**

## Prerequisites

- Azure Active Directory Premium

- Microsoft Intune subscription

- Zimperium Mobile Threat Defense subscription

  - For more information, see [Zimperium website](https://www.zimperium.com/zips-mobile-ips).

## Next steps

- [Integrate Zimperium with Intune](zimperium-mtd-connector-integration.md)

- [Set up Zimperium apps](mtd-apps-ios-app-configuration-policy-add-assign.md)

- [Create Zimperium device compliance policy](mtd-device-compliance-policy-create.md)

- [Enable Zimperium MTD connector](mtd-connector-enable.md)

- [Create an MTD app protection policy](../protect/mtd-app-protection-policy.md)
