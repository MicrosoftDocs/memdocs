---
# required metadata

title: Set up Zimperium MTD integration with Microsoft Intune
titleSuffix: Microsoft Intune
description: How to set up the Zimperium Mobile Threat Defense (MTD) solution with Microsoft Intune to control mobile device access to your corporate resources.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 08/27/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.assetid: 363fd280-1865-4a61-855b-eb75c3c62753

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

# Integrate Zimperium with Intune

Complete the following steps to integrate the Zimperium Mobile Threat Defense solution with Intune.

## Before you begin

The following steps are done in the [Zimperium MTD console](https://www.zimperium.com/platform) and enable a connection to Zimperium's service for both Intune enrolled devices (using device compliance) and unenrolled devices (using app protection policies).

Before starting the process of integrating Zimperium with Intune, make sure you have the following subscription and credentials:

- Microsoft Intune Plan 1 subscription

- Microsoft Entra Global Administrator admin credentials to grant the following permissions:

  - Sign in and read user profile
  - Access the directory as the signed-in user
  - Read directory data
  - Send device information to Intune

- Admin credentials to access Zimperium MTD console.

### Zimperium app authorization

The Zimperium app authorization process follows:

- Grant the Zimperium service permissions to communicate information related to device health state back to Intune. To grant these permissions, you must use Global Administrator credentials. Granting permissions is a one-time operation. After the permissions are granted, the Global Administrator credentials aren't needed for day to day operation.

- Zimperium syncs with Microsoft Entra Enrollment Group membership to populate its device's database.
- Allow Zimperium admin console to use Microsoft Entra single sign-on (SSO).
- Allow the Zimperium app to sign in using Microsoft Entra SSO.

For more information about consent and Microsoft Entra applications, see [Introduction to permissions and consent](/azure/active-directory/develop/permissions-consent-overview) in the Microsoft Entra documentation.

## To set up Zimperium integration

1. Go to [Zimperium MTD console](https://www.zimperium.com/platform) and sign in with your credentials. To perform the Zimperium integration setup process, you must sign in with a Microsoft Entra user who has the Global Administrator role. This one-time setup operation uses the Global Administrator rights to grant permission in your organization for the Zimperium apps to communicate with Intune. 

2. Choose **Management** from the left menu.

3. Choose the **MDM settings** tab.

4. Choose **Add MDM,** then select **Microsoft Intune** from the **MDM provider** list.

5. After you set Microsoft Intune as the MDM service, the **Microsoft Intune Configuration** window pops up, choose the **Add Microsoft Entra ID** for each option: **Zimperium zConsole**, **zIPS iOS and Android apps** to authorize Zimperium to communicate with Intune and Microsoft Entra ID through Microsoft Entra single sign-on.

   > [!IMPORTANT]
   >
   > You must add the Zimperium zConsole, zIPS iOS and Android apps to complete the integration process with Intune.

6. Choose **Accept** to authorize the Zimperium app to communicate with Intune and Microsoft Entra.

7. After you add the **Zimperium zConsole** and the **zIPS iOS and Android** apps to Microsoft Entra, add the Microsoft Entra security groups. This addition allows Zimperium to synchronize the Microsoft Entra security group with its service.

8. Choose **Finish** to save the configuration and start the first Microsoft Entra security group synchronization.

9. Sign out of the Zimperium MTD console.

## Next steps

- [Set up Zimperium apps for enrolled devices](mtd-apps-ios-app-configuration-policy-add-assign.md)
- [Set up Zimperium apps for unenrolled devices](mtd-add-apps-unenrolled-devices.md)
