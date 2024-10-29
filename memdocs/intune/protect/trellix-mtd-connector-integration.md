---
# required metadata

title: Set up Trellix Mobile Security MTD with Microsoft Intune
titleSuffix: Microsoft Intune
description: How to set up the Trellix Mobile Security mobile threat defense (MTD) solution with Microsoft Intune to control mobile device access to your corporate resources
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 08/23/2024
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

# Integrate Trellix Mobile Security with Intune

Complete the following steps to integrate the Trellix Mobile Security threat defense solution with Intune.

## Before you begin

The following steps are done in the [Trellix console](https://manage.trellix.com) to enable a connection to the Trellix service for Intune enrolled devices (using device compliance) and unenrolled devices (using app protection policies).

Before starting the process of integrating Trellix Mobile Security with Intune, make sure you have the following subscription and credentials:

- Microsoft Intune Plan 1 subscription
- Microsoft Entra Global Administrator admin credentials to grant the following permissions:

  - Sign in and read user profile
  - Access the directory as the signed-in user
  - Read directory data
  - Send device information to Intune

- Admin credentials to access the Trellix console.

### Trellix Mobile Security app authorization

The Trellix Mobile Security app authorization process follows:

- Grant the Trellix Mobile Security service permissions to communicate information related to device health state back to Intune. To grant these permissions, you must use Global Administrator credentials. Granting permissions is a one-time operation. After the permissions are granted, the Global Administrator credentials aren't needed for day to day operation.

- Trellix Mobile Security syncs with Microsoft Entra Enrollment Group membership to populate its device's database.
- Allow Trellix Mobile Security admin console to use Microsoft Entra Single Sign On (SSO).
- Allow the Trellix Mobile Security app to sign in using Microsoft Entra SSO.

For more information about consent and Microsoft Entra applications, see [Request the permissions from a directory admin](/azure/active-directory/develop/v2-permissions-and-consent#request-the-permissions-from-a-directory-admin) in the Microsoft Entra article *Permissions and consent in the Microsoft Entra v2.0 endpoint*.

## To set up Trellix Mobile Security integration

1. Open the [Trellix console](https://manage.trellix.com) and sign in with your credentials. To perform the Trellix Mobile Security integration setup process, you must sign in with a Microsoft Entra user who has the Global Administrator role. This one-time setup operation uses the Global Administrator rights to grant permission in your organization for the Trellix Mobile Security apps to communicate with Intune.

2. Choose **Manage** from the left menu.
3. Choose the **Integrations** tab.

4. Choose **Add MDM,** then select **Microsoft Intune** from the **MDM provider** list.

5. After you set Microsoft Intune as the MDM service, the **Microsoft Intune Configuration** window pops up, choose the **Add Microsoft Entra ID** for each option: **Trellix console**, **Trellix Mobile Security iOS and Android apps** to authorize Trellix Mobile Security to communicate with Intune and Microsoft Entra ID through Microsoft Entra single sign-on.

   > [!IMPORTANT]
   >
   > You must add the console, and the Trellix Mobile Security iOS and Android apps to complete the integration process with Intune.

6. Choose **Accept** to authorize the Trellix Mobile Security app to communicate with Intune and Microsoft Entra ID.

7. After you add the console and Trellix Mobile Security iOS and Android apps to Microsoft Entra ID, add the Microsoft Entra security groups. This addition allows Trellix Mobile Security to synchronize the Microsoft Entra security group with its service.

8. Choose **Finish** to save the configuration and start the first Microsoft Entra security group synchronization.

9. Sign out of the Trellix Mobile Security MTD console.

## Next steps

- [Set up Trellix Mobile Security apps for enrolled devices](mtd-apps-ios-app-configuration-policy-add-assign.md)
- [Set up Trellix Mobile Security apps for unenrolled devices](mtd-add-apps-unenrolled-devices.md)
