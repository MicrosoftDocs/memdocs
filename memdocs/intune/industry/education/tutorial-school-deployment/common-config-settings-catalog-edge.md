---
title: Common Education Microsoft Edge configuration
description: Learn about common Microsoft Edge configuration used by Education organizations in Intune.
ms.date: 5/2/2024
ms.topic: tutorial
author: yegor-a
ms.author: egorabr
ms.manager: dougeby
no-loc: [Microsoft, Windows, Autopatch, Autopilot]
---

# Microsoft Edge

Microsoft Intune and Intune for Education can configure Microsoft Edge settings. This article summarizes the configurations that are most commonly used for student and teacher devices that provide a clean and seamless experience for staff and students.

Microsoft Edge supports mandatory and recommended policies. Mandatory policies override user preferences and prevent the user from modifying the policy. Recommended policies provide a default setting that the user can override. Most policies are only mandatory but there's a subset that is mandatory and recommended. If both versions of a policy are set, the mandatory setting takes precedence. A recommended policy can be overwritten by the user.

> [!NOTE]
> Microsoft Intune settings catalog categories:
>
>- Mandatory policies category: **Microsoft Edge**
>- Recommended policies category: **Microsoft Edge – Default Settings (users can override)**

To learn more, see:

- [Use the settings catalog to configure settings on Windows, iOS/iPadOS, and macOS devices](/mem/intune/configuration/settings-catalog)
- [Microsoft Edge - Policies](/deployedge/microsoft-edge-policies)
- [Configure Microsoft Edge policy settings on Windows devices](/deployedge/configure-microsoft-edge)

> [!TIP]
> When creating a settings catalog profile in the Microsoft Intune admin center, you can copy a policy name from this article and paste it into the settings picker search field to find the desired policy.

## Settings catalog policies

