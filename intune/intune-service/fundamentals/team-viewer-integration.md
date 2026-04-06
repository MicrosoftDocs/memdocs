---
title: Use the latest TeamViewer integration in Microsoft Intune 
description: Learn how to use the latest TeamViewer integration in Microsoft Intune to initiate remote assistance sessions for managed devices.
author: lenewsad
ms.author: lanewsad
ms.date: 04/07/2026
ms.topic: how-to
ms.collection:
- M365-identity-device-management
---

# Use the TeamViewer integration in Microsoft Intune  

> [!IMPORTANT]
> A new TeamViewer remote assistance experience is available in Intune and is described in this article. 
>
> Your old TeamViewer configurations remain available in the Microsoft Intune admin center under **TeamViewer connector (old)**. To use the new experience, you must set up the new connector under **TeamViewer connector**.  
>
> If both connectors are enabled, helpdesk agents see two options when starting a remote assistance session:  
> - **TeamViewer (old)**: Previous remote assistance experience  
> - **TeamViewer**: New remote assistance experience  
>
> For information about the previous connector, see [Use TeamViewer to remotely administer Intune devices](teamviewer-support.md).  

Devices managed by Microsoft Intune can be administered remotely using TeamViewer, a third-party remote assistance solution that you purchase separately. This article describes:

- How to configure the latest TeamViewer connector in the Intune admin center.  
- How to start a remote assistance session on a managed device using TeamViewer.  
- What data Intune shares with TeamViewer on behalf of your tenant to enable the remote assistance experience.  

This feature applies to:  

- Android (all enrollment options, including BYOD, COBO, COSU, COPE, AOSP, and DA)
- iOS/iPadOS  
- macOS  
- Windows   

> [!NOTE]
> TeamViewer isn't supported on GCC or GCC High environments.  

## Prerequisites  

Before you configure the TeamViewer connector in Intune, make sure the following requirements are met:

