---
# required metadata

title: Manage attack account protection settings with endpoint security policies in Microsoft Intune | Microsoft Docs
description: Configure and deploy policies for devices you manage with endpoint security account protection policy settings in Microsoft Endpoint Manager.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/15/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology:

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha

---

# Account protection policy for endpoint security in Intune

Use Intune endpoint security policies for account protection to protect the identity and accounts of your users. The account protection policy is focused on settings for  Windows Hello and Credential Guard, which is part of Windows identity and access management.

- *Windows Hello for Business* replaces passwords with strong two-factor authentication on PCs and mobile devices.
- *Credential Guard* helps protect credentials and secrets that you use with your devices.

To learn more, see [Identity and access management](https://docs.microsoft.com/windows/security/identity-protection/) in the Windows identity and access management documentation.

Find the endpoint security policies for Account protection under *Manage* in the **Endpoint security** node of the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

View [settings for account protection profiles](../protect/endpoint-security-asr-profile-settings.md).

## Prerequisites for Account protection profiles

- Windows 10 or later

## Account protection profiles

**Windows 10 profiles**:

- **Account protection** – Settings for account protection policies help you protect user credentials.

## Next steps

[Configure Endpoint security policies](../protect/endpoint-security-policy.md#create-an-endpoint-security-policy)
