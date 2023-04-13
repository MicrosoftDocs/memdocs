---
# required metadata

title: Integrate SentinelOne MTD with Microsoft Intune
titleSuffix: Microsoft Intune
description: How to set up the SentinelOne Mobile Threat Defense (MTD) solution with Microsoft Intune to control mobile device access to your corporate resources.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 01/20/2023
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology:
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

# Integrate SentinelOne with Intune

Complete the following steps to integrate the SentinelOne Mobile Threat Defense solution with Intune.

## Before you begin

The following steps are done in the [SentinelOne Management Console](https://console.mobile.sentinelone.net) and will enable a connection to SentinelOne’s service for both Intune enrolled devices (using device compliance) and unenrolled devices (using app protection policies).

Before starting the process of integrating SentinelOne with Intune, make sure you have the following subscription and credentials:

- Microsoft Intune Plan 1 subscription

- Azure Active Directory Global Administrator admin credentials to grant the following permissions:

  - Sign in and read user profile

  - Access the directory as the signed-in user

  - Read directory data

  - Send device information to Intune

- Admin credentials to access the SentinelOne Management Console.

### SentinelOne app authorization

The SentinelOne app authorization process follows:

- Grant the SentinelOne service permissions to communicate information related to device health state back to Intune. To grant these permissions, you must use Global Administrator credentials. Granting permissions is a one-time operation. After the permissions are granted, the Global Administrator credentials aren't needed for day to day operation.

- SentinelOne syncs with Azure Active Directory (AD) Enrollment Group membership to populate its device's database.

- Allow SentinelOne Management Console to use Azure AD Single Sign On (SSO).

- Allow the SentinelOne app to sign in using Azure AD SSO.

For more information about consent and Azure Active Directory applications, see [Request the permissions from a directory admin](/azure/active-directory/develop/v2-permissions-and-consent#request-the-permissions-from-a-directory-admin) in the Azure Active Directory article *Permissions and consent in the Azure Active Directory v2.0 endpoint*.

## To set up SentinelOne integration

1. Go to [SentinelOne Management Console]( https://console.mobile.sentinelone.net) and sign in with your credentials. To perform the SentinelOne integration setup process, you must sign in with an Azure Active Directory user who has the Global Administrator role. This one-time setup operation uses the Global Administrator rights to grant permission in your organization for the SentinelOne apps to communicate with Intune.  

2. Choose **Management** from the left menu.

3. Choose the **MDM settings** tab.

4. Choose **Add MDM,** then select **Microsoft Intune** from the **MDM provider** list.

5. After you set Microsoft Intune as the MDM service, the **Microsoft Intune Configuration** window pops up, choose the **Add Azure Active Directory** for each option: **SentinelOne Management Console**, **SentinelOne iOS and Android apps**, to authorize SentinelOne to communicate with Intune and Azure AD through Azure AD Single Sign-On.

    > [!IMPORTANT]  
    > You must add the SentinelOne Management Console and SentinelOne iOS and Android apps to complete the integration process with Intune.

6. Choose **Accept** to authorize the SentinelOne app to communicate with Intune and Azure Active Directory.

7. After you add the **SentinelOne Management Console** and the **SentinelOne iOS and Android apps** apps to Azure AD, add the Azure AD security groups. This addition allows SentinelOne to synchronize the Azure AD security group with its service.

8. Choose **Finish** to save the configuration and start the first Azure AD security group synchronization.

9. Sign out of the SentinelOne MTD console.

## Next steps

- [Set up SentinelOne apps for enrolled devices](mtd-apps-ios-app-configuration-policy-add-assign.md)
- [Set up SentinelOne apps for unenrolled devices](mtd-add-apps-unenrolled-devices.md)