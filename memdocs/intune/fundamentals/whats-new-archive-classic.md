---
# required metadata

title: What's new in Microsoft Intune classic portal archive
description: Archived What's New announcements for Microsoft Intune
keywords:
author: dougeby  
ms.author: dougeby
manager: dougeby
ms.date: 06/08/2017
ms.topic: archived
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: medium
ms.technology:
ms.assetid: ed2db991-4729-49a7-a1e6-be2ffa0d03d1

# optional metadata

ROBOTS: noindex,nofollow
#audience:

#ms.reviewer:
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-classic
ms.collection: M365-identity-device-management
---
# What's new in the Intune classic portal - previous months

[!INCLUDE [classic-portal](../includes/classic-portal.md)]

This page lists new features and notices previously announced on the [What's new page](whats-new.md) for the Intune classic portal.

## April 2017

### New capabilities

#### MyApps available for Managed Browser <!--822308, 822303-->

Microsoft MyApps now have better support within the Managed Browser. Managed Browser users who are not targeted for management will be brought directly to the MyApps service, where they can access their admin-provisioned SaaS apps. Users who are targeted for Intune management will continue to be able to access MyApps from the built-in Managed Browser bookmark.

#### New icons for the Managed Browser and the Company Portal <!--918433, 918431, 971473-->

The Managed Browser is receiving updated icons for both the Android and iOS versions of the app. The new icon will contain the updated Intune badge to make it more consistent with other apps in Enterprise Mobility + Security (EM+S). You can see the new icon for the Managed Browser on the [what's new in Intune app UI page](whats-new-app-ui.md).

The Company Portal is also receiving updated icons for the Android, iOS, and Windows versions of the app to improve consistency with other apps in EM+S. These icons will be gradually released across platforms from April to late May.

#### Sign in progress indicator in Android Company Portal <!--953374-->

An update to the Android Company Portal app shows a sign-in progress indicator when the user launches or resumes the app. The indicator progresses through new statuses, beginning with "Connecting...", then "Signing in...", then "Checking for security requirements..." before allowing the user to access the app. You can see the new screens for the Company Portal app for Android on the [what's new in Intune app UI page](whats-new-app-ui.md).

#### Block apps from accessing SharePoint Online <!-- 679339 -->

You can now create an app-based Conditional Access policy to block apps, which don't have app protection policies applied to them, from accessing [SharePoint Online](../protect/app-based-conditional-access-intune-create.md). In the apps-based Conditional Access scenario, you can specify the apps that you want to have access to SharePoint Online using the Azure portal.

#### Single sign-on support from the Company Portal for iOS to Outlook for iOS <!--834012-->
Users no longer have to sign in to the Outlook app if they are signed in to the Company Portal app for iOS on the same device with the same account. When users launch the Outlook app, they will be able to select their account and automatically sign in. We are also working toward adding this functionality for other Microsoft apps.

#### Improved status messaging in the Company Portal app for iOS <!--744866-->
New, more specific error messages will now be displayed within the Company Portal app for iOS to provide more accessible information about what is happening on devices. These error cases were previously included in a general error message titled "Company Portal Temporarily Unavailable". Additionally, if a user launches the Company Portal on iOS when they do not have an Internet connection, they will now see a persistent status bar on the homepage saying "No Internet Connection."

#### Improved app install status for the Windows 10 Company Portal app <!--676495-->

New improvements for app install started in the Windows 10 Company Portal app include:
- Faster install progress reporting for MSI packages
- Faster install progress reporting for modern apps on devices running the Windows 10 Anniversary Update and beyond
- New progress bar for modern app installs on devices running the Windows 10 Anniversary Update and beyond

You can see the new progress bar on the [what's new in Intune app UI page](whats-new-app-ui.md).

#### Bulk Enroll Windows 10 devices <!-- 747607 -->

You can now join large numbers of devices that run the Windows 10 Creators update to Azure Active Directory and Intune with Windows Configuration Designer (WCD). To enable [bulk MDM enrollment](../enrollment/windows-bulk-enroll.md) for your Azure AD tenant, create a provisioning package that joins devices to your Azure AD tenant using Windows Configuration Designer, and apply the package to corporate-owned devices you'd like to bulk enroll and manage. Once the package is applied to your devices, they will Azure AD join, enroll in Intune, and be ready for your Azure AD users to log on.  Azure AD users are standard users on these devices and receive assigned policies and required apps. Self-service and Company Portal scenarios are not supported at this time.

### What's new in the public preview of Intune in the Azure portal<!--736542-->

In early calendar year 2017 we will be migrating our full admin experience onto Azure, allowing for powerful and integrated management of core EMS workflows on a modern service platform that's extensible using Graph APIs.

New trial tenants will start to see the public preview of the new admin experience in the Azure portal this month. While in preview state, capabilities and parity with the existing Intune console will be delivered iteratively.

The admin experience in the Azure portal will use the already announced new grouping and targeting functionality; when your existing tenant is migrated to the new grouping experience you will also be migrated to preview the new admin experience on your tenant. In the meantime, if you want to test or look at any of the new functionality until your tenant is migrated, sign up for a new Intune trial account or take a look at the [new documentation](whats-new.md).

You can find what's new in the Intune preview in Azure [here](whats-new.md).

### Notices

#### Direct access to Apple enrollment scenarios <!--951869-->

For Intune accounts created after January 2017, Intune has enabled direct access to Apple enrollment scenarios using the Enroll Devices workload in the Azure Preview portal. Previously, the Apple enrollment preview was only accessible from links in the Azure portal. Intune accounts created before January 2017 will require a one-time migration before these features are available in Azure. The schedule for migration has not been announced yet, but details will be made available as soon as possible. We strongly recommend creating a trial account to test out the new experience if your existing account cannot access the preview.

#### What's coming for Appx in Intune in the Azure portal <!-- 1000270 -->

As part of the migration to Intune in the Azure portal, we are making three appx changes:

1. Adding a new appx app type in the Intune console that can only be deployed to MDM-enrolled devices.
2. Repurposing the existing appx app type to only be targeted to PCs managed through the Intune PC agent.
3. Converting all existing appxs into MDM appxs with the migration.

##### How does this affect me?

This will not impact any of your existing deployments to devices that are managed through the Intune PC agent. However, after migration, you will not be able to deploy those migrated appxs to any new devices that are managed through the Intune PC agent that were not previously targeted.

##### What action do I need to take

After migration, you will need to re-upload the appx again as a PC appx if you want to do new PC deployments. To learn more, see [Appx changes in Intune in the Azure portal](https://aka.ms/appxchange) on the Intune Support team blog.  

#### Administration roles being replaced in Azure portal

The existing mobile application management (MAM) administration roles (Contributor, Owner, and Read-Only) used in the Intune classic portal (Silverlight) are being replaced with a full set of new role-based administration controls (RBAC) in the Intune Azure portal. Once you are migrated to the Azure portal, you will need to re-assign your admins to these new administration roles. For more information about RBAC and the new roles, see [Role-based access control for Microsoft Intune](role-based-access-control.md).

### What's coming

#### Improved sign in experience across Company Portal apps for all platforms <!--User Story 1132123-->

We are announcing a change that is coming in the next few months that will improve the sign-in experience for the Intune Company Portal apps for Android, iOS, and Windows. The new user experience will automatically appear across all platforms for the Company Portal app when Azure AD makes this change. In addition, users can now sign in to the Company Portal from another device with a generated, single-use code. This is especially useful in cases when users need to sign in without credentials.

You can find screenshots of the previous sign-in experience, the new sign-in experience with credentials, and the new sign-in experience from another device on the [What's new in app UI](whats-new-app-ui.md) page.

#### Plan for change: Intune is changing the Intune Partner Portal experience <!-- 1050016 -->

We are removing the Intune Partner page from manage.microsoft.com beginning with the service update in mid-May 2017.  

If you are a partner administrator, you will no longer be able to view and take action on behalf of your customers from the Intune Partner page, but will instead need to sign in at one of two other partner portals at Microsoft.

Both the [Microsoft Partner Center](https://partnercenter.microsoft.com/) and the [Microsoft 365 admin center](https://admin.microsoft.com/) will allow you to sign into the customer accounts you manage. Moving forward as a partner, please use one of these sites to manage your customers.


#### Apple to require updates for Application Transport Security <!--748318-->

Apple has announced that they will enforce specific requirements for Application Transport Security (ATS). ATS is used to enforce stricter security on all app communications over HTTPS. This change impacts Intune customers using the iOS Company Portal apps.

We have made available a version of the Company Portal app for iOS through the Apple TestFlight program that enforces the new ATS requirements. If you would like to try it so you can test your ATS compliance, email <a href="mailto:CompanyPortalBeta@microsoft.com?subject=Register to TestFlight ATS Company Portal app">CompanyPortalBeta@microsoft.com</a> with your first name, last name, email address, and company name. Review our [Intune support blog](https://aka.ms/compportalats) for more details.

## March 2017

### New Capabilities

#### Support for Skycure

You can now control mobile device access to corporate resources using Conditional Access based on risk assessment conducted by Skycure, a mobile threat defense solution that integrates with Microsoft Intune. Risk is assessed based on telemetry collected from devices running Skycure, including:

- Physical defense
- Network defense
- Application defense
- Vulnerabilities defense

You can configure EMS Conditional Access policies based on Symantec Endpoint Protection Mobile (Skycure) risk assessment enabled through Intune device compliance policies. You can use these policies to allow or block noncompliant devices access to corporate resources based on detected threats. For more information, see [Symantec Endpoint Protection Mobile connector](../protect/skycure-mobile-threat-defense-connector.md).

#### New user experience for the Company Portal app for Android <!--621622-->

The Company Portal app for Android will be updating its user interface for a more modern look and feel, and better user experience. The notable updates are:

- Colors: Company Portal tab headers are colored in IT-defined branding.
- Apps: In the **Apps** tab, the **Featured Apps** and **All Apps** buttons are updated.
- Search: In the **Apps** tab, the **Search** button is a floating action button.
- Navigating Apps: **All Apps** view shows a tabbed view of **Featured**, **All**, and **Categories** for easier navigation.
- Support: **My Devices** and **Contact IT** tabs are updated to improve readability.

For more details about these changes, see [UI updates for Intune end user apps](whats-new-app-ui.md).

#### Non-managed devices can access assigned apps <!--664691-->

As part of the design changes on the Company Portal website, iOS and Android users will be able to install apps assigned to them as "available without enrollment" on their non-managed devices. Using their Intune credentials, users will be able to log into the Company Portal website and see the list of apps assigned to them. The app packages of the "available without enrollment" apps are made available for download via the Company Portal website. Apps which require enrollment for installation are not affected by this change, as users will be prompted to enroll their device if they wish to install those apps.

#### Signing Script for Windows 10 Company Portal <!--941642-->

If you need to download and sideload the Windows 10 Company Portal app, you can now use a script to simplify and streamline the app-signing process for your organization.   To download the script and the instructions for using it, see  [Microsoft Intune Signing Script for Windows 10 Company Portal](https://aka.ms/intunecpscript). For more details about this announcement, see [Updating your Windows 10 Company Portal app](https://blogs.technet.microsoft.com/intunesupport/2017/03/13/updating-your-windows-10-company-portal-app/) on the Intune Support Team Blog.


### Notices

#### Support for iOS 10.3

The iOS 10.3 release started rolling out on March 27, 2017 to iOS users. All existing Intune MDM and MAM scenarios are compatible with the latest version of Apple's OS. We anticipate all existing Intune features currently available for managing iOS devices will continue to work as your users upgrade their devices and apps to iOS 10.3.

There are currently no known issues to share. If you run into any issues with iOS 10.3, please feel free to reach out to the [Intune support team](../../get-support.md).

#### Improved support for Android users based in China <!--720444-->

Due to the absence of the Google Play Store in China, Android devices must obtain apps from Chinese marketplaces. The Company Portal will support this workflow by redirecting Android users in China to download the Company Portal and Outlook apps from local app stores. This will improve the user experience when Conditional Access policies are enabled, both for Mobile Device Management and for Mobile Application Management. The Company Portal and Outlook apps for Android are available on the following Chinese app stores:

- [Baidu](https://go.microsoft.com/fwlink/?linkid=836946)
- [Tencent](https://go.microsoft.com/fwlink/?linkid=836949)
- [Wandoujia](https://go.microsoft.com/fwlink/?linkid=836950)

#### Best practice: make sure your Company Portal apps are up to date <!--879465-->

In December 2016, we released an update that enabled enforcement for multi-factor authentication (MFA) on a group of users when they enroll an iOS, Android, Windows 8.1+, or Windows Phone 8.1+ device. This feature cannot work without certain baseline versions of the Company Portal app for Android (v5.0.3419.0+) and iOS (v2.1.17+).

Microsoft is continuously improving Intune by adding new functions to both the console and the Company Portal apps on all supported platforms. As a result, Microsoft only releases fixes for issues that we find in the current version of the Company Portal app. We therefore recommend using the latest versions of the Company Portal apps for the best user experience.

>[!Tip]
> Have your users set their devices to automatically update apps from the appropriate app store. If you have made the Android Company Portal app available on a network share, you can download the latest version from [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=49140).

#### Microsoft Teams is now enabled for MAM on iOS and Android

Microsoft has announced the general availability of Microsoft Teams. The updated Microsoft Teams apps for iOS and Android are now enabled with Intune mobile app management (MAM) capabilities, so you can empower your teams to work freely across devices, while ensuring that conversations and corporate data is protected at every turn. For more details, see [the Microsoft Teams announcement](https://blogs.technet.microsoft.com/enterprisemobility/2017/03/14/microsoft-teams-is-now-generally-available-and-mam-enabled-on-ios-and-android/) on the Enterprise Mobility and Security blog.


## February 2017

### New Capabilities

### Modernizing the Company Portal website <!--753980-->
The Company Portal website will support apps that are targeted to users who do not have managed devices. The website will align with other Microsoft products and services by using a new contrasting color scheme, dynamic illustrations, and a "hamburger menu," ![Small image of the hamburger menu that is now added at the top left corner of the Company Portal website](./media/whats-new-archive-classic/CP_hamburger_menu.png).

### Notices

#### Group migration will not require any updates to groups or policies for iOS devices <!--898837-->
For every Intune device group pre-assigned by a Corporate Device Enrollment profile, a corresponding dynamic device group will be created in Azure AD based on the Corporate Device Enrollment profile's name, during the migration to Azure Active Directory device groups. This will ensure the as devices enroll, they will be automatically grouped and receive the same policies and apps as the original Intune group.

Once a tenant enters the migration process for grouping and targeting, Intune will automatically create a dynamic Azure AD group to correspond to an Intune group targeted by a Corporate Device Enrollment profile. If the Intune Admin deletes the targeted Intune group, the corresponding dynamic Azure AD group will not be deleted. The group's members and the dynamic query will be cleared, but the group itself will remain until the IT Admin removes it via the Azure AD portal.

Similarly, if the IT Admin changes which Intune group is targeted by a Corporate Device Enrollment profile, Intune will create new dynamic group reflecting the new profile assignment, but will not remove the dynamic group created for the old assignment.

### Defaulting to managing Windows desktop devices through Windows settings <!--663050-->
The default behavior for enrolling Windows 10 desktops is changing. New enrollments will follow the typical MDM agent enrollment flow rather than through the PC agent. The Company Portal website will provide Windows 10 desktop users with enrollment instructions that guide them through the process of adding Windows 10 desktop computers as mobile devices. This will not impact currently enrolled PCs, and your organization can still manage Windows 10 desktops using the PC agent [if you prefer](./intune-legacy-pc-client.md).

#### Improving mobile app management support for selective wipe <!--581242-->
End users will be given additional guidance on how to regain access to work or school data if that data is automatically removed due to the "Offline interval before app data is wiped" policy.<!--, or the removal of the Intune Company Portal on Android.-->

#### Company Portal for iOS links open inside the app <!--665954-->
Links inside of the Company Portal app for iOS, including those to documentation and apps, will open directly in the Company Portal app using an in-app view of Safari. This update will ship separately from the service update in January.

#### New MDM server address for Windows devices <!--893007-->
Windows and Windows Phone users attempting to enroll a device will fail if they enter __manage.microsoft.com__ as the MDM server address (if prompted). The MDM server address is changing from __manage.microsoft.com__ to __enrollment.manage.microsoft.com__. Notify your user to use __enrollment.manage.microsoft.com__ as the MDM server address if prompted for it while enrolling a Windows or and Windows Phone device. No changes are needed to your CNAME setup. For additional information about this change, visit [aka.ms/intuneenrollsvrchange](https://aka.ms/intuneenrollsvrchange).

#### New user experience for the Company Portal app for Android <!--621622-->
Beginning in March, the Company Portal app for Android will follow [material design guidelines](https://material.io/guidelines/material-design/introduction.html) to create a more modern look and feel. This improved user experience includes:

* __Colors__: tab headers can be colored according to your custom color palette.
* __Interface__: Featured Apps and All Apps buttons have been updated in the Apps tab. The Search button is now a floating action button.
* __Navigation__: All Apps shows a tabbed view of Featured, All and Categories for easier navigation.
* __Service__: My Devices and Contact IT tabs have improved readability.

You can find before and after images on the [UI updates page](whats-new-app-ui.md).

### Associate multiple management tools with the Microsoft Store for Business <!--926135-->
If you are using more than one management tool to deploy Microsoft Store for Business apps, previously, you could only associate one of these with the Microsoft Store for Business. You can now associate multiple management tools with the store, for example, Intune and Configuration Manager. For details, see [Manage apps you purchased from the Microsoft Store for Business with Microsoft Intune](../apps/windows-store-for-business.md).

## What's new in the public preview of Intune in the Azure portal <!--736542-->

In early calendar year 2017 we will be migrating our full admin experience onto Azure, allowing for powerful and integrated management of core EMS workflows on a modern service platform that's extensible using Graph APIs.

New trial tenants will start to see the public preview of the new admin experience in the Azure portal this month. While in preview state, capabilities and parity with the existing Intune console will be delivered iteratively.

The admin experience in the Azure portal will use the already announced new grouping and targeting functionality; when your existing tenant is migrated to the new grouping experience you will also be migrated to preview the new admin experience on your tenant. In the meantime, if you want to test or look at any of the new functionality until your tenant is migrated, sign up for a new Intune trial account or take a look at the [new documentation](whats-new.md).

You can find what's new in the Intune preview in Azure [here](whats-new.md).

## January 2017

### New Capabilities

#### In-console reports for MAM without enrollment <!--677961-->
New app protection reports have been added for both enrolled devices and devices that have not been enrolled. Find out more about how you can [monitor mobile app management policies with Intune](../apps/app-protection-policies-monitor.md).

#### Android 7.1.1 support <!--694397-->
Intune now fully supports and manages Android 7.1.1.

#### Resolve issue where iOS devices are inactive, or the admin console cannot communicate with them <!--unknown-->
When users' devices lose contact with Intune, you can give them new troubleshooting steps to help them regain access to company resources. See [Devices are inactive, or the admin console cannot communicate with them](/troubleshoot/mem/intune/troubleshoot-device-enrollment-in-intune#devices-are-inactive-or-the-admin-console-cant-communicate-with-them).

### Notices

#### Defaulting to managing Windows desktop devices through Windows settings <!--663050-->
The default behavior for enrolling Windows 10 desktops is changing. New enrollments will follow the typical MDM agent enrollment flow rather than through the PC agent.

The Company Portal website will provide Windows 10 desktop users with enrollment instructions that guide them through the process of adding Windows 10 desktop computers as mobile devices. This will not impact currently enrolled PCs, and your organization can still manage Windows 10 desktops using the PC agent [if you prefer](./intune-legacy-pc-client.md).

#### Improving mobile app management support for selective wipe <!--581242-->
End users will be given additional guidance on how to regain access to work or school data if that data is automatically removed due to the "Offline interval before app data is wiped" policy.<!--, or the removal of the Intune Company Portal on Android.-->

#### Company Portal for iOS links open inside the app <!--665954-->
Links inside of the Company Portal app for iOS, including those to documentation and apps, will open directly in the Company Portal app using an in-app view of Safari. This update will ship separately from the service update in January.

#### Modernizing the Company Portal website <!--753980-->
Beginning in February, the Company Portal website will support apps that are targeted to users who do not have managed devices. The website will align with other Microsoft products and services by using a new contrasting color scheme, dynamic illustrations, and a "hamburger menu," ![Company Portal website hamburger menu](./media/whats-new-archive-classic/CP_hamburger_menu.png).

#### New documentation for app protection policies <!--583398-->
We have updated our documentation for admins and app developers who want to enable app protection policies (known as MAM policies) in their iOS and Android apps using the Intune App Wrapping Tool or Intune App SDK.

The following articles have been updated:

* [Decide how to prepare apps for mobile application management with Microsoft Intune](../developer/apps-prepare-mobile-application-management.md)
* [Prepare iOS apps for mobile application management with the Intune App Wrapping Tool](../developer/app-wrapper-prepare-ios.md)
* [Get started with the Microsoft Intune App SDK](../developer/app-sdk-get-started.md)
* [Intune App SDK for iOS developer guide](../developer/app-sdk-ios.md)

The following articles are new additions to the docs library:

* [Intune App SDK Cordova Plugin](../developer/app-sdk.md)
* [Intune App SDK Xamarin Component](../developer/app-sdk-xamarin.md)

#### Progress bar when launching the Company Portal on iOS <!--665978-->
The Company Portal for iOS is introducing a progress bar on the launch screen to provide the user with information about the loading processes that occur. There will be a phased rollout of the progress bar to replace the spinner. This means that some of your users will see the new progress bar while others will continue to see the spinner.

## December 2016

### Public preview of Intune in the Azure portal<!--736542-->
In early calendar year 2017, we will be migrating our full admin experience onto Azure, allowing for powerful and integrated management of core EMS workflows on a modern service platform that's extensible using Graph APIs. In advance of the general availability of this portal for all Intune tenants, we're excited to announce that we will begin rolling out a preview of this new admin experience later this month to select tenants.

The admin experience in the Azure portal will use the already announced new grouping and targeting functionality; when your existing tenant is migrated to the new grouping experience you will also be migrated to preview the new admin experience on your tenant. In the meantime, find out more about what we have in store for Microsoft Intune in the Azure portal in our [new documentation](what-is-intune.md).

__Telecom expense management integration in public preview of Azure portal__ <!--747605-->
We are now beginning to preview integration with third-party telecom expense management (TEM) services within the Azure portal. You can use Intune to enforce limits on domestic and roaming data usage. We are beginning these integrations with [Saaswedo](http://www.saaswedo.com/). To enable this feature in your trial tenant, please [contact Microsoft support](../../get-support.md).

### New Capabilities

__Multi-factor authentication across all platforms__ <!--747590-->
You can now enforce multi-factor authentication (MFA) on a selected group of users when they enroll an iOS, Android, Windows 8.1+, or Windows Phone 8.1+ device from the Azure Management Portal by configuring MFA on the Microsoft Intune Enrollment application in Azure Active Directory.

__Ability to restrict mobile device enrollment__ <!--747596-->
Intune is adding new enrollment restrictions that control which mobile device platforms are allowed to enroll. Intune separates mobile device platforms as iOS, macOS, Android, Windows and Windows Mobile.
* Restricting mobile device enrollment does not restrict PC client enrollment.
* For iOS only, there is one additional option to block the enrollment of personally owned devices.

Intune marks all new devices as personal unless the IT admin takes action to mark them as corporate owned, as explained in [this article](../enrollment/device-enrollment.md).

### Notices

__Multi-Factor Authentication on Enrollment moving to the Azure portal__ <!--VSO 750545-->
Previously, admins would go to either the Intune console or the Configuration Manager (earlier than release October 2016) console to set MFA for Intune enrollments. With this updated feature, you will now login to the [Microsoft Azure portal](https://portal.azure.com) using your Intune credentials and configure MFA settings through Azure AD. Learn more about this [here](/azure/active-directory/authentication/howto-mfa-mfasettings).

__Company Portal app for Android now available in China__ <!--VSO 658093-->
We are publishing the Company Portal app for Android for download in China. Due to the absence of Google Play Store in China, Android devices must obtain apps from Chinese app marketplaces. The Company Portal app for Android will be available for download on the following stores:
* [Baidu](https://go.microsoft.com/fwlink/?linkid=836946)
* [Tencent](https://www.tencent.com/en-us/index.html)
* [Wandoujia](https://go.microsoft.com/fwlink/?linkid=836950)

The Company Portal app for Android uses Google Play Services to communicate with the Microsoft Intune service. Since Google Play Services are not yet available in China, performing any of the following tasks can take up to 8 hours to complete.

|Intune Admin Console| Intune Company Portal app for Android |Intune Company Portal Website|
|---|---|---|
|Full wipe| Remove a remote device| Remove device (local and remote)|
|Selective wipe| Reset device| Reset device|
|New or updated app deployments| Install available line-of-business apps| Device passcode reset|
|Remote lock|||
|Passcode reset|||

### Deprecations

__Firefox to no longer support Silverlight__ <!--VSO TBA-->
Mozilla is removing support for Silverlight in version 52 of the [Firefox browser](https://www.mozilla.org/firefox), effective March 2017. As a result, you will no longer be able to log in to the existing Intune console using Firefox versions greater than 51. We recommend using Internet Explorer 10 or 11 to access the admin console, or a [version of Firefox prior to version 52](https://ftp.mozilla.org/pub/firefox/releases/). Intune's transition to the Azure portal will allow it to support a number of [modern browsers](/azure/azure-preview-portal-supported-browsers-devices) without dependency on Silverlight.

__Removal of Exchange Online mobile inbox policies__ <!--770687-->
Beginning in December, admins will no longer be able to view or configure Exchange Online (EAS) mobile mailbox policies within the Intune console. This change will roll out to all Intune tenants over December and January. All existing policies will stay as configured; for configuring new policies, use the Exchange Management Shell. Find out more information [here](/exchange/mobile-device-mailbox-policies-exchange-2013-help).

__Intune AV Player, Image Viewer, and PDF Viewer apps are no longer supported on Android__ <!--747553-->
From mid-December 2016 on, users will no longer be able to use the Intune AV Player, Image Viewer, and PDF Viewer apps. These apps have been replaced with the Azure Information Protection app. Find out more about the Azure Information Protection app [here](/information-protection/rms-client/mobile-app-faq).

## November 2016

### New capabilities

__New Microsoft Intune Company Portal available for Windows 10 devices__
Microsoft has released a new [Microsoft Intune Company Portal app for Windows 10 devices](https://www.microsoft.com/store/apps/9wzdncrfj3pz). This app, which leverages the new Windows 10 Universal format, will provide the user with an updated user experience within the app and identical experiences across all Windows 10 devices, PC and Mobile alike, while still enabling all the same functionality that they are using today.

The new app will also allow users to leverage additional platform features like single sign-on (SSO) and certificate-based authentication on Windows 10 devices. The app will be made available as an upgrade to the existing Windows 8.1 Company Portal and Windows Phone 8.1 Company Portal installs from the Microsoft Store. For more details, go to [aka.ms/intunecp_universalapp](https://aka.ms/intunecp_universalapp).

> [!IMPORTANT]
> __An Update on Intune and Android for Work__
> While you can deploy Android for Work apps with an action of __Required__, you can only deploy apps as __Available__ if your Intune groups have been migrated to the new Azure AD groups experience.

__Intune App SDK for Cordova plugin now supports MAM without enrollment__
App developers can now use the Intune App SDK for Cordova plugin to enable MAM functionality without device enrollment in their Cordova-based apps for Android and iOS/iPadOS.

__Intune App SDK Xamarin component now supports MAM without enrollment__
App developers can now use the Intune App SDK Xamarin component to enable MAM functionality without device enrollment in their Xamarin-based apps for Android and iOS/iPadOS. The Intune App SDK Xamarin component can be found [here](https://www.npmjs.com/package/cordova-plugin-ms-intune-mam).

### Notices

__Symantec signing certificate no longer requires signed Windows Phone 8 Company Portal for upload__
Uploading the Symantec signing certificate will no longer require a signed Windows Phone 8 Company Portal app. The certificate can be uploaded independently.

### Deprecations

__Support for the Windows Phone 8 Company Portal__
Support for Windows Phone 8 Company Portal will now be deprecated. Support for the Windows Phone 8 and WinRT platforms was deprecated in October 2016. Support for the Windows 8 Company Portal was also deprecated in October 2016.


## See also
See [What's New in Microsoft Intune](whats-new.md) for details on recent developments.
