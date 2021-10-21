---
# required metadata

title: Integrate Blackberry Mobile Threat Protection with Microsoft Intune
titleSuffix: Microsoft Intune
description: How to set up the Blackberry Mobile Threat Protection (MTD) solution with Microsoft Intune to control mobile device access to your corporate resources.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 1/22/2021
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology:
ms.assetid: 363fd280-1865-4a61-855b-eb75c3c62753

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Integrate Blackberry Mobile Threat Protection with Intune

Complete the following steps to integrate the Blackberry mobile threat defense solution with Intune.

## Before you begin

The following steps are done in the Blackberry Mobile Threat Protection console <!-- Link pending --> and will enable a connection to Blackberry's service for Intune enrolled devices (using device compliance) and unenrolled devices (using app protection policies).

Before starting the process of integrating Blackberry Mobile Threat Protection with Intune, make sure you have the following subscription and credentials:

- Microsoft Intune subscription

- Azure Active Directory Global Administrator admin credentials to grant the following permissions:

  - Sign in and read user profile

  - Access the directory as the signed-in user

  - Read directory data

  - Send device information to Intune

- Admin credentials to access the Blackberry Mobile Threat Protection console.

### Blackberry Mobile Threat Protection app authorization

The Blackberry Mobile Threat Protection app authorization process follows:

- Grant the Blackberry Mobile Threat Protection service permissions to communicate information related to device health state back to Intune. To grant these permissions, you must use Global Administrator credentials. Granting permissions is a one-time operation. After the permissions are granted, the Global Administrator credentials aren't needed for day to day operation.

- Blackberry Mobile Threat Protection syncs with Azure Active Directory (AD) Enrollment Group membership to populate its device's database.

- Allow Blackberry Mobile Threat Protection admin console to use Azure AD Single Sign On (SSO).

- Allow the Blackberry Mobile Threat Protection app to sign in using Azure AD SSO.

For more information about consent and Azure Active Directory applications, see [Request the permissions from a directory admin](/azure/active-directory/develop/v2-permissions-and-consent#request-the-permissions-from-a-directory-admin) in the Azure Active Directory article *Permissions and consent in the Azure Active Directory v2.0 endpoint*.


## To set up Blackberry Mobile Threat Protection integration

***The actual console name, link, and following step details are pending***

1. Go to [Blackberry Mobile Threat Protection console]() and sign in with your credentials. To perform the Blackberry Mobile Threat Protection integration setup process, you must sign in with an Azure Active Directory user who has the Global Administrator role. This one-time setup operation uses the Global Administrator rights to grant permission in your organization for the Blackberry Mobile Threat Protection apps to communicate with Intune.

2. Choose **Management** from the left menu.

3. Choose the **MDM settings** tab.

4. Choose **Add MDM,** then select **Microsoft Intune** from the **MDM provider** list.

5. After you set Microsoft Intune as the MDM service, the **Microsoft Intune Configuration** window pops up, choose the **Add Azure Active Directory** for each option: **Blackberry Mobile Threat Protection console**, **Blackberry Mobile Threat Protection iOS and Android apps** to authorize Blackberry Mobile Threat Protection to communicate with Intune and Azure AD through Azure AD Single Sign-On.

    > [!IMPORTANT]  
    > You must add the console, and the Blackberry Mobile Threat Protection iOS and Android apps to complete the integration process with Intune.

6. Choose **Accept** to authorize the Blackberry Mobile Threat Protection app to communicate with Intune and Azure Active Directory.

7. After you add the console and Blackberry Mobile Threat Protection iOS and Android apps to Azure AD, add the Azure AD security groups. This addition allows Blackberry Mobile Threat Protection to synchronize the Azure AD security group with its service.

8. Choose **Finish** to save the configuration and start the first Azure AD security group synchronization.

9. Sign out of the Blackberry Mobile Threat Protection MTD console.

## Next steps

- [Set up Blackberry Mobile Threat Protection apps for enrolled devices](mtd-apps-ios-app-configuration-policy-add-assign.md)
- [Set up Blackberry Mobile Threat Protection apps for unenrolled devices](mtd-add-apps-unenrolled-devices.md)
