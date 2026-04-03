---
title: Use the TeamViewer integration in Microsoft Intune 
description: Learn how to use the TeamViewer integration in Microsoft Intune to initiate remote assistance sessions for managed devices.
author: lenewsad
ms.author: lanewsad
ms.date: 04/07/2026
ms.topic: how-to
ms.collection:
- M365-identity-device-management
---

# Use the TeamViewer integration in Microsoft Intune  

> [!IMPORTANT]
> A new TeamViewer remote assistance experience is available in Intune. This article describes the new integration. If you’re using the previous TeamViewer connector, see [Use TeamViewer to remotely administer Intune devices](teamviewer-support.md).  

Devices managed by Microsoft Intune can be administered remotely using TeamViewer, a third-party remote assistance solution that you purchase separately. This article describes how to configure the new TeamViewer connector in the Intune admin center, how to start a remote assistance session on a managed device using TeamViewer, and what data Intune shares with TeamViewer on behalf of your tenant to enable the remote assistance experience.  

This feature applies to:  

- All Android Device Enrollment options: BYOD, COSU, COBO, COPE, AOSP and DA.
- iOS/iPadOS
- macOS
- Windows

## TeamViewer license and privacy terms

- [TeamViewer End User License Agreement (EULA)](https://www.teamviewer.com/en/legal/eula/)
- [TeamViewer Privacy Terms](https://www.teamviewer.com/en/legal/privacy-and-cookies/)

An eligible TeamViewer license is required in order to use the TeamViewer integration. Visit the [TeamViewer Integration web page](https://www.teamviewer.com/en/integrations/microsoft-intune/) or contact the TeamViewer sales team for more information about required licenses.  

> [!NOTE]
> TeamViewer isn't supported on GCC or GCC High environments.

## Prerequisites

Before you configure the TeamViewer connector in Intune, make sure the following requirements are met:

- **Intune administrator license:**  
  The administrator configuring the TeamViewer connector must have an Intune license. You can give administrators access to Microsoft Intune without them requiring an Intune license. For more information, see [Unlicensed admins](../../fundamentals/licensing/unlicensed-admins.md).

- **Intune roles and permissions:**  
  Users must be assigned the Remote assistance connectors/Read and Remote assistance connectors/Update permissions (or the Intune Administrator or Global Administrator role) in the Intune admin center to onboard TeamViewer. For more information, see [Role-based access control (RBAC) with Microsoft Intune](role-based-access-control.md).

- **TeamViewer account and license:**  
  A licensed [TeamViewer](https://www.teamviewer.com/) account. Only some TeamViewer licenses support integration with Intune. For more information, see the [TeamViewer Intune Integration overview](https://www.teamviewer.com/integrations/microsoft-intune/)(opens the TeamViewer website).  

The integration supports connections to TeamViewer Managed Devices that have been managed by your TeamViewer company with an installed TeamViewer Host or Full Client. Any connection settings, policies or TeamViewer Conditional Access rules you have configured will also apply to connections started from the integration. For more information, see [Getting Started with Intune Integration](https://www.teamviewer.com/link/?url=178709)(opens the TeamViewer website).

>[!TIP]
> To ensure a seamless setup, you can configure Intune Sync in your TeamViewer company settings to match your Intune and TeamViewer device group setups. For more information, see [TeamViewer Intune Device Sync](https://www.teamviewer.com/link/?url=737977)(opens the TeamViewer website).  

>[!TIP]
> To get the best experience while using the integration, we recommend you enable single sign-on (SSO) between TeamViewer and Microsoft Entra identity provider.  

## Configure the TeamViewer connector

To enable remote assistance through TeamViewer, an Intune administrator must configure the TeamViewer connector in the Intune admin center. This connector establishes the connection between your Intune tenant and your TeamViewer environment.  

### Before you begin  

- Confirm that your organization has an active TeamViewer license that supports the new Microsoft Intune integration.  
- Ensure you're signed in with an account that has permissions.
- Users with **Remote assistance connectors / Read** permission can view the connector status.
- Users with **Remote assistance connectors / Read** and **Remote Tasks/Offer Remote assistance** permissions can view the connector status and initiate TeamViewer sessions.
- Users with **Remote assistance connectors / Read** and **Remote assistance connectors / Update** permissions can view and modify the connector configuration.
- If a user has **Read** permission without **Update**, they can still view the connector, but they may not edit any configurations.
- These permissions allow you to delegate connector management and session initiation without granting full administrative access to Intune.
- If your tenant previously used the older TeamViewer connector, see [Migration from the previous TeamViewer connector](#migration-from-the-previous-teamviewer-connector).

### Step-by-step configuration

1. Sign in to the Intune admin center with an account that has permissions.
2. Navigate to the TeamViewer connector by selecting **Tenant administration > Connectors and tokens > TeamViewer connector**.
   > [!NOTE]
   > The new TeamViewer connector is named **TeamViewer connector** and the previous one has changed to **TeamViewer connector (old)**.
3. On the TeamViewer connector page, flip the **Turn on TeamViewer connector** toggle to **On**. This toggle enables TeamViewer as a remote assistance option for your tenant.
4. Review the [Data shared with TeamViewer](#data-shared-with-teamviewer) section later in this article to understand the data that will be sent to TeamViewer when this connector is enabled.
5. When the toggle is enabled, configure the TeamViewer base URL. It's automatically prefilled with `https://web.teamviewer.com/`, which is the correct choice for most companies. If your organization uses a specific TeamViewer region, enter the appropriate subdomain of the URL. This URL determines which TeamViewer environment Intune launches when a helpdesk user starts a remote assistance session.
6. Select **Save** to apply the configuration. When the configuration is saved successfully, a confirmation message appears and the connector status is updated.

After the TeamViewer connector is enabled and saved:  
  - When authorized users select **New remote assistance session** on a device, TeamViewer is available as an option.  
  - Intune uses the configured TeamViewer URL each time it launches a session.  
  - Configuration changes and session launches are recorded in Intune audit logs for administrative visibility.  

## Remotely administer a device using TeamViewer

Once the TeamViewer connector is configured, authorized support personnel can initiate a remote assistance session to an Intune managed device through the Intune admin center. Session launches are recorded in the Intune audit logs.

1. In the Microsoft Intune admin center, go to **Devices > All devices**.
2. Select a device and choose **New Remote Assistance Session**.
3. Select **TeamViewer**, and then select **Continue**.
4. Intune opens a new browser tab and loads the TeamViewer URL with device identifiers.
5. From this point on, TeamViewer handles ownership of experience including authentication and session management. Complete the steps as prompted.  
6. Close the TeamViewer window to end the session.    

## End user experience

When a support technician starts a remote assistance session via Intune and TeamViewer, the connection is established using the access policies, such as the Conditional Access rules, device policies, and access control settings, defined in your TeamViewer organizational settings.  

## Data shared with TeamViewer

This TeamViewer integration requires Intune to exchange a limited set of data with the TeamViewer service on behalf of your tenant. This data sharing is strictly to enable the remote assistance sessions that you initiate.

### During session creation

When a helpdesk agent launches a new remote assistance session to a device, Intune passes specific device identification data to TeamViewer as query parameters in the session URL which includes the base URL you configured for TeamViewer.

| Data element              | Description                                                                                 |
|---------------------------|---------------------------------------------------------------------------------------------|
| Microsoft Entra Device ID | A tenant unique identifier for the device, used by TeamViewer to look up the device record. |
| Device Name               | The device name of the Intune registered device, used as a fallback if Entra Device ID isn't available. |

## Migration from the previous TeamViewer connector

If you previously configured the TeamViewer connection in Intune, the existing connector has been renamed **TeamViewer connector (old)**. A new connector is now available as **TeamViewer connector**, which must be set up to enable the new experience.

If both connectors are enabled, helpdesk agents will see two TeamViewer options when starting a remote assistance session: **TeamViewer (old)** for the existing experience and **TeamViewer** for the new experience.

## Where to get help

Microsoft Intune supports the setup of TeamViewer Remote assistance from the Intune admin center. After you launch a remote assistance session, the experience is owned and supported by TeamViewer.  