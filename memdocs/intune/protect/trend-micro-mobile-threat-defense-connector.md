---
# required metadata

title: Trend Micro Mobile Security as a Service connector with Intune
titleSuffix: Intune on Azure
description: Set up the Trend Micro Mobile Threat Defense connector with Intune.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 09/20/2022
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
ms.collection:
- tier2
- M365-identity-device-management
---

# Use Trend Micro Mobile Security as a Service with Microsoft Intune

Control mobile device access to corporate resources using Conditional Access based on risk assessment conducted by Trend Micro Mobile Security as a Service, a mobile threat defense (MTD) solution that integrates with Microsoft Intune. Risk is assessed based on telemetry collected from devices protected by the Trend Micro Mobile Security as a Service, including:

- Malicious  apps installed
- Malicious network behavior and profiles
- Operating system vulnerabilities
- Device misconfiguration

You can configure Conditional Access policies based on Trend Micro Mobile Security as a Service’s risk assessment, enabled through Intune device compliance policies for enrolled devices. You can set up your policies to allow or block noncompliant devices from accessing corporate resources based on detected threats.

For more information about how to integrate Trend Micro with Microsoft Intune, see [Integration with Microsoft Endpoint Manager (Intune)](http://docs.trendmicro.com/en-us/enterprise/trend-micro-vision-one/mobile-security/getting-started-with_003/integration-with-int.aspx) in the [Trend Micro Mobile Security documentation](https://docs.trendmicro.com/en-us/enterprise/trend-micro-vision-one/mobile-security.aspx).

> [!NOTE]
> This Mobile Threat Defense vendor is not supported for unenrolled devices.

## Supported platforms

- **Android 7.0 and later**
- **iOS 11.0 and later**

## Prerequisites

- Azure Active Directory Premium
- Microsoft Intune subscription
- Trend Micro account with administrative access to the Trend Micro Vision One console

## How do Intune and the Trend Micro MTD connector help protect your company resources?

The Trend Micro Mobile Security as a Service mobile agent app for Android and iOS/iPadOS captures file system, network stack, device, and application telemetry where available, then sends the telemetry data to Trend Micro Mobile Security as a Service to assess the device's risk for mobile threats.

- **Support for enrolled devices** - Intune device compliance policy includes a rule for MTD, which can use risk assessment information from Trend Micro. When the MTD rule is enabled, Intune evaluates device compliance with the policy that you enabled. If the device is found noncompliant, users are blocked access to corporate resources, such as Exchange Online and SharePoint Online. Users also receive guidance from the Trend Micro Mobile Security as a Service mobile agent app installed on their devices to resolve the issue and regain access to corporate resources. To support using Trend Micro with enrolled devices:

  - [Add MTD apps to devices](../protect/mtd-apps-ios-app-configuration-policy-add-assign.md) (This is done automatically when  setting up Trend Micro Mobile Security as a Service integration)
  - [Create a device compliance policy that supports MTD](../protect/mtd-device-compliance-policy-create.md)
  - [Enable the MTD connector in Intune](../protect/mtd-connector-enable.md)

## Sample scenarios

The following scenarios demonstrate the use of Trend Micro MTD when integrated with Intune:

### Control access based on threats from malicious apps

When malicious apps such as malware are detected on devices, you can block devices until the threat is resolved:

- Connecting to corporate e-mail
- Syncing corporate files with the OneDrive for Work app
- Accessing company apps

*Block when malicious apps are detected:*

:::image type="content" source="./media/trend-micro-mobile-threat-defense-connector/trend-micro-malicious-apps-blocked.png" alt-text="Product flow for blocking access due to malicious apps.":::

*Access granted on remediation:*

:::image type="content" source="./media/trend-micro-mobile-threat-defense-connector/trend-micro-malicious-apps-unblocked.png" alt-text="Product flow for granting access when malicious apps are remediated.":::

### Control access based on threat to network

Detect threats like **Man-in-the-middle** in network, and protect access to Wi-Fi networks based on the device risk.

*Block network access through Wi-Fi:*

:::image type="content" source="./media/trend-micro-mobile-threat-defense-connector/trend-micro-network-wifi-blocked.png" alt-text="Product flow for blocking access through Wi-Fi due to an alert.":::

*Access granted on remediation:*

:::image type="content" source="./media/trend-micro-mobile-threat-defense-connector/trend-micro-network-wifi-unblocked.png" alt-text=" Product flow for granting access through Wi-Fi after the alert is remediated. ":::

### Control access to SharePoint Online based on threat to network

Detect threats like **Man-in-the-middle** in network and prevent synchronization of corporate files based on the device risk.

*Block SharePoint Online when network threats are detected:*

:::image type="content" source="./media/trend-micro-mobile-threat-defense-connector/trend-micro-network-spo-blocked.png" alt-text="Product flow for blocking access to the organizations files due to an alert.":::

*Access granted on remediation:*

:::image type="content" source="./media/trend-micro-mobile-threat-defense-connector/trend-micro-network-spo-unblocked.png" alt-text="Product flow for granting access to the organizations files after the alert is remediated.":::

## Next steps

- [Integrate Trend Micro Mobile Security as a Service with Intune](../protect/trend-micro-mtd-connector-integration.md)
- [Set up Trend Micro Mobile Security as a Service mobile agent app](../protect/mtd-apps-ios-app-configuration-policy-add-assign.md)
- [Create Trend Micro Mobile Security as a Service device compliance policy](../protect/mtd-device-compliance-policy-create.md)
- [Enable Trend Micro Mobile Security as a Service MTD connector](../protect/mtd-connector-enable.md)
