---
# required metadata

title: Manage Microsoft Edge on iOS and Android with Intune
titleSuffix: 
description: Use Intune app protection and configuration policies with Edge for iOS and Android to ensure corporate websites are always accessed with safeguards in place. 
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 10/24/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: medium
ms.assetid: 3fb2f050-ec94-42ab-be05-c3d4101148bb

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: ilwu
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.collection:
- tier1
- M365-identity-device-management
- Android
- highpri
- FocusArea_Apps_SpecificApp
ms.custom: intune-azure
---

# Manage Microsoft Edge on iOS and Android with Intune

Edge for iOS and Android is designed to enable users to browse the web and supports multi-identity. Users can add a work account, as well as a personal account, for browsing. There's complete separation between the two identities, which is like what is offered in other Microsoft mobile apps.

This feature applies to:
- iOS/iPadOS 14.0 or later
- Android 8.0 or later for enrolled devices and Android 9.0 or later for unenrolled devices

> [!NOTE]
> Edge for iOS and Android doesn't consume settings that users set for the native browser on their devices, because Edge for iOS and Android can't access these settings.

The richest and broadest protection capabilities for Microsoft 365 data are available when you subscribe to the Enterprise Mobility + Security suite, which includes Microsoft Intune and Microsoft Entra ID P1 or P2 features, such as Conditional Access. At a minimum, you'll want to deploy a Conditional Access policy that only allows connectivity to Edge for iOS and Android from mobile devices and an Intune app protection policy that ensures the browsing experience is protected.

> [!NOTE]
> New web clips (pinned web apps) on iOS devices will open in Edge for iOS and Android instead of the Intune Managed Browser when required to open in a protected browser. For older iOS web clips, you must re-target these web clips to ensure they open in Edge for iOS and Android rather than the Managed Browser.

## Create Intune app protection policies

As organizations increasingly adopt SaaS and web applications, browsers have become essential tools for businesses. Users often need to access these applications from mobile browsers while on the go. Ensuring that data accessed through mobile browsers is protected from intentional or unintentional leaks is crucial. For instance, users might inadvertently share organizations’ data with personal apps, leading to data leakage, or download it to local devices, which also poses a risk. 

Organizations can protect data from being leaked when users browse with Microsoft Edge for mobile by configuring App Protection Policies (APP), which define what apps are allowed and the actions they can take with your organizations' data. The choices available in APP enable organizations to tailor the protection to their specific needs. For some, it may not be obvious which policy settings are required to implement a complete scenario. To help organizations prioritize mobile client endpoint hardening, Microsoft has introduced taxonomy for its APP data protection framework for iOS and Android mobile app management.

The APP data protection framework is organized into three distinct configuration levels, with each level building off the previous level:

- **Enterprise basic data protection** (Level 1) ensures that apps are protected with a PIN and encrypted and performs selective wipe operations. For Android devices, this level validates Android device attestation. This is an entry level configuration that provides similar data protection control in Exchange Online mailbox policies and introduces IT and the user population to APP.
- **Enterprise enhanced data protection** (Level 2) introduces APP data leakage prevention mechanisms and minimum OS requirements. This is the configuration that is applicable to most mobile users accessing work or school data.
- **Enterprise high data protection** (Level 3) introduces advanced data protection mechanisms, enhanced PIN configuration, and APP Mobile Threat Defense. This configuration is desirable for users that are accessing high risk data.

To see the specific recommendations for each configuration level and the minimum apps that must be protected, review [Data protection framework using app protection policies](app-protection-framework.md).

Regardless of whether the device is enrolled in a unified endpoint management (UEM) solution, an Intune app protection policy needs to be created for both iOS and Android apps, using the steps in [How to create and assign app protection policies](app-protection-policies.md). These policies, at a minimum, must meet the following conditions:

- They include all Microsoft 365 mobile applications, such as Edge, Outlook, OneDrive, Office, or Teams, as this ensures that users can access and manipulate work or school data within any Microsoft app in a secure fashion.

- They're assigned to all users. This ensures that all users are protected, regardless of whether they use Edge for iOS or Android.

- Determine which framework level meets your requirements. Most organizations should implement the settings defined in **Enterprise enhanced data protection** (Level 2) as that enables data protection and access requirements controls.

> [!NOTE]
> One of the settings related to browsers is 'Restrict web content transfer with other apps'. In **Enterprise enhanced data protection** (Level 2), the value of this setting is configured to Microsoft Edge.
> When Outlook and Microsoft Teams are protected by App Protection Policies (APP), Microsoft Edge will be used to open links from these apps, ensuring that the links are secure and protected. 
> For more information on the available settings, see [Android app protection policy settings](app-protection-policy-settings-android.md) and [iOS app protection policy settings](app-protection-policy-settings-ios.md).

> [!IMPORTANT]
> To apply Intune app protection policies against apps on Android devices that are not enrolled in Intune, the user must also install the Intune Company Portal.  

## Apply Conditional Access
While it's important to protect Microsoft Edge with App Protection Policies (APP), it's also crucial to ensure Microsoft Edge is the mandatory browser for opening corporate applications. Users might otherwise use other unprotected browsers to access corporate applications, potentially leading to data leaks.

Organizations can use Microsoft Entra Conditional Access policies to ensure that users can only access work or school content using Edge for iOS and Android. To do this, you'll need a Conditional Access policy that targets all potential users. These policies are described in [Conditional Access: Require approved client apps or app protection policy](/azure/active-directory/conditional-access/howto-policy-approved-app-or-app-protection).

Follow the steps in [Require approved client apps or app protection policy with mobile devices](/azure/active-directory/conditional-access/howto-policy-approved-app-or-app-protection#require-approved-client-apps-or-app-protection-policy-with-mobile-devices), which allows Edge for iOS and Android, but blocks other mobile device web browsers from connecting to Microsoft 365 endpoints.

>[!NOTE]
> This policy ensures mobile users can access all Microsoft 365 endpoints from within Edge for iOS and Android. This policy also prevents users from using InPrivate to access Microsoft 365 endpoints.

With Conditional Access, you can also target on-premises sites that you have exposed to external users via the [Microsoft Entra application proxy](/azure/active-directory/active-directory-application-proxy-get-started).

> [!NOTE]
> To leverage app-based Conditional Access policies, the Microsoft Authenticator app must be installed on iOS devices. For Android devices, the Intune Company Portal app is required. For more information, see [App-based Conditional Access with Intune](../protect/app-based-conditional-access-intune.md).

## Single sign-on to Microsoft Entra connected web apps in policy-protected browsers

Edge for iOS and Android can take advantage of single sign-on (SSO) to all web apps (SaaS and on-premises) that are Microsoft Entra connected. SSO allows users to access Microsoft Entra connected web apps through Edge for iOS and Android, without having to re-enter their credentials.

SSO requires your device to be registered by either the Microsoft Authenticator app for iOS devices, or the Intune Company Portal on Android. When users have either of these, they're prompted to register their device when they go to a Microsoft Entra connected web app in a policy-protected browser (this is only true if their device hasn't already been registered). After the device is registered with the user's account managed by Intune, that account has SSO enabled for Microsoft Entra connected web apps.

> [!NOTE]
> Device registration is a simple check-in with the Microsoft Entra service. It doesn't require full device enrollment, and doesn't give IT any additional privileges on the device.

## Use app configuration to manage the browsing experience

Edge for iOS and Android supports app settings that allow unified endpoint management, like Microsoft Intune, administrators to customize the behavior of the app.

