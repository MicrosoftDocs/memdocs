---
title: Use Microsoft Tunnel VPN with iOS/iPad devices that don't enroll with Microsoft Intune
description: Add support for Mobile Application Management (MAM) for iOS to the Microsoft Tunnel Gateway. Tunnel support for MAM expands access to your organizational resources for devices that can't or haven't enrolled with Microsoft Intune. Admins should use this article to create policies that support per-app VPN in line of business (LOB) apps.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 01/08/2025
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
# optional metadata

#ROBOTS:
#audience:
 
ms.reviewer: ochukwunyere
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
- sub-intune-suite
---

# Microsoft Tunnel for Mobile Application Management for iOS/iPadOS

[!INCLUDE [intune-add-on-note](../includes/intune-add-on-note.md)]

When you add Microsoft Tunnel for Mobile Application Management (MAM) to your tenant, you can use Microsoft Tunnel VPN Gateway with unenrolled iOS devices to support MAM the following scenarios:

- Provide secure access to on-premises resources using modern authentication, single sign-on (SSO), and Conditional Access.
- Allow end users to use their personal device to access company on-premises resources. MDM (Mobile Device Management) enrollment isn't required and company data stays protected.
- Allow organizations to adopt a bring-your-own-device (BYOD) program. BYOD or personal devices reduce the overall total cost of ownership, ensure user privacy, and corporate data remains protected on these devices.

Applies to:

- iOS/iPadOS

Tunnel for MAM iOS is a powerful tool that allows organizations to securely manage and protect their mobile applications. The VPN connection for this solution is provided through the [Microsoft Tunnel for MAM iOS SDK](../developer/tunnel-mam-ios-sdk.md).

In addition to using MAM Tunnel with unenrolled devices, you can also use it with enrolled devices. However, an enrolled device must use either the MDM Tunnel configurations or the MAM Tunnel configurations, but not both. For example, enrolled devices can't have an app like Microsoft Edge that uses MAM tunnel configurations while other apps use MDM Tunnel configurations.

