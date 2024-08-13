---
# required metadata

title: Zimperium MTD connector with Microsoft Intune
titleSuffix: Intune on Azure
description: How to set up Zimperium Mobile Threat Defense with Microsoft Intune to control mobile device access to your corporate resources
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 11/17/2023
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.assetid: 975d8d84-792a-41ad-925a-4a7f1ae4dcaf

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
#ms.tgt-pltfrm:
ms.custom: intune-azure
ms.collection:
- tier3
- M365-identity-device-management
- sub-mtd-apps
---

# Zimperium Mobile Threat Defense connector with Intune

You can control mobile device access to corporate resources using Conditional Access based on risk assessment conducted by Zimperium, a Mobile Threat Defense (MTD) solution that integrates with Microsoft Intune. Risk is assessed based on telemetry collected from devices running the Zimperium app.

You can configure Conditional Access policies based on Zimperium risk assessment enabled through Intune device compliance policies for enrolled devices, which you can use to allow or block noncompliant devices to access corporate resources based on detected threats. For unenrolled devices, you can use app protection policies to enforce a block or selective wipe based on detected threats.

## Supported platforms

- **Android 5.1 and later**

- **iOS 10 and later**

## Prerequisites

- Microsoft Entra ID P1
- Microsoft Intune Plan 1 subscription
- Zimperium Mobile Threat Defense subscription
  - For more information, see [Zimperium website](https://www.zimperium.com/zips-mobile-ips)

## How do Intune and Zimperium help protect your company resources?

The Zimperium app for Android and iOS/iPadOS captures file system, network stack, device, and application telemetry where available, then sends the telemetry data to the Zimperium cloud service to assess the device's risk for mobile threats.

- **Support for enrolled devices** - Intune device compliance policy includes a rule for Mobile Threat Defense (MTD), which can use risk assessment information from Zimperium. When the MTD rule is enabled, Intune evaluates device compliance with the policy that you enabled. If the device is found noncompliant, users are blocked access to corporate resources like Exchange Online and SharePoint Online. Users also receive guidance from the Zimperium app installed in their devices to resolve the issue and regain access to corporate resources. To support using Zimperium with enrolled devices:
  - [Add MTD apps to devices](../protect/mtd-apps-ios-app-configuration-policy-add-assign.md)
  - [Create a device compliance policy that supports MTD](../protect/mtd-device-compliance-policy-create.md)
  - [Enable the MTD connector in Intune](../protect/mtd-connector-enable.md)

- **Support for unenrolled devices** - Intune can use the risk assessment data from the Zimperium app on unenrolled devices when you use Intune app protection policies. Admins can use this combination to help protect corporate data within a [Microsoft Intune protected app](../apps/apps-supported-intune-apps.md), Admins can also issue a block or selective wipe for corporate data on those unenrolled devices. To support using Zimperium with unenrolled devices:
  - [Add the MTD app to unenrolled devices](../protect/mtd-add-apps-unenrolled-devices.md)
  - [Create a Mobile Threat Defense app protection policy](../protect/mtd-app-protection-policy.md)
  - [Enable the MTD connector in Intune for unenrolled devices](../protect/mtd-enable-unenrolled-devices.md)
  
## Sample scenarios

See below a few scenarios when integrating Zimperium with Intune:

### Control access based on threats from malicious apps

When malicious apps such as malware are detected on devices, you can block devices until the threat is resolved:

- Connecting to corporate e-mail
- Syncing corporate files with the OneDrive for Work app
- Accessing company apps

*Block when malicious apps are detected:*

:::image type="content" source="./media/zimperium-mobile-threat-defense-connector/maliciousapps-blocked-zimperium.png" alt-text="Product flow for blocking access due to malicious apps.":::

*Access granted on remediation:*

:::image type="content" source="./media/zimperium-mobile-threat-defense-connector/maliciousapps-unblocked-zimperium.png" alt-text="Product flow for granting access when malicious apps are remediated.":::

### Control access based on threat to network

Detect threats like **Man-in-the-middle** in network, and protect access to Wi-Fi networks based on the device risk.

*Block network access through Wi-Fi:*

:::image type="content" source="./media/zimperium-mobile-threat-defense-connector/network-wifi-blocked-zimperium.png" alt-text="Product flow for blocking access through Wi-Fi due to an alert.":::

*Access granted on remediation:*

:::image type="content" source="./media/zimperium-mobile-threat-defense-connector/network-wifi-unblocked-zimperium.png" alt-text=" Product flow for granting access through Wi-Fi after the alert is remediated.":::

### Control access to SharePoint Online based on threat to network

Detect threats like **Man-in-the-middle** in network, and prevent synchronization of corporate files based on the device risk.

*Block SharePoint Online when network threats are detected:*

:::image type="content" source="./media/zimperium-mobile-threat-defense-connector/network-spo-blocked-zimperium.png" alt-text="Product flow for blocking access to the organizations files due to an alert.":::

*Access granted on remediation:*

:::image type="content" source="./media/zimperium-mobile-threat-defense-connector/network-spo-unblocked-zimperium.png" alt-text="Product flow for granting access to the organizations files after the alert is remediated.":::

### Control access on unenrolled devices based on threats from malicious apps

When the Zimperium Mobile Threat Defense solution considers a device to be infected:

:::image type="content" source="./media/zimperium-mobile-threat-defense-connector/zimperium-mobile-app-policy-block.png" alt-text="Product flow for App protection policies to block access due to malware.":::

Access is granted on remediation:

:::image type="content" source="./media/zimperium-mobile-threat-defense-connector/zimperium-mobile-app-policy-remediated.png" alt-text="Product flow for App protection policies to grant access after malware is remediated.":::

## Next steps

- [Integrate Zimperium with Intune](zimperium-mtd-connector-integration.md)

- [Set up Zimperium apps](mtd-apps-ios-app-configuration-policy-add-assign.md)

- [Create Zimperium device compliance policy](mtd-device-compliance-policy-create.md)

- [Enable Zimperium MTD connector](mtd-connector-enable.md)

- [Create an MTD app protection policy](../protect/mtd-app-protection-policy.md)
