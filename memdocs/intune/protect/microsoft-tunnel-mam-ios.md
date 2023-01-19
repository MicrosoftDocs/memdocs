---
title: Use Microsoft Tunnel VPN with iOS/iPad devices that don't enroll with Microsoft Intune
description: Add support for Mobile Application Management (MAM) for iOS to the Microsoft Tunnel Gateway. Tunnel support for MAM expands access to your organizational resources for devices that can't or haven't enrolled with Microsoft Intune
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 01/18/2023
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

# Microsoft Tunnel for Mobile Application Management for iOS/iPadOS (public preview)

In public preview, you can use Microsoft Tunnel VPN Gateway with unenrolled iOS devices to support Mobile Application Management (MAM) scenarios. With support for MAM, your unenrolled devices can use Tunnel to securely connect to your organization allowing users and apps safe access to your organizational data.

Applies to:

- iOS/iPadOS

> [!NOTE]
> While in public preview, Microsoft Tunnel for MAM is available at no additional cost. When Tunnel for MAM becomes generally available, it will be available as a [**premium add-on**](/fundamentals/premium-add-ons.md) and require an additional cost to the licensing options that include Microsoft Endpoint Manager or Intune.

MAM Tunnel for iOS is a powerful tool that allows organizations to securely manage and protect their mobile applications. The VPN connection for this solution is provided through the Microsoft Tunnel for MAM SDK for iOS.

To use the MAM Tunnel for iOS during the public preview, you must update your Line of Business (LOB) apps to integrate the following three SDK’s. You’ll find guidance for integrating each SDK later in this article:

- [Intune App SDK for iOS](../developer/app-sdk-ios)
- [Microsoft Authentication Library](../developer/app-sdk-ios#setup-msal) (MSAL)
- Tunnel for MAM SDK for iOS

## Tunnel for MAM SDK for iOS Architecture

The following diagram describes the flow from a managed app that has successfully been integrated with Tunnel for MAM SKD for iOS. 
:::image type="content" source="./media/microsoft-tunnel-mam-ios/tunnel-for-mam-ios-flow.png" alt-text="Drawing of the Microsoft Tunnel Gateway for MAM on iOS architecture.":::

**Actions**:

- **0.** Upon initial launch of the app a connection is made via the Tunnel for MAM SDK.
- **1.** An authentication token is required to authenticate.
  - **a.** The device may already have an AAD auth token obtained from a previous login using another MAM enabled app on the device (i.e., Outlook, Edge, M365 Office mobile apps)
- **2.** A TCP Connect (TLS Handshake occurs with the token to the tunnel server
- **3.** If UDP is enabled on the Microsoft Tunnel Gateway, a data-channel connection using DTLS is made.  If UDP is disabled, then TCP is used to establish the data channel to Tunnel gateway.  See TCP, UDP notes in the [Microsoft Tunnel Architecture](../protect/microsoft-tunnel-overview.md#architecture)
- **4.** When the mobile app makes a connection to an on-premises corporate resource:
  - **a.** A MS Tunnel for MAM API connect request for that company resource occurs.
  - **b.** An encrypted web request gets made to the corporate resource.

> [!NOTE]  
> Tunnel for MAM SDK for iOS provides VPN Tunnel. It’s scoped to the networking layer within the app.  VPN connections are not displayed in iOS settings.

## Configure Microsoft Tunnel for MAM iOS

Configuration of MAM Tunnel for iOS requires the following steps:


### Configure an app configuration policy

Create an app configuration policy for apps that will use Tunnel for MAM. This policy configures an app to support identity-switch, providing the ability to automatically connect the VPN Tunnel when signing-in or switching to a Microsoft "Work or school" account, and automatically disconnect the VPN tunnel when switching to a Microsoft personal account.

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and go to **Apps** > **App Configuration polices** > **Add** > **Managed Apps**.

2. On the *Basics* tab, enter a *Name* for the policy and a *Description* (optional).

3. For LOB apps, click on Select custom apps to open the *Select apps to target* pane., then on the *Select apps to target* pane:

   1. For *Bundle or Package ID*, specify the LOB apps Bundle ID
   1. For *Platform*, select **iOS/iPadOS*, and then click **Add**.
   1. Select the app you just added, and then **Select**.

   > [!NOTE]  
   > LOB apps require Intune App SDK for iOS and MSAL integration. MSAL requires an Azure AD App registration.  Ensure the Bundle ID used in the App configuration policy is the same Bundle ID specified in the AAD App registration and the Xcode app project.

   After selecting an app, select **Next**.

   For more information about adding custom apps to policies, see [App configuration policies for Intune App SDK managed apps](../apps/app-configuration-policies-managed-app.md).

4. On the *Settings* tab, expand *Microsoft Tunnel for Mobile Application Management settings (Preview)* and configure the following. 

   1. Set *Use Microsoft Tunnel for MAM* to **Yes**.
   1. For *Connection name*, specify a user facing name for this connection, like *mam-tunnel-vpn*.
   1. Next, select **Select a Site**, and choose one of your Microsoft Tunnel Gateway sites. If you haven’t configured a Tunnel Gateway site, see [Configure Microsoft Tunnel](../protect/microsoft-tunnel-configure.md).
   1. If your app requires a trusted certificate, select **Root Certificate** and then select a trusted certificate profile to use.

   > [!NOTE]
   > MAM Tunnel for iOS doesn’t use the following:  
   > - The *General configuration settings* category.
   > - Per-App VPN. The Tunnel for MAM SDK for iOS provides Per-App VPN directly to integrated apps.
   >
   > Additionally, the Public Preview doesn’t support use of a Proxy automatic configuration script (PAC).

   After configuring the Tunnel MAM settings, Select **Next** to open the *Assignments* tab.

5. On the *Assignments* tab, select **Add Groups**, and then select one or more Azure AD user groups that will receive this policy. After configuring groups, select **Next**.

6. On the *Review + Create* tab, select **Create** to complete creation of the policy and deploy the policy to the assigned groups.

The new policy will appear in the list of App configuration policies.





## Next steps

- [Configure Microsoft Tunnel](../protect/microsoft-tunnel-configure.md)
- [Monitor Microsoft Tunnel](../protect/microsoft-tunnel-monitor.md)
- [MAM Tunnel for Android](../protect/microsoft-tunnel-mam-android.md)
