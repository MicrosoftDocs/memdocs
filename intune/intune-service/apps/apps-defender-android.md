---
title: Deploy and Configure Microsoft Defender for Endpoint on Android Using Microsoft Intune
description: Learn how to deploy and configure Microsoft Defender for Endpoint on Android devices using Microsoft Intune, including app configuration policies, always-on VPN, and low-touch onboarding.
ms.date: 03/19/2026
ms.topic: how-to
ms.author: brenduns
ms.reviewer: aanavath
ai-usage: ai-assisted
ms.collection:
- M365-identity-device-management
- sub-secure-endpoints
---

# Deploy and Configure Microsoft Defender for Endpoint on Android Using Microsoft Intune

Use Microsoft Intune to deploy Microsoft Defender for Endpoint to Android devices to support onboarding those devices to the Defender for Endpoint service. On Android, onboarding is app-driven: a device is considered onboarded when the Defender app is opened and setup is complete. Intune manages the app deployment and provides configuration policies that configure Defender features and streamline the steps users need to complete during onboarding. This article covers app acquisition from Managed Google Play, app assignment and verification, app configuration policies, always-on VPN setup, and low-touch onboarding.

> [!TIP]
> You can also use Intune to deploy Defender for Endpoint to Android devices that aren't enrolled in Intune mobile device management (MDM). This includes unmanaged devices and devices enrolled with another MDM, through use of Intune mobile application management (MAM). See [Configure Microsoft Defender for Endpoint risk signals in app protection policy (MAM)](/defender-endpoint/android-configure-mam).

## Prerequisites

