---
# required metadata

title: Manage Edge for iOS and Android for iOS and Android with Intune 
titleSuffix: 
description: Use Intune app protection policies with Edge for iOS and Android to ensure corporate websites are always accessed with safeguards in place. 
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 05/11/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology:
ms.assetid: 3fb2f050-ec94-42ab-be05-c3d4101148bb

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: ilwu
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Manage web access by using Edge for iOS and Android with Microsoft Intune

Edge for iOS and Android is designed to enable users to browse the web and supports multi-identity. Users can add a work account, as well as a personal account, for browsing. There is complete separation between the two identities, which is like what is offered in other Microsoft mobile apps.

Edge for iOS is supported on iOS 12.0 and later. Edge for Android is supported on Android 5 and later.

> [!NOTE]
> Edge for iOS and Android doesn't consume settings that users set for the native browser on their devices, because Edge for iOS and Android can't access these settings.

The richest and broadest protection capabilities for Office 365 data are available when you subscribe to the Enterprise Mobility + Security suite, which includes Microsoft Intune and Azure Active Directory Premium features, such as conditional access. At a minimum, you will want to deploy a conditional access policy that only allows connectivity to Edge for iOS and Android from mobile devices and an Intune app protection policy that ensures the browsing experience is protected.

> [!NOTE]
> New web clips (pinned web apps) on iOS devices will open in Edge for iOS and Android instead of the Intune Managed Browser when required to open in a protected browser. For older iOS web clips, you must re-target these web clips to ensure they open in Edge for iOS and Android rather than the Managed Browser.