**Try the interactive demo**  
The [Microsoft Tunnel for Mobile Application Management for iOS/iPadOS]( https://regale.cloud/Microsoft/viewer/1976/microsoft-tunnel-for-mobile-application-management-for-ios-ipados/index.html#/0/0) interactive demo shows how Tunnel for MAM extends the Microsoft Tunnel VPN Gateway to support iOS and iPadOS devices not enrolled with Intune.

## Government cloud support

Microsoft Tunnel for MAM on iOS/iPadOS is supported with the following sovereign cloud environments:

- U.S. Government Community Cloud (GCC) High
- U.S. Department of Defense (DoD)

Microsoft Tunnel for MAM on iOS/iPadOS doesn't support Federal Information Processing Standard (FIPS).

For more information, see [Microsoft Intune for US Government GCC service description](../fundamentals/intune-govt-service-description.md).

## Required SDKs for iOS

To use the Microsoft Tunnel for MAM iOS, you must update your Line of Business (LOB) apps to integrate the following three SDKs. Find guidance for integrating each SDK later in this article:

- [Intune App SDK for iOS](../developer/app-sdk-ios.md)
- [Microsoft Authentication Library](../developer/app-sdk-ios-phase2.md) (MSAL)
- [Tunnel for MAM iOS SDK](../developer/tunnel-mam-ios-sdk.md)

## Tunnel for MAM iOS SDK Architecture

The following diagram describes the flow from a managed app that has successfully been integrated with Tunnel for MAM SDK for iOS.

:::image type="content" source="./media/microsoft-tunnel-mam-ios/tunnel-for-mam-ios-flow.png" alt-text="Drawing of the Microsoft Tunnel Gateway for MAM on iOS architecture.":::

### Actions

0. Upon initial launch of the app, a connection is made via the Tunnel for MAM SDK.  
1. An authentication token is required to authenticate.  
    1. The device might already have a Microsoft Entra auth token obtained from a previous sign-in using another MAM enabled app on the device (like Outlook, Microsoft Edge, and Microsoft 365 Office mobile apps).  
2. A TCP Connect (TLS Handshake) occurs with the token to the tunnel server.  
3. If UDP is enabled on the Microsoft Tunnel Gateway, a data-channel connection using DTLS is made.  If UDP is disabled, then TCP is used to establish the data channel to Tunnel gateway.  See TCP, UDP notes in the [Microsoft Tunnel Architecture](../protect/microsoft-tunnel-overview.md#architecture).  
4. When the mobile app makes a connection to an on-premises corporate resource:  
   1. A Microsoft Tunnel for MAM API connect request for that company resource occurs.
   2. An encrypted web request gets made to the corporate resource.

> [!NOTE]  
> The Tunnel for MAM iOS SDK provides VPN Tunnel. It's scoped to the networking layer within the app. VPN connections are not displayed in iOS settings.
>
> Each active line-of-business (LOB) app that's integrated with Tunnel for MAM iOS-SDK and that runs in the foreground represents an active client connection on the Tunnel Gateway server. The mst-cli command line tool can be used to monitor active client connections. For information about the mst-cli command-line tool, see [Reference for Microsoft Tunnel Gateway](../protect/microsoft-tunnel-reference.md).

## Configure Intune policies for Microsoft Tunnel for MAM iOS

Microsoft Tunnel for MAM iOS uses the following Intune policies and profiles:

- **App configuration policy** - Configures the Microsoft Tunnel Gateway settings for Edge and LOB apps. You can add any trusted certificates required for on-premises resource access.
- **App protection policy** - Configures data protection settings. It also establishes a way to deploy an app configuration policy that configures the Microsoft Tunnel settings for Edge and LOB apps.
- **Trusted certificate profile** - For apps that connect to on-premises resources and are protected by an SSL/TLS certificate issued by an on-premises or private certificate authority (CA).

### Configure an app configuration policy for LOB apps

Create an app configuration policy for apps that use Tunnel for MAM. This policy configures an app to use a specific Microsoft Tunnel Gateway Site, proxy, and trusted certificate(s) for Edge and line-of-business (LOB) apps. These resources are used when connecting to on-premises resources.

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and go to **Apps** > **Configuration** > **Create** > **Managed Apps**.

2. On the *Basics* tab, enter a *Name* for the policy and a *Description* (optional).

3. For LOB apps, select **+ Select custom apps** to open the *Select apps to target* pane. On the *Select apps to target* pane:

   1. For *Bundle or Package ID*, specify the LOB apps Bundle ID
   1. For *Platform*, select **iOS/iPadOS**, and then select **Add**.
   1. Select the app you just added, and then **Select**.

   > [!NOTE]  
   > LOB apps require Intune App SDK for iOS and MSAL integration. MSAL requires a Microsoft Entra app registration.  Ensure the Bundle ID used in the App configuration policy is the same Bundle ID specified in the Microsoft Entra app registration and the Xcode app project. Xcode is the Apple Integrated Developer Environment that that runs on macOS and used to integrate the Tunnel for MAM iOS SDK with your app.
   >
   > To get the bundle ID of an app added to Intune, [you can use the Intune admin center](../apps/get-app-bundle-id-intune-admin-center.md).

   After selecting an app, select **Next**.

   For more information about adding custom apps to policies, see [App configuration policies for Intune App SDK managed apps](../apps/app-configuration-policies-managed-app.md).

4. On the *Settings* tab, expand *Microsoft Tunnel for Mobile Application Management settings and configure the following options:

   > [!NOTE]  
   > When configuring proxy and split tunneling:
   > -  A proxy automatic configuration script (PAC) file allows you to enable both split tunneling and proxy.
   > -  It is not supported to enable both split tunneling and proxy when using proxy address or port number. All traffic will go through the proxy if the included routes have the proxy server configured. If the included routes do not have the proxy server configured, then all traffic will be excluded from using the tunnel.


   1. Set *Use Microsoft Tunnel for MAM* to **Yes**.
   1. For *Connection name*, specify a user facing name for this connection, like *mam-tunnel-vpn*.
   1. Next, select **Select a Site**, and choose one of your Microsoft Tunnel Gateway sites. If you haven't configured a Tunnel Gateway site, see [Configure Microsoft Tunnel](../protect/microsoft-tunnel-configure.md).
   1. If your app requires a trusted certificate, select **Root Certificate**, and then select a trusted certificate profile to use. For more information, see [Configure a trusted certificate profile](#configure-a-trusted-certificate-profile) later in this article.

   For federated Microsoft Entra tenants, the following configurations are required to ensure that your applications can authenticate and access the required resources. This configuration bypasses the URL of the publicly available secure token service:

   1. On the *Settings* tab, expand *General configuration settings* and then configure the *Name* and *Value* pair as follows to set up the Edge profile for Tunnel:

      - **Name** =  `com.microsoft.tunnel.custom_configuration`
      - **Value** = `{"bypassedUrls":["Company'sSTSURL"]}`

   > [!NOTE]  
   > The bypassedUrl should include the federation STS endpoint.

   :::image type="content" source="./media/microsoft-tunnel-mam-ios/ios-bypass.png" alt-text="Image that shows the name and value pair.":::

   For example, *Value* might appear as **{"bypassedUrls":["ipcustomer.com", "whatsmyip.org"]}**.

   After configuring the Tunnel MAM settings, Select **Next** to open the *Assignments* tab.

5. On the *Assignments* tab, select **Add Groups**, and then select one or more Microsoft Entra user groups that will receive this policy. After configuring groups, select **Next**.

6. On the *Review + Create* tab, select **Create** to complete creation of the policy and deploy the policy to the assigned groups.

The new policy appears in the list of App configuration policies.

### Configure an app configuration policy for Microsoft Edge

Create an App configuration policy for Microsoft Edge. This policy configures Edge on the device to connect to Microsoft Tunnel.

> [!NOTE]  
> If you already have an app configuration policy created for your LOB App, you can edit that policy to include Edge and the required *key/value pair* settings.

1. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Apps** > **Configuration** > **Create** > **Managed Apps**.

2. On the *Basics* tab:

    1. Enter a *Name* for the policy and a *Description* (optional).
    2. Click on **Select public apps**, select **Microsoft Edge for iOS/iPadOS**, and then click **Select**.
    3. After *Microsoft Edge* is listed for *Public apps*, select **Next**.

3. On the *Settings* tab, expand *General configuration settings* and then configure the *Name* and *Value* pair as follows to set up the Edge profile for Tunnel:

    | Name | Description |
    | --- | --- |
    | `com.microsoft.intune.mam.managedbrowser.StrictTunnelMode` <br/><br/> **Value**: `True` | When set to `True`, it provides **Strict Tunnel Mode** support to Edge. When users sign into Edge with an organization account, if the VPN isn't connected, then **Strict Tunnel Mode** blocks internet traffic. <br/><br/> When the VPN reconnects, internet browsing is available again. |
    | `com.microsoft.intune.mam.managedbrowser.TunnelAvailable.IntuneMAMOnly`<br/><br/> **Value**: `True` | When set to `True`, it provides **Identity switch** support to Edge. <br/><br/> When users sign in with **Work account or School account**, Edge automatically connects to the VPN. When users enable in-private browsing, Edge switches to a **Personal account** and disconnects the VPN. |
    | &nbsp; | &nbsp; |
    | **Federated Microsoft Entra tenants only** | &nbsp; |
    | `com.microsoft.tunnel.custom_configuration` <br/><br/> **Value**: `{"bypassedUrls":["Company'sSTSURL"]}` | Used by federated Microsoft Entra tenants. To make sure that Edge can authenticate and access required resources, this setting is required. It bypasses the URL of the publicly available secure token service. <br/> <br/> The `bypassedUrl` value should include the federation STS endpoint. For example, the value might be like `{"bypassedUrls":["ipcustomer.com", "whatsmyip.org"]}`. |

    The following image shows the `bypassedUrl` setting in an app configuration policy for Microsoft Edge:

    :::image type="content" source="./media/microsoft-tunnel-mam-ios/ios-bypass.png" alt-text="Image that shows the bypassedUrls configuration key and value for MAM Tunnel on unmanaged iOS devices in Microsoft Intune.":::

   > [!NOTE]  
   > Ensure there are no trailing spaces at the end of the General configuration settings.

   You can use this same policy to configure other Microsoft Edge configurations in the *Microsoft Edge configuration settings* category. After any additional configurations for Microsoft Edge are ready, select **Next**.

4. On the *Assignments* tab, select **Add Groups**, and then select one or more Microsoft Entra groups that will receive this policy. After configuring groups, select **Next**.

5. On the *Review + Create tab*, select **Create** to complete creation of the policy and deploy the policy to the assigned groups.

### Configure an app protection policy

An App protection policy is required to configure Microsoft Tunnel for apps that use the Microsoft Tunnel for MAM iOS.

This policy provides the necessary data protection and establishes a means of delivering app configuration policy to apps. To create an app protection policy, use the following steps:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and go to **Apps** > **Protection** > **+ Create policy** >  and select **iOS/iPadOS**.
2. On the *Basics* tab, enter a *Name* for the policy, and a *Description* (optional), and then select **Next**.
3. On the *Apps* tab, for LOB apps, select **+ Select custom apps**  to open the *Select apps to target* pane. Then, on the *Select apps to target* pane:  
   1. For *Bundle ID*, specify the LOB apps Bundle ID and then select **Add**.
   1. Select the app you just added,  and then **Select**.

   :::image type="content" source="./media/microsoft-tunnel-mam-ios/app-protection-custom-lob-app.png" alt-text="Add the custom app to the app protection policy.":::

   > [!NOTE]  
   > LOB apps require Intune App SDK for iOS and MSAL integration. MSAL requires a Microsoft Entra app registration.  Ensure the Bundle ID used in the App configuration policy is the same Bundle ID specified in the Microsoft Entra app registration and the Xcode app project.
   >
   > To get the bundle ID of an app added to Intune, [you can use the Intune admin center](../apps/get-app-bundle-id-intune-admin-center.md).

5. In the *Data protection*, *Access requirements*, and *Conditional launch* tabs, configure any remaining app protection policy settings based on your deployment and data protection requirements.

6. On the *Assignments* tab, select **Add Groups**, and then select one or more Microsoft Entra user groups that will receive this policy. After configuring groups, select **Next**.

The new policy appears in the list of App protection policies.

### Configure a trusted certificate profile

Apps that use the MAM Tunnel to connect to an on-premises resource protected by an SSL/TLS certificate issued by an on-premises or private certificate authority (CA) require a *trusted certificate profile*. If your apps don't require this type of connection, then you can skip this section. The trusted certificate profile isn't added to the app configuration policy.

A trusted certificate profile is required to establish a chain of trust with your on-premises infrastructure. The profile allows the device to trust the certificate that's used by the on-premises web or application server, ensuring secure communication between the app and the server.

Tunnel for MAM uses the public-key certificate payload contained in the Intune trusted certificate profile but doesn't require the profile be assigned to any Microsoft Entra user or device groups. As a result, a trusted certificate profile for any platform can be used. So, an iOS device can use a trusted certificate profile for Android, iOS, or Windows to meet this requirement.

> [!IMPORTANT]
> Tunnel for MAM iOS SDK requires that trusted certificates use the **DER encoded binary X.509 or PEM** certificate format.

During configuration of the app configuration profile for an app that will use Tunnel for MAM, you select the certificate profile that is used.
For information on configuring these profiles, see [Trusted root certificate profiles for Microsoft Intune](../protect/certificates-trusted-root.md).

## Configure Line of Business apps in the Microsoft Entra admin center

Line of Business apps that use Microsoft Tunnel for MAM iOS require:

- A *Microsoft Tunnel Gateway* service principal Cloud app
- Microsoft Entra app registration

### Microsoft Tunnel Gateway service principal

If not already created for Microsoft Tunnel MDM Conditional Access, provision the Microsoft Tunnel Gateway service principal Cloud app. For guidance, see [Use Microsoft Tunnel VPN gateway with Conditional Access policies](../protect/microsoft-tunnel-conditional-access.md#provision-your-tenant).

### Microsoft Entra app registration

When you integrate the Tunnel for MAM iOS SDK into a line-of-business app, the following app registration settings must match your Xcode app project:

- Application ID
- Tenant ID

Depending on your needs, choose one of the following options:

- [Create a new app registration](#create-a-new-app-registration)  
  If you have an iOS app that hasn't been previously integrated with the Intune App SDK for iOS, or the Microsoft Authentication Library (MSAL), then you need to create a new app registration. The steps to create a new app registration include:  

  - App registration
  - Authentication configuration
  - Adding API Permissions
  - Token configuration
  - Verify using Integration assistant

- [Update an existing app registration](#update-an-existing-app-registration)  
  If you have an iOS app that previously integrated with the Intune App SDK for iOS, then you need to review and update the existing app registration.

#### Create a new app registration

The Microsoft Entra online docs provide detailed instruction and guidance on how to [create an app registration](/azure/active-directory/develop/howto-create-service-principal-portal#app-registration-app-objects-and-service-principals).

The following guidance is specific to requirements for the Tunnel for MAM iOS SDK integration.

1. In the [Microsoft Entra admin center ](https://entra.microsoft.com/) for your tenant, expand **Applications**, and then select **App registrations** > **+ New registration**.
2. On the *Register an application* page:
   - Specify a **Name for the app registration
   - Select **Account in this organizational directory only (*YOUR_TENANT_NAME only - Single tenant*)**.
   - A *Redirect URI* doesn't need to be provided at this time. One is created automatically during a later step.
  
   Select **Register** button to complete the registration and opens an *Overview* page for the app registration.

3. On the *Overview* pane, note the values for *Application (client) ID* and the *Directory (tenant) ID*. These values are required for the app registrations Xcode project. After recording the two values, select under *Manage*, select **Authentication**.

4. On the *Authentication* pane for your app registration, select **+ Add a platform**, and then select the tile for **iOS/macOS**. The *Configure your iOS or macOS app* pane opens.

   :::image type="content" source="./media/microsoft-tunnel-mam-ios/app-registration-authentication1.png" alt-text="Configure authentication for the app registration.":::

5. On the *Configure your iOS or macOS app* pane, Enter the *Bundle ID* for the Xcode app to be integrated with the Tunnel for MAM iOS SDK, and then select **Configure**. The iOS/macOS configuration pane opens.

   :::image type="content" source="./media/microsoft-tunnel-mam-ios/app-registration-configuration-pane.png" alt-text="Review the app registration configuration pane.":::

   The *Bundle ID* in this view must exactly match the *Bundle ID* in Xcode. This detail can be found in the following locations in the Xcode project:

   - info.plist > IntuneMAMSettings: ADALRedirectUri
   - Project > General > Identity: Bundle ID

   A *Redirect URI* and *MSAL Configuration* are automatically generated. Select **Done** at the bottom of the dialog window to finish.  No other settings are required for *Authentication*.

6. Next, while viewing the app registration, select **API permissions** and then  **+ Add a permission**. Add the API permissions for *Microsoft Mobile Application Management* and *Microsoft Tunnel Gateway*:

   - On the *Request API permissions* page, select the tab for **APIs my organization uses**.
   - Search for *Microsoft Mobile Application Management*, select the result, and then select the checkbox.
   - Select **Add permissions**.
     :::image type="content" source="./media/microsoft-tunnel-mam-ios/request-api-permissions1.png" alt-text="Configure API permissions for Microsoft Mobile Application Management.":::

   Next, repeat the process for the second permission:
   - Select **+ Add a permission** and go to the **APIs my organization uses** tab.
   - Search for *Microsoft Tunnel Gateway*, select the result, and then select the checkbox for *Tunnel Allow*.
   - Select **Add permissions**.
     :::image type="content" source="./media/microsoft-tunnel-mam-ios/request-api-permissions2.png" alt-text="Configure API permissions for Microsoft Tunnel Gateway.":::

   To complete the configuration, return to the *API permissions* pane and select **Grant admin consent for YOUR_TENANT**, and then select **Yes**.

   :::image type="content" source="./media/microsoft-tunnel-mam-ios/grant-api-permissions-consent.png" alt-text="Grand admin consent.":::

7. Next, while viewing the app registration, select **Token configuration**, and then **+ Add optional claim**. On the *Add optional claim* page, for *Token type* select **Access**, and then for *Claim*, select the checkbox for **acct**. Tunnel for MAM requires this Auth token to authenticate users to Microsoft Entra ID.
   Select **Add** to complete configuration of the Token.

   :::image type="content" source="./media/microsoft-tunnel-mam-ios/configure-token.png" alt-text="Configure the authentication token.":::

8. To verify that all settings were applied successfully, select **Integration assistant**:

   - For *What application types are you building?* select **Mobile app (Android, iOS, Xamarin, UWP)**.
   - Set *Is this application calling APIs?* to **No**, and then select **Evaluate my app registration**.

   :::image type="content" source="./media/microsoft-tunnel-mam-ios/integration-assistant.png" alt-text="Use the app registration Integration assistant to verify settings.":::

   The results should show a status of *Complete* for both *Recommended configurations* and *Discouraged configurations*.

#### Update an existing app registration

When you already have an app registration, you can choose to update it instead of creating a new one. Review the following settings and make changes when needed.

- *Application ID* and *Tenant ID*
- Authentication configuration
- API Permissions
- Token configuration
- Integration assistant

1. In the [Microsoft Entra admin center ](https://entra.microsoft.com/),  expand **Applications**, and then select  **App registrations**. Next, select the app registration that you want to review and update to open its *Overview* pane. Record the values for the *Application (client) ID* and the *Directory (tenant) ID*.

   These values must exactly match the following values in your Xcode app project:
   - info.plist > IntuneMAMSettings
     - Application (client) ID = ADALClientId
     - Directory (tenant) ID = ADALAuthority

2. Select **Authentication** and review the app platform type. It must be *iOS/macOS* and have a *Bundle ID* and *Redirect URI*. The Redirect URI must be formed as `msauth.Your_Bundle_ID://auth`.

   Next, select **View** to view the details of the *Bundle ID* and *Redirect URI*. Ensure that an *MSAL Configuration* is present. If it isn't, see [Create a Microsoft Entra application and service principal that can access resources](/azure/active-directory/develop/howto-create-service-principal-portal#app-registration-app-objects-and-service-principals) for guidance.

   As in the previous step, compare the values *Bundle ID* and *Redirect URI* with these values from your Xcode app project:  
   - Project > General > Identity: Bundle ID
   - info.plist > IntuneMAMSettings: ADALRedirectUri

   Also ensure the Xcode Bundle Identifier in your app project matches the app registration Bundle ID:

   :::image type="content" source="./media/microsoft-tunnel-mam-ios/review-authentication.png" alt-text="Compare authentication settings to the Bundle ID in your Xcode.":::

3. Verify, and update the **API permissions**. Ensure you have *Microsoft Graph*, and *Microsoft Mobile Application Management* permissions already set.

   :::image type="content" source="./media/microsoft-tunnel-mam-ios/review-api-permissions.png" alt-text="Review the APP permissions in the app registration.":::

   Next add permissions for the *Microsoft Tunnel Gateway* service principal:

   1. Select **+ Add a permission**.
   2. Select the **API my organization uses** tab
   3. Search for *Microsoft Tunnel Gateway*, and select it to **Request API permissions**.

      If *Microsoft Tunnel Gateway* doesn't appear in the list, then it hasn't been provisioned. To provision it, see [Use Microsoft Tunnel VPN gateway with Conditional Access policies](microsoft-tunnel-conditional-access.md#provision-your-tenant).

   4. Select the **Tunnel_Allow** permission and select on **Add permission** to continue.

   Next, grant *admin consent* for the new permissions:

   1. Select **Grant admin consent for YOUR_TENANT_NAME**.
   1. In the *Grant admin consent confirmation* dialog, select **Yes**.

   After being updated, you should see the following three API permissions with the status of *Granted for YOUR_TENANT_NAME*:
   - Microsoft Graph
   - Microsoft Mobile Management
   - Microsoft Tunnel Gateway

4. Select **Token configuration** to confirm the settings.  For *Claim*, you should see a value for *acct* with a *Token type* of *Access*.

   If *acct* isn't present, select **+Add optional claim** to add a claim:

   1. For *Token type*, select *Access*.
   1. Select the checkbox for *acct*.
   1. Select **Add** to complete the configuration.

5. Select **Integration assistant** to validate the app registration:

   1. For *What application types are you building?* select **Mobile app (Android, iOS, Xamarin, UWP)**
   1. Set *Is this application calling APIs?* to **No**, and then select **Evaluate my app registration**.

   The results should show a status of *Complete* for both *Recommended configurations* and *Discouraged configurations*.

## Xcode Line of Business app integration

Xcode is the Apple Integrated Developer Environment that that runs on macOS and used to integrate the Tunnel for MAM iOS SDK with your app.

The following are requirements for using Xcode to successfully integrate an iOS App to use Microsoft Tunnel for MAM iOS:

- macOS - To run Xcode
- Xcode 14.0 or later
- MAM-SDK – min version: 16.1.1
- MSAL-SDK – min version: 1.2.3
- Tunnel for MAM iOS SDK, available on GitHub

For guidance on integrating the SDK, see [Tunnel for MAM iOS SDK developer guide](../developer/tunnel-mam-ios-sdk.md).

## Known Issues

The following are known issues or limitations for Tunnel for MAM on iOS. For known issues with the Microsoft Tunnel for MAM iOS SDK, go to [Tunnel for MAM iOS SDK developer guide](../developer/tunnel-mam-ios-sdk.md#known-issues).

### MAM Tunnel not supported when using the MDM Tunnel

You can choose to use MAM Tunnel with enrolled devices instead of using MDM Tunnel configurations.   However, deploying both MAM and MDM Tunnel App configuration policies containing Microsoft Tunnel settings, to the same device isn't supported and results in client networking failures.

For example, enrolled devices can't have an app like Microsoft Edge that uses MAM tunnel App configuration policy setting while other apps use MDM Tunnel configurations.

**Workaround**: To use MAM Tunnel with enrolled devices, ensure, the Defender for Endpoint iOS app doesn't have an App configuration policy with Microsoft Tunnel settings configured.

### Firebase Integration with Tunnel for MAM iOS

When using Microsoft Tunnel for iOS with an app that integrates Firebase, if the app doesn't establish a connection to Tunnel before initializing Firebase, initialization issues and unexpected behavior can occur.

**Workaround**: To avoid this issue, ensure that the app logic prioritizes establishing a successful connection to Tunnel before initializing Firebase.

To learn more about Firebase, see [https://firebase.google.com/](https://firebase.google.com/).

### Newly created custom app not showing in UX

When you create a custom app configuration policy, the newly added app might not appear in the list of targeted apps or the list of available custom apps.

**Workaround**: This issue can be resolved by refreshing the Intune admin center and accessing the policy again:

1. In the Intune admin center, go to **Apps** > **Configuration** > **Create**.
2. Select custom apps, add a Bundle or Package ID for iOS, complete the flow, and create the app config policy.
3. Edit the basic settings. The newly added bundle ID should appear in the list of targeted custom apps.

### Microsoft Azure Authenticator app doesn't work with Tunnel for MAM iOS Conditional Access  

**Workaround**: If you have a Conditional Access policy for Microsoft Tunnel Gateway that requires multifactor authentication as a Grant Access control, you must implement the "onTokenRequiredWithCallback" method in the Microsoft Tunnel Delegate Class within your Line of Business Applications.

### Federated Microsoft Entra tenants

Create a General configuration setting in App config to exclude the customers STS (federated server URL) to address the MAM-Tunnel connect login issue:

Experienced in Edge browser when users sign-in with work account. Also experienced when users sign-in to LOB app for the first time.

**Workaround**:
Create a "General configuration setting":

key: com.microsoft.tunnel.custom_configuration

value: {"bypassedUrls":["ipchicken.com", "whatsmyip.org"]}

> [!NOTE]  
> The bypassedUrl should include the federation STS endpoint.

### Limitations when using Edge on iOS/iPadOS

Tunnel for MAM doesn't support:  

- On-premises sites using Kerberos.
- Certificate-based authentication for websites using Edge

**Workaround**: None.

> [!TIP]
> Tunnel for MAM on iOS does support NTLM integrated authentication webserver sign-in with Microsoft Edge, but not for Line of Business (LOB) apps. For more information, see [Manage NTLM single sign-on sites](../apps/manage-microsoft-edge.md#manage-ntlm-single-sign-on-sites) in *Manage Microsoft Edge on iOS and Android with Intune*.

## Next steps

- [Configure Microsoft Tunnel](../protect/microsoft-tunnel-configure.md)
- [Monitor Microsoft Tunnel](../protect/microsoft-tunnel-monitor.md)
- [MAM Tunnel for Android](../protect/microsoft-tunnel-mam-android.md)
