---
title: Deploy and configure Microsoft Defender for Endpoint on Android
description: Learn how to deploy and configure Microsoft Defender for Endpoint on Android devices using Microsoft Intune, including app configuration policies, always-on VPN, and low-touch onboarding.
ms.date: 04/06/2026
ms.topic: how-to
ms.author: brenduns
ms.reviewer: aanavath
ai-usage: ai-assisted
ms.collection:
- M365-identity-device-management
- sub-secure-endpoints
---

# Deploy and configure Microsoft Defender for Endpoint on Android

Use Microsoft Intune to deploy Microsoft Defender for Endpoint to Android devices to support onboarding those devices to the Defender for Endpoint service. On Android, onboarding is app-driven: a device is considered onboarded when the Defender app is opened and setup is complete. Intune manages the app deployment and provides configuration policies that configure Defender features and streamline the steps users need to complete during onboarding. This article covers adding the app from Managed Google Play, assigning and verifying the deployment, creating app configuration policies, setting up always-on VPN, and optionally enabling low-touch onboarding.

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

1. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Apps** (1) and then select the Android tile to open the **Android apps** page (2). Select **Create** (3) and for App type, select **Managed Google Play app** (4), and then **Select**.

   :::image type="content" source="./media/apps-defender-android/managed-google-play-app.png" alt-text="Screenshot that shows where in the Microsoft Intune admin center portal to create a Managed Google Play app." lightbox="./media/apps-defender-android/managed-google-play-app.png":::

    1. On the *Managed Google Play* page, search for `Microsoft Defender`. Select **Microsoft Defender: Antivirus** from the search results. This is the name of the Defender for Endpoint app on the Managed Google Play store.

    2. On the apps page, review the app details and then select **Select** (1), followed by selecting **Sync** (2) to sync the app with Intune.

       :::image type="content" source="./media/apps-defender-android/select-and-sync.png" alt-text="Screenshot showing the locations of the Select and Sync buttons." lightbox="./media/apps-defender-android/select-and-sync.png" width="250":::

       The sync completes in a few minutes.

2. After the sync completes, return to the Intune admin center and on the *Android apps* screen, select **Refresh**. *Microsoft Defender: Antivirus* should now appear in the apps list.

   :::image type="content" source="./media/apps-defender-android/defender-in-app-list.png" alt-text="Screenshot showing the Microsoft Defender for Endpoint app in the apps list." lightbox="./media/apps-defender-android/defender-in-app-list.png":::

Stay on the *Android apps* page for the following procedure.

### Assign the app

Assign the app as a required app so it installs automatically in the work profile during the next device sync through the Company Portal app.

1. From the *Android apps* page of the Intune admin center, select **Microsoft Defender: Antivirus** from the apps list. Go to **Properties** (1), and for *Assignments*, select **Edit** (2).

   :::image type="content" source="./media/apps-defender-android/edit-app-properties.png" alt-text="Screenshot showing the Edit option on the Properties page." lightbox="./media/apps-defender-android/edit-app-properties.png":::

2. On the *Edit application* pane, go to the *Required* section (1) and select **Add group** to open the *Select groups* pane.

   :::image type="content" source="./media/apps-defender-android/add-groups.png" alt-text="Screenshot showing the Select groups pane." lightbox="./media/apps-defender-android/add-groups.png":::

3. On the **Select groups** pane, select the groups you want to receive this app, and then select **Select**.

4. Back on the *Edit application* pane, select **Review + Save** from the bottom of the pane, and then **Save** to commit the assignment.

### Verify deployment

After the assignment is saved, you can confirm the installation status for targeted devices before proceeding with configuration.

1. From the *Android apps* page of the Intune admin center, select **Microsoft Defender: Antivirus** from the apps list. On the default app page, *Overview*, Intune displays chart tiles that provide a rollup of installation status.

2. To identify if a specific device has installed the app, select **Device install status** or select the **Device status** tile. Intune displays a list of targeted devices with additional details.

   :::image type="content" source="./media/apps-defender-android/device-status-detail.png" alt-text="Screenshot showing the Device install status pane." lightbox="./media/apps-defender-android/device-status-detail.png":::

3. Confirm that target devices show a successful installation state before continuing.

## Configure Microsoft Defender for Endpoint on Android

After deploying the app, use Intune policies to configure Microsoft Defender for Endpoint on Android devices. This involves creating an app configuration policy to grant app permissions and a device configuration profile to set up always-on VPN for web protection. For optional feature configurations specific to Defender, such as network protection and privacy controls, see [Configure Microsoft Defender for Endpoint on Android features](/defender-endpoint/android-configure) in the Defender documentation.

