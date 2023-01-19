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

To use the MAM Tunnel for iOS during the public preview, you must update your Line of Business (LOB) apps to integrate the following three SDKs. You’ll find guidance for integrating each SDK later in this article:

- [Intune App SDK for iOS](../developer/app-sdk-ios.md)
- [Microsoft Authentication Library](../developer/app-sdk-ios.md#setup-msal) (MSAL)
- Tunnel for MAM SDK for iOS

## Tunnel for MAM SDK for iOS Architecture

The following diagram describes the flow from a managed app that has successfully been integrated with Tunnel for MAM SKD for iOS. 
:::image type="content" source="./media/microsoft-tunnel-mam-ios/tunnel-for-mam-ios-flow.png" alt-text="Drawing of the Microsoft Tunnel Gateway for MAM on iOS architecture.":::

**Actions**:

- **0.** Upon initial launch of the app, a connection is made via the Tunnel for MAM SDK.
- **1.** An authentication token is required to authenticate.
  - **a.** The device may already have an Azure AD auth token obtained from a previous sign-in using another MAM enabled app on the device (like Outlook, Microsoft Edge, and Microsoft 365 Office mobile apps)
- **2.** A TCP Connect (TLS Handshake occurs with the token to the tunnel server
- **3.** If UDP is enabled on the Microsoft Tunnel Gateway, a data-channel connection using DTLS is made.  If UDP is disabled, then TCP is used to establish the data channel to Tunnel gateway.  See TCP, UDP notes in the [Microsoft Tunnel Architecture](../protect/microsoft-tunnel-overview.md#architecture)
- **4.** When the mobile app makes a connection to an on-premises corporate resource:
  - **a.** A Microsoft Tunnel for MAM API connect request for that company resource occurs.
  - **b.** An encrypted web request gets made to the corporate resource.

> [!NOTE]  
> Tunnel for MAM SDK for iOS provides VPN Tunnel. It’s scoped to the networking layer within the app.  VPN connections are not displayed in iOS settings.

## Configure Intune policies for Microsoft Tunnel for MAM iOS

MAM Tunnel for iOS uses the following Intune policies and profiles:

- App configuration policy - to configure apps to support account switching and enable the app to automatically connect and disconnect from the VPN tunnel.
- App protection policy - to configure the Microsoft Tunnel for apps that will use the MAM Tunnel for iOS.
- Trusted certificate profile - for Apps that connect to on-premises resources that are protected by an SSL/TLS certificate issued by an on-premises or private certificate authority (CA).

### Configure an app configuration policy

Create an app configuration policy for apps that will use Tunnel for MAM. This policy configures an app to support identity-switch and provides the ability to automatically connect the VPN Tunnel when signing-in or switching to a Microsoft "Work or school" account, and automatically disconnect the VPN tunnel when switching to a Microsoft personal account.

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and go to **Apps** > **App Configuration polices** > **Add** > **Managed Apps**.

2. On the *Basics* tab, enter a *Name* for the policy and a *Description* (optional).

3. For LOB apps, click on **+ Select custom apps** to open the *Select apps to target* pane. On the *Select apps to target* pane:

   1. For *Bundle or Package ID*, specify the LOB apps Bundle ID
   1. For *Platform*, select **iOS/iPadOS**, and then select **Add**.
   1. Select the app you just added, and then **Select**.

   > [!NOTE]  
   > LOB apps require Intune App SDK for iOS and MSAL integration. MSAL requires an Azure AD App registration.  Ensure the Bundle ID used in the App configuration policy is the same Bundle ID specified in the AAD App registration and the Xcode app project.

   After selecting an app, select **Next**.

   For more information about adding custom apps to policies, see [App configuration policies for Intune App SDK managed apps](../apps/app-configuration-policies-managed-app.md).

4. On the *Settings* tab, expand *Microsoft Tunnel for Mobile Application Management settings (Preview)* and configure the following options:

   1. Set *Use Microsoft Tunnel for MAM* to **Yes**.
   1. For *Connection name*, specify a user facing name for this connection, like *mam-tunnel-vpn*.
   1. Next, select **Select a Site**, and choose one of your Microsoft Tunnel Gateway sites. If you haven’t configured a Tunnel Gateway site, see [Configure Microsoft Tunnel](../protect/microsoft-tunnel-configure.md).
   1. If your app requires a trusted certificate, select **Root Certificate**, and then select a trusted certificate profile to use. For more information see [Configure a trusted certificate profile](#configure-a-trusted-certificate-profile) later in this article.

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

### Configure an app protection policy

An App protection policy is required to configure Microsoft Tunnel for apps that will use the MAM Tunnel for iOS.

This policy provides the necessary data protection and establishes a means of delivering app configuration policy to apps. To create an app protection policy, use the following steps:

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and go to **Apps** > **App protection policies** > **+ Create policy** >  and select **iOS/iPadOS**. 
2. On the *Basics* tab, enter a *Name* for the policy, and a *Description* (optional), and then select **Next**.
3. On the *Apps* tab:  
   1. Set *Target apps on all device types* to **No**.
   1. For *Device types*, select **Unmanaged**.

   :::image type="content" source="./media/microsoft-tunnel-mam-ios/app-protection-target-policy.png" alt-text="Configure the app protection policy to target unmanaged devices.":::

4. For LOB apps, click on **+ Select custom apps**  to open the *Select apps to target* pane. Next, on the *Select apps to target* pane:  
   1. For *Bundle ID*, specify the LOB apps Bundle ID and then select **Add**.
   1. Select the app you just added,  and then **Select**.

   :::image type="content" source="./media/microsoft-tunnel-mam-ios/app-protection-custom-lob-app.png" alt-text="Add the custom app to the app protection policy.":::

   > [!NOTE]  
   > LOB apps require Intune App SDK for iOS and MSAL integration. MSAL requires an Azure AD App registration.  Ensure the Bundle ID used in the App configuration policy is the same Bundle ID specified in the AAD App registration and the Xcode app project.

5. Configure any remaining app protection policy settings based on your deployment and data protection requirements using the *Data protection*, *Access requirements*, and *Conditional launch* tabs.

6. On the *Assignments* tab, select **Add Groups**, and then select one or more Azure AD user groups that will receive this policy. After configuring groups, select **Next**.

The new policy will appear in the list of App protection policies.

### Configure a trusted certificate profile

Apps that will use the MAM Tunnel to connect to an on-premises resource protected by an SSL/TLS certificate issued by an on-premises or private certificate authority (CA) require you to configure a *trusted certificate profile*. If your apps don't require this type of connection, you can skip this section, and not add the trusted certificate profile to the app configuration policy.

A trusted certificate profile is required to establish a chain of trust with your on-premises infrastructure and allows the device to trust the certificate that's used by the on-premises web or application server, ensuring secure communication between the app and the server.

Tunnel for MAM uses the public-key certificate payload contained in the Intune trusted certificate profile but doesn’t require the profile be assigned to any Azure AD user or device groups.  As a result, a trusted certificate profile for any platform can be used. This means that an iOS device can use a trusted certificate profile for Android, iOS, or Windows to meet this requirement.

During configuration of the app configuration profile for an app that will use Tunnel for MAM, you select the certificate profile that will be used. 
For information on configuring these profiles, see [Trusted root certificate profiles for Microsoft Intune](../protect/certificates-trusted-root.md). 

## Configure Line of Business apps in the Azure AD portal

Line of Business apps that use Microsoft Tunnel for MAM iOS require:

- A *Microsoft Tunnel Gateway* service principal Cloud app
- Azure AD App registration

### Microsoft Tunnel Gateway service principal

If not already created for Microsoft Tunnel MDM Conditional Access, you’ll need to provision the Microsoft Tunnel Gateway service principal Cloud app.  For guidance, see [Use Microsoft Tunnel VPN gateway with Conditional Access policies](../protect/microsoft-tunnel-conditional-acces.md#provision-your-tenant).

### Azure AD App registration

When integrating Tunnel for MAM SDK for iOS into a line-of-business app, the following App registration settings must match your Xcode app project:

- Application ID
- Tenant ID

Depending on your needs, choose one of the following options:

- [Create a new App registration](#create-a-new-app-registration)  
  If you have an iOS app that hasn’t been previously integrated with the Intune App SDK for iOS, or the Microsoft Authentication Library (MSAL), then you will need to create a new app registration. The steps to create a new App registration include:  

  - App registration.
  - Authentication configuration.
  - Adding API Permissions.
  - Token configuration.
  - Verify using Integration assistant

- [Update an existing App registration](#update-an-exiting-app-registration)  
  If you have an iOS app that has been previously integrated with the Intune App SDK for iOS, then you will need to update the existing app registration.

#### Create a new App registration

The Azure AD online docs provide detailed instruction and guidance on how to [create an App registration](/azure/active-directory/develop/howto-create-service-principal-portal#app-registration-app-objects-and-service-principals).

The following guidance is specific to requirements for Tunnel for MAM SDK for iOS integration.

1. In the [Azure AD portal](https://aad.portal.azure.com/) for your tenant, go to *Azure Active Directory*, and then under *Manage*, select **App registrations** > **+ New registration**.
2. On the *Register an application* page:
   - Specify a **Name**for the app registration 
   - Select **Account in this organizational directory only (*YOUR_TENANT_NAME only - Single tenant*)**.
   - A *Redirect URI* doesn't need to be provided at this time.
  
   Select **Register** button to complete the registration and opens an *Overview* page for the app registration.

3. On the *Overview* pane, note the values for *Application (client) ID* and the *Directory (tenant) ID*. These values are required for the app registrations Xcode project. After recording the two values, select under *Manage*, select **Authentication**.

4. On the *Authentication* pane for your app registration, select **+ Add a plaform**, and then select the tile for **iOS/macOS**. This will open the *Configure your iOS or macOS app* pane.  

   :::image type="content" source="./media/microsoft-tunnel-mam-ios/app-registration-authentication1.png" alt-text="Configure authentication for the app registration..":::

5. On the *Configure your iOS or macOS app* pane, Enter the *Bundle ID* for the Xcode app to be integrated with Tunnel for MAM SDK for iOS, and then select **Configure**. This opens the iOS/macOS configuration pane: 

   :::image type="content" source="./media/microsoft-tunnel-mam-ios/app-registration-configuration-pane.png" alt-text="Review the app registration configuration pane.":::


1






#### Update an existing App registration



## Next steps

- [Configure Microsoft Tunnel](../protect/microsoft-tunnel-configure.md)
- [Monitor Microsoft Tunnel](../protect/microsoft-tunnel-monitor.md)
- [MAM Tunnel for Android](../protect/microsoft-tunnel-mam-android.md)
