---
title: Use Microsoft Tunnel VPN with Android devices that don't enroll with Microsoft Intune
description: Add support for Mobile Application Management (MAM) for Android to the Microsoft Tunnel Gateway. Tunnel support for MAM expands access to your organizational resources for devices that can't or haven't enrolled with Microsoft Intune
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/01/2023
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
ms.collection:
- tier2
- M365-identity-device-management
---

# Microsoft Tunnel for Mobile Application Management for Android

[!INCLUDE [intune-add-on-note](../includes/intune-add-on-note.md)]

When you add Microsoft Tunnel for Mobile Application Management (MAM) to your tenant, you can use Microsoft Tunnel VPN Gateway with unenrolled Android devices to support MAM scenarios. With support for MAM, your unenrolled devices can use Tunnel to securely connect to your organization allowing users and apps safe access to your organizational data.

Applies to:  
- Android Enterprise

To extend your existing [Microsoft Tunnel configuration](../protect/microsoft-tunnel-configure.md) to support [MAM](../fundamentals/deployment-guide-enrollment-mamwe.md), you’ll create and deploy three profiles that configure this support on your unenrolled devices:

- App configuration policy for Microsoft Defender. This policy configures Microsoft Defender for Endpoint on a device as the VPN tunnel client app.
- App configuration policy for Microsoft Edge. This policy configures Microsoft Edge to support identity-switch, which automatically connects and disconnects the VPN tunnel when switching from a Microsoft "Work or school" account to a Microsoft "personal account" in Microsoft Edge.
- App protection policy to automatically start the connection to Microsoft Tunnel when the MAM enabled app on the device accesses corporate resources.

With these policies in place, your existing Site and Server configurations for Tunnel support access from devices that aren't enrolled in Intune. In addition, you can choose to deploy your configurations for MAM Tunnel to enrolled devices instead of using MDM Tunnel configurations. In this scenario, an enrolled device must use only the MDM Tunnel configurations or the MAM Tunnel configurations, but not both. For example, enrolled devices can't have an app like Microsoft Edge that uses MAM tunnel configurations while other apps use MDM Tunnel configurations.

## Prerequisites

**Infrastructure and tenant**:

Tunnel for MAM requires the same considerations and prerequisites as using Tunnel for enrolled devices. For more information, see [Tunnel prerequisites](../protect/microsoft-tunnel-prerequisites.md).

After [configuring Microsoft Tunnel](../protect/microsoft-tunnel-configure.md), you’ll be ready to add the two *App configuration policies* and the *App protection policy* that enables unenrolled devices to use Tunnel. Configuration of these policies is detailed in the following sections.

**Devices**:

Users of devices that aren't enrolled with Intune must install the following apps on their Android device before they can use the Tunnel for MAM scenario. These apps can all be manually installed from the Google Play store:

