---
# required metadata

title: Optional diagnostic data from Intune Client apps
titleSuffix: Microsoft Intune
description: Learn about the optional diagnostic data that Intune Client apps collect.
keywords: privacy, GDPR, personal data
author: erikjeMS
ms.author: erikje
manager: dougeby
ms.date: 09/16/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: angerobe
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---


# Optional diagnostic data from Intune Client apps

Intune collects various optional data to detect, diagnose, and fix problems from users through various Intune client apps. Intune client apps includes:
- iOS/iPadOS Company Portal
- MacOS Company Portal
- Windows Company Portal
- Android Company Portal
- Android Intune app
- MacOS sidecar
- Windows sidecar
- Android Mobile App Management (MAM)

The optional data collected from clients aren't required to successful run Intune services. The data collected helps us make product improvements and provide enhanced information to help us detect, diagnose, and fix issues.

## Data collected

Optional diagnostic data collected by Intune client apps may cover the following areas:

- Microsoft generated user information
    - AAD User ID
    - Device ID
    - Correlation ID
    - App Session GUID
    - SDK User ID
- Admin and account information
    - Tenant ID
    - AAD tenant ID
- Hardware and software information
    - Device OS version
    - Device Model
    - Device Make
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
        - AAD authentication failure
    - Crash report
    - Consent state
    - Compliance status
    - Policy status
- Company Portal events
    - Company Portal Error
    - Company Portal Page Action
    - Company Portal Page View
    - Company Portal Version
- Performance measurement
    - Duration
    - Response time
 
## Data not collected
The data doesn't include any customer information, like device name, phone number, or contents to the user’s files or photo.

## Turn off data collection
Users can [turn off usage data collection](https://docs.microsoft.com/mem/intune/user-help/turn-off-microsoft-usage-data-collection-android) for their individual devices from the Settings app.


## Next steps

[Find out more about data collection in Intune.](privacy-data-collect.md)



