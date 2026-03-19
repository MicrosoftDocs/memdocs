---
title: Deploy and Configure Microsoft Defender for Endpoint on Android Using Microsoft Intune
description: Learn how to deploy and configure Microsoft Defender for Endpoint on Android devices using Microsoft Intune, including app configuration policies, always-on VPN, and low-touch onboarding.
ms.date: 03/19/2026
ms.topic: how-to
ms.reviewer: aanavath
ms.collection:
- M365-identity-device-management
- sub-secure-endpoints
---

# Deploy and Configure Microsoft Defender for Endpoint on Android Using Microsoft Intune

Use Microsoft Intune to deploy and configure Microsoft Defender for Endpoint on Android devices. This article covers app acquisition from Managed Google Play, app assignment and verification, app configuration policies, always-on VPN setup, and low-touch onboarding.

> [!NOTE]
> **Defender for Endpoint on Android is available on [Google Play](https://play.google.com/store/apps/details?id=com.microsoft.scmx).** Updates to the app are automatic via Google Play.

[!INCLUDE [android_device_administrator_support](../includes/android-device-administrator-support.md)]

## Prerequisites

- The device must be enrolled in Microsoft Intune using one of the following Android Enterprise enrollment types:
  - Personally-owned devices with a work profile
  - Corporate-owned devices with a work profile
  - Corporate-owned, fully managed user device enrollment

- The Microsoft Intune service-to-service connection with Microsoft Defender for Endpoint must be enabled. For more information, see [Configure Microsoft Defender for Endpoint with Intune and Onboard Devices](../protect/microsoft-defender-integrate.md).

## Deploy Microsoft Defender for Endpoint on Android

### Add the app from Managed Google Play

To add the Microsoft Defender for Endpoint app to your Managed Google Play store and make it available in Intune:

1. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Apps** > **Android Apps** > **Add** and select **Managed Google Play app**.

   :::image type="content" source="./media/apps-defender-android/579ff59f31f599414cedf63051628b2e.png" alt-text="Screenshot that shows the application-adding pane in the Microsoft Intune admin center portal." lightbox="./media/apps-defender-android/579ff59f31f599414cedf63051628b2e.png":::

2. On the Managed Google Play page, search for `Microsoft Defender`. Select **Microsoft Defender for Endpoint** from the search results.

   :::image type="content" source="./media/apps-defender-android/0f79cb37900b57c3e2bb0effad1c19cb.png" alt-text="Screenshot that shows the Managed Google Play page in the Microsoft Intune admin center portal." lightbox="./media/apps-defender-android/0f79cb37900b57c3e2bb0effad1c19cb.png":::

3. On the **App description** page, review the app details. Select **Select** to select the app, and then select **Sync** to sync the app with Intune.

   :::image type="content" source="./media/apps-defender-android/app-description-page.png" alt-text="Screenshot of the Microsoft Defender app page in the store." lightbox="./media/apps-defender-android/app-description-page.png":::

   The sync completes in a few minutes.

4. Select **Refresh** in the Android apps screen. Microsoft Defender for Endpoint should now appear in the apps list.

   :::image type="content" source="./media/apps-defender-android/fa4ac18a6333335db3775630b8e6b353.png" alt-text="Screenshot showing the Microsoft Defender for Endpoint app in the apps list." lightbox="./media/apps-defender-android/fa4ac18a6333335db3775630b8e6b353.png":::

### Assign the app

Assign the app as a required app so it installs automatically in the work profile during the next device sync through the Company Portal app.

1. Select **Microsoft Defender** from the apps list, and then go to **Properties** > **Assignments** > **Edit**.

   :::image type="content" source="./media/apps-defender-android/mda-properties.png" alt-text="Screenshot showing the Edit option on the Properties page." lightbox="./media/apps-defender-android/mda-properties.png":::

2. In the **Required** section, select **Add group**, select the appropriate user or device group, and then choose **Select**.

   :::image type="content" source="./media/apps-defender-android/ea06643280075f16265a596fb9a96042.png" alt-text="Screenshot showing the Edit application page." lightbox="./media/apps-defender-android/ea06643280075f16265a596fb9a96042.png":::

3. Select **Review + Save**, and then select **Save** to commit the assignment.

### Verify deployment

After the assignment is saved, confirm the installation status before proceeding with configuration.

1. Select **Microsoft Defender** from the apps list, and then select **Device install status**.

   :::image type="content" source="./media/apps-defender-android/900c0197aa59f9b7abd762ab2b32e80c.png" alt-text="Screenshot showing the Device install status pane." lightbox="./media/apps-defender-android/900c0197aa59f9b7abd762ab2b32e80c.png":::

2. Confirm that target devices show a successful installation state before continuing.

## Configure Microsoft Defender for Endpoint on Android

After deploying the app, use the following procedures to configure Microsoft Defender for Endpoint on Android devices.

### Configure app configuration policies

Defender for Endpoint supports app configuration policies for managed devices using Microsoft Intune. Use app configuration policies to select feature configurations and grant application permissions for Defender for Endpoint.

1. In the **Apps** page, go to **Policy** > **App configuration policies** > **Add** > **Managed devices**.

   :::image type="content" source="./media/apps-defender-android/android-mem.png" alt-text="The App configuration policies pane in the Microsoft Intune admin center portal" lightbox="./media/apps-defender-android/android-mem.png":::

2. In the **Create app configuration policy** page, specify the following details:

   - Name: **Microsoft Defender for Endpoint**.
   - Choose **Android Enterprise** as platform.
   - Choose **Personally-owned Work Profile only** or **Fully Managed, Dedicated, and Corporate-owned work profile only** as Profile Type.
   - Select **Select App**, choose **Microsoft Defender**, select **OK** and then **Next**.

     :::image type="content" source="./media/apps-defender-android/android-create-app.png" alt-text="Screenshot of the Associated app details pane." lightbox="./media/apps-defender-android/android-create-app.png":::

3. Select **Permissions** \> **Add**. From the list, select the available app permissions \> **OK**.

4. Select an option for each permission to grant with this policy:

   - **Prompt** - Prompts the user to accept or deny.
   - **Auto grant** - Automatically approves without notifying the user.
   - **Auto deny** - Automatically denies without notifying the user.

5. Go to the **Configuration settings** section, and then choose **Use configuration designer**.

   :::image type="content" source="./media/apps-defender-android/configurationformat.png" alt-text="Image of android create app configuration policy." lightbox="./media/apps-defender-android/configurationformat.png":::

6. Select **Add** to view a list of supported configurations. Select the required configuration, and then select **Ok**.

   :::image type="content" source="./media/apps-defender-android/selectconfigurations.png" alt-text="Image of selecting configuration policies for android." lightbox="./media/apps-defender-android/selectconfigurations.png":::

7. You should see all the selected configurations listed. You can change the configuration value as required and then select **Next**.

   :::image type="content" source="./media/apps-defender-android/listedconfigurations.png" alt-text="Image of selected configuration policies." lightbox="./media/apps-defender-android/listedconfigurations.png":::

8. In the **Assignments** page, select the user group to which this app config policy would be assigned. Select **Select groups to include**, select a group, and then select **Next**. The group selected here is usually the same group to which you assign the Microsoft Defender for Endpoint Android app.

   :::image type="content" source="./media/apps-defender-android/android-select-group.png" alt-text="The Selected groups pane" lightbox="./media/apps-defender-android/android-select-group.png":::

9. In the **Review + Create** page that comes up next, review all the information, and then select **Create**.

   The app configuration policy for Defender for Endpoint is now assigned to the selected user group.

### Set up always-on VPN

Defender for Endpoint supports device configuration policies for managed devices with Microsoft Intune. Use a device configuration profile to set up always-on VPN on Android Enterprise enrolled devices, so users don't need to manually configure a VPN service during onboarding.

1. On **Devices**, select **Configuration Profiles** \> **Create Profile** \> **Platform** \> **Android Enterprise**. Select **Device restrictions** under one of the following, based on your device enrollment type:

   - **Fully Managed, Dedicated, and Corporate-Owned Work Profile**
   - **Personally owned Work Profile**

   Then, select **Create**.

   :::image type="content" source="./media/apps-defender-android/1autosetupofvpn.png" alt-text="The Configuration profiles menu item in the Policy pane" lightbox="./media/apps-defender-android/1autosetupofvpn.png":::

2. In **Configuration Settings**, provide a **Name** and a **Description** to uniquely identify the configuration profile.

   :::image type="content" source="./media/apps-defender-android/2autosetupofvpn.png" alt-text="The devices configuration profile Name and Description fields in the Basics pane" lightbox="./media/apps-defender-android/2autosetupofvpn.png":::

3. Select **Connectivity**, and then configure your VPN:

   1. Enable **Always-on VPN**. Set up a VPN client in the work profile to automatically connect and reconnect to the VPN whenever possible. Only one VPN client can be configured for always-on VPN on a given device, so make sure no more than one always-on VPN policy is deployed to a single device.

   2. In the **VPN client** list, select **Custom**. In this case, the custom VPN is the Defender for Endpoint VPN, which provides Web Protection.

      > [!NOTE]
      > The Microsoft Defender for Endpoint app must be installed on the user's device for automatic VPN setup to occur.

   3. Specify the **Package ID** of the Microsoft Defender for Endpoint app in Google Play store. For the [Microsoft Defender app URL](https://play.google.com/store/apps/details?id=com.microsoft.scmx), the package ID is `com.microsoft.scmx`.

   4. Set **Lockdown mode** to **Not configured (Default)**.

      :::image type="content" source="./media/apps-defender-android/3autosetupofvpn.png" alt-text="The Connectivity pane under the Configuration settings tab" lightbox="./media/apps-defender-android/3autosetupofvpn.png":::

4. In the **Assignments** page, select the user group to which this device configuration profile would be assigned. Choose **Select groups** to include, select the applicable group, and then select **Next**.

   The group to select is typically the same group to which you assign the Microsoft Defender for Endpoint Android app.

   :::image type="content" source="./media/apps-defender-android/4autosetupofvpn.png" alt-text="Screenshot of the devices configuration profile Assignment pane in the Device restrictions." lightbox="./media/apps-defender-android/4autosetupofvpn.png":::

5. In the **Review + Create** page that comes up next, review all the information and then select **Create**.

   :::image type="content" source="./media/apps-defender-android/5autosetupofvpn.png" alt-text="A devices configuration profile's provision for Review + create" lightbox="./media/apps-defender-android/5autosetupofvpn.png":::

### Configure low-touch onboarding

> [!NOTE]
> Android low-touch onboarding is generally available.

In low-touch onboarding mode, users need to provide only a reduced set of permissions to complete onboarding. Android low-touch onboarding is disabled by default. To enable it, create an app configuration policy in Intune by following these steps:

1. Verify that the Microsoft Defender app is deployed to the target user groups. See [Add the app from Managed Google Play](#add-the-app-from-managed-google-play) if needed.

2. Push a VPN profile to users' devices by following the steps in [Set up always-on VPN](#set-up-always-on-vpn).

3. In **Apps** > **Application configuration policies**, select **Managed Devices**.

4. Provide a name to uniquely identify the policy:

   - For **Platform**, select `Android Enterprise`.
   - Select the required profile type.
   - For the targeted app, select `Microsoft Defender: Antivirus`.

   Then select **Next**.

5. Add runtime permissions. Select **Location access (fine)**, **POST_NOTIFICATIONS** and change the **Permission state** to `Auto grant`. (This permission isn't supported for Android 13 and later.)

6. Under **Configuration settings**, select `Use Configuration designer`, and then select **Add**.

7. Select **Low touch onboarding and User UPN**. For User UPN, change the value type to `Variable`, and set the configuration value to `User Principal Name`. Enable low-touch onboarding by changing its configuration value to `1`.

   After the policy is created, these value types show up as string values.

8. Assign the policy to the target user group.

9. Review and create the policy.

## Complete device onboarding

After policies are pushed to devices, users complete onboarding from the device.

1. On the device, validate the onboarding status by going to the work profile. Confirm that Defender for Endpoint is available, and that you're enrolled using **Personally owned devices with work profile**. If you're enrolled using a **Corporate-owned, fully managed user device**, you have a single profile on the device where you can confirm that Defender for Endpoint is available.

   :::image type="content" source="./media/apps-defender-android/c2e647fc8fa31c4f2349c76f2497bc0e.png" alt-text="The application display pane" lightbox="./media/apps-defender-android/c2e647fc8fa31c4f2349c76f2497bc0e.png":::

2. When the app is installed, open the app, and then accept the permissions. Onboarding should successfully complete.

   :::image type="content" source="./media/apps-defender-android/MDE-new.png" alt-text="The display of a Microsoft Defender for Endpoint application on a mobile device" lightbox="./media/apps-defender-android/MDE-new.png":::

3. Verify onboarding status in the [Microsoft Defender portal](https://security.microsoft.com). Navigate to the **Device inventory** page.

   :::image type="content" source="./media/apps-defender-android/9fe378a1dce0f143005c3aa53d8c4f51.png" alt-text="The Microsoft Defender for Endpoint portal" lightbox="./media/apps-defender-android/9fe378a1dce0f143005c3aa53d8c4f51.png":::

## Next steps

- [Configure Microsoft Defender for Endpoint web protection settings for Android](../protect/microsoft-defender-configure-android.md) — Manage web protection settings from Intune by enrollment type.
- [Configure Microsoft Defender for Endpoint on Android features](/defender-endpoint/android-configure) — Configure privacy controls and other Android-specific Defender features.
