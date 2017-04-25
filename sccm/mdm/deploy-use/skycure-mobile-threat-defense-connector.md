---
title: "Skycure Mobile Threat Defense connector | Microsoft Docs"
description: "Understand how Skycure Mobile Threat Defense connector works with Intune"
ms.custom: na
ms.date: 04/25/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c40079d1-1f0e-4637-828a-1d852b28a5cd
caps.latest.revision:
author: andredm7
ms.author: andredm
manager: angrobe

---

# Skycure Mobile Threat Defense connector

*Applies to: System Center Configuration Manager (Current Branch)*

You can control mobile device access to corporate resources using conditional access based on risk assessment conducted by Skycure, a mobile threat defense solution that integrates with Microsoft Intune. Risk is assessed based on telemetry collected from devices running Skycure, including:

-   Physical defense

-   Network defense

-   Application defense

-   Vulnerabilities defense

You can configure conditional access policies based on Skycure risk assessment enabled through Intune device compliance policies, which you can use to allow or block non-compliant devices to access corporate resources based on detected threats.

## How do Intune and Skycure help protect your company resources?

Skycure mobile app for Android or iOS captures file system, network stack, device and application telemetry where available, then sends it to the Skycure cloud service to assess the device's risk for mobile threats.

The Intune device compliance policy includes a rule for Skycure mobile threat defense, which is based on the Skycure risk assessment. When this rule is enabled, Intune evaluates device compliance with the policy that you enabled.

If the device is found non-compliant, access to resources like Exchange Online and SharePoint Online are blocked. Users on blocked devices receive guidance from the Skycure mobile app to resolve the issue and regain access to corporate resources.

Intune supports two modes of integration with Skycure:

-   **Basic setup** which is a read only mode that allows Skycure visibility for devices in Intune.

-   **Full integration** which allows Skycure to report device risk and security incident details to Intune.

## Sample scenarios

Here are some common scenarios:

### Control access based on threats from malicious apps

When malicious apps such as malware are detected on devices, you can block devices until the threat is resolved:

-   Connecting to corporate e-mail

-   Syncing corporate files with the OneDrive for Work app

-   Accessing company apps

**Block when malicious apps are detected:**

![Malicious apps detected](../media/mtp/skycure-arch-1.png)

**Access granted on remediation:**

![Malicious apps detected access granted](../media/mtp/skycure-arch-2.png)

### Control access based on threat to network

Detect threats like **Man-in-the-middle** in network, and protect access to Wi-Fi networks based on the device risk.

**Block network access through Wi-Fi:**

![Block network access through Wi-Fi](../media/mtp/skycure-arch-3.png)

**Access granted on remediation:**

![Access granted on remediation](../media/mtp/skycure-arch-4.png)

### Control access to SharePoint Online based on threat to network

Detect threats like **Man-in-the-middle** in network, and prevent synchronization of corporate files based on the device risk.

**Block SharePoint Online when network threats are detected:**

![Block SharePoint Online when network threats are detected](../media/mtp/skycure-arch-5.png)

**Access granted on remediation:**

![Access granted on remediation for Sharepoint example](../media/mtp/skycure-arch-6.png)

## Supported platforms

-   **Android 4.1 and later**

-   **iOS 8 and later**

## Pre-requisites

-   Azure Active Directory Premium

-   Microsoft Intune subscription

-   Skycure Mobile Threat Defense subscription

For more information, check [Skycure website](https://www.skycure.com/skycure-microsoft-integration/).

## Next steps

Here are the steps you need to complete to integrate Intune with Skycure:

1.  [Configure Skycure to use Azure Active Directory Single Sign On (SSO)](https://docs.microsoft.com/sccm/mdm/deploy-use/configure-skycure-to-use-azure-active-directory-single-sign-on)

2.  [Download Skycure iOS app configuration policy](https://docs.microsoft.com/sccm/mdm/deploy-use/download-skycure-ios-app-configuration-policy)

3.  [Add Skycure apps, Microsoft Authenticator and iOS app configuration policy](https://docs.microsoft.com/sccm/mdm/deploy-use/add-skycure-apps-microsoft-authenticator-and-ios-app-configuration-policy)

4.  [Deploy Skycure apps, Microsoft Authenticator and iOS app configuration policy](https://docs.microsoft.com/intune/deploy-use/sccm/mdm/deploy-skycure-apps-microsoft-authenticator-app-and-ios-app-configuration-policy)

5.  [Setup Skycure integration with Intune](https://docs.microsoft.com/sccm/mdm/deploy-use/setup-the-skycure-integration-with-Intune)

6.  [Enable Skycure Mobile Threat Defense in Intune](https://docs.microsoft.com/sccm/mdm/deploy-use/enable-skycure-mobile-threat-defense-in-intune)

7.  [Create Skycure Mobile Threat Defense compliance policy in Intune](https://docs.microsoft.com/sccm/mdm/deploy-use/create-skycure-mobile-threat-defense-compliance-policy)
