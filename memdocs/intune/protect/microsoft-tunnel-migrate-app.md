---
title: Migrate Microsoft Tunnel to the Microsoft Defender for Endpoint app for Microsoft Intune - Azure | Microsoft Docs
description: Migrate your Microsoft Tunnel configuration from using the standalone Tunnel app to use Microsoft Defender for Endpoint.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/30/2021
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

*Microsoft Defender for Endpoint support for Android is in public preview*.

Use a preview version of Microsoft Defender for Endpoint as the tunnel application for the Microsoft Tunnel Gateway in Microsoft Intune. The preview version of **Microsoft Defender for Endpoint** includes the Tunnel app functionality. The new app replaces the standalone **Microsoft Tunnel** app as the tunnel client on supported devices.

> [!TIP]
> For more information about the preview, see the blog **Simplify mobile security with a single app for Microsoft Tunnel and Microsoft Defender for Endpoint** at [aka.ms/defendertunnel](https://aka.ms/defendertunnel).
>
> For general information about Microsoft Tunnel, see [Microsoft Tunnel overview](../protect/microsoft-tunnel-overview.md).

When this preview for Android is over and the Microsoft Defender for Endpoint app that supports Tunnel becomes generally available, the standalone app is deprecated. Support for the standalone apps ends after 60 days.

The public preview supports the following device platforms:

- Android Enterprise:
  - Fully Managed
  - Corporate-Owned Work Profile
  - Personally-Owned Work profile

> [!IMPORTANT]  
> The preview version of Microsoft Defender for Endpoint as the Tunnel application isn’t supported for Android Enterprise personally-owned work profile devices when you use [*App configuration policies*](../apps/app-configuration-policies-overview.md) to configure Microsoft Defender for Endpoint. In this scenario, do not migrate to the Tunnel app.

Unlike most public previews for Intune, you must opt in before you can use  this preview. When you opt in, Microsoft grants your tenant access to the preview build of Microsoft Defender for Endpoint that supports the tunnel app functionality. After you opt in:

- Your tenant receives access to the app, and we'll send you an email with instructions for deploying it.
- You’ll deploy the Microsoft Defender for Endpoint app to devices.
- Replace your existing VPN profile for Microsoft Tunnel with a new VPN profile that directs devices to use the Microsoft Defender for Endpoint app.

## Changes introduced with this preview

The introduction of the public preview version of Microsoft Defender for Endpoint brings the following changes.

**Renamed connection type for VPN profiles for all tenants**:

To support this preview, all VPN profiles created before March 2, 2021 that have a connection type of **Microsoft Tunnel** were updated to a connection type of **Microsoft Tunnel (standalone client)**.

This change:  

- Applies to all tenants.
- Has no effect on the functionality of those existing profiles.
- Supports the change to use Microsoft Defender for Endpoint to support Microsoft Tunnel functionality.
- Cannot be reversed. You can’t edit existing profiles to change their connection type.

The following connection types are now available in VPN profiles:

- **Microsoft Tunnel (standalone client)** - The new name of the original connection type for VPN profiles. Use this connection type for profiles assigned to devices that aren't part of the preview:

  - A VPN profile with this connection type directs devices to use the Microsoft Tunnel app to connect to the Microsoft Tunnel Gateway.

  - Use this connection type with VPN profiles for devices that run Android Enterprise and iOS/iPadOS.

  > [!TIP]
  > This connection type and the standalone Tunnel app will be deprecated after the preview for Tunnel functionality in Microsoft Defender for Endpoint moves out of preview and into general availability. Deprecation will happen at least 60 days after it's announced.

- **Microsoft Tunnel** – A new connection type added to VPN profiles to support Microsoft Defender for Endpoint. This connection type reuses the name of the original connection type. Use this connection type for profiles assigned to devices that are part of the preview:

  - A VPN profile with this connection type directs devices to use the Microsoft Defender for Endpoint app to connect to Microsoft Tunnel Gateway.

  - Use this connection type with VPN profiles for devices that run Android Enterprise.

  > [!IMPORTANT]
  > Although this connection type appears for iOS/iPad OS VPN profiles, these platforms aren't yet supported. Because the public preview doesn’t support iOS/iPadOS, VPN profiles for them with a connection type of Microsoft Tunnel won't function.



**End-user changes**:

On devices that install the new app as part of this preview, users can start using the Microsoft Defender for Endpoint app. The preview version of the Microsoft Defender for Endpoint app includes a new tab for the Microsoft Tunnel functionality.

## Licensing

The preview app combines functionality of Microsoft Defender for Endpoint with the functionality of the Microsoft Tunnel app. The new app doesn't require any change to your existing licenses.

A license for Microsoft Intune grants access to the following tab of the preview app:

- **Tunnel** is where users connect to the Tunnel Gateway and can view connection statistics and client configuration settings.

A license for Microsoft Defender for Endpoint grants access to the following tabs:

- **Dashboard** displays a summary of the device’s overall health, app security status, web protection status, and Tunnel status.
- **App security** is where users can view the status of automatic scans on the device. Users can also uninstall the apps identified as threats and run a manual scan.
- **Web Protection** shows the status of the feature enabled or disabled by administrators, and details of the feature described in the flip cards.

With both licenses, all four tabs are available.

:::image type="content" source="./media/microsoft-tunnel-migrate-app/defender-app-tabs.png" alt-text="Screenshot of the Defender for Endpoint tabs.":::

For information about license requirements for Microsoft Defender for Endpoint, see [Get Microsoft Defender for Endpoint](/windows/security/threat-protection/microsoft-defender-atp/switch-to-microsoft-defender-prepare#get-microsoft-defender-for-endpoint).

## Migrate devices to Microsoft Defender for Endpoint

After you sign up and have access to the preview version of Microsoft Defender for Endpoint, you can migrate supported devices from the Tunnel app to the new app. You can also deploy the preview app to other devices that haven't previously used the Microsoft Tunnel.

Migration to the preview of Microsoft Defender for Endpoint requires the following broad actions, which are described in the following sections:

1. Join the public preview.
2. Review and record your current Tunnel configurations.
3. Deploy the preview version of Microsoft Defender for Endpoint.
4. Create new VPN profiles.
5. Clean up your previous deployments.

### Join the Microsoft Defender for Endpoint public preview for Microsoft Tunnel

To gain access to the Microsoft Defender for Endpoint app that includes support for Microsoft Tunnel, you must opt into the public preview. That’s because the version of the app that’s available from the regular Google Play store doesn’t support the Microsoft Tunnel functionality. Only tenants that sign-up for the preview will have access to the preview app.

**To opt into the preview**:

Sign up at https://aka.ms/VPNpreview where you provide your Managed Google Play Organization ID and contact email.

After you sign up, you’ll be alerted by email when your tenant has access to the preview app. The email includes instructions for deploying the preview Microsoft Defender for Endpoint app from the Managed Google Play store.

### Review and record your current Tunnel configurations

Before you begin your migration to the preview, take the time to review and record the settings you currently use for the following Intune configurations:

- VPN profiles for Microsoft Tunnel
- App deployments of the Microsoft Tunnel

You'll use this information when you deploy new VPN profiles and the preview version of the Microsoft Defender for Endpoint app, to mirror your existing deployments.

1. Sign in to [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Devices** > **Configuration profiles**. Locate the VPN profiles you use for Microsoft Tunnel for your Android devices. They display a connection type of *Microsoft Tunnel (standalone client)*. You’ll replace these profiles with new profiles that use the preview app.

   1. Select each profile and then **Properties**.

   2. From Properties, record the available values. This information will help you create new VPN profiles that mirror your current configurations.

1. Next, record details for your Tunnel app deployments. In the admin center, go to **Apps**. Locate your deployments of Microsoft Tunnel to Android Enterprise devices.

   1. Select each applicable deployment and review its **Properties**.

   2. From Properties, record the available values. This information will help you to create similar deployments for the Microsoft Defender for Endpoint app.

### Deploy the preview version of Microsoft Defender for Endpoint

After receiving confirmation for the public preview, you can access and deploy the preview version of the Microsoft Defender for Endpoint app to your devices. This app is available from the Managed Google Play store.

1. Locate and **Approve** the app in the Managed Google Play store for your tenant, and then **Sync** it. For information on this process, see [Managed Google Play store apps](../apps/apps-add-android-for-work.md#managed-google-play-store-apps).

2. **Assign** the app to groups. While assigning the app, under App settings set **Tracks** to **SuperApp Public Preview**.

   Only **Available** deployments are supported for the public preview.
3. Complete the assignment, and then ask users to install the Microsoft Defender for Endpoint app.

### Create new VPN profiles

To enable devices to use Microsoft Defender for Endpoint to connect to Microsoft Tunnel Gateway, deploy new VPN profiles with the Microsoft Tunnel connection type. Editing the connection type of an existing profile isn’t supported.

1. Use the information from [Create a VPN Profile](../protect/microsoft-tunnel-configure.md#create-a-vpn-profile) to create and deploy new VPN profiles for your Android Enterprise devices.

2. During configuration, reference the settings you recorded from your existing profiles, but use a *connection type* of **Microsoft Tunnel**.

### Clean up previous deployments

After devices install the Microsoft Defender for Endpoint app and receive new VPN profiles, you can remove configurations for the original deployments.

For deployments of the original Microsoft Tunnel app:

1. Remove **Required** and **Available for enrolled devices**.

2. Add **Uninstall** to trigger removal of the application.

## Next Steps

[Use Conditional Access with the Microsoft Tunnel](microsoft-tunnel-conditional-access.md)  
[Monitor Microsoft Tunnel](microsoft-tunnel-monitor.md)
