---
# required metadata

title: Set permissions to Managed Home Screen using Android Enterprise OEMConfig
description: Add the Samsung Knox Service Plugin, Zebra OEMConfig Powered by MX, and Legacy Zebra OEMConfig apps to Intune, and use the app schemas to configure permissions for the Managed Home Screen (MHS) app on Android Enterprise devices.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/07/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: abigailstein
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
---

# Configure permissions for the Managed Home Screen (MHS) on Android Enterprise devices

The Managed Home Screen (MHS) is an Intune feature that allows you to configure the home screen on the device. It's designed to only show the apps that your users access and the device settings that admins need to manage.

The MHS is typically used for kiosk devices, including frontline worker (FLW) devices. It replaces the default launcher on your Android dedicated devices. For more information on the MHS, go to [Configure the Microsoft MHS app for Android Enterprise](../apps/app-configuration-managed-home-screen-app.md).

Typically, when you configure the MHS on a device, end users need to manually accept the permissions that MHS needs. These permissions allow the MHS to access device features and settings.

Instead of relying on end users to accept the permissions, you can use [OEMConfig device configuration policy](android-oem-configuration-overview.md) to automatically grant permissions to the MHS app.

This feature applies to:

- Android Enterprise
- Samsung
- Zebra

This article lists the steps to create an OEMConfig policy that automatically grants permissions for the MHS app on Samsung and Zebra devices.

## Required permissions

For the MHS to work, certain permissions are required for certain functionalities. Samsung and Zebra have auto-grant permissions for devices using OEMConfig. The following Managed Home Screen permissions are offered for Samsung and Zebra.

The following table lists the permissions that you can configure for the MHS app on Samsung and Zebra devices:

| Permission  | Samsung | Zebra | Legacy Zebra |
|---|---|---|---|
| **Overlay Permission** includes: <br/><br/>- Virtual home button<br/>- Screen saver <br/>- Automatic sign out | ✅ | ✅ | ✅ |
| **Notification Permission** includes:<br/><br/>- Notification badge| ✅ | ✅ | ❌ |
| **Alarms & Reminders** permission includes: <br/><br/>- Screen saver<br/>- Automatic sign out<br/>- Automatic re-launch   | ✅ | ❌ | ? |
| **Write Settings** permission includes: <br/><br/>- Brightness toggle<br/>- Rotation toggle | ✅ | ❌ | ? |

## Before you begin

- This article creates OEMConfig configuration profile in Intune. Before you create OEMConfig profiles, review the [OEMConfig profiles in Microsoft Intune - Before you begin](android-oem-configuration-overview.md#before-you-begin) section for important information, as there's a 500-KB file size limit and other important information.
- Devices must be MDM enrolled in Intune.
- To configure this policy, at a minimum, sign into the Intune admin center with the **Policy and Profile manager** role. For more information on the built-in roles in Intune, go to [Role-based access control with Microsoft Intune](../fundamentals/role-based-access-control.md).

## Step 1 - Get the app from the Managed Google Play Store

OEMs provide their own OEMConfig app that lets you configure features within the app. In this step, you:

✅ Get the OEMConfig app from the Managed Google Play Store.

✅ Assign the app to your devices or device groups that use the MHS.

Samsung and Zebra OEMs use the following Managed Google Play apps:

| OEM | App name |
|---|---|
| Samsung | Knox Service Plugin |
| Zebra | Zebra OEMConfig Powered by MX <br/><br/>Zebra OEMConfig Powered by MX is a new version of the OEMConfig app released in May 2023.|
| Zebra | Legacy Zebra OEMConfig |

# [Samsung](#tab/samsung-app)

1. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), sign in to your **Managed Google Play account**.
2. Search for the **Knox Service Plugin** app, select the app, and then select **Sync**.

    For the specific steps, go to [Add Managed Google Play apps to Android Enterprise devices with Intune](../apps/apps-add-android-for-work.md).

