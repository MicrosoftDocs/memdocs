---
author: Yusuke Shinoki (HE/HIM)
ms.date: 04/10/2024
---
### Microsoft Edge

A list of Microsoft Edge policies commonly used in education to provide a clean and seamless experience for staff and students.

Microsoft Edge supports mandatory and recommended policies. Mandatory policies override user preferences and prevent the user from the policy. Recommended policies provide a default setting that the user can override. Most policies are only mandatory but there's a subset that is mandatory and recommended. If both versions of a policy are set, the mandatory setting takes precedence. A recommended policy only takes effect when the user hasn't modified the setting.

Microsoft Intune Settings Catalog categories:

- Mandatory policies category: Microsoft Edge
- Recommended policies category: Microsoft Edge – Default Settings (users can override)

Additional information:

- [Microsoft Edge - Policies](https://learn.microsoft.com/deployedge/microsoft-edge-policies)
- [Configure Microsoft Edge policy settings on Windows devices](https://learn.microsoft.com/en-us/deployedge/configure-microsoft-edge)

  | **Settings Catalog** | **Value** | **Notes** | **CSP** |
  |---|---|---|---|
  | **Ads setting for sites with intrusive ads** | Disabled | Block ads on sites with intrusive ads. | [AdsSettingForIntrusiveAdsSites](https://learn.microsoft.com/deployedge/microsoft-edge-policies) |
  | **Default sensors setting** | Disabled | Do not allow any site to access sensors. | [DefaultSensorsSetting](https://learn.microsoft.com/deployedge/microsoft-edge-policies) |
  | **Allow import of data from other browsers on each Microsoft Edge launch** | Disabled | Users will never see a prompt to import their browsing data from other browsers on each Microsoft Edge launch. | [ImportOnEachLaunch](https://learn.microsoft.com/deployedge/microsoft-edge-policies) |
  | **Allow importing of browser settings** | Disabled | Browser settings aren't imported at first run, and users can't import them manually. | [ImportBrowserSettings](https://learn.microsoft.com/deployedge/microsoft-edge-policies) |
  | **Allow importing of favorites** | Disabled | Favorites aren't imported at first run, and users can't import them manually. | [ImportFavorites](https://learn.microsoft.com/deployedge/microsoft-edge-policies) |
  | **Allow recommendations and promotional notifications from Edge** | Disabled | This setting controls the in-browser assistance notifications which are intended to help users get the most out of Microsoft Edge. This is done by recommending features and by helping them use browser features. | [ShowRecommendationsEnabled](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-policies) |
  | **Allow suggestions from local providers** | Disabled | Suggestions from local providers are never used. Local history and local favorites suggestions will not appear. | [LocalProvidersEnabled](https://learn.microsoft.com/deployedge/microsoft-edge-policies) |
  | **Allow surf game** | Disabled | Users won't be able to play the surf game when the device is offline or if the user navigates to edge://surf. | [AllowSurfGame](https://learn.microsoft.com/deployedge/microsoft-edge-policies) |
  | **Allow user feedback** | Disabled | Microsoft Edge uses the Edge Feedback feature (enabled by default) to allow users to send feedback, suggestions or customer surveys and to report any issues with the browser. | [UserFeedbackAllowed](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-policies) |
  | **Allow users to access the games menu** | Disabled | Users won't be able to access the games menu. | [AllowGamesMenu](https://learn.microsoft.com/deployedge/microsoft-edge-policies) |
  | **Allow users to proceed from the HTTPS warning page** | Disabled | Users are blocked from clicking through any warning page. | [SSLErrorOverrideAllowed](https://learn.microsoft.com/deployedge/microsoft-edge-policies) |
  | **Allow websites to query for available payment methods** | Disabled | Websites that use Payment Request will be informed that no payment methods are available. | [PaymentMethodQueryEnabled](https://learn.microsoft.com/deployedge/microsoft-edge-policies)v |
  | **Block access to a list of URLs** | Enabled | Only enables the setting configuration. | [URLBlocklist](https://learn.microsoft.com/deployedge/microsoft-edge-policies) |
  | **Block access to a list of URLs\Block access to a list of URLs (Device)** | edge://flags | Define a list of sites, based on URL patterns, that are blocked (your users can't load them). | [URLBlocklist](https://learn.microsoft.com/deployedge/microsoft-edge-policies) |
  | **Block all ads on Bing search results** | Enabled | A user can search on bing.com and have an ad-free search experience. At the same time, the SafeSearch setting will be set to 'Strict' and can't be changed by the user. | [BingAdsSuppression](https://learn.microsoft.com/deployedge/microsoft-edge-policies) |
  | **Block tracking of users' web-browsing activity** | Enabled | Only enables the setting configuration. | [TrackingPrevention](https://learn.microsoft.com/deployedge/microsoft-edge-policies) |
  | **Block tracking of users' web-browsing activity\Block tracking of users' web-browsing activity (Device)** | Balanced (blocks harmful trackers and trackers from sites user has nt visited; content and ads will be less personalized) | Optional:<br>Strict (blocks harmful trackers and majority of trackers from all sites; content and ads will have minimal personalization. Some parts of sites might not work) | [TrackingPrevention](https://learn.microsoft.com/deployedge/microsoft-edge-policies) |
  | **Browser sign-in settings** | Enabled | Only enables the setting configuration. | [BrowserSignin](https://learn.microsoft.com/deployedge/microsoft-edge-policies) |
  | **Browser sign-in settings\Browser sign-in settings (Device)** | Force users to sign-in to use the browser | This policy requires user cloud identity. | [BrowserSignin](https://learn.microsoft.com/deployedge/microsoft-edge-policies) |
  | **Clear browsing data when Microsoft Edge closes** | Disabled | Users can configure the Clear browsing data option in Settings. | [ClearBrowsingDataOnExit](https://learn.microsoft.com/deployedge/microsoft-edge-policies) |
  | **Configure Do Not Track** | Enable | Do Not Track requests let the websites you visit know that you don't want your browsing activity to be tracked. | [ConfigureDoNotTrack](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-policies) |
  | **Configure InPrivate mode availability** | Enabled | Only enables the setting configuration. | [InPrivateModeAvailability](https://learn.microsoft.com/deployedge/microsoft-edge-policies) |
  | **Configure InPrivate mode availability\Configure InPrivate mode availability (Device)** | InPrivate mode disabled | | [InPrivateModeAvailability](https://learn.microsoft.com/deployedge/microsoft-edge-policies) |
  | **Configure Microsoft Defender SmartScreen to block potentially unwanted apps** | Enabled | Potentially unwanted app blocking with Microsoft Defender SmartScreen provides warning messages to help protect users from adware, coin miners, bundleware, and other low-reputation apps that are hosted by websites. | [SmartScreenPuaEnabled](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-policies) |
  | **Configure users ability to override feature flags** | Disabled | Users can't override state of feature flags using command line arguments or edge://flags page. | [FeatureFlagOverridesControl](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-policies) |
  | **Configure whether a user always has a default profile automatically signed in with their work or school account** | Enabled | A non-removable profile will be created with the user's work or school account on Windows. This profile can't be signed out or removed. | [NonRemovableProfileEnabled](https://learn.microsoft.com/deployedge/microsoft-edge-policies) |
  | **Continue running background apps after Microsoft Edge closes** | Disabled | Background mode disable to prevent conflicts with assessment software. | [BackgroundModeEnabled](https://learn.microsoft.com/deployedge/microsoft-edge-policies) |
  | **Control where developer tools can be used** | Enabled | Only enables the setting configuration. | [DeveloperToolsAvailability](https://learn.microsoft.com/deployedge/microsoft-edge-policies) |
  | **Control where developer tools can be used (Device)** | Don't allow using the developer tools | | [DeveloperToolsAvailability](https://learn.microsoft.com/deployedge/microsoft-edge-policies) |
  | **Enable AutoFill for addresses** | Disabled | AutoFill never suggests or fills in address information, nor does it save additional address information that the user might submit while browsing the web. | [AutofillAddressEnabled](https://learn.microsoft.com/deployedge/microsoft-edge-policies) |
  | **Enable AutoFill for credit cards** | Disabled | AutoFill never suggests, fills, or recommends new payment Instruments. Additionally, it won't save any payment instrument information that users submit while browsing the web. | [AutofillCreditCardEnabled](https://learn.microsoft.com/deployedge/microsoft-edge-policies) |
  | **Enable Drop feature in Microsoft Edge** | Disabled | Drop lets users send messages or files to themselves. | [EdgeEDropEnabled](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-policies) |
  | **Enable full-tab promotional content** | Disabled | This setting controls the presentation of welcome pages that help users sign into Microsoft Edge, choose their default browser, or learn about product features. | [PromotionalTabsEnabled](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-policies) |
  | **Enable Microsoft Search in Bing suggestions in the address bar** | Enabled | Enables the display of relevant Microsoft Search in Bing suggestions in the address bar's suggestion list when the user types a search string in the address bar. | [AddressBarMicrosoftSearchInBingProviderEnabled](https://learn.microsoft.com/deployedge/microsoft-edge-policies) |
  | **Enable profile creation from the Identity flyout menu or the Settings page** | Disabled | Users cannot add new profiles from the Identity flyout menu or the Settings page. | [BrowserAddProfileEnabled](https://learn.microsoft.com/deployedge/microsoft-edge-policies) |
  | **Enable search suggestions** | Enabled | Enables web search suggestions in Microsoft Edge's Address Bar and Auto-Suggest List. | [SearchSuggestEnabled](https://learn.microsoft.com/deployedge/microsoft-edge-policies) |
  | **Enforce Bing** **SafeSearch** | Enabled | Only enables the setting configuration. | [ForceBingSafeSearch](https://learn.microsoft.com/deployedge/microsoft-edge-policies) |
  | **Enforce Bing** **SafeSearch (Device)** | Configure strict search restrictions in Bing | | [ForceBingSafeSearch](https://learn.microsoft.com/deployedge/microsoft-edge-policies) |
  | **Enforce Google** **SafeSearch** | Enabled | Forces queries in Google Web Search to be performed with SafeSearch set to active, and prevents users from changing this setting. | [ForceGoogleSafeSearch](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-policies) |
  | **Force minimum YouTube Restricted Mode** | Enabled | Only enables the setting configuration. | [ForceYouTubeRestrict](https://learn.microsoft.com/deployedge/microsoft-edge-policies) |
  | **Force minimum YouTube Restricted Mode (Device)** | Enforce Strict Restricted Mode for YouTube | | [ForceYouTubeRestrict](https://learn.microsoft.com/deployedge/microsoft-edge-policies) |
  | **Force synchronization of browser data and do not show the sync consent prompt** | Enabled | Forces data synchronization in Microsoft Edge. This policy also prevents the user from turning sync off. | [ForceSync](https://learn.microsoft.com/deployedge/microsoft-edge-policies) |
  | **Hide the First-run experience and splash screen** | Enabled | The First-run experience and the splash screen will not be shown to users when they run Microsoft Edge for the first time. | [HideFirstRunExperience](https://learn.microsoft.com/deployedge/microsoft-edge-policies) |
  | **In-app support Enabled** | Disabled | Microsoft Edge uses the in-app support feature (enabled by default) to allow users to contact our support agents directly from the browser. | [InAppSupportEnabled](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-policies) |
  | **Microsoft Edge Insider Promotion Enabled** | Disabled | The Microsoft Edge Insider promotion content will not be shown on the About Microsoft Edge page. | [MicrosoftEdgeInsiderPromotionEnabled](https://learn.microsoft.com/deployedge/microsoft-edge-policies) |
  | **Save and fill memberships** | Disabled | Users can't have their membership info automatically saved and used to fill form fields while using Microsoft Edge. | [AutofillMembershipsEnabled](https://learn.microsoft.com/deployedge/microsoft-edge-policies) |
  | **Send all intranet sites to Internet Explorer** | Disabled | | [SendIntranetToInternetExplorer](https://learn.microsoft.com/deployedge/microsoft-edge-policies) |
  | **Shopping in Microsoft Edge Enabled** | Disabled | Shopping features such as price comparison, coupons, rebates and express checkout will not be automatically found for retail domains. | [EdgeShoppingAssistantEnabled](https://learn.microsoft.com/deployedge/microsoft-edge-policies) |
  | **Show Hubs Sidebar** | Disabled | The Sidebar will never be shown. | [HubsSidebarEnabled](https://learn.microsoft.com/deployedge/microsoft-edge-policies) |
  | **Show Microsoft Rewards experiences** | Disabled | | [ShowMicrosoftRewards](https://learn.microsoft.com/deployedge/microsoft-edge-policies) |
  | **Update policy override default** | Enabled | Only enables the setting configuration. | [UpdateDefault](https://learn.microsoft.com/deployedge/microsoft-edge-update-policies) |
  | **Update policy override default\Policy (Device)** | Always allow updates (recommended) | | [UpdateDefault](https://learn.microsoft.com/deployedge/microsoft-edge-update-policies) |
  | **Configure cookies** | Enabled | Only enables the setting configuration. | [DefaultCookiesSetting](https://learn.microsoft.com/deployedge/microsoft-edge-policies) |
  | **Configure cookies (Device)** | Let all sites create cookies | | [DefaultCookiesSetting](https://learn.microsoft.com/deployedge/microsoft-edge-policies) |
  | **Default pop-up window setting** | Enabled | Only enables the setting configuration. | [DefaultPopupsSetting](https://learn.microsoft.com/deployedge/microsoft-edge-policies) |
  | **Default pop-up window setting (Device)** | Allow all sites to show pop-ups | | [DefaultPopupsSetting](https://learn.microsoft.com/deployedge/microsoft-edge-policies) |
  | **Blocks external extensions from being installed** | Disabled | External extensions are allowed to be installed. | [BlockExternalExtensions](https://learn.microsoft.com/deployedge/microsoft-edge-policies) |
  | **Control which extensions cannot be installed** | Disabled | The user can install any extension in Microsoft Edge. | [ExtensionInstallBlocklist](https://learn.microsoft.com/deployedge/microsoft-edge-policies) |
  | **Enable implicit sign-in** | Enabled | Edge will attempt to sign the user into their profile based on what and how they sign in to their OS. | [ImplicitSignInEnabled](https://learn.microsoft.com/deployedge/microsoft-edge-policies) |
  | **Enable printing** | Enabled | | [PrintingEnabled](https://learn.microsoft.com/deployedge/microsoft-edge-policies) |
  | **Prevent bypassing Microsoft Defender SmartScreen prompts for sites** | Enabled | Users can't ignore Microsoft Defender SmartScreen warnings and they are blocked from continuing to the site. | [PreventSmartScreenPromptOverride](https://learn.microsoft.com/deployedge/microsoft-edge-policies) |
  | **Allow Microsoft News content on the new tab page** | Disabled | Microsoft Edge does not display Microsoft News content on the new tab page, the Content control in the NTP settings flyout is disabled and set to 'Content off'. | [NewTabPageContentEnabled](https://learn.microsoft.com/deployedge/microsoft-edge-policies) |
  | **Hide the default top sites from the new tab page** | Enabled | The default top site tiles are hidden. | [NewTabPageHideDefaultTopSites](https://learn.microsoft.com/deployedge/microsoft-edge-policies) |

#### (Optional) Startup, home page and new tab page

| **Settings Catalog** | **Value** | **Notes** | **CSP** |
|---|---|---|---|
| **Action to take on startup** | ***custom*** | Specify how Microsoft Edge behaves when it starts. | [**RestoreOnStartup**](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-policies) |
| **Configure the home page URL** | Enabled | Configures the default home page URL in Microsoft Edge.The home page is the page opened by the Home button. | [HomepageLocation](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-policies) |
| **Home page URL (Device)** | _custom_ _url_ | | [HomepageLocation](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-policies) |
| **Configure the new tab page URL** | Disabled | This policy determines the page that's opened when new tabs are created (including when new windows are opened). It also affects the startup page if that's set to open to the new tab page. | [NewTabPageLocation](https://learn.microsoft.com/deployedge/microsoft-edge-policies) |
| **New tab page URL (Device)** | _custom_ _url_ | | [NewTabPageLocation](https://learn.microsoft.com/deployedge/microsoft-edge-policies) |

#### (Optional) Content settings in Microsoft 365 admin center

If you leave the default configuration, when users open a new tab page they will see a combination of the Microsoft 365 feed and news. You can control the visibility of news from the Microsoft 365 admin center.

In the Microsoft 365 admin center (<https://admin.microsoft.com>), go to **Settings** > **Org settings** > **Services** > [News](https://admin.microsoft.com/adminportal/home?).

In the **News** panel, click **Microsoft Edge new tab page**.

Untick **Show company information and industry news on the new tab page**. 

