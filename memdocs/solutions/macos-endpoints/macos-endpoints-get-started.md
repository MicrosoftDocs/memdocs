---
# required metadata

title: Tutorial-Get started with macOS corporate endpoints
titleSuffix: Microsoft Intune
description: Set up secure macOS corporate endpoints that are enrolled in Intune, and then deploy at scale with Apple Business Manager or Apple School Manager.
keywords:
author: scottbreenmsft
  
ms.author: scbree
manager: 
ms.date: 01/16/2024
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: 
ms.localizationpriority: high
ms.technology:
ms.assetid: 
# optional metadata
 
#audience:
#ms.devlang:
ms.reviewer: scbree;rogerso
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
  - M365-identity-device-management
  - highpri
  - highseo
  - intune-scenario
---

# Tutorial: Get started with macOS corporate endpoints

This document guides you through the steps to create a macOS endpoint configuration for your organization for corporate or school-owned devices. This document focuses on devices enrolled through Apple Business Manager or Apple School Manager using Automated Device Enrollment with user affinity. User affinity is typically used for devices with one primary user. For more information on the different types of management and enrollment types for macOS, see [macOS device enrollment guide for Microsoft Intune](/mem/intune/fundamentals/deployment-guide-enrollment-macos).

## How to get started
Use the seven ordered phases in this guide, which build on each other to help you prepare your macOS endpoint configuration. By completing these phases in order, you see tangible progress and are ready to provision new devices.

Phases:  
- Phase 1 - Set up your environment.
- Phase 2 - Enroll a macOS endpoint.
- Phase 3 - Secure your macOS endpoint.
- Phase 4 - Apply organization specific customizations.
- Phase 5 - Optional advanced configuration.
- Phase 6 - Enroll your devices.
- Phase 7 - Support and reporting.

At the end of this guide, you have a macOS endpoint enrolled into Intune ready to start validating in your environment.

## Phase 1 - Set up your environment

Before you build your first macOS endpoint, there are some key requirements and configuration that need to be checked. This phase walks you through checking the requirements, configuring integration with Apple Business Manager, and creating some settings and applications.

### Step 1 - Network requirements

To successfully deploy/provision you macOS endpoint, it requires access to several public internet services. Start your testing on an open network, or use your corporate network after providing access to all the endpoints that are listed at [Network endpoints for Microsoft Intune](/mem/intune/fundamentals/intune-endpoints).

If your wireless network requires certificates, you can start with an Ethernet connection during testing while you determine the best approach for wireless connections for device provisioning.

### Step 2 - Enrollment and Licensing

Before you enroll in Intune, there are a few things you need to check. You could create a new Microsoft Entra ID group, such as the name Intune MDM Users. Then, add specific test user accounts and target each of the following configurations at that group to limit who can enroll devices while you set up your configuration. To create an Microsoft Entra ID group, see [Create a basic group and add members](/azure/active-directory/fundamentals/active-directory-groups-create-azure-portal).

 - **Enrollment Restrictions**

   Enrollment restrictions allow you to control what types of devices can enroll into management with Intune. For this guide to be successful, make sure macOS (MDM) enrollment is allowed, which is the default configuration.

   For information on configuring Enrollment Restrictions, see [Set enrollment restrictions in Microsoft Intune](/mem/intune/enrollment/enrollment-restrictions-set).

