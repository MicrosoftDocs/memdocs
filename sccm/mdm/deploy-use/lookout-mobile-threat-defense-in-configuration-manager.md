---
title: Restrict access based on risk
titleSuffix: Configuration Manager
description: Restrict access to company resources based on device, network and application risk.
ms.date: 08/14/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 9083c571-f4fc-4a78-adc5-8aec84dabcbd
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Manage access to company resource based on device, network, and application risk

*Applies to: System Center Configuration Manager (Current Branch)*

Control access from mobile devices to corporate resources based on risk assessment conducted by Lookout. Lookout is a device threat protection solution integrated with Microsoft Intune. The risk is based on data collected by the Lookout service. It gathers data from devices for OS vulnerabilities, installed malicious apps, and malicious network profiles. 

Based on Lookout's reported risk assessment enabled through Configuration Manager compliance policies, you configure conditional access policies. These policies allow or block devices that Configuration Manager determines to be noncompliant due to threats detected on those devices.

> [!Important]  
> As of August 14, 2018, hybrid mobile device management is a [deprecated feature](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures). For more information, see [What is hybrid MDM](/sccm/mdm/understand/hybrid-mobile-device-management).<!--Intune feature 2683117-->  



## How does it work?

How do the hybrid MDM deployment and Lookout device threat protection help protect company resources?

Lookout's mobile app (Lookout for Work) runs on mobile devices. It captures file system, network stack, and device and application usage data where available. The app sends this data to the Lookout device threat protection cloud service to calculate an aggregate device risk for mobile threats. Use the Lookout console to change the classification of the risk level for the threats to suit your requirements.  

The compliance policy in Configuration Manager now includes a new rule for Lookout mobile threat protection that's based on the Lookout device threat risk assessment. When you enable this rule, Configuration Manager evaluates the device for compliance.

If the device is noncompliant with the compliance policy, you can block access to resources like Exchange Online and SharePoint Online using conditional access policies. When access is blocked, the end user receives a walkthrough to help resolve the issue and gain access to company resources. The user launches this walkthrough through the Lookout for Work app.



## Supported platforms

- **Android 4.1 and later**, and enrolled in Microsoft Intune.  

- **iOS 8 and later**, and enrolled in Microsoft Intune.  


For information about platforms and languages that Lookout supports, see this [Lookout support article](https://personal.support.lookout.com/hc/articles/114094140253).



## Prerequisites

- [Hybrid MDM](/sccm/mdm/understand/hybrid-mobile-device-management)  

- A subscription to Microsoft Intune, and Azure Active Directory.  

- An enterprise subscription to Lookout Mobile EndPoint Security. For more information, see [Lookout Mobile Endpoint Security](https://www.lookout.com/products/mobile-endpoint-security).  



## Example scenarios


### Control access based on threat from malicious apps

When malicious apps such as malware are detected on the device, you can block such devices from:

- Connecting to corporate e-mail before resolving the threat  

- Synchronizing corporate files using the OneDrive for Work app  

- Accessing business-critical apps  

#### Access blocked when malicious apps are detected

![Conditional access policy blocking access when malicious app detected](media/config-mgr-maliciousapps_blocked.png)

#### Device unblocked and is able to access company resources when the threat is remediated

![Conditional access policy granting access when device is compliant](media/config-mgr-maliciousapps-unblocked.png)


### Control access based on threat to network

Detect threats to your network such as man-in-the-middle attacks and restrict access to WiFi networks based on the device risk.

#### Access to network through WiFi blocked

![Conditional access blocking WiFi access based on network threats](media/config-mgr-network-wifi-blocked.png)

#### Access granted on remediation

![Conditional access allowing access on remediation of the threat](media/config-mgr-network-wifi-unblocked.png)


### Control access to SharePoint Online based on threat to network

Detect threats to your network such as man-in-the-middle attacks, and prevent synchronization of corporate files based on the device risk.

#### Access blocked SharePoint Online based on network threat detected on the device

![Conditional access blocking device access to SharePoint Online](media/config-mgr-network-spo-blocked.png)


#### Access granted on remediation

![Conditional access allowing access after the threat is remediated](media/config-mgr-network-spo-unblocked.png)



## Next steps

To implement this solution, use the following steps:  

1.	[Set up your subscription with Lookout mobile threat protection](set-up-your-subscription-with-lookout.md)
2.	[Enable Lookout MTP connection in Intune](enable-lookout-connection-in-intune.md)
3.  [Configure and deploy Lookout for work application](configure-and-deploy-lookout-for-work-apps.md)
4.	[Configure compliance policy](enable-device-threat-protection-rule-compliance-policy.md)
5.	[Troubleshoot Lookout integration](troubleshoot-lookout-integration.md)