| **Name** | **Value** | **Notes** | **CSP** |
|---|---|---|---|
| **:::no-loc text="Ads setting for sites with intrusive ads":::** | Disabled | Block ads on sites with intrusive ads. | [AdsSettingForIntrusiveAdsSites](/deployedge/microsoft-edge-policies#adssettingforintrusiveadssites) |
| **:::no-loc text="Default sensors setting":::** | Disabled | Don't allow any site to access sensors. | [DefaultSensorsSetting](/deployedge/microsoft-edge-policies#defaultsensorssetting) |
| **:::no-loc text="Allow import of data from other browsers on each Microsoft Edge launch":::** | Disabled | Users are not prompted to import their browsing data from other browsers on each Microsoft Edge launch. | [ImportOnEachLaunch](/deployedge/microsoft-edge-policies#importoneachlaunch) |
| **:::no-loc text="Allow importing of browser settings":::** | Disabled | Browser settings aren't imported at first run, and users can't import them manually. | [ImportBrowserSettings](/deployedge/microsoft-edge-policies#importbrowsersettings) |
| **:::no-loc text="Allow importing of favorites":::** | Disabled | Favorites aren't imported at first run, and users can't import them manually. | [ImportFavorites](/deployedge/microsoft-edge-policies#importfavorites) |
| **:::no-loc text="Allow recommendations and promotional notifications from Edge":::** | Disabled | This setting controls the *in-browser assistance notifications*. Assistance notifications are intended to help users get the most out of Microsoft Edge by recommending features and use browser features. | [ShowRecommendationsEnabled](/deployedge/microsoft-edge-policies#showrecommendationsenabled) |
| **:::no-loc text="Allow suggestions from local providers":::** | Disabled | Suggestions from local providers are never used. Local history and favorites suggestions don't appear. | [LocalProvidersEnabled](/deployedge/microsoft-edge-policies#localprovidersenabled) |
| **:::no-loc text="Allow surf game":::** | Disabled | The surf game shown when the device is offline or if the user navigates to edge://surf is disabled. | [AllowSurfGame](/deployedge/microsoft-edge-policies#allowsurfgame) |
| **:::no-loc text="Allow user feedback":::** | Disabled | Microsoft Edge uses the Edge Feedback feature (enabled by default) to allow users to send feedback, suggestions, or customer surveys and to report any issues with the browser. | [UserFeedbackAllowed](/deployedge/microsoft-edge-policies#userfeedbackallowed) |
| **:::no-loc text="Allow users to access the games menu":::** | Disabled | Users can't access the games menu. | [AllowGamesMenu](/deployedge/microsoft-edge-policies#allowgamesmenu) |
| **:::no-loc text="Allow users to proceed from the HTTPS warning page":::** | Disabled | Users are blocked from clicking through any warning page. | [SSLErrorOverrideAllowed](/deployedge/microsoft-edge-policies#sslerroroverrideallowed) |
| **:::no-loc text="Allow websites to query for available payment methods":::** | Disabled | Websites that use Payment Request are informed that no payment methods are available. | [PaymentMethodQueryEnabled](/deployedge/microsoft-edge-policies#paymentmethodqueryenabled) |
| **:::no-loc text="Block access to a list of URLs":::** | Enabled | Only enables the setting configuration. | [URLBlocklist](/deployedge/microsoft-edge-policies#urlblocklist) |
| **:::no-loc text="Block access to a list of URLs\Block access to a list of URLs (Device)":::** | edge://flags | Define a list of sites, based on URL patterns, that are blocked (your users can't load them). | [URLBlocklist](/deployedge/microsoft-edge-policies#urlblocklist) |
| **:::no-loc text="Block all ads on Bing search results":::** | Enabled | A user can search on bing.com and have an ad-free search experience. The SafeSearch setting is set to 'Strict' and can't be changed by the user. | [BingAdsSuppression](/deployedge/microsoft-edge-policies#bingadssuppression) |
| **:::no-loc text="Block tracking of users' web-browsing activity":::** | Enabled | Only enables the setting configuration. | [TrackingPrevention](/deployedge/microsoft-edge-policies#trackingprevention) |
| **:::no-loc text="Block tracking of users' web-browsing activity\Block tracking of users' web-browsing activity (Device)":::** | Balanced (blocks harmful trackers and trackers from sites user hasn't visited; content and ads are less personalized) | Optional:<br>Strict (blocks harmful trackers and most trackers from all sites; content and ads have minimal personalization. Some parts of sites might not work) | [TrackingPrevention](/deployedge/microsoft-edge-policies#trackingprevention) |
| **:::no-loc text="Browser sign-in settings":::** | Enabled | Only enables the setting configuration. | [BrowserSignin](/deployedge/microsoft-edge-policies#browsersignin) |
| **:::no-loc text="Browser sign-in settings\Browser sign-in settings (Device)":::** | Force users to sign-in to use the browser | This policy requires user cloud identity. | [BrowserSignin](/deployedge/microsoft-edge-policies#browsersignin) |
| **:::no-loc text="Clear browsing data when Microsoft Edge closes":::** | Disabled | Users can configure the Clear browsing data option in Settings. | [ClearBrowsingDataOnExit](/deployedge/microsoft-edge-policies#clearbrowsingdataonexit) |
| **:::no-loc text="Configure Do Not Track":::** | Enable | Do Not Track requests let the websites you visit know that you don't want your browsing activity to be tracked. | [ConfigureDoNotTrack](/deployedge/microsoft-edge-policies#configuredonottrack) |
| **:::no-loc text="Configure InPrivate mode availability":::** | Enabled | Only enables the setting configuration. | [InPrivateModeAvailability](/deployedge/microsoft-edge-policies#inprivatemodeavailability) |
| **:::no-loc text="Configure InPrivate mode availability\Configure InPrivate mode availability (Device)":::** | InPrivate mode disabled | | [InPrivateModeAvailability](/deployedge/microsoft-edge-policies#inprivatemodeavailability) |
| **:::no-loc text="Configure Microsoft Defender SmartScreen to block potentially unwanted apps":::** | Enabled | Potentially unwanted app blocking with Microsoft Defender SmartScreen provides warning messages to help protect users from adware, coin miners, bundleware, and other low-reputation apps. | [SmartScreenPuaEnabled](/deployedge/microsoft-edge-policies#smartscreenpuaenabled) |
| **:::no-loc text="Configure users ability to override feature flags":::** | Disabled | Users can't override state of feature flags using command line arguments or edge://flags page. | [FeatureFlagOverridesControl](/deployedge/microsoft-edge-policies#featureflagoverridescontrol) |
| **:::no-loc text="Configure whether a user always has a default profile automatically signed in with their work or school account":::** | Enabled | A non-removable profile is created with the user's work or school account on Windows. This profile can't be signed out or removed. | [NonRemovableProfileEnabled](/deployedge/microsoft-edge-policies#nonremovableprofileenabled) |
| **:::no-loc text="Continue running background apps after Microsoft Edge closes":::** | Disabled | Background mode disable to prevent conflicts with assessment software. | [BackgroundModeEnabled](/deployedge/microsoft-edge-policies#backgroundmodeenabled) |
| **:::no-loc text="Control where developer tools can be used":::** | Enabled | Only enables the setting configuration. | [DeveloperToolsAvailability](/deployedge/microsoft-edge-policies#developertoolsavailability) |
| **:::no-loc text="Control where developer tools can be used (Device)":::** | Don't allow using the developer tools | | [DeveloperToolsAvailability](/deployedge/microsoft-edge-policies#developertoolsavailability) |
| **:::no-loc text="Enable AutoFill for addresses":::** | Disabled | AutoFill never suggests or fills in address information, nor does it save additional address information that the user might submit while browsing the web. | [AutofillAddressEnabled](/deployedge/microsoft-edge-policies#autofilladdressenabled) |
| **:::no-loc text="Enable AutoFill for credit cards":::** | Disabled | AutoFill never suggests, fills, or recommends new payment Instruments. Additionally, payment instrument information isn't saved. | [AutofillCreditCardEnabled](/deployedge/microsoft-edge-policies#autofillcreditcardenabled) |
| **:::no-loc text="Enable Drop feature in Microsoft Edge":::** | Disabled | Drop lets users send messages or files to themselves. | [EdgeEDropEnabled](/deployedge/microsoft-edge-policies#edgeedropenabled) |
| **:::no-loc text="Enable full-tab promotional content":::** | Disabled | This setting controls the presentation of welcome pages that help users sign into Microsoft Edge, choose their default browser, or learn about product features. | [PromotionalTabsEnabled](/deployedge/microsoft-edge-policies#promotionaltabsenabled) |
| **:::no-loc text="Enable Microsoft Search in Bing suggestions in the address bar":::** | Enabled | Enables the display of relevant Microsoft Search in Bing suggestions in the address bar's suggestion list when the user types a search string in the address bar. | [AddressBarMicrosoftSearchInBingProviderEnabled](/deployedge/microsoft-edge-policies#addressbarmicrosoftsearchinbingproviderenabled) |
| **:::no-loc text="Enable profile creation from the Identity flyout menu or the Settings page":::** | Disabled | Users can't add new profiles from the Identity flyout menu or the Settings page. | [BrowserAddProfileEnabled](/deployedge/microsoft-edge-policies#browseraddprofileenabled) |
| **:::no-loc text="Enable search suggestions":::** | Enabled | Enables web search suggestions in Microsoft Edge's Address Bar and Auto-Suggest List. | [SearchSuggestEnabled](/deployedge/microsoft-edge-policies#searchsuggestenabled) |
| **:::no-loc text="Enforce Bing SafeSearch":::** | Enabled | Only enables the setting configuration. | [ForceBingSafeSearch](/deployedge/microsoft-edge-policies#forcebingsafesearch) |
| **:::no-loc text="Enforce Bing SafeSearch (Device)":::** | Configure strict search restrictions in Bing | | [ForceBingSafeSearch](/deployedge/microsoft-edge-policies#forcebingsafesearch) |
| **:::no-loc text="Enforce Google SafeSearch":::** | Enabled | Forces queries in Google Web Search to be performed with SafeSearch set to active, and prevents users from changing this setting. | [ForceGoogleSafeSearch](/deployedge/microsoft-edge-policies#forcegooglesafesearch) |
| **:::no-loc text="Force minimum YouTube Restricted Mode":::** | Enabled | Only enables the setting configuration. | [ForceYouTubeRestrict](/deployedge/microsoft-edge-policies#forceyoutuberestrict) |
| **:::no-loc text="Force minimum YouTube Restricted Mode (Device)":::** | Enforce Strict Restricted Mode for YouTube | | [ForceYouTubeRestrict](/deployedge/microsoft-edge-policies#forceyoutuberestrict) |
| **:::no-loc text="Force synchronization of browser data and do not show the sync consent prompt":::** | Enabled | Forces data synchronization in Microsoft Edge. This policy also prevents the user from turning sync off. | [ForceSync](/deployedge/microsoft-edge-policies#forcesync) |
| **:::no-loc text="Hide the First-run experience and splash screen":::** | Enabled | The First-run experience and the splash screen isn't shown to users when they run Microsoft Edge for the first time. | [HideFirstRunExperience](/deployedge/microsoft-edge-policies#hidefirstrunexperience) |
| **:::no-loc text="In-app support Enabled":::** | Disabled | Microsoft Edge uses the in-app support feature (enabled by default) to allow users to contact our support agents directly from the browser. | [InAppSupportEnabled](/deployedge/microsoft-edge-policies#inappsupportenabled) |
| **:::no-loc text="Microsoft Edge Insider Promotion Enabled":::** | Disabled | The Microsoft Edge Insider promotion content isn;t shown on the About Microsoft Edge page. | [MicrosoftEdgeInsiderPromotionEnabled](/deployedge/microsoft-edge-policies#microsoftedgeinsiderpromotionenabled) |
| **:::no-loc text="Save and fill memberships":::** | Disabled | Users can't have their membership info automatically saved and used to fill form fields while using Microsoft Edge. | [AutofillMembershipsEnabled](/deployedge/microsoft-edge-policies#autofillmembershipsenabled) |
| **:::no-loc text="Send all intranet sites to Internet Explorer":::** | Disabled | | [SendIntranetToInternetExplorer](/deployedge/microsoft-edge-policies#sendintranettointernetexplorer) |
| **:::no-loc text="Shopping in Microsoft Edge Enabled":::** | Disabled | The automatic shopping features such as price comparison, coupons, rebates, and express checkout is disabled for retail domains. | [EdgeShoppingAssistantEnabled](/deployedge/microsoft-edge-policies#edgeshoppingassistantenabled) |
| **:::no-loc text="Show Hubs Sidebar":::** | Disabled | The Sidebar is never shown. | [HubsSidebarEnabled](/deployedge/microsoft-edge-policies#hubssidebarenabled) |
| **:::no-loc text="Show Microsoft Rewards experiences":::** | Disabled | | [ShowMicrosoftRewards](/deployedge/microsoft-edge-policies#showmicrosoftrewards) |
| **:::no-loc text="Update policy override default":::** | Enabled | Only enables the setting configuration. | [UpdateDefault](/deployedge/microsoft-edge-update-policies#updatedefault) |
| **:::no-loc text="Update policy override default\Policy (Device)":::** | Always allow updates (recommended) | | [UpdateDefault](/deployedge/microsoft-edge-update-policies#updatedefault) |
| **:::no-loc text="Configure cookies":::** | Enabled | Only enables the setting configuration. | [DefaultCookiesSetting](/deployedge/microsoft-edge-policies#defaultcookiessetting) |
| **:::no-loc text="Configure cookies (Device)":::** | Let all sites create cookies | | [DefaultCookiesSetting](/deployedge/microsoft-edge-policies#defaultcookiessetting) |
| **:::no-loc text="Default pop-up window setting":::** | Enabled | Only enables the setting configuration. | [DefaultPopupsSetting](/deployedge/microsoft-edge-policies#defaultpopupssetting) |
| **:::no-loc text="Default pop-up window setting (Device)":::** | Allow all sites to show pop-ups | | [DefaultPopupsSetting](/deployedge/microsoft-edge-policies#defaultpopupssetting) |
| **:::no-loc text="Blocks external extensions from being installed":::** | Disabled | External extensions are allowed to be installed. | [BlockExternalExtensions](/deployedge/microsoft-edge-policies#blockexternalextensions) |
| **:::no-loc text="Control which extensions cannot be installed":::** | Disabled | The user can install any extension in Microsoft Edge. | [ExtensionInstallBlocklist](/deployedge/microsoft-edge-policies#extensioninstallblocklist) |
| **:::no-loc text="Enable implicit sign-in":::** | Enabled | Edge attempts to sign the user into their profile based on what and how they sign in to their OS. | [ImplicitSignInEnabled](/deployedge/microsoft-edge-policies#implicitsigninenabled) |
| **:::no-loc text="Enable printing":::** | Enabled | | [PrintingEnabled](/deployedge/microsoft-edge-policies#printingenabled) |
| **:::no-loc text="Prevent bypassing Microsoft Defender SmartScreen prompts for sites":::** | Enabled | Users can't ignore Microsoft Defender SmartScreen warnings and they're blocked from continuing to the site. | [PreventSmartScreenPromptOverride](/deployedge/microsoft-edge-policies#preventsmartscreenpromptoverride) |
| **:::no-loc text="Allow Microsoft News content on the new tab page":::** | Disabled | Microsoft Edge does not display Microsoft News content on the new tab page, the Content control in the NTP settings flyout is disabled and set to 'Content off'. | [NewTabPageContentEnabled](/deployedge/microsoft-edge-policies#newtabpagecontentenabled) |
| **:::no-loc text="Hide the default top sites from the new tab page":::** | Enabled | The default top site tiles are hidden. | [NewTabPageHideDefaultTopSites](/deployedge/microsoft-edge-policies#newtabpagehidedefaulttopsites) |

## (Optional) Startup, home page and new tab page

| **Name** | **Value** | **Notes** | **CSP** |
|---|---|---|---|
| **:::no-loc text="Action to take on startup":::** | _custom_ | Specify how Microsoft Edge behaves when it starts. | [RestoreOnStartup](/deployedge/microsoft-edge-policies#restoreonstartup) |
| **:::no-loc text="Configure the home page URL":::** | Enabled | Configures the default home page URL in Microsoft Edge. The home page is the page opened by the Home button. | [HomepageLocation](/deployedge/microsoft-edge-policies#homepagelocation) |
| **:::no-loc text="Home page URL (Device)":::** | _custom_ _url_ | | [HomepageLocation](/deployedge/microsoft-edge-policies#homepagelocation) |
| **:::no-loc text="Configure the new tab page URL":::** | Disabled | This policy determines the page that's opened when new tabs are created (including when new windows are opened). It also affects the startup page if that's set to open to the new tab page. | [NewTabPageLocation](/deployedge/microsoft-edge-policies#newtabpagelocation) |
| **:::no-loc text="New tab page URL (Device)":::** | _custom_ _url_ | | [NewTabPageLocation](/deployedge/microsoft-edge-policies#newtabpagelocation) |

## (Optional) Content settings in Microsoft 365 admin center

If you leave the default configuration, when users open a new tab page they'll see a combination of the Microsoft 365 feed and news. You can control the visibility of news from the Microsoft 365 admin center.

1. In the Microsoft 365 admin center (<https://admin.microsoft.com>), go to **Settings** > **Org settings** > **Services** > [News](https://admin.microsoft.com/adminportal/home?).
2. In the **News** panel, click **Microsoft Edge new tab page**.
3. Untick **Show company information and industry news on the new tab page**.
