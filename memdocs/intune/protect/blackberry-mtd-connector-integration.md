---
# required metadata

title: Integrate Blackberry Cylance AI with Microsoft Intune
titleSuffix: Microsoft Intune
description: How to set up the Blackberry Cylance AI with Microsoft Intune to control mobile device access to your corporate resources.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 12/16/2021
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

# Integrate Blackberry Cylance AI with Intune

Complete the following steps to integrate the Blackberry Cylance AI solution with Intune.

## Before you begin

The following steps are done in the Blackberry Cylance AI console and will enable a connection to Blackberry's service for Intune enrolled devices (using device compliance) and unenrolled devices (using app protection policies).

Before starting the process of integrating Blackberry Cylance AI with Intune, make sure you have the following subscription and credentials:

- Microsoft Intune subscription

- Azure Active Directory Global Administrator admin credentials to grant the following permissions:

  - Sign in and read user profile

  - Access the directory as the signed-in user

  - Read directory data

  - Send device information to Intune

- Admin credentials to access the Blackberry Cylance AI console.

### Blackberry Cylance AI app authorization

The Blackberry Cylance AI app authorization process follows:

- Grant the Blackberry Cylance AI service permissions to communicate information related to device health state back to Intune. To grant these permissions, you must use Global Administrator credentials. Granting permissions is a one-time operation. After the permissions are granted, the Global Administrator credentials aren't needed for day to day operation.

- Blackberry Cylance AI syncs with Azure Active Directory (AD) Enrollment Group membership to populate its device's database.

- Allow Blackberry Cylance AI admin console to use Azure AD Single Sign On (SSO).

- Allow the Blackberry Cylance AI app to sign in using Azure AD SSO.

For more information about consent and Azure Active Directory applications, see [Request the permissions from a directory admin](/azure/active-directory/develop/v2-permissions-and-consent#request-the-permissions-from-a-directory-admin) in the Azure Active Directory article *Permissions and consent in the Azure Active Directory v2.0 endpoint*.


## To set up Blackberry Cylance AI integration

During setup, use an Azure Active Directory (Azure AD) account that has Global Administrator rights. These rights are needed to grant permission for Blackberry Mobile Threat Protection apps to communicate with Intune. For detailed setup instructions, see [How to set up UES](https://docs.blackberry.com/en/unified-endpoint-security/blackberry-ues) on the Blackberry UES website.         

1.	Sign it to the Blackberry Mobile Threat Protection console. 
2.	Go to your MDM settings and add Microsoft Intune as an MDM provider.  
3.	A new window opens and prompts you with Microsoft Intune configuration settings. Add Azure AD for each of the following options:
    * Blackberry Mobile Threat Protection console 
    * Blackberry Mobile Threat Protection iOS and Android apps  

    This step authorizes Blackberry Mobile Threat Protection to communicate with Intune and Azure AD via Azure AD single sign-on.  
4.	Read and accept the terms that authorize the Blackberry Mobile Threat Protection app to communicate with Intune and Azure AD.  
5.	Add Azure AD security groups to sync them with the Blackberry Mobile Threat Protection service.  
6.	Finish setup to save your configurations and start the first Azure AD security group-synchronization.  
7.	Sign out of the Blackberry Mobile Threat Protection MTD console.  

## Next steps

- [Set up Blackberry Cylance AI apps for enrolled devices](mtd-apps-ios-app-configuration-policy-add-assign.md)
- [Set up Blackberry Cylance AI apps for unenrolled devices](mtd-add-apps-unenrolled-devices.md)
