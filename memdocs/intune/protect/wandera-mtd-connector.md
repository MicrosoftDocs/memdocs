---
# required metadata

title: Set up Wandera Mobile Security with Intune
titleSuffix: Intune on Azure
description: How to set up the Wandera Mobile Security with Microsoft Intune to control mobile device access to your corporate resources.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/2/2020
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
- tier3
- M365-identity-device-management
---

# Wandera Mobile Threat Defense connector with Intune  

Control mobile device access to corporate resources using conditional access based on risk assessment conducted by Wandera. Wandera is a Mobile Threat Defense (MTD) solution that integrates with Microsoft Intune.  Risk is assessed based on telemetry collected from devices by the Wandera service, including:
- Operating system vulnerabilities
- Malicious apps installed
- Malicious network profiles
- Cryptojacking

You can configure *conditional access* policies that are based on Wandera's risk assessment, enabled through Intune device compliance policies. Risk assessment policy can allow or block noncompliant devices from accessing corporate resources based on detected threats.  

## How do Intune and Wandera Mobile Threat Defense help protect your company resources?  

Wandera's mobile app seamlessly installs using Microsoft Intune. This app captures file system, network stack, and device and application telemetry (where available). This information synchronizes to the Wandera cloud service to assess the device's risk for mobile threats. These risk level classifications are configurable to suit your needs in the Wandera console, RADAR.

The compliance policy in Intune includes a rule for MTD  based on Wandera's risk assessment. When this rule is enabled, Intune evaluates device compliance with the policy that you enabled.

For devices that are noncompliant, access to resources like Microsoft 365 can be blocked. Users on blocked devices receive guidance from the Wandera app to resolve the issue and regain access.

Wandera will update Intune with each device’s latest threat level (Secure, Low, Medium, or High) whenever it changes. This threat level is continuously re-calculated by the Wandera Security Cloud and is based upon device state, network activity, and numerous mobile threat intelligence feeds across various threat categories.

These categories and their associated threat levels are configurable in Wandera's RADAR console such that the total calculated threat level for each device is customizable per your organization’s security requirements. With threat level in hand, there are two Intune policy types that make use of this information to manage access to corporate data:

* Using **Device Compliance Policies** with Conditional Access, administrators set policies to automatically mark a managed device as “out of compliance” based upon the Wandera-reported threat level. This compliance flag subsequently drives Conditional Access Policies to allow or deny access to applications that utilize modern authentication.  See [Create Mobile Threat Defense (MTD) device compliance policy](../protect/mtd-device-compliance-policy-create.md) with Intune for configuration details.

* Using **App Protection Policies** with Conditional Launch, administrators can set policies that are enforced at the native app level (e.g. Android and iOS/iPad OS apps like Outlook, OneDrive, etc.) based upon the Wandera-reported threat level. These policies may also be used for unenrolled devices with MAM managed applications to provide uniform policy across all device platforms and ownership modes. See [Create Mobile Threat Defense app protection policy](../protect/mtd-app-protection-policy.md) with Intune for configuration details.

## Supported platforms  

The following platforms are supported for Wandera when enrolled in Intune:

- Android 9.0 and later  
- iOS 13.7 and later 

For more information about platform and device, see the [Wandera website](https://www.wandera.com/mobile-threat-defense/).

## Prerequisites  

- Microsoft Intune subscription  
- Azure Active Directory  
- Wandera Mobile Threat Defense (formerly Wandera Secure)  

For more information, see [Wandera Mobile Security](https://www.wandera.com/mobile-security/).
 
## Sample scenarios

Here are the common scenarios when using Wandera MTD with Intune.

### Control access based on threats from malicious apps  

When malicious apps such as malware are detected on devices, you can block devices from common tools until you can resolve the threat. Common blocks  include:  
- Connecting to corporate e-mail  
- Syncing corporate files with the OneDrive for Work app  
- Accessing company apps  

*Block when malicious apps are detected*:

:::image type="content" source="./media/wandera-mtd-connector/wandera-malicious-apps-blocked.png" alt-text="Product flow for blocking access due to malicious apps.":::

*Access granted on remediation*: 

:::image type="content" source="./media/wandera-mtd-connector/wandera-malicious-apps-unblocked.png" alt-text="Product flow for granting access when malicious apps are remediated.":::

### Control access based on threat to network  

Detect threats to your network such as man-in-the-middle attacks and protect access to Wi-Fi networks based on the device risk.  

*Block network access through Wi-Fi*:  

:::image type="content" source="./media/wandera-mtd-connector/wandera-network-wifi-blocked.png" alt-text="Product flow for blocking access through Wi-Fi due to an alert.":::

*Access granted on remediation*:  

:::image type="content" source="./media/wandera-mtd-connector/wandera-network-wifi-unblocked.png" alt-text=" Product flow for granting access through Wi-Fi after the alert is remediated.":::

## Control access to SharePoint Online based on threat to network

Detect threats to your network such as Man-in-the-middle attacks, and prevent synchronization of corporate files based on the device risk.

*Block SharePoint Online when network threats are detected*:  

:::image type="content" source="./media/wandera-mtd-connector/wandera-network-spo-blocked.png" alt-text="Product flow for blocking access to the organizations files due to an alert.":::

*Access granted on remediation*:  

:::image type="content" source="./media/wandera-mtd-connector/wandera-network-spo-unblocked.png" alt-text="Product flow for granting access to the organizations files after the alert is remediated.":::

### Control access on unenrolled devices based on threats from malicious apps

When the Wandera Mobile Threat Defense solution considers a device to be infected:

:::image type="content" source="./media/wandera-mtd-connector/wandera-mobile-app-policy-block.png" alt-text="Product flow for App protection policies to block access due to malware.":::


Access is granted on remediation:

:::image type="content" source="./media/wandera-mtd-connector/wandera-mobile-app-policy-remediated.png" alt-text=" Product flow for App protection policies to grant access after malware is remediated.":::

## Next steps

- [Integrate Wandera with Intune](wandera-mtd-connector-integration.md)
- [Set up Wandera apps](mtd-apps-ios-app-configuration-policy-add-assign.md)
- [Create Wandera device compliance policy](mtd-device-compliance-policy-create.md)
- [Enable Wandera MTD connector](mtd-connector-enable.md)
