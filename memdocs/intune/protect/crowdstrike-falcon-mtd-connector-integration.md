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
---

# Integrate CrowdStrike Falcon for Mobile with Microsoft Intune

Complete the following steps to integrate the CrowdStrike Falcon Mobile Threat Defense solution with Intune.

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

## To set up CrowdStrike Falcon for Mobile integration

<!-- This procedural guidance, or link to CrowdStrike docs, is pending.>

1. Go to [CrowdStrike Falcon for Mobile console](https://falcon.crowdstrike.com) and sign in with your credentials.

2. Select on the **Settings** tab.

3. Choose **Device management**, then **Settings**.

4. Choose **Microsoft Intune** from the **MDM Service** drop-down list.

5. Once you set Microsoft Intune as the MDM Service, the **Microsoft Intune Configuration** window pops up, choose the **Add to my organization** for each device platform: iOS/iPadOS, Android and Windows to authorize CrowdStrike Falcon for Mobile to communicate with Intune and Microsoft Entra ID.

   > [!IMPORTANT]
   >
   > You must add all device platforms to proceed to the next step.

6. Choose **Accept** to authorize the CrowdStrike Falcon app to communicate with Intune and Microsoft Entra.

7. Once you enabled all device platforms, you need to enter the Microsoft Entra security group.

8. Choose **Verify**, once the Microsoft Entra security group is successfully verified, choose **Save**.
-->

## Next steps

- [Set up CrowdStrike Falcon apps](mtd-apps-ios-app-configuration-policy-add-assign.md)