- **Licenses:** Users must be assigned both a Microsoft Intune license and a Microsoft Defender for Endpoint license. For licensing details, see [Microsoft Defender for Endpoint licensing requirements](/defender-endpoint/minimum-requirements#licensing-requirements).

- **Enrollment:** Devices must be enrolled in Microsoft Intune using one of the following [Android Enterprise](/intune/intune-service/enrollment/android-enterprise-overview) enrollment types:
  - Personally-owned devices with a work profile
  - Corporate-owned devices with a work profile
  - Corporate-owned, fully managed user device enrollment

   [!INCLUDE [android_device_administrator_support](../includes/android-device-administrator-support.md)]

- **Android OS version:** For supported OS versions, see [System requirements](/defender-endpoint/microsoft-defender-endpoint-android#system-requirements) for Microsoft Defender for Endpoint on Android.

- **Managed Google Play:** Your Intune tenant must be [connected to Managed Google Play](/intune/intune-service/enrollment/connect-intune-android-enterprise) before you can add and assign apps for Android Enterprise devices.

- **Intune–Defender connection:** The Microsoft Intune service-to-service connection with Microsoft Defender for Endpoint must be enabled. For more information, see [Configure Microsoft Defender for Endpoint with Intune and Onboard Devices](../protect/microsoft-defender-integrate.md).

## Deploy Microsoft Defender for Endpoint on Android

### Add the app from Managed Google Play

To add the Microsoft Defender for Endpoint app to your Managed Google Play store and make it available in Intune:

1. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Apps** (1) > **Android apps** (2) > **Create** (3) and for App type, select **Managed Google Play app** (4).

   :::image type="content" source="./media/apps-defender-android/managed-google-play-app.png" alt-text="Screenshot that shows where in the Microsoft Intune admin center portal to create a Managed Google Play app." lightbox="./media/apps-defender-android/managed-google-play-app.png":::

    1. On the *Managed Google Play* page, search for `Microsoft Defender`. Select **Microsoft Defender for Endpoint** from the search results. The store displays the app with the name *Microsoft Defender: Antivirus*.

    2. On the *App description* page, review the app details. Select **Select** to select the app, and then select **Sync** to sync the app with Intune.

       The sync completes in a few minutes.

2. After the sync completes, return to the Intune admin center on the  the Android apps screen, select**Refresh**. *Microsoft Defender: Antivirus* should now appear in the apps list.

   :::image type="content" source="./media/apps-defender-android/defender-in-app-list.png" alt-text="Screenshot showing the Microsoft Defender for Endpoint app in the apps list." lightbox="./media/apps-defender-android/defender-in-app-list.png":::

Stay on the *Android apps* page for the following procedure.

### Assign the app

Assign the app as a required app so it installs automatically in the work profile during the next device sync through the Company Portal app.

1. From the *Android apps* page of the Intune admin center, select **Microsoft Defender: Antivirus** from the apps list. Go to **Properties** (1)\ and For *Assignments*, select **Edit** (2).

   :::image type="content" source="./media/apps-defender-android/edit-app-properties.png" alt-text="Screenshot showing the Edit option on the Properties page." lightbox="./media/apps-defender-android/edit-app-properties.png":::

2. On the *Edit application* pane, go the *Required* section (1) and select **Add group** to open the *Select groups* pane.

   :::image type="content" source="./media/apps-defender-android/add-groups.png" alt-text="Screenshot showing the Select groups pane." lightbox="./media/apps-defender-android/add-groups.png":::

3. On the **Select groups** pane, select the groups you want to receive this app, and then select **Select**.

4. Back on the *Edit application* pane, select **Review + Save** from the bottom of the pane, and then **Save** to commit the assignment.

### Verify deployment

After the assignment is saved, you can confirm the installation status for targeted devices before proceeding with configuration.

1. From the *Android apps* page of the Intune admin center, select **Microsoft Defender: Antivirus** from the apps list. On the default app page, *Overview*, Intune displays chart tiles that provide a rollup of installation status.  

2. To identify if a specific device has installed the app, select **Device install status** or click on the **Device status** tile. Intune displays a list of the selected objects with additional details.


   :::image type="content" source="./media/apps-defender-android/device-status-detail.png" alt-text="Screenshot showing the Device install status pane." lightbox="./media/apps-defender-android/device-status-detail.png":::

3. Confirm that target devices show a successful installation state before continuing.

## Configure Microsoft Defender for Endpoint on Android

After deploying the app, use Intune policies to configure Microsoft Defender for Endpoint on Android devices. This involves creating an app configuration policy to grant app permissions and a device configuration profile to set up always-on VPN for web protection. You can also optionally configure low-touch onboarding to reduce the steps users need to complete. For optional feature configurations specific to Defender, such as network protection and privacy controls, see [Configure Microsoft Defender for Endpoint on Android features](/defender-endpoint/android-configure) in the Defender documentation.

### Grant app permissions

Create an app configuration policy to grant Defender the permissions it needs on the device without prompting users during onboarding.

1. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Apps** > **App configuration policies** > **Add** > **Managed devices**.

1. On the **Basics** page, specify the following details:

   - **Name**: Enter a descriptive name, such as *Microsoft Defender for Endpoint*.
   - **Platform**: **Android Enterprise**
   - **Profile type**: Select the type that matches your device enrollment:
     - **Personally-owned Work Profile only**
     - **Fully Managed, Dedicated, and Corporate-owned work profile only**
   - **Targeted app**: Select **Microsoft Defender: Antivirus**, then select **Next**.

1. On the **Settings** page, for **Permissions** select **Add**. From the list, select the available app permissions, and then select **OK**.

1. For each permission, set the permission state:

   - **Prompt**: Prompts the user to accept or deny.
   - **Auto grant**: Automatically approves without notifying the user.
   - **Auto deny**: Automatically denies without notifying the user.

   > [!NOTE]
   > On Android 12 and later, **Auto grant** isn't supported for certain permissions on corporate-owned work profile and dedicated devices. For details, see [Add app configuration policies for managed Android Enterprise devices](app-configuration-policies-use-android.md).

1. Select **Next**, assign the policy to the same user group you used when deploying the app, and then select **Next** > **Create**.

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

- [Configure Microsoft Defender for Endpoint web protection settings for Android](../protect/microsoft-defender-configure-android.md): Manage web protection settings from Intune by enrollment type.
- [Configure Microsoft Defender for Endpoint on Android features](/defender-endpoint/android-configure): Configure privacy controls and other Android-specific Defender features.
