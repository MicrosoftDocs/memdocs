---
# required metadata

title: Tutorial-Get started with macOS corporate endpoints
titleSuffix: Microsoft Intune
description: Set up secure macOS corporate organization-owned endpoints that are enrolled in Intune, and then deploy at scale with Apple Business Manager or Apple School Manager.
keywords:
author: MandiOhlinger
  
ms.author: mandia
manager: 
ms.date: 01/24/2024
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

# End-to-end guide to get started with macOS endpoints

This article guides you through the steps to create a macOS endpoint configuration for your organization for corporate or school-owned devices.

It focuses on devices enrolled through Apple Business Manager or Apple School Manager using Automated Device Enrollment with user affinity. User affinity is typically used for devices with one primary user.

For more information on the different types of management and enrollment types for macOS, go to [macOS device enrollment guide for Microsoft Intune](../../intune/fundamentals/deployment-guide-enrollment-macos.md).

## How to get started

This guide has seven phases. Each phase has a set of steps to help you build your macOS endpoint configuration. The steps are designed to be completed in order. You can skip steps if you've already completed them.

The phases include:

- [Phase 1 - Set up your environment](#phase-1---set-up-your-environment)
- [Phase 2 - Pre-enrollment tasks](#phase-2---pre-enrollment-tasks)
- [Phase 3 - Secure your macOS endpoint](#phase-3---secure-your-macos-endpoints)
- [Phase 4 - Apply organization specific customizations](#phase-4---apply-organization-specific-customizations)
- [Phase 5 - Optional advanced configuration](#phase-5---optional-advanced-configuration)
- [Phase 6 - Enroll your devices](#phase-6---enroll-your-devices)
- [Phase 7 - Support and reporting](#phase-7---support-and-reporting)

At the end of this guide, you have a macOS endpoint enrolled into Intune and ready to start validating in your environment.

## Phase 1 - Set up your environment

Before you build your first macOS endpoint, there are some requirements and configuration features that should be configured. This phase walks you through checking the requirements, configuring integration with Apple Business Manager, configuring some features, and deploying some apps.

### Step 1 - Network requirements

✅ Set up your network

To successfully provision and deploy you macOS endpoint, the endpoint requires access to several public Internet services.

- Start your testing on an open network. Or, in your organization network, provide access to all the endpoints listed at [Network endpoints for Microsoft Intune](../../intune/fundamentals/intune-endpoints.md). Then, you can use your organization network to test your configuration.

- If your wireless network requires certificates, you can start with an Ethernet connection during testing. The Ethernet connection gives you some time to determine the best approach for wireless connections that devices need for provisioning.

### Step 2 - Enrollment and licensing

✅ Create a new group, configure enrollment restrictions, and assign licenses

To get the endpoints ready for enrollment, you need to make sure the correct endpoints are affected, your endpoints enroll successfully, and that the endpoints are licensed correctly. 

Specifically:

- **Create a new group**

  Create a new Microsoft Entra test group, like **Intune MDM Users**. Then, add test user accounts to this group. To limit who can enroll devices while you set up your configuration, target the configurations to this group.

  To create a Microsoft Entra group, you can use the Intune admin center or the Microsoft Entra admin center. When you create a group in Intune, you are creating an Entra group. You don't see the Entra branding, but that's what you're using. For more information, go to:

  - [Create a group to manage users in Intune](../../intune/fundamentals/quickstart-create-group.md)
  - [Quickstart: Create a group with members and view all groups & members in Entra ID](/entra/fundamentals/groups-view-azure-portal)

  ?? Since this is an Intune article, my preference is to NOT direct users to the Azure portal. If agreed, I'll remove the Entra info. ??

- **Enrollment Restrictions**

  Enrollment restrictions allow you to control the types of devices that can enroll into Intune management. For this guide to be successful, make sure macOS (MDM) enrollment is allowed, which is the default configuration. Assign your enrollment restrictions to the new group you created.

  For information on configuring Enrollment Restrictions, go to [Set enrollment restrictions in Microsoft Intune](../../intune/enrollment/enrollment-restrictions-set.md).

- **Licensing**
  
  Users enrolling macOS devices require a Microsoft Intune or Microsoft Intune for Education license. To assign licenses, go to [Assign Microsoft Intune licenses](../../intune/fundamentals/licenses-assign.md). Assign the licenses to the test accounts you created.

  > [!NOTE]
  > Both types of licenses are typically included with licensing bundles, like Microsoft 365 E3 (or A3) and higher. For more information, go to [Compare Microsoft 365 Enterprise Plans](https://www.microsoft.com/microsoft-365/compare-microsoft-365-enterprise-plans).

### Step 3 - Add Apple MDM Certificate

✅ Add the push certificate with a Managed Apple ID

- To manage macOS devices, Apple requires the Intune tenant be configured with an MDM push certificate. If you currently manage iOS/iPadOS devices in this same tenant, then this step is done.

- Use a Managed Apple ID with the Apple Business Manager (or Apple School Manager) instance.

  **Don't use a personal Apple ID**. Management of the Apple Push Notification Service certificate is critical over the life of your device management solution. Access with a personal Apple ID can become unavailable, as staff does change over time.

For information on configurating an Apple MDM push certificate, go to [Get an Apple MDM Push certificate for Intune](../../intune/enrollment/apple-mdm-push-certificate-get.md).

### Step 4 - Add the Apple automated device enrollment token

✅ Link Apple token for Automated Device Enrollment

To manage devices enrolled through Apple Business Manager (or Apple School Manager), you need to set up an MDM token and link the token with Intune.

This token is required for Automated Device Enrollment (ADE) in Intune. The token:

- Lets Intune sync ADE device information from your Apple Business Manager (or Apple School Manager account).
- Allows Intune to upload enrollment profiles to Apple.
- Allows Intune to assign devices to those profiles.

If you currently manage iOS/iPadOS devices in this same tenant using ADE, then this step is done.

For information on configuring Apple Business Manager with Intune, go to [Enroll macOS devices - Apple Business Manager or Apple School Manager](../../intune/enrollment/device-enrollment-program-enroll-macos.md).

The high-level steps to configure Apple Business Manager (or Apple School Manager) with Intune are:

1. Connect Intune to Apple Business Manager (or Apple School Manager).
2. In Intune, create ADE profiles for the Apple Business Manager token.
3. In Apple Business Manager, assign devices to your Intune MDM.
4. In Intune, assign the ADE profiles to your devices.

### Step 5 - Target devices

✅ Target specific groups using dynamic groups or Intune filters

In Intune, you might need to target specific groups of macOS devices. There are two common options for how customers dynamically group macOS devices:

- **Option 1 – Microsoft Entra dynamic group based on enrollmentProfileName**

  To limit the configurations from this guide to the test devices that you import through Apple Business Manager, create a dynamic Microsoft Entra group. This example creates a group that includes all devices enrolled with the profile *macOS corporate*. You can then target all your configurations and applications at this group.

  1. Open the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
  2. Select **Groups** > **New Group**, and enter the following details:

      - **Group type**: Select **Security**.
      - **Group Name**: Enter **macOS Endpoints**.
      - **Membership type**: Select **Dynamic Device**.

  3. Select **Add dynamic query**.
      - Select enrollment profile name, equals, enter your enrollment profile name

      ?? ADD SCREENSHOT ??

  4. Select **OK** > **Save** > **Create**.

  Now when creating apps and policies, you can target the policies to this new dynamic Microsoft Entra group.

   > [!NOTE]
   > After changes occur, Dynamic groups can take several minutes to populate. In large organizations, it [can take longer](/entra/identity/users/groups-troubleshooting#troubleshooting-dynamic-memberships-for-groups). After creating a new group, wait several minutes before you check if the device is a member of the group.
   >
   > For more information about dynamic groups for devices, go to [Dynamic membership rules for groups in Microsoft Entra ID: Rules for devices](/entra/identity/users/groups-dynamic-membership#rules-for-devices).

- **Option 2 - All devices group with an assignment filter on enrollmentProfileName**
  
  For critical apps and policies that must apply immediately after enrollment (security settings, restrictions, the Company Portal app), you can assign the policies to the built-in Intune **All Devices** group with an assignment filter.

  Policies and apps targeted to the **All Devices** group apply faster after enrollment than dynamic groups. Not all configuration profiles (like macOS scripts) support filters.

  For more information on assignment filters, go to [Create filters in Microsoft Intune](../../intune/fundamentals/filters.md).

### Step 6 - Use single sign-on (SSO)

✅ Reduce sign-in prompts with SSO

In Intune, you can configure settings that reduce the number of sign-in prompts end users receive when using apps, including Microsoft 365 apps. There are two parts to this configuration:

- **Part 1** - Use the [Microsoft Enterprise SSO plug-in](../../intune/configuration/use-enterprise-sso-plug-in-macos-with-intune.md) to provide single sign-on (SSO) to apps and websites that use Microsoft Entra ID for authentication, including Microsoft 365 apps. This plug-in uses an Intune device configuration policy.

  In the policy, you:

  - Enter the app bundle IDs that you want to enable SSO for.

  - Configure the following optional settings:

    | Key | Type | Value |
    |---|---|---|
    | AppPrefixAllowList | String | `com.microsoft.,com.apple.` |
    | browser_sso_interaction_enabled | Integer | 1 |
    | disable_explicit_app_prompt | Integer | 1 |

  For more information on the Enterprise SSO plug-in, including how to create the policy, go to [Configure macOS Enterprise SSO plug-in with Intune](../../intune/configuration/use-enterprise-sso-plug-in-macos-with-intune.md).

- **Part 2** - Use the [Intune settings catalog](../../intune/configuration/settings-catalog.md) to configure other settings that reduce sign-in prompts, including Microsoft AutoUpdate (MAU) and Microsoft Office.

  - **Authentication** > **Extensible Single Sign On (SSO)**: Add and configure the following settings:

    | Name | Configuration |
    |---|---|
    | Extension Identifier | `com.microsoft.CompanyPortalMac.ssoextension`|
    | Team Identifier | `UBF8T346G9` |
    | Type | Redirect |
    | URLs | `https://login.microsoftonline.com` <br/> `https://login.microsoft.com` <br/> `https://sts.windows.net` <br/> `https://login.partner.microsoftonline.cn` <br/> `https://login.chinacloudapi.cn` <br/> `https://login.microsoftonline.us` <br/> `https://login-us.microsoftonline.com` |

  - **Microsoft AutoUpdate (MAU)**: Add and configure the following settings:

    - **Automatically acknowledge data collection policy**: Select **Acknowledge – send required and optional data**.

      For more information about this setting, go to [Use preferences to manage privacy controls for Office for Mac](/deployoffice/privacy/mac-privacy-preferences#preference-setting-for-the-required-data-notice-dialog-for-microsoft-autoupdate)

    - **Enable AutoUpdate**: Select **True**.

      This setting forces Microsoft AutoUpdate to on. For more information about Microsoft AutoUpdate, which updates Microsoft 365 Apps and Company Portal, go to [Deploy updates for Office for Mac](/deployoffice/mac/deploy-updates-for-office-for-mac).

  - **Microsoft Office** > **Microsoft Office**: Add and configure the following settings:

    - **Office Activation Email Address**: Enter `{{userprincipalname}}`.
    - **Enable automatic sign-in**: Select **True**.

    These settings streamline the sign in process when opening Office apps for the first time. For more information on these setting, go to Set suite-wide preferences for Office for Mac.

  For more information on the settings catalog, including how to create a policy, go to [Use the settings catalog to configure settings in Microsoft Intune](../../intune/configuration/settings-catalog.md).

> [!NOTE]
> Microsoft will be releasing support for [Platform SSO](https://support.apple.com/guide/deployment/dep7bbb05313/web) (opens Apple's website). When it's available, it will be announced in [Intune What's New](/mem/intune/fundamentals/whats-new). For more information on platform SSO, go to [Coming Soon – Platform SSO for macOS](https://techcommunity.microsoft.com/t5/microsoft-entra-blog/coming-soon-platform-sso-for-macos/ba-p/3902280).

### Step 7 - Create and assign some apps

- **Company Portal app**

  It's recommended to deploy the Intune Company Portal app to all devices as a required application. The Company Portal app is the self-service hub for users. In the Company Portal app, users can install apps, sync their device with Intune, check compliance status, and more.

  To deploy the Company Portal app as a required app, go to [Add the Company Portal for macOS app](../../intune/apps/apps-company-portal-macos.md).

- **Microsoft 365 Apps**

  Microsoft 365 apps, like Word, Excel, OneDrive and Outlook, can easily be deployed to devices using the built-in Microsoft 365 apps for macOS app profile in Intune.

  To deploy Microsoft 365 Apps, go to:

  - [Assign Microsoft 365 to macOS devices with Microsoft Intune](../../intune/apps/apps-add-office365-macos.md)
  - [Deploying Microsoft 365 Apps for Mac with Microsoft Intune - A Deep Dive](https://techcommunity.microsoft.com/t5/intune-customer-success/deploying-microsoft-365-apps-for-mac-with-microsoft-endpoint/ba-p/2243040)

## Phase 2 - Pre-enrollment tasks

To enroll your first organization macOS endpoint, make sure the macOS endpoint is:

> [!div class="checklist"]
>
> - [Registered in Apple Business Manager and assigned to your Intune MDM](https://support.apple.com/guide/apple-business-manager/axmf500c0851/web) (opens Apple's website)
> - [Assigned an enrollment profile in Intune](../../intune/enrollment/device-enrollment-program-enroll-macos.md#assign-an-enrollment-profile-to-devices)

The high-level steps to enroll your first macOS endpoint with Intune are:

1. Erase or reset the macOS endpoint. ?? Why? ??
2. Go through Setup Assistant.
3. Open the Company Portal app and sign in with your organization account (`user@contoso.com`).

When the user signs in, the enrollment policy apply in the background. When it comples, your macOS endpoint is enrolled in Intune.

## Phase 3 - Secure your macOS endpoints

In this phase, you build security settings for your organization. This section focuses on the different endpoint security features in Microsoft Intune, including:

- Compliance and Conditional Access policies
- Microsoft Defender for Endpoint
- Endpoint Security - FileVault
- Endpoint Security - Firewall
- macOS Software Updates
- Accounts configuration
- Idle Login Configuration
- Mac Evaluation Utility

### Compliance and Conditional Access policies

✅ Create compliance policies and enforce compliance with Conditional Access

- **Compliance policies** verify the device settings you configure and can remediate some settings that aren't compliant. For example, you can create compliance policies that check password complexity, jailbroken status, threat levels, enrollment status, and more.

  If there are configuration settings that conflict between compliance policies and other policies, then the compliance policy takes precedence. For more information, go to [Compliance and device configuration policies that conflict](../../intune/configuration/device-profile-troubleshoot.md#compliance-and-device-configuration-policies-that-conflict).

  **Conditional Access** can be used to enforce the compliance policies you create. When combined, end users can be required to enroll their devices and meet a minimum security standard before accessing organization resources. If a device is non-compliant, then you can block access to resources, like email, or require the user to enroll their device and fix the issue.

You can create compliance and Conditional Access policies in the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

For more information, go to:

- [Use compliance policies to set rules for devices you manage with Intune](../../intune/protect/device-compliance-get-started.md)
- [Conditional Access and Intune](../../intune/protect/conditional-access.md)
- [What is Conditional Access in Microsoft Entra ID?](/entra/identity/conditional-access/overview)

### Microsoft Defender for Endpoint

✅ Use Microsoft Defender for Endpoint for threat defense

Microsoft Defender for Endpoint is a mobile threat defense solution that helps protect your devices from security threats. 

In Intune, you can connect to your Microsoft Defender for Endpoint service, create Intune policies using Microsoft Defender for Endpoint settings, and then deploy the policies to your devices.

For more information, go to:

- [Configure Microsoft Defender for Endpoint in Intune](../../intune/protect/advanced-threat-protection-configure.md)
- [Deploy Microsoft Defender for Endpoint on macOS with Microsoft Intune](/microsoft-365/security/defender-endpoint/mac-install-with-intune)

### Built-in endpoint security

✅ Encrypt devices with FileVault disk encryption  

**FileVault** is a whole-disk encryption feature that helps prevent unauthorized access. The FileVault settings are built into the Intune settings catalog and are available as compliance policies.

So, you can configure FileVault, check for compliance, and deploy the policies to your devices.

To create these policies, in the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to:

- Devices > Configuration > Settings catalog > Full Disk Encryption
- Devices > Compliance > Require encryption of data storage on device

For more information about FileVault, go to:

- [Encrypt macOS devices with FileVault disk encryption with Intune](../../intune/protect/encrypt-devices-filevault.md)
- [Use FileVault to encrypt the startup disk on your Mac](https://support.apple.com/guide/mac-help/mh1710e6fa5b/mac) (opens Apple's website)

✅ Configure the firewall  

The **firewall** is an application firewall and helps prevent incoming attacks. The firewall settings are built into the Intune settings catalog and are available as compliance policies.

So, you can configure the firewall, check for compliance, and deploy the policies to your devices.

To create these policies, in the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to:

- Devices > Configuration > Settings catalog:
  - Networking > Firewall
  - Security > Security preferences

- Devices > Compliance > Firewall

For more information about the macOS firewall, go to:

- [Firewall policy for endpoint security in Intune](../../intune/protect/endpoint-security-firewall-policy.md)
- [Change Firewall settings on Mac](https://support.apple.com/guide/mac-help/mh11783/mac) (opens Apple's website)

✅ Configure Gatekeeper

**Gatekeeper** makes sure that only trusted software runs on the device. The Gatekeeper settings are built into the Intune settings catalog and are available as compliance policies.

So, you can configure Gatekeeper, check for compliance, and deploy the policies to your devices.

To create these policies, in the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to:

- Devices > Configuration > Settings catalog > System policy > System Policy Control
  - **Allow Identified Developer**: Select **True**.
  - **Enable Assessment**: Select **True**.

- Devices > Configuration > Settings catalog > System policy > System Policy Managed
  - **Disable Override**: Select **True**.

- Devices > Compliace > Gatekeeper

For more information about Gatekeeper, go to:

- [Use the settings catalog to configure settings in Microsoft Intune](../../intune/configuration/settings-catalog.md)
- [Gatekeeper and runtime protection in macOS](https://support.apple.com/guide/security/sec5599b66df/web) (opens Apple's website)

### Software Updates

?? NEEDS WORK ??

✅ Configure Software Updates

On devices, software updates are critical and you must determine how the updates will be installed. You have two options:

- **Option 1 (not recommended)** - End users manually install the updates. This approach relies on end users to decide when to install the updates and they may install an update that's not approved by your organization.

- **Option 2 (recommended)** - Use the [Intune settings catalog](../../intune/configuration/settings-catalog.md) to create a [managed software updates policy](../../intune/protect/managed-software-updates-ios-macos.md). This feature uses Apple's declarative device management (DDM), and is the recommended approach to update macOS devices.

  Specifically, you can configure the following settings:

  - Settings catalog > Declarative Device Management > Software Update

    When you configure these DDM settings, you enforce and restrict the behavior in the Settings app > Software Update node:

    - Automatic Check Enabled
    - Critical Updates Install
    - Automatically Install App Updates
    - Restrict Software Require Admin To Install
    - Config Data Install
    - Automatic Download

  - Settings catalog > Restrictions

    Using the following restrictions, you can delay how long after an update is released that users can install them manually:

    - Enforced Software Update Minor OS Deferred Install Delay: 0-30
    - Enforced Software Update Major OS Deferred Install Delay: 0-30
    - Enforced Software Update Non OS Deferred Install Delay: 0-30

For more information on planning your update strategy for macOS devices, go to [Software updates planning guide for managed macOS devices in Microsoft Intune](../../intune/protect/software-updates-guide-macos.md).

### Guest account

✅ Disable guest account

It's recommended to disable the guest account on macOS endpoints. You can disable guest account using [Intune settings catalog](../../intune/configuration/settings-catalog.md):

- Settings catalog > Accounts > Accounts:
  - **Disable Guest Account**: Select **True**.

### Idle login

✅ Set an idle timeout

Using the [Intune settings catalog](../../intune/configuration/settings-catalog.md), you control the time period after idle that macOS prompts for a password:

- Settings catalog > System Configuration > Screensaver:

  - **Ask for Password**: Select **True**.
  - **Login Windows Idle Time**: Enter something like `300`, which is 5 minutes.
  - **Ask for Password Delay**: Enter something like `5`.
  - **Module Name**: Enter the name of the screensaver module, like **Flurry**.

- Settings catalog > User Experience > Screensaver User:

  - **Idle Time**: Enter something like `300`, which is 5 minutes.
  - **Module Name**: Enter the name of the screensaver module, like **Flurry**.

> [!TIP]
> To find the screensaver module name, set the screensaver, open the Terminal app, and run the following command:
>
> `defaults -currentHost read com.apple.screensaver`

### macOS Evaluation Utility

✅ Use the macOS Evaluation Utility

The Mac Evaluation Utility confirms that your Mac has the configuration and settings recommended by Apple. To access the Mac Evaluation Utility, sign into [Apple Seed for IT](https://beta.apple.com/it) (opens Apple's website) > **Resources**.

## Phase 4 - Apply organization specific customizations

In this phase, you apply organization-specific settings and apps, and review your on-premises configuration. The phase helps you customize any features specific to your organization. Notice the various components of macOS. There are sections for each of the following areas:

- Apps
- Device Configuration
- Notifications
- Wallpaper
- Dock Configuration
- Device name
- Certificates
- Wi-Fi
- Custom profiles and preference files

### Apps

- **Line of business (LOB) apps**

  In Intune, you can deploy LOB apps using the following options:

  - [Add the app package (`.pkg`) to Intune, and use Intune policy to deploy the app](../../intune/apps/lob-apps-macos.md).
  - [Add the app package (`.pkg`) to Intune, and use a shell script to deploy the app](../../intune/apps/macos-unmanaged-pkg.md). This feature uses the Intune Management Extension and can deploy unsigned packages & packages without a payload.
  - [Add the app disk image (`.dmg`) to Intune, and use Intune policy to deploy the app](../../intune/apps/lob-apps-macos-dmg.md)
  - [Apps licensed with Apple's Volume Purchase Plan (VPP) and use Intune policy to deploy the app](../../intune/apps/vpp-apps-ios.md)

- **Microsoft Edge**

  You can deploy Microsoft Edge to macOS endpoints using the built-in deployment type. For more information, go to [Add Microsoft Edge to macOS devices using Microsoft Intune](../../intune/apps/apps-edge-macos.md).

  You can also configure Microsoft Edge settings using the [Intune settings catalog](../../intune/configuration/settings-catalog.md):

  - Settings Catalog > Microsoft Edge

- **Microsoft OneDrive**

  In [Phase 1](#phase-1---set-up-your-environment), you added Microsoft 365 apps, which includes Microsoft OneDrive. So, if you previously added Microsoft OneDrive, then you don't need to add it again. If necessary, you can also deploy Microsoft OneDrive separately using a [downloaded app package (`.pkg`) or using a VPP token](/sharepoint/deploy-and-configure-on-macos).

  You can also configure the [Microsoft OneDrive settings](/sharepoint/deploy-and-configure-on-macos) using the [Intune settings catalog](../../intune/configuration/settings-catalog.md). For example, the following settings might apply to your organization:

  - Microsoft Office > Microsoft OneDrive:

    - **Automatically and silently enable the Folder Backup feature (Known Folder Move)**: Enter your \<Microsoft Entra tenant ID>.
    - **Enable Files On-Demand**: Select **True**.
    - **Open at login**: Select **True**.

  - App Management > NS Extension Management:

    - **Allowed Extensions**: Enter `com.microsoft.OneDrive.FinderSync`.

    If you're deploying the VPP version of OneDrive, then enter `com.microsoft.OneDrive-Mac.FinderSync`.

    During Microsoft OneDrive configuration, end users are prompted to allow sync icons by enabling the Finder Sync extension. There's a sample script that can configure the finder extension for the user. For more information on the script, go to the [Intune Shell samples GitHub site](https://github.com/microsoft/shell-intune-samples/blob/master/macOS/Config/EnableOneDriveFinderSync/EnableOneDriveFinderSync.sh).

### Device Configuration

The settings catalog simplifies how you create a policy, and how you can see all the available settings. In different phases and steps in this guide, the [Intune settings catalog](../../intune/configuration/settings-catalog.md) is used to configure device features and settings.

For example, we used the settings catalog to configure the following feature areas:

- Microsoft Edge browser settings
- Microsoft AutoUpdate
- Microsoft Office
- Software Updates
- User Experience

There are many device settings you can configure using the settings catalog, including:

✅ **Dock**

You can configure the dock:

- Settings Catalog > User Experience > Dock

You can also add or remove items from the dock using a [GitHub - Microsoft Intune dock shell sample](https://github.com/microsoft/shell-intune-samples/tree/master/macOS/Config/Dock) or third-party command line tools like [GitHub - DockUtil](https://github.com/kcrawford/dockutil).

✅ **Notifications**

You can control notification prompts:

- Settings Catalog > User Experience > Notifications > Notification Settings

  You should enter the bundle ID for each application you want to control notifications for.

For more information, go to [Notifications MDM payload settings for Apple devices](https://support.apple.com/guide/deployment/dep46b6547ba/web) (opens Apple's website).

✅ **Preference files**

CONTINUE HERE

Custom profiles and preference files

For more information about this featue in Intune, go to [Add a property list file to macOS devices using Microsoft Intune](../../intune/configuration/preference-file-settings-macos.md)

Most settings required are available in [settings catalog](../../intune/configuration/settings-catalog.md), however if necessary Intune also supports deploying [custom profiles](/mem/intune/configuration/custom-settings-macos) and [preference files (plist)](../../intune/configuration/preference-file-settings-macos.md).

✅ **Wallpaper**

You can enforce a wallpaper on macOS using a combination of a sample script and the settings catalog:

- Settings Catalog > User Experience > Desktop:
  - Override Picture Path: Enter the \<path of the image>

The image file must exist on the macOS endpoint. To download a picture from a web location, you can use a sample script at [GitHub - Microsoft Intune wallpaper shell sample](https://github.com/microsoft/shell-intune-samples/tree/master/macOS/Config/Wallpaper). You can also use an app package tool to copy a file and then deploy it using the [unmanaged PKG](../../intune/apps/macos-unmanaged-pkg.md) deployment feature.

### Certificates

Intune supports deploying certificates. For more information, go to [Learn about the types of certificate that are supported by Microsoft Intune](../../intune/protect/certificates-configure.md).

### Wi-Fi

Intune supports deploying Wi-Fi profiles. See [Configure Wi-Fi settings for macOS devices in Microsoft Intune](../../intune/configuration/wi-fi-settings-macos.md).

## Phase 5 - Optional advanced configuration

✅ Content Caching

If you have a large number of macOS or iOS devices on your network, you can choose to deploy Apple Content Cache as a way to reduce your internet bandwidth. Apple Content Cache can cache content that is hosted on Apple services like Software Updates and VPP apps. For more information, go to [Intro to content caching](https://support.apple.com/guide/deployment/depde72e125f/web) (opens Apple's website).

✅ AutoUpdate local cache

Many Microsoft apps on macOS are updated using the Microsoft Autoupdate application. This application can be configured to reference a different URL for content. There's a project on GitHub that helps you configure this approach if it's relevant for your environment. For more information, go to the third party open source tool at [Microsoft AutoUpdate Cache Admin](https://github.com/pbowden-msft/MAUCacheAdmin).

## Phase 6 - Enroll your devices

macOS endpoints can now be enrolled into Intune. For more information, go to [distribute devices](../../intune/enrollment/device-enrollment-program-enroll-macos.md#distribute-devices).

## Phase 7 - Support and troubleshooting

macOS devices are managed through Intune by using a combination of the built-in operating system MDM capabilities and an agent installed by Intune called the Intune Management Extension (IME). These two components offer separate functionality and communicate with the macOS device through different channels. Enrollment is orchestrated through Apple Business Manager, MDM is orchestrated through the Apple Push Notification Service and the IME communicates directly with Intune.

:::image type="content" source="../media/macos-endpoints/macos-endpoint-ime-architecture.png" alt-text="A visual representation of how MDM and the Intune Managemnt Extension work together to support managemetn of macOS devices":::
 
For more information about the Intune Management Extension, go to [Understanding Microsoft Intune management agent for macOS](../../intune/apps/lob-apps-macos-agent.md).

### macOS enrollment maintenance

For your Mac devices to maintain their connection to Intune and continue enrolling there are several important areas you should check in the console periodically and action as necessary:

- **Apple Push Notification Service certificate expiry**.

   Apple's Push Notification Service certificate needs to be renewed yearly. When this certificate expires, Intune can't manage devices that enrolled via that certificate. It's important to ensure this certificate is renewed each year. For more information, go to [Get an Apple MDM Push certificate for Intune](../../intune/enrollment/apple-mdm-push-certificate-get.md#renew-apple-mdm-push-certificate).

- **Apple Automated Device Enrollment certificate expiry**

   When you set up a connection between Apple Business (or School) Manager and Intune there's a certificate that is used. This certificate needs to be renewed yearly. If this certificate isn't renewed, changes from Apple Business (or School) Manager won't sync to Intune. For more information, go to [Enroll macOS devices - Apple Business Manager or Apple School Manager](../../intune/enrollment/device-enrollment-program-enroll-macos.md#renew-enrollment-program-token).

- **Apple Automated Device Enrollment sync status**

   Apple suspends syncing of ADE tokens when the terms and conditions are changed in Apple Business (or School) Manager. These typically occur after a major OS release but can happen anytime. You should monitor the sync status to ensure there are no problems that require attention. For more information, go to [sync managed devices](../../intune/enrollment/device-enrollment-program-enroll-macos.md#sync-managed-devices).

### Remote Help

Remote Help is a cloud-based solution for secure help desk connections with role-based access controls. With the connection, your support staff can remote connect to the user's device.
For more information, go to [Using Remote Help on macOS to assist authenticated users](../../intune/fundamentals/remote-help-macos.md).

### Custom attributes

You can create custom attribute profiles which enable you to collect custom properties from managed macOS device using shell scripts. For more information, go to [Use shell scripts on macOS devices in Microsoft Intune](../../intune/apps/macos-shell-scripts#custom-attributes-for-macos.md).

## Resources