3. In the **Knox Service Plugin** app properties, make it a required app, and assign the app to your devices or device groups that use the MHS.

    For the specific steps, go to [Add Managed Google Play apps to Android Enterprise devices with Intune](../apps/apps-deploy.md#assign-an-app).

# [Zebra](#tab/zebra-mx-app)

1. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), sign in to your **Managed Google Play account**.
2. Search for the **Zebra OEMConfig Powered by MX** app, select the app, and then select **Sync**.

    For the specific steps, go to [Add Managed Google Play apps to Android Enterprise devices with Intune](../apps/apps-add-android-for-work.md).

3. In the **Zebra OEMConfig Powered by MX** app properties, make it a required app, and assign the app to your devices or device groups that use the MHS.

    For the specific steps, go to [Add Managed Google Play apps to Android Enterprise devices with Intune](../apps/apps-deploy.md#assign-an-app).

# [Zebra Legacy](#tab/zebra-legacy-app)

1. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), sign in to your **Managed Google Play account**.
2. Search for the **Legacy Zebra OEMConfig** app, select the app, and then select **Sync**.

    For the specific steps, go to [Add Managed Google Play apps to Android Enterprise devices with Intune](../apps/apps-add-android-for-work.md).

3. Optional. Install [Remote Help](../fundamentals/remote-help-android.md) on the device.

    When you use Legacy Zebra OEMConfig, OEMConfig profiles are applied as one-off actions, not persistent policy states.

    So, if you use Remote Help, then deploy the Remote Help app on the device first, and then assign the OEMConfig configuration policy. If you uninstall and reinstall the Remote Help app on the device, after the Remote Help app is reinstalled, then re-apply this OEMConfig policy. You can create a new OEMConfig profile and assign it to the device, or edit the previously created OEMConfig profile.

    ??Does this apply to any other apps or policies? Or, does it only apply to Remote Help??

