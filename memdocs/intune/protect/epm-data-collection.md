---
title: Review the data that Endpoint Privilege Management collects when used with Microsoft Intune
description: View details about the type of data Endpoint Privilege Management can collect and store when used with Microsoft Intune.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/24/2023
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology:

# optional metadata

#ROBOTS:
#audience:
 
ms.reviewer: mattcall
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier 1
- M365-identity-device-management
---

# Data collection and privacy for Endpoint Privilege Management

<!-- [!INCLUDE [intune-add-on-note](../includes/intune-add-on-note.md)] -->
> [!NOTE]  
> This capability is in public preview and available to use without a license. After public preview, it will be available as an Intune add-on. For more information, see [Use Intune Suite add-on capabilities](../fundamentals/intune-add-ons.md).

Microsoft Intune Endpoint Privilege Management (EPM) allows your organization’s users to run as a standard user (without administrator rights) and complete tasks that require elevated privileges. 

Tasks that commonly require administrative privileges are application installs (like Microsoft 365 Applications), updating device drivers, and running certain Windows diagnostics. 

Endpoint Privilege Management supports your zero-trust journey by helping your organization achieve a broad user base running with least privilege, while allowing users to still run tasks allowed by your organization to remain productive.

This article provides information about the data that EMP can collect from devices.

Applies to:

- Windows 10
- Windows 11

## Overview of data collection

Endpoint Privilege Management on devices can be configured to report on the following data types:

- Diagnostic data
- Usage data

When configuring EPM, you configure the *Reporting scope* in a [Windows elevation settings policies](../protect/epm-policies.md#about-windows-elevation-settings-policy) to determine which data is reported to Microsoft.

## Diagnostic Data

Diagnostic data is event data that is used by Microsoft to monitor the health of the client side components that provide the capability to elevate as a standard user.

## Usage Data

Usage data is elevation data that is used by customers to determine what elevations have occurred in their environment. This data is stored with your Intune infrastructure and is used to populate the elevation reports. When configuring *reporting scope*, you have the ability to configure what scope of data is collected. You can choose between none, only elevations completed by EPM, or all elevations that take place on a device.

### Data collection reference

|Data Type |Property Name|Description|
|-------- |:------------ |---------------|
|**Usage Data** |Tenant Identifier|Identifier (GUID) unique to the tenant.|
||Device Identifier|Identifier (GUID) unique to the device.|
||User Name|Identifier ("AzureAd\User") of the user completing the elevation.|
||Justification|Justification string (if provided) provided by the user when completing the elevation|
||File name|Name of the file (String) that completed the elevation|
||Event Id|Internal identifier (Integer) used to identify the type of elevation described in the event.|
||Event Name|Internal Name (String) used to identify the type of elevation described in the event.|
||Time Created|Time the event was generated on the device.|
||Product Name|File metadata (String) that completed the elevation.|
||Publisher|File metadata (String) that completed the elevation.|
||File Version|File metadata (String) that completed the elevation.|
||File Description|File metadata (String) that completed the elevation.|
||Internal File name|File metadata (String) that completed the elevation.|
||Certificate Payload|File metadata (String) that completed the elevation.|
||Elevation Type|Type of elevation that was facilitated|
||Result|Exit code of elevation operation (Success/Failure)|
||Account Type|Type of account (local or organizational) that completed the elevation.|
||Product Name|File metadata (String) that completed the elevation.|
|**Diagnostic Data** |Device Identifier|Identifier (GUID) unique to the device.|
||Event Id|Internal identifier (Integer) used to identify the type of elevation described in the event.|
||Event Name|Internal Name (String) used to identify the type of elevation described in the event.|
||Time Created|Time the event was generated on the device.|
||Publisher|File metadata (String) that completed the elevation.|
||File Version|File metadata (String) that completed the elevation.|
||Account Type|Type of account (local or organizational) that completed the elevation.|
||Error Code|Exit code of elevation operation (Success/Failure)|
||Parent Process Id|Process Id of the parent process that facilitates the elevation|
||Policy Type|Type of policy that facilitated the elevation (if applicable)|
||Policy Identifier|Identifier (GUID) unique to the policy that facilitated the elevation|
||Policy Version|Version of the policy that facilitated the elevation|
||Elevation Type|Type of elevation that was facilitated|
||Operation Type|Type of policy application, used for policy application operations |
||Cancellation Action Type|Type of cancellation generated by the Administrator|


## Next steps

- [Learn about Endpoint Privilege Management](../protect/epm-overview.md)
- [Guidance for creating Elevation Rules](../protect/epm-guidance-for-creating-rules.md)
- [Configure policies for Endpoint Privilege Management](../protect/epm-policies.md)
- [Reports for Endpoint Privilege Management](../protect/epm-policies.md)
