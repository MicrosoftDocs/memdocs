---
# required metadata
title: What's new in Microsoft Intune - Azure | Microsoft Docs
titleSuffix:
description: Find out what's new in the Intune Azure portal
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 04/20/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology:
ms.assetid: 791ed23f-bd13-4ef0-a3dd-cd2d7332c5cc

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: dougeby
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
---

# What's new in Microsoft Intune

Learn what's new each week in Microsoft Intune in [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431). You can also find [important notices](#notices), [past releases](whats-new-archive.md), and information about [how Intune service updates are released](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Microsoft-Intune-Service-Updates/ba-p/358728). 

> [!Note]
> Each [monthly update](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Microsoft-Intune-Service-Updates/ba-p/358728) may take up to three days to rollout and will be in the following order:
>
> - Day 1: Asia Pacific (APAC)
> - Day 2: Europe, Middle East, Africa (EMEA)
> - Day 3: North America
> - Day 4+: Intune for Government
>
> Some features may roll out over several weeks and might not be available to all customers in the first week.
>
> Check the [In development page](in-development.md) for a list of upcoming features in a release.

**RSS feed**: Get notified when this page is updated by copying and pasting the following URL into your feed reader: `https://docs.microsoft.com/api/search/rss?search=%22What%27s+new+in+microsoft+intune%3F+-+Azure%22&locale=en-us`

<!-- Common categories:  
### App management
### Device configuration
### Device enrollment
### Device management
### Device security
### Intune apps
### Monitor and troubleshoot

<!-- ########################## -->
## Week of April 20, 2020 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### App management

#### Microsoft Office 365 ProPlus rename<!-- 6368143 -->
Microsoft Office 365 ProPlus is being renamed to **Microsoft 365 Apps for enterprise**. To learn more, see [Name change for Office 365 ProPlus](https://docs.microsoft.com/deployoffice/name-change). In our documentation, we'll commonly refer to it as Microsoft 365 Apps. In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), you can find the apps suite by selecting **Apps** > **Windows** > **Add**. For information about adding apps, see [Add apps to Microsoft Intune](../apps/apps-add.md).

<!-- ########################## -->
## Week of April 13, 2020 (2004 Service release)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### App management

#### Manage S/MIME settings for Outlook on Android Enterprise devices<!-- 6517085   -->
You can use app configuration policies to manage the S/MIME setting for Outlook on devices that run Android Enterprise. You can also choose whether or not to allow the device users to enable or disable S/MIME in Outlook settings. To use app configuration policies for Android, in the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) go to **Apps** > **App configuration policies** > **Add** > **Managed devices**. For more information about configuring settings for Outlook, see [Microsoft Outlook configuration settings](../apps/app-configuration-policies-outlook.md).

#### Pre-release testing for Managed Google Play apps<!-- 2681933  -->
Organizations that are using [Google Play's closed test tracks for app pre-release testing](https://support.google.com/googleplay/android-developer/answer/3131213) can manage these tracks with Intune. You can selectively assign apps that are published to Google Play's pre-production tracks to pilot groups in order to perform testing. In Intune, you can see whether an app has a pre-production build test track published to it, as well as be able to assign that track to AAD user or device groups. This feature is available for all of our currently supported Android Enterprise scenarios (work profile, fully managed, and dedicated). In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), you can add a Managed Google Play app by selecting **Apps** > **Android** > **Add**. For more information, see [Working with Managed Google Play Closed Testing Tracks](../apps/apps-add-android-for-work.md#working-with-managed-google-play-closed-testing-tracks).

#### Microsoft Teams is now included in the Office 365 Suite for macOS<!-- 5903936  -->
Users who are assigned Microsoft Office for macOS in Microsoft Endpoint Manager will now receive Microsoft Teams in addition to the existing Microsoft Office apps (Word, Excel, PowerPoint, Outlook, and OneNote). Intune will recognize the existing Mac devices that have the other Office for macOS apps installed, and will attempt to install Microsoft Teams the next time the device checks in with Intune. In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), you can find the **Office 365 Suite** for macOS by selecting **Apps** > **macOS** > **Add**. For more information, see [Assign Office 365 to macOS devices with Microsoft Intune](../apps/apps-add-office365-macos.md).

#### Update to Android app configuration policies<!-- 6113334  -->
Android app configuration policies have been updated to allow admins to select the device enrollment type before creating an app config profile. The functionality is being added to account for certificate profiles that are based on enrollment type (Work profile or Device Owner).  This update provides the following:

1. If a new profile is created and Work Profile and Device Owner Profile are selected for device enrollment type, you will not be able to associate a certificate profile with the app config policy.
2. If a new profile is created and Work Profile only is selected, Work Profile certificate policies created under Device Configuration can be utilized.
3. If a new profile is created and Device Owner only is selected, Device Owner certificate policies created under Device Configuration can be utilized. 

> [!IMPORTANT]
> Existing policies created prior to the release of this feature (April 2020 release - 2004) that do not have any certificate profiles associated with the policy will default to Work Profile and Device Owner Profile for device enrollment type. Also, existing policies created prior to the release of this feature that have certificate profiles associated with them will default to Work Profile only.

Additionally, we are adding Gmail and Nine email configuration profiles that will work for both Work Profile and Device Owner enrollment types, including the use of certificate profiles on both email configuration types.  Any Gmail or Nine policies that you have created under Device Configuration for Work Profiles will continue to apply to the device and it is not necessary to move them to app configuration policies.

In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), you can find app configuration policies by selecting **Apps** > **App configuration policies**. For more information about app configuration policies, see [App configuration policies for Microsoft Intune](../apps/app-configuration-policies-overview.md).