4. In the **Legacy Zebra OEMConfig** app properties, make it a required app, and assign the app to your devices or device groups that use the MHS.

    For the specific steps, go to [Add Managed Google Play apps to Android Enterprise devices with Intune](../apps/apps-deploy.md#assign-an-app).

## Step 2 - Create the OEMConfig profile that configures the app

The next step is to create an OEMConfig profile that configures the permissions in the OEMConfig app. In this profile, you configure the app schema settings that auto-grant permissions to the MHS app features.

# [Samsung](#tab/samsung-policy)

This profile grants the **Overlay Permission**, **Notification Permission**, and **Alarms & Reminders Permission** using the schema settings in the **Knox Service Plugin** app.

1. Sign in to the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Devices** > **Configuration** > **Create** > **New policy**.
3. Enter the following properties:

    - **Platform**: Select **Android Enterprise**.
    - **Profile type**: Select **OEMConfig**.

4. Select **Create**.
5. In **Basics**, enter the following properties:

    - **Name**: Enter a descriptive name for the new profile.
    - **Description**: Enter a description for the profile. This setting is optional, but recommended.
    - **OEMConfig app**: Choose **Select an OEMConfig app**.
    - **Associated app**: Select the **Knox Service Plugin** app.

6. Select **Next**.
7. In **Configuration settings**, select the **Configuration designer**. The properties available within the app schema are shown for you to configure.

8. Select the **Device-wide policies (Selectively applicable to Fully Manage Device (DO) or Work Profile-on company owned devices (WP-C) mode as noted)** setting.

    Select **Configure** and configure the following settings:

    - **Enable device policy controls**: Select **true**.
    - **Application management policies**: Select **Configure** and configure the following settings:

      - **Enable application management controls**: Select **true**.
      - **Enable permission controls**: Select **true**.

9. Select the **Knox Service Plugin** top node:

    :::image type="content" source="./media/oemconfig-managed-home-screen-permissions-android/knox-service-plugin-top-node.png" alt-text="Screenshot that shows how to select the top node in the Knox Service Plugin app schema in an OEMConfig device configuration policy in Microsoft Intune." lightbox="./media/oemconfig-managed-home-screen-permissions-android/knox-service-plugin-top-node.png":::

    1. Select the **Permission Controls** node > **Configure**. Scroll up to see this node in the **Settings** list:

        :::image type="content" source="./media/oemconfig-managed-home-screen-permissions-android/knox-service-plugin-permission-controls-node.png" alt-text="Screenshot that shows how to configure the Permission Controls node in the Knox Service Plugin app schema in an OEMConfig device configuration policy in Microsoft Intune." lightbox="./media/oemconfig-managed-home-screen-permissions-android/knox-service-plugin-permission-controls-node.png":::

    2. Select the **Permission Controls** ellipsis > **Add Setting**. Do this step twice to add two child nodes.

        :::image type="content" source="./media/oemconfig-managed-home-screen-permissions-android/knox-service-plugin-add-settings.png" alt-text="Screenshot that shows how to add a setting to the Permission Controls node in the Knox Service Plugin app schema in an OEMConfig device configuration policy in Microsoft Intune." lightbox="./media/oemconfig-managed-home-screen-permissions-android/knox-service-plugin-add-settings.png":::

    3. Select the first child node and configure the following settings:

        - **Permission Policy**: Select **Appear on top** and **Alarms & Reminders**.
        - **Package or Component Name**: Enter the MHS package name: `com.microsoft.launcher.enterprise`.

    4. Select the second child node and configure the following settings:

        - **Permission Policy**: Select **Notification access**.
        - **Package or Component Name**: Enter the MHS notification service package name: `com.microsoft.launcher.enterprise/com.microsoft.launcher.next.model.notification.AppNotificationService`.

    When complete, your **Settings** list should look like the following list. You can select any node to see the settings you configured:

    :::image type="content" source="./media/oemconfig-managed-home-screen-permissions-android/knox-service-plugin-all-configured-nodes.png" alt-text="Screenshot that shows all the nodes you configured in the Knox Service Plugin app schema in an OEMConfig device configuration policy in Microsoft Intune.":::

10. Select **Next**, add any [optional scope tags](../fundamentals/scope-tags.md) > **Next**.

11. In **Assignments**, select the devices or device groups that will receive your profile. Assign one profile to each device. The OEMConfig model only supports one policy per device.

    For more information on assigning profiles, go to [Assign user and device profiles](device-profile-assign.md).

12. Select **Next**, and review your settings. When you select **Create**, your changes are saved, and the profile is assigned. The policy is also shown in the profiles list.

The next time the device checks for configuration updates, the settings you configured are applied to the app.

# [Zebra OEMConfig Powered by MX](#tab/zebra-mx-policy)

This profile grants the **Overlay Permission** and **Notification Permission** using the schema settings in the **Zebra OEMConfig Powered by MX** app.

For more information on these permissions, go to:

- [Enable Notification Access Permission via MDM/EMM OEMConfig 11.9.x.x and Up](https://supportcommunity.zebra.com/s/article/000027795) (opens Zebra's web site)
- [Enabling Display Over Other Apps Permission via MDM/EMM OEMConfig](https://supportcommunity.zebra.com/s/article/000021297) (opens Zebra's web site)

> [!NOTE]
> On Android 11, the **Zebra OEMConfig Powered by MX** app schema doesn't work if the board support package (BSP) version is `HE_FULL_UPDATE_11-20-18.00-RG-U00-STD-HEL-04`. To use the Zebra OEMConfig powered by MX app, you must upgrade to a newer BSP.
>
> For more information on updating Zebra devices with Intune, go to [Zebra LifeGuard Over-the-Air Integration with Microsoft Intune](../protect/zebra-lifeguard-ota-integration.md).

1. Sign in to the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Devices** > **Configuration** > **Create** > **New policy**.
3. Enter the following properties:

    - **Platform**: Select **Android Enterprise**.
    - **Profile type**: Select **OEMConfig**.

4. Select **Create**.
5. In **Basics**, enter the following properties:

    - **Name**: Enter a descriptive name for the new profile.
    - **Description**: Enter a description for the profile. This setting is optional, but recommended.
    - **OEMConfig app**: Choose **Select an OEMConfig app**.
    - **Associated app**: Select the **Zebra OEMConfig Powered by MX** app.

6. Select **Next**.
7. In **Configuration settings**, select the **Configuration designer**. The properties available within the app schema are shown for you to configure.

8. Select the **Package Configuration** node > **Configure**. This node is added to the **Settings** list:

    :::image type="content" source="./media/oemconfig-managed-home-screen-permissions-android/zebra-mx-package-configuration-node.png" alt-text="Screenshot that shows how to configure the Package Configuration node in the Zebra OEMConfig Powered by MX app schema in a device configuration policy in Microsoft Intune." lightbox="./media/oemconfig-managed-home-screen-permissions-android/zebra-mx-package-configuration-node.png":::

    1. Select the **Package Configuration** ellipsis > **Add Setting**.

        :::image type="content" source="./media/oemconfig-managed-home-screen-permissions-android/zebra-mx-add-setting.png" alt-text="Screenshot that shows how to add a setting to the Package Configuration node in the Zebra OEMConfig Powered by MX app schema in a device configuration policy in Microsoft Intune." lightbox="./media/oemconfig-managed-home-screen-permissions-android/zebra-mx-add-setting.png":::

    2. Select the new **Package** child node and configure the following settings:

        - **Package name**: Enter `com.microsoft.launcher.enterprise`.
        - **Package Signing Certificate**: Enter `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`.

    3. Select **Permissions** > **Configure**:

        :::image type="content" source="./media/oemconfig-managed-home-screen-permissions-android/zebra-mx-permissions-node.png" alt-text="Screenshot that shows how to select the Permissions node and configure the settings in the Zebra OEMConfig Powered by MX app schema in an OEMConfig device configuration policy in Microsoft Intune." lightbox="./media/oemconfig-managed-home-screen-permissions-android/zebra-mx-permissions-node.png":::

    4. The **Permissions** child node is added to the **Settings** list. Select the ellipsis > **Add setting**. Do this step twice to add two child nodes.

        :::image type="content" source="./media/oemconfig-managed-home-screen-permissions-android/zebra-mx-permissions-node-add-setting.png" alt-text="Screenshot that shows how to add settings to the Permissions node in the Zebra OEMConfig Powered by MX app schema in an OEMConfig device configuration policy in Microsoft Intune." lightbox="./media/oemconfig-managed-home-screen-permissions-android/zebra-mx-permissions-node-add-setting.png":::

    5. Select the first child node and configure the following settings:

        - **Name**: Select **System Alert Window**.
        - **State**: Select **Grant**.

    6. Select the second child node and configure the following settings:

        - **Name**: Select **Bind Notification Listener**.
        - **State**: Select **Grant**.

    When complete, your **Settings** list should look like the following list. You can select any node to see the settings you configured:

    :::image type="content" source="./media/oemconfig-managed-home-screen-permissions-android/zebra-mx-all-configured-nodes.png" alt-text="Screenshot that shows all the nodes you configured in the Zebra OEMConfig Powered by MX app schema in an OEMConfig device configuration policy in Microsoft Intune.":::

9. Select **Next**, add any [optional scope tags](../fundamentals/scope-tags.md) > **Next**.

10. In **Assignments**, select the devices or device groups that will receive your profile. Assign one profile to each device. The OEMConfig model only supports one policy per device.

    For more information on assigning profiles, go to [Assign user and device profiles](device-profile-assign.md).

11. Select **Next**, and review your settings. When you select **Create**, your changes are saved, and the profile is assigned. The policy is also shown in the profiles list.

The next time the device checks for configuration updates, the settings you configured are applied to the app.

# [Legacy Zebra OEMConfig](#tab/zebra-legacy-policy)

??Which permissions does this profile grant??

This profile grants permissions using the schema settings in the **Legacy Zebra OEMConfig** app.

1. Sign in to the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Devices** > **Configuration** > **Create** > **New policy**.
3. Enter the following properties:

    - **Platform**: Select **Android Enterprise**.
    - **Profile type**: Select **OEMConfig**.

4. Select **Create**.
5. In **Basics**, enter the following properties:

    - **Name**: Enter a descriptive name for the new profile.
    - **Description**: Enter a description for the profile. This setting is optional, but recommended.
    - **OEMConfig app**: Choose **Select an OEMConfig app**.
    - **Associated app**: Select the **Legacy ZebraOEMConfig** app.

6. Select **Next**.
7. In **Configuration settings**, select the **Configuration designer**. The properties available within the app schema are shown for you to configure.

8. Select the **Transaction steps** node > **Configure**. This node is added to the **Settings** list:

    :::image type="content" source="./media/oemconfig-managed-home-screen-permissions-android/zebra-legacy-transaction-steps-node.png" alt-text="Screenshot that shows how to configure the Transaction steps node in the Legacy Zebra OEMConfig app schema in a device configuration policy in Microsoft Intune." lightbox="./media/oemconfig-managed-home-screen-permissions-android/zebra-legacy-transaction-steps-node.png":::

    1. Select the **Transaction steps** ellipsis > **Add Setting**:

        :::image type="content" source="./media/oemconfig-managed-home-screen-permissions-android/zebra-legacy-add-setting.png" alt-text="Screenshot that shows how to add a setting to the Transaction Steps node in the Legacy Zebra OEMConfig app schema in a device configuration policy in Microsoft Intune." lightbox="./media/oemconfig-managed-home-screen-permissions-android/zebra-legacy-add-setting.png":::

    2. Select the new **Transaction Step** child node > **Permission Access Configuration** > **Configure**:

        :::image type="content" source="./media/oemconfig-managed-home-screen-permissions-android/zebra-legacy-permission-access-configuration.png" alt-text="Screenshot that shows how to configure the Permission Access Configuration node in the Legacy Zebra OEMConfig app schema in a device configuration policy in Microsoft Intune.":::

    3. Configure the following settings:

        - **Permission Access Action**: Select **Grant**.
        - **Grant Permission**: Select **System Alert Window**.
        - **Grant Application Package**: Enter `com.microsoft.launcher.enterprise`.
        - **Grant Application Signature**: Enter `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`.

    4. Select the **Transaction Steps** node > Select the ellipsis > **Add setting**:

        :::image type="content" source="./media/oemconfig-managed-home-screen-permissions-android/zebra-legacy-transaction-steps-node-add-setting.png" alt-text="Screenshot that shows how to add another setting to the Transaction Steps node in the Legacy Zebra OEMConfig app schema in a device configuration policy in Microsoft Intune." lightbox="./media/oemconfig-managed-home-screen-permissions-android/zebra-legacy-transaction-steps-node-add-setting.png":::

    5. Select the new **Transaction Step** child node > **Permission Access Configuration** > **Configure**.

        Configure the following settings:

        - **Permission Access Action**: Select **Grant**.
        - **Grant Permission**: Select **Bind Notification Listener**.
        - **Grant Application Package**: Enter `com.microsoft.launcher.enterprise`.
        - **Grant Application Signature**: Under **Package Signing Certificate**, enter: `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`.

    When complete, your **Settings** list should look like the following list. You can select any node to see the settings you configured:

    :::image type="content" source="./media/oemconfig-managed-home-screen-permissions-android/zebra-legacy-all-configured-nodes.png" alt-text="Screenshot that shows all the nodes you configured in the Legacy Zebra OEMConfig app schema in an OEMConfig device configuration policy in Microsoft Intune.":::

9. Select **Next**, add any [optional scope tags](../fundamentals/scope-tags.md) > **Next**.

10. In **Assignments**, select the devices or device groups that will receive your profile. Assign one profile to each device. The OEMConfig model only supports one policy per device.

    For more information on assigning profiles, go to [Assign user and device profiles](device-profile-assign.md).

11. Select **Next**, and review your settings. When you select **Create**, your changes are saved, and the profile is assigned. The policy is also shown in the profiles list.

The next time the device checks for configuration updates, the settings you configured are applied to the app.

## Related articles

- [Use and manage Android Enterprise devices with OEMConfig in Microsoft Intune](android-oem-configuration-overview.md)