## Apply Conditional Access
Organizations can use use Azure AD Conditional Access policies to ensure that users can only access work or school content using Edge for iOS and Android. To do this, you will need a conditional access policy that targets all potential users. Details on creating this policy can be found in [Require app protection policy for cloud app access with Conditional Access](https://docs.microsoft.com/azure/active-directory/conditional-access/app-protection-based-conditional-access).

1. Follow [Scenario 3: Browser apps require approved apps with app protection policies](https://docs.microsoft.com/azure/active-directory/conditional-access/app-protection-based-conditional-access), which allows Edge for iOS and Android, but blocks other mobile device web browsers from connecting to Office 365 endpoints.

   >[!NOTE]
   > This policy ensures mobile users can access all Office 365 endpoints from within Edge for iOS and Android. This policy also prevents users from using InPrivate to access Office 365 endpoints.

With Conditional Access, you can also target on-premises sites that you have exposed to external users via the [Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-get-started).

## Create Intune app protection policies

App Protection Policies (APP) define which apps are allowed and the actions they can take with your organization's data. The choices available in APP enable organizations to tailor the protection to their specific needs. For some, it may not be obvious which policy settings are required to implement a complete scenario. To help organizations prioritize mobile client endpoint hardening, Microsoft has introduced taxonomy for its APP data protection framework for iOS and Android mobile app management.

The APP data protection framework is organized into three distinct configuration levels, with each level building off the previous level:

- **Enterprise basic data protection** (Level 1) ensures that apps are protected with a PIN and encrypted and performs selective wipe operations. For Android devices, this level validates Android device attestation. This is an entry level configuration that provides similar data protection control in Exchange Online mailbox policies and introduces IT and the user population to APP.
- **Enterprise enhanced data protection** (Level 2) introduces APP data leakage prevention mechanisms and minimum OS requirements. This is the configuration that is applicable to most mobile users accessing work or school data.
- **Enterprise high data protection** (Level 3) introduces advanced data protection mechanisms, enhanced PIN configuration, and APP Mobile Threat Defense. This configuration is desirable for users that are accessing high risk data.

To see the specific recommendations for each configuration level and the minimum apps that must be protected, review [Data protection framework using app protection policies](app-protection-framework.md).

Regardless of whether the device is enrolled in an MDM solution, an Intune app protection policy needs to be created for both iOS and Android apps, using the steps in [How to create and assign app protection policies](app-protection-policies.md). These policies, at a minimum, must meet the following conditions:

1. They include all Microsoft mobile applications, such as Outlook, OneDrive, Office, or Teams, as this will ensure that users can access and manipulate work or school data within any Microsoft app in a secure fashion.

2. They are assigned to all users. This ensures that all users are protected, regardless of whether they use Edge for iOS or Android.

3. Determine which framework level meets your requirements. Most organizations should implement the settings defined in **Enterprise enhanced data protection** (Level 2) as that enables data protection and access requirements controls.

For more information on the available settings, see [Android app protection policy settings](app-protection-policy-settings-android.md) and [iOS app protection policy settings](app-protection-policy-settings-ios.md).

> [!IMPORTANT]
> To apply Intune app protection policies against apps on Android devices that are not enrolled in Intune, the user must also install the Intune Company Portal. For more information, see [What to expect when your iOS/iPadOS app is managed by app protection policies](../fundamentals/end-user-mam-apps-ios.md).

## Single sign-on to Azure AD-connected web apps in policy-protected browsers

Edge for iOS and Android on iOS and Android can take advantage of single sign-on (SSO) to all web apps (SaaS and on-premises) that are Azure AD-connected. SSO allows users to access Azure AD-connected web apps through Edge for iOS and Android, without having to re-enter their credentials.

SSO requires your device to be registered by either the Microsoft Authenticator app for iOS devices, or the Intune Company Portal on Android. When users have either of these, they are prompted to register their device when they go to an Azure AD-connected web app in a policy-protected browser (this is only true if their device hasn't already been registered). After the device is registered with the user's account managed by Intune, that account has SSO enabled for Azure AD-connected web apps.

> [!NOTE]
> Device registration is a simple check-in with the Azure AD service. It doesn't require full device enrollment, and doesn't give IT any additional privileges on the device.

## Utilize app configuration to manage the browsing experience

Edge for iOS and Android supports app settings that allow mobile device management (MDM), like Microsoft Endpoint Manager, administrators to customize the behavior of the app.

App configuration can be delivered either through the MDM OS channel on enrolled devices ([Managed App Configuration](https://developer.apple.com/library/content/samplecode/sc2279/Introduction/Intro.html) channel for iOS or the [Android in the Enterprise](https://developer.android.com/work/managed-configurations) channel for Android) or through the Intune App Protection Policy (APP) channel. Edge for iOS and Android supports the following configuration scenarios:

- Organization allowed accounts mode
- General app configuration settings
- Data protection settings

> [!IMPORTANT]
> For configuration scenarios that require device enrollment on Android, the devices must be enrolled in Android Enterprise and Edge for Android must be deployed via the managed Google Play store. For more information, see [Set up enrollment of Android Enterprise work profile devices](../enrollment/android-work-profile-enroll.md) and [Add app configuration policies for managed Android Enterprise devices](app-configuration-policies-use-android.md).

Each configuration scenario highlights its specific requirements. For example, whether the configuration scenario requires device enrollment, and thus works with any MDM provider, or requires Intune App Protection Policies.

> [!NOTE]
> With Microsoft Endpoint Manager, app configuration delivered through the MDM OS channel is referred to as a **Managed Devices** App Configuration Policy (ACP); app configuration delivered through the App Protection Policy channel is referred to as a **Managed Apps** App Configuration Policy.

## Only allow work or school accounts

Respecting the data security and compliance policies of our largest and highly regulated customers is a key pillar to the Microsoft 365 value. Some companies have a requirement to capture all communications information within their corporate environment, as well as, ensure the devices are only used for corporate communications. To support these requirements, Edge for iOS and Android on enrolled devices can be configured to only allow a single corporate account to be provisioned within the app.

You can learn more about configuring the org allowed accounts mode setting here:

- [Android setting](app-configuration-policies-use-android.md#allow-only-configured-organization-accounts-in-multi-identity-apps)
- [iOS setting](app-configuration-policies-use-ios.md#allow-only-configured-organization-accounts-in-multi-identity-apps)

This configuration scenario only works with enrolled devices. However, any MDM provider is supported. If you are not using Microsoft Endpoint Manager, you need to consult with your MDM documentation on how to deploy these configuration keys.

## General app configuration scenarios

Edge for iOS and Android offers administrators the ability to customize the default configuration for several in-app settings. This capability is currently only offered when Edge for iOS and Android has an Intune App Protection Policy applied.

> [!IMPORTANT]
> Edge for Android does not support Chromium settings that are available in Managed Google Play.

Edge supports the following settings for configuration:

- New Tab Page experiences
- Bookmark experiences
- App behavior experiences
- Kiosk mode experiences

### New Tab Page experiences

Edge for iOS and Android offers organizations several options for adjusting the New Tab Page experience.

#### Organization logo and brand color

These settings allow you to customize the New Tab Page for Edge for iOS and Android to display your organization's logo and brand color as the page background.

To upload your organization's logo and color, first complete the following steps:
1. Within [Microsoft Endpoint Manager](https://endpoint.microsoft.com), navigate to **Tenant Administration** -> **Customization** -> **Company Identity Branding**.
2. To set your brand's logo, under "Display", choose "Company Logo only". Transparent background logos are recommended.
3. To set your brand's background color, under "Display" choose "Theme Color". Edge for iOS and Android applies a lighter shade of the color on the New Tab Page, which ensures the page has high readability.

Next, utilize the following key/value pairs to pull your organization's branding into Edge for iOS and Android:

|    Key    |    Value    |
|--------------------------------------------------------------------|------------|
|    com.microsoft.intune.mam.managedbrowser.NewTabPage.BrandLogo    |    **true** shows organization's brand logo<br>**false** (default) will not expose a logo    |
|    com.microsoft.intune.mam.managedbrowser.NewTabPage.BrandColor    |    **true** shows organization's brand color<br>**false** (default) will not expose a color    |

#### Homepage shortcut

This setting allows you to configure a homepage shortcut for Edge for iOS and Android. The homepage shortcut you configure appears as the first icon beneath the search bar when the user opens a new tab in Edge for iOS and Android. The user can't edit or delete this shortcut in their managed context. The homepage shortcut displays your organization's name to distinguish it. 

Use the following key/value pair to configure a homepage shortcut:

|    Key    |    Value    |
|-------------------------------------------------------------------|-------------|
|    com.microsoft.intune.mam.managedbrowser.homepage   |    Specify a valid URL. Incorrect URLs are blocked as a security measure.<br>**Example:** <`https://www.bing.com`>     |

#### Multiple top site shortcuts

Similarly to configuring a homepage shortcut, you can configure multiple top site shortcuts on new tab pages in Edge for iOS and Android. The user can't edit or delete these shortcuts in a managed context. Note: you can configure a total of 8 shortcuts, including a homepage shortcut. If you have configured a homepage shortcut, that will override the first top site configured. 

|    Key    |    Value    |
|-------------------------------------------------------------------|-------------|
|    com.microsoft.intune.mam.managedbrowser.managedTopSites   |    Specify set of value URLs. Each top site shortcut consists of a title and URL. Separate the title and URL with the `|` character. For example: <br> `GitHub|https://github.com/||LinkedIn|https://www.linkedin.com`    |

#### Industry news

You can configure the New Tab Page experience within Edge for iOS and Android to display industry news that is relevant to your organization. When you enable this feature, Edge for iOS and Android uses your organization's domain name to aggregate news from the web about your organization, organization's industry, and competitors, so your users can find relevant external news all from the centralized new tab pages within Edge for iOS and Android. Industry News is off by default. 

|    Key    |    Value    |
|------------------------------------------------------|----------------------------------------------------------------------------------------------------------------|
|    com.microsoft.intune.mam.managedbrowser.NewTabPage.IndustryNews    |    **true** shows Industry News on the New Tab Page<br>**false** (default) hides Industry News from the New Tab Page    |

### Bookmark experiences

Edge for iOS and Android offers organizations several options for managing bookmarks.

#### Managed bookmarks

For ease of access, you can configure bookmarks that you'd like your users to have available when they are using Edge for iOS and Android.

- Bookmarks only appear in the work or school account and are not exposed to personal accounts.
- Bookmarks can't be deleted or modified by users.
- Bookmarks appear at the top of the list. Any bookmarks that users create appear below these bookmarks.
- If you have enabled Application Proxy redirection, you can add Application Proxy web apps by using either their internal or external URL.
- Ensure that you prefix all URLs with **http://** or **https://** when entering them into the list.

Use the following key/value pair to configure managed bookmarks:

|    Key    |    Value    |
|---------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    com.microsoft.intune.mam.managedbrowser.bookmarks    |    The value for this configuration is a   list of bookmarks. Each bookmark consists of the bookmark title and the   bookmark URL. Separate the title and URL with the `|` character.      Example:<br>`Microsoft Bing|https://www.bing.com`<br>To configure multiple bookmarks, separate each pair with the double character `||`.<p>Example:<br>`Microsoft Bing|https://www.bing.com||Contoso|https://www.contoso.com`    |

#### MyApps sites

By default, users are shown the MyApps sites that are configured to them within a folder inside Edge for iOS and Android bookmarks. The folder is labeled with the name of your organization.

|    Key    |    Value    |
|---------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    com.microsoft.intune.mam.managedbrowser.MyApps    |    **true** (default) shows MyApps within the Edge for iOS and Android bookmarks<br>**false** hides MyApps within Edge for iOS and Android    |

### App behavior experiences

Edge for iOS and Android offers organizations several options for managing the app's behavior.

#### Default protocol handler

By default, Edge for iOS and Android uses the HTTPS protocol handler when the user doesn't specify the protocol in the URL. Generally, this is considered a best practice, but can be disabled.

|    Key    |    Value    |
|---------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    com.microsoft.intune.mam.managedbrowser.defaultHTTPS     |     **true** (default) default protocol handler is HTTPS<br>**false** default protocol handler is HTTP     |

#### Disable data sharing for personalization

By default, Edge for iOS and Android prompts users for usage data collection and sharing browsing history to personalize their browsing experience. Organizations can disable this data sharing by preventing this prompt from being shown to end users.

|    Key    |    Value    |
|----------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    com.microsoft.intune.mam.managedbrowser.disableShareUsageData    |     **true** disables this prompt from displaying to end users<br>**false** (default) users are prompted to share usage data    |
|     com.microsoft.intune.mam.managedbrowser.disableShareBrowsingHistory    |     **true** disables this prompt from displaying to end users<br>**false** (default) users are prompted to share browsing history     |

#### Disable specific features

Edge for iOS and Android allows organizations to disable certain features that are enabled by default. To disable these features, configure the following setting:

|    Key    |    Value    |
|-----------------------|-----------------------|
|    com.microsoft.intune.mam.managedbrowser.disabledFeatures    |    **password** disables prompts that offer to save passwords for the end user<br>**inprivate** disables InPrivate browsing<p>To disable multiple features, separate values with `|`. For example, `inprivate|password` disables both InPrivate and password storage.     |

#### Disable extensions

You can disable the extension framework within Edge for iOS and Android to prevent users from installing any app extensions. To do this, configure the following setting:

|    Key    |    Value    |
|-----------|-------------|
|    com.microsoft.intune.mam.managedbrowser.disableExtensionFramework    |    **true** disables the extension framework<br>**false** (default) enables the extension framework    |

### Kiosk mode experiences on Android devices

Edge for Android can be enabled as a kiosk app with the following settings:

|    Key    |    Value    |
|-----------|-------------|
|    com.microsoft.intune.mam.managedbrowser.enableKioskMode    |    **true** enables kiosk mode for Edge for Android<br>**false** (default) disables kiosk mode    |
|    com.microsoft.intune.mam.managedbrowser.showAddressBarInKioskMode    |    **true** shows the address bar in kiosk mode<br> **false** (default) hides the address bar in kiosk mode    |
|    com.microsoft.intune.mam.managedbrowser.showBottomBarInKioskMode    |    **true** shows the bottom action bar in kiosk mode<br> **false** (default) hides the bottom bar in kiosk mode    |

## Data protection app configuration scenarios

Edge for iOS and Android supports app configuration policies for the following data protection settings when the app is managed by Microsoft Endpoint Manager with an Intune App Protection Policy applied:

- Manage restricted web sites
- Manage NTLM single sign-on sites
- Manage proxy configuration
- Manage account synchronization

These settings can be deployed to the app regardless of device enrollment status.

### Manage restricted web sites

Organizations can define which sites users can access within the work or school account context in Edge for iOS and Android. If you use an allow list, your users are only able to access the sites explicitly listed. If you use a blocked list, users can access all sites except for those explicitly blocked. You should only impose either an allowed or a blocked list, not both. If you impose both, only the allowed list is honored.

Organization also define what happens when a user attempts to navigate to a restricted web site. By default, transitions are allowed. If the organization allows it, restricted web sites can be opened in the personal account context, the AAD account’s InPrivate context, or whether the site is blocked entirely. For more information on the various scenarios that are supported, see TODO. By allowing transitioning experiences, the organization's users stay protected, while keeping corporate resources safe.

> [!NOTE]
> Edge for iOS and Android can block access to sites only when they are accessed directly. It doesn't block access when users use intermediate services (such as a translation service) to access the site.

Use the following key/value pairs to configure either an allowed or blocked site list for Edge for iOS and Android. 

|Key  |Value  |
|---------|---------|
|com.microsoft.intune.mam.managedbrowser.AllowListURLs     |The corresponding value for the key is a list of URLs. You enter all the URLs you want to allow as a single value, separated by a pipe `|` character.<p>**Examples:**<br>`URL1|URL2|URL3`<br>`http://.contoso.com/|https://.bing.com/|https://expenses.contoso.com`         |
|com.microsoft.intune.mam.managedbrowser.BlockListURLs     |The corresponding value for the key is a list of URLs. You enter all the URLs you want to block as a single value, separated by a pipe `|` character.<br>**Examples:**<br>`URL1|URL2|URL3`<br>`http://.contoso.com/|https://.bing.com/|https://expenses.contoso.com`         |
|com.microsoft.intune.mam.managedbrowser.AllowTransitionOnBlock     |**true** (default) allows Edge for iOS and Android to transition restricted sites. When personal accounts are not disabled, users are prompted to either switch to the personal context to open the restricted site, or to add a personal account. If com.microsoft.intune.mam.managedbrowser.openInPrivateIfBlocked is set to true, users have the capability of opening the restricted site in the InPrivate context.<p>**false** prevents Edge for iOS and Android from transitioning users. Users are simply shown a message stating that the site they are trying to access is blocked.         |
|com.microsoft.intune.mam.managedbrowser.openInPrivateIfBlocked     |**true** allows restricted sites to be opened in the AAD account's InPrivate context. If the AAD account is the only account configured in Edge for iOS and Android, the restricted site is opened automatically in the InPrivate context. If the user has a personal account configured, the user is prompted to choose between opening InPrivate or switch to the personal account.<p> **false** (default) requires the restricted site to be opened in the user's personal acccount. If personal accounts are disabled, then the site is blocked.<p>In order for this setting to take effect, com.microsoft.intune.mam.managedbrowser.AllowTransitionOnBlock must be set to true.          |
|com.microsoft.intune.mam.managedbrowser.durationOfOpenInPrivateSnackBar     | Enter the number of seconds that users will see the snack bar notification "Link opened with InPrivate mode. Your organization requires the use of InPrivate mode for this content." By default, the snack bar notification is shown for 7 seconds.

The following sites are always allowed regardless of the defined allow list or block list settings:
- `https://*.microsoft.com/*`
- `http://*.microsoft.com/*`
- `https://microsoft.com/*`
- `http://microsoft.com/*`
- `https://*.windowsazure.com/*`
- `https://*.microsoftonline.com/*`
- `https://*.microsoftonline-p.com/*`

#### URL formats for allowed and blocked site list 

You can use various URL formats to build your allowed/blocked sites lists. These permitted patterns are detailed in the following table.

- Ensure that you prefix all URLs with **http://** or **https://** when entering them into the list.
- You can use the wildcard symbol (\*) according to the rules in the following permitted patterns list.
- A wildcard can only match an entire component of the hostname (separated by periods) or entire parts of the path (separated by forward slashes). For example, `http://*contoso.com` is **not** supported.
- You can specify port numbers in the address. If you do not specify a port number, the values used are:
  - Port 80 for http
  - Port 443 for https
- Using wildcards for the port number is **not** supported. For example, `http://www.contoso.com:*` and `http://www.contoso.com:*/` are not supported. 

    |    URL    |    Details    |    Matches    |    Does not match    |
    |-------------------------------------------|--------------------------------------------------------|-------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------|
    |    `http://www.contoso.com`    |    Matches a single page    |    `www.contoso.com`    |    `host.contoso.com`<br>`www.contoso.com/images`<br>`contoso.com/`    |
    |    `http://contoso.com`    |    Matches a single page    |    `contoso.com/`    |    `host.contoso.com`<br>`www.contoso.com/images`<br>`www.contoso.com`    |
    |    `http://www.contoso.com/*;`   |    Matches all URLs that begin with `www.contoso.com`    |    `www.contoso.com`<br>`www.contoso.com/images`<br>`www.contoso.com/videos/tvshows`    |    `host.contoso.com`<br>`host.contoso.com/images`    |
    |    `http://*.contoso.com/*`    |    Matches all subdomains under `contoso.com`    |    `developer.contoso.com/resources`<br>`news.contoso.com/images`<br>`news.contoso.com/videos`    |    `contoso.host.com`
    |    `http://*contoso.com/*`    |    Matches all subdomains ending with `contoso.com/`    |    `http://news-contoso.com`<br>`http://news-contoso.com.com/daily`    |    `http://news-contoso.host.com`    |
    `http://www.contoso.com/images`    |    Matches a single folder    |    `www.contoso.com/images`    |    `www.contoso.com/images/dogs`    |
    |    `http://www.contoso.com:80`    |    Matches a single page, by using a port   number    |    `http://www.contoso.com:80`    |         |
    |    `https://www.contoso.com`    |    Matches a single, secure page    |    `https://www.contoso.com`    |    `http://www.contoso.com`    |
    |    `http://www.contoso.com/images/*`    |    Matches a single folder and all subfolders    |    `www.contoso.com/images/dogs`<br>`www.contoso.com/images/cats`    |    `www.contoso.com/videos`    |
  
- The following are examples of some of the inputs that you can't specify:
  - `*.com`
  - `*.contoso/*`
  - `www.contoso.com/*images`
  - `www.contoso.com/*images*pigs`
  - `www.contoso.com/page*`
  - IP addresses
  - `https://*`
  - `http://*`
  - `https://*contoso.com`
  - `http://www.contoso.com:*`
  - `http://www.contoso.com: /*`

### Manage NTLM single sign-on sites

Organizations may require users to authenticate with NTLM to access intranet web sites. By default, users are prompted to enter credentials each time they access a web site that requires NTLM authentication as NTLM credential caching is disabled. 

Organizations can enable NTLM credential caching for particular web sites. For these sites, after the user enters credentials and successfully authenticates, the credentials are cached by default for 30 days.


|Key  |Value  |
|---------|---------|
|com.microsoft.intune.mam.managedbrowser.NTLMSSOURLs     |The corresponding value for the key is a list of URLs. You enter all the URLs you want to allow as a single value, separated by a pipe `|` character.<p>**Examples:**<br>`URL1|URL2`<br>`http://app.contoso.com/|https://expenses.contoso.com`<p>For more information on the types of URL formats that are supported, see [URL formats for allowed and blocked site list](#url-formats-for-allowed-and-blocked-site-list).         |
|com.microsoft.intune.mam.managedbrowser.durationOfNTLMSSO     |Number of hours to cache credentials, default is 720 hours         |

### Manage proxy configuration

You can use Edge for iOS and Android and [Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-get-started) together to give users access to intranet sites on their mobile devices. For example: 

- A user is using the Outlook mobile app, which is protected by Intune. They then click a link to an intranet site in an email, and Edge for iOS and Android recognizes that this intranet site has been exposed to the user through Application Proxy. The user is automatically routed through Application Proxy, to authenticate with any applicable multi-factor authentication and Conditional Access, before reaching the intranet site. The user is now able to access internal sites, even on their mobile devices, and the link in Outlook works as expected.
- A user opens Edge for iOS and Android on their iOS or Android device. If Edge for iOS and Android is protected with Intune, and Application Proxy is enabled, the user can go to an intranet site by using the internal URL they are used to. Edge for iOS and Android recognizes that this intranet site has been exposed to the user through Application Proxy. The user is automatically routed through Application Proxy, to authenticate before reaching the intranet site. 

Before you start:

- Set up your internal applications through Azure AD Application Proxy.
  - To configure Application Proxy and publish applications, see the [setup documentation](https://docs.microsoft.com/azure/active-directory/manage-apps/application-proxy).
- The Edge for iOS and Android app must have an [Intune app protection policy](app-protection-policy.md) assigned.
- Microsoft apps must have an app protection policy that has **Restrict web content transfer with other apps** data transfer setting set to **Microsoft Edge**.

> [!NOTE]
> Updated Application Proxy redirection data can take up to 24 hours to take effect in Edge for iOS and Android.

Target Edge for iOS with the following key/value pair, to enable Application Proxy:

|    Key    |    Value    |
|-------------------------------------------------------------------|-------------|
|    com.microsoft.intune.mam.managedbrowser.AppProxyRedirection    |    **true** enables Azure AD App Proxy redirection scenarios<br>**false** (default) prevents Azure AD App Proxy scenarios    |

> [!NOTE]
> Edge for Android does not consume this key. Instead, Edge for Android consumes Azure AD Application Proxy configuration automatically as long as the signed in AAD account has an App Protection Policy applied.

For more information about how to use Edge for iOS and Android and Azure AD Application Proxy in tandem for seamless (and protected) access to on-premises web apps, see [Better together: Intune and Azure Active Directory team up to improve user access](https://techcommunity.microsoft.com/t5/enterprise-mobility-security/better-together-intune-and-azure-active-directory-team-up-to/ba-p/250254). This blog post references the Intune Managed Browser, but the content applies to Edge for iOS and Android as well.

### Manage account synchronization

By default, Microsoft Edge sync enables users to access their browsing data across all their signed-in devices. The data supported by sync includes:

- Favorites
- Passwords
- Addresses and more (form-fill)
- Settings

Sync functionality is enabled via user consent and users can turn sync on or off for each of the data types listed above. For more information see [Microsoft Edge Sync](https://docs.microsoft.com/DeployEdge/microsoft-edge-enterprise-sync).

Organizations have the capability to disable Edge sync on iOS and Android. 

|Key  |Value  |
|---------|---------|
|com.microsoft.intune.mam.managedbrowser.account.syncDisabled     |**true** (default) allows Edge sync<br>**false** disables Edge sync          |

## Deploy app configuration scenarios with Microsoft Endpoint Manager

If you are using Microsoft Endpoint Manager as your mobile app management provider, the following steps allow you to create a managed apps app configuration policy. After the configuration is created, you can assign its settings to groups of users.

1. Sign into [Microsoft Endpoint Manager](https://endpoint.microsoft.com).

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

11. On the **Assignments** section, choose **Select groups to include**. Select the Azure AD group to which you want to assign the app configuration policy, and then choose **Select**.

12. When you are finished with the assignments, choose **Next**.

13. On the **Create app configuration policy Review + Create** blade, review the settings configured and choose **Create**.

The newly created configuration policy is displayed on the **App configuration** blade.

## Use Edge for iOS and Android to access managed app logs

Users with Edge for iOS and Android installed on their iOS or Android device can view the management status of all Microsoft published apps. They can send logs for troubleshooting their managed iOS or Android apps by using the following steps:

1. Open Edge for iOS and Android on your device.
2. Type `about:intunehelp` in the address box.
3. Edge for iOS and Android launches troubleshooting mode.

For a list of the settings stored in the app logs, see [Review app protection logs in the Managed Browser](app-protection-policy-settings-log.md).

To see how to view logs on Android devices, see [Send logs to your IT admin by email](https://docs.microsoft.com/mem/intune/user-help/send-logs-to-your-it-admin-by-email-android).

## Next steps

- [What are app protection policies?](app-protection-policy.md) 