1. **Microsoft Defender** – Get it from [Microsoft Defender - Apps on Google Play](https://play.google.com/store/apps/details?id=com.microsoft.scmx&hl=en_US&gl=US&pli=1). Microsoft Defender includes the tunnel client app that the device uses to connect to Microsoft Tunnel. To support Tunnel for MAM, Microsoft Defender for Endpoint must be version **1.0.4722.0101** or higher.

2. **Microsoft Edge** – Get it from [Microsoft Edge: Web Browser - Apps on Google Play](https://play.google.com/store/apps/details?id=com.microsoft.emmx&hl=en_US&gl=US). Each device must manually enable the Tunnel functionality for Microsoft Edge before the device can use Tunnel. To enable support for Tunnel, users must browse to **edge://flags** from within the Microsoft Edge app, and then search for and select **Tunnel** to enable it.

3. **Company Portal** – Get it at [Intune Company Portal - Apps on Google Play](https://play.google.com/store/apps/details?id=com.microsoft.windowsintune.companyportal&hl=en_US&gl=US). Devices must install the Company Portal app, even though users won’t need to sign into the app or enroll their device with Intune.

**Line of Business apps**:

For your Line of Business (LOB) apps, integrate them with the MAM SDK. Later, you’ll need to [add your LOB apps](#configure-line-of-business-applications) to your app protection policy and app configuration polices for MAM Tunnel. See [Getting started with MAM for Android](../developer/app-sdk-android-phase3.md).

## Configure policies to support Microsoft Tunnel for MAM

To support using Tunnel for MAM, create and deploy the three profiles detailed in the following sections. These policies can be created in any order:

- [App configuration policy for Microsoft Edge](#app-configuration-policy-for-microsoft-edge)
- [App configuration policy for Microsoft Defender](#app-configuration-policy-for-microsoft-defender)
- [App protection policy for Tunnel](#app-protection-policy-for-tunnel)

When all three are configured and deployed to the same groups, the app protection policy will automatically trigger Tunnel to connect to the VPN whenever Microsoft Edge is launched.

### App configuration policy for Microsoft Defender

Create an App configuration policy to configure Microsoft Defender for Endpoint on the device for use as the tunnel client app.
> [!NOTE]
> Ensure only a single Defender app configuration policy targets the unenrolled device. Targeting more than 1 app configuration policy with different tunnel settings for Defender for Endpoint will create tunnel connection issues on the device.

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and go to **Apps** > **App Configuration polices** > **Add** > **Managed Apps**.

2. On the *Basics* tab:

   1. Enter a *Name* for this policy, and a *Description (optional)*.
   2. Click on **Select public apps**, select **Microsoft Defender Endpoint** for *Android*, and then click Select.

   When Microsoft Defender Endpoint is listed for *Public apps*, select **Next**.

   :::image type="content" source="./media/microsoft-tunnel-mam-android/public-apps-defender.png" alt-text="Screen shot of configuring an app configuration policy with Microsoft Defender Endpoint as a public app.":::

3. On the *Settings* tab, skip the *General configuration settings* category, which isn't used for this policy. For the *Microsoft Tunnel settings* category, make the following configurations:

   - Set *Use Microsoft Tunnel VPN* to **Yes**.
   - For *Connection name*, specify the connection name of your VPN.

   Next, click **Select a site**:

   - For *Site Name*, select an available site, and then click **OK**.

   - *Per-App VPN (Android only)* is an optional setting.  Select public or custom apps, to restrict the use of use the Tunnel VPN connection to these specified apps.
   - *Proxy* is an optional setting.  Configure proxy settings to meet your on-premises network requirements.  
     > [!NOTE]  
     > Proxy server configurations are not supported with versions of Android prior to version 10.  For more information, see [VpnService.Builder](https://developer.android.com/reference/android/net/VpnService.Builder#setHttpProxy%28android.net.ProxyInfo%29) in that Android developer documentation.

   > [!IMPORTANT]
   > Microsoft Tunnel for MAM Android doesn’t support use of trusted root certificates, even though *Root Certificate* is an available option when configuring the App configuration policy. Configuration of a trusted root certificate for Android should be skipped as it will not work.

   When ready, select **Next** to continue.

   :::image type="content" source="./media/microsoft-tunnel-mam-android/settings-configuration-defender.png " alt-text="Screen shot of the app configuration policies settings configuration.":::

4. On the *Assignments* tab, select **Add Groups**, and then select the same Azure Active Directory groups that you deployed the Microsoft Edge App configuration profile to, and then select **Next**.

5. On the *Review + Create* tab, select **Create** to complete creation of the policy and deploy the policy to the assigned groups.

The new policy will appear in the list of App configuration policies.

### App configuration policy for Microsoft Edge

Create an App configuration policy for Microsoft Edge. This policy configures Microsoft Edge to support identity-switch, providing the ability to automatically connect the VPN Tunnel when signing-in or switching to a Microsoft "Work or school" account, and automatically disconnect the VPN tunnel when switching to a Microsoft personal account.

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and go to **Apps** > **App Configuration polices** > **Add** > **Managed Apps**.

2. On the *Basics* tab:

   1. Enter a *Name* for the policy, and a *Description (optional)*.
   2. Click on **Select public apps**, select **Microsoft Edge** for *Android*, and then click **Select**.

   After Microsoft Edge is listed for *Public apps*, select **Next**.

   :::image type="content" source="./media/microsoft-tunnel-mam-android/public-apps-edge.png" alt-text="Screen shot of configuring an app configuration policy with Microsoft Edge as a public app.":::

3. On the *Settings* tab, configure the *Name* and *Value* pair in the *General configuration settings* category as follows:

   - Name = **com.microsoft.intune.mam.managedbrowser.TunnelAvailable.IntuneMAMOnly**
   - Value = **True**

   :::image type="content" source="./media/microsoft-tunnel-mam-android/name-value-pair-edge.png" alt-text="Screen shot that shows the configuration of the name and value pair.":::

   > [!NOTE]
   > Ensure there are no trailing spaces at the end of the General configuration setting. This setting provides “Identity switch” support to Edge on Android. This enables Edge on Android to automatically connect the VPN when signing in with a “Work account or School account” and disconnect the VPN when switching to a “Personal account” enabling in-Private browsing.

   You can also use this same policy to configure other configurations for Microsoft Edge in the *Microsoft Edge configuration settings* category. After any additional configurations for Microsoft Edge are ready, select **Next**.

4. On the *Assignments* tab, select **Add Groups**, and then select one or more Azure Active Directory groups that will receive this policy.   After configuring groups, select **Next**.

5. On the *Review + Create* tab, select **Create** to complete creation of the policy and deploy the policy to the assigned groups.

The new policy will appear in the list of App configuration policies.

### App protection policy for Tunnel

Create an app protection policy to automatically start the Microsoft Tunnel VPN connection when the app is launched.

> [!NOTE]  
> When the app is started, the Tunnel VPN connection will attempt to start, once started, the device will have access to the on-premises network routes available via the Microsoft Tunnel Gateway.  If you wish to limit the tunnel network access to specific apps, then configure the "Per-App VPN (Android only) settings.

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and go to **Apps** > **App protection policies** > **Create policy** > **Android**.

2. On the *Basics* tab, enter a *Name* for this policy, and a *Description (optional)*, and then select **Next**.

3. On the *Apps* tab, click **Select public apps**, select **Microsoft Edge**, and then click **Select**.

   When Microsoft Edge is listed for *Public apps*, select **Next**.
  
   :::image type="content" source="./media/microsoft-tunnel-mam-android/app-protection-edge.png" alt-text="Screen shot of configuring an app protection policy with Microsoft Edge as a public app.":::

4. On the *Data protection* tab, scroll to the bottom and set *Start Microsoft Tunnel connection on app-launch* to **Yes**, and then select **Next**.

   :::image type="content" source="./media/microsoft-tunnel-mam-android/app-protection-data-protection-tab.png" alt-text="Screen shot of configuring an app protection policy setting for using Tunnel on app-launch.":::

5. Continue past the *Access requirements* and *Conditional launch* tabs.

6. On the *Assignments* tab, select **Add Groups**, and then select the same Azure Active Directory groups that you deployed the two app configuration profiles to, and then select **Next**.

7. On the *Review + Create* tab, select **Create** to complete creation of the policy and deploy the policy to the assigned groups.

The new policy will appear in the list of app configuration policies.

## Configure Line of Business applications

If you’ve integrated your LOB apps with the MAM SDK, you can use them with Microsoft Tunnel by adding them as *custom apps* to the three MAM Tunnel policies you’ve [previously created](#configure-policies-to-support-microsoft-tunnel-for-mam).

For more information about adding custom apps to policies, see the following articles for the two policy types:

- [App configuration policies for Intune App SDK managed apps](../apps/app-configuration-policies-managed-app.md)
- [How to create and assign app protection policies](../apps/app-protection-policies.md)

To support LOB apps on your unenrolled devices, the apps must deploy as *available apps*  from within Microsoft Endpoint Manager admin center. You can’t use Intune to deploy apps as required apps to unenrolled devices.

## Known Issues

The following are known issues or limitations for MAM Tunnel for Android. 
### Delivering trusted root certs to unenrolled devices

When unenrolled devices access resources protected by SSL/TLS certificates issued by an on-premises certificate authority (CA), the devices require the trusted certificate public keychain of the issuing CA to establish a chain of trust with the on-premises endpoint (that is, web server, application web service). As a result, a  browser (Microsoft Edge or third party browser), or application won't trust the endpoint without the necessary on-premises CA keychain (trusted cert). For example, Microsoft Edge reports that the connection isn’t private or is untrusted, and SSL or https connections aren't available. Users can ignore this warning and connect to the endpoint.

Microsoft Tunnel for MAM on Android doesn't provide support for delivering Trusted certificates to unenrolled devices.

**Work around**: Manually deploy and install the trusted root certificate on unenrolled Android devices that will use Tunnel.

### Microsoft Edge can't reach internal resources for a short time after being launched

Immediately after Microsoft Edge opens, the browser attempts to connect to internal resources before successfully connecting to Tunnel. This behavior results in the browser reporting that the resource or destination URL is unavailable.

**Work around**: Refresh the browser connection on the device. The resource becomes available after the connection to Tunnel is established.

### The three apps required to support Tunnel for unenrolled devices aren't visible in the Company Portal app on a device

After Microsoft Edge, Microsoft Defender for Endpoint, and the Company Portal, are assigned to a device as *available with or without enrollment*, the targeted user can't find the apps in the Company Portal or at *portal.manage.microsoft.com*.

**Work around**: Install all three apps manually from the Google Play store. You'll find links to all three apps on Google Play in this articles [Prerequisites](#prerequisites) section.

### Error: “MSTunnel VPN is failed to start, contact your IT administrator for help"

This error message can occur even though the tunnel is connected.

**Work around**: This message can be ignored.

### Error: Invalid Licensing, please contact administrator

This error occurs when the version of Microsoft Defender for Endpoint doesn't support Tunnel.

**Work around**: Install the supported version of Defender for Endpoint from [Microsoft Defender - Apps on Google Play](https://play.google.com/store/apps/details?id=com.microsoft.scmx&hl=en_US&gl=US&pli=1).

### Using multiple policies for Defender to configure different tunnel sites for different apps isn't supported

Use of two or more app configuration policies for Microsoft Defender that specify different Tunnel Sites isn't supported and can result in a race condition that prevents successful use of Tunnel.

**Work around**: Target each device with a single app configuration policy for Microsoft Defender, ensuring each unenrolled device is configured to use only one Site.

### GCC High and FIPS support

Microsoft Tunnel for MAM is supported for GGC High environments, but doesn't support Federal Information Processing Standard (FIPS).

## Next steps

- [Overview of Microsoft Tunnel for Mobile Application Management](../protect/microsoft-tunnel-mam.md)
- [MAM Tunnel for iOS](../protect/microsoft-tunnel-mam-ios.md)

Also see:

- [Configure Microsoft Tunnel](../protect/microsoft-tunnel-configure.md)
- [Monitor Microsoft Tunnel](../protect/microsoft-tunnel-monitor.md)
