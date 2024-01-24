---
# required metadata

title: Tutorial-Get started with macOS corporate endpoints
titleSuffix: Microsoft Intune
description: Set up secure macOS corporate organization-owned endpoints that are enrolled in Intune, and then deploy at scale with Apple Business Manager or Apple School Manager.
keywords:
author: MandiOhlinger
  
ms.author: mandia
manager: 
ms.date: 01/23/2024
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

This article guides you through the steps to create a macOS endpoint configuration for your organization for corporate or school-owned devices. It focuses on devices enrolled through Apple Business Manager or Apple School Manager using Automated Device Enrollment with user affinity. User affinity is typically used for devices with one primary user. For more information on the different types of management and enrollment types for macOS, go to [macOS device enrollment guide for Microsoft Intune](../../fundamentals/deployment-guide-enrollment-macos.md).

## How to get started

This guide has seven phases. Each phase has a set of steps to help you build your macOS endpoint configuration. The steps are designed to be completed in order. You can skip steps if you've already completed them.

The phases include:

- [Phase 1 - Set up your environment](#phase-1---set-up-your-environment)
- [Phase 2 - Enroll a macOS endpoint](#phase-2---enroll-a-macos-endpoint)
- [Phase 3 - Secure your macOS endpoint](#phase-3---secure-your-macos-endpoint)
- [Phase 4 - Apply organization specific customizations](#phase-4---apply-organization-specific-customizations)
- [Phase 5 - Optional advanced configuration](#phase-5---optional-advanced-configuration)
- [Phase 6 - Enroll your devices](#phase-6---enroll-your-devices)
- [Phase 7 - Support and reporting](#phase-7---support-and-reporting)

At the end of this guide, you have a macOS endpoint enrolled into Intune and ready to start validating in your environment.

## Phase 1 - Set up your environment

Before you build your first macOS endpoint, there are some key requirements and configuration that need to be checked. This phase walks you through checking the requirements, configuring integration with Apple Business Manager, and creating some settings and applications.

### Step 1 - Network requirements

✅ Setup your network

To successfully provision and deploy you macOS endpoint, the endpoint requires access to several public internet services. Start your testing on an open network. Or, in your organization network, provide access to all the endpoints listed at [Network endpoints for Microsoft Intune](../../fundamentals/intune-endpoints.md). Then, you can use your organization network to test your configuration.

If your wireless network requires certificates, you can start with an Ethernet connection during testing. The Ethernet connection gives you some time to determine the best approach for wireless connections that devices need for provisioning.

### Step 2 - Enrollment and licensing

✅ Create a new group, configure enrollment restrictions, and assign licenses

Before your endpoints enroll in Intune, there are some things you need to check. These checks make sure the correct endpoints are affected, your endpoints enroll successfully, and that the endpoints are licensed correctly. These checks include:

- **Create a new group**

  Create a new Microsoft Entra test group, like **Intune MDM Users**. Then, add specific test user accounts to this group. To limit who can enroll devices while you set up your configuration, target the configurations to this group.

  To create a Microsoft Entra group, you can use the Intune admin center or the Microsoft Entra admin center. When you create a group in Intune, you are creating an Entra group. You don't see the Entra branding, but that's what you're using. For more information, go to:

  - [Create a group to manage users in Intune](../../fundamentals/quickstart-create-group.md)
  - [Quickstart: Create a group with members and view all groups & members in Entra ID](/entra/fundamentals/groups-view-azure-portal)

  ?? Since this is an Intune article, my preference is to NOT direct users to the Azure portal. If agreed, I'll remove the Entra link. ??

- **Enrollment Restrictions**

  Enrollment restrictions allow you to control the types of devices that can enroll into Intune management. For this guide to be successful, make sure macOS (MDM) enrollment is allowed, which is the default configuration. Assign your enrollment restrictions to the new group you created.

  For information on configuring Enrollment Restrictions, go to [Set enrollment restrictions in Microsoft Intune](../../enrollment/enrollment-restrictions-set.md).

- **Licensing**
  
  Users enrolling macOS devices require a Microsoft Intune or Microsoft Intune for Education license. To assign licenses, go to [Assign Microsoft Intune licenses](../../fundamentals/licenses-assign.md). Assign the licenses to the test accounts you created.

  > [!NOTE]
  > Both types of licenses are typically included with licensing bundles, like Microsoft 365 E3 (or A3) and higher. For more information, go to [Compare Microsoft 365 Enterprise Plans](https://www.microsoft.com/microsoft-365/compare-microsoft-365-enterprise-plans).

### Step 3 - Add Apple MDM Certificate

✅ Add the push certificate with a Managed Apple ID

To manage macOS devices, Apple requires the tenant be configured with an MDM push certificate. If you manage iOS/iPadOS devices already, this step is likely already completed. For information on configurating an Apple MDM push certificate, go to [Get an Apple MDM Push certificate for Intune](../../enrollment/apple-mdm-push-certificate-get.md).

> [!NOTE]
> Don't use a personal Apple ID for this process. Management of the Apple Push Notification Service certificate is critical over the life of your device management solution. Access with a personal Apple ID can become unavailable as staff changes over time. Instead, use a Managed Apple ID to keep control within the Apple Business Manager (or Apple School Manager) instance.

### Step 4 - Apple Automated Device Enrollment (organization owned devices)

✅ Link Apple token

To manage devices enrolled through Apple Business Manager (or Apple School Manager), you need to set up an MDM token and link the token with Intune. For information on configuring Apple Business Manager with Intune, go to [Enroll macOS devices - Apple Business Manager or Apple School Manager](../../enrollment/device-enrollment-program-enroll-macos.md).

Overview of the high-level steps to configure Apple Business Manager with Intune:

1. Connect Intune to Apple Business Manager.
2. In Intune, create enrollment profiles for the Apple Business Manager token.
3. In Apple Business Manager, assign devices to your Intune MDM.
4. In Intune, assign profiles to your devices.

### Step 5 - Target devices

✅ Target specific groups

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

  4. Select **OK** > **Save** > **Create**.

  Now when creating apps and policies, you can target the policies to this new dynamic Microsoft Entra group.

   > [!NOTE]
   > Dynamic groups can take several minutes to populate after changes occur. In large organizations, it [can take longer](/entra/identity/users/groups-troubleshooting#troubleshooting-dynamic-memberships-for-groups). After creating a new group, wait several minutes before you check if the device is a member of the group.
   >
   > For more information about dynamic groups for devices, go to [Dynamic membership rules for groups in Microsoft Entra ID: Rules for devices](/entra/identity/users/groups-dynamic-membership#rules-for-devices).

- **Option 2 - All devices group with an assignment filter on enrollmentProfileName**
  
  For critical apps and policies that must apply immediately after enrollment (security settings, restrictions, the Company Portal app), you can assign the policies to the built-in **All Devices** group with an assignment filter. Policies and apps targeted to the **All Devices** group apply faster after enrollment than dynamic groups. Not all configuration profiles (like macOS scripts) support filters.

  For more information on assignment filters, go to [Create filters in Microsoft Intune](../../fundamentals/filters.md).

### Step 6 - Reduce sign-in prompts for apps

✅ Reduce sign-in prompts

In Intune, you can configure settings that reduce the number of sign-in prompts end users receive when using apps, including Microsoft 365 apps. There are two parts to this configuration:

- **Part 1** - Use the [Microsoft Enterprise SSO plug-in](../../configuration/use-enterprise-sso-plug-in-macos-with-intune.md) to provide single sign-on (SSO) to apps and websites that use Microsoft Entra ID for authentication, including Microsoft 365 apps. This plug-in uses an Intune device configuration policy.

  In the policy, you:

  - Enter the app bundle IDs that you want to enable SSO for.

  - Configure the following optional settings:

    | Key | Type | Value |
    |---|---|---|
    | AppPrefixAllowList | String | `com.microsoft.,com.apple.` |
    | browser_sso_interaction_enabled | Integer | 1 |
    | disable_explicit_app_prompt | Integer | 1 |

  For more information on the Enterprise SSO plug-in, including how to create the policy, go to [Configure macOS Enterprise SSO plug-in with Intune](../../configuration/use-enterprise-sso-plug-in-macos-with-intune.md).

- **Part 2** - Use the [Intune settings catalog](../../configuration/settings-catalog.md) to configure other settings that reduce sign-in prompts, including Microsoft AutoUpdate (MAU) and Microsoft Office.

  - **Authentication** > **Extensible Single Sign On (SSO)**

    | Name | Configuration |
    |---|---|
    | Extension Identifier | `com.microsoft.CompanyPortalMac.ssoextension`|
    | Team Identifier | `UBF8T346G9` |
    | Type | Redirect |
    | URLs | `https://login.microsoftonline.com` <br/> `https://login.microsoft.com` <br/> `https://sts.windows.net` <br/> `https://login.partner.microsoftonline.cn` <br/> `https://login.chinacloudapi.cn` <br/> `https://login.microsoftonline.us` <br/> `https://login-us.microsoftonline.com` |

  - **Microsoft AutoUpdate (MAU)**

    - **Automatically acknowledge data collection policy**: Select **Acknowledge – send required and optional data**.

      For more information about this setting, go to [Use preferences to manage privacy controls for Office for Mac](/deployoffice/privacy/mac-privacy-preferences#preference-setting-for-the-required-data-notice-dialog-for-microsoft-autoupdate)

    - **Enable AutoUpdate**: Select **True**.

      This setting forces Microsoft AutoUpdate to on. For more information about Microsoft AutoUpdate, which updates Microsoft 365 Apps and Company Portal, go to [Deploy updates for Office for Mac](/deployoffice/mac/deploy-updates-for-office-for-mac).

  - **Microsoft Office** > **Microsoft Office**

    These settings streamline the sign in process when opening Office apps for the first time. For more information on these setting, go to Set suite-wide preferences for Office for Mac.

    - **Office Activation Email Address**: Enter `{{userprincipalname}}`.
    - **Enable automatic sign-in**: Select **True**.

  For more information on the settings catalog, including how to create a policy, go to [Use the settings catalog to configure settings in Microsoft Intune](../../configuration/settings-catalog.md).

> [!NOTE]
> Microsoft will be releasing support for [Platform SSO](https://support.apple.com/guide/deployment/dep7bbb05313/web). When it's available, it will be announced in [Intune What's New](/mem/intune/fundamentals/whats-new). For more information on platform SSO, go to [Coming Soon – Platform SSO for macOS](https://techcommunity.microsoft.com/t5/microsoft-entra-blog/coming-soon-platform-sso-for-macos/ba-p/3902280).

### Step 7 - Create and assign some applications

- **Company Portal app**

  It's recommended to deploy the Intune Company Portal app to all devices as a required application. The Company Portal app is the self-service hub for users. In the Company Portal app, users can install apps, sync their device with Intune, check compliance status, and more.

  To deploy the Company Portal app as a required app, go to [Add the Company Portal for macOS app](../../apps/apps-company-portal-macos.md).

- **Microsoft 365 Apps**

  Microsoft 365 apps, like Word, Excel, OneDrive and Outlook, can easily be deployed to devices using the built-in Microsoft 365 apps for macOS app profile in Intune.

  To deploy Microsoft 365 Apps, go to:

  - [Assign Microsoft 365 to macOS devices with Microsoft Intune](../../apps/apps-add-office365-macos.md)
  - [Deploying Microsoft 365 Apps for Mac with Microsoft Intune - A Deep Dive](https://techcommunity.microsoft.com/t5/intune-customer-success/deploying-microsoft-365-apps-for-mac-with-microsoft-endpoint/ba-p/2243040)

## Phase 2 - Enroll a macOS endpoint

To enroll your first organization macOS endpoint, make sure the macOS endpoint is:

> [!div class="checklist"]
>
> - [Registered in Apple Business Manager and assigned to the Intune MDM](https://support.apple.com/guide/apple-business-manager/axmf500c0851/web)
> - [Assigned to an enrollment profile in Intune](../../enrollment/device-enrollment-program-enroll-macos.md#assign-an-enrollment-profile-to-devices)

To enroll your first macOS endpoint, use the following steps as an overview:

1. Erase or reset the macOS endpoint.
2. Go through Setup Assistant.
3. Open the Company Portal app and sign in with your organization account (`user@contoso.com`).
4. Your test macOS endpoint is enrolled into Intune.

## Phase 3 - Secure your macOS endpoint

In this phase, you build security settings for your organization. This section draws your attention to the various Endpoint Security components in Microsoft Intune including:

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

Compliance policies verify the device settings you configure and can remediate some settings that aren't compliant. For example, you can create compliance policies that check password complexity, jailbroken status, threat levels, enrollment status, and more.

If there are configuration settings that conflict between compliance policies and other policies, then the compliance policy takes precedence. For more information, go to [Compliance and device configuration policies that conflict](../../configuration/device-profile-troubleshoot.md#compliance-and-device-configuration-policies-that-conflict).

Conditional Access can be used to enforce the compliance policies you create. When combined, end users can be required to enroll their devices and meet a minimum security standard before accessing organization resources. If a device is non-compliant, then you can block access to resources, like email, or require the user to enroll their device and fix the issue.

You can create compliance and Conditional Access policies in the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

For more information, go to:

- [Use compliance policies to set rules for devices you manage with Intune](../../protect/device-compliance-get-started.md)
- [Conditional Access and Intune](../../protect/conditional-access.md)
- [What is Conditional Access in Microsoft Entra ID?](/entra/identity/conditional-access/overview)

### Microsoft Defender for Endpoint

✅ Use Microsoft Defender for Endpoint

Microsoft Defender for Endpoint is a mobile threat defense solution that helps protect your devices from security threats. In Intune, you can connect to your Microsoft Defender for Endpoint service, create Intune policies using Microsoft Defender for Endpoint settings, and then deploy the policies to your devices.

For more information, go to:

- [Configure Microsoft Defender for Endpoint in Intune](../../protect/advanced-threat-protection-configure.md)
- [Deploy Microsoft Defender for Endpoint on macOS with Microsoft Intune](/microsoft-365/security/defender-endpoint/mac-install-with-intune)

### Built-in endpoint security

✅ Encrypt devices with FileVault disk encryption  
✅ Configure the firewall  
✅ Configure Gatekeeper

endpoint protection
sc > Full disk encryption
compliance

- **FileVault** is a whole-disk encryption feature that helps prevent unauthorized access. The FileVault settings are built into the Intune settings catalog and are available as compliance policies.

  In the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to:

  - Devices > Configuration > Settings catalog > Full Disk Encryption
  - Devices > Compliance > Require encryption of data storage on device

  So, you can configure FileVault, check for compliance, and deploy the policies to your devices. For more information about FileVault, go to:

  - [Encrypt macOS devices with FileVault disk encryption with Intune](../../protect/encrypt-devices-filevault.md)
  - [Use FileVault to encrypt the startup disk on your Mac](https://support.apple.com/guide/mac-help/mh1710e6fa5b/mac) (opens Apple's website)

- The **firewall** is an application firewall and helps prevent incoming attacks. The firewall settings are built into the Intune settings catalog and are available as compliance policies.

  In the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to:

  - Devices > Configuration > Settings catalog:
    - Networking > Firewall
    - Security > Security preferences
  - Devices > Compliance > Firewall

  So, you can configure the firewall, check for compliance, and deploy the policies to your devices. For more information about the macOS firewall, go to:

  - [Firewall policy for endpoint security in Intune](../../protect/endpoint-security-firewall-policy.md)
  - [Change Firewall settings on Mac](https://support.apple.com/guide/mac-help/mh11783/mac) (opens Apple's website)

- **Gatekeeper** makes sure that only trusted software runs on the device. The Gatekeeper settings are built into the Intune settings catalog and are available as compliance policies.

  In the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to:

  - Devices > Configuration > Settings catalog > System policy > System Policy Control
    - **Allow Identified Developer**: Select **True**.
    - **Enable Assessment**: Select **True**.

  - Devices > Configuration > Settings catalog > System policy > System Policy Managed
    - **Disable Override**: Select **True**.
  - Devices > Compliace > Gatekeeper

  So, you can configure Gatekeeper, check for compliance, and deploy the policies to your devices. For more information about Gatekeeper, go to:

  - [Use the settings catalog to configure settings in Microsoft Intune](../../configuration/settings-catalog.md)
  - [Gatekeeper and runtime protection in macOS](https://support.apple.com/guide/security/sec5599b66df/web) (opens Apple's website)

### Software Updates

CONTINUE HERE

✅ Configure Software Updates

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

✅ Disable guest account

You can disable guest account usage with settings catalog:

- Accounts > Accounts
  - **Disable Guest Account:** Enabled

### Idle Login Configuration

✅ Set an idle timeout

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

✅ Use the macOS Evaluation Utility

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

You can deploy Microsoft Edge to macOS endpoints using the built-in deployment type. For more information, go to [Add Microsoft Edge to macOS devices using Microsoft Intune](/mem/intune/apps/apps-edge-macos).

### Microsoft OneDrive

Microsoft OneDrive is installed with Microsoft 365 apps earlier in Phase 1. If necessary, you can also deploy it separately using a [downloaded PKG or via VPP](/sharepoint/deploy-and-configure-on-macos).

[Settings for OneDrive](/sharepoint/deploy-and-configure-on-macos) can be configured using [settings catalog](/mem/intune/configuration/settings-catalog). As an example, these are some settings that might be applicable to your organization:

- Microsoft Office > OneDrive
  - **Automatically and silently enable the Folder Backup feature (Known Folder Move):** \<your Microsoft Entra tenant ID>
  - **Enable Files On-Demand:** True
  - **Open at login:** True

- App Management > NS Extension Management
  - **Allowed Extensions:** com.microsoft.OneDrive.FinderSync

>[!NOTE]
>If you are deploying the VPP version of OneDrive this will be com.microsoft.OneDrive-Mac.FinderSync

During configuration by the end user, the user is prompted to allow sync icons by enabling the Finder Sync extension. A script can be used to configure the finder extension on behalf of the user. There's a sample script on the [Intune Shell Samples GitHub site](https://github.com/microsoft/shell-intune-samples/blob/master/macOS/Config/EnableOneDriveFinderSync/EnableOneDriveFinderSync.sh).

### Device Configuration

The settings catalog is a single location where all configurable macOS settings are listed. This feature simplifies how you create a policy, and how you see all the available settings. For more information, go to [Create a policy using the settings catalog in Microsoft Intune](/mem/intune/configuration/settings-catalog).

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

For more information, go to [Notifications MDM payload settings for Apple devices](https://support.apple.com/guide/deployment/dep46b6547ba/web). 

### Wallpaper

You can enforce a wallpaper on macOS using a combination of a sample script and settings catalog:

- User Experience > Desktop
  - Override Picture Path: \<path>

The file must exist on the macOS endpoint. There's a sample script you can use to download a picture from a web location - [shell-intune-samples/macOS/Config/Wallpaper at master · microsoft/shell-intune-samples](https://github.com/microsoft/shell-intune-samples/tree/master/macOS/Config/Wallpaper). You can also use a package tool to copy a file and then deploy it using the [unmanaged PKG](/mem/intune/apps/macos-unmanaged-pkg) deployment capability.

### Dock configuration

Items can be added and removed from the dock using [example scripts](https://github.com/microsoft/shell-intune-samples/tree/master/macOS/Config/Dock) or third-party command line tools like [DockUtil](https://github.com/kcrawford/dockutil).

### Certificates

Intune supports deploying certificates. For more information, go to [Learn about the types of certificate that are supported by Microsoft Intune](/mem/intune/protect/certificates-configure).

### Wi-Fi

Intune supports deploying Wi-Fi profiles. See [Configure Wi-Fi settings for macOS devices in Microsoft Intune](/mem/intune/configuration/wi-fi-settings-macos).

### Custom profiles and preference files

Most settings required are available in [settings catalog](/mem/intune/configuration/settings-catalog), however if necessary Intune also supports deploying [custom profiles](/mem/intune/configuration/custom-settings-macos) and [preference files (plist)](/mem/intune/configuration/preference-file-settings-macos).

## Phase 5 - Optional Advanced Configuration
### Content Caching

If you have a large number of macOS or iOS devices on your network, you can choose to deploy Apple Content Cache as a way to reduce your internet bandwidth. Apple Content Cache can cache content that is hosted on Apple services like Software Updates and VPP apps. For more information, go to [Intro to content caching](https://support.apple.com/guide/deployment/depde72e125f/web).

### AutoUpdate local cache

Many Microsoft apps on macOS are updated using the Microsoft Autoupdate application. This application can be configured to reference a different URL for content. There's a project on GitHub that helps you configure this approach if it's relevant for your environment. For more information, go to the third party open source tool at [Microsoft AutoUpdate Cache Admin](https://github.com/pbowden-msft/MAUCacheAdmin).

## Phase 6 - Enroll your devices

macOS endpoints can now be enrolled into Intune. For more information, go to [distribute devices](/mem/intune/enrollment/device-enrollment-program-enroll-macos#distribute-devices).

## Phase 7 - Support and Troubleshooting

macOS devices are managed through Intune by using a combination of the built-in operating system MDM capabilities and an agent installed by Intune called the Intune Management Extension (IME). These two components offer separate functionality and communicate with the macOS device through different channels. Enrollment is orchestrated through Apple Business Manager, MDM is orchestrated through the Apple Push Notification Service and the IME communicates directly with Intune.

:::image type="content" source="../media/macos-endpoints/macos-endpoint-ime-architecture.png" alt-text="A visual representation of how MDM and the Intune Managemnt Extension work together to support managemetn of macOS devices":::
 
For more information about the Intune Management Extension, go to [Understanding Microsoft Intune management agent for macOS](/mem/intune/apps/lob-apps-macos-agent).

### macOS Enrollment Maintenance

For your Mac devices to maintain their connection to Intune and continue enrolling there are several important areas you should check in the console periodically and action as necessary:

- **Apple Push Notification Service certificate expiry**.

   Apple's Push Notification Service certificate needs to be renewed yearly. When this certificate expires, Intune can't manage devices that enrolled via that certificate. It's important to ensure this certificate is renewed each year. For more information, go to [Get an Apple MDM Push certificate for Intune](/mem/intune/enrollment/apple-mdm-push-certificate-get#renew-apple-mdm-push-certificate).

- **Apple Automated Device Enrollment certificate expiry**

   When you set up a connection between Apple Business (or School) Manager and Intune there's a certificate that is used. This certificate needs to be renewed yearly. If this certificate isn't renewed, changes from Apple Business (or School) Manager won't sync to Intune. For more information, go to [Enroll macOS devices - Apple Business Manager or Apple School Manager](/mem/intune/enrollment/device-enrollment-program-enroll-macos#renew-enrollment-program-token).

- **Apple Automated Device Enrollment sync status**

   Apple suspends syncing of ADE tokens when the terms and conditions are changed in Apple Business (or School) Manager. These typically occur after a major OS release but can happen anytime. You should monitor the sync status to ensure there are no problems that require attention. For more information, go to [sync managed devices](/mem/intune/enrollment/device-enrollment-program-enroll-macos#sync-managed-devices).

### Remote Help

Remote Help is a cloud-based solution for secure help desk connections with role-based access controls. With the connection, your support staff can remote connect to the user's device.
For more information, go to [Using Remote Help on macOS to assist authenticated users](/mem/intune/fundamentals/remote-help-macos).

### Custom attributes

You can create custom attribute profiles which enable you to collect custom properties from managed macOS device using shell scripts. For more information, go to [Use shell scripts on macOS devices in Microsoft Intune](/mem/intune/apps/macos-shell-scripts#custom-attributes-for-macos).