#### Push notification when device ownership type is changed<!-- 5575875 -->
You can configure a push notification to send to both your Android and iOS Company Portal users when their device ownership type has been changed from Personal to Corporate as a privacy courtesy. This push notification is set to off by default. The setting can be found in the Microsoft Endpoint Manager by selecting **Tenant administration** > **Customization**. To learn more about how device ownership affects your end-users, see [Change device ownership](../enrollment/corporate-identifiers-add.md#change-device-ownership).

#### Group targeting support for Customization pane<!-- 4722837  -->
You can target the settings in the **Customization** pane to user groups. To find these settings in Intune, navigate to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Tenant administration** > **Customization**. For more information about customization, see [How to customize the Intune Company Portal apps, Company Portal website, and Intune app](../apps/company-portal-app.md).


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device configuration

#### Multiple "Evaluate each connection attempt" on-demand VPN rules supported on iOS, iPadOS, and macOS<!-- 6424615  -->
The Intune user experience allows multiple on-demand VPN rules in the same VPN profile with the **Evaluate each connection attempt** action (**Devices** > **Configuration profiles** > **Create profile** > **iOS/iPadOS** or **macOS** for platform > **VPN** for profile > **Automatic VPN** > **On-demand**).

It only honored the first rule in the list. This behavior is fixed, and Intune evaluates all rules in the list. Each rule is evaluated in the order it appears in the on-demand rules list.

> [!NOTE]
> If you have existing VPN profiles that use these on-demand VPN rules, the fix applies the next time you change the VPN profile. For example, make a minor change, such as change the connection the name, and then save the profile.
>
> If you're using SCEP certificates for authentication, this change causes the certificates for this VPN profile to be re-issued.

Applies to:
- iOS/iPadOS
- macOS

For more information on VPN profiles, see [Create VPN profiles](../configuration/vpn-settings-configure.md).

#### Additional options in SSO and SSO app extension profiles on iOS/iPadOS devices<!-- 6504155   -->

On iOS/iPadOS devices, you can:
- In SSO profiles (**Devices** > **Configuration profiles** > **Create profile** > **iOS/iPadOS** for platform > **Device features** for profile > **Single sign-on**), set the Kerberos principal name to be the Security Account Manager (SAM) account name in SSO profiles. 
- In SSO app extension profiles (**Devices** > **Configuration profiles** > **Create profile** > **iOS/iPadOS** for platform > **Device features** for profile > **Single sign-on app extension**), configure the iOS/iPadOS Microsoft Azure AD extension with fewer clicks by using a new SSO app extension type. You can enable the Azure AD extension for devices in shared device mode and send extension-specific data to the extension.

Applies to:
- iOS/iPadOS 13.0+

For more information on using single sign-on on iOS/iPadOS devices, see [Single sign-on app extension overview](../configuration/device-features-configure.md#single-sign-on-app-extension) and [Single sign-on settings list](../configuration/ios-device-features-settings.md#single-sign-on-app-extension).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device enrollment

#### Delete Apple Automated Device Enrollment token when default profile is present<!--6393220 -->
Previously, you couldn't delete a default profile, which meant that you couldn't delete the Automated Device Enrollment token associated with it. Now, you can delete the token when:
- no devices are assigned to the token
- a default profile is present
To do so, delete the default profile and then delete the associated token.
For more information, see [Delete an ADE token from Intune](../enrollment/device-enrollment-program-enroll-ios.md#delete-an-ade-token-from-intune).

#### Scaled up support for Apple Automated Device Enrollment and Apple Configurator 2 devices, profiles, and tokens<!--3542402 -->
To help distributed IT departments and organizations, Intune now supports up to 1000 enrollment profiles per token, 2000 Automated Device Enrollment (formerly known as DEP) tokens per Intune account, and 75,000 devices per token. There is no specific limit for devices per enrollment profile, below the maximum number of devices per token.

Intune now supports up to 1000 Apple Configurator 2 profiles.

For more information, see [Supported volume](../enrollment/device-enrollment-program-enroll-ios.md#supported-volume).

#### All devices page column entry changes<!--6967616 -->
On the **All devices** page, the entries for the **Managed by** column have changed:
- *Intune* is now displayed instead of *MDM*
- *Co-managed* is now displayed instead of *MDM/ConfigMgr Agent*

The export values are unchanged.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

#### Trusted Platform Manager (TPM) Version information now on Device Hardware page<!--6224914 idmiss -->
You can now see the TPM version number on a device's hardware page ([Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Devices** > choose a device > **Hardware** > look under **System enclosure**).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Monitor and troubleshoot

#### Collect logs to better troubleshoot scripts assigned to macOS devices<!-- 6359853  -->
You can now collect logs for improved troubleshooting of scripts assigned to macOS devices. You can collect logs up to 60 MB (compressed) or 25 files, whichever occurs first. For more information, see [Troubleshoot macOS shell script policies using log collection](../apps/macos-shell-scripts.md#troubleshoot-macos-shell-script-policies-using-log-collection).
 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Security

#### Derived credentials to provision Android Enterprise Fully Managed devices with certificates<!--4839592    -->
Intune now supports use of [derived credentials](../protect/derived-credentials.md) as an authentication method for Android devices. Derived credentials are an implementation of the National Institute of Standards and Technology (NIST) 800-157 standard for deploying certificates to devices. Our support for Android expands on our support for devices that run iOS/iPadOS.

Derived credentials rely on the use of a Personal Identity Verification (PIV) or Common Access Card (CAC) card, like a smart card. To get a derived credential for their mobile device, users start in the Microsoft Intune app and follow an enrollment workflow that is unique to the provider you use. Common to all providers is the requirement to use a smart card on a computer to authenticate to the derived credential provider. That provider then issues a certificate to the device that's derived from the user’s smart card.

You can use derived credentials as the authentication method for device configuration profiles for VPN and WiFi. You can also use them for app authentication, and S/MIME signing and encryption for applications that support it.

Intune now supports the following derived credential providers with Android:
- Entrust Datacard
- Intercede

A third provider, DISA Purebred, will be available for Android in a future release.

#### Microsoft Edge security baseline is now Generally Available<!--6586139 -->

*This new baseline is rolling out to tenants over the next several weeks. We expect all tenants will have this new baseline in early May.*

A new version of the [Microsoft Edge security baseline](../protect/security-baselines.md#available-security-baselines) is now available, and is released as generally available (GA). The previous Edge baseline was in Preview.  The new baseline version ins April 2020 (Edge version 80 and later). 

With the release of this new baseline, you'll no longer be able to create profiles based on the previous baseline versions, but you can continue to use profiles you created with those versions. You can also choose to [update your existing profiles to use the latest baseline version](../protect/security-baselines.md#change-the-baseline-version-for-a-profile). 

<!-- ########################## -->
## Week of April 6, 2020

#### New shell script settings for macOS devices<!-- 6884363 -->
When configuring shell scripts for macOS devices, you can now configure the following new settings: 
- Hide script notifications on devices
- Script frequency
- Maximum number of times to retry if script fails

For more information, see [Use shell scripts on macOS devices in Intune](../apps/macos-shell-scripts.md).

<!-- ########################## -->
## Week of March 30, 2020

### New URL for the Microsoft Endpoint Manager admin center<!-- 3704810 -->
To align with the announcement of Microsoft Endpoint Manager at Ignite last year, we have changed the URL for the Microsoft Endpoint Manager admin center (formerly Microsoft 365 Device Management) to [https://endpoint.microsoft.com](https://endpoint.microsoft.com). The old admin center URL ([https://devicemanagement.microsoft.com](https://devicemanagement.microsoft.com)) will continue to work, but we recommend you start accessing the Microsoft Endpoint Manager admin center using the new URL.

For more information, see [Simplify IT tasks using the Microsoft Endpoint Manager admin center](what-is-device-management.md#simplify-it-tasks-using-the-device-management-admin-center).  


### App management  

#### Company Portal for iOS supports landscape mode<!--6048329  -->   
Users can now enroll their devices, find apps, and get IT support using the screen orientation of their choice. The app will automatically detect and adjust screens to fit portrait or landscape mode, unless users lock the screen in portrait mode.  

#### Script support for macOS devices (Public Preview)<!-- 4280361  -->
You can add and deploy scripts to macOS devices. This support extends your ability to configure macOS devices beyond what is possible using native MDM capabilities on macOS devices. For more information, see [Use shell scripts on macOS devices in Intune](../apps/macos-shell-scripts.md).

<!-- ########################## -->
## Week of March 24, 2020

### Improved user interface experience when creating device restrictions profiles on Android and Android Enterprise devices<!-- 5841361 -->

> [!NOTE] 
> The Intune user interface is updating to a full screen experience, and may take several weeks. Until your tenant receives this update, you will have a slightly different workflow when you create or edit settings.

When you create a profile for Android or Android Enterprise devices, the experience in the Endpoint Management admin center is updated. This change impacts the following device configuration profiles (**Devices** > **Configuration Profiles** > **Create profile** > **Android device administrator** or **Android Enterprise** for platform):

- Device restrictions: Android device administrator
- Device restrictions: Android Enterprise device owner
- Device restrictions: Android Enterprise work profile

For more information on the device restrictions you can configure, see [Android device administrator](../configuration/device-restrictions-android.md) and [Android Enterprise](../configuration/device-restrictions-android-for-work.md).

### Improved user interface experience when creating configuration profiles on iOS/iPadOS and macOS devices<!-- 5569002 5568997 -->

> [!NOTE]
> The Intune user interface is updating to a full screen experience, and may take several weeks. Until your tenant receives this update, you will have a slightly different workflow when you create or edit settings.

When you create a profile for iOS or macOS devices, the experience in the Endpoint Management admin center is updated. This change impacts the following device configuration profiles (**Devices** > **Configuration Profiles** > **Create profile** > **iOS/iPadOS** or **macOS** for platform):

- Custom: iOS/iPadOS, macOS
- Device features: iOS/iPadOS, macOS
- Device restrictions: iOS/iPadOS, macOS
- Endpoint protection: macOS
- Extensions: macOS
- Preference file: macOS

### Hide from user configuration setting in device features on macOS devices<!-- 6524869 -->

> [!NOTE]
> This change will roll out to all customers over the next couple of weeks.

When you create a device features configuration profile on macOS devices, there's a new **Hide from user configuration** setting (**Devices** > **Configuration profiles** > **Create profile** > **macOS** for platform > **Device features** for profile > **Login items**).

This feature sets an app's hide checkmark in the **Users & Groups** login items apps list on macOS devices. Existing profiles show this setting within the list as unconfigured. To configure this setting, administrators can update existing profiles.

When set to **Hide**, the hide checkbox is checked for the app, and users can't change it. It also hides the app from users after users sign in to their devices.

> [!div class="mx-imgBorder"]
> ![Hide apps on macOS devices after users sign in to the device in Microsoft Intune and Endpoint Manager](./media/whats-new/macos-hide-checkmark-users-groups-login-items-apps-list.png)

For more information on the setting you can configure, see [macOS device feature settings](../configuration/macos-device-features-settings.md).

This feature applies to:

- macOS

## Week of March 16, 2020 (2003 Service release)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### App management

#### macOS and iOS Company Portal updates<!-- 5779439, 5780234  -->
The Profile pane of the macOS and iOS Company Portal has been updated to include the sign-out button. Additionally, UI improvements have been made to the Profile pane in the macOS Company Portal. For more information about the Company Portal, see [How to configure the Microsoft Intune Company Portal app](../apps/company-portal-app.md).

#### Retarget web clips to Microsoft Edge on iOS devices<!-- 5455276   -->
Newly deployed web clips (pinned web apps) on iOS devices that are required to open in a protected browser, will open in Microsoft Edge rather than the Intune Managed Browser. You must retarget pre-existing web clips to ensure they open in Microsoft Edge rather than the Managed Browser. For more information, see [Manage web access by using Microsoft Edge with Microsoft Intune](../apps/manage-microsoft-edge.md) and [Add web apps to Microsoft Intune](../apps/web-app.md).

#### Use the Intune diagnostic tool with Microsoft Edge for Android<!-- 4735244  -->
Microsoft Edge for Android is now integrated with the Intune diagnostic tool. Similarly to the experience on Microsoft Edge for iOS, entering "about:intunehelp" into the URL bar (the address box) of Microsoft Edge on the device will start the Intune diagnostic tool. This tool will provide detailed logs. Users can be guided to collect and send these logs to their IT department, or view MAM logs for specific apps.

#### Updates to Intune branding and customization<!-- 5236032  -->
We have updated the Intune pane that was named "Branding and customization" with improvements, including:

- Renaming the pane to **Customization**.
- Improving the organization and design of the settings.
- Improving the settings text and tooltips.

To find these settings in Intune, navigate to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Tenant administration** > **Customization**. For information about existing customization, see [How to configure the Microsoft Intune Company Portal app](../apps/company-portal-app.md).

#### User's personal encrypted recovery key<!-- 6273943  -->
A new Intune feature is available that enables users to retrieve their personal encrypted **FileVault** recovery key for Mac devices through the Android Company Portal application or through the Android Intune application. There is a link in both the Company Portal application and Intune application that will open a Chrome browser to the Web Company Portal where the user can see the **FileVault** recovery key needed to access their Mac devices. For more information about encryption, see [Use device Encryption with Intune](../protect/encrypt-devices.md).

#### Optimized dedicated device enrollment <!-- 6114580  -->
We're optimizing the enrollment for Android Enterprise dedicated devices and making it easier for SCEP certificates associated with Wi-Fi to apply to dedicated devices enrolled prior to November 22, 2019. For new enrollments, the Intune app will continue to install, but end-users will no longer need to perform the **Enable Intune Agent** step during enrollment. Installment will happen in the background automatically and SCEP certificates associated with Wi-Fi can be deployed and set without end-user interaction.  

These changes will be rolling out on a phased basis throughout the month of March as the Intune service backend deploys. All tenants will have this new behavior by the end of March. For related information, see [Support for SCEP certificates in Android Enterprise dedicated devices](https://techcommunity.microsoft.com/t5/intune-customer-success/support-for-scep-certificates-in-android-enterprise-dedicated/ba-p/928147).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device configuration

#### New user experience when creating administrative templates on Windows devices<!--5096036 -->
Based on customer feedback, and our move to the new Azure full screen experience, we've rebuilt the Administrative Templates profile experience with a folder view. We haven't made changes to any settings or existing profiles. So, your existing profiles will stay the same, and will be usable in the new view. You can still navigate all settings options by selecting **All Settings**, and using search. The tree view is split by Computer and User configurations. You will find Windows, Office, and Edge settings in their associated folders.  

Applies to:
- Windows 10 and newer

#### VPN profiles with IKEv2 VPN connections can use always on with iOS/iPadOS devices<!-- 1947932   -->
On iOS/iPadOS devices, you can create a VPN profile that uses an IKEv2 connection (**Devices** > **Configuration profiles** > **Create profile** > **iOS/iPadOS** for platform > **VPN** for profile type). Now, you can configure always-on with IKEv2. When configured, IKEv2 VPN profiles connect automatically, and stay connected (or quickly reconnect) to the VPN. It stays connected even when moving between networks or restarting devices.

On iOS/iPadOS, always-on VPN is limited to IKEv2 profiles.

To see the IKEv2 settings you can configure, go to [Add VPN settings on iOS devices in Microsoft Intune](../configuration/vpn-settings-ios.md#ikev2-settings).

Applies to:
- iOS/iPadOS

#### Delete bundles and bundle arrays in OEMConfig device configuration profiles on Android Enterprise devices<!-- 5550355   -->
On Android Enterprise devices, you create and update OEMConfig profiles (**Devices** > **Configuration profiles** > **Create profile** > **Android Enterprise** for platform > **OEMConfig** for profile type). Users can now delete bundles and bundle arrays using the **Configuration designer** in Intune.

For more information on OEMConfig profiles, see [Use and manage Android Enterprise devices with OEMConfig in Microsoft Intune](../configuration/android-oem-configuration-overview.md).

Applies to:
- Android Enterprise

#### Configure the iOS/iPadOS Microsoft Azure AD SSO app extension<!-- 5672534   -->
The Microsoft Azure AD team created a redirect single sign-on (SSO) app extension to allow iOS/iPadOS 13.0+ users to gain access to Microsoft apps and websites with one sign-on. All apps that previously had brokered authentication with the Microsoft Authenticator app will continue to get SSO with the new SSO extension. With the Azure AD SSO app extension release, you can configure the SSO extension with the redirect SSO app extension type (**Devices** > **Configuration profiles** > **Create profile** > **iOS/iPadOS** for platform > **Device features** for profile type > **Single sign-on app extension**).

Applies to:
- iOS 13.0 and newer
- iPadOS 13.0 and newer

For more information about iOS SSO app extensions, see [Single sign-on app extension](../configuration/device-features-configure.md#single-sign-on-app-extension).

#### Enterprise app trust settings modification setting is removed from iOS/iPadOS device restriction profiles<!-- 6225131   -->
On iOS/iPadOS devices, you create a device restrictions profile (**Devices** > **Configuration profiles** > **Create profile** > **iOS/iPadOS** for platform > **Device restrictions** for profile type). The **Enterprise app trust settings modification** setting is removed by Apple, and is removed from Intune. If you currently use this setting in a profile, it has no impact, and is removed from existing profiles. This setting is also removed from any reporting in Intune.

Applies to:
- iOS/iPadOS

To see the settings you can restrict, go to [iOS and iPadOS device settings to allow or restrict features](../configuration/device-restrictions-ios.md).

#### Troubleshooting: Pending MAM policy notification changed to informational icon<!--6348954 -->
The notification icon for a pending MAM policy on the Troubleshooting blade has been change to an informational icon.

####  UI update when configuring compliance policy<!-- 3961639    -->

> [!NOTE]
> The Intune user interface is updating to a full screen experience, and may take several weeks. Until your tenant receives this update, you will have a slightly different workflow when you create or edit settings.

We've updated the UI for [creating compliance policies](../protect/create-compliance-policy.md#create-the-policy) in Microsoft Endpoint manager (**Devices** > **Compliance policies** > **Policies** > **Create Policy**). We've a new user experience that includes the same settings and details you've used previously. The new experience follows a wizard-like process to create the compliance policy and includes a page where you can add *Assignments* for the policy, and a *Review + Create* page where you can review your configuration before creating the policy.

#### Retire noncompliant devices<!-- 1827291       -->
We've added a new action for noncompliant devices that you can add to any policy, to  [retire the noncompliant device](../protect/actions-for-noncompliance.md#add-actions-for-noncompliance).  The new action, **Retire the noncompliant device**, results in removal of all company data from the device, and also removes the device from being managed by Intune.  This action runs when the configured value in days is reached and at that point the device becomes eligible to be retired. The minimum value is 30 days.  Explicit IT admin approval will be required to retire the devices by using  the *Retire Non-compliant devices* section, where admins can retire all eligible devices.

#### Support for WPA and WPA2 in iOS Enterprise Wi-Fi profiles<!--6215273   -->
[Enterprise Wi-Fi profiles for iOS](../configuration/wi-fi-settings-ios.md#enterprise-profiles) now support the *Security type* field. For *Security type*, you can select either of **WPA Enterprise** or **WPA/WPA2 Enterprise**, and then specify a selection for the *EAP type*.  (**Devices** > **Configuration profiles** > **Create profile** and select **iOS/iPadOS** for *Platform* and then **Wi-Fi** for *Profile*). 

The new Enterprise options are like those that have been available for a Basic Wi-Fi profile for iOS.

#### New user experience for certificate, email, VPN, and Wi-Fi, VPN profiles<!-- 5615208   -->
We've updated the [user experience](../configuration/device-profile-create.md) in the Endpoint Management Admin Center (**Devices** > **Configuration profiles** > **Create profile**) for creating and modifying the following profile types. The new experience presents the same settings as before, but uses a wizard-like experience that doesn't require as much horizontal scrolling. You won't need to modify existing configurations with the new experience.

- Derived credential
- Email
- PKCS certificate
- PKCS imported certificate
- SCEP certificate
- Trusted certificate
- VPN
- Wi-Fi

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device enrollment

#### Configure if enrollment is available in Company Portal for Android and iOS<!-- 4260128  -->
You can configure whether device enrollment in the Company Portal on Android and iOS devices is available with prompts, available without prompts, or unavailable to users. To find these settings in Intune, navigate to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and, select **Tenant administration** > **Customization** > **Edit** > **Device enrollment**.  

Support for the device enrollment setting requires end users have these Company Portal versions:
-    Company Portal on iOS: version 4.4 or later
-    Company Portal on Android: version 5.0.4715.0 or later

For more information about existing Company Portal customization, see [How to configure the Microsoft Intune Company Portal app](../apps/company-portal-app.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

#### New Android report on Android Devices overview page<!-- 5435435   -->
We've added a report to the Microsoft Endpoint Manager admin console in the Android Devices overview page that displays how many Android devices have been enrolled in each device management solution. This chart (like the same chart already in the Azure console) shows work profile, fully managed, dedicated, and device administrator enrolled device counts. To see the report, choose **Devices** > **Android** > **Overview**.

#### Guide users from Android device administrator management to work profile management<!--5857738   wnstaged-->
We're releasing a new compliance setting for the Android device administrator platform. This setting lets you make a device non-compliant if it's managed with device administrator.

On these non-compliant devices, on the **Update device settings** page users will see the **Move to new device management setup** message. If they tap the **Resolve** button, they'll be guided through:

1. Unenrolling from device administrator management
2. Enrolling in work profile management
3. Resolving compliance issues 
 
Google is decreasing device administrator support in new Android releases in an effort to move to modern, richer, and more secure device management with Android Enterprise.  Intune can only provide full support for device administrator-managed Android devices running Android 10 and later through Q2 CY2020. Device administrator-managed devices (except Samsung) that are running Android 10 or later after this time won't be able to be entirely managed. In particular, impacted devices won't receive new password requirements.

For more information about this setting, see [Move Android devices from device administrator to work profile management](../enrollment/android-move-device-admin-work-profile.md). 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Monitor and troubleshoot

#### The Data Warehouse now provides the MAC address<!-- 6123680  -->
The Intune Data Warehouse provides the MAC address as a new property (`EthernetMacAddress`) in the `device` entity to allow admins to correlate between the user and host mac address. This property helps to reach specific users and troubleshoot incidents occurring on the network. Admins can also use this property in [Power BI reports](../developer/reports-proc-get-a-link-powerbi.md) to build richer reports. For more information, see the Intune Data Warehouse [device](../developer/intune-data-warehouse-collections.md#devices) entity.

#### Additional Data Warehouse device inventory properties<!-- 6125732  -->
Additional device inventory properties are available using the Intune Data Warehouse. The following properties are now exposed via the [devices](../developer/intune-data-warehouse-collections.md#devices) collection:
- 'Model' - The device model.
- 'Office365Version' - The version of Office 365 that is installed on the device.
- 'PhysicalMemoryInBytes` - The physical memory in bytes.
- `TotalStorageSpaceInBytes` - Total storage capacity in bytes.

For more information, see [Microsoft Intune Data Warehouse API](../developer/reports-nav-intune-data-warehouse.md) and the Intune Data Warehouse [device](../developer/intune-data-warehouse-collections.md#devices) entity.

#### Help and support workflow update to support additional services<!-- 5654170   -->
We've updated the Help and support page in the Microsoft Endpoint Manager admin center where you now [choose the management type you use](../fundamentals/get-support.md#options-to-access-help-and-support). With this change you'll be able to select from the following management types:

- Configuration Manager (includes Desktop Analytics)
- Intune
- Co-management

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Security

#### Use a preview of security administrator focused policies as part of Endpoint security<!--6131401  -->
As a public preview, we've added several new policy groups under the Endpoint security node in the Microsoft Endpoint Management admin center. As a security admin you can use these new policies to focus on specific aspects of device security to manage discrete groups of related settings without the overhead of the larger Device Configuration policy body.

With the exception of the new *Antivirus policy for Microsoft Defender Antivirus* (see below), the settings in each new of these new preview policies and profiles are the same settings that you might already configure through [Device configuration profiles](../configuration/device-profile-create.md) today.

The following are the new policy types that are all in preview, and their available profile types:

- **Antivirus (Preview)**:
  - macOS:
    - **Antivirus** - Manage [Antivirus policy settings](../protect/antivirus-microsoft-defender-settings-macos.md) for macOS to manage [Microsoft Defender ATP for Mac](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac).

  - Windows 10 and later:
    - **Microsoft Defender Antivirus** - Manage [Antivirus policy settings](../protect/antivirus-microsoft-defender-settings-windows.md) for cloud protection, Antivirus exclusions, remediation, scan options, and more.

      The Antivirus profile for *Microsoft Defender Antivirus* is an exception that introduces a new instance of settings that are found as part of a device restriction profile. These new Antivirus settings:

        - Are the same settings as found in device restrictions, but support a third option for configuration that's not available when configured as a device restriction.
        - Apply to devices that are co-managed with Configuration Manager, when the [co-management workload slider](https://docs.microsoft.com/configmgr/comanage/how-to-switch-workloads) for Endpoint Protection is set to Intune.

     Plan to use the new *Antivirus* > *Microsoft Defender Antivirus* profile in place of configuring them through a device restriction profile.

  - **Windows Security experience** - Manage the Windows Security settings that end users can view in the Microsoft Defender Security center and the notifications they receive. These settings are unchanged from those available as a Device configuration Endpoint Protection profile.

- **Disk encryption (Preview)**:
  - macOS:
    - **FileVault**
  - Windows 10 and later:
    - **BitLocker**
- **Firewall (Preview)**:
  - macOS:
    - **macOS firewall**
  - Windows 10 and later:
    - **Microsoft Defender Firewall**
- **Endpoint detection and response (Preview)**:
  - Windows 10 and later:
    -**Windows 10 Intune**
- **Attack surface reduction (Preview)**:
  - Windows 10 and later:
    - **App and browser isolation**
    - **Web protection**
    - **Application control**
    - **Attack surface reduction rules**
    - **Device control**
    - **Exploit protection**
- **Account protection (Preview)**:
  - Windows 10 and later:
    - **Account protection**

<!-- ########################## -->
## Week of March 9, 2020

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### App management

#### Configure Delivery Optimization agent when downloading Win32 app content<!-- 5410945 -->

You can configure the Delivery Optimization agent to download Win32 app content either in background or foreground mode based on assignment. For existing Win32 apps, content will continue to download in background mode. In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Apps** > **All apps** > *select the Win32 app* > **Properties**. Select **Edit** next to **Assignments**.  Edit the assignment by selecting **Include** under **Mode** in the **Required** section.  You will find the new setting in the **App settings** section. For more information about Delivery Optimization, see [Win32 app management - Delivery Optimization](../apps/apps-win32-app-management.md#delivery-optimization).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

#### Change Primary User for Windows devices<!-- 3794742   -->
You can change the Primary User for Windows hybrid and Azure AD Joined devices. To do so, go to **Intune** > **Devices** > **All devices** > choose a device > **Properties** > **Primary User**. For more information, see [Change a device's primary user](../remote-actions/find-primary-user.md#change-a-devices-primary-user).

A new RBAC permission (Managed Devices / Set primary user) has also been created for this task. The permission has been added to built-in roles including Helpdesk Operator, School Administrator, and Endpoint Security Manager.

This feature is rolling out to customers globally under preview. You should see the feature within the next few weeks.


<!-- ########################## -->
## Week of March 2, 2020

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

#### Microsoft Endpoint Manager tenant attach: Device sync and device actions<!-- 6317104, CM3555758-->
Microsoft Endpoint Manager is bringing together Configuration Manager and Intune into a single console. Starting in Configuration Manager technical preview version 2002.2, you can upload your Configuration Manager devices to the cloud service and take actions on them in the admin center. For more information, see [Features in Configuration Manager technical preview version 2002.2](https://docs.microsoft.com/configmgr/core/get-started/2020/technical-preview-2002-2#bkmk_attach).

Review the [Configuration Manager technical preview article](https://docs.microsoft.com/configmgr/core/get-started/technical-preview) before installing this update. This article familiarizes you with the general requirements and limitations for using a technical preview, how to update between versions, and how to provide feedback.

#### Bulk remote actions<!--4576882-->
You can now issue bulk commands for the following remote actions: restart, rename, Autopilot reset, wipe, and delete. To see the new bulk actions, go to [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Devices** > **All devices** > **Bulk actions**.

#### All devices list improved search, sort, and filter<!--6179023-->
The All devices list has been improved for better performance, searching, sorting, and filtering. For more information, see [this Support Tip](https://techcommunity.microsoft.com/t5/intune-customer-success/support-tip-changes-in-all-devices-list-and-reporting-in-intune/ba-p/1220946).  

### App management  
####  Improved sign-in experience in Company Portal for Android    
We've updated the layout of several sign-in screens in the Company Portal app for Android to make the experience more modern, simple, and clean for users. For a look at the improvements, see [What's New in the app UI](https://docs.microsoft.com/mem/intune/fundamentals/whats-new-app-ui).

<!-- ########################## -->
## Week of February 24, 2020

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### App management

#### macOS Company Portal user experience improvements<!-- 5568987 -->
We have made improvements to the macOS device enrollment experience and the Company Portal app for Mac. You will see the following improvements:
- A better Microsoft **AutoUpdate** experience during enrollment that will ensure your users have the latest version of the Company Portal.
- An enhanced compliance check step during enrollment.
- Support for copied Incident IDs, so your users can send errors from their devices to your company support team faster.

For more information about enrollment and the Company Portal app for Mac, see [Enroll your macOS device using the Company Portal app](../user-help/enroll-your-device-in-intune-macos-cp.md).

#### App protection policies for Better Mobile now supports iOS and iPadOS<!-- 6224512  -->

In October of 2019, Intune app protection policy added the capability to use data from our Microsoft Threat Defense partners. With this update, you can now use an app protection policy to block, or selectively wipe the users corporate data based on the health of a device using Better Mobile on iOS and iPadOS.  For more information, see [Create Mobile Threat Defense app protection policy with Intune](../protect/mtd-app-protection-policy.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

#### Exports from the All devices list  now in zipped CSV format<!--6343117-->
Exports from the **Devices** > **All devices** page are now in zipped CSV format.


<!-- ########################## -->
## Week of February 17, 2020 (2002 Service release)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### App management

#### Microsoft Defender Advanced Threat Protection (ATP) app for macOS<!-- 5424618 -->
Intune provides an easy way to deploy the Microsoft Defender Advanced Threat Protection (ATP) app for macOS to managed Mac devices. For more information, see [Add Microsoft Defender ATP to macOS devices using Microsoft Intune](../apps/apps-advanced-threat-protection-macos.md) and [Microsoft Defender Advanced Threat Protection for Mac](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac).  

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device configuration

#### Enable network access control (NAC) with Cisco AnyConnect VPN on iOS devices<!-- 4860111  -->
On iOS devices, you can create a VPN profile, and use different connection types, including Cisco AnyConnect (**Device configuration** > **Profiles** > **Create profile** > **iOS** for platform > **VPN** for profile type > **Cisco AnyConnect** for connection type).

You can enable network access control (NAC) with Cisco AnyConnect. To use this feature:

1. At [Cisco Identity Services Engine Administrator Guide](https://www.cisco.com/c/en/us/td/docs/security/ise/2-1/admin_guide/b_ise_admin_guide_21/b_ise_admin_guide_20_chapter_01000.html), use the steps in **Configuring Microsoft Intune as an MDM Server** to configure the Cisco Identity Services Engine (ISE) in Azure.
2. In the Intune device configuration profile, select the **Enable Network Access Control (NAC)** setting.

To see all the available VPN settings, go to [Configure VPN settings on iOS devices](../configuration/vpn-settings-ios.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device enrollment

#### Serial number on the Apple MDM Push certificate page<!--5947765  -->
The Apple MDM Push certificate page now shows the serial number. The serial number is needed to regain access to the Apple MDM Push certificate if access to the Apple ID that created the certificate is lost. To see the serial number, go to **Devices** > **iOS** > **iOS enrollment** > **Apple MDM Push certificate**.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

#### New update schedule options for pushing OS updates to enrolled iOS/iPadOS devices<!--5879689  -->
You can choose from the following options when scheduling operating system updates for iOS/iPadOS devices. These options apply to devices that that used the Apple Business Manager or Apple School Manager enrollment types.
- Update at next check-in
- Update during scheduled time
- Update outside of scheduled time

For the latter two options, you can create multiple time windows.

To see the new options, go to MEM > **Devices** > **iOS** > **Update policies for iOS/iPadOS** > **Create profile**.

#### Choose which iOS/iPadOS updates to push to enrolled devices<!--5879689  -->
You can choose a specific iOS/iPadOS update (except for the most recent update) to push to devices that have enrolled by using either Apple Business Manager or Apple School Manager. Such devices must have a device configuration policy set to delay software update visibility for some number of days. To see this feature, go to MEM > **Devices** > **iOS** > **Update policies for iOS/iPadOS** > **Create profile**.



<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device security

#### Improved Intune reporting experience<!-- 3791418   -->
Intune now provides an improved reporting experience, including new report types, better report organization, more focused views, improved report functionality, as well as more consistent and timely data. The reporting experience will move from public preview to GA (general availability). Additionally, the GA release will provide localization support, bug fixes, design improvements, and aggregate device compliance data on tiles in the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

New report types focus on the following information:

- **Operational** - Provides fresh records with a negative health focus. 
- **Organizational** - Provides a broader summary of the overall state.
- **Historical** - Provides patterns and trends over a period of time.
- **Specialist** - Allows you to use raw data to create your own custom reports.

The first set of new reports focuses on device compliance. For more information, see [Blog - Microsoft Intune reporting framework](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/New-Reporting-Framework-Coming-to-Intune/ba-p/1009553) and [Intune reports](reports.md).

#### Consolidated the location of security baselines in the UI<!-- 6177074   -->
We've consolidated the paths to find [security baselines](../protect/security-baselines.md) in the Microsoft Endpoint Manager admin center by removing *Security baselines* from several UI locations. To find Security baselines, you now use the following path:  **Endpoint security** > **Security baselines**.

#### Expanded support for imported PKCS certificates<!-- 6044197  -->
We've expanded support for using [imported PKCS certificates](../protect/certificates-imported-pfx-configure.md#supported-platforms) to support *Android Enterprise fully managed devices*. Generally, importing PFX certificates is used for S/MIME encryption scenarios, where a user's encryption certificates are required on all of their devices so that email decryption can occur.

The following platforms support import of PFX certificates:

- Android - Device Administrator
- Android Enterprise - Fully Managed
- Android Enterprise - Work profile
- iOS
- Mac
- Windows 10

#### View the endpoint security configuration for devices<!-- 6206460  -->
We've updated the name of the option in the Microsoft Endpoint Manager admin center, for viewing [endpoint security configurations that apply to a specific device](../protect/security-baselines-monitor.md#view-endpoint-security-configurations-per-device). This option is renamed to **Endpoint security configuration** because it shows applicable security baselines and additional policies created outside of security baselines. Previously, this option was named *Security baselines*.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Role-based access control

#### Intune Roles user interface changes coming<!--5801612   -->
The user interface for [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Tenant administration** > **Roles** has been improved to a more user-friendly and intuitive design. This experience provides the same settings and details that you use now, however the new experience employs a wizard-like process.

<!-- ########################## -->
## Week of February 17, 2020

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### App management

#### Microsoft's new Office app<!-- 5859926 -->
Microsoft's new Office app is now generally available for download and use. The Office app is a consolidated experience where your users can work across Word, Excel, and PowerPoint within a single app. You can target the app with an app protection policy to ensure the data being accessed is protected.

For more information, see [How to enable Intune app protection policies with the Office mobile preview app](https://techcommunity.microsoft.com/t5/intune-customer-success/support-tip-how-to-enable-intune-app-protection-policies-with/ba-p/1045493).

<!-- ########################## -->

## Week of February 10, 2020

### Windows 7 ends extended support<!--3042987 -->
Windows 7 reached end of extended support on January 14, 2020. Intune deprecated support for devices running Windows 7 at the same time. Technical assistance and automatic updates that help protect your PC are no longer available. You should upgrade to Windows 10. For more information, see the [Plan for Change blog post](https://aka.ms/Windows7_Intune).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### App management

#### Microsoft Edge version 77 and later on Windows 10 devices<!-- 5843584 -->
Intune now supports uninstalling Microsoft Edge version 77 and later on Windows 10 devices. For more information, see [Add Microsoft Edge for Windows 10 to Microsoft Intune](../apps/apps-windows-edge.md).

#### Screen removed from Company Portal, Android work profile enrollment<!--6103987 -->
The **What's next?** screen has been removed from the Android work profile enrollment flow in Company Portal to streamline the user experience. Go to [Enroll with Android work profile](../user-help/enroll-device-android-work-profile.md) to see the updated Android work profile enrollment flow.  

#### Company Portal app improved performance<!-- 6178652 -->
The Company Portal app has been updated to support improved performance for devices that use ARM64 processors, such as the Surface Pro X. Previously, the Company Portal operated in an emulated ARM32 mode. Now, in version 10.4.7080.0 and above, the Company Portal app is natively compiled for ARM64. For more information about the Company Portal app, see [How to configure the Microsoft Intune Company Portal app](../apps/company-portal-app.md).

<!-- ########################## -->
## Week of January 27, 2020

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### App management

#### Intune support for additional Microsoft Edge version 77 deployment channel for macOS<!-- 5983950  -->
Microsoft Intune now support the additional **Stable** deployment channel for the Microsoft Edge app for macOS. The **Stable** channel is the recommended channel for deploying Microsoft Edge broadly in Enterprise environments. It updates every six weeks, each release incorporating improvements from the **Beta** channel. In addition to the **Stable** and **Beta** channels, Intune supports a **Dev** channel. The public preview offers stable and dev channels for Microsoft Edge version 77 and later for macOS. Automatic updates of the browser are On by default. For more information, see [Add Microsoft Edge for macOS devices using Microsoft Intune](../apps/apps-edge-macos.md).

#### Retirement of Intune Managed Browser<!--5728447 -->
The Intune Managed Browser will be retired. Use Microsoft Edge for your protected Intune browser experience. For more information, see the entry '[Take Action: Use Microsoft Edge for your Protected Intune Browser Experience](whats-new.md#take-action-use-microsoft-edge-for-your-protected-intune-browser-experience)' in the [Notices](whats-new.md#notices) section below.

<!-- ########################## -->
## Week of January 20, 2020 (2001 Service release)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### App management

#### User experience change when adding apps to Intune<!-- 4705829   -->
You'll see a new user experience when adding apps to via Intune. This experience provides the same settings and details that you have used previously, however the new experience follows a wizard-like process before adding an app to Intune. This new experience also provides a review page before adding the app. From the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Apps** > **All apps** > **Add**. For more information, see [Add apps to Microsoft Intune](../apps/apps-add.md).

#### Require Win32 apps to restart <!-- 5622282   -->
You can require that a Win32 app must restart after a successful install. Also, you can choose the amount of time (the grace period) before the restart must occur.

#### User experience change when configuring apps in Intune<!-- 4207990   -->
You'll see a new user experience when creating app configuration policies in Intune. This experience provides the same settings and details that you have used previously, however the new experience follows a wizard-like process before adding a policy to Intune. From the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Apps** > **App configuration policies** > **Add**. For more information, see [App configuration policies for Microsoft Intune](../apps/app-configuration-policies-overview.md). 

#### Intune support for additional Microsoft Edge for Windows 10 deployment channel<!-- 5861774 -->
Microsoft Intune now support the additional **Stable** deployment channel for the Microsoft Edge (version 77 and later) for Windows 10 app. The **Stable** channel is the recommended channel for deploying Microsoft Edge for Windows 10 broadly in Enterprise environments. This channel updates every six weeks, each release incorporating improvements from the **Beta** channel. In addition to the **Stable** and **Beta** channels, Intune supports a **Dev** channel. For more information, see [Microsoft Edge for Windows 10 - Configure app settings](../apps/apps-windows-edge.md#configure-app-settings).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device configuration

#### Improved user interface experience when configuring Exchange ActiveSync on-premises connector UI<!-- 5695492   -->
We've updated the experience for [configuring the Exchange ActiveSync on-premises connector](../protect/exchange-connector-install.md). The updated experience uses a single pane to configure, edit, and summarize the details of your on-premises connectors.

#### Add automatic proxy settings to Wi-Fi profiles for Android Enterprise work profiles<!-- 4490822   -->
On Android Enterprise Work Profile devices, you can create Wi-Fi profiles. When you choose the Wi-Fi Enterprise type, you can also enter the Extensible Authentication Protocol (EAP) type used on your Wi-Fi network.

Now when you choose the Enterprise type, you can also enter automatic proxy settings, including a proxy server URL, such as `proxy.contoso.com`.

To see the current Wi-Fi settings you can configure, go to [Add Wi-Fi settings for devices running Android Enterprise and Android kiosk in Microsoft Intune](../configuration/wi-fi-settings-android-enterprise.md#work-profile-only).

Applies to:
- Android Enterprise work profile

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device enrollment

#### Block Android enrollments by device manufacturer<!--5197392  -->
You can block devices from enrolling based on the manufacturer of the device. This feature applies to Android device administrator and Android Enterprise work profile devices. To see enrollment restrictions, go to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Devices** > **Enrollment restrictions**.

#### Improvements to the iOS/iPadOS Create enrollment type profile UI<!-- 6055005 -->
For iOS/iPadOS User Enrollment, the **Create enrollment type profile** **Settings** page has been streamlined to improve the **Enrollment type** choice process while keeping the same functionality. To see the new UI, go to [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Devices** > **iOS** > **iOS enrollment** > **Enrollment types** > **Create profile** > **Settings** page. For more information, see [Create a User Enrollment profile in Intune](../enrollment/ios-user-enrollment.md#create-a-user-enrollment-profile-in-intune).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

#### New information in device details<!-- 4471759 5604099  -->
The following information is now on the **Overview** page for devices:
- Memory Capacity (amount of physical memory on the device)
- Storage Capacity (amount of physical storage on the device) 
- CPU architecture

#### iOS Bypass Activation Lock remote action renamed to Disable Activation Lock <!--5904591  -->
The remote action **Bypass Activation Lock** has been renamed to **Disable Activation Lock**. For more information, see [Disable iOS Activation Lock with Intune](../remote-actions/device-activation-lock-disable.md).

#### Windows 10 feature update deployment support for Autopilot devices<!-- 5948137   -->
Intune now supports targeting Autopilot registered devices using [Windows 10 feature update deployments](../protect/windows-update-for-business-configure.md#windows-10-feature-updates).

Windows 10 feature update policies cannot be applied during the Autopilot out of box experience (OOBE) and will only apply at the first Windows Update scan after a device has finished provisioning (which is typically a day).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Monitor and troubleshoot

#### Windows Autopilot deployment reports (preview) <!-- 3856172   -->
A new report details each device deployed through Windows Autopilot. For more information, see [Autopilot deployment report](../enrollment/enrollment-autopilot.md#autopilot-deployments-report).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Role-based access control

#### New Intune built-in role Endpoint security manager<!--4253397   -->
A new Intune built-in role is available: the Endpoint security manager. This new role gives admins full access to the Endpoint Manager node in Intune and ready-only access to other areas. The role is an expansion of the "Security Administrator" role from Azure AD. If you currently just have Global Admins as roles, then there's no changes needed. If you use roles, and you'd like the granularity that the Endpoint Security Manager provides, then assign that role when it is available. For more information about built-in roles, see [Role-based access control](role-based-access-control.md).

<!-- ########################## -->
## Week of January 6, 2020

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### App management

#### S/MIME support for Microsoft Outlook for iOS<!-- 2669398 -->
Intune supports delivering S/MIME signing and encryption certificates that can be used with Outlook for iOS on iOS devices. For more information, see [Sensitivity labeling and protection in Outlook for iOS and Android](https://aka.ms/omsmime).

#### Cache Win32 app content using Microsoft Connected Cache server<!-- 6030314 -->
You can install a Microsoft Connected Cache server on your Configuration Manager distribution points to cache Intune Win32 app content. For more information, see [Microsoft Connected Cache in Configuration Manager - Support for Intune Win32 apps](https://docs.microsoft.com/configmgr/core/plan-design/hierarchy/microsoft-connected-cache#bkmk_intune).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Role-based access control

#### Windows 10 administrative templates (ADMX) profiles now support scope tags <!--5137390 -->
You can now assign scope tags to administrative template profiles (ADMX). To do so, go to **Intune** > **Devices** > **Configuration profiles** > choose an administrative templates profile in the list > **Properties** > **Scope tags**. For more information about scope tags, see [Assign scope tags to other objects](../fundamentals/scope-tags.md#assign-scope-tags-to-other-objects).

<!-- ########################## -->
## Week of December 30, 2019

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### App management

#### Retrieve personal recovery key from MEM encrypted macOS devices<!-- 4851745 -->
End users can retrieve their personal recovery key (FileVault key) using the iOS Company Portal app. The device that has the personal recovery key must be enrolled with Intune and encrypted with FileVault through Intune. Using the iOS Company Portal app, an end user can retrieve their personal recovery key on their encrypted macOS device by clicking **Get recovery key**. You can also retrieve the recovery key from Intune by selecting **Devices** > *the encrypted and enrolled macOS device* > **Get recovery key**. For more information about FileVault, see [FileVault encryption for macOS](../protect/encrypt-devices.md#filevault-encryption-for-macos).

#### iOS and iPadOS user-licensed VPP apps<!-- 5619268 -->
For user enrolled iOS and iPadOS devices, end users will no longer be presented with newly created device-licensed VPP applications deployed as available. However, end users will continue to see all user-licensed VPP apps within the Company Portal. For more information about VPP apps, see [How to manage iOS and macOS apps purchased through Apple Volume Purchase Program with Microsoft Intune](../apps/vpp-apps-ios.md).

<!-- ########################## -->
## Week of December 23, 2019

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### App management

#### Notice - Windows 10 1703 (RS2) will be moving out of support <!-- 5026679 -->
Starting October 9, 2018, Windows 10 1703 (RS2) moved out of Microsoft platform support for Home, Pro, and Pro for Workstations editions. For Windows 10 Enterprise and Education editions, Windows 10 1703 (RS2) moved out of platform support on October 8, 2019. Starting December 26, 2019, we will be updating the minimum version of the Windows Company Portal application to Windows 10 1709 (RS3). Computers running versions prior to 1709 will no longer receive updated versions for the application from the Microsoft Store. We have previously communicated this change to customers who are managing older versions of Windows 10 via the message center. For more information, see [Windows lifecycle fact sheet](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet).

<!-- ########################## -->

## Week of December 16, 2019

### Device configuration

#### Updates to Administrative Templates for Windows 10 devices <!-- 5941568 -->

You can use ADMX templates in Microsoft Intune to control and manage settings for Microsoft Edge, Office, and Windows. Administrative Templates in Intune made the following policy setting updates:

- Added support for Microsoft Edge versions 78 and 79.
- Includes the November 11, 2019 ADMX files in [Administrative Template files (ADMX/ADML) and Office Customization Tool for Office 365 ProPlus, Office 2019, and Office 2016](https://www.microsoft.com/download/details.aspx?id=49030).

For more information on ADMX templates in Intune, see [Use Windows 10 templates to configure group policy settings in Microsoft Intune](../configuration/administrative-templates-windows.md).

Applies to:

- Windows 10 and later

## Week of December 9, 2019 (1912 Service release)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### App management

#### Migrating to Microsoft Edge for managed browsing scenarios<!-- 5173762 -->
As we move closer to the retirement of the Intune Managed Browser, we made changes to app protection policies to simplify the steps needed to move your users over to Edge. We have updated the options for the app protection policy setting **Restrict web content transfer with other apps** to be one of the following:

- Any app
- Intune Managed Browser
- Microsoft Edge
- Unmanaged browser 

When you select **Microsoft Edge**, your end users will see conditional access messaging notifying them that Microsoft Edge is required for managed browsing scenarios. They will be prompted to download and sign in to Microsoft Edge with their AAD accounts, if they have not already done so.  This will be the equivalent to having targeted your MAM-enabled apps with the app config setting `com.microsoft.intune.useEdge` set to **True**. Existing app protection policies that used the **Policy managed browsers** setting will now have **Intune Managed Browser** selected, and you will see no change in behavior. This means your users will see messaging to use Microsoft Edge if you've set the **useEdge** app configuration setting to **True**. We encourage all customers leveraging managed browsing scenarios to update their app protection policies with **Restrict web content transfer with other apps** to ensure users are seeing the proper guidance to transition to Microsoft Edge, no matter which app they are launching links from. 

#### Configure app notification content for organization accounts<!-- 2576686  -->
Intune app protection policies (APP) on Android and iOS devices allow you to control app notification content for Org accounts. You can select an option (Allow, Block org Data, or Blocked) to specify how notifications for org accounts are shown for the selected app. This feature requires support from applications and may not be available for all APP enabled applications. Outlook for iOS version 4.15.0 (or later) and Outlook for Android 4.83.0 (or later) will support this setting. The setting is available in the console, but the functionality will begin to take effect after December 16, 2019. For more about APP, see [What are app protection policies?](../apps/app-protection-policy.md).

#### Microsoft app icons update<!--4677605  -->
The icons used for Microsoft apps in the app targeting pane for App protection policies and App configuration policies have been updated.

#### Require use of approved keyboards on Android<!--4761794  -->
As part of an app protection policy, you can specify the setting [**Approved keyboards**](../apps/app-protection-policy-settings-android.md#data-protection) to manage which Android keyboards can be used with managed Android apps. When a user opens the managed app and doesn't already use an approved keyboard for that app, they are prompted to switch to one of the approved keyboards already installed on their device. If needed, they're presented with a link to download an approved keyboard from the Google Play Store, which they can install and set up. The user can only edit text fields in a managed app when their active keyboard isn't one of the approved keyboards.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device configuration

#### Updated single sign-on experience for apps and websites on your iOS, iPadOS, and macOS devices<!-- 4999578  -->
Intune has added more single sign-on (SSO) settings for iOS, iPadOS, and macOS devices. You can now configure redirect SSO app extensions written by your organization or by your identity provider. Use these settings to configure a seamless single sign-on experience for apps and websites that use modern authentication methods, such as OAuth and SAML2. 

These new settings expand on the previous settings for SSO app extensions and Apple's built-in Kerberos extension (**Devices** > **Device configuration** > **Profiles** > **Create profile** > **iOS/iPadOS** or **macOS** for platform type > **Device features** for profile type). 

To see the full range of SSO app extension settings you can configure, go to [SSO on iOS](../configuration/ios-device-features-settings.md#single-sign-on-app-extension) and [SSO on macOS](../configuration/macos-device-features-settings.md#single-sign-on-app-extension).

Applies to:

- iOS/iPadOS
- macOS

#### We have updated two device restriction settings for iOS and iPadOS devices to correct their behavior<!-- 5701352    -->
For iOS devices, you can create device restriction profiles that **Allow over-the-air PKI updates** and **Blocks USB Restricted mode** (**Devices** > **Device configuration** > **Profiles** > **Create profile** > **iOS/iPadOS** for platform > **Device restrictions** for profile type). Prior to this release, the UI settings and descriptions for the following settings were incorrect, and they have now been corrected. Beginning with this release, the settings behavior is as follows:

**Block over-the-air PKI updates**: **Block** prevents your users from receiving software updates unless the device is connected to a computer. **Not configured** (default): allows a device to receive software updates without being connected to a computer.
- Previously, this setting let you configure it as: **Allow**, which let your users receive software updates without connecting their devices to a computer.
**Allow USB accessories while device is locked**: **Allow** lets USB accessories exchange data with a device that's been locked for over an hour. **Not configured** (default) doesn't update USB Restricted mode on the device, and USB accessories will be blocked from transferring data from the device if locked for over an hour.
- Previously, this setting let you configure it as: **Block** to disable USB Restricted mode on supervised devices.

For more information on the setting you can configure, see [iOS and iPadOS device settings to allow or restrict features using Intune](../configuration/device-restrictions-ios.md).

This feature applies to:

- OS/iPadOS

#### Wired network device configuration profiles for macOS devices<!-- 3508686  -->
   > [!NOTE]
   > This feature has been delayed, but will be released soon.

#### Block users from configuring certificate credentials in the managed keystore on Android Enterprise device owner devices<!-- 3311998 -->
On Android Enterprise device owner devices, you can configure a new setting that blocks users from configuring their certificate credentials in the managed keystore (**Device configuration** > **Profiles** > **Create profile** > **Android Enterprise** for platform > **Device Owner Only > Device Restrictions** for profile type > **Users + Accounts**).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

#### Protected wipe action now available<!--51150000 -->
You now have the option to use the Wipe device action to perform a protected wipe of a device. Protected wipes are the same as standard wipes, except that they can't be circumvented by powering off the device. A protected wipe will keep trying to reset the device until successful. In some configurations, this action may leave the device unable to reboot. For more information, see [Retire or wipe devices](../remote-actions/devices-wipe.md).

#### Device Ethernet MAC address added to device's Overview page<!--5562275 -->
You can now see a device's Ethernet MAC address on the device details page (**Devices** > **All devices** > choose a device > **Overview**.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device security

#### Improved experience on a shared device when device-based conditional access policies are enabled<!-- 1734096  -->
We improved the experience on a shared device with multiple users who are targeted with device-based conditional access policy by checking the latest compliance evaluation for the user when enforcing policy. 
For more information, see  the following overview articles:
- [Azure overview for Conditional Access](https://docs.microsoft.com/azure/active-directory/conditional-access/overview)
- [Intune device compliance overview](../protect/device-compliance-get-started.md)

#### Use PKCS certificate profiles to provision devices with certificates<!-- 2317124, 2317130, 2317139, 2340517, 2340528, 2340529  -->
You can now use PKCS certificate profiles to issue certificates to *devices* that run Android for Work, iOS/iPadOS, and Windows, when associated with profiles like those for Wi-Fi and VPN. Previously those three platforms supported only user-based certificates, with device-based support being limited to macOS.

> [!NOTE]
> PKCS certificate profiles are not supported with Wi-Fi profiles. Instead, use SCEP certificate profiles when you use an [EAP type](../configuration/wi-fi-settings-windows.md#enterprise-profile).

To use a device-based certificate, while [creating a PKCS certificate profile](../protect/certficates-pfx-configure.md#create-a-pkcs-certificate-profile) for the supported platforms, select **Settings**. You'll now see the setting for **Certificate type**, which supports the options for Device, or User.


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Monitor and troubleshoot

#### Centralized audit logs<!--5603185, 5697164 -->
A new centralized audit log experience now collects audit logs for all categories into one page. You can filter the logs to get the data you're looking for. To see the audit logs, go to **Tenant administration** > **Audit logs**. 

#### Scope tag information included in audit log activity details<!--5763534 -->
Audit log activity details now include scope tag information (for Intune objects that support scope tags). For more information about audit logs, see [Use audit logs to track and monitor events](monitor-audit-logs.md).

<!-- ########################## -->
## Week of December 2, 2019

#### New Microsoft Endpoint Configuration Manager co-management licensing<!--5027281-->
Configuration Manager customers with Software Assurance can get Intune co-management for Windows 10 PCs without having to purchase an additional Intune license for co-management. Customers no longer need to assign individual Intune/EMS licenses to their end users for co-managing Windows 10.
- Devices managed by Configuration Manager and enrolled into co-management have almost the same rights as Intune Standalone MDM-managed PCs. However, after resetting they can't be re-provisioned by using Autopilot.
- Windows 10 devices enrolled into Intune by using other means require full Intune licenses.
- Devices on other platforms still require full Intune licenses.

For more information, see [Licensing terms](https://www.microsoft.com/en-us/Licensing/product-licensing/products).

<!-- ########################## -->
## Week of November 18, 2019 (1911 Service release)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### App management

#### UI update when selectively wiping app data<!-- 4102028 -->
The UI to selectively wipe app data in Intune has been updated. UI changes include:
- A simplified experience by using a wizard-style format condensed within one pane.
- An update to the create flow to include assignments.
- A summarized page of all things set when viewing properties, prior to creating a new policy or when editing a property. Also, when editing properties, the summary will only show a list of items from the category of properties being edited.

For more information, see [How to wipe only corporate data from Intune-managed apps](../apps/apps-selective-wipe.md).

#### iOS and iPadOS third-party keyboard support<!-- 4922950 -->
In March  2019, we announced the removal of support for the iOS App protection policy setting "Third party keyboards". The feature is returning to Intune with both iOS and iPadOS support. To enable this setting, visit the **Data protection** tab of a new or existing iOS/iPadOS app protection policy and find the **Third party keyboards** setting under **Data Transfer**.

The behavior of this policy setting differs slightly from the previous implementation. In multi-identity apps using SDK version 12.0.16 and later, targeted by app protection policies with this setting configured to **Block**, end users will be unable to opt for third party keyboards in both their organization and personal accounts. Apps using SDK versions 12.0.12 and earlier will continue to exhibit the behavior documented in our blog post title, [Known issue: Third party keyboards are not blocked in iOS for personal accounts](https://aka.ms/3rdparty_iOS_Intune).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device configuration

#### Target macOS user groups to require Jamf management<!-- 4061739  --> 
You can target specific groups of users that will get their [macOS devices managed by Jamf](../protect/conditional-access-integrate-jamf.md). This targeting enables you to apply the Jamf compliance integration to a subset of macOS devices while other devices are managed by Intune. If you are already using the Jamf integration, All Users will be targeted for the integration by default.

#### New Exchange ActiveSync settings when creating an Email device configuration profile on iOS devices<!-- 4892824   --> 
On iOS/iPadOS devices, you can configure email connectivity in a device configuration profile (**Device configuration** > **Profiles** > **Create profile** > **iOS/iPadOS** for platform > **Email** for profile type). 

There are new Exchange ActiveSync settings available, including:
- **Exchange data to sync**: Choose the Exchange services to sync (or block syncing) for Calendar, Contacts, Reminders, Notes, and Email.
- **Allow users to change sync settings**: Allow (or block) users to change the sync settings for these services on their devices.  

For more information on these settings, go to [Email profile settings for iOS devices in Intune](../configuration/email-settings-ios.md). 

Applies to:

- iOS 13.0 and newer
- iPadOS 13.0 and newer

#### Prevent users from adding personal Google accounts to Android Enterprise fully managed and dedicated devices<!-- 5353228   -->
On Android Enterprise fully managed and dedicated devices, there's a new setting that prevents users from creating personal Google accounts (**Device configuration** > **Profiles** > **Create profile** > **Android Enterprise** for platform > **Device Owner Only > Device Restrictions** for profile type > **Users and Accounts settings** > **Personal Google Accounts**).

To see the settings you can configure, go to [Android Enterprise device settings to allow or restrict features using Intune](../configuration/device-restrictions-android-for-work.md).

Applies to:

- Android Enterprise fully managed devices
- Android Enterprise dedicated devices

#### Server-side logging for Siri commands setting is removed in iOS/iPadOS device restrictions profile <!-- 5468501   -->
On iOS and iPadOS devices, the **Server-side logging for Siri commands** setting is removed from the Microsoft Endpoint Manager admin console (**Device configuration** > **Profiles** > **Create profile** > **iOS/iPadOS** for platform > **Device restrictions** for profile type > **Built-in apps**). 

This setting has no effect on devices. To remove the setting from existing profiles, open the profile, make any change, and then save the profile. The profile is updated, and the setting is deleted from devices.

To see all the settings you can configure, see [iOS and iPadOS device settings to allow or restrict features using Intune](../configuration/device-restrictions-ios.md).

Applies to:

- iOS/iPadOS

#### Windows 10 feature updates (public preview)<!-- 2384877 -->
You can now deploy [Windows 10 feature updates](../protect/windows-update-for-business-configure.md#windows-10-feature-updates) to Windows 10 devices. Windows 10 feature updates are a new software update policy that sets the version of Windows 10 that you want devices to install and remain at. You can use this new policy type along with your existing Windows 10 update rings.

Devices that receive Windows 10 feature updates policy will install the specified version of Windows, and then remain at that version until the policy is edited or removed. Devices that run a later version of Windows remain at their current version. Devices that are held at a specific version of Windows can still install quality and security updates for that version from Windows 10 update rings.

This new type of policy begins rolling out to tenants this week. If this policy isn't available for your tenant yet, it will be soon.

#### Add and change key information in plist files for macOS applications<!-- 4736278 -->
On macOS devices, you can now create a device configuration profile that uploads a property list file (.plist) associated with an app or with the device (**Devices** > **Configuration profiles** > **Create profile** > **macOS** for platform > **Preference File** for profile type).

Only some apps support managed preferences, and these apps might not allow you to manage all settings. Be sure to upload a property list file that configures device channel settings, not user channel settings.

For more information on this feature, see [Add a property list file to macOS devices using Microsoft Intune](../configuration/preference-file-settings-macos.md).

Applies to:

- macOS devices running 10.7 and newer

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

#### Edit device name value for Autopilot devices<!-- 2640074 -->
You can edit the Device Name value for Azure AD Joined Autopilot devices.  For more information, see [Edit Autopilot device attributes](../enrollment/enrollment-autopilot.md#edit-autopilot-device-attributes).

#### Edit Group Tag value for Autopilot devices<!-- 4816775   -->
You can edit the Group Tag value for Autopilot devices. For more information, see [Edit Autopilot device attributes](../enrollment/enrollment-autopilot.md#edit-autopilot-device-attributes).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Monitor and troubleshoot

#### Updated support experience<!-- 5012398 -->

Starting today, an updated and streamlined in-console experience for [getting help and support for Intune](get-support.md) is rolling out to tenants. If this new experience isn't available for you yet, it will be soon.

We've improved the in-console search and feedback for common issues, and the workflow you use to contact support. When opening a support issue, you'll see real-time estimates for when you can expect a callback or email reply, and Premier and Unified support customers can easily specify a severity for their issue, to help get support faster.

#### Improved Intune reporting experience (public preview) <!-- 3791418 -->
Intune now provides an improved reporting experience, including new report types, better report organization, more focused views, improved report functionality, as well as more consistent and timely data. New report types focus on the following:

- **Operational** - Provides fresh records with a negative health focus. 
- **Organizational** - Provides a broader summary of the overall state.
- **Historical** - Provides patterns and trends over a period of time.
- **Specialist** - Allows you to use raw data to create your own custom reports.

The first set of new reports focuses on device compliance. For more information, see [Blog - Microsoft Intune reporting framework](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/New-Reporting-Framework-Coming-to-Intune/ba-p/1009553) and [Intune reports](reports.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Role-based access control

#### Duplicate custom or built-in roles <!-- 1081938   -->
You can now copy built-in and custom roles. For more information, see [Copy a role](../fundamentals/create-custom-role.md#copy-a-role).

#### New permissions for school administrator role <!-- 5621805  -->  
Two new permissions, **Assign profile** and **Sync device**, have been added to the school administrator role > **Permissions** > **Enrollment programs**. The sync profile permission lets group admins sync Windows Autopilot devices. The assign profile permission lets them delete user-initiated Apple enrollment profiles. It also gives them permission to manage Autopilot device assignments and Autopilot deployment profile assignments. For a list of all school administrator/group admin permissions, see [Assign group admins](https://docs.microsoft.com/intune-education/group-admin-delegate).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Security

#### BitLocker key rotation<!-- 2564951  -->
You can use an Intune device action to remotely [rotate BitLocker recovery keys](../protect/encrypt-devices.md#rotate-bitlocker-recovery-keys)  for managed devices that run Windows version 1909 or later. To qualify to have recovery keys rotated, devices must be configured to support recovery key rotation.  

#### Updates to dedicated device enrollment to support SCEP device certificate deployment <!-- 5198878  -->
Intune now supports SCEP device certificate deployment to Android Enterprise dedicated devices for certificate-based access to Wi-Fi profiles. The Microsoft Intune app must be present on the device for deployment to work. As a result, we've updated the enrollment experience for Android Enterprise dedicated devices. New enrollments still start the same (with QR, NFC, Zero-touch, or device identifier) but now have a step that requires users to install the Intune app. Existing devices will start getting the app automatically installed on a rolling basis.

#### Intune audit logs for business-to-business collaboration<!--5670211 -->
Business-to-business (B2B) collaboration allows you to securely share you company's applications and services with guest users from any other organization, while maintaining control over your own corporate data. Intune now supports audit logs for B2B guest users. For example, when guest users make changes, Intune will be able to capture this data through audit logs. For more information, see [What is guest user access in Azure Active Directory B2B?](https://docs.microsoft.com/azure/active-directory/b2b/what-is-b2b)

<!-- ########################## -->
## Week of November 11, 2019  

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### App management  

#### Improved macOS enrollment experience in Company Portal <!-- 5074349  -->  
The Company Portal for macOS enrollment experience has a simpler enrollment process that aligns more closely with the Company Portal for iOS enrollment experience. Device users now see:  

- A sleeker user interface.  
- An improved enrollment checklist.  
- Clearer instructions about how to enroll their devices.  
- Improved troubleshooting options.  

#### Web apps launched from the Windows Company Portal app<!-- 5030972 -->
End users can now launch web apps directly from the Windows Company Portal app. End users can select the web app and then choose the option **Open in browser**. The published web URL is opened directly in a web browser. This functionality will be rolled out over the next week. For more information about Web apps, see [Add web apps to Microsoft Intune](../apps/web-app.md).  

#### New assignment type column in Company Portal for Windows 10 <!-- 5459950  -->
The Company Portal > **Installed Apps** > **Assignment type** column has been renamed to **Required by your organization**.  Under that column, users will see a **Yes** or **No** value to indicate that an app is either required or made optional by their organization. These changes were made because device users were confused about the concept of available apps. Your users can find more information about installing apps from Company Portal in [Install and share apps on your device](../user-help/install-apps-cpapp-windows.md). For more  information about configuring the Company Portal app for your users, see [How to configure the Microsoft Intune Company Portal app](../apps/company-portal-app.md).  

<!-- ########################## -->
## Week of November 4, 2019

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device security

#### Security baselines are supported on Microsoft Azure Government<!-- 4062552 -->

Instances of  Intune that are hosted on *Microsoft Azure Government* can now use [security baselines](../protect/security-baselines.md) to help you secure and protect your users and devices.

## What's New archive
For previous months, see the [What's New archive](whats-new-archive.md).

## Notices

[!INCLUDE [Intune notices](../includes/intune-notices.md)]


