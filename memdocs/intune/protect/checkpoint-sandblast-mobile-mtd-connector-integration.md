---
# required metadata

title: Integrate Check Point SandBlast MTD
titleSuffix: Microsoft Intune
description: How to set up CheckPoint SandBlast Mobile Threat Defense (MTD) with Intune to control mobile device access to your corporate resources.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 10/21/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology:
ms.assetid: 1e9b1576-b239-48cc-a672-da6b5fb7be0a

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: davidra
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
---

# Integrate Check Point SandBlast Mobile with Intune

Complete the following steps to integrate the Check Point SandBlast Mobile Threat Defense solution with Intune.

> [!NOTE]
> This Mobile Threat Defense vendor is not supported for unenrolled devices.

## Before you begin

The instructions in this article are done in the [Check Point SandBlast Mobile console](https://intune-4.eu1.locsec.net/). 

Before starting the process of integrating Check Point SandBlast Mobile with Intune, make sure you have the following:

- Microsoft Intune subscription

- Azure Active Directory admin credentials to grant the following permissions:

  - Sign in and read user profile

  - Access the directory as the signed-in user

  - Read directory data

  - Send device information to Intune

- Admin credentials to access Check Point SandBlast Mobile MTD console.

### Check Point SandBlast app authorization

The Check Point SandBlast app authorization process consists of the following:

- Allow the Check Point SandBlast Mobile service to communicate information related to device health state back to Intune.

- CheckPoint SandBlast Mobile syncs with Azure AD Enrollment Group membership to populate its device’s database.

- Allow Check Point SandBlast admin console to use Azure AD Single Sign On (SSO).

- Allow the Check Point SandBlast Mobile app to sign in using Azure AD SSO.

## To set up Check Point SandBlast Mobile integration

1. Go to [Check Point SandBlast Mobile MTD console](https://intune-4.eu1.locsec.net/) and sign in with your credentials.

2. Click on the **Settings** tab.

3. Choose **Device management**, then **Settings**.

4. Choose **Microsoft Intune** from the **MDM Service** drop-down list.

5. Once you set Microsoft Intune as the MDM Service, the **Microsoft Intune Configuration** window pops up, choose the **Add to my organization** for each device platform: iOS/iPadOS, Android and Windows to authorize Check Point SandBlast Mobile to communicate with Intune and Azure AD.

    ![Image showing Check Point MTD Intune configuration](./media/checkpoint-sandblast-mobile-mtd-connector-integration/checkpoint-MTD-1.PNG)

    > [!IMPORTANT]
    > You must add all device platforms to proceed to the next step.

6. Choose **Accept** to authorize the Check Point SandBlast Mobile app to communicate with Intune and Azure Active Directory.

7. Once you enabled all device platforms, you need to enter the Azure AD security group.

8. Choose **Verify**, once the Azure AD security group is successfully verified, choose **Save**.

## Next steps

- [Set up Check Point SandBlast Mobile apps](mtd-apps-ios-app-configuration-policy-add-assign.md)
