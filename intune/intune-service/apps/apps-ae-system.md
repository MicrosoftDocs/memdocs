---
title: Manage Android Enterprise System Apps in Microsoft Intune
description: Learn how to manage Android Enterprise system apps in Microsoft Intune.
ms.date: 08/18/2025
ms.topic: how-to
ms.reviewer: priyar
ms.collection:
- M365-identity-device-management
- Android
- FocusArea_Apps_Add
---

# Manage Android Enterprise system apps in Microsoft Intune

Before you assign an Android Enterprise system app to a device, you must first enable the app in Microsoft Intune. System apps are supported on Android Enterprise devices. You can enable a system app for [Android Enterprise dedicated devices](../enrollment/android-kiosk-enroll.md), [fully managed devices](../enrollment/android-fully-managed-enroll.md), [Android Enterprise corporate-owned with work profile](../enrollment/android-corporate-owned-work-profile-enroll.md), or [Android Enterprise personally owned work profiles](../apps/android-deployment-scenarios-app-protection-work-profiles.md). When you no longer need the system app, you can disable it. Android Enterprise system apps will enable or disable apps that are already part of the platform. To enable an app, assign the system app as **Required**. To disable an app, assign the system app as **Uninstall**. System apps can't be assigned as available for a user.

## Enable a system app in Intune

You can enable an Android Enterprise system app in Intune using the following steps:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Apps** > **All Apps** > **Create**.
3. In the **Select app type** pane, under the available **Other** types, select **Android Enterprise system app**.
4. Click **Select**. The **Add app** steps are displayed.
In the **App information** page, add the app details:
    - **App Name**: Enter the name of the app.
    - **Publisher**: Enter the name of the publisher of the app.
    - **Package Name**: Enter a package name. Intune will validate that the package name is valid.
5. Click **Next** to display the **Scope tags** page.
6. Click **Select scope tags** to optionally add scope tags for the app. For more information, see [Use role-based access control (RBAC) and scope tags for distributed IT](../fundamentals/scope-tags.md).
7. Click **Next** to display the **Assignments** page.
8. Select the group assignments for the app. To enable the app, assign the app as **Required**. For more information, see [Add groups to organize users and devices](../fundamentals/groups-add.md).
9. Click **Next** to display the **Review + create** page. Review the values and settings you entered for the app.
10. When you're done, click **Create** to enable the app in Intune.

The **Overview** blade of the app you've created is displayed.

> [!NOTE]
> You'll need to work with the OEM of your device to find the package name of the app you would like to enable/disable.
>
> You can't create an Android Enterprise system app when there's the same app in Managed Google Play in Intune.
>
> The Notes section won't appear for an Android Enterprise system app and isn't editable.

The app you've created is displayed in the apps list, where you can assign it to the groups that you select.

## Disable an existing system app

You can disable an Android Enterprise system app in Intune using the following steps:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Apps** > **All Apps**.
3. Select the system app from the app list.
4. Change the assignment for the app to **Uninstalled** and save.

## Disable a new system app

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Apps** > **Android** > **Create**.
3. In **Select app type**, select **Other** > **Android Enterprise system app**.
4. Click **Select**. In **App information**, add the app details:
    - **App Name**: Enter the name of the app.
    - **Publisher**: Enter the name of the publisher of the app.
    - **Package Name**: Enter a package name, like `com.microsoft.word`. Intune validates that the package name is valid.

    For example, to disable the on-device AI experience, you can block the AICore system service by entering the following:

    - **Name**: Enter `AICore`.
    - **Publisher**: Enter `Google Android`.
    - **Package Name**: Enter `com.google.android.aicore`.

6. Select **Next**.
7. Click **Select scope tags** to optionally add scope tags for the app. For more information, see [Use role-based access control (RBAC) and scope tags for distributed IT](../fundamentals/scope-tags.md).

    Select **Next**.

8. In **Assignments** > **Uninstall**, select the group assignments for the app. When you select **Uninstall**, the app is disabled.

    For more information, see [Add groups to organize users and devices](../fundamentals/groups-add.md).
9. Select **Next**. In **Review + create**, review the values and settings you entered for the app. When you're done, select **Create** to disable the app in Intune.

## Next steps

- [Assign apps to groups](apps-deploy.md)