- TeamViewer account and license: Visit the [TeamViewer integration docs](https://www.teamviewer.com/en/integrations/microsoft-intune/)(opens the TeamViewer website) or contact the TeamViewer sales team for more information about account setup and required licenses.  

- Intune administrator license: The administrator configuring the TeamViewer connector must have an Intune license. You can give administrators access to Microsoft Intune without them requiring an Intune license. For more information, see [Unlicensed admins](../../fundamentals/licensing/unlicensed-admins.md).

- Intune roles and permissions: To onboard TeamViewer in the Microsoft Intune admin center, you must be assigned the *Remote assistance connectors/Read* permission and *Remote assistance connectors/Update* permission, or be an Intune Administrator. For more information, see [Role based access control](#role-based-access-control) in this article.  

The integration supports connections to TeamViewer‑managed devices that have the TeamViewer host or full client installed and are managed by your Intune tenant. Any connection settings, policies, or TeamViewer conditional access rules you configured will also apply to connections started from the integration. For more information, see [Getting started with Intune integration](https://www.teamviewer.com/link/?url=178709)(opens the TeamViewer website).  

## Configure the TeamViewer connector  

To enable remote assistance through TeamViewer, an Intune administrator must configure the TeamViewer connector in the Intune admin center. This connector establishes the connection between your Intune tenant and your TeamViewer environment.  

### Role based access control  

These Intune permissions allow you to delegate connector management and session initiation without granting full administrative access to Intune:  

- *Remote assistance connectors/Read*: View the connector status.
- *Remote assistance connectors/Read* and *Remote Tasks/Offer Remote assistance*: View the connector status and initiate TeamViewer sessions.  
- *Remote assistance connectors/Read* and *Remote assistance connectors/Update*: View and modify the connector configuration.  

If a user has *read* permission without *update* permission, they can still view the connector, but they can't edit any configurations. For more information about role requirements, see [Role-based access control (RBAC) with Microsoft Intune](role-based-access-control.md).  

### Optimize setup  

To ensure a seamless setup, you can configure Intune Sync in your TeamViewer company settings to match your Intune and TeamViewer device group setups. For more information, see [TeamViewer Intune Device Sync](https://www.teamviewer.com/link/?url=737977)(opens the TeamViewer website).  

To get the best experience while using the integration, we recommend you enable single sign-on (SSO) between TeamViewer and the Microsoft Entra identity provider.  

### Setup  
Complete these steps to integrate the TeamViewer connector with Microsoft Intune.   

1. Sign in to the Intune admin center as an Intune administrator or user with [sufficient permissions](#role-based-access-control).  
1. Go to **Tenant administration** > **Connectors and tokens** > **TeamViewer connector**.  
   > [!NOTE]
   > The new TeamViewer connector appears as **TeamViewer connector** in the admin center. The previous connector is now called **TeamViewer connector (old)**.  
1. On the TeamViewer connector page, flip the **Turn on TeamViewer connector** toggle to **On**. This toggle enables TeamViewer as a remote assistance option for your tenant.
1. Review the [Data shared with TeamViewer](#data-shared-with-teamviewer) section later in this article to understand the data that's sent to TeamViewer when the connector is enabled. 
1. The TeamViewer base URL is prefilled with `https://web.teamviewer.com/`, which is the appropriate URL for most companies. If your organization uses a specific TeamViewer region, enter the appropriate subdomain of the URL. This URL determines which TeamViewer environment Intune launches when a helpdesk user starts a remote assistance session.  
1. Select **Save** to apply the configuration. When the configuration is complete, a confirmation message appears and the connector status is updated.  

After the TeamViewer connector is enabled and saved:  
  - When authorized users select **New remote assistance session** on a device, TeamViewer is available as an option.  
  - Intune uses the configured TeamViewer URL each time it launches a session.  
  - Configuration changes and session launches are recorded in Intune audit logs for administrative visibility.  

## Remotely administer a device with TeamViewer  

Authorized support personnel can initiate a remote assistance session on a Microsoft Intune managed device through the Intune admin center. Session launches are recorded in the Intune audit logs. 

When a support technician starts a remote assistance session via Intune and TeamViewer, the connection is established on the device using the access policies, such as the Conditional Access rules, device policies, and access control settings, defined in your TeamViewer organizational settings.  

1. In the Intune admin center, go to **Devices** > **All devices**.
1. Select the device that needs remote assistance, and then choose **New Remote Assistance Session**.  
1. Select **TeamViewer**, and then select **Continue**.  
1. Intune opens a new browser tab and loads the TeamViewer URL with device identifiers. For information about these identifiers, see [Data shared with TeamViewer](#data-shared-with-teamviewer) in this article.  
1. From this point on, TeamViewer handles ownership of the experience, including authentication and session management. Complete the steps as prompted.  
1. Close the TeamViewer window to end the session.  

## Data shared with TeamViewer

The TeamViewer integration requires Intune to exchange a limited set of data with the TeamViewer service on behalf of your tenant. Data sharing is strictly to enable the remote assistance sessions that you initiate. This section describes the type of data shared.  

When a helpdesk agent launches a new remote assistance session to a device, Intune passes specific device identification data to TeamViewer as query parameters in the session URL,  which includes the base URL you configured for TeamViewer.  

| Data element              | Description                                                                                 |
|---------------------------|---------------------------------------------------------------------------------------------|
| Microsoft Entra device ID | A tenant-unique identifier for the device, used by TeamViewer to look up the device record. |
| Device name               | The device name of the Intune-registered device, used as a fallback if the Microsoft Entra device ID is unavailable. |  

## TeamViewer license and privacy terms  
For the TeamViewer license and privacy terms, see:  

- [TeamViewer End User License Agreement (EULA)](https://www.teamviewer.com/en/legal/eula/)(opens TeamViewer website)
- [TeamViewer Privacy Terms](https://www.teamviewer.com/en/legal/privacy-and-cookies/)(opens TeamViewer website)

## Get help  

Microsoft Intune supports the setup of TeamViewer remote assistance from the Microsoft Intune admin center. After you launch a remote assistance session, the experience is owned and supported by TeamViewer.  