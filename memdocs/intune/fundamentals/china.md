---
# required metadata

title: Intune operated by 21Vianet in China
titleSuffix: 
description: Intune operated by 21Vianet in China.
keywords:
author: Smritib17
ms.author: smbhardwaj
manager: dougeby
ms.date: 08/23/2022
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
ms.collection:
- tier2
- M365-identity-device-management
---

# Intune operated by 21Vianet in China  

Intune operated by 21Vianet is designed to meet the needs for secure, reliable, and scalable cloud services in China. Intune as a service is built on top of Microsoft Azure. Microsoft Azure operated by 21Vianet is a physically separated instance of cloud services located in China. It's independently operated and transacted by 21Vianet. This service is powered by technology that Microsoft has licensed to 21Vianet.

Microsoft doesn't operate the service itself. 21Vianet operates, provides, and manages delivery of the service. 21Vianet is an Internet data center services provider in China. It provides hosting, managed network services, and cloud computing infrastructure services. By licensing Microsoft technologies, 21Vianet operates local datacenters to provide you the ability to use Intune service while keeping your data within China. 21Vianet also provides your subscription, billing, and support services.

[!INCLUDE [GDPR-related guidance](../includes/gdpr-dsr-and-stp-note.md)]

## Feature differences in Intune operated by 21Vianet

Because the China services are operated by a partner from inside China, there are some feature differences with Intune. 

- Intune operated by 21Vianet only supports standalone deployments. Customers can use co-management to attach their existing Configuration Manager deployment to the Microsoft Intune cloud.
- Migrations from public clouds to sovereign clouds aren't supported. Customers interested in moving to Intune operated by 21Vianet must migrate manually.
- The tenant attach feature (syncing devices to Intune without enrollment to support cloud console scenarios) isn't currently supported.
- Derived Credentials are not supported with Intune operated by 21Vianet.
- Management of Windows 10 is supported by using the modern MDM channel.
- Intune operated by 21Vianet doesn't support on-premises Exchange Connector.
- Windows Autopilot and Business Store features aren't currently available.
- Microsoft Endpoint Manager Endpoint Analytics and Log Analytics features aren't currently available.
- Because Google Mobile Services isn't available in China, customers in Intune operated by 21Vianet can't use features that require Google Mobile Services. These features include:
  - Google Play Protect capabilities such as SafetyNet device attestation.
  - Managing apps from the Google Play Store.
  - Android Enterprise capabilities. For more information, see this [Google documentation](https://support.google.com/work/android/answer/6270910?hl=en).
- The Intune Company Portal app for Android uses Google Mobile Services  to communicate with the Microsoft Intune service. Because Google Play services isn't available in China, some tasks can require up to 8 hours to finish. For more information, see this [article](../apps/manage-without-gms.md#limitations-of-intune-management-when-gms-is-unavailable). 
- To follow local regulations and provide improved functionality, the Intune client experience (Company Portal app) may differ in China.
- Fencing isn't available.
- Mobile Application Management (MAM) availability is conditional on those apps being available in People's Republic of China.
- Intune operated by 21Vianet doesn't support Android (AOSP) management for corporate devices. 
- Intune operated by 21Vianet doesn't support Mobile Threat Defense (MTD) connector for Android and iOS devices with MTD vendors.
- Intune operated by 21Vianet doesn't support partner device management integration with Jamf for macOS devices.

## You control customer data

In Microsoft Azure, Intune, Microsoft 365, and Power BI operated by 21Vianet, you have full control of your data:
- You know where customer data is located.
- You control access to your customer data.
- You control your customer data if you leave the service.
- You have options to control the security of your customer data.

With Microsoft Azure, Intune, Microsoft 365, and Power BI operated by 21Vianet, you’re the owner of your data:
- 21Vianet doesn’t use customer data for advertising.
- You control who has access to your customer data.
- We use logical isolation to segregate each customer’s data.
- We provide simple, transparent data-use policies, and get independent audits.
- Our subcontractors are under contract to meet our privacy requirements.

## Data subject requests

The Tenant Administrator role for Intune operated by 21Vianet can request data for data subjects in the following ways:

- Using the Azure Active Directory Admin Center, a Tenant Administrator can permanently delete a data subject from Azure Active Directory and related services. For more information, see [Azure Data Subject Requests - Delete](/microsoft-365/compliance/gdpr-dsr-azure#step-5-delete)
- System-generated logs for Microsoft services operated by 21Vianet can be exported by Tenant Administrators using the Data Log Export. For more information, see [Azure Data Subject Requests - Export](/microsoft-365/compliance/gdpr-dsr-azure#step-6-export).

## Next steps

[Learn more about Intune supported configurations](supported-devices-browsers.md)
