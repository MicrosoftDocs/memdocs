---
# required metadata

title: Miscellaneous policy mapping from Basic Mobility and Security to Intune
titleSuffix: Microsoft Intune
description: A detailed miscellaneous policy map between Basic Mobility and Security access requirements and Intune.
keywords:
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 12/18/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: dagerrit
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: seodec18
ms.collection: M365-identity-device-management
---

# Miscellaneous policy mapping from Basic Mobility and Security to Intune
This article provides mapping details between Basic Mobility and Security to Intune. Specifically, this page maps the following Office 365 Security and Compliance portal policies to the equivalent polices in Microsoft Endpoint Manager admin center:
- Manage organization-wide device access settings 
- Policy name and description
- Device view settings

Because Intune offers more flexibility, each Office policy will translate into multiple Intune and Azure Active Directory (Azure AD) policies to achieve the same result.

If you’re migrating from Basic Mobility and Security to Intune, you can use the [Migration evaluation tool](migrate-to-intune.md) to automate much of this mapping.

## Manage organization-wide device access settings
To see these settings in the office 365 Security and Compliance portal, sign in to the portal and then select **Device security policies** > **Manage organization-wide device access settings**.

These settings are backed by the conditional access policy GraphAggregatorService. It includes:
- Device platforms: iOS, Android
- Target client apps: Mobile app desktop clients
- Access controls: require compliant device

### If a device isn't supported by MDM for Office 365, do you want to allow or block it from using an Exchange account to access your organization's email?

One conditional access policy:

- **Endpoint security** > **Conditional access** > **Classic policies** > **[GraphAggregatorService] Device policy** > **Conditions** > **Client apps (Preview) > **Mobile apps and desktop clients > **Exchange ActiveSync clients** > **Apply policy only to spported platform**

### Are there any security groups you want to exclude from access control?

One conditional access policy:
- **Endpoint security** > **Conditional access** > policy name > **Users and groups** > **Exclude**

## Name and Description

To see these settings in the office 365 Security and Compliance portal, sign in to the portal and then select **Device security policies** > policy name > **Edit policy** > **Name**.

### Name

Three compliance policies and one conditional access policy:
- **Devices** > **Windows** > **Compliance policies** > policy name > **Properties** >  **Basics Edit** > **Name**
- **Devices** > **iOS/iPadOS** > **Compliance policies** > policy name > **Properties** > **Basics Edit** > **Name**
- **Devices** > **Android** > **Compliance policies** > policy name > **Properties** > **Basics Edit** > **Name**
- **Endpoint security** > **Conditional access** > policy name > **Name**

### Description
Intune conditional access policies don’t contain a **Description**. So, the Basic Mobility and Security policy description will only be applied to the compliance policies.

Three compliance policies:
- **Devices** > **Windows** > **Compliance policies** > policy name > **Properties** >  **Basics Edit** > **Description**
- **Devices** > **iOS/iPadOS** > **Compliance policies** > policy name > **Properties** > **Basics Edit** > **Description**
- **Devices** > **Android** > **Compliance policies** > policy name > **Properties** > **Basics Edit** > **Description**

## Device view settings
To see these settings, sign in to the [Microsoft 365 admin center](https://portal.office.com/adminportal/home#/MifoDevices) and then select a device.

### User
- **Devices** > **All devices** > device name > **Overview** > **Enrolled by**

### Device type
- **Devices** > **All devices** > device name > **Overview** > **Operating system**

### State
This is not a default column in the Intune portal device list. You can show it by using the **Columns** picker.
- **Devices** > **All devices** > **Device state** column

### OS version
- **Devices** > **All devices** > device name > **Hardware** > **Operating system version**

### Factory reset
- **Devices** > **All devices** > device name > **Overview** > **Wipe**

### Remove company data
- **Devices** > **All devices** > device name > **Overview** > **Retire**

