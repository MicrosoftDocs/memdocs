---
# required metadata

title: Set up CrowdStrike Falcon for Mobile integration with Intune
titleSuffix: Microsoft Intune
description: How to set up CrowdStrike Falcon Threat Defense with Microsoft Intune to control mobile device access to your corporate resources.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/22/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.assetid:

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier3
- M365-identity-device-management
- sub-mtd-apps
---

# Integrate CrowdStrike Falcon for Mobile with Microsoft Intune

Complete the following steps to integrate the CrowdStrike Falcon for Mobile solution with Intune.

> [!NOTE]
>
> This Mobile Threat Defense vendor is not supported for unenrolled devices.

## Before you begin

The instructions in this article are done in the [CrowdStrike Falcon for Mobile console](https://falcon.crowdstrike.com).

Before starting the process of integrating CrowdStrike Falcon with Intune, make sure you have the following configurations:

- Microsoft Intune Plan 1 subscription
- Microsoft Entra admin credentials to grant the following permissions:

  - Sign in and read user profile
  - Access the directory as the signed-in user
  - Read directory data
  - Send device information to Intune

- Admin credentials to access the CrowdStrike Falcon for Mobile console.

### CrowdStrike Falcon app authorization

The CrowdStrike Falcon app authorization process consists of the following steps:

- Allow the CrowdStrike Falcon for Mobile service to communicate information related to device health state back to Intune.

- CrowdStrike Falcon syncs with Microsoft Entra Enrollment Group membership to populate its device's database.

- Allow the CrowdStrike Falcon for Mobile console to use Microsoft Entra single sign-on (SSO).

- Allow the CrowdStrike Falcon app to sign in using Microsoft Entra SSO.

## Set up CrowdStrike Falcon for Mobile integration

The integration steps are documented by CrowdStrike at [Integrating Falcon for Mobile with Microsoft Intune for remediation actions](https://falcon.crowdstrike.com/documentation/page/odf8977b/integrating-falcon-for-mobile-with-microsoft-intune-for-remediation-actions) in the CrowdStrike documentation. You must sign in with your CrowdStrike credentials before you can access this content.

## Next steps

- [Set up CrowdStrike Falcon apps](mtd-apps-ios-app-configuration-policy-add-assign.md)
