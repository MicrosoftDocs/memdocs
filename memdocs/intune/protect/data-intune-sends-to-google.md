---
# required metadata

title: Data Intune sends to Google
titleSuffix: Microsoft Intune
description: List of data that Intune sends to Google when Android enterprise device management is enabled with Intune.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/08/2022
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology:
ms.assetid: a5c3bec4-18ed-11e8-accf-0ed5f89f718b


# optional metadata

#ROBOTS:
#audience:

ms.reviewer: 
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Data Intune sends to Google

When Android enterprise device management is enabled on a device, Microsoft Intune establishes a connection with Google and shares user and device information with Google. Before Microsoft Intune can establish a connection, you must create a Google account.

The following table lists the data that Microsoft Intune sends to Google when device management is enabled on a device:


| Data sent to Google | Details | Used for | Example |
|:---:|:---:|:---:|:---:|
| EnterpriseId | Originated in Google upon binding your Gmail account to Intune. | Primary identifier used to communicate between Intune and Google.  This communication includes setting policies, managing devices, and binding/unbinding of Android enterprise with Intune. | Unique identifier, Example format: LC04eik8a6 |
| Policy Body | Originated in Intune when saving a new app or configuration policy. | Applying policies to devices. | This is a collection of all configured settings for an application or configuration policy. This can contain customer information if provided as part of a policy, such as network names, application names, and app-specific settings. |
| Device Data | Devices for Android Enterprise Corporate-Owned Personally-Owned Work Profile scenarios begin with enrollment in Intune. Devices for Managed device scenarios begin with enrollment into Google. | Device Data information is sent between Intune and Google for various actions such as applying policies, managing the device and general reporting. | **Unique identifier to represent Device Name.** Example: enterprises/LC04ebru7b/devices/3592d971168f9ae4<br>**Unique Identifier to represent User Name.** Example: Enterprises/LC04ebru7b/users/116838519924207449711<br>**Device state.** Examples: Active, Disabled, Provisioning.<br>**Compliance states.** Examples: Setting not supported, missing required apps<br>**Software Info.** Examples: software versions & patch level.<br>**Network Info.** Examples: IMEI, MEID, WifiMacAddress<br>**Device Settings.** Examples: Information on encryption levels & whether device allows unknown apps.<br> See below for an example of a JSON message. |
| newPassword | Originated in Intune. | Resetting device passcode. | String representing new password. |
| Google User | Google | Managing the work profile for Personally-Owned Work Profile (BYOD) scenarios. | Unique identifier to represent the linked Gmail account. Example: 114223373813435875042 |
| Application Data | Originated in Intune when saving application policy. |  | Application Name string. Example: app:com.microsoft.windowsintune.companyportal |
| Enterprise Service Account | Originated in Google upon Intune request. | Used for authentication between Intune and Google for transactions involving this customer. | There are several parts:<br> **Enterprise Id**: documented previously.<br>**UPN**: generated UPN used in authentication on behalf of customer.<br>Example: w49d77900526190e26708c31c9e8a0@pfwp-commicrosoftonedfmdm2.google.com.iam.gserviceaccount.com<br>**Key**: Base64 encoded blob used in auth requests, stored encrypted in the service, but this is what the blob looks like:<br> Unique Identifier to represent the customer's key<br>Example: a70d4d53eefbd781ce7ad6a6495c65eb15e74f1f |

To stop using Android enterprise device management with Microsoft Intune and delete the data, you must both disable the Microsoft Intune Android enterprise device management and also delete your Google account. Refer to Google account how to perform account management.