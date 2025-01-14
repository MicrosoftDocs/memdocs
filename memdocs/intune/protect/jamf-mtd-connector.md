---
# required metadata

title: Set up Jamf Mobile Security with Intune
titleSuffix: Intune on Azure
description: How to set up Jamf Mobile Threat Defense with Microsoft Intune to control mobile device access to your corporate resources.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 02/28/2024
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
#ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
#ms.custom:
ms.collection:
- tier3
- M365-identity-device-management
- sub-mtd-apps
---

# Jamf Mobile Threat Defense connector with Intune

Control mobile device access to corporate resources using Conditional Access based on risk assessment conducted by Jamf. Jamf is a Mobile Threat Defense (MTD) solution that integrates with Microsoft Intune. Risk is assessed based on telemetry collected from devices by the Jamf service, including:

- Operating system vulnerabilities
- Malicious apps installed
- Malicious network profiles
- Cryptojacking

You can configure *Conditional Access* policies that are based on Jamf's risk assessment, enabled through Intune device compliance policies. Risk assessment policy can allow or block noncompliant devices from accessing corporate resources based on detected threats.

## How do Intune and Jamf Mobile Threat Defense help protect your company resources?

Jamf's mobile app seamlessly installs using Microsoft Intune. This app captures file system, network stack, and device and application telemetry (where available). This information synchronizes to the Jamf cloud service to assess the device's risk for mobile threats. These risk level classifications are configurable to suit your needs in the Jamf administrator console.

The compliance policy in Intune includes a rule for MTD based on Jamf's risk assessment. When this rule is enabled, Intune evaluates device compliance with the policy that you enabled.

For devices that are noncompliant, access to resources like Microsoft 365 can be blocked. Users on blocked devices receive guidance from the Jamf app to resolve the issue and regain access.

Jamf updates Intune with each device’s latest threat level (Secure, Low, Medium, or High) whenever it changes. This threat level is continuously recalculated by the Jamf Security Cloud and is based upon device state, network activity, and numerous mobile threat intelligence feeds across various threat categories.

These categories and their associated threat levels are configurable in Jamf Security Cloud portal such that the total calculated threat level for each device is customizable per your organization’s security requirements. With threat level in hand, there are two Intune policy types that make use of this information to manage access to corporate data:

- Using **Device Compliance Policies** with Conditional Access, administrators set policies to automatically mark a managed device as “out of compliance” based upon the Jamf-reported threat level. This compliance flag subsequently drives Conditional Access Policies to allow or deny access to applications that utilize modern authentication. See [Create Mobile Threat Defense (MTD) device compliance policy](../protect/mtd-device-compliance-policy-create.md) with Intune for configuration details.

- Using **App Protection Policies** with Conditional Launch, administrators can set policies that are enforced at the native app level (for example, Android and iOS/iPad OS apps like Outlook, OneDrive, etc.) based upon the Jamf-reported threat level. These policies can also be used for unenrolled devices with MAM managed applications to provide uniform policy across all device platforms and ownership modes. See [Create Mobile Threat Defense app protection policy](../protect/mtd-app-protection-policy.md) with Intune for configuration details.

## Supported platforms

The following platforms are supported for Jamf when enrolled in Intune:

- Android 11 and later
- iOS / iPadOS 15.6 and later (iOS App Bundle ID: com.jamf.trust)

For more information about platform and device, see the [Jamf website](https://www.jamf.com/products/jamf-protect/).

## Prerequisites

- Microsoft Intune Plan 1 subscription
- Microsoft Entra ID
- Jamf Mobile Threat Defense

For more information, see [Jamf Mobile Security](https://www.jamf.com/solutions/threat-prevention-remediation/).

## Sample scenarios

Here are the common scenarios when using Jamf MTD with Intune.

### Control access based on threats from malicious apps

When malicious apps such as malware are detected on devices, you can block devices from common tools until you can resolve the threat. Common blocks include:

- Connecting to corporate e-mail
- Syncing corporate files with the OneDrive for Work app
- Accessing company apps

*Block when malicious apps are detected*:

:::image type="content" source="./media/jamf-mtd-connector/jamf-malicious-apps-blocked.png" alt-text="Product flow for blocking access due to malicious apps.":::

*Access granted on remediation*: 

:::image type="content" source="./media/jamf-mtd-connector/jamf-malicious-apps-unblocked.png" alt-text="Product flow for granting access when malicious apps are remediated.":::

### Control access based on threat to network

Detect threats to your network such as man-in-the-middle attacks and protect access to Wi-Fi networks based on the device risk.

*Block network access through Wi-Fi*:

:::image type="content" source="./media/jamf-mtd-connector/jamf-network-wifi-blocked.png" alt-text="Product flow for blocking access through Wi-Fi due to an alert.":::

*Access granted on remediation*:

:::image type="content" source="./media/jamf-mtd-connector/jamf-network-wifi-unblocked.png" alt-text=" Product flow for granting access through Wi-Fi after the alert is remediated.":::

## Control access to SharePoint Online based on threat to network

Detect threats to your network such as Man-in-the-middle attacks, and prevent synchronization of corporate files based on the device risk.

*Block SharePoint Online when network threats are detected*:

:::image type="content" source="./media/jamf-mtd-connector/jamf-network-spo-blocked.png" alt-text="Product flow for blocking access to the organizations files due to an alert.":::

*Access granted on remediation*:

:::image type="content" source="./media/jamf-mtd-connector/jamf-network-spo-unblocked.png" alt-text="Product flow for granting access to the organizations files after the alert is remediated.":::

### Control access on unenrolled devices based on threats from malicious apps

When the Jamf Mobile Threat Defense solution considers a device to be infected:

:::image type="content" source="./media/jamf-mtd-connector/jamf-mobile-app-policy-block.png" alt-text="Product flow for App protection policies to block access due to malware.":::

*Access is granted on remediation*:

:::image type="content" source="./media/jamf-mtd-connector/jamf-mobile-app-policy-remediated.png" alt-text=" Product flow for App protection policies to grant access after malware is remediated.":::

## Next steps

- [Integrate Jamf with Intune](jamf-mtd-connector-integration.md)
- [Set up Jamf apps](mtd-apps-ios-app-configuration-policy-add-assign.md)
- [Create Jamf device compliance policy](mtd-device-compliance-policy-create.md)
- [Enable Jamf MTD connector](mtd-connector-enable.md)
