---
# required metadata

title: Optional diagnostic data that is collected by Intune client apps 
titleSuffix: Microsoft Intune
description: Learn about the optional diagnostic data that Intune Client apps collect.
keywords: privacy, personal data
author: Smritib17
ms.author: smbhardwaj
manager: dougeby
ms.date: 04/08/2022
ms.topic: article
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: angerobe
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
- privacy
- sub-data-privacy
---


# Optional diagnostic data from Intune Client apps

Intune collects various optional data to detect, diagnose, and fix problems from users through various Intune client apps.  These optional diagnostic data we collect help to proactively detect problems in your organization so they can be addressed before they become an issue. Intune client apps include:

- iOS/iPadOS Company Portal
- macOS Company Portal
- Windows Company Portal
- Android Company Portal
- Android Intune app
- Microsoft Intune Management Agent for macOS
- Microsoft Intune Management Extension
- Android Mobile App Management (MAM)

The optional data collected from clients aren't required to successful run Intune services. The data collected helps:

- Provides enhanced information to help us proactively detect, diagnose, and fix issues.
- Makes product and service improvements.

## Data collected

Optional diagnostic data collected by Intune client apps may cover the following areas:

- Microsoft-generated user information
  - Microsoft Entra user ID
  - Device ID
  - Correlation ID
  - App Session ID
  - User Session ID
- Admin and account information
  - Tenant ID
  - Microsoft Entra tenant ID
- Hardware and software information
  - Device OS version
  - Device model
  - Device make
  - Application ID
  - User language
  - User time zone
- Service events and error information
  - Enrollment event
  - Failure event
    - Network failure
    - Runtime failure
    - Task schedule failure
    - Enrollment failure
    - Microsoft Entra authentication failure
  - Crash report
  - Consent state
  - Compliance status
  - Policy status
- Company Portal events
  - Company Portal error
  - Company Portal page action
  - Company Portal page view
  - Company Portal version
- Performance measurement
  - Duration
  - Response time

## Data not collected

The data do not include any customer information, like:

- Device name
- Phone number
- Contents to the user’s files or photo.

## Turn off data collection

We think there are compelling reasons for people to share this optional data. All optional diagnostic data Microsoft collects during the use of any Microsoft 365 Apps for enterprise applications and services is pseudonymized as defined in the ISO/IEC 19944-1:2020 (section 8.3.3) standard.

Users can [turn off usage data collection](../user-help/turn-off-microsoft-usage-data-collection-android.md) for their individual devices.

## Next steps

[Find out more about data collection in Intune.](privacy-data-collect.md)
