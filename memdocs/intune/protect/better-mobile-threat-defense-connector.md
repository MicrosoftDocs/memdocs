---
# required metadata

title: Better Mobile Threat Defense connector with Intune
titleSuffix: Intune on Azure
description: Set up Better Mobile Threat Defense connector with Intune.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/09/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: aanavath
#ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
#ms.custom:
ms.collection: M365-identity-device-management
---

# Better Mobile Threat Defense connector with Intune

You can control mobile device access to corporate resources using Conditional Access based on risk assessment conducted by Better Mobile, a Mobile Threat Defense (MTD) solution that integrates with Microsoft Intune. Risk is assessed based on telemetry collected from devices running the Better Mobile app.

You can configure Conditional Access policies based on Better Mobile risk assessment enabled through Intune device compliance policies for enrolled devices, which you can use to allow or block noncompliant devices to access corporate resources based on detected threats. For unenrolled devices, you can use app protection policies to enforce a block or selective wipe based on detected threats.

## How do Intune and Better Mobile help protect your company resources?

The Better Mobile app is installed and run on mobile devices. This app captures file system, network stack, device, and application telemetry where available, and then sends the data to the Better Mobile cloud service to assess the device's risk for mobile threats.

- **Support for enrolled devices** - Intune device compliance policy includes a rule for Mobile Threat Defense (MTD), which can use risk assessment information from Better Mobile. When the MTD rule is enabled, Intune evaluates device compliance with the policy that you enabled. If the device is found noncompliant, users are blocked access to corporate resources like Exchange Online and SharePoint Online. Users also receive guidance from the Better Mobile app installed in their devices to resolve the issue and regain access to corporate resources. To support using Better Mobile with enrolled devices:
  - [Add MTD apps to devices](../protect/mtd-apps-ios-app-configuration-policy-add-assign.md)
  - [Create a device compliance policy that supports MTD](../protect/mtd-device-compliance-policy-create.md)
  - [Enable the MTD connector in Intune](../protect/mtd-connector-enable.md)

- **Support for unenrolled devices** - Intune can use the risk assessment data from the Better Mobile app on unenrolled devices when you use Intune app protection policies. Admins can use this combination to help protect corporate data within a [Microsoft Intune protected app](../apps/apps-supported-intune-apps.md), Admins can also issue a block or selective wipe for corporate data on those unenrolled devices. To support using Better Mobile with unenrolled devices:
  - [Add the MTD app to unenrolled devices](../protect/mtd-add-apps-unenrolled-devices.md)
  - [Create a Mobile Threat Defense app protection policy](../protect/mtd-app-protection-policy.md)
  - [Enable the MTD connector in Intune for unenrolled devices](../protect/mtd-enable-unenrolled-devices.md)

## Supported platforms

- **Android 4.1 and later**

- **iOS 8.0 and later**

## Prerequisites

- Azure Active Directory Premium

- Microsoft Intune subscription

- Better Mobile Threat Defense subscription

  - For more information, see the [Better Mobile website](https://www.better.mobi/).

## Sample scenarios

Here are some common scenarios.

### Control access based on threats from malicious apps

When malicious apps such as malware are detected on devices, you can block devices from the following actions until the threat is resolved:

- Connecting to corporate e-mail

- Syncing corporate files with the OneDrive for Work app

- Accessing company apps

Block when malicious apps are detected:

:::image type="content" source="./media/better-mobile-threat-defense-connector/better-mobile-maliciousapps-blocked.png" alt-text="Product flow for blocking access due to malicious apps.":::

Access is granted on remediation:

:::image type="content" source="./media/better-mobile-threat-defense-connector/better-mobile-maliciousapps-unblocked.png" alt-text="Product flow for granting access when malicious apps are remediated.":::

### Control access based on threat to network

Detect threats to your network like **Man-in-the-middle** attacks, and protect access to Wi-Fi networks based on the device risk.

Block network access through Wi-Fi:

:::image type="content" source="./media/better-mobile-threat-defense-connector/better-mobile-network-wifi-blocked.png" alt-text="Product flow for blocking access through Wi-Fi due to an alert.":::

Access is granted on remediation:

:::image type="content" source="./media/better-mobile-threat-defense-connector/better-mobile-network-wifi-unblocked.png" alt-text=" Product flow for granting access through Wi-Fi after the alert is remediated.":::

### Control access to SharePoint Online based on threat to network

Detect threats to your network like **Man-in-the-middle** attacks, and prevent synchronization of corporate files based on the device risk.

Block SharePoint Online when network threats are detected:

:::image type="content" source="./media/better-mobile-threat-defense-connector/better-mobile-network-spo-blocked.png" alt-text="Product flow for blocking access to the organizations files due to an alert.":::

Access granted on remediation:

:::image type="content" source="./media/better-mobile-threat-defense-connector/better-mobile-network-spo-unblocked.png" alt-text="Product flow for granting access to the organizations files after the alert is remediated.":::

### Control  access on unenrolled devices based on threats from malicious apps

When the BETTER Mobile Threat Defense solution considers a device to be infected:

:::image type="content" source="./media/better-mobile-threat-defense-connector/better-mobile-app-policy-block.png" alt-text="Product flow for App protection policies to block access due to malware.":::

Access is granted on remediation:

:::image type="content" source="./media/better-mobile-threat-defense-connector/better-mobile-app-policy-remediated.png" alt-text=" Product flow for App protection policies to grant access after malware is remediated.":::

## Next steps

- [Integrate Better Mobile with Intune](better-mobile-mtd-connector-integration.md)

- [Set up Better Mobile apps](mtd-apps-ios-app-configuration-policy-add-assign.md)

- [Create Better Mobile device compliance policy](mtd-device-compliance-policy-create.md)

- [Enable Better Mobile MTD connector](mtd-connector-enable.md)

- [Create an MTD app protection policy](mtd-app-protection-policy.md) 
