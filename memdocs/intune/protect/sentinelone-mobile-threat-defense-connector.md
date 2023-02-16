---
# required metadata

title: SentinelOne MTD connector with Intune
titleSuffix: Intune on Azure
description: Learn about integrating Intune with SentinelOne Mobile Threat Defense to control mobile device access to your corporate resources.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 01/20/2023
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
ms.suite: ems
search.appverid: MET150
#ms.tgt-pltfrm:
ms.custom: intune-azure
ms.collection:
- tier3
- M365-identity-device-management
---

# SentinelOne Mobile Threat Defense connector with Intune

You can control mobile device access to corporate resources using Conditional Access based on risk assessment conducted by SentinelOne, a Mobile Threat Defense (MTD) solution that integrates with Microsoft Intune. Risk is assessed based on telemetry collected from devices running the SentinelOne app.

You can configure Conditional Access policies based on SentinelOne risk assessment enabled through Intune device compliance policies for enrolled devices, which you can use to allow or block noncompliant devices to access corporate resources based on detected threats. For unenrolled devices, you can use app protection policies to enforce a block or selective wipe based on detected threats.

## Supported platforms

- **Android 5.0 and later**

- **iOS 10.0 and later**

## Prerequisites

- Azure Active Directory Premium

- Microsoft Intune subscription

- SentinelOne Mobile Threat Defense subscription

  - For more information, see [SentinelOne website](https://www.sentinelone.com/).

## How do Intune and SentinelOne help protect your company resources?

The SentinelOne app for Android and iOS/iPadOS captures file system, network stack, device, and application telemetry where available, then sends the telemetry data to the SentinelOne cloud service to assess the device's risk for mobile threats.

- **Support for enrolled devices** - Intune device compliance policy includes a rule for Mobile Threat Defense (MTD), which can use risk assessment information from SentinelOne. When the MTD rule is enabled, Intune evaluates device compliance with the policy that you enabled. If the device is found noncompliant, users are blocked access to corporate resources like Exchange Online and SharePoint Online. Users also receive guidance from the SentinelOne app installed in their devices to resolve the issue and regain access to corporate resources. To support using SentinelOne with enrolled devices:  
  - [Add MTD apps to devices](../protect/mtd-apps-ios-app-configuration-policy-add-assign.md)
  - [Create a device compliance policy that supports MTD](../protect/mtd-device-compliance-policy-create.md)
  - [Enable the MTD connector in Intune](../protect/mtd-connector-enable.md)

- **Support for unenrolled devices** - Intune can use the risk assessment data from the SentinelOne app on unenrolled devices when you use Intune app protection policies. Admins can use this combination to help protect corporate data within a [Microsoft Intune protected app](../apps/apps-supported-intune-apps.md), Admins can also issue a block or selective wipe for corporate data on those unenrolled devices. To support using SentinelOne with unenrolled devices:  
  - [Add the MTD app to unenrolled devices](../protect/mtd-add-apps-unenrolled-devices.md)
  - [Create a Mobile Threat Defense app protection policy](../protect/mtd-app-protection-policy.md)
  - [Enable the MTD connector in Intune for unenrolled devices](../protect/mtd-enable-unenrolled-devices.md)
  
## Sample scenarios

See below a few scenarios when integrating SentinelOne with Intune:

### Control access based on threats from malicious apps

When malicious apps such as malware are detected on devices, you can block devices until the threat is resolved:

- Connecting to corporate e-mail

- Syncing corporate files with the OneDrive for Work app

- Accessing company apps

*Block when malicious apps are detected:*

:::image type="content" source="./media/sentinelone-mtd-connector/malicious-apps-blocked-sentinelone.png" alt-text="Product flow for blocking access due to malicious apps.":::

*Access granted on remediation:*

:::image type="content" source="./media/sentinelone-mtd-connector/malicious-apps-blocked-sentinelone.png" alt-text="Product flow for granting access when malicious apps are remediated.":::

### Control access based on threat to network

Detect threats like **Man-in-the-middle** in network, and protect access to Wi-Fi networks based on the device risk.

*Block network access through Wi-Fi:*

:::image type="content" source="./media/sentinelone-mtd-connector/network-wifi-blocked-sentinelone.png" alt-text="Product flow for blocking access through Wi-Fi due to an alert.":::

*Access granted on remediation:*

:::image type="content" source="./media/sentinelone-mtd-connector/network-wifi-unblocked-sentinelone.png" alt-text=" Product flow for granting access through Wi-Fi after the alert is remediated.":::

### Control access to SharePoint Online based on threat to network

Detect threats like **Man-in-the-middle** in network, and prevent synchronization of corporate files based on the device risk.

*Block SharePoint Online when network threats are detected:*

:::image type="content" source="./media/sentinelone-mtd-connector/network-spo-blocked-sentinelone.png" alt-text="Product flow for blocking access to the organizations files due to an alert.":::

*Access granted on remediation:*

:::image type="content" source="./media/sentinelone-mtd-connector/network-spo-unblocked-sentinelone.png" alt-text="Product flow for granting access to the organizations files after the alert is remediated.":::

### Control access on unenrolled devices based on threats from malicious apps

When the sentinelone Mobile Threat Defense solution considers a device to be infected:

:::image type="content" source="./media/sentinelone-mtd-connector/mobile-app-policy-block-sentinelone.png" alt-text="Product flow for App protection policies to block access due to malware.":::

*Access is granted on remediation*:

:::image type="content" source="./media/sentinelone-mtd-connector/mobile-app-policy-remediated-sentinelone.png" alt-text="Product flow for App protection policies to grant access after malware is remediated.":::

## Next steps

- [Integrate sentinelone with Intune](sentinelone-mtd-connector-integration.md)

- [Set up sentinelone apps](mtd-apps-ios-app-configuration-policy-add-assign.md)

- [Create sentinelone device compliance policy](mtd-device-compliance-policy-create.md)

- [Enable sentinelone MTD connector](mtd-connector-enable.md)

- [Create an MTD app protection policy](../protect/mtd-app-protection-policy.md)
