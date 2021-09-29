---
title: Migrate Microsoft Tunnel to the Microsoft Defender for Endpoint app for Microsoft Intune
description: Migrate your Microsoft Tunnel configuration from using the standalone tunnel client app to use Microsoft Defender for Endpoint.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 10/01/2021
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology:

# optional metadata

#ROBOTS:
#audience:
 
ms.reviewer: tycast
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Migrate to Microsoft Defender for Endpoint for the Microsoft Tunnel in Intune

When you use Microsoft Tunnel as a VPN gateway solution for Microsoft Intune, plan to migrate from the standalone Microsoft Tunnel client app to Microsoft Defender for Endpoint with support for Microsoft Tunnel.

## Platform support

The following device platforms support Microsoft Defender for Endpoint as the tunnel client app:

- **Android Enterprise**:
  - Fully managed
  - Corporate-owned work profile
  - Personally-owned work Profile

  On June 14 2021, Microsoft Defender for Endpoint became generally available as the Microsoft Tunnel client app for Android for use with the Microsoft Tunnel Gateway in Microsoft Intune.

  If you've previously configured Microsoft Tunnel for Android using the standalone Microsoft Tunnel client app, you must migrate your devices to use Microsoft Defender for Endpoint as the tunnel client app before support for the Android standalone tunnel client app ends on October 26, 2021.

  When using Microsoft Defender for Endpoint to connect to Tunnel for Android, use [custom settings](../protect/microsoft-tunnel-configure.md#use-custom-settings-for-microsoft-defender-for-endpoint) in the VPN profile to manage Defender for Endpoint instead of using a separate app configuration profile. If you don't intend to use any Defender functionality, including web protection, use [custom settings](../protect/microsoft-tunnel-configure.md#use-custom-settings-for-microsoft-defender-for-endpoint) in the VPN profile and set the **defendertoggle** setting to **0**.

  <!-- Hiding the following info box, but keeping it for historical context and in case these issues resurface in the future >

  > [!IMPORTANT]
  > If you are using per-app VPN and also have Defender web protection enabled, you may experience connectivity issues for apps outside your per-app VPN list in the following scenarios, which may prevent devices from communicating with Intune:
  > - You are using an internal proxy. In this case, you must disable web protection in the VPN profile by adding the **antiphishing** setting in the [custom settings](../protect/microsoft-tunnel-configure.md#use-custom-settings-for-microsoft-defender-for-endpoint) section and entering a value of **0**.
  > - You are using internal DNS servers. You must include the IP address of at least one publicly-accessible DNS server, like 1.1.1.1, in your Tunnel Gateway [server configurations](../protect/microsoft-tunnel-configure.md#create-a-server-configuration).

  -->

- **iOS/iPadOS devices (in public preview)**:

  On September 28 2021, a preview version of Microsoft Defender for Endpoint became available as the Microsoft Tunnel client app for iOS/iPadOS devices for use with the Microsoft Tunnel Gateway in Microsoft Intune.

  Unlike most public previews for Intune, you must opt in before you can use this preview. When you opt in, Microsoft grants your tenant access to the preview build of Microsoft Defender for Endpoint that supports the tunnel app functionality. For information on how to opt in to this public preview, see [BLOG](URL).

  After you opt in:
  - Your tenant receives access to the app, and we'll send you an email with instructions for deploying it.
  - You’ll deploy the Microsoft Defender for Endpoint app to devices.
  - Replace your existing VPN profile for Microsoft Tunnel with a new VPN profile that directs devices to use the Microsoft Defender for Endpoint app.

  When using Microsoft Defender for Endpoint to connect to Tunnel for iOS/iPadOS, use custom settings in the VPN profile to manage Defender for Endpoint instead of using a separate app configuration profile. If you don't intend to use any Defender functionality, including web protection, use custom settings in the VPN profile and set the **TunnelOnly** setting to **True**.

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
    - A VPN profile with this connection type directs devices to use the Microsoft Defender for Endpoint app to connect to Microsoft Tunnel Gateway.
    - Use this connection type with VPN profiles for devices that run Android Enterprise.
    - A connection type of *Microsoft Tunnel (standalone client)* can no longer be created for Android. Existing VPN profiles with this connection type should be migrated to *Microsoft Tunnel* and use of Defender for Endpoint as the tunnel client app.

- **iOS/iPadOS**:
  - **Microsoft Tunnel (preview)**
    - A VPN profile with this connection type directs devices to use the public preview version of the Microsoft Defender for Endpoint app to connect to Microsoft Tunnel Gateway.

  - **Microsoft Tunnel (standalone client) (preview)**
    - A VPN profile with this connection type directs devices to use the standalone Tunnel client app.

**End-user changes**:

The Microsoft Defender for Endpoint app that you use as the tunnel client app includes a new tab for the Microsoft Tunnel functionality.

## Functionality in the Defender for Endpoint app

The Microsoft Defender for Endpoint app combines functionality of Microsoft Defender for Endpoint with the functionality of the Microsoft Tunnel app. Use of the new Defender app with support for Microsoft Tunnel doesn’t require a change to your existing licenses or the addition of a license for Defender for Endpoint.

The functionality that’s available in the Microsoft Defender for Endpoint app depends on the policy settings you deploy to manage the app on a device. The following tabs are available:

- **Tunnel** - This tab is where users connect to the Tunnel Gateway and can view connection statistics and client configuration settings.

  The Tunnel tab is available after a device receives a VPN Profile for Microsoft Tunnel that supports Defender for Endpoint. However, this tab isn’t available when the VPN profile turns off the Defender functionality (iOS/iPadOS and Android) or the Defender functionality is turned off by a separate app configuration profile (Android).

- **Dashboard** – This tab displays a summary of the device’s overall health, app security status, web protection status, and Tunnel status.
- **App security** (Android only) – On this tab, users can view the status of automatic scans on the device. Users can also uninstall the apps identified as threats and run a manual scan.
- **Web Protection** – This tab displays the status of the feature enabled or disabled by administrators, and details of the feature described in the flip cards.

Screenshot of the Defender for Endpoint app on Android:

:::image type="content" source="./media/microsoft-tunnel-migrate-app/defender-app-android.png" alt-text="Screenshot of the Defender for Endpoint app on Android.":::

<!--
Screenshot of the Defender for Endpoint app on iOS/iPadOS:

:::image type="content" source="./media/microsoft-tunnel-migrate-app/defender-app-ios.png" alt-text="Screenshot of the Defender for Endpoint app on iOS/iPadOS.":::
-->

For information about license requirements for Microsoft Defender for Endpoint, see [Get Microsoft Defender for Endpoint](/windows/security/threat-protection/microsoft-defender-atp/switch-to-microsoft-defender-prepare#get-microsoft-defender-for-endpoint).

## Migrate Android devices to Defender for Endpoint

When you're ready to use Microsoft Defender for Endpoint with Android devices, migrate supported devices from the standalone tunnel client app to the new app. You can also deploy the new app to other devices that haven't previously used the Microsoft Tunnel.

Migrating to Microsoft Defender for Endpoint requires the following broad actions, which are described in the following sections:

1. Review and record your current Tunnel configurations.
2. Deploy Microsoft Defender for Endpoint to supported devices.
3. Create new VPN profiles.
4. Clean up your previous deployments.

<!-- No longer needed due to fix made in early September, 2021, but retaining for history and in case issues arise again 

> [!IMPORTANT]
>
> If you use *Always-on VPN* with the standalone Tunnel client app today, during migration to Microsoft Defender for Endpoint:
>
> - Set *Always-on VPN* to **Not configured** in profiles for **Microsoft Tunnel (standalone client)**, which is the old client app.
> - Set *Always-on VPN* to **Enable** in profiles for **Microsoft Tunnel**, which is the new Microsoft Defender for Endpoint client app.
-->

### Deploy Defender for Endpoint for Android

Microsoft Defender for Endpoint with support for Microsoft Tunnel on Android, is available from the Managed Google Play store.

1. Locate and **Approve** the app in the Managed Google Play store for your tenant, and then **Sync** it. For information on this process, see [Managed Google Play store apps](../apps/apps-add-android-for-work.md#managed-google-play-store-apps).

2. **Assign** the app to groups.

3. Complete the assignment, and then ask users to install the Microsoft Defender for Endpoint app.

### Review and record your current Tunnel configurations

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

To enable devices to use Microsoft Defender for Endpoint to connect to Microsoft Tunnel Gateway, deploy new VPN profiles with the Microsoft Tunnel connection type. Editing the connection type of an existing profile isn’t supported.

1. Use the information from [Create a VPN Profile](../protect/microsoft-tunnel-configure.md#create-a-vpn-profile) to create and deploy new VPN profiles for your Android Enterprise devices.

2. During configuration, reference the settings you recorded from your existing profiles, but use a *connection type* of **Microsoft Tunnel**.

   If you’re using only the Tunnel functionality from the Defender for Endpoint app, and not Defender-specific functionality, add a [custom setting](../protect/microsoft-tunnel-configure.md#use-custom-settings-for-microsoft-defender-for-endpoint) of **defendertoggle** that is set to **0**. This configuration disables the Defender functionality, leaving only the Tunnel capabilities.

> [!NOTE]
> If you are using the Microsoft Defender for Endpoint app for Android, have web protection enabled, and are using per-app VPN, web protection will only apply to the apps in the per-app VPN list. On devices with a work profile, in this scenario we recommend adding all web browsers in the work profile to the per-app VPN list to ensure all work profile web traffic is protected.

### Clean up previous deployments for Android

After devices install the Microsoft Defender for Endpoint app and receive new VPN profiles, you can remove configurations for the original deployments.

For deployments of the original Microsoft Tunnel app:

1. Remove **Required** and **Available for enrolled devices**.

2. Add **Uninstall** to trigger removal of the application.

## Migrate iOS/iPadOS devices to Defender for Endpoint

When you're ready to use Microsoft Defender for Endpoint for iOS/iPadOS devices, migrate supported devices from the standalone tunnel client app to the new app. You can also deploy the new app to other devices that haven't previously used the Microsoft Tunnel.

Use of the Defender for Endpoint as the Tunnel client app will eventually be required. This is because the standalone Tunnel client app will go away, and Defender for Endpoint app will then be the only supported Tunnel app.

Migrating to Defender for Endpoint requires the following broad actions, which are described in the following sections:

1. Opt in to the public preview.
1. Review and record your current Tunnel configurations.
1. Get and deploy the Defender for Endpoint app from TestFlight.
1. Create new VPN profiles that use *Microsoft Tunnel (preview)* as the connection type.
1. Clean up your previous deployments.

The server settings stay exactly the same regardless of the client you’re using.

### Join the Defender for Endpoint public preview for Microsoft Tunnel on iOS

To gain access to the Microsoft Defender for Endpoint app that includes support for Microsoft Tunnel on iOS, you must opt into the public preview. Only tenants that sign-up for the preview will have access to the preview app that supports Microsoft Tunnel.

**To opt into the preview**, sign up at [SignUp URL](RUL).

After you sign up, you’ll be alerted by email when your tenant has access to the preview app. The email includes instructions for deploying the preview Microsoft Defender for Endpoint app. Unlike other apps, you won't deploy the preview Defender for Endpoint app to users and devices. Instead, users must install the app themselves.

### Install the TestFlight version of Defender for Endpoint

Defender for Endpoint app isn't available to download and deploy to iOS/iPadOS devices. Instead, each use must access TestFlight (testflight.apple.com) to install the app. Users will need their Apple ID to complete the installation.

1. On an iOS/iPadOS device that will use Defender for Endpoint as the Tunnel client app, browse to [https://aka.ms/mdeiosv2beta]( https://aka.ms/mdeiosv2beta). You're prompted to install the TestFlight app on the device or open TestFlight if it is already installed.

2. On the TestFlight app, follow the onscreen instructions to install Microsoft Defender for Endpoint. Verify that the version number is **1.1.21030301**.

3. Sign-in and onboard the Defender for Endpoint using your corporate account.

### Review and record your current Tunnel configurations for iOS/iPadOS

Before you begin your migration to Defender for Endpoint, use the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) to review and record the settings you currently use for the following Intune configurations:

- **VPN profiles for Microsoft Tunnel (standalone client) (preview)**

  1. Go to **Devices** > **Configuration profiles** and select each applicable profile and review its **Properties**.

  2. From Properties, record the available values. This information will help you create new VPN profiles that mirror your current configurations.

- **If you use per-app VPN**, look at your iOS app deployments and record details for apps that are assigned to a **Microsoft Tunnel (standalone client) (preview)** profile. Also note which are assigned as *required* and which are assigned as *available*.

  1. Go to **Apps** and select each applicable deployment and review its **Properties**.

  2. From Properties, record the available values including those that are assigned as *required* or are assigned as *available*. This information will help you to create similar deployments for the Microsoft Defender for Endpoint app.

### Create new VPN profiles for iOS/iPadOS

To enable devices to use Microsoft Defender for Endpoint to connect to Microsoft Tunnel Gateway, deploy new VPN profiles with the **Microsoft Tunnel (preview)** connection type. Editing the connection type of an existing profile isn’t supported.

1. Use the information from [Create a VPN Profile](../protect/microsoft-tunnel-configure.md#create-a-vpn-profile) to create and deploy new VPN profiles for your iOS/iPadOS devices.

2. During configuration, reference the settings you recorded from your existing profiles, but use a *connection type* of **Microsoft Tunnel (preview)**.
If you’re using only the Tunnel functionality from the Defender for Endpoint app, and not Defender-specific functionality, add a [custom setting](../protect/microsoft-tunnel-configure.md#use-custom-settings-for-microsoft-defender-for-endpoint) of **TunnelOnly** that is set to **True**. This configuration disables the Defender functionality, leaving only the Tunnel capabilities.

3. After the profile deploys, wait for devices to check in or force devices to sync to get the new policies.

4. Verify that users can connect to Tunnel manually in the Defender for Endpoint app. If your VPN Profile includes on-demand rules, users must open the Defender for Endpoint app one time before the new on-demand rules can apply.

5. If you’re using per-app VPN:
   1. Wait at least 10 minutes after creating the new VPN profile. After 10 minutes you can then change the app deployment assignments from *Microsoft Tunnel (standalone client) (preview)* to use the new VPN Profile for *Microsoft Tunnel (preview)*.

   2. For each app that is assigned as *available*, users must reinstall the app ***after the new VPN profile is installed on their device*** so that the VPN profile assignment can update. This can be done by going to Company Portal, going to **Apps**, tapping the app, and tapping **Install**.

## Next Steps

[Use Conditional Access with the Microsoft Tunnel](microsoft-tunnel-conditional-access.md)  
[Monitor Microsoft Tunnel](microsoft-tunnel-monitor.md)
