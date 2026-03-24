---
title: Set up iVerify Enterprise Mobile Threat Defense with Intune
description: How to set up iVerify Enterprise Mobile Security with Microsoft Intune to control mobile device access to your corporate resources.
author: brenduns
ms.author: brenduns
ms.date: 12/02/2025
ms.topic: how-to
ms.reviewer: ilwu
ms.collection:
- M365-identity-device-management
- sub-mtd-apps
---

# Integrate iVerify Enterprise with Microsoft Intune

Complete the following steps to integrate the iVerify Enterprise platform with Intune.

> [!NOTE]
> This Mobile Threat Defense vendor is not supported for unenrolled devices.

## Before you begin

Before starting the process of integrating iVerify Enterprise with Intune, make sure you have the following configurations:

- **Microsoft Intune Plan 1 subscription**
- **Microsoft Entra admin credentials** to grant the following permissions:
  - Sign in and read user profile
  - Access the directory as the signed-in user
  - Read directory data
  - Send device information to Intune
- **Admin credentials** to access the iVerify Admin Console

## iVerify Enterprise app authorization

The iVerify Enterprise app authorization process consists of the following steps:

1. Sign in to the **iVerify Enterprise Admin Console**.
2. Navigate to **Integrations** and select **Microsoft Intune Mobile Threat Defense**.
3. When prompted, choose **Accept** to authorize the iVerify MTD app to communicate with Intune and Microsoft Entra ID.
4. Once authorization is complete, configure device policies within the **iVerify Enterprise Admin Console** to define and manage device threat levels across your fleet.

## To set up iVerify Enterprise integration

For step-by-step setup guidance, see [Connecting iVerify Enterprise with Microsoft Intune](https://edr.iverify.io/docs/iverify-portal-guide/Integrations/intune-mtd) in the iVerify documentation.

> [!NOTE]
> You’ll need to sign in with your iVerify Admin Console credentials to view the documentation.


## Related content

- [Mobile Threat Defense with Microsoft Intune](mobile-threat-defense.md)
- [Enable mobile threat connectors in Intune](mtd-connector-enable.md)
