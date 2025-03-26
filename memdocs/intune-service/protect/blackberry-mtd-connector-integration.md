---
# required metadata

title: Set up BlackBerry Protect with Microsoft Intune
titleSuffix: Microsoft Intune
description: How to set up the CylancePROTECT (BlackBerry) MTD solution with Microsoft Intune to control mobile device access to your corporate resources.
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

# Connect BlackBerry Protect Mobile MTD connector in Microsoft Intune

Connect the BlackBerry Protect Mobile MTD connector to monitor and mitigate device risk levels on Intune-managed devices. BlackBerry Protect Mobile (powered by Cylance AI) works by reporting device risk levels to Microsoft Intune. Intune then uses that information to enforce the appropriate app configuration and risk assessment policies. For more information about BlackBerry Protect Mobile, see [Key features of BlackBerry Protect Mobile](https://docs.blackberry.com/en/unified-endpoint-security/blackberry-ues/how-do-i/integrate-ces-with-mdm) (opens BlackBerry UES docs).

This article describes the requirements and steps to connect the MTD connector in your tenant.

## Before you begin

The following subscriptions and accounts are required to integrate UES with Microsoft Intune.

- Microsoft Intune Plan 1 subscription

- Microsoft Entra account with Global Administrator rights to grant the following permissions:

  - Sign in and read user profile

  - Access the directory as the signed-in user

  - Read directory data

  - Send device information to Intune

- Admin sign-in credentials to access the UES management console

### App authorization

The following authorization process happens when you connect the BlackBerry Protect Mobile MTD connector:

- Allow BlackBerry UES to communicate information related to device health state back to Intune. To grant these permissions, you must use Global Administrator credentials. Granting permissions is a one-time operation. After the permissions are granted, the Global Administrator credentials aren't needed for day-to-day operation.

- Allow BlackBerry UES to sync Microsoft Entra enrollment group membership to populate its device's database.

- Allow BlackBerry UES management console to use Microsoft Entra single sign-on (SSO).

- Allow BlackBerry Protect app to sign in using Microsoft Entra SSO.

For more information about consent and Microsoft Entra applications, see [Introduction to permissions and consent](/azure/active-directory/develop/v2-permissions-and-consent).

## Set up BlackBerry Protect Mobile MTD connector

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) with an Intune administrator account.
2. Go to **Tenant administration**.
3. Select **Connectors and tokens**.
4. Under **Cross platform**, select **Mobile Threat Defense**.
5. Select **Add**.
6. For **Select the Mobile Threat Defense connector to setup,** choose **CylancePROTECT Mobile**.
7. Select **Open the CylancePROTECT Mobile admin console**. Keep the Microsoft Intune admin center tab open for later.
8. Sign in with your Microsoft Entra account, and then follow the instructions in [Integrating UES with Intune to respond to mobile threats](https://docs.blackberry.com/en/unified-endpoint-security/blackberry-ues/setup/setup/Setting-up-BlackBerry-Protect/Integrating-EMM-to-respond-to-mobile-threats) (opens BlackBerry UES docs) to complete setup.
9. After you finish setup in the UES management console, return to your tab in the Microsoft Intune admin center.
10. Under **MDM Compliance Policy Settings**, turn on the following settings:
    - **Connect Android devices to BlackBerry Protect Mobile**
    - **Connect iOS devices to BlackBerry Protect Mobile**
    These settings allow BlackBerry Protect Mobile to evaluate the devices in your organization.
11. Select **Create** to save your connector configurations.

## Next steps

- [Set up BlackBerry Protect app for enrolled devices](mtd-apps-ios-app-configuration-policy-add-assign.md)
