---
# required metadata

title: Integrate Lookout Mobile Endpoint with Microsoft Intune
titleSuffix: Microsoft Intune
description: Learn about integrating Intune with Lookout Mobile Threat Defense (MTD) to control mobile device access to your corporate resources.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/17/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology:
ms.assetid: 3a730a5d-2a90-42b0-aa28-aadfc7a18788

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Lookout Mobile Endpoint Security connector with Intune

You can control mobile device access to corporate resources based on risk assessment conducted by Lookout, a Mobile Threat Defense solution integrated with Microsoft Intune. Risk is assessed based on telemetry collected from devices by the Lookout service including:
- Operating system vulnerabilities
- Malicious apps installed
- Malicious network profiles

You can configure Conditional Access policies based on Lookout's risk assessment enabled through Intune compliance policies for enrolled devices, which you can use to allow or block noncompliant devices to access corporate resources based on detected threats. For unenrolled devices, you can use app protection policies to enforce a block or selective wipe based on detected threats.

## How do Intune and Lookout Mobile Endpoint Security help protect company resources?

Lookout's mobile app, **Lookout for work**, is installed and run on mobile devices. This app captures file system, network stack, and device and application telemetry where available, then sends it to the Lookout cloud service to assess the device's risk for mobile threats. You can change risk level classifications for threats in the Lookout console to suit your requirements.

- **Support for enrolled devices** - Intune device compliance policy includes a rule for Mobile Threat Defense (MTD), which can use risk assessment information from Lookout for work. When the MTD rule is enabled, Intune evaluates device compliance with the policy that you enabled. If the device is found noncompliant, users are blocked access to corporate resources like Exchange Online and SharePoint Online. Users also receive guidance from the Lookout for work app installed in their devices to resolve the issue and regain access to corporate resources. To support using Lookout for work with enrolled devices:
  - [Add MTD apps to devices](../protect/mtd-apps-ios-app-configuration-policy-add-assign.md)
  - [Create a device compliance policy that supports MTD](../protect/mtd-device-compliance-policy-create.md)
  - [Enable the MTD connector in Intune](../protect/mtd-connector-enable.md)

- **Support for unenrolled devices** - Intune can use the risk assessment data from the Lookout for work app on unenrolled devices when you use Intune app protection policies. Admins can use this combination to help protect corporate data within a [Microsoft Intune protected app](../apps/apps-supported-intune-apps.md), Admins can also issue a block or selective wipe for corporate data on those unenrolled devices. To support using Lookout for work with unenrolled devices:
  - [Add the MTD app to unenrolled devices](../protect/mtd-add-apps-unenrolled-devices.md)
  - [Create a Mobile Threat Defense app protection policy](../protect/mtd-app-protection-policy.md)
  - [Enable the MTD connector in Intune for unenrolled devices](../protect/mtd-enable-unenrolled-devices.md)

## Supported platforms

The following platforms are supported for Lookout when enrolled in Intune:

- **Android 5.0 and later**  
- **iOS 12 and later**  

For additional information about platform and language support, visit the [Lookout website](https://personal.support.lookout.com/hc/articles/114094140253).  

## Prerequisites

- Lookout Mobile Endpoint Security enterprise subscription  
- Microsoft Intune subscription
- Azure Active Directory Premium
- Enterprise Mobility and Security (EMS) E3 or E5, with licenses assigned to users.  

For more information, see [Lookout Mobile Endpoint Security](https://www.lookout.com/products/mobile-endpoint-security)

## Sample scenarios

Here are the common scenarios when using Mobile Endpoint Security with Intune.

### Control access based on threats from malicious apps

When malicious apps such as malware are detected on devices, you can block devices from the following until the threat is resolved:

- Connecting to corporate e-mail
- Syncing corporate files with the OneDrive for Work app
- Accessing company apps

*Block when malicious apps are detected:*

:::image type="content" source="./media/lookout-mobile-threat-defense-connector/malicious-apps-blocked.png" alt-text="Product flow for blocking access due to malicious apps.":::

*Access granted on remediation:*

:::image type="content" source="./media/lookout-mobile-threat-defense-connector/malicious-apps-unblocked.png" alt-text="Product flow for granting access when malicious apps are remediated.":::

### Control access based on threat to network

Detect threats to your network such as man-in-the-middle attacks and protect access to WiFi networks based on the device risk.

*Block network access through WiFi:*

:::image type="content" source="./media/lookout-mobile-threat-defense-connector/network-wifi-blocked.png" alt-text="Product flow for blocking access through Wi-Fi due to an alert.":::

*Access granted on remediation:*

:::image type="content" source="./media/lookout-mobile-threat-defense-connector/network-wifi-unblocked.png" alt-text=" Product flow for granting access through Wi-Fi after the alert is remediated.":::

### Control access to SharePoint Online based on threat to network

Detect threats to your network such as Man-in-the-middle attacks, and prevent synchronization of corporate files based on the device risk.

*Block SharePoint Online when network threats are detected:*

:::image type="content" source="./media/lookout-mobile-threat-defense-connector/network-spo-blocked.png" alt-text="Product flow for blocking access to the organizations files due to an alert.":::

*Access granted on remediation:*

:::image type="content" source="./media/lookout-mobile-threat-defense-connector/network-spo-unblocked.png" alt-text="Product flow for granting access to the organizations files after the alert is remediated.":::

### Control access on unenrolled devices based on threats from malicious apps

When the Lookout Mobile Threat Defense solution considers a device to be infected:

:::image type="content" source="./media/lookout-mobile-threat-defense-connector/lookout-app-policy-block.png" alt-text="Product flow for App protection policies to block access due to malware.":::

Access is granted on remediation:

:::image type="content" source="./media/lookout-mobile-threat-defense-connector/lookout-app-policy-remediated.png" alt-text=" Product flow for App protection policies to grant access after malware is remediated.":::

## Next steps

Here are the main steps you must do to implement this solution:

- [Set up your Lookout integration](lookout-mtd-connector-integration.md)
- [Enable Mobile Endpoint Security in Intune](mtd-connector-enable.md)
- [Add and assign the Lookout for Work app](mtd-apps-ios-app-configuration-policy-add-assign.md)
- [Configure Lookout device compliance policy](mtd-device-compliance-policy-create.md)
- [Create an MTD app protection policy](mtd-app-protection-policy.md)
