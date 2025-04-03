---
# required metadata

title: Get app bundle ID
description: Get the app bundle ID in Microsoft Intune for Android, iOS/iPadOS, macOS, and Windows apps. Use the bundle ID in your app policies, device configuration profiles, enrollment policies, and compliance policies in Microsoft Intune.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 04/30/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: medium
ms.assetid:

# optional metadata

#ROBOTS:
#audience:

ms.reviewer:
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
---

# Get the app bundle ID for your policies in Microsoft Intune

When you add an app to Intune or use the built-in apps, the bundle ID of the app is also added. This bundle ID identifies the app, and you can use the bundle ID in your policies.

For example, you can use the bundle ID in an Intune device configuration profile to allow or block specific apps.

Applies to:

- Android
- iOS/iPadOS
- macOS
- Windows

This article lists the steps to get the app bundle IDs using the Intune admin center.

## Get the app bundle ID

1. Sign into the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
1. Select **Apps** > **All Apps**.
1. Select **Columns**.

    :::image type="content" source="./media/get-app-bundle-id-intune-admin-center/all-apps-column.png" alt-text="Screenshot that shows how to select the Columns option in All Apps in Microsoft Intune and the Intune admin center.":::

1. In the list, select **App identifier** > **Apply**.

    :::image type="content" source="./media/get-app-bundle-id-intune-admin-center/columns-select-app-identifier.png" alt-text="Screenshot that shows how to select the App Bundle ID column in All Apps in Microsoft Intune and the Intune admin center.":::

1. The **App identifier** column shows the bundle ID of the app.

## Related articles

- [Add apps to Microsoft Intune](../apps/apps-add.md)
- [Bundle IDs for built-in iOS and iPadOS apps you can use in Intune](../configuration/bundle-ids-built-in-ios-apps.md)
- [Add built-in apps to Microsoft Intune](../apps/apps-add-built-in.md)
