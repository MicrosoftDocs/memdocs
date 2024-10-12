---
# required metadata

title: Pradeo Mobile Threat Defense connector and Microsoft Intune
titleSuffix: Intune on Azure
description: How to set up the Pradeo Mobile Threat Protection with Microsoft Intune to control mobile device access to your corporate resources.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 08/27/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.assetid: cde4d389-1770-4226-85a3-a2f3b3fb92a3

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: aanavath
#ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
#ms.custom:
ms.collection:
- tier3
- M365-identity-device-management
- sub-mtd-apps
---

# Pradeo Mobile Threat Defense connector with Intune

You can control mobile device access to corporate resources using Conditional Access based on risk assessment conducted by Pradeo, a Mobile Threat Defense (MTD) solution that integrates with Microsoft Intune. Risk is assessed based on telemetry collected from devices running the Pradeo app.

You can configure Conditional Access policies based on Pradeo risk assessment enabled through Intune device compliance policies, which you can use to allow or block noncompliant devices to access corporate resources based on detected threats.

> [!NOTE]
> This Mobile Threat Defense vendor is not supported for unenrolled devices.

## Supported platforms

- **Android 5.1 and later**
- **iOS 12.1 and later**

## Prerequisites

- Microsoft Entra ID P1
- Microsoft Intune Plan 1 subscription
- Pradeo Security for Mobile Threat Defense subscription
  - For more information, see the [Pradeo website](https://pradeo.com/en/solutions/mobile-device-security/mobile-threat-defense/).

## How do Intune and Pradeo help protect your company resources?

Pradeo app for Android and iOS/iPadOS captures file system, network stack, device, and application telemetry where available, and then sends the telemetry data to the Pradeo cloud service to assess the device's risk for mobile threats.

The Intune device compliance policy includes a rule for Pradeo Mobile Threat Defense, which is based on the Pradeo risk assessment. When this rule is enabled, Intune evaluates device compliance with the policy that you enabled. If the device is found noncompliant, users are blocked access to corporate resources like Exchange Online and SharePoint Online. Users also receive guidance from the Pradeo app installed in their devices to resolve the issue and regain access to corporate resources.

## Sample scenarios

Here are some common scenarios.

### Control access based on threats from malicious apps

When malicious apps such as malware are detected on devices, you can block devices from the following actions until the threat is resolved:

- Connecting to corporate e-mail
- Syncing corporate files with the OneDrive for Work app
- Accessing company apps

*Block when malicious apps are detected:*

:::image type="content" source="./media/pradeo-mobile-threat-defense-connector/pradeo-maliciousapps-blocked.png" alt-text="Product flow for blocking access due to malicious apps.":::

*Access granted on remediation:*

:::image type="content" source="./media/pradeo-mobile-threat-defense-connector/pradeo-maliciousapps-unblocked.png" alt-text="Product flow for granting access when malicious apps are remediated.":::

### Control access based on threat to network

Detect threats to your network like **Man-in-the-middle** attacks, and protect access to Wi-Fi networks based on the device risk.

*Block network access through Wi-Fi:*

:::image type="content" source="./media/pradeo-mobile-threat-defense-connector/pradeo-network-wifi-blocked.png" alt-text="Product flow for blocking access through Wi-Fi due to an alert.":::

*Access granted on remediation:*

:::image type="content" source="./media/pradeo-mobile-threat-defense-connector/pradeo-network-wifi-unblocked.png" alt-text=" Product flow for granting access through Wi-Fi after the alert is remediated.":::

### Control access to SharePoint Online based on threat to network

Detect threats to your network like **Man-in-the-middle** attacks, and prevent synchronization of corporate files based on the device risk.

*Block SharePoint Online when network threats are detected:*

:::image type="content" source="./media/pradeo-mobile-threat-defense-connector/pradeo-network-spo-blocked.png" alt-text="Product flow for blocking access to the organizations files due to an alert.":::

*Access granted on remediation:*

:::image type="content" source="./media/pradeo-mobile-threat-defense-connector/pradeo-network-spo-unblocked.png" alt-text="Product flow for granting access to the organizations files after the alert is remediated.":::

## Next steps

- [Integrate Pradeo with Intune](pradeo-mtd-connector-integration.md)

- [Set up Pradeo apps](mtd-apps-ios-app-configuration-policy-add-assign.md)

- [Create Pradeo device compliance policy](mtd-device-compliance-policy-create.md)

- [Enable Pradeo MTD connector](mtd-connector-enable.md)
