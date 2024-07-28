---
# required metadata

title: Miscellaneous policy mapping from Basic Mobility and Security to Intune
description: A detailed miscellaneous policy map between Basic Mobility and Security access requirements and Intune.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 11/02/2023
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: dagerrit
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.collection:
- tier2
- M365-identity-device-management
---

# Miscellaneous policy mapping from Basic Mobility and Security to Intune

This article provides mapping details between Basic Mobility and Security to Intune. Specifically, this page maps the following Microsoft Purview compliance portal policies and device properties to the equivalent policies and properties in the Microsoft Intune admin center:

- Device properties and actions
- Organization-wide device access settings
- Device security policies Name and Description

Intune offers more policy flexibility. So, each Office policy translates into multiple Intune and Microsoft Entra policies to achieve the same result.

If you're migrating from Basic Mobility and Security to Intune, you can use the [Migration evaluation tool](migrate-to-intune.md) to automate much of this mapping.

## Device properties and actions

To see these settings, sign in to the [Microsoft 365 admin center](https://portal.office.com/adminportal/home#/MifoDevices) and then select a device.

### User

- **Devices** > **All devices** > device name > **Overview** > **Enrolled by**

### Device type

- **Devices** > **All devices** > device name > **Overview** > **Operating system**

### State

This setting isn't a default column in the admin center device list. You can show it by using the **Columns** picker.

- **Devices** > **All devices** > **Device state** column

### OS version

- **Devices** > **All devices** > device name > **Hardware** > **Operating system version**

### Factory reset

- **Devices** > **All devices** > device name > **Overview** > **Wipe**

### Remove company data

- **Devices** > **All devices** > device name > **Overview** > **Retire**

## Organization-wide device access settings

To see these settings in the Microsoft Purview compliance portal, sign in to the [Purview compliance portal](https://protection.office.com/devicev2). Then, select **Device security policies** > **Manage organization-wide device access settings**.

These settings are backed by the Conditional Access policy [GraphAggregatorService] Device policy. It includes:

- Device platforms: iOS, Android
- Target client apps: Mobile app desktop clients
- Access controls: require compliant device

### If a device isn't supported by MDM for Office 365, do you want to allow or block it from using an Exchange account to access your organization's email?

This setting modifies one classic Conditional Access policy:

- **Endpoint security** > **Conditional access** > **Classic policies** > **[GraphAggregatorService] Device policy** > **Conditions** > **Client apps (Preview)** > **Mobile apps and desktop clients** > **Exchange ActiveSync clients** > **Apply policy only to supported platform**

### Are there any security groups you want to exclude from access control?

This setting modifies five classic Conditional Access policies:

- [GraphAggregatorService] Device policy
- [Office 365 Exchange Online] Device policy
- [Outlook Service for Exchange] Device policy
- [Office 365 SharePoint Online] Device policy
- [Outlook Service for OneDrive] Device policy

- **Endpoint security** > **Conditional access** > policy name > **Users and groups** > **Exclude**

## Device security policy Name and Description

To see these settings in the Microsoft Purview compliance portal, sign in to the [Purview compliance portal](https://protection.office.com/devicev2). Then, select **Device security policies** > policy name > **Edit policy** > **Name**.

### Name

Up to three compliance policies and up to six configuration profiles (three for restrictions and three for email):

- **Devices** > **By platform** > **Windows** > **Manage devices** > **Compliance** > policy name_O365_W > **Properties** >  **Basics Edit** > **Name**
- **Devices** > **By platform** > **iOS/iPadOS** > **Manage devices** > **Compliance** > policy name_O365_i > **Properties** > **Basics Edit** > **Name**
- **Devices** > **By platform** > **Android** > **Manage devices** > **Compliance** > policy name_O365_A > **Properties** > **Basics Edit** > **Name**
- **Devices** > **By platform** > **Windows** > **Manage devices** > **Configuration** > policy name_O365_W > **Properties** >  **Basics Edit** > **Name**
- **Devices** > **By platform** > **iOS/iPadOS** > **Manage devices** > **Configuration**> policy name_O365_i > **Properties** > **Basics Edit** > **Name**
- **Devices** > **By platform** > **Android** > **Manage devices** > **Configuration** > policy name_O365_A > **Properties** > **Basics Edit** > **Name**
- **Devices** > **By platform** > **Windows** > **Manage devices** > **Configuration** > policy name_O365_W_Email > **Properties** >  **Basics Edit** > **Name**
- **Devices** > **By platform** > **iOS/iPadOS** > **Manage devices** > **Configuration**> policy name_O365_i_Email > **Properties** > **Basics Edit** > **Name**
- **Devices** > **By platform** > **Android** > **Manage devices** > **Configuration** > policy name_O365_A_Email > **Properties** > **Basics Edit** > **Name**

### Description

Up to three compliance policies and up to six configuration profiles (three for restrictions and three for email):

- **Devices** > **By platform** > **Windows** > **Manage devices** > **Compliance** > policy name_O365_W > **Properties** >  **Basics Edit** > **Description**
- **Devices** > **By platform** > **iOS/iPadOS** > **Manage devices** > **Compliance** > policy name_O365_i > **Properties** > **Basics Edit** > **Description**
- **Devices** > **By platform** > **Android** > **Manage devices** > **Compliance** > policy name_O365_A > **Properties** > **Basics Edit** > **Description**
- **Devices** > **By platform** > **Windows** > **Manage devices** > **Configuration** > policy name_O365_W > **Properties** >  **Basics Edit** > **Description**
- **Devices** > **By platform** > **iOS/iPadOS** > **Manage devices** > **Configuration**> policy name_O365_i > **Properties** > **Basics Edit** > **Description**
- **Devices** > **By platform** > **Android** > **Manage devices** > **Configuration** > policy name_O365_A > **Properties** > **Basics Edit** > **Description**
- **Devices** > **By platform** > **Windows** > **Manage devices** > **Configuration** > policy name_O365_W_Email > **Properties** >  **Basics Edit** > **Description**
- **Devices** > **By platform** > **iOS/iPadOS** > **Manage devices** > **Configuration**> policy name_O365_i_Email > **Properties** > **Basics Edit** > **Description**
- **Devices** > **By platform** > **Android** > **Manage devices** > **Configuration** > policy name_O365_A_Email > **Properties** > **Basics Edit** > **Description**

## Related article

To migrate these policies, you can use the [Migration evaluation tool](migrate-to-intune.md).
