---
title: iVerify Enterprise Mobile Threat Defense with Intune
description: Set up iVerify Enterprise Mobile Security with Microsoft Intune to control mobile device access to your corporate resources.
author: brenduns
ms.author: brenduns
ms.date: 11/10/2025
ms.topic: how-to
ms.reviewer: ilwu
ms.collection:
- M365-identity-device-management
- sub-mtd-apps
---

# Set up iVerify Mobile Threat Defense Connector

Microsoft Intune supports use of iVerify as a Mobile Threat Defense solution. When integrated with Intune, iVerify is supported for enrolled devices using device compliance and telemetry collected from devices that run the iVerify app.

This article details basic information for using iVerify integration with Intune. For step-by-step guidance to set up and integrate iVerify with Intune, see  the iVerify documentation at [Connecting iVerify Enterprise with Microsoft Intune](https://edr.iverify.io/docs/iverify-portal-guide/Integrations/intune-mtd). To access iVerify content, you must sign in to your iVerify subscription.

## Supported platforms

Use iVerify Enterprise with the following platforms and version:

- Android 9.0 and later
- iOS/iPadOS 15.0 and later 

## Prerequisites

- Microsoft Intune Plan 1 subscription
- Microsoft Entra admin credentials to grant the following permissions:
  - Sign in and read user profile
  - Access the directory as the signed-in user
  - Read directory data
  - Send device information to Intune
- Admin credentials to access the iVerify Admin Console console.

## Get the iVerify Enterprise app

You can download th *iVerify Enterprise* app from the Android and Apple app stores:

- [Apple Store](https://apps.apple.com/us/app/iverify-enterprise/id6677005195)
- [Google Play](https://play.google.com/store/apps/details?id=com.trailofbits.iverify.orgs&utm_source=na_Med)

## Authorize the iVerify Enterprise app

Use the following guidance to authorize the **iVerify Enterprise** app:

1. Sign in to the iVerify Enterprise Admin Console.
2. Navigate to **Integrations** and select **Microsoft Intune Mobile Threat Defense**.
3. When prompted, select **Accept** to authorize the iVerify Mobile Threat Defense app to communicate with Intune and Microsoft Entra ID.
4. When authorization is complete, you can configure device policies within the iVerify Enterprise Admin Console to define and manage device threat levels across your fleet.

## Set up iVerify Enterprise integration

For step-by-step setup guidance, see [Connecting iVerify Enterprise with Microsoft Intune](https://edr.iverify.io/docs/iverify-portal-guide/Integrations/intune-mtd) in the iVerify documentation. To access this content, sign in to your iVerify subscription.

## Related content

- [Create device compliance policy for Mobile Threat Protection](mtd-device-compliance-policy-create.md)
- [Enable mobile threat connectors in Intune](mtd-connector-enable.md)
- [Create an Mobile Threat Protection app protection policy](../protect/mtd-app-protection-policy.md)