- **Licensing**
  
  Users enrolling macOS devices require a Microsoft Intune or Microsoft Intune for Education license.
  
  To assign licenses, go to [Assign Microsoft Intune licenses](/mem/intune/fundamentals/licenses-assign).

  > [!NOTE]
  > Both types of licenses are typically included with licensing bundles, like Microsoft 365 E3 (or A3) and higher. For more information, see [Compare Microsoft 365 Enterprise Plans](https://www.microsoft.com/microsoft-365/compare-microsoft-365-enterprise-plans).

### Step 3 - Add Apple MDM Certificate

To manage macOS devices, Apple requires a tenant be configured with an MDM push certificate. If you manage iOS devices already, this step is likely already completed. For information on configurating an Apple MDM push certificate, see [Get an Apple MDM Push certificate for Intune](/mem/intune/enrollment/apple-mdm-push-certificate-get).

>[!NOTE]
>Avoid using a personal Apple ID for this process as management of the Apple Push Notification Service certificate will be critical over the life of your device management solution and access via a personal Apple ID may become unavailable as staff change over time. Using a Managed Apple ID keeps control within the Apple Business Manager (or Apple School Manager) instance.

### Step 4 - Apple Automated Device Enrollment (corporate devices)

To manage devices enrolled through Apple Business (or School) manager, you need to set up an MDM token and link it with Intune. For information on configuring Apple Business Manager with Intune, see [Enroll macOS devices - Apple Business Manager or Apple School Manager](/mem/intune/enrollment/device-enrollment-program-enroll-macos).

High-level steps:

1. Connect Intune to Apple Business Manager.
2. Create enrollment profiles in Intune for the ABM token.
3. Assign devices in ABM to Intune MDM.
4. Assign devices to profiles in Intune.

### Step 5 - Targeting devices

In Intune, you may need to target particular groups of macOS devices. There are two common options for how customers dynamically group macOS devices.

 - **Option 1 – Microsoft Entra ID dynamic group based enrollmentProfileName**

   To limit the configurations from this guide to the test devices that you import through Apple Business Manager, create a dynamic Microsoft Entra ID group. This example creates a group that includes all devices enrolled with the profile "_macOS corporate_". You can then target all your configurations and applications at this group.
   
   1. Open the **Microsoft Intune admin center**.
   2. Select **Groups**.
   3. Select **New Group** and enter the following details:

      1. **Group type:** Security
      2. **Group Name:** macOS Endpoints
      3. **Membership type:** Dynamic Device
   4. Select **Add dynamic query**.
      - Select enrollment profile name, equals, enter your enrollment profile name
   5. Select **OK** > **Save** > **Create**.
   6. Now when creating profiles, policies and apps, you can target them at this new Microsoft Entra ID group.

   >[!NOTE]
   >Dynamic groups take a few minutes to populate after changes occur. In large organizations, it [can take much longer](/azure/active-directory/enterprise-users/groups-troubleshooting#troubleshooting-dynamic-memberships-for-groups). After creating a new group, wait a few minutes before you check to confirm the device is now a member of the group.
   >
   >For more information about dynamic groups for devices, see [Rules for devices](/azure/active-directory/enterprise-users/groups-dynamic-membership#rules-for-devices).

-  **Option 2 - All devices with a filter enrollmentProfileName**
  
   For profiles and apps that are critical to the apply immediately after enrollment like security settings, restrictions, and the company portal app – you might choose to assign to All Devices with a filter. Profiles and apps targeted at All Devices apply faster after enrollment than dynamic groups, however not all configuration profiles (like macOS scripts) support filters.
   
   For more information on filters, see [Create filters in Microsoft Intune](/mem/intune/fundamentals/filters).

### Step 6 - Configure settings for an optimal Microsoft 365 Experience

These settings demonstrate an optimal Microsoft 365 end-user experience on your macOS device. These settings are configured using a device configuration settings catalog profile. For more information, see [Create a policy using the settings catalog in Microsoft Intune](/mem/intune/configuration/settings-catalog).

The Microsoft Enterprise SSO plug-in provides single sign-on (SSO) to apps and websites that use Microsoft Entra ID for authentication, including Microsoft 365. For more information on the SSO extension, see [Configure macOS Enterprise SSO plug-in with MDM](/mem/intune/configuration/use-enterprise-sso-plug-in-macos-with-intune).  You can configure the SSO extension using these settings:

- Authentication > Extensible Single Sign On (SSO)
   
   |Name|Configuiration|
   |--|--|
   |Type|Redirect|
   |Extension Identifier|com.microsoft.CompanyPortalMac.ssoextension|
   |Team ID|UBF8T346G9|
   |URLs|https://login.microsoftonline.com<br>https://login.microsoft.com<br>https://sts.windows.net<br>   https://login.partner.microsoftonline.cn<br>https://login.chinacloudapi.cn<br>https://login.microsoftonline.us<br>https://login-us.microsoftonline.com|
   |

    - There are also some optional settings that can be configured under the **Additional configuration** setting:

    |Key|Type|Value|
    |---|---|---|
    |browser_sso_interaction_enabled|Integer|1|
    |disable_explicit_app_prompt|Integer|1|
    |AppPrefixAllowList|String|com.microsoft.,com.apple.|

>[!NOTE]
>Microsoft will soon be releasing support for [Platform SSO](https://support.apple.com/en-gb/guide/deployment/dep7bbb05313/web). Check [Intune What’s New](/mem/intune/fundamentals/whats-new) for the settings required once it’s released. For more information, see [Coming Soon – Platform SSO for macOS](https://techcommunity.microsoft.com/t5/microsoft-entra-blog/coming-soon-platform-sso-for-macos/ba-p/3902280).

You can configure these settings to reduce the number of prompts a user receives when using Microsoft apps:
- Microsoft Office > Microsoft Office
   
   These settings streamline the sign in process when opening Office apps for the first time. For more information on these setting, see Set suite-wide preferences for Office for Mac.
   - **Enable automatic sign-in:** Enabled.
   - **Office Activation Email Address:** {{userprincipalname}}

- Microsoft AutoUpdate
   - **Enable AutoUpdate:** Enabled.
   
      This setting forces Microsoft AutoUpdate to on. For more information about Microsoft AutoUpdate, which updates Microsoft 365 Apps and Company Portal, see [Deploy updates for Office for Mac](/deployoffice/mac/deploy-updates-for-office-for-mac).
   - **Automatically acknowledge data collection policy:** Acknowledge – send required and optional data.
   
      For more information about this setting, see [Use preferences to manage privacy controls for Office for Mac](/deployoffice/privacy/mac-privacy-preferences#preference-setting-for-the-required-data-notice-dialog-for-microsoft-autoupdate)

### Step 7 - Create and assign some applications
 - **Company Portal**
    
    Deploying the Intune Company Portal app to all devices as a required application is recommended. Company Portal app is the self-service hub for users that they use to install applications. Users also use the Company Portal app to sync their device with Intune, check compliance status, and so on.

    To deploy Company Portal as required, see [Add the Company Portal for macOS app](/mem/intune/apps/apps-company-portal-macos).

- **Microsoft 365 Apps**
   Microsoft 365 Apps such as Word, Excel, OneDrive and Outlook can easily be deployed to devices using the built-in Microsoft 365 apps for macOS app profile in Intune.

   To deploy Microsoft 365 Apps, see [Deploying Microsoft 365 Apps for Mac with Microsoft Endpoint Manager - A Deep Dive](https://techcommunity.microsoft.com/t5/intune-customer-success/deploying-microsoft-365-apps-for-mac-with-microsoft-endpoint/ba-p/2243040).

## Phase 2 - Enroll a macOS endpoint

To enroll your first corporate macOS endpoint. Start by checking the macOS endpoint is:
> [!div class="checklist"]
> * [Registered in Apple Business Manager and assigned to the Intune MDM](https://support.apple.com/en-gb/guide/apple-business-manager/axmf500c0851/web), and;
> * [Assigned to an enrollment profile in Intune](/mem/intune/enrollment/device-enrollment-program-enroll-macos#assign-an-enrollment-profile-to-devices).

Follow these steps to enroll your first macOS endpoint:
1. Erase or reset the macOS endpoint.
2. Go through setup assistant.
3. Open Company Portal and sign in.
4. Your test macOS endpoint is enrolled into Intune.

## Phase 3 - Secure your macOS endpoint

This phase is designed to help you build out security settings for your organization. This section draws your attention to the various Endpoint Security components in Microsoft Intune including:
- Compliance policies.
- Defender for Endpoint.
- Endpoint Security - FileVault.
- Endpoint Security - Firewall.
- macOS Software Updates.
- Accounts configuration.
- Idle Login Configuration.
- Mac Evaluation Utility.

### Compliance policies
Conditional access rules can be used to secure your environment. Using a combination of Compliance Policies and conditional access rules end users can be required to enroll their devices and meet a minimum security standard before accessing services protected by conditional access. For more information on Conditional Access, see [What is Conditional Access in Microsoft Entra ID?](/entra/identity/conditional-access/overview).

Compliance policies in Intune both verify and attempt to remediate the required configuration. If you have configuration that conflicts between compliance policies and other policies, then the compliance policy takes precedence. For more information, see [Compliance and device configuration policies that conflict](/mem/intune/configuration/device-profile-troubleshoot#compliance-and-device-configuration-policies-that-conflict). 

Compliance policies are configured in Intune under **Devices** > **Compliance policies**.

### Defender for Endpoint
Follow the steps in [Deploy Microsoft Defender for Endpoint on macOS with Microsoft Intune](/microsoft-365/security/defender-endpoint/mac-install-with-intune) to configure Defender for Endpoint using Intune.

### Endpoint Security - FileVault

Follow the steps in [Encrypt macOS devices with FileVault disk encryption with Intune](/mem/intune/protect/encrypt-devices-filevault) to configure FileVault with Intune using settings catalog.

### Endpoint Security - Firewall
macOS has a built-in firewall that can be configured using Intune. For more information about the macOS firewall, go to [Change Firewall settings on Mac](https://support.apple.com/guide/mac-help/mh11783/mac).

Firewall settings for macOS can be configured in **Intune Admin Console** > **Endpoint Security** > **Firewall**.

### Gatekeeper
macOS includes a security technology called Gatekeeper, which is designed to help ensure that only trusted software runs on a user’s Mac. For more information about Gatekeeper, go to Apple’s website [Gatekeeper and runtime protection in macOS](https://support.apple.com/guide/security/sec5599b66df/web). Gatekeeper can be configured in macOS [settings catalog](/mem/intune/configuration/settings-catalog). 

The settings are located under:
- System Policy > System Policy Control
   - **Allow Identified Developer:** True
   - **Enable Assessment:** True
- System Policy > System Policy Managed
   - **Disable Override:** True

### Software Updates

Software Updates on macOS endpoints managed by Intune can be installed:
- Manually by end users;
- Using [declarative software updates](/mem/intune/protect/software-updates-declarative-ios-macos), or;
- Using a [Software Update policy](/mem/intune/protect/software-updates-macos).

Settings for the Software Update client on macOS can be configured using settings catalog:
- Software Update

   Using these settings you can enforce and restrict the behavior of the Software Update node in the Settings app
   - Automatic Check Enabled
   - Critical Updates Install
   - Automatically Install App Updates
   - Restrict Software Require Admin To Install
   - Config Data Install
   - Automatic Download

- Restrictions

   Using these restrictions you can delay how long after an update is released that a user can install them manually.
   - Enforced Software Update Minor OS Deferred Install Delay: 0-30
   - Enforced Software Update Major OS Deferred Install Delay: 0-30
   - Enforced Software Update Non OS Deferred Install Delay: 0-30

### Accounts configuration
You can disable guest account usage with settings catalog:
- Accounts > Accounts
   - **Disable Guest Account:** Enabled

### Idle Login Configuration
It's possible to control the period of time after idle that macOS prompts for a password using settings under the Screensaver category. 

>[!NOTE]
>To find the module name of a screensaver, set the screensaver and then run this command from Terminal:
>
> defaults -currentHost read com.apple.screensaver

These settings are available in settings catalog:
- System Configuration > Screensaver
   - **Module Name:**
      - For example, "Flurry"
   - **Ask for Password Delay:**
      - For example: 5
   - **Login Windows Idle Time:**
      - For example: 600
   - **Ask for Password:** 
      - Enabled
- User Experience > Screensaver User
   - **Module Name:** 
      - For example, "Flurry"
   - **Idle Time:** 
      - For example, 600

### macOS Evaluation Utility
You can use the Mac Evaluation Utility to confirm that your Mac has configuration and settings suggested by Apple configured. You can access the Mac Evaluation Utility from [Apple Seed for IT](https://beta.apple.com/it) under **Resources**.

## Phase 4 - Apply organization specific customizations 

In this phase, you apply organization-specific settings, apps, and review your on-premises configuration. The phase helps you build any customizations specific to your organization. Notice the various components of macOS. There are sections for each of the following areas:
 - Apps
 - Microsoft Edge
 - Microsoft OneDrive
 - Device Configuration
 - Notifications
 - Wallpaper
 - Dock Configuration
 - Device name
 - Certificates
 - Wi-Fi
 - Custom profiles and preference files

### Line of business applications
Intune supports the deployment of:
- [PKG via the MDM channel](/mem/intune/apps/lob-apps-macos);
- [PKG via the Intune Management Extension (including unsigned packages and packages without a payload)](/mem/intune/apps/macos-unmanaged-pkg);
- [DMG](/mem/intune/apps/lob-apps-macos-dmg), and; 
- [VPP apps](/mem/intune/apps/vpp-apps-ios).

### Microsoft Edge
You can deploy Microsoft Edge to macOS endpoints using the built-in deployment type. For more information, see [Add Microsoft Edge to macOS devices using Microsoft Intune](/mem/intune/apps/apps-edge-macos).

### Microsoft OneDrive
Microsoft OneDrive is installed with Microsoft 365 apps earlier in Phase 1. If necessary, you can also deploy it separately using a [downloaded PKG or via VPP](/sharepoint/deploy-and-configure-on-macos).

[Settings for OneDrive](/sharepoint/deploy-and-configure-on-macos) can be configured using [settings catalog](/mem/intune/configuration/settings-catalog). As an example, these are some settings that may be applicable to your organization:
- Microsoft Office > OneDrive
   - **Automatically and silently enable the Folder Backup feature (Known Folder Move):** \<your Microsoft Entra ID tenant ID>
   - **Enable Files On-Demand:** True
   - **Open at login:** True
- App Management > NS Extension Management
   - **Allowed Extensions:** com.microsoft.OneDrive.FinderSync

>[!NOTE]
>If you are deploying the VPP version of OneDrive this will be com.microsoft.OneDrive-Mac.FinderSync

During configuration by the end user, the user is prompted to allow sync icons by enabling the Finder Sync extension. A script can be used to configure the finder extension on behalf of the user. There's a sample script on the [Intune Shell Samples GitHub site](https://github.com/microsoft/shell-intune-samples/blob/master/macOS/Config/EnableOneDriveFinderSync/EnableOneDriveFinderSync.sh).

### Device Configuration
The settings catalog is a single location where all configurable macOS settings are listed. This feature simplifies how you create a policy, and how you see all the available settings. For more information, see [Create a policy using the settings catalog in Microsoft Intune](/mem/intune/configuration/settings-catalog).

Examples of settings catalog categories that might be useful are:
- Microsoft Edge browser settings
- Microsoft AutoUpdate
- Microsoft Office
- Software Updates
- User Experience

### Notifications
You can control notification prompts using MDM. You can find the settings for notifications in settings catalog under:
- User Experience > Notifications > Notification Settings
   - You should enter the bundle ID for each application you want to control notifications for.

For more information, see [Notifications MDM payload settings for Apple devices](https://support.apple.com/guide/deployment/dep46b6547ba/web). 

### Wallpaper
You can enforce a wallpaper on macOS using a combination of a sample script and settings catalog:
- User Experience > Desktop
   - Override Picture Path: \<path>

The file must exist on the macOS endpoint. There's a sample script you can use to download a picture from a web location - [shell-intune-samples/macOS/Config/Wallpaper at master · microsoft/shell-intune-samples](https://github.com/microsoft/shell-intune-samples/tree/master/macOS/Config/Wallpaper). You can also use a package tool to copy a file and then deploy it using the [unmanaged PKG](/mem/intune/apps/macos-unmanaged-pkg) deployment capability.

### Dock configuration
Items can be added and removed from the dock using [example scripts](https://github.com/microsoft/shell-intune-samples/tree/master/macOS/Config/Dock) or third-party command line tools like [DockUtil](https://github.com/kcrawford/dockutil).

### Certificates
Intune supports deploying certificates. For more information, see [Learn about the types of certificate that are supported by Microsoft Intune](/mem/intune/protect/certificates-configure).

### Wi-Fi
Intune supports deploying Wi-Fi profiles. See [Configure Wi-Fi settings for macOS devices in Microsoft Intune](/mem/intune/configuration/wi-fi-settings-macos).

### Custom profiles and preference files
Most settings required are available in [settings catalog](/mem/intune/configuration/settings-catalog), however if necessary Intune also supports deploying [custom profiles](/mem/intune/configuration/custom-settings-macos) and [preference files (plist)](/mem/intune/configuration/preference-file-settings-macos).

## Phase 5 - Optional Advanced Configuration
### Content Caching
If you have a large number of macOS or iOS devices on your network, you may choose to deploy Apple Content Cache as a way to reduce your internet bandwidth. Apple Content Cache can cache content that is hosted on Apple services like Software Updates and VPP apps. For more information, see [Intro to content caching](https://support.apple.com/guide/deployment/depde72e125f/web).

### AutoUpdate local cache
Many Microsoft apps on macOS are updated using the Microsoft Autoupdate application. This application can be configured to reference a different URL for content. There's a project on GitHub that helps you configure this approach if it's relevant for your environment. For more information, see the third party open source tool at [Microsoft AutoUpdate Cache Admin](https://github.com/pbowden-msft/MAUCacheAdmin).

## Phase 6 - Enroll your devices
macOS endpoints can now be enrolled into Intune. For more information, see [distribute devices](/mem/intune/enrollment/device-enrollment-program-enroll-macos#distribute-devices).

## Support and Troubleshooting
macOS devices are managed through Intune by using a combination of the built-in operating system MDM capabilities and an agent installed by Intune called the Intune Management Extension (IME). These two components offer separate functionality and communicate with the macOS device through different channels. Enrollment is orchestrated through Apple Business Manager, MDM is orchestrated through the Apple Push Notification Service and the IME communicates directly with Intune. 

:::image type="content" source="../media/macos-endpoints/macos-endpoint-ime-architecture.png" alt-text="A visual representation of how MDM and the Intune Managemnt Extension work together to support managemetn of macOS devices":::
 
For more information about the Intune Management Extension, see [Understanding Microsoft Intune management agent for macOS](/mem/intune/apps/lob-apps-macos-agent).

### macOS Enrollment Maintenance
For your Mac devices to maintain their connection to Intune and continue enrolling there are several important areas you should check in the console periodically and action as necessary:
- **Apple Push Notification Service certificate expiry**.
   
   Apple’s Push Notification Service certificate needs to be renewed yearly. When this certificate expires, Intune can't manage devices that enrolled via that certificate. It’s important to ensure this certificate is renewed each year. For more information, see [Get an Apple MDM Push certificate for Intune](/mem/intune/enrollment/apple-mdm-push-certificate-get#renew-apple-mdm-push-certificate).

- **Apple Automated Device Enrollment certificate expiry**
   
   When you set up a connection between Apple Business (or School) Manager and Intune there's a certificate that is used. This certificate needs to be renewed yearly. If this certificate isn't renewed, changes from Apple Business (or School) Manager won't sync to Intune. For more information, see [Enroll macOS devices - Apple Business Manager or Apple School Manager](/mem/intune/enrollment/device-enrollment-program-enroll-macos#renew-enrollment-program-token).

- **Apple Automated Device Enrollment sync status**
   
   Apple suspends syncing of ADE tokens when the terms and conditions are changed in Apple Business (or School) Manager. These typically occur after a major OS release but can happen anytime. You should monitor the sync status to ensure there are no problems that require attention. For more information, see [sync managed devices](/mem/intune/enrollment/device-enrollment-program-enroll-macos#sync-managed-devices).

### Remote Help
Remote Help is a cloud-based solution for secure help desk connections with role-based access controls. With the connection, your support staff can remote connect to the user's device.
For more information, see [Using Remote Help on macOS to assist authenticated users](/mem/intune/fundamentals/remote-help-macos).

### Custom attributes
You can create custom attribute profiles which enable you to collect custom properties from managed macOS device using shell scripts. For more information, see [Use shell scripts on macOS devices in Microsoft Intune](/mem/intune/apps/macos-shell-scripts#custom-attributes-for-macos).
