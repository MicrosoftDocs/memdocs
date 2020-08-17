---
title: Conditional Access with co-management
titleSuffix: Configuration Manager
description: Control user access to organizational resources based on compliance rules from Intune
ms.date: 05/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: 4cf640b3-610c-4c3c-b966-c62e9f5654ff
author: aczechowski
ms.author: aaroncz
manager: dougeby


---

# Conditional Access with co-management

Conditional Access makes sure that only trusted users can access organizational resources on trusted devices using trusted apps. It's built from scratch in the cloud. Whether you're managing devices with Intune or extending your Configuration Manager deployment with co-management, it works the same way.

In the following video, senior program manager Joey Glocke and product marketing manager Locky Ainley discuss and demo Conditional Access with co-management:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/The-Security-Benefits-of-Conditional-Access/player]

With co-management, Intune evaluates every device in your network to determine how trustworthy it is. It does this evaluation in the following two ways:

1. Intune makes sure a device or app is managed and securely configured. This check depends on how you set your organization's compliance policies. For example, make sure all devices have encryption enabled and aren't jailbroken.  

    - This evaluation is pre-security breach and configuration-based  

    - For co-managed devices, Configuration Manager also does configuration-based evaluation. For example, required updates or apps compliance. Intune combines this evaluation along with its own assessment.  

2. Intune detects active security incidents on a device. It uses the intelligent security of [Microsoft Defender Advanced Threat Protection](/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection) (formerly Windows Defender ATP) and other [mobile threat defense providers](https://www.lookout.com/about/partners/microsoft). These partners run ongoing behavioral analysis on devices. This analysis detects active incidents, and then passes this information to Intune for real-time compliance evaluation.  

    - This evaluation is post-security breach and incident-based  

Microsoft corporate vice president Brad Anderson discusses Conditional Access in depth with live demos during the Ignite 2018 keynote. 

> [!VIDEO https://www.youtube.com/embed/7tDbUhVCX_I?start=1071]

Conditional Access also provides you a centralized place to see the health of all network-connected devices. You get the advantages of cloud scale, which is especially valuable for testing Configuration Manager production instances.


## Benefits

Every IT team is obsessed with network security. It's mandatory to make sure that every device meets your security and business requirements before accessing your network. With Conditional Access, you can determine the following factors: 
- If every device is encrypted  
- If malware is installed  
- If its settings are updated  
- If it's jailbroken or rooted  

Conditional Access combines granular control over organizational data with a user experience that maximizes worker productivity on any device from any location.

The following video shows how [Advanced Thread Protection](https://www.microsoft.com/windowsforbusiness/windows-atp) (ATP) is integrated into common scenarios that you regularly experience:

> [!VIDEO https://www.youtube.com/embed/A7IrxAH87wc?start=178]

With co-management, Intune can incorporate Configuration Manager's responsibilities for assessing your security standards compliance of required updates or apps. This behavior is important for any IT organization that wants to continue using Configuration Manager for complex app and patch management.

Conditional Access is also a critical part of developing your [Zero Trust Network](https://cloudblogs.microsoft.com/microsoftsecure/2018/06/14/building-zero-trust-networks-with-microsoft-365/) architecture. With Conditional Access, compliant device access controls cover the foundational layers of Zero Trust Network. This functionality is a large part of how you secure your organization in the future.

For more information, see the blog post on [Enhancing Conditional Access with machine-risk data from Microsoft Defender Advanced Threat Protection](https://techcommunity.microsoft.com/t5/Enterprise-Mobility-Security/Enhancing-conditional-access-with-machine-risk-data-from-Windows/ba-p/250559).



## Case studies

The IT consulting firm Wipro uses Conditional Access to protect and manage the devices used by all 91,000 employees. In a recent case study, the vice president of IT at Wipro noted:

> *Achieving Conditional Access is a big win for Wipro. Now, all our employees have mobile access to information on demand.*
> *We enhanced our security posture and employee productivity. Now 91,000 employees benefit from highly secure access to more than 100 apps from any device, anywhere.*

<!-- waiting for the case study to be public
For more information, see [Wipro drives mobile productivity with Microsoft cloud security tools to improve customer engagements](https://customers.microsoft.com/story/446f72f9-2f50-4697-b688-6d279786e010)
-->

Other examples include: 

- Nestlé, who uses app-based Conditional Access for over 150,000 employees  

- The automation software company, Cadence, who can now make sure that "only managed devices have access to Microsoft 365 Apps like Teams and the company's intranet." They can also offer their workforce "safer access to other cloud-based apps, such as Workday and Salesforce." For more information about Cadence's experience with Intune, see [Cadence increases the pace of business with mobile collaboration tools in Microsoft 365](https://customers.microsoft.com/story/cadence-partner-professional-services-microsoft-365).

Intune is also fully integrated with partners like Cisco ISE, Aruba Clear Pass, and Citrix NetScaler. With these partners, you can maintain access controls based on the Intune enrollment and the device compliance state across these other platforms.

For more information, see the following videos:
- [Brad Anderson demos Conditional Access in detail](https://youtu.be/8321obNofgM?t=547)  
- [Additional detail from Endpoint Zone 1805](https://youtu.be/f-ILlEuBFZg?t=196)  


## Value proposition

With Conditional Access and ATP integration, you're fortifying a fundamental component of every IT organization: secure cloud access.

In more than 63% of all data breaches, the attackers gain access to the organization's network through weak, defaulted, or stolen user credentials. Because Conditional Access focuses on securing the user identity, it restricts credential theft. Conditional Access manages and protects your identities, whether privileged or non-privileged. There's no better way to protect the devices and the data on them.

Since Conditional Access is a core component of Enterprise Mobility + Security (EMS), there's no on-premises setup or architecture required. With Intune and Azure Active Directory (Azure AD), you can quickly configure Conditional Access in the cloud. If you're currently using Configuration Manager, you can easily extend your environment to the cloud with co-management and begin using it right now.

For more information about the ATP integration, see this blog post [Microsoft Defender ATP device risk score exposes new cyberattack, drives Conditional Access to protect networks](https://cloudblogs.microsoft.com/microsoftsecure/2018/11/28/windows-defender-atp-device-risk-score-exposes-new-cyberattack-drives-conditional-access-to-protect-networks/). It details how an advanced hacker group used never before seen tools. The Microsoft cloud detected and stopped them because the targeted users had Conditional Access. The intrusion activated the device's risk-based Conditional Access policy. Although the attacker already established a foothold in the network, the exploited machines were automatically restricted from access to organizational services and data managed by Azure AD.



## Configure

Conditional Access is easy to use when you [enable co-management](how-to-enable.md). It requires moving the **Compliance Policies** workload to Intune. For more information, see [How to switch Configuration Manager workloads to Intune](how-to-switch-workloads.md). 

For more information about using Conditional Access, see the following articles: 

- [Conditional Access in Azure AD](https://docs.microsoft.com/azure/active-directory/conditional-access/overview)  

- [Intune device compliance policies](https://docs.microsoft.com/intune/device-compliance)  

- [App-based Conditional Access with Intune](https://docs.microsoft.com/intune/app-based-conditional-access-intune)  

> [!Note]  
> Conditional Access features become available immediately for hybrid Azure AD-joined devices. These features include multi-factor authentication and hybrid Azure AD join access control. This behavior is because they're based on Azure AD properties. To leverage configuration-based assessment from Intune and Configuration Manager, enable co-management. This configuration gives you access control directly from Intune for compliant devices. It also gives you Intune's compliance policies evaluation feature.  