App configuration can be delivered either through the mobile device management (MDM) OS channel on enrolled devices ([Managed App Configuration](https://developer.apple.com/library/content/samplecode/sc2279/Introduction/Intro.html) channel for iOS or the [Android in the Enterprise](https://developer.android.com/work/managed-configurations) channel for Android) or through the MAM (Mobile Application Management) channel. Edge for iOS and Android supports the following configuration scenarios:

- Only allow work or school accounts
- General app configuration settings
- Data protection settings
- Additional app configuration for managed devices

> [!IMPORTANT]
> For configuration scenarios that require device enrollment on Android, the devices must be enrolled in Android Enterprise and Edge for Android must be deployed via the Managed Google Play store. For more information, see [Set up enrollment of Android Enterprise personally owned work profile devices](../enrollment/android-work-profile-enroll.md) and [Add app configuration policies for managed Android Enterprise devices](app-configuration-policies-use-android.md).

Each configuration scenario highlights its specific requirements. For example, whether the configuration scenario requires device enrollment, and thus works with any UEM provider, or requires Intune App Protection Policies.

> [!IMPORTANT]
> App configuration keys are case sensitive. Use the proper casing to ensure the configuration takes effect.

> [!NOTE]
> With Microsoft Intune, app configuration delivered through the MDM OS channel is referred to as a **Managed Devices** App Configuration Policy (ACP); app configuration delivered through the MAM (Mobile Application Management) channel is referred to as a **Managed Apps** App Configuration Policy.

## Only allow work or school accounts

Respecting the data security and compliance policies of our largest and highly regulated customers is a key pillar to the Microsoft 365 value. Some companies have a requirement to capture all communications information within their corporate environment, as well as, ensure the devices are only used for corporate communications. To support these requirements, Edge for iOS and Android on enrolled devices can be configured to only allow a single corporate account to be provisioned within the app.

You can learn more about configuring the org allowed accounts mode setting here:

- [Android setting](app-configuration-policies-use-android.md#allow-only-configured-organization-accounts-in-apps)
- [iOS setting](app-configuration-policies-use-ios.md#allow-only-configured-organization-accounts-in-apps)

This configuration scenario only works with enrolled devices. However, any UEM provider is supported. If you are not using Microsoft Intune, you need to consult with your UEM documentation on how to deploy these configuration keys.

## General app configuration scenarios

Edge for iOS and Android offers administrators the ability to customize the default configuration for several in-app settings. This capability is offered when Edge for iOS and Android has a managed apps App Configuration Policy applied to the work or school account that is signed into the app.

Edge supports the following settings for configuration:

- New Tab Page experiences
- Bookmark experiences
- App behavior experiences
- Kiosk mode experiences

These settings can be deployed to the app regardless of device enrollment status.

### New Tab Page layout
The **inspirational** layout is the default one for the new tab page. It shows top site shortcuts, wallpaper and news feed. Users can change the layout according to their preferences. Organizations can also manage the layout settings.

|Key |Value |
|:-----------|:-------------|
|com.microsoft.intune.mam.managedbrowser.NewTabPageLayout |**focused** Focused is selected <br> **inspirational** (Default) Inspirational is selected <br> **informational** Informational is selected <br> **custom** Custom is selected, top site shortcuts toggle is on, wallpaper toggle is on, and news feed toggle is on|
|com.microsoft.intune.mam.managedbrowser.NewTabPageLayout.Custom |**topsites** Turn on top site shortcuts <br> **wallpaper** Turn on wallpaper <br> **newsfeed** Turn on news feed <br> In order for this policy to take effect, com.microsoft.intune.mam.managedbrowser.NewTabPageLayout must be set to **custom** <br><br> The default value is `topsites|wallpaper|newsfeed|` |
|com.microsoft.intune.mam.managedbrowser.NewTabPageLayout.UserSelectable |**true** (Default) Users can change the page layout settings <br> **false** Users cannot change the page layout settings. The page layout is determined by the values specified via the policy or default values will be used |

> [!IMPORTANT]
> **NewTabPageLayout** policy is intended to set the initial layout. Users can change page layout settings based on their reference. Therefore, **NewTabPageLayout** policy only takes effect if users do not change layout settings. You can enforce **NewTabPageLayout** policy by configuring **UserSelectable**=false.

> [!NOTE]
> As of version 129.0.2792.84, the default page layout is changed to **inspirational**.

An example of turning off the news feeds
- com.microsoft.intune.mam.managedbrowser.NewTabPageLayout=**custom**
- com.microsoft.intune.mam.managedbrowser.NewTabPageLayout.Custom=**topsites**
- com.microsoft.intune.mam.managedbrowser.NewTabPageLayout.UserSelectable=**false**

### New Tab Page experiences

Edge for iOS and Android offers organizations several options for adjusting the New Tab Page experience including organization logo, brand color, your home page, top sites, and industry news.

#### Organization logo and brand color

The organization logo and brand color settings allow you to customize the **New Tab Page** for Edge on iOS and Android devices. The **Banner logo** is used as your organization's logo and the **Page background color** is used as your organization's brand color. For more information, see [Configure your company branding](/entra/fundamentals/how-to-customize-branding). 

Next, use the following key/value pairs to pull your organization's branding into Edge for iOS and Android:

|Key |Value |
|:---------|:------------|
|com.microsoft.intune.mam.managedbrowser.NewTabPage.BrandLogo |**true** shows organization's brand logo <br>**false** (default) won't expose a logo |
|com.microsoft.intune.mam.managedbrowser.NewTabPage.BrandColor |**true** shows organization's brand color <br>**false** (default) won't expose a color |

#### Homepage shortcut

This setting allows you to configure a homepage shortcut for Edge for iOS and Android in the New Tab Page. The homepage shortcut you configure appears as the first icon beneath the search bar when the user opens a new tab in Edge for iOS and Android. The user can't edit or delete this shortcut in their managed context. The homepage shortcut displays your organization's name to distinguish it.

|Key |Value |
|:-----------|:-------------|
|com.microsoft.intune.mam.managedbrowser.homepage <br><br> This policy name has been replaced by the UI of **Homepage shortcut URL** under Edge Configuration settings |Specify a valid URL. Incorrect URLs are blocked as a security measure. <br>For example: `https://www.bing.com` |

#### Multiple top site shortcuts

Similarly to configuring a homepage shortcut, you can configure multiple top site shortcuts on New Tab Pages in Edge for iOS and Android. The user can't edit or delete these shortcuts in a managed context. Note: you can configure a total of 8 shortcuts, including a homepage shortcut. If you have configured a homepage shortcut, that shortcut will override the first top site configured. 

|Key |Value |
|:------------|:------------|
|com.microsoft.intune.mam.managedbrowser.managedTopSites |Specify set of value URLs. Each top site shortcut consists of a title and URL. Separate the title and URL with the `|` character. <br>For example: `GitHub|https://github.com/||LinkedIn|https://www.linkedin.com`|

#### Industry news

You can configure the New Tab Page experience within Edge for iOS and Android to display industry news that is relevant to your organization. When you enable this feature, Edge for iOS and Android uses your organization's domain name to aggregate news from the web about your organization, organization's industry, and competitors, so your users can find relevant external news all from the centralized new tab pages within Edge for iOS and Android. Industry News is off by default. 

|Key |Value |
|:------------|:--------------|
|com.microsoft.intune.mam.managedbrowser.NewTabPage.IndustryNews |**true** shows Industry News on the New Tab Page<br>**false** (default) hides Industry News from the New Tab Page |

#### Homepage instead of New Tab Page experience

Edge for iOS and Android allows organizations to disable the New Tab Page experience and instead have a web site launch when the user opens a new tab. While this is a supported scenario, Microsoft recommends organizations take advantage of the New Tab Page experience to provide dynamic content that is relevant to the user.

|Key |Value |
|:-----------|:-------------|
|com.microsoft.intune.mam.managedbrowser.NewTabPage.CustomURL |Specify a valid URL. If no URL is specified, the app uses the New Tab Page experience. Incorrect URLs are blocked as a security measure.<br>For example: `https://www.bing.com`|

### Bookmark experiences

Edge for iOS and Android offers organizations several options for managing bookmarks.

#### Managed bookmarks

For ease of access, you can configure bookmarks that you'd like your users to have available when they're using Edge for iOS and Android.

- Bookmarks only appear in the work or school account and aren't exposed to personal accounts.
- Bookmarks can't be deleted or modified by users.
- Bookmarks appear at the top of the list. Any bookmarks that users create appear below these bookmarks.
- If you have enabled Application Proxy redirection, you can add Application Proxy web apps by using either their internal or external URL.
- Bookmarks are created in a folder named after the organization's name which is defined in Microsoft Entra ID.

|Key |Value |
|:-----------|:-------------|
|com.microsoft.intune.mam.managedbrowser.bookmarks <br><br> This policy name has been replaced by the UI of **Managed bookmarks** under Edge Configuration settings |The value for this configuration is a list of bookmarks. Each bookmark consists of the bookmark title and the bookmark URL. Separate the title and URL with the `|` character.<br>For example: `Microsoft Bing|https://www.bing.com`<br><br>To configure multiple bookmarks, separate each pair with the double character `||`.<br>For example: `Microsoft Bing|https://www.bing.com||Contoso|https://www.contoso.com`|

#### My Apps bookmark

By default, users have the My Apps bookmark configured within the organization folder inside Edge for iOS and Android.

|Key |Value |
|:-----------|:-------------|
|com.microsoft.intune.mam.managedbrowser.MyApps |**true** (default) shows My Apps within the Edge for iOS and Android bookmarks <br>**false** hides My Apps within Edge for iOS and Android|

### App behavior experiences

Edge for iOS and Android offers organizations several options for managing the app's behavior.

<a name='azure-ad-password-single-sign-on'></a>

#### Microsoft Entra password single sign-on

The Microsoft Entra Password single sign-on (SSO) functionality offered by Microsoft Entra ID brings user access management to web applications that don't support identity federation. By default, Edge for iOS and Android does not perform SSO with the Microsoft Entra credentials. For more information, see [Add password-based single sign-on to an application](/azure/active-directory/manage-apps/configure-password-single-sign-on-non-gallery-applications).

|Key |Value |
|:-----------|:-------------|
|com.microsoft.intune.mam.managedbrowser.PasswordSSO |**true** Microsoft Entra Password SSO is enabled <br>**false** (default) Microsoft Entra Password SSO is disabled|

#### Default protocol handler

By default, Edge for iOS and Android uses the HTTPS protocol handler when the user doesn't specify the protocol in the URL. Generally, this is considered a best practice, but can be disabled.


|Key |Value |
|:-----------|:-------------|
|com.microsoft.intune.mam.managedbrowser.defaultHTTPS|**true** (default) default protocol handler is HTTPS <br>**false** default protocol handler is HTTP|

#### Disable optional diagnostic data

By default, users can choose to send optional diagnostic data from **Settings**->**Privacy and security**->**Diagnostic data**->**Optional diagnostic data** setting. Organizations can disable this setting.

|Key |Value |
|:-----------|:-------------|
|com.microsoft.intune.mam.managedbrowser.disableShareUsageData |**true** Optional diagnostic data setting is disabled <br>**false** (default) The option can be turned on or off by users |

> [!NOTE]
> **Optional diagnostic data** setting is also prompted to users during the First Run Experience (FRE). Organizations can skip this step by using the MDM policy [EdgeDisableShareUsageData](/deployedge/microsoft-edge-mobile-policies#edgedisableshareusagedata)

#### Disable specific features

Edge for iOS and Android allows organizations to disable certain features that are enabled by default. To disable these features, configure the following setting:

|Key |Value |
|:-----------|:-------------|
|com.microsoft.intune.mam.managedbrowser.disabledFeatures|**password** disables prompts that offer to save passwords for the end user <br>**inprivate** disables InPrivate browsing <br>**autofill** disables "Save and Fill Addresses" and "Save and Fill Payment info". Autofill will be disabled even for previously saved information <br>**translator** disables translator <br> **readaloud** disables read aloud <br> **drop** disables drop <br>**coupons** disables coupons <br>**extensions** disables extensions (Edge for Android only) <br>**developertools** grays out the build version numbers to prevent users from accessing Developer options (Edge for Android only) <br>**UIRAlert** suppress re-verify account popups in new tab page screen <br> **share** disables Share under menu <br> **sendtodevices** disables Send to devices under menu <br> **weather** disables weather in NTP (New Tab Page) <br> **webinspector** disables Web Inspector setting (Edge for iOS only) <br><br>To disable multiple features, separate values with `|`. For example, `inprivate|password` disables both InPrivate and password storage. |

#### Disable import passwords feature

Edge for iOS and Android allows users to import passwords from Password Manager. To disable import passwords, configure the following setting:

|Key |Value |
|:-----------|:-------------|
|com.microsoft.intune.mam.managedbrowser.disableImportPasswords| **true** Disable import passwords <br>**false** (default) Allow import passwords |

> [!NOTE]
> In the Password Manager of Edge for iOS, there's an **Add** button. When the import passwords feature is disabled, the **Add** button will also be disabled.

#### Control Cookie Mode

You can control whether sites can store cookies for your users within Edge for Android.  To do this, configure the following setting:

|Key |Value |
|:-----------|:-------------|
|com.microsoft.intune.mam.managedbrowser.cookieControlsMode |**0** (default) allow cookies <br>**1** block non-Microsoft cookies <br>**2** block non-Microsoft cookies in InPrivate mode <br>**3** block all cookies |

> [!NOTE]
> Edge for iOS does not support controlling cookies.

### Kiosk mode experiences on Android devices

Edge for Android can be enabled as a kiosk app with the following settings:

|Key |Value |
|:--|:----|
|com.microsoft.intune.mam.managedbrowser.enableKioskMode |**true** enables kiosk mode for Edge for Android <br>**false** (default) disables kiosk mode |
|com.microsoft.intune.mam.managedbrowser.showAddressBarInKioskMode |**true** shows the address bar in kiosk mode <br>**false** (default) hides the address bar when kiosk mode is enabled|
|com.microsoft.intune.mam.managedbrowser.showBottomBarInKioskMode |**true** shows the bottom action bar in kiosk mode <br>**false** (default) hides the bottom bar when kiosk mode is enabled |

> [!NOTE]
> Kiosk mode is not supported on iOS devices. However, you may want to use Locked View Mode (MDM policy only) to achieve a similar user experience, where users are unable to navigate to other websites, as the URL address bar becomes read-only in Locked View Mode.

### Locked view mode

Edge for iOS and Android can be enabled as locked view mode with MDM policy **[EdgeLockedViewModeEnabled](/deployedge/microsoft-edge-mobile-policies#edgelockedviewmodeenabled)**.

|Key  |Value  |
|:---------|:---------|
|EdgeLockedViewModeEnabled |**false** (default) Locked view mode is disabled <br> **true** Locked view mode is enabled | 

It allows organizations to restrict various browser functionalities, providing a controlled and focused browsing experience.

- The URL address bar becomes read-only, preventing users from making changes to the web address
- Users are not allowed to create new tabs
- The contextual search feature on web pages is disabled
- The following buttons under the overflow menu are disabled

|Buttons | State |
|:--|:----|
|New InPrivate tab|Disabled|
|Send to Devices|Disabled|
|Drop|Disabled|
|Add to Phone (Android) |Disabled|
|Download Page (Android) |Disabled|

The locked view mode is often used together with MAM policy **com.microsoft.intune.mam.managedbrowser.NewTabPage.CustomURL** or MDM policy    **EdgeNewTabPageCustomURL**, which allow organizations to configure a specific web page that is automatically launched when Edge is opened. Users are restricted to this web page and cannot navigate to other websites, providing a controlled environment for specific tasks or content consumption.

> [!NOTE]
> By default, users are not allowed to create new tabs in locked view mode. To allow tab creation, set the MDM policy **[EdgeLockedViewModeAllowedActions](/deployedge/microsoft-edge-mobile-policies#edgelockedviewmodeallowedactions)** to **newtabs**.

### Switch network stack between Chromium and iOS 
By default, Microsoft Edge for both iOS and Android uses the Chromium network stack for Microsoft Edge service communication, including sync services, auto search suggestions and sending feedback. Microsoft Edge for iOS also provides the iOS network stack as a configurable option for Microsoft Edge service communication.

Organizations can modify their network stack preference by configuring the following setting.

|Key  |Value  |
|:---------|:---------|
|com.microsoft.intune.mam.managedbrowser.NetworkStackPref|**0** (default) use the Chromium network stack <br> **1** use the iOS network stack | 

> [!NOTE]
> Using the Chromium network stack is recommended. If you experience sync issues or failure when sending feedback with the Chromium network stack, for example with certain per-app VPN solutions, using the iOS network stack may solve the issues.

### Set a proxy .pac file URL

Organizations can specify a URL to a proxy auto-config (PAC) file for Microsoft Edge for iOS and Android

|Key |Value |
|:-----------|:-------------|
|com.microsoft.intune.mam.managedbrowser.proxyPacUrl |Specify a valid URL to a proxy .pac file.  <br>For example: `https://internal.site/example.pac` |

### PAC failed-open support 

By default, Microsoft Edge for iOS and Android will block network access with invalid or unavailable PAC script. However, organizations can modify the default behavior to PAC failed open.

|Key |Value |
|:-----------|:-------------|
|com.microsoft.intune.mam.managedbrowser.proxyPacUrl.FailOpenEnabled |**false** (default) Block network access  <br>**true** Allow network access |

### Configure network relays

Edge for iOS now supports network relays on iOS 17. These are a special type of proxy that can be used for remote access and privacy solutions. They support secure and transparent tunneling of traffic, serving as a modern alternative to VPNs when accessing internal resources. For more information about network relays, see [Use network relays on Apple devices](https://support.apple.com/guide/deployment/use-network-relays-dep91a6e427d/web).

Organizations can configure relay proxy URLs to route traffic based on matched and excluded domains. 

|Key |Value |
|:-----------|:-------------|
|com.microsoft.intune.mam.managedbrowser.ProxyRelayUrl |Specify a valid URL to a relay configuration json file.  <br>For example: `https://yourserver/relay_config.json` |

A json file example for network relays <br>
{ <br>
 "default": [{ <br>
            "proxy_type": "http", <br>
            "host_name": "170.200.50.300", <br>
            "port": "3128",  <br>
            "failover_allowed":0, <br>
            "match_domains": [ <br>
                "domain1.com", <br>
                "domain2.com" ], <br>
            "excluded_domains": [ <br>
                "domain3.com", <br>
                "domain4.com" ] <br>
        } ] <br>
} <br>

### Proxy for users to sign in to Edge in Android

A Proxy Auto-Configuration (PAC) is typically configured in the VPN profile. However, due to platform limitation, the PAC cannot be recognized by Android WebView, which is used during Edge sign-in process. Users may not be able to sign in to Edge in Android. 

Organizations can specify dedicated proxy via MDM policy for users to sign in to Edge in Android.

|Key  |Value  |
|:---------|:---------|
|EdgeOneAuthProxy |  The corresponding value is a string <br> **Example** `http://MyProxy.com:8080` |

### iOS Website data store

The website data store in Edge for iOS is essential for managing cookies, disk and memory caches, and various types of data. However, there is only one persistent website data store in Edge for iOS. By default, this data store is exclusively used by personal accounts, leading to a limitation where work or school accounts cannot utilize it. Consequently, browsing data, excluding cookies, is lost after each session for work or school accounts. To improve the user experience, organizations can configure the website data store for use by work or school accounts, ensuring the persistence of browsing data.

|Key |Value |
|:-----------|:-------------|
|com.microsoft.intune.mam.managedbrowser.PersistentWebsiteDataStore |**0** The website data store is always used only by personal account  <br>**1** The website data store will be used by the first signed-in account <br>**2** (Default) The website data store will be used by work or school account regardless of the sign-in order |

> [!NOTE]
> With the release of iOS 17, multiple persistent stores are now supported. Work and personal account have its own designated persistent store. Therefore, this policy is no longer valid from version 122.

### Microsoft Defender SmartScreen

Microsoft Defender SmartScreen is a feature that helps users avoid malicious sites and downloads. It is enabled by default. Organizations can disable this setting.

|Key |Value |
|:-----------|:-------------|
|com.microsoft.intune.mam.managedbrowser.SmartScreenEnabled |**true** (default) Microsoft Defender SmartScreen is enabled. <br>**false**  Microsoft Defender SmartScreen is disabled.|

### Certificate verification

By default, Microsoft Edge for Android verifies server certificates using the built-in certificate verifier and the Microsoft Root Store as the source of public trust. Organizations can switch to system certificate verifier and system root certificates.

|Key |Value |
|:-----------|:-------------|
|com.microsoft.intune.mam.managedbrowser.MicrosoftRootStoreEnabled |**true** (default) Use built-in certificate verifier and Microsoft Root Store to verify certificates <br>**false** Use system certificate verifier and system root certificates as the source of public trust to verify certificates |

> [!NOTE]
> A use case for this policy is that you need to use system certificate verifier and system root certificates when using [Microsoft MAM Tunnel in Edge for Android](../protect/microsoft-tunnel-mam-android.md).

#### SSL warning page control
By default, users can click through warning pages shows when users navigate to sites that have SSL errors. Organizations can manage the behavior.

|Key |Value |
|:-----------|:-------------|
|com.microsoft.intune.mam.managedbrowser.SSLErrorOverrideAllowed |**true** (default) Allow users to click through SSL warning pages <br>**false** Prevent users from clicking through SSL warning pages|

### Pop-ups settings
By default, pop-ups is blocked. Organizations can manage the behavior.

|Key |Value |
|:-----------|:-------------|
|com.microsoft.intune.mam.managedbrowser.DefaultPopupsSetting |**1** Allow all sites to show pop-ups <br>**2** (Default) Do not allow any site to show pop-ups|

### Allow pop-up on specific sites
If this policy is not configured, the value from the **DefaultPopupsSetting** policy (if set) or the user's personal configuration is used for all sites. Organizations can define a list of sites that can open pop-up. 

|Key |Value |
|:-----------|:-------------|
|com.microsoft.intune.mam.managedbrowser.PopupsAllowedForUrls |The corresponding value for the key is a list of URLs. You enter all the URLs you want to block as a single value, separated by a pipe `|` character. <br><br> **Examples:** <br>`URL1|URL2|URL3` <br>`http://www.contoso.com/|https://www.bing.com/|https://[*.]contoso.com`|

For more information about the URLs format, see [Enterprise policy URL pattern format](/deployedge/edge-learnmore-ent-policy-url-patterns).

### Block pop-up on specific sites
If this policy is not configured, the value from the **DefaultPopupsSetting** policy (if set) or the user's personal configuration is used for all sites. Organizations can define a list of sites that are blocked from opening pop-up.

|Key |Value |
|:-----------|:-------------|
|com.microsoft.intune.mam.managedbrowser.PopupsBlockedForUrls |The corresponding value for the key is a list of URLs. You enter all the URLs you want to block as a single value, separated by a pipe `|` character. <br><br> **Examples:** <br>`URL1|URL2|URL3` <br>`http://www.contoso.com/|https://www.bing.com/|https://[*.]contoso.com`|

For more information about the URLs format, see [Enterprise policy URL pattern format](/deployedge/edge-learnmore-ent-policy-url-patterns).

### Default search provider
By default, Edge uses the default search provider to perform a search when users enter non-URL texts in the address bar. Users can change the search provider list. Organizations can manage the search provider behavior.

|Key |Value |
|:-----------|:-------------|
|com.microsoft.intune.mam.managedbrowser.DefaultSearchProviderEnabled |**true** Enable the default search provider <br> **false** Disable the default search provider |

### Configure search provider
Organizations can configure a search provider for users. To configure a search provider, it's required to configure policy **DefaultSearchProviderEnabled** first. 

|Key |Value |
|:-----------|:-------------|
|com.microsoft.intune.mam.managedbrowser.DefaultSearchProviderName | The corresponding value is a string <br> **Example** `My Intranet Search`  |
|com.microsoft.intune.mam.managedbrowser.DefaultSearchProviderSearchURL | The corresponding value is a string <br> **Example** `https://search.my.company/search?q={searchTerms}`|

### Copilot

> [!NOTE]
> As of version 128, Copilot for work or school accounts has been deprecated. Therefore, the following policies will no longer be valid in version 128.
> If you want to block access to the web version of Copilot, copilot.microsoft.com, you can use policy AllowListURLs or BlockListURLs.

Copilot is available on Microsoft Edge for iOS and Android. Users can start Copilot by clicking on Copilot button in bottom bar. 

There are three settings in **Settings**->**General**->**Copilot**.

- **Show Copilot** – Control whether to show Bing button on bottom bar
- **Allow access to any web page or PDF** – Control whether to allow Copilot to access page content or PDF
- **Quick access on text selection** – Control whether to show quick chat panel when text on a webpage is selected

You can manage the settings for Copilot.

|Key |Value |
|:-----------|:-------------|
|com.microsoft.intune.mam.managedbrowser.Chat |**true** (default) Users can see Copilot button in bottom bar. Setting **Show Copilot** is on by default and can be turned off by users <br>**false** Users cannot see Copilot button in bottom bar. Setting **Show Copilot** is disabled and cannot be turned on by users|
|com.microsoft.intune.mam.managedbrowser.ChatPageContext |**true** (default) **Allow access to any web page or PDF** and **Quick access on text selection** can be turned on by users <br>**false** **Allow access to any web page or PDF** and **Quick access on text selection** will be disabled and cannot be turned on by users|

## Data protection app configuration scenarios

Edge for iOS and Android supports app configuration policies for the following data protection settings when the app is managed by Microsoft Intune with a managed apps App Configuration Policy applied to the work or school account that is signed into the app:

- Manage account synchronization
- Manage restricted web sites
- Manage proxy configuration
- Manage NTLM single sign-on sites

These settings can be deployed to the app regardless of device enrollment status.

### Manage account synchronization

By default, Microsoft Edge sync enables users to access their browsing data across all their signed-in devices. The data supported by sync includes:

- Favorites
- Passwords
- Addresses and more (autofill form entry)

Sync functionality is enabled via user consent and users can turn sync on or off for each of the data types listed above. For more information see [Microsoft Edge Sync](/DeployEdge/microsoft-edge-enterprise-sync).

Organizations have the capability to disable Edge sync on iOS and Android.

|Key |Value |
|:--|:----|
|com.microsoft.intune.mam.managedbrowser.account.syncDisabled |**true** disables Edge sync <br>**false** (default) allows Edge sync |

### Manage restricted web sites

Organizations can define which sites users can access within the work or school account context in Edge for iOS and Android. If you use an allow list, your users are only able to access the sites explicitly listed. If you use a blocked list, users can access all sites except for those explicitly blocked. You should only impose either an allowed or a blocked list, not both. If you impose both, only the allowed list is honored.

Organizations also define what happens when a user attempts to navigate to a restricted web site. By default, transitions are allowed. If the organization allows it, restricted web sites can be opened in the personal account context, the Microsoft Entra account’s InPrivate context, or whether the site is blocked entirely. For more information on the various scenarios that are supported, see [Restricted website transitions in Microsoft Edge mobile](https://techcommunity.microsoft.com/t5/intune-customer-success/restricted-website-transitions-in-microsoft-edge-mobile/ba-p/1381333). By allowing transitioning experiences, the organization's users stay protected, while keeping corporate resources safe.

To enhance the profile-switching experience by reducing the need for users to manually switch to personal profiles or InPrivate mode to open blocked URLs, we’ve introduced two new policies:
- `com.microsoft.intune.mam.managedbrowser.AutoTransitionModeOnBlock`
- `com.microsoft.intune.mam.managedbrowser.ProfileAutoSwitchToWork`

Since these policies bring different results based on their configurations and combinations, we recommend trying our policy suggestions below for a quick evaluation to see if the profile-switching experience aligns well with your organization’s needs before exploring detailed documentation. Suggested profile-switching configuration settings include the following values:
- `com.microsoft.intune.mam.managedbrowser.AllowTransitionOnBlock=true`
- `com.microsoft.intune.mam.managedbrowser.openInPrivateIfBlocked=true`
- `com.microsoft.intune.mam.managedbrowser.AutoTransitionModeOnBlock=1`
- `com.microsoft.intune.mam.managedbrowser.ProfileAutoSwitchToWork=2`

> [!NOTE]
> Edge for iOS and Android can block access to sites only when they're accessed directly. It doesn't block access when users use intermediate services (such as a translation service) to access the site. URLs that start with **Edge**, such as `Edge://*`, `Edge://flags`, and `Edge://net-export`, aren't supported in app configuration policy **AllowListURLs** or **BlockListURLs** for managed apps. You can disable these URLs with **com.microsoft.intune.mam.managedbrowser.InternalPagesBlockList**. <br><br> If your devices are managed, you can also use app configuration policy [URLAllowList](/deployedge/microsoft-edge-mobile-policies#urlallowlist) or [URLBlocklist](/deployedge/microsoft-edge-mobile-policies#urlblocklist) for managed devices. For related information, see [Microsoft Edge mobile policies](/deployedge/microsoft-edge-mobile-policies).

Use the following key/value pairs to configure either an allowed or blocked site list for Edge for iOS and Android. 

|Key |Value |
|:--|:----|
|com.microsoft.intune.mam.managedbrowser.AllowListURLs <br><br> This policy name has been replaced by the UI of **Allowed URLs** under Edge Configuration settings|The corresponding value for the key is a list of URLs. You enter all the URLs you want to allow as a single value, separated by a pipe `|` character. <br><br>**Examples:** <br>`URL1|URL2|URL3` <br>`http://www.contoso.com/|https://www.bing.com/|https://expenses.contoso.com` |
|com.microsoft.intune.mam.managedbrowser.BlockListURLs <br><br> This policy name has been replaced by the UI of **Blocked URLs** under Edge Configuration settings|The corresponding value for the key is a list of URLs. You enter all the URLs you want to block as a single value, separated by a pipe `|` character. <br><br> **Examples:** <br>`URL1|URL2|URL3` <br>`http://www.contoso.com/|https://www.bing.com/|https://expenses.contoso.com` |
|com.microsoft.intune.mam.managedbrowser.AllowTransitionOnBlock <br><br> This policy name has been replaced by the UI of **Redirect restricted sites to personal context** under Edge Configuration settings|**true** (default) allows Edge for iOS and Android to transition restricted sites. When personal accounts aren't disabled, users are prompted to either switch to the personal context to open the restricted site, or to add a personal account. If com.microsoft.intune.mam.managedbrowser.openInPrivateIfBlocked is set to true, users have the capability of opening the restricted site in the InPrivate context. <br>**false** prevents Edge for iOS and Android from transitioning users. Users are simply shown a message stating that the site they are trying to access is blocked. |
|com.microsoft.intune.mam.managedbrowser.openInPrivateIfBlocked |**true** allows restricted sites to be opened in the Microsoft Entra account's InPrivate context. If the Microsoft Entra account is the only account configured in Edge for iOS and Android, the restricted site is opened automatically in the InPrivate context. If the user has a personal account configured, the user is prompted to choose between opening InPrivate or switch to the personal account. <br>**false** (default) requires the restricted site to be opened in the user's personal account. If personal accounts are disabled, then the site is blocked. <br>In order for this setting to take effect, com.microsoft.intune.mam.managedbrowser.AllowTransitionOnBlock must be set to true. |
|com.microsoft.intune.mam.managedbrowser.durationOfOpenInPrivateSnackBar | Enter the number of seconds that users will see the snack bar notification "Access to this site is blocked by your organization. We’ve opened it in InPrivate mode for you to access the site." By default, the snack bar notification is shown for 7 seconds.|

The following sites except copilot.microsoft.com are always allowed regardless of the defined allow list or block list settings:
- `https://*.microsoft.com/*`
- `http://*.microsoft.com/*`
- `https://microsoft.com/*`
- `http://microsoft.com/*`
- `https://*.windowsazure.com/*`
- `https://*.microsoftonline.com/*`
- `https://*.microsoftonline-p.com/*`

### Control the behavior of the Site Blocked popup
When attempting to access blocked websites, users will be prompted to use either switch to InPrivate or personal account to open the blocked websites. You can choose preferences between InPrivate and personal account.

|Key |Value |
|:--|:----|
|com.microsoft.intune.mam.managedbrowser.AutoTransitionModeOnBlock |**0**: (Default) Always show the popup window for user to choose.<br>**1**: Automatically switch to personal account when personal account is signed in.If personal account is not signed in, the behavior will be changed to value 2. <br>**2**:Automatically switch to InPrivate if InPrivate switch is allowed by com.microsoft.intune.mam.managedbrowser.openInPrivateIfBlocked=true. |

### Control the behavior of the post request when account switch
When attempting to access blocked websites, users will be prompted to use either switch to InPrivate or personal account to open the blocked websites. You can choose preferences on how to handle the post request during the account switch. The MAM policy is only for iOS.

|Key |Value |
|:--|:----|
|com.microsoft.intune.mam.managedbrowser.IgnorePostRequestOnAutoTransition |**false**: (Default) Continue the post request when URL blocked switches to private mode or personal account.<br>**true**: Ignore the post request when URL blocked switches to private mode or personal account.|

### Control the behavior of switching personal profile to work profile 
When Edge is under the personal profile and users are attempting to open a link from Outlook or Microsoft Teams which are under the work profile, by default, Intune will use the Edge work profile to open the link because both Edge, Outlook, and Microsoft Teams are managed by Intune. However, when the link is blocked, the user will be switched to the the personal profile. This causes a friction experience for users

You can configure a policy to enhance users' experience. This policy is recommended to be used together with AutoTransitionModeOnBlock as it may switch users to the personal profile according to the policy value you configured.

|Key |Value |
|:--|:----|
|com.microsoft.intune.mam.managedbrowser.ProfileAutoSwitchToWork |**1**: (Default) Switch to work profile even if the URL is blocked by Edge policy.<br> **2**: The blocked URLs will open under personal profile if personal profile is signed in. If personal profile is not signed in, the blocked URL will opened in InPrivate mode. |

#### Manage Sub Resource Blocking
By default, AllowListURLs and BlockListURLs apply only at the navigation level. When you embed blocked URLs (either URLs configured in BlockListURLs or URLs not configured in AllowListURLs) as sub resources within a web page, those sub resource URLs are not blocked. 

To further restrict these sub resources, you can configure a policy to block the sub resource URLs.

|Key |Value |
|:--|:----|
|com.microsoft.intune.mam.managedbrowser.ManageRestrictedSubresourceEnabled |**false**: (Default) Sub resource URLs will not be blocked even if the sub resource URLs are blocked.<br> **true**: Sub resource URLs will be blocked if they are listed as blocked. |

> [!NOTE]
> It is recommended to use this policy in conjunction with BlockListURLs. If used with AllowListURLs, ensure that all sub resource URLs are included in the AllowListURLs. Otherwise, some sub resources may fail to load

#### URL formats for allowed and blocked site list

You can use various URL formats to build your allowed/blocked sites lists. These permitted patterns are detailed in the following table.

- Ensure that you prefix all URLs with **http://** or **https://** when entering them into the list.
- You can use the wildcard symbol (\*) according to the rules in the following permitted patterns list.
- A wildcard can only match a portion (e.g., `news-contoso.com`) or entire component of the hostname (e.g., `host.contoso.com`) or entire parts of the path when separated by forward slashes (`www.contoso.com/images`).
- You can specify port numbers in the address. If you do not specify a port number, the values used are:
  - Port 80 for http
  - Port 443 for https
- Using wildcards for the port number is supported in Edge for iOS only. For example, you can specify `http://www.contoso.com:*` and `http://www.contoso.com:*/`.
- Specifying IPv4 addresses with CIDR notation is supported. For example, you can specify 127.0.0.1/24 (a range of IP addresses).

  |URL |Details |Matches |Does not match |
  |:----|:-------|:----------|:----------------|
  |`http://www.contoso.com` |Matches a single page |`www.contoso.com` |`host.contoso.com` <br>`www.contoso.com/images` <br>`contoso.com/` |
  |`http://contoso.com`|Matches a single page |`contoso.com/`|`host.contoso.com` <br>`www.contoso.com/images` <br>`www.contoso.com` |
  |`http://www.contoso.com/*`|Matches all URLs that begin with `www.contoso.com`|`www.contoso.com` <br>`www.contoso.com/images` <br>`www.contoso.com/videos/tvshows` |`host.contoso.com` <br>`host.contoso.com/images`|
  |`http://*.contoso.com/*`|Matches all subdomains under `contoso.com`|`developer.contoso.com/resources` <br>`news.contoso.com/images` <br>`news.contoso.com/videos` |`contoso.host.com` <br>`news-contoso.com`|
  |`http://*contoso.com/*`|Matches all subdomains ending with `contoso.com/`|`news-contoso.com` <br>`news-contoso.com/daily` |`news-contoso.host.com` <br>`news.contoso.com`|
  |`http://www.contoso.com/images`|Matches a single folder |`www.contoso.com/images`|`www.contoso.com/images/dogs`|
  |`http://www.contoso.com:80`|Matches a single page, by using a port number |`www.contoso.com:80`| |
  |`https://www.contoso.com`|Matches a single, secure page|`www.contoso.com`|`www.contoso.com/images`|
  |`http://www.contoso.com/images/*` |Matches a single folder and all subfolders |`www.contoso.com/images/dogs` <br>`www.contoso.com/images/cats` | `www.contoso.com/videos`|
  |`http://contoso.com:*` |Matches any port number for a single page |`contoso.com:80` <br>`contoso.com:8080` | |
  |`10.0.0.0/24` |Matches a range of IP addresses from 10.0.0.0 to 10.0.0.255 |`10.0.0.0` <br>`10.0.0.100`| `192.168.1.1`| 
    
  - The following are examples of some of the inputs that you can't specify:
  - `*.com`
  - `*.contoso/*`
  - `www.contoso.com/*images`
  - `www.contoso.com/*images*pigs`
  - `www.contoso.com/page*`
  - `https://*`
  - `http://*`
  - `http://www.contoso.com: /*`

### Disable Edge internal pages
You can disable Edge internal pages such as `Edge://flags` and `Edge://net-export`. More pages can be found from `Edge://about`

|Key |Value |
|:--|:----|
|com.microsoft.intune.mam.managedbrowser.InternalPagesBlockList | The corresponding value for the key is a list of page names. You can enter the internal pages you want to block as a single value, separated by a pipe `|` character. <br><br> **Examples:** <br>`flags|net-export`|

### Manage websites to allow upload files
There may be scenarios where users are only allowed to view websites, without the ability to upload files. Organizations have the option to designate which websites can receive file uploads.

|Key |Value |
|:-----------|:-------------|
|com.microsoft.intune.mam.managedbrowser.FileUploadAllowedForUrls |The corresponding value for the key is a list of URLs. You enter all the URLs you want to block as a single value, separated by a pipe `|` character. <br><br> **Examples:** <br>`URL1|URL2|URL3` <br>`https://contoso.com/|http://contoso.com/|https://[*.]contoso.com|[*.]contoso.com`|
|com.microsoft.intune.mam.managedbrowser.FileUploadBlockedForUrls | The corresponding value for the key is a list of URLs. You enter all the URLs you want to block as a single value, separated by a pipe `|` character. <br><br> **Examples:** <br>`URL1|URL2|URL3` <br>`https://external.filesupload1.com/|http://external.filesupload2.com/|https://[*.]external.filesupload1.com|[*.]filesupload1.com`|

The example to block all websites, including internal websites, from uploading files
- com.microsoft.intune.mam.managedbrowser.FileUploadBlockedForUrls=`*`

An example to allow specific websites to upload files
- com.microsoft.intune.mam.managedbrowser.FileUploadAllowedForUrls=`https://[*.]contoso.com/|[*.]sharepoint.com/`
- com.microsoft.intune.mam.managedbrowser.FileUploadBlockedForUrls=`*`

For more information about the URLs format, see [Enterprise policy URL pattern format](/deployedge/edge-learnmore-ent-policy-url-patterns).

> [!NOTE]
> For Edge on iOS, the paste action will be blocked in addition to uploads. Users will not see the paste option in the action menu.

### Manage proxy configuration

You can use Edge for iOS and Android and [Microsoft Entra application proxy](/azure/active-directory/active-directory-application-proxy-get-started) together to give users access to intranet sites on their mobile devices. For example: 

- A user is using the Outlook mobile app, which is protected by Intune. They then click a link to an intranet site in an email, and Edge for iOS and Android recognizes that this intranet site has been exposed to the user through Application Proxy. The user is automatically routed through Application Proxy, to authenticate with any applicable multi-factor authentication and Conditional Access, before reaching the intranet site. The user is now able to access internal sites, even on their mobile devices, and the link in Outlook works as expected.
- A user opens Edge for iOS and Android on their iOS or Android device. If Edge for iOS and Android is protected with Intune, and Application Proxy is enabled, the user can go to an intranet site by using the internal URL they are used to. Edge for iOS and Android recognizes that this intranet site has been exposed to the user through Application Proxy. The user is automatically routed through Application Proxy, to authenticate before reaching the intranet site.

Before you start:

- Set up your internal applications through Microsoft Entra application proxy.
  - To configure Application Proxy and publish applications, see the [setup documentation](/azure/active-directory/manage-apps/application-proxy).
  - Ensure that the user is assigned to the Microsoft Entra application proxy app, even if the app is configured with Passthrough pre-authentication type.
- The Edge for iOS and Android app must have an [Intune app protection policy](app-protection-policy.md) assigned.
- Microsoft apps must have an app protection policy that has **Restrict web content transfer with other apps** data transfer setting set to **Microsoft Edge**.

> [!NOTE]
> Edge for iOS and Android updates the Application Proxy redirection data based on the last successful refresh event. Updates are attempted whenever the last successful refresh event is greater than one hour.

Target Edge for iOS and Android with the following key/value pair, to enable Application Proxy.

|Key |Value|
|:-------------|:-------------|
|com.microsoft.intune.mam.managedbrowser.AppProxyRedirection <br><br> This policy name has been replaced by the UI of **Application proxy redirection** under Edge Configuration settings |**true** enables Microsoft Entra application proxy redirection scenarios <br>**false** (default) prevents Microsoft Entra application proxy scenarios |

For more information about how to use Edge for iOS and Android and Microsoft Entra application proxy in tandem for seamless (and protected) access to on-premises web apps, see [Better together: Intune and Microsoft Entra team up to improve user access](https://techcommunity.microsoft.com/t5/enterprise-mobility-security/better-together-intune-and-azure-active-directory-team-up-to/ba-p/250254). This blog post references the Intune Managed Browser, but the content applies to Edge for iOS and Android as well.

### Manage NTLM single sign-on sites

Organizations may require users to authenticate with NTLM to access intranet web sites. By default, users are prompted to enter credentials each time they access a web site that requires NTLM authentication as NTLM credential caching is disabled. 

Organizations can enable NTLM credential caching for particular web sites. For these sites, after the user enters credentials and successfully authenticates, the credentials are cached by default for 30 days.

> [!NOTE]
> If you're using a proxy server, ensure that it's configured using the NTLMSSOURLs policy where you specifically specify both **https** and **http** as part of the key value. 
>
> Currently, both **https** and **http** schemes need to be specified in the NTLMSSOURLs key value. For example, you need to configure both `https://your-proxy-server:8080`
> and `http://your-proxy-server:8080`. Currently, specifying the format as host:port (such as `your-proxy-server:8080`) is not sufficient.
>
> In addition, the wildcard symbol (*) is not supported when configuring proxy servers in the NTLMSSOURLs policy.

|Key  |Value  |
|:---------|:---------|
|com.microsoft.intune.mam.managedbrowser.NTLMSSOURLs |The corresponding value for the key is a list of URLs. You enter all the URLs you want to allow as a single value, separated by a pipe `|` character. <br><br>**Examples:** <br>`URL1|URL2` <br>`http://app.contoso.com/|https://expenses.contoso.com` <br><br>For more information on the types of URL formats that are supported, see [URL formats for allowed and blocked site list](#url-formats-for-allowed-and-blocked-site-list). |
|com.microsoft.intune.mam.managedbrowser.durationOfNTLMSSO |Number of hours to cache credentials, default is 720 hours |

## Additional app configuration for managed devices

The following policies, originally configurable through managed apps app configuration policy, is now available through managed devices app configuration policy. When using policies for managed apps, users must sign into Microsoft Edge. When using policies for managed devices, users aren't required to sign into Edge to apply the policies.

As app configuration policies for managed devices needs device enrollment, any unified endpoint management (UEM) is supported. To find more policies under the MDM channel, see [Microsoft Edge Mobile Policies](/deployedge/microsoft-edge-mobile-policies). 

|     MAM policy    |     MDM policy    |
|---|---|
|     com.microsoft.intune.mam.managedbrowser.NewTabPage.CustomURL    |     EdgeNewTabPageCustomURL    |
|     com.microsoft.intune.mam.managedbrowser.MyApps    |     EdgeMyApps    |
|     com.microsoft.intune.mam.managedbrowser.defaultHTTPS       |     EdgeDefaultHTTPS    |
|     com.microsoft.intune.mam.managedbrowser.disableShareUsageData    |     EdgeDisableShareUsageData    |
|     com.microsoft.intune.mam.managedbrowser.disabledFeatures    |     EdgeDisabledFeatures    |
|     com.microsoft.intune.mam.managedbrowser.disableImportPasswords    |     EdgeImportPasswordsDisabled    |
|     com.microsoft.intune.mam.managedbrowser.enableKioskMode    |     EdgeEnableKioskMode    |
|     com.microsoft.intune.mam.managedbrowser.showAddressBarInKioskMode    |     EdgeShowAddressBarInKioskMode    |
|     com.microsoft.intune.mam.managedbrowser.showBottomBarInKioskMode    |     EdgeShowBottomBarInKioskMode    |
|     com.microsoft.intune.mam.managedbrowser.account.syncDisabled    |     EdgeSyncDisabled    |
|     com.microsoft.intune.mam.managedbrowser.NetworkStackPref    |     EdgeNetworkStackPref    |
| com.microsoft.intune.mam.managedbrowser.SmartScreenEnabled | SmartScreenEnabled|
|     com.microsoft.intune.mam.managedbrowser.MicrosoftRootStoreEnabled | MicrosoftRootStoreEnabled |
| com.microsoft.intune.mam.managedbrowser.SSLErrorOverrideAllowed | SSLErrorOverrideAllowed|
|com.microsoft.intune.mam.managedbrowser.DefaultPopupsSetting | DefaultPopupsSetting|
|com.microsoft.intune.mam.managedbrowser.PopupsAllowedForUrls | PopupsAllowedForUrls|
|com.microsoft.intune.mam.managedbrowser.PopupsBlockedForUrls | PopupsBlockedForUrls|
|com.microsoft.intune.mam.managedbrowser.DefaultSearchProviderEnabled	| DefaultSearchProviderEnabled|
|com.microsoft.intune.mam.managedbrowser.DefaultSearchProviderName | DefaultSearchProviderName|
|com.microsoft.intune.mam.managedbrowser.DefaultSearchProviderSearchURL | DefaultSearchProviderSearchURL|
|com.microsoft.intune.mam.managedbrowser.Chat | EdgeCopilotEnabled |
|com.microsoft.intune.mam.managedbrowser.ChatPageContext	| EdgeChatPageContext|

## Deploy app configuration scenarios with Microsoft Intune

If you are using Microsoft Intune as your mobile app management provider, the following steps allow you to create a managed apps app configuration policy. After the configuration is created, you can assign its settings to groups of users.

1. Sign into the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Apps** and then select **App configuration policies**.

3. On the **App Configuration policies** blade, choose **Add** and select **Managed apps**.

4. On the **Basics** section, enter a **Name**, and optional **Description** for the app configuration settings.

5. For **Public apps**, choose **Select public apps**, and then, on the **Targeted apps** blade, choose **Edge for iOS and Android** by selecting both the iOS and Android platform apps. Click **Select** to save the selected public apps.

6. Click **Next** to complete the basic settings of the app configuration policy.

7. On the **Settings** section, expand the **Edge configuration settings**.

8. If you want to manage the data protection settings, configure the desired settings accordingly:

    - For **Application proxy redirection**, choose from the available options: **Enable**, **Disable** (default).

    - For **Homepage shortcut URL**, specify a valid URL that includes the prefix of either *http://* or *https://*. Incorrect URLs are blocked as a security measure.

    - For **Managed bookmarks**, specify the title and a valid URL that includes the prefix of either *http://* or *https://*.

    - For **Allowed URLs**, specify a valid URL (only these URLs are allowed; no other sites can be accessed). For more information on the types of URL formats that are supported, see [URL formats for allowed and blocked site list](#url-formats-for-allowed-and-blocked-site-list).

    - For **Blocked URLs**, specify a valid URL (only these URLs are blocked). For more information on the types of URL formats that are supported, see [URL formats for allowed and blocked site list](#url-formats-for-allowed-and-blocked-site-list).

    - For **Redirect restricted sites to personal context**, choose from the available options: **Enable** (default), **Disable**.

    > [!NOTE]
    > When both Allowed URLs and Blocked URLs are defined in the policy, only the allowed list is honored.

9. If you want to additional app configuration settings not exposed in the above policy, expand the **General configuration settings** node and enter in the key value pairs accordingly.

10. When you are finished configuring the settings, choose **Next**.

11. On the **Assignments** section, choose **Select groups to include**. Select the Microsoft Entra group to which you want to assign the app configuration policy, and then choose **Select**.

12. When you are finished with the assignments, choose **Next**.

13. On the **Create app configuration policy Review + Create** blade, review the settings configured and choose **Create**.

The newly created configuration policy is displayed on the **App configuration** blade.

## Use Microsoft Edge for iOS and Android to access managed app logs  

Users with Edge for iOS and Android installed on their iOS or Android device can view the management status of all Microsoft published apps. They can send logs for troubleshooting their managed iOS or Android apps by using the following steps:

1. Open Edge for iOS and Android on your device.

2. Type `edge://intunehelp/` in the address box.

3. Edge for iOS and Android launches troubleshooting mode.

You can retrieve logs from Microsoft Support by giving them the user's incident ID.  

For a list of the settings stored in the app logs, see [Review client app protection logs](app-protection-policy-settings-log.md). 

## Diagnostic logs

In additional to Intune logs from `edge://intunehelp/`, you may be asked by Microsoft Support to provide diagnostic logs of Microsoft Edge for iOS and Android. You can either upload the logs to Microsoft server or save them locally and share them directly with Microsoft Support.

### Upload logs to Microsoft server
Follow these steps to upload logs to Microsoft server:
1. Reproduce the issue.
2. Open the overflow menu by selecting the hamburger icon at the bottom-right corner.
3. Swipe left and select **Help and feedback**.
4. In the **Describe what's happening section**, provide details about the issue so the support team can identify the relevant logs.
5. Upload the logs to Microsoft server by selecting the button at the top-right corner.


### Save logs locally and share directly with Microsoft Support
Follow these steps to save logs locally and share them:
1. Reproduce the issue.
2. Open overflow menu by selecting on the hamburger menu on the bottom-right corner.
3. Swipe left and select **Help and feedback**.
4. Select **diagnostic data**.
6. For Microsoft Edge for iOS, tap the **Share** icon at the top-right corner. The OS sharing dialog will appear, allowing you to save the logs locally or share them via other apps.
For Microsoft Edge for Android, open the submenu in the top-right corner and select the option to save logs. The logs will be saved in the **Download** > **Edge** folder.

If you want to clear the old logs, select the **Clear** icon at the top-right when selecting **diagnostic data**. Then, reproduce the issue again to ensure that only fresh logs are captured.

> [!NOTE]
> Saving logs also respects the Intune App Protection Policy. Therefore, you may not be allowed to save diagnostic data to local devices.

## Next steps

- [What are app protection policies?](app-protection-policy.md) 
- [App configuration policies for Microsoft Intune](app-configuration-policies-overview.md)
