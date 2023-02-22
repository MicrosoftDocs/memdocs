---
# required metadata

title: BlackBerry Protect Mobile connector for Intune
titleSuffix: Intune on Azure
description: Learn about the Blackberry Protect Mobile MTD connector, which enables you to control mobile device access to your corporate resources.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 01/03/2022
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

# Use BlackBerry Protect Mobile with Intune

Control mobile device access to corporate resources using Conditional Access based on risk assessment conducted by BlackBerry Protect Mobile (powered by Cylance AI), a mobile threat defense (MTD) solution that integrates with Microsoft Intune. Risk is assessed based on telemetry collected from devices running the BlackBerry Protect Mobile app.

You can configure Conditional Access policies based on a BlackBerry Protect risk assessment, enabled through Intune device compliance policies for enrolled devices. You can set up your policies to allow or block noncompliant devices from accessing corporate resources based on detected threats.

For more information about how to integrate BlackBerry UES with Microsoft Intune, see the [BlackBerry UES documentation](https://docs.blackberry.com/en/unified-endpoint-security/blackberry-ues).  

> [!NOTE]
> This Mobile Threat Defense vendor is not supported for unenrolled devices.

## Supported platforms

- **Android 9.0 and later**

- **iOS 13.0 and later**

## Prerequisites

- Azure Active Directory Premium

- Microsoft Intune subscription

- BlackBerry UES account with access to UES management console 

## How do Intune and the BlackBerry MTD connector help protect your company resources?

The BlackBerry Protect Mobile app for Android and iOS/iPadOS captures file system, network stack, device, and application telemetry where available, then sends the telemetry data to the Cylance AI Protection cloud service to assess the device's risk for mobile threats.

- **Support for enrolled devices** - Intune device compliance policy includes a rule for MTD, which can use risk assessment information from BlackBerry Protect. When the MTD rule is enabled, Intune evaluates device compliance with the policy that you enabled. If the device is found noncompliant, users are blocked access to corporate resources, such as Exchange Online and SharePoint Online. Users also receive guidance from the BlackBerry Protect app installed on their devices to resolve the issue and regain access to corporate resources. To support using BlackBerry Protect with enrolled devices:
  - [Add MTD apps to devices](../protect/mtd-apps-ios-app-configuration-policy-add-assign.md)
  - [Create a device compliance policy that supports MTD](../protect/mtd-device-compliance-policy-create.md)
  - [Enable the MTD connector in Intune](../protect/mtd-connector-enable.md)
  
## Sample scenarios

The following scenarios demonstrate the use of BlackBerry Protect Mobile MTD when integrated with Intune:

### Control access based on threats from malicious apps

When malicious apps such as malware are detected on devices, you can block devices until the threat is resolved:

- Connecting to corporate e-mail

- Syncing corporate files with the OneDrive for Work app

- Accessing company apps

*Block when malicious apps are detected:*

:::image type="content" source="./media/blackberry-mobile-threat-defense-connector/blackberry-malicious-apps-blocked.png" alt-text="Product flow for blocking access due to malicious apps.":::

*Access granted on remediation:*

:::image type="content" source="./media/blackberry-mobile-threat-defense-connector/blackberry-malicious-apps-unblocked.png" alt-text="Product flow for granting access when malicious apps are remediated.":::

### Control access based on threat to network

Detect threats like **Man-in-the-middle** in network, and protect access to Wi-Fi networks based on the device risk.

*Block network access through Wi-Fi:*

:::image type="content" source="./media/blackberry-mobile-threat-defense-connector/blackberry-network-wifi-blocked.png" alt-text="Product flow for blocking access through Wi-Fi due to an alert.":::

*Access granted on remediation:*

:::image type="content" source="./media/blackberry-mobile-threat-defense-connector/blackberry-network-wifi-unblocked.png" alt-text=" Product flow for granting access through Wi-Fi after the alert is remediated. ":::

### Control access to SharePoint Online based on threat to network

Detect threats like **Man-in-the-middle** in network, and prevent synchronization of corporate files based on the device risk.

*Block SharePoint Online when network threats are detected:*

:::image type="content" source="./media/blackberry-mobile-threat-defense-connector/blackberry-network-spo-blocked.png" alt-text="Product flow for blocking access to the organizations files due to an alert.":::

*Access granted on remediation:*

:::image type="content" source="./media/blackberry-mobile-threat-defense-connector/blackberry-network-spo-unblocked.png" alt-text="Product flow for granting access to the organizations files after the alert is remediated.":::

## Next steps

- [Integrate BlackBerry Protect Mobile with Intune](blackberry-mtd-connector-integration.md)

- [Set up BlackBerry Protect Mobile app](mtd-apps-ios-app-configuration-policy-add-assign.md)

- [Create BlackBerry Protect Mobile device compliance policy](mtd-device-compliance-policy-create.md)

- [Enable BlackBerry Protect Mobile MTD connector](mtd-connector-enable.md)  