### Configure app permissions and onboarding settings

Create an app configuration policy to grant Defender the permissions it needs on the device and, optionally, enable low-touch onboarding to reduce the steps users complete during first launch.

1. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Apps**, expand *Managed apps* and select **Configuration** > **Create** > **Managed devices**.

1. On the **Basics** page, specify the following details:

   - **Name**: Enter a descriptive name, such as *Microsoft Defender for Endpoint*.
   - **Platform**: **Android Enterprise**
   - **Profile type**: Select the type that matches your device enrollment:
     - **Personally-owned Work Profile only**
     - **Fully Managed, Dedicated, and Corporate-owned work profile only**
   - **Targeted app**: Select **Microsoft Defender: Antivirus**, select **OK**, and then select **Next**.

1. On the **Settings** page, leave *Configuration settings format* at its default for now. For *Permissions*, select **Add**. From the *Add permissions* list, select the available app permissions, and then select **OK**.

   Defender for Endpoint recommends granting the following permissions during deployment:

   | Permission | Recommended state | Why it matters |
   |---|---|---|
   | **Location access (fine)** | **Auto grant** | Required for web protection and [Network Protection](/defender-endpoint/android-configure#network-protection). Without it, Defender can only protect against rogue certificates — Wi-Fi threat detection is unavailable. Users must also select **Allow all the time** during onboarding for full Wi-Fi threat coverage. |
   | **POST_NOTIFICATIONS** | **Auto grant** | Required for threat alerts to reach the user. See the note below for enrollment-type and OS version limitations. |
   
   After adding the permissions, use the *Permission state* dropdown to set the desired behavior for each:

   - **Prompt**: Prompts the user to accept or deny.
   - **Auto grant**: Automatically approves without notifying the user.
   - **Auto deny**: Automatically denies without notifying the user.

   > [!NOTE]
   > On Android 12 and later, **Auto grant** isn't supported for certain permissions on corporate-owned work profile and dedicated devices. For details, see [Add app configuration policies for managed Android Enterprise devices](app-configuration-policies-use-android.md).

1. **(Optional) Enable low-touch onboarding.**

   Low-touch onboarding is disabled by default. Without it, users who open Defender for the first time must enter their work account credentials and step through the app's setup wizard manually. In low-touch onboarding mode, the policy pre-populates the user's identity (UPN), so users don't need to type their sign-in credentials during first launch. When combined with the always-on VPN profile covered in the next section, this minimizes the prompts and steps users encounter during onboarding.

   Low-touch onboarding can be useful for corporate-owned, fully managed deployments where you want to reduce user friction. For personally-owned work profile devices, where users might expect more active participation in app setup, the standard flow can be more appropriate. If you skip this step, the policy works as a permissions-only policy and users complete onboarding through the standard flow.

   > [!NOTE]
   > Unlike iOS (supervised) and Windows, Android doesn't support fully silent or zero-touch onboarding. Android's permission model requires explicit user consent for certain permissions, so some degree of user interaction during first launch is always required. Low-touch onboarding is the closest available option for minimizing that interaction.

   To enable low-touch onboarding, on the **Settings** page set the *Configuration settings format* dropdown to **Use configuration designer**, select **Add**, and then configure the following keys:

   | Key | Value type | Configuration value |
   |---|---|---|
   | **Low touch onboarding** | Integer | `1` |
   | **User UPN** | Variable | `User Principal Name (UPN)` |

   Select both keys from the list and select **OK**, then set the *Value type* and *Configuration value* for each as shown in the table.
   

1. On the **Assignments** page, assign this policy to the same user groups you used when deploying the *Microsoft Defender: Antivirus* app.  

1. On **Review + create**, confirm your choices, and then select **Create**.

### Set up always-on VPN

Defender for Endpoint supports device configuration policies for managed devices with Microsoft Intune. Use a device configuration profile to set up always-on VPN on Android Enterprise enrolled devices, so users don't need to manually configure a VPN service during onboarding.

1. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** (1), expand *Manage devices* and select **Configuration** (2). On the *Policies* tab (3), select **Create** (4) \> **New Policy**. On the *Create a profile* pane Set *Platform* to **Android Enterprise** and *Profile type* to **Templates** (5), and then select **Device restrictions** (6) for one of the following template types, based on your device enrollment type:

   - **Fully Managed, Dedicated, and Corporate-Owned Work Profile**
   - **Personally-Owned Work Profile**

   Then, select **Create** to open the Device restrictions policy configuration workflow.

   :::image type="content" source="./media/apps-defender-android/1autosetupofvpn.png" alt-text="The Configuration profiles menu item in the Policy pane" lightbox="./media/apps-defender-android/1autosetupofvpn.png":::

2. On the **Basics** page, provide a **Name** and a **Description** to uniquely identify the configuration profile.

   :::image type="content" source="./media/apps-defender-android/2autosetupofvpn.png" alt-text="The devices configuration profile Name and Description fields in the Basics pane" lightbox="./media/apps-defender-android/2autosetupofvpn.png":::

3. For **Configuration settings**, expand **Connectivity**, and then configure your VPN:

   1. Enable **Always-on VPN (work profile-level)**. Set up a VPN client in the work profile to automatically connect and reconnect to the VPN whenever possible. Only one VPN client can be configured for always-on VPN on a given device, so make sure no more than one always-on VPN policy is deployed to a device.

   2. Use the **VPN client** dropdown list to select **Custom**. In this case, the custom VPN is the Defender for Endpoint VPN, which provides Web Protection.

      > [!NOTE]
      > The Microsoft Defender for Endpoint app must be installed on the user's device for automatic VPN setup to occur.

   3. For **Package ID** , specify the ID of the *Microsoft Defender: Antivirus* app from the Managed Google Play store. For the [Microsoft Defender app URL](https://play.google.com/store/apps/details?id=com.microsoft.scmx), the package ID is `com.microsoft.scmx`.

   4. Set **Lockdown mode** to **Not configured**, which is the default.

      :::image type="content" source="./media/apps-defender-android/3autosetupofvpn.png" alt-text="The Connectivity pane under the Configuration settings tab" lightbox="./media/apps-defender-android/3autosetupofvpn.png":::

4. On the **Assignments** page, select the user group to which this device configuration profile should be assigned. Choose **Select groups** to include, select the applicable group, and then select **Next**.

   The group to select is typically the same group to which you assign the Microsoft Defender for Endpoint Android app.

5. On the **Review + Create** page, review your settings and then select **Create**.

## Complete device onboarding

After policies are pushed to devices, users complete onboarding from the device.

1. Users can validate onboarding status on the device by going to the work profile and confirming that Defender for Endpoint is available. On personally owned devices with a work profile, Defender appears in the work profile. On corporate-owned fully managed devices, Defender appears in the single device profile.

   :::image type="content" source="./media/apps-defender-android/c2e647fc8fa31c4f2349c76f2497bc0e.png" alt-text="The application display pane" lightbox="./media/apps-defender-android/c2e647fc8fa31c4f2349c76f2497bc0e.png":::

2. Users open the app and accept the permissions to complete onboarding.

   > [!TIP]
   > Instruct users to select **Allow all the time** when prompted for location access during app setup. This enables full Wi-Fi threat detection through [Network Protection](/defender-endpoint/android-configure#network-protection). If users select *While using the app* or deny the permission, Defender can still protect against rogue certificates but cannot detect threats on open or suspicious Wi-Fi networks. There's no admin configuration that enforces this choice — it requires user consent at the OS level.

   :::image type="content" source="./media/apps-defender-android/MDE-new.png" alt-text="The display of a Microsoft Defender for Endpoint application on a mobile device" lightbox="./media/apps-defender-android/MDE-new.png":::

## Verify onboarding status

After users complete onboarding, confirm that devices are reporting successfully.

To verify from the Intune admin center:

1. Go to **Endpoint security** > **Endpoint detection and response**.
2. Select the **EDR Onboarding Status** tab and review the onboarding status for your Android devices. Devices that successfully onboarded show a status of *Successfully onboarded*.

To verify from the Microsoft Defender portal:

1. In the [Microsoft Defender portal](https://security.microsoft.com), navigate to the **Device inventory** page and confirm that your Android devices appear there.

   :::image type="content" source="./media/apps-defender-android/9fe378a1dce0f143005c3aa53d8c4f51.png" alt-text="The Microsoft Defender for Endpoint portal" lightbox="./media/apps-defender-android/9fe378a1dce0f143005c3aa53d8c4f51.png":::

For more detail on using Intune to monitor onboarding status across platforms, see [Monitor device onboarding status](../protect/microsoft-defender-integrate.md#monitor-device-onboarding-status).

## Next steps

- [Configure Microsoft Defender for Endpoint web protection settings for Android](../protect/microsoft-defender-configure-android.md): Manage web protection settings from Intune by enrollment type.
- [Configure Microsoft Defender for Endpoint on Android features](/defender-endpoint/android-configure): Configure privacy controls and other Android-specific Defender features.
