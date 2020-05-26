---
# required metadata

title: Intune operated by 21Vianet in China
titleSuffix: 
description: Intune operated by 21Vianet in China.
keywords:
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 05/27/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: amsaeedi
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-classic; get-started
ms.collection: M365-identity-device-management
---

# Intune operated by 21Vianet in China  

Intune operated by 21Vianet is designed to meet the needs for secure, reliable, and scalable cloud services in China. Intune as a service is built on top of Microsoft Azure. Microsoft Azure operated by 21Vianet is a physically separated instance of cloud services located in China. It's independently operated and transacted by 21Vianet. This service is powered by technology that Microsoft has licensed to 21Vianet.

Microsoft doesn't operate the service itself. 21Vianet operates, provides, and manages delivery of the service. 21Vianet is an Internet data center services provider in China. It provides hosting, managed network services, and cloud computing infrastructure services. By licensing Microsoft technologies, 21Vianet operates local datacenters to provide you the ability to use Intune service while keeping your data within China. 21Vianet also provides your subscription, billing, and support services.

## Feature differences in Intune operated by 21Vianet

Because the China services are operated by a partner from datacenters inside China, there are some features differences with Intune. 

- Intune operated by 21Vianet only supports standalone deployments and co-management with System Center Configuration Manager.
- Migrations from public clouds to sovereign clouds aren't supported. Customers interested in moving to Intune operated by 21Vianet must migrate manually.
- Co-management support is tracked for August 2020. Tenant attach (syncing devices to Intune without enrollment to support cloud console scenarios) isn't currently supported.
- Intune operated by 21Vianet doesn't support the Intune agent and so doesn't support legacy PC management.
- Management of Windows 10 is supported by using the modern MDM channel.
- Intune operated by 21Vianet doesn't support on-premises Exchange Connector.
- Windows Autopilot and Business Store features aren't currently available.
- Because Google Mobile Services isn't available in China, customers in Intune operated by 21Vianet can't use features that require Google Mobile Services. These features include:
  - Google Play Protect capabilities such as SafetyNet device attestation.
  - Managing apps from the Google Play Store.
  - Android Enterprise capabilities. For more information, see this [Google documentation](https://support.google.com/work/android/answer/6270910?hl=en).
- The Intune Company Portal app for Android uses Google Mobile Services  to communicate with the Microsoft Intune service. Because Google Play services isn't available in China, some tasks can require up to 8 hours to finish. For more information, see this [article](https://docs.microsoft.com/mem/intune/apps/manage-without-gms#limitations-of-intune-device-administrator-management-when-gms-is-unavailable). 
- To follow local regulations and provide improved functionality, the Intune client experience (Company Portal app) may differ in China.
- Fencing isn't available.
- Mobile Application Management (MAM) availability is conditional on those apps being available in mainland China.

## You control customer data

In Microsoft Azure, Intune, Office 365, and Power BI operated by 21Vianet, you have full control of your data:
- You know where customer data is located.
- You control access to your customer data.
- You control your customer data if you leave the service.
- You have options to control the security of your customer data.

With Microsoft Azure, Intune, Office 365, and Power BI operated by 21Vianet, you’re the owner of your data:
- 21Vianet doesn’t use customer data for advertising.
- You control who has access to your customer data.
- We use logical isolation to segregate each customer’s data.
- We provide simple, transparent data-use policies, and get independent audits.
- Our subcontractors are under contract to meet our privacy requirements.

## Data subject requests for GDPR

[General Data Protection Regulation (GDPR)](https://www.microsoft.com/trustcenter/privacy/gdpr/gdpr-overview) grants individuals certain rights concerning their personal data processing. These rights include the right to:
- correct inaccurate data
- erase data or restrict its processing
- receive their data
- fulfill a request to transmit their data to another controller.

The Tenant Administrator role for Intune operated by 21Vianet can request data for data subjects in the following ways:

- Using the Azure Active Directory Admin Center, a Tenant Administrator can permanently delete a data subject from Azure Active Directory and related services.
- System-generated logs for Microsoft services operated by 21Vianet can be exported by Tenant Administrators using the Data Log Export.

## Next steps

[Learn more about Intune supported configurations](supported-devices-browsers.md)