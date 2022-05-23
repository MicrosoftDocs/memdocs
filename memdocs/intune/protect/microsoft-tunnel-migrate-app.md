---
title: Migrate Microsoft Tunnel to the Microsoft Defender for Endpoint app for Microsoft Intune
description: Migrate your Microsoft Tunnel configuration from using the standalone tunnel client app to use Microsoft Defender for Endpoint.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/12/2022
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology:

# optional metadata

#ROBOTS:
#audience:
 
ms.reviewer: ochukwunyere
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Migrate to Microsoft Defender for Endpoint for the Microsoft Tunnel in Intune

If you use Microsoft Tunnel as a VPN gateway solution for Microsoft Intune, plan to migrate from the standalone Microsoft Tunnel client app to Microsoft Defender for Endpoint with support for Microsoft Tunnel.

## Platform support

If you've previously configured Microsoft Tunnel for iOS using the standalone Microsoft Tunnel client app, you must migrate your devices to use Microsoft Defender for Endpoint as the tunnel client app before support for the iOS standalone tunnel client app ends by the end of July 29, 2022.

Support for the Android standalone tunnel client app ended on January 31, 2022.

The following device platforms support Microsoft Defender for Endpoint as the tunnel client app:

- **Android Enterprise**:
  - Fully managed
  - Corporate-owned work profile
  - Personally owned work Profile

  On June 14, 2021, Microsoft Defender for Endpoint became generally available as the Microsoft Tunnel client app for Android for use with the Microsoft Tunnel Gateway in Microsoft Intune.

  If you've previously configured Microsoft Tunnel for Android using the standalone Microsoft Tunnel client app, you must migrate your devices to use Microsoft Defender for Endpoint as the Tunnel client app before support for the Android standalone Tunnel client app ends on October 26, 2021.

  When using Microsoft Defender for Endpoint to connect to Tunnel for Android, use [custom settings](../protect/microsoft-tunnel-configure.md#use-custom-settings-for-microsoft-defender-for-endpoint) in the VPN profile to manage Defender for Endpoint instead of using a separate app configuration profile. If you don't intend to use any Defender for Endpoint functionality, including web protection, use [custom settings](../protect/microsoft-tunnel-configure.md#use-custom-settings-for-microsoft-defender-for-endpoint) in the VPN profile and set the **defendertoggle** setting to **0**.

- **iOS/iPadOS devices**:

  On April 29, 2022, Microsoft Defender for Endpoint became available as the Microsoft Tunnel client app for iOS/iPadOS devices for use with the Microsoft Tunnel Gateway in Microsoft Intune.

  If you've previously configured Microsoft Tunnel for iOS/iPadOS using the standalone Microsoft Tunnel client app, you must migrate your devices to use Microsoft Defender for Endpoint as the Tunnel client app. Support for the iOS standalone Tunnel client app ends on July 29, 2022.

  To configure the Microsoft Defender for Endpoint app to connect to Tunnel, you'll need to create a new VPN profile with the *Microsoft Tunnel (preview)* connection type.

  When using Microsoft Defender for Endpoint to connect to Tunnel for iOS/iPadOS, use [custom settings](../protect/microsoft-tunnel-configure.md#use-custom-settings-for-microsoft-defender-for-endpoint) in the VPN profile to manage Defender for Endpoint. If you don't intend to use any Defender for Endpoint functionality, including web protection, use custom settings in the VPN profile and set the **TunnelOnly** setting to **True**.

## Changes introduced to support Defender for Endpoint

The introduction of Microsoft Defender for Endpoint as the tunnel client app brings the following changes.

**Renamed connection type for VPN profiles for all tenants**:

To support Defender for Endpoint, all VPN profiles created before March 2, 2021 that have a connection type of **Microsoft Tunnel** were updated to a connection type of **Microsoft Tunnel (standalone client)**.

This change:

- Applies to all tenants.
- Applies to both the Android and iOS/iPadOS platforms.
- Has no effect on the functionality of those existing profiles other than the change of connection type name.
- Supports the change to use Microsoft Defender for Endpoint to support Microsoft Tunnel functionality now or at a future time.
- Cannot be reversed. You can’t edit existing profiles to change their connection type.

The following connection types are now available in VPN profiles:

- **Android**:
  - **Microsoft Tunnel**
    - A VPN profile with this connection type configures the Microsoft Defender for Endpoint app to connect to Microsoft Tunnel Gateway.
    - Use this VPN connection type for devices that run Android Enterprise.
    - A connection type of *Microsoft Tunnel (standalone client)* should no longer be created for Android. Existing VPN profiles with this connection type should be migrated to *Microsoft Tunnel* and you should use Defender for Endpoint as the Tunnel client app.

- **iOS/iPadOS**:
  - **Microsoft Tunnel (preview)**
    - A VPN profile with this connection type configures the Microsoft Defender for Endpoint app to connect to Microsoft Tunnel Gateway.
    - A connection type of *Microsoft Tunnel (standalone client) (preview)* should no longer be created for iOS/iPadOS. Existing VPN profiles with this connection type should be migrated to *Microsoft Tunnel (preview)*, which requires Defender for Endpoint as the Tunnel client app.

    > [!Note]
    > On April 29, 2022, the *Microsoft Tunnel (preview)* connection type became generally available and supports Microsoft Defender for Endpoint as a tunnel client app. However, the connection type continues to reflect *preview*.

    
**End-user changes**:

The Microsoft Defender for Endpoint app that you use as the Tunnel client app includes a new tab for the Microsoft Tunnel functionality.

## Functionality in the Defender for Endpoint app

The Microsoft Defender for Endpoint app combines functionality of Microsoft Defender for Endpoint with the functionality of the Microsoft Tunnel app. You can use the new Defender app with Microsoft Tunnel to connect to Tunnel Gateway, even if you don’t otherwise use or have a license for Microsoft Defender for Endpoint.

The functionality that’s available in the Microsoft Defender for Endpoint app depends on the policy settings you deploy to manage the app on a device. The following tabs are available:

- **Tunnel** - This tab is where users connect to the Tunnel Gateway and can view connection statistics and client configuration settings.

  The Tunnel tab is available after a device receives a VPN profile for Microsoft Tunnel that supports Defender for Endpoint.

- **Dashboard** – This tab displays a summary of the device’s overall health, app security status, web protection status, and Tunnel status.

- **App security** (Android only) – On this tab, users can view the status of automatic scans on the device. Users can also uninstall the apps identified as threats and run a manual scan. This tab isn’t available when the VPN profile turns off the Defender for Endpoint functionality or when the Defender for Endpoint functionality is turned off by a separate app configuration profile.

- **Web Protection** – This tab displays the status of the feature enabled or disabled by administrators, and details of the feature described in the flip cards. This tab isn’t available when the VPN profile turns off the Defender for Endpoint functionality (iOS/iPadOS and Android) or the Defender for Endpoint functionality is turned off by a separate app configuration profile (Android).

Screenshot of the Defender for Endpoint app on Android:

:::image type="content" source="./media/microsoft-tunnel-migrate-app/defender-app-android.png" alt-text="Screenshot of the Defender for Endpoint app on Android.":::

For information about license requirements for Microsoft Defender for Endpoint, see [Get Microsoft Defender for Endpoint](/windows/security/threat-protection/microsoft-defender-atp/switch-to-microsoft-defender-prepare#get-microsoft-defender-for-endpoint).

## Migrate Android devices to Defender for Endpoint

When you're ready to use Microsoft Defender for Endpoint with Android devices, migrate supported devices from the standalone tunnel client app to the new app. You can also deploy the new app to other devices that haven't previously used Microsoft Tunnel.

Migrating to Microsoft Defender for Endpoint requires the following broad actions, which are described in the following sections:

1. Review and record your current Tunnel configurations.
2. Deploy Microsoft Defender for Endpoint to supported devices.
3. Create new VPN profiles.
4. Clean up your previous deployments.

### Deploy Defender for Endpoint for Android

Microsoft Defender for Endpoint with support for Microsoft Tunnel on Android, is available from the Managed Google Play store.

1. Locate and **Approve** the app in the Managed Google Play store for your tenant, and then **Sync** it. For information on this process, see [Managed Google Play store apps](../apps/apps-add-android-for-work.md#managed-google-play-store-apps).

2. **Assign** the app to groups.

3. Complete the assignment, and then ask users to install the Microsoft Defender for Endpoint app.

### Review and record your current Tunnel configurations for Android

Before you begin your migration to Defender for Endpoint, take the time to review and record the settings you currently use for the following Intune configurations for Android devices:

- VPN profiles for Microsoft Tunnel
- App deployments of the Microsoft Tunnel

You'll use this information when you deploy new VPN profiles and the Defender for Endpoint app, to mirror your existing deployments.

1. Sign in to [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Devices** > **Configuration profiles**. Locate the VPN profiles you use for Microsoft Tunnel for your Android devices. They display a connection type of *Microsoft Tunnel (standalone client)*. You’ll replace these profiles with new profiles that use the Defender for Endpoint app.

   1. Select each profile and then **Properties**.

   2. From Properties, record the available values. This information will help you create new VPN profiles that mirror your current configurations.

1. Next, record details for your Tunnel app deployments. In the admin center, go to **Apps**. Locate your deployments of Microsoft Tunnel to Android Enterprise devices.

   1. Select each applicable deployment and review its **Properties**.

   2. From Properties, record the available values. This information will help you to create similar deployments for the Microsoft Defender for Endpoint app.

### Create new VPN profiles for Android

To enable devices to use Microsoft Defender for Endpoint to connect to Microsoft Tunnel Gateway, deploy new VPN profiles with the *Microsoft Tunnel* connection type. Editing the connection type of an existing profile isn’t supported.

1. Use the information from [Create a VPN Profile](../protect/microsoft-tunnel-configure.md#create-a-vpn-profile) to create and deploy new VPN profiles for your Android Enterprise devices.

2. During configuration, reference the settings you recorded from your existing profiles, but use a *connection type* of **Microsoft Tunnel**.

   If you’re using only the Tunnel functionality from the Defender for Endpoint app, and not Defender-specific functionality, add a [custom setting](../protect/microsoft-tunnel-configure.md#use-custom-settings-for-microsoft-defender-for-endpoint) of **defendertoggle** that is set to **0**. This configuration disables the Defender for Endpoint functionality, leaving only the Tunnel capabilities.

> [!NOTE]  
> If you are using the Microsoft Defender for Endpoint app for Android, have web protection enabled, and are using per-app VPN, web protection will only apply to the apps in the per-app VPN list. On devices with a work profile, in this scenario we recommend adding all web browsers in the work profile to the per-app VPN list to ensure all work profile web traffic is protected.

### Clean up previous deployments for Android

After devices install the Microsoft Defender for Endpoint app and receive new VPN profiles, you can remove configurations for the original deployments.

For deployments of the original Microsoft Tunnel app:

1. Remove **Required** and **Available for enrolled devices**.

2. Add **Uninstall** to trigger removal of the application.

## Migrate iOS/iPadOS devices to Defender for Endpoint

When you're ready to use the generally available version of Microsoft Defender for Endpoint for iOS/iPadOS devices, migrate supported devices from the standalone tunnel client app to the new app. You can also deploy the new app to other devices that haven't previously used the Microsoft Tunnel.

Migrating to Defender for Endpoint requires the following broad actions, which are described in the following sections:

1. Deploy Microsoft Defender for Endpoint to supported devices.
2. Review and record your current Tunnel configurations.
3. Create new VPN profiles or reconfigure existing profiles to use *Microsoft Tunnel (preview)* as the connection type.
4. Clean up your previous deployments.

The server settings stay exactly the same regardless of the client you’re using.

### Install Microsoft Defender for Endpoint

Microsoft Defender for Endpoint with support for Microsoft Tunnel for iOS is available from the Apple app store.

1. Locate and **Approve** the app in the Apple app store for your tenant, and then **Sync** it. For information on this process, see [Add iOS store apps to Microsoft Intune](../apps/store-apps-ios.md).
2. **Assign** the app to groups.
3. Complete the assignment, and then ask users to install the Microsoft Defender for Endpoint app.

### Review and record your current Tunnel configurations for iOS/iPadOS

Before you begin your migration to Defender for Endpoint, use the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) to review and record the settings you currently use for the following Intune configurations:

- **VPN profiles for Microsoft Tunnel (standalone client) (preview)**

  1. Go to **Devices** > **Configuration profiles** and select each applicable profile and review its **Properties**.

  2. From Properties, record the available values. This information will help you create new VPN profiles that mirror your current configurations.

- **If you use per-app VPN**, look at your iOS app deployments and record details for apps that are assigned to a **Microsoft Tunnel (standalone client) (preview)** profile.

  1. Go to **Apps** and select each applicable deployment and review its **Properties**.

  2. From Properties, record the available values including those that are assigned as *required* or are assigned as *available*. This information will help you to create similar deployments for the Microsoft Defender for Endpoint app.

### Manage VPN profiles for iOS/iPadOS

To enable devices to use Microsoft Defender for Endpoint to connect to Microsoft Tunnel Gateway, deploy VPN profiles that use the **Microsoft Tunnel (preview)** connection type. During migration you can choose to edit your existing profiles to use the new connection type, or create new VPN profiles with the new connection type.

#### Modify a VPN Profile for Microsoft Tunnel

Use the following steps to modify a VPN profile to migrate devices from  the standalone tunnel client app to Microsoft Defender for Endpoint as the tunnel client app.

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and go to > **Devices** > **Configuration profiles** > **iOS/iPadOS**.
2. Select the VPN profile you want to edit, and then select **Properties**, and then **Edit** the *Configuration settings*.
3. On the *Configuration settings* page:

   1. Review the current settings for each category. When you change the *Connection type* the profiles settings are cleared and you’ll need to restore them.
   2. Change the *Connection type* from *Microsoft Tunnel (standalone client)(preview)* to **Microsoft Tunnel(preview)**.
   3. Reenter the applicable settings for this VPN profile.

      > [!IMPORTANT]  
      > Even when a setting appears to remain configured and not cleared, reenter each setting to ensure the correct values are applied.

   4. If you’re using only the Tunnel functionality from the Defender for Endpoint app, and not Defender-specific functionality, add a [custom setting](../protect/microsoft-tunnel-configure.md#use-custom-settings-for-microsoft-defender-for-endpoint) of **TunnelOnly** that is set to **True**. This configuration disables the Defender functionality, leaving only the Tunnel capabilities.

4. Select **Review + save** to save the profile.
5. After the profile redeploys, wait for devices to check in or force devices to sync to get the new policies.
6. Verify that users can connect to Tunnel manually in the Defender for Endpoint app. If your VPN profile includes on-demand rules, users must open the Defender for Endpoint app one time before the new on-demand rules can apply.

#### Create a new VPN profile for Microsoft Tunnel

Use the following steps to create a new VPN profile for devices that will use *Microsoft Defender for Endpoint* as the tunnel client app. When the profile is configured as a per-app VPN, the last step requires you to restart devices after they receive the VPN profile. To avoid this you can choose to [modify an existing VPN profile](#modify-a-vpn-profile-for-microsoft-tunnel) instead of creating and deploying a new one.

1. Use the information from [Create a VPN Profile](../protect/microsoft-tunnel-configure.md#create-a-vpn-profile) to create and deploy new VPN profiles for your iOS/iPadOS devices.

2. During configuration, reference the settings you recorded from your existing profiles, but use a *connection type* of **Microsoft Tunnel (preview)**.
If you’re using only the Tunnel functionality from the Defender for Endpoint app, and not Defender-specific functionality, add a [custom setting](../protect/microsoft-tunnel-configure.md#use-custom-settings-for-microsoft-defender-for-endpoint) of **TunnelOnly** that is set to **True**. This configuration disables the Defender for Endpoint functionality, leaving only the Tunnel capabilities.

3. After the profile deploys, wait for devices to check in or force devices to sync to get the new policies.

4. Verify that users can connect to Tunnel manually in the Defender for Endpoint app. If your VPN profile includes on-demand rules, users must open the Defender for Endpoint app one time before the new on-demand rules can apply.

5. If you’re using per-app VPN:
   1. Wait at least 10 minutes after creating the new VPN profile. After 10 minutes you can then change the app deployment assignments from the *Microsoft Tunnel (standalone client) (preview)* VPN profile to the new VPN profile for *Microsoft Tunnel (preview)*.

   2. After the new VPN profile deploys to a device, that device must restart before the new VPN profile is used. To restart a device, see [remotely restart devices with Intune](/intune/remote-actions/device-restart). 

## Next Steps

[Use Conditional Access with Microsoft Tunnel](microsoft-tunnel-conditional-access.md)  
[Monitor Microsoft Tunnel](microsoft-tunnel-monitor.md)
