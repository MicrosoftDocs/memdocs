---
# required metadata
title: What's new in Microsoft Intune - Azure | Microsoft Docs
titleSuffix:
description: Find out what's new in the Intune Azure portal
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 09/02/2020
ms.topic: reference
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
### Role-based access control
### Scripts

<!-- ########################## -->
## Week of September 7, 2020

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

### Tenant attach: CMPivot from the admin center
<!--IN7220536, CM6024392-->
Bring the power of CMPivot to the Microsoft Endpoint Manager admin center. Allow additional personas, like Helpdesk, to be able to initiate real-time queries from the cloud against an individual ConfigMgr managed device and return the results back to the admin center. This gives all the traditional benefits of CMPivot, which allows IT Admins and other designated personas the ability to quickly assess the state of devices in their environment and take action.

For more information about CMPivot from the admin center, see [CMPivot prerequisites](../../configmgr/tenant-attach/cmpivot-start.md), [CMPivot overview](../../configmgr/tenant-attach/cmpivot-overview-attached.md), and [CMPivot sample scripts](../../configmgr/tenant-attach/cmpivot-samples-attached.md).

## Week of August 31, 2020

### Device configuration

#### New version of the PFX Certificate Connector and changes for PKCS certificate profile support <!--  4839686  -->

We’ve released a new version of the PFX Certificate Connector, version **6.2008.60.607**. This new connector version:

- Supports PKCS certificate profiles on all supported platforms except Windows 8.1
 
  We’ve consolidated all of the PCKS support in the PFX Certificate Connector.  This means if you don’t use SCEP in your environment, and don’t use NDES for other intents, you can remove the Microsoft Certificate Connector and uninstall NDES from your environment. 
 
- Because the Microsoft Certificate Connector hasn’t had functionality removed, you can continue to use them to support PKCS certificate profiles.
- Supports certificate revocation for Outlook S/MIME
- Requires .NET Framework 4.7.2

For more information about certificate connectors, including a list of connector release for both certificate connectors, see [Certificate connectors](../protect/certificate-connectors.md)


<!-- ########################## -->
## Week of August 24, 2020 (2008 Service release)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### App management

#### Associated licenses revoked before deletion of Apple VPP token<!--6195322  -->
When you delete an Apple VPP token in Microsoft Endpoint Manager, all Intune-assigned licenses associated with that token are automatically revoked before the deletion.

#### Improvement to Update device settings page in Company Portal app for Android to shows descriptions <!-- 7414768 wnstaged -->
In the Company Portal app on Android devices, the **Update device settings** page lists the settings that need updated to be compliant. Users expand the issue to see more information, and see the **Resolve** button.

This user experience is improved. The listed settings are expanded by default to show the description, and show the **Resolve** button, when applicable. Previously, the issues were collapsed by default. This new default behavior reduces the number of clicks, so users can resolve issues more quickly.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device configuration

#### Use NetMotion as a VPN connection type for iOS/iPadOS and macOS devices<!-- 1333631   -->
When you create a VPN profile, NetMotion is available as a VPN connection type (**Devices** > **Device configuration** > **Create profile** > **iOS/iPadOS** or **macOS** for platform > **VPN** for profile > **NetMotion** for connection type).

For more information on VPN profiles in Intune, see [Create VPN profiles to connect to VPN servers](../configuration/vpn-settings-configure.md).

Applies to:
- iOS/iPadOS
- macOS

#### More Protected Extensible Authentication Protocol (PEAP) options for Windows 10 Wi-Fi profiles<!-- 3805024  -->
On Windows 10 devices, you can create Wi-Fi profiles using the Extensible Authentication Protocol (EAP) to authenticate Wi-Fi connections (**Devices** > **Configuration profiles** > **Create profile** > **Windows 10 and later** for platform > **Wi-Fi** for profile > **Enterprise**).

When you select Protected EAP (PEAP), there are new settings available:
- **Perform server validation in PEAP phase 1**: In PEAP negotiation phase 1, the server is verified by the certificate validation.
  - **Disable user prompts for server validation in PEAP phase 1**: In PEAP negotiation phase 1, user prompts asking to authorize new PEAP servers for trusted certification authorities aren't shown.
- **Require cryptographic binding**: Prevents connections to PEAP servers that don't use cryptobinding during the PEAP negotiation.

To see the settings you can configure, go to [Add Wi-Fi settings for Windows 10 and later devices](../configuration/wi-fi-settings-windows.md).

Applies to: 
- Windows 10 and newer

#### Configure the macOS Microsoft Enterprise SSO plug-in<!-- 5627576  idstaged -->

> [!IMPORTANT]
> On macOS, the Microsoft Azure AD SSO extension is still being developed. It's listed in the Intune user interface, but doesn't work as expected. On macOS, don't use **Microsoft Azure AD** for the SSO app extension type.

The Microsoft Azure AD team created a redirect single sign-on (SSO) app extension to allow macOS 10.15+ users to gain access to Microsoft apps, organization apps, and websites that support Apple's SSO feature and authenticate using Azure AD, with one sign-on. With the Microsoft Enterprise SSO plug-in release, you can configure the SSO extension with the new Microsoft Azure AD app extension type (**Devices** > **Configuration profiles** > **Create profile** > **macOS** for platform > **Device features** for profile >  **Single sign-on app extension** > SSO app extension type > **Microsoft Azure AD**).

To achieve SSO with the Microsoft Azure AD SSO app extension type, users need to install and sign in to the Company Portal app on their macOS devices. 

For more information about macOS SSO app extensions, see [Single sign-on app extension](../configuration/device-features-configure.md#single-sign-on-app-extension).

Applies to:
- macOS 10.15 and newer

#### Prevent users from unlocking Android Enterprise work profile devices using face and iris scanning<!--6069759 idmiss -->
You can now prevent users from using face or iris scanning to unlock their work profile managed devices, either at the device level or the work profile level. This can be set in **Devices** > **Configuration profiles** > **Create profile** > **Android Enterprise** for platform > **Work profile > Device restrictions** for profile > **Work profile settings** and **Password** sections.

For more information, see [Android Enterprise device settings to allow or restrict features using Intune](../configuration/device-restrictions-android-for-work.md#work-profile-only).

Applies to: 
- Android Enterprise work profile

#### Use SSO app extensions on more iOS/iPadOS apps with the Microsoft Enterprise SSO plug-in<!-- 7369991  -->
The [Microsoft Enterprise SSO plug-in for Apple devices](/azure/active-directory/develop/apple-sso-plugin) can be used with all apps that support SSO app extensions. In Intune, this feature means the plug-in works with mobile iOS/iPadOS apps that don't use the Microsoft Authentication Library (MSAL) for Apple devices. The apps don't need to use MSAL, but they do need to authenticate with Azure AD endpoints.

To configure your iOS/iPadOS apps to use SSO with the plug-in, add the app bundle identifiers in an iOS/iPadOS configuration profile (**Devices** > **Configuration profiles** > **Create profile** > **iOS/iPadOS** for platform > **Device features** for profile > **Single sign-on app extension** > **Microsoft Azure AD** for SSO app extension type > **App bundle IDs**).

To see the current SSO app extension settings you can configure, go to [Single sign-on app extension](../configuration/ios-device-features-settings.md#single-sign-on-app-extension).

Applies to:
- iOS/iPadOS

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device security

#### Deploy endpoint security Antivirus policy to tenant attached devices (preview)<!-- 5475441  -->
As a preview, you can deploy endpoint security [policy for Antivirus](../protect/endpoint-security-antivirus-policy.md) to devices you manage with Configuration Manager. This scenario requires you to configure a tenant attach between a supported version of Configuration Manager and your Intune subscription. The following versions of Configuration Manager are supported:

- Configuration Manager current branch 2006

For more information, see the [requirements for Intune endpoint security policies](../protect/tenant-attach-intune.md#specific-requirements-for-intune-endpoint-security-policies) to support Tenant Attach.

#### Changes for Endpoint security Antivirus policy exclusions<!--5583940, 6018119    -->
We’ve introduced two changes for managing the Microsoft Defender Antivirus exclusion lists you configure as part of an [Endpoint Security Antivirus policy](../protect/endpoint-security-antivirus-policy.md). The changes help you to prevent conflicts between different policies and resolve exclusion list conflicts that might exist in your previously deployed policies.

Both of the changes apply to policy settings for the following [Microsoft Defender Antivirus Configuration Service Providers](../protect/antivirus-microsoft-defender-settings-windows.md#microsoft-defender-antivirus-exclusions) (CSPs):

- Defender/ExcludedPaths
- Defender/ExcludedExtensions
- Defender/ExcludedProcesses

The changes are:

- New profile type: **Microsoft Defender Antivirus exclusions** - Use this new profile type for Windows 10 and later to define a policy that is focused only on Antivirus exclusions. This profile helps simplify management of your exclusion lists by separating them from other policy configurations.

  The exclusions you can configure include Defender *processes*, *file extensions*, and *files* and *folders* that you don’t want Microsoft Defender to scan.

- **Policy merge** – Intune now merges the list of exclusions you’ve defined in separate profiles into a single list of exclusions to apply to each device or user. For example, if you target a user with three separate policies, the exclusion lists from those three policies merge into a single superset of *Microsoft Defender Antivirus exclusions*, that then apply to that user.

#### Import and export lists of address ranges for Windows firewall rules<!-- 8125400  -->

We've added support to **Import** or **Export** a list of address ranges using .csv files to the Microsoft Defender Firewall rules profile in the Firewall policy for Endpoint security. The following Windows firewall rule settings now support import and export:

- **Local address ranges**
- **Remote address ranges**

We've also improved validation of both local and remote address range entry to help prevent duplicate or invalid entries.

For more information about these settings, see the settings for [Microsoft Defender Firewall rules](../protect/endpoint-security-firewall-profile-settings.md#microsoft-defender-firewall-rules).





<!-- ########################## -->
## Week of August 17, 2020

### Intune apps

#### Custom brand image now displayed in the Windows Company Portal profile page<!-- 4280187 -->
As a Microsoft Intune administrator, you can upload a custom brand image to Intune which will be displayed as a background image on the user's profile page in the Windows Company Portal app. For more information, see [How to customize the Intune Company Portal apps, Company Portal website, and Intune app](../apps/company-portal-app.md#branding).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### App management

#### The Company Portal adds Configuration Manager application support<!-- 4297660 -->
The Company Portal now supports Configuration Manager applications. This feature allows end users to see both Configuration Manager and Intune deployed applications in the Company Portal for co-managed customers. This new version of the Company Portal will display Configuration Manager deployed apps for all co-managed customers. This support will help administrators consolidate their different end user portal experiences. For more information, see [Use the Company Portal app on co-managed devices](../../configmgr/comanage/company-portal.md). 

### Device security

#### Set device compliance state from third-party MDM providers<!-- 6361689 -->

Intune now supports [third-party MDM solutions as a source of device compliance details](../protect/device-compliance-partners.md). This third-party compliance data can be used to enforce Conditional Access policies for Microsoft 365 apps on iOS and Android through integration with Microsoft Intune.  Intune evaluates the compliance details from the third-party provider to determine if a device is trusted, and then sets the conditional access attributes in Azure AD.  You'll continue to create your Azure AD Conditional Access policies from within the Microsoft Endpoint Manager admin center or the Azure AD portal.

The following third-party MDM providers are supported with this release, as a public preview:

- VMware Workspace ONE UEM (previously known as AirWatch)

*This update is rolling out to customers globally. You should see this capability within the next week.*

<!-- ########################## -->
## Week of August 10, 2020

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

#### Tenant attach: Install an application from the admin center <!-- IN7220536 CM6024389-->
You can now initiate an application install in real time for a tenant attached device from the Microsoft Endpoint Manager admin center. For more information, see [Tenant attach: Install an application from the admin center](../../configmgr/tenant-attach/applications.md).

<!-- ########################## -->
## Week of July 27, 2020

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Monitor and troubleshoot

#### Power BI compliance report template V2.0<!-- 636958 -->
Power BI template apps enable Power BI partners to build Power BI apps with little or no coding, and deploy them to any Power BI customer. Admins can update the version of the Power BI compliance report template from V1.0 to V2.0. V2.0 includes an improved design, as well as changes to the calculations and data that is surfaced as part of the template. For more information, see [Connect to the Data Warehouse with Power BI](../developer/reports-proc-get-a-link-powerbi.md) and [Update a template app](/power-bi/service-template-apps-install-distribute#update-a-template-app). Additionally, see the blog post [Announcing a New Version of the Power BI Compliance Report with Intune Data Warehouse](https://aka.ms/new_compliance_report).

<!-- ########################## -->
## Week of July 13, 2020  (2007 Service release)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### App management

#### Exchange On-Premises Connector support<!-- 7138486  -->
Intune is removing support for the Exchange On-Premises Connector feature from the Intune service beginning in the 2007 (July) release. Existing customers with an active connector will be able to continue with the current functionality at this time. New customers and existing customers that do not have an active connector will no longer be able to create new connectors or manage Exchange ActiveSync (EAS) devices from Intune. For those customers, Microsoft recommends the use of Exchange [hybrid modern authentication (HMA)](/office365/enterprise/hybrid-modern-auth-overview) to protect access to Exchange on-premises. HMA enables both Intune App Protection Policies (also known as MAM) and Conditional Access through Outlook Mobile for Exchange on-premises.

#### S/MIME for Outlook on iOS and Android devices without enrollment<!-- 6517155 -->
You can now enable S/MIME for Outlook on iOS and Android devices using an app configuration policy for managed apps. This allows for policy delivery regardless of device enrollment state. In [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Apps** > **App configuration policies** > **Add** > **Managed apps**. Additionally, you can choose whether or not to allow users to change this setting in Outlook. However, to automatically deploy S/MIME certificates to Outlook for iOS and Android, the device must be enrolled. For general information about S/MIME, see [S/MIME overview to sign and encrypt email in Intune](../protect/certificates-s-mime-encryption-sign.md). For more information about Outlook configuration settings, see [Microsoft Outlook configuration settings](../apps/app-configuration-policies-outlook.md) and [Add app configuration policies for managed apps without device enrollment](../apps/app-configuration-policies-managed-app.md). For Outlook for iOS and Android S/MIME information, see [S/MIME scenarios](/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/outlook-for-ios-and-android-configuration-with-microsoft-intune#smime-scenarios) and [Configuration keys - S/MIME settings](/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/outlook-for-ios-and-android-configuration-with-microsoft-intune#smime-settings). 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device configuration

#### New VPN settings for Windows 10 and newer devices<!-- 6602122   -->

When you create a VPN profile using the IKEv2 connection type, there are new settings you can configure (**Devices** > **Configuration profiles** > **Create profile** > **Windows 10 and later** for platform > **VPN** for profile > **Base VPN**):

- **Device Tunnel**: Allows devices to automatically connect to VPN without requiring any user interaction, including user log on. This feature requires you to enable **Always On**, and use **Machine certificates** as the authentication method.
- Cryptography suite settings: Configure the algorithms used to secure IKE and child security associations, which allow you to match client and server settings.

To see the settings you can configure, go to [Windows device settings to add VPN connections using Intune](../configuration/vpn-settings-windows-10.md).

Applies to:

- Windows 10 and newer

#### Configure more Microsoft Launcher settings in a device restrictions profile on Android Enterprise devices (COBO)<!-- 6285001  -->

On Android Enterprise Fully Managed devices, you can configure more Microsoft Launcher settings using a device restrictions profile (**Devices** > **Configuration profiles** > **Create profile** > **Android Enterprise** for platform > **Device Owner only** > **Device restrictions** > **Device experience** > **Fully managed**). 

To see these settings, go to [Android Enterprise device settings to allow or restrict features](../configuration/device-restrictions-android-for-work.md#device-experience).

You can also configure the Microsoft Launcher settings using an [app configuration profile](../apps/configure-microsoft-launcher.md).

Applies to:

- Android Enterprise device owner fully managed devices (COBO)

#### New features for Managed Home Screen on Android Enterprise device owner dedicated devices (COSU)<!-- 7414175 7133328 7133720 7134873 7135184   idstaged -->

On Android Enterprise devices, administrators can use device configuration profiles to customize the Managed Home Screen on dedicated devices using multi-app kiosk mode (**Devices** > **Configuration profiles** > **Create profile** > **Android Enterprise** for platform > **Device Owner Only** > **Device Restrictions** for profile > **Device experience** > **Dedicated device** > **Multi-app**).

Specifically, you can:

- Customize icons, change the screen orientation , and show app notifications on badge icons <!--7414175-->
- Hide the Managed Settings shortcut <!--7133328-->
- Easier access to the debug menu <!--7133720-->
- Create an allowed list of Wi-Fi networks <!-- 7134873-->
- Easier access to the device information <!-- 7135184-->

For more information, see [Android Enterprise device settings to allow or restrict features](../configuration/device-restrictions-android-for-work.md) and [this blog](https://techcommunity.microsoft.com/t5/intune-customer-success/how-to-setup-microsoft-managed-home-screen-on-dedicated-devices/ba-p/1388060).

Applies to:

- Android Enterprise device owner, dedicated devices (COSU)

#### Administrative templates updated for Microsoft Edge 84<!--7722068-->
The ADMX settings available for Microsoft Edge have been updated. End users can now configure and deploy new ADMX settings added in Edge 84. For more information, see the [Edge 84 release notes](/deployedge/microsoft-edge-relnote-stable-channel#policy-updates).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device enrollment

#### Corporate-owned, personally enabled devices (preview)<!--4442275  -->
Intune now supports Android Enterprise corporate-owned devices with a work profile for OS versions Android 8 and above. Corporate-owned devices with a work profile is one of the corporate management scenarios in the Android Enterprise solution set. This scenario is for single user devices intended for corporate and personal use. This corporate-owned, personally-enabled (COPE) scenario offers:

- work and personal profile containerization
- device-level control for admins
- a guarantee for end users that their personal data and applications will remain private

The first public preview release will include a subset of the features that will be included in the generally available release. Additional features will be added on a rolling basis. The features that will be available in the first preview include:

- Enrollment: Admins can create multiple enrollment profiles with unique tokens that do not expire. Device enrollment can be done through NFC, token entry, QR code, Zero Touch, or Knox Mobile Enrollment.
- Device configuration: A subset of the existing fully managed and dedicated device settings.
- Device compliance: The compliance policies that are currently available for fully managed devices.
- Device Actions: Delete device (factory reset), reboot device, and lock device.  
- App management: App assignments, app configuration, and the associated reporting capabilities 
- Conditional Access

For more information about corporate-owned with work profile preview, see the [support blog](https://techcommunity.microsoft.com/t5/intune-customer-success/microsoft-announces-public-preview-for-android-enterprise/ba-p/1524325).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

#### Updates to the remote lock action for macOS devices<!--7032805   -->
Changes to the remote lock action for macOS devices include:
- The recovery pin is displayed for 30 days before deletion (instead of 7 days).
- If an admin has a second browser open and tries to trigger the command again from a different tab or browser, Intune lets the command to go through. But the reporting status is set to failed rather than generating a new pin.
- The admin isn't allowed to issue another remote lock command if the previous command is still pending or if the device hasn’t checked back in.
These changes are designed to prevent the correct pin from being overwritten after multiple remote lock commands.

#### Device actions report differentiates between wipe and protected wipe<!--7118901 -->
The **Device actions** report now differentiates between the wipe and protected wipe actions. To see the report, go to [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Devices** > **Monitor** > **Device Actions** (under **Other**).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device security

#### Microsoft Defender Firewall rule migration tool preview<!-- 6423187   -->
As a public preview, we're working on a PowerShell based tool that will migrate Microsoft Defender Firewall rules. When you install and run the tool, it automatically creates endpoint security firewall rule policies for Intune that are based on the current configuration of a Windows 10 client. For more information, see [Endpoint security firewall rule migration tool overview](../protect/endpoint-security-firewall-rule-tool.md).

#### Endpoint detection and response policy for onboarding Tenant Attached devices to MDATP is Generally Available<!-- 7303816   -->
As part of endpoint security in Intune, the [Endpoint detection and response (EDR) policies for use with devices managed by Configuration Manager](../protect/endpoint-security-edr-policy.md) are no longer in *preview* and are  now *Generally Available*.

To use EDR policy with devices from a supported version of Configuration Manager, configure [Tenant attach for Configuration Manager](../../configmgr/tenant-attach/device-sync-actions.md). After you complete the tenant attach configuration, you can deploy EDR policies to onboard devices managed by Configuration Manager to Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP).

#### Bluetooth settings are available in Device Control profiles for Endpoint security Attack surface reduction policy <!--7032084   -->
We've added settings to manage Bluetooth on Windows 10 devices to the [Device control profile](../protect/endpoint-security-asr-profile-settings.md#device-control-profile) for *Endpoint security Attack surface Reduction policy*.  These are the same settings as those that have been available in Device restriction profiles for *Device configuration*.

#### Manage source locations for definition updates with endpoint security antivirus policy for Windows 10 devices<!-- 6347801   -->  
We've added two new settings to the *Updates* category of [endpoint security antivirus policy for Windows 10 devices](../protect/antivirus-microsoft-defender-settings-windows.md#updates)  that can help you manage how devices get update definitions:

- *Define file shares for downloading definition updates*
- *Define the order of sources for downloading definition updates*

With the new settings you can add UNC file shares as download source locations for definition updates, and define the order in which different source locations are contacted.

#### Improved security baselines node<!-- 7433136    -->
We've made some changes to improve the usability of the [security baseline node](../protect/security-baselines.md) in the Microsoft Endpoint Manager admin center. Now when you drill in to **Endpoint security** > **Security baselines** and then select a security baseline type like the MDM Security Baseline, your presented with the **Profiles** pane. On the Profiles pane you view the profiles you've created for that Baseline type.  Previously the console presented an Overview pane which included an aggregate data roll up that didn't always match the details found in the reports for individual profiles.

Unchanged, from the Profiles pane you can select a profile to drill-in to view that profiles properties as well as various reports that are available under *Monitor*.  Similarly, at the same level as Profiles you can still select **Versions** to view a the various versions of that profile type that you've deployed. When you drill-in to a version, you also gain access to reports, similar to the profile reports. 

#### Derived credentials support for Windows<!-- 4886090   -->
You can now use derived credentials with your Windows devices. This will  expand on the existing support for iOS/iPadOS and Android, and will be available for the same derived credential providers:
- Entrust Datacard
- Intercede
- DISA Purebred

Support for Widows includes use of a derived credential to authenticate to Wi-Fi or VPN profiles. For Windows devices, the derived credential is issued from the client app that's provided by the derived credential provider that you use.

#### Manage FileVault encryption for devices that were encrypted by the device user and not by Intune<!--5239424  -->
Intune can now [assume management of FileVault disk encryption on a macOS device that was encrypted by the device user](../protect/encrypt-devices-filevault.md#assume-management-of-filevault-on-previously-encrypted-devices), and not by Intune policy.  This scenario requires:
- The device to receive disk encryption policy from Intune that enables FileVault.
- The device user to use the Company Portal website to upload their personal recovery key for the encrypted device to Intune. To upload the key, they select the *Store recovery key* option for their encrypted macOS device.

After the user uploads their recovery key, Intune rotates the key to confirm it is valid. Intune can now manage the key and encryption as if it used policy to encrypt the device directly. Should a user need to recover their device, they can access the recovery key using any device from the following locations:   
- Company Portal website
- Company Portal app for iOS/iPadOS 
- Company Portal app for Android
- Intune app

#### Hide the personal recovery key from a device user during macOS FileVault disk encryption<!--  5475632-->
When you use endpoint security policy to configure macOS FileVault disk encryption, use the [**Hide recovery key**](../protect/endpoint-security-disk-encryption-profile-settings.md#filevault) setting to prevent display of the *personal recovery key* to the device user, while the device is being encrypted. By hiding the key during encryption, you can help keep it secure as users won’t be able to write it down while waiting for the device to encrypt. 

Later, if recovery is needed, a user can always use any device to view their personal recovery key through the Intune Company Portal website, the iOS/iPadOS Company Portal, the Android Company Portal, or the Intune app.

#### Improved view of security baseline details for devices<!-- 5536846  -->
You can now drill-in to the details for a device to view the settings details for security baselines that apply to the device. The settings appear in a simple, flat list, which includes the setting category, setting name, and status. For more information, see [View Endpoint security configurations per device](../protect/security-baselines-monitor.md#view-endpoint-security-configurations-per-device).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Monitor and troubleshoot

#### Device compliance logs now in English<!--6014904  -->
The Intune DeviceComplianceOrg logs previously only had enumerations for ComplianceState, OwnerType, and DeviceHealthThreatLevel. Now, these logs have English information in the columns.


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Role-based access control

#### Assign profile and Update profile permission changes<!--7177586   -->
Role-based access control permissions has changed for Assign profile and Update profile for the Automated Device Enrollment flow:

Assign profile: Admins with this permission can also assign the profiles to tokens and assign a default profile to a token for Automated Device Enrollment.

Update profile: Admins with this permission can update existing profiles only for Automated Device Enrollment.

To see these roles, go to [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Tenant administration** > **Roles** > **All roles** > **Create** > **Permissions** > **Roles**.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Scripting

#### Additional Data Warehouse v1.0 properties<!-- 6125732  -->
Additional properties are available using the Intune Data Warehouse v1.0. The following properties are now exposed via the [devices](../developer/reports-ref-devices.md#devices) entity:
- `ethernetMacAddress` -  The unique network identifier of this device.
- `office365Version` - The version of Microsoft 365 that is installed on the device.

The following properties are now exposed via the [devicePropertyHistories](../developer/reports-ref-devices.md#devicepropertyhistories) entity:
- `physicalMemoryInBytes` - The physical memory in bytes.
- `totalStorageSpaceInBytes` - Total storage capacity in bytes.

For more information, see [Microsoft Intune Data Warehouse API](../developer/reports-nav-intune-data-warehouse.md).

<!-- ########################## -->
## Week of July 06, 2020

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### App management

#### Update to device icons in Company Portal and Intune apps on Android<!-- 6057023 -->
We have updated the device icons in the Company Portal and Intune apps on Android devices to create a more modern look and feel and to align with the Microsoft Fluent Design System. For related information, see [Update to icons in Company Portal app for iOS/iPadOS and macOS](whats-new-app-ui.md#update-to-icons-in-company-portal-app-for-iosipados-and-macos-). 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device enrollment

#### iOS Company Portal will support Apple's Automated Device Enrollment without user affinity<!-- 7282707 --> 
The iOS Company Portal is now supported on devices enrolled using Apple's Automated Device Enrollment without requiring an assigned user. An end user can sign in to the iOS Company Portal to establish themselves as the primary user on an iOS/iPadOS device enrolled without device affinity. For more information about Automated Device Enrollment, see [Automatically enroll iOS/iPadOS devices with Apple's Automated Device Enrollment](../enrollment/device-enrollment-program-enroll-ios.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

#### Tenant attach: ConfigMgr client details in the admin center (preview)<!-- 7552762 -->

You can now see ConfigMgr client details including collections, boundary group membership, and real-time client information for a specific device in the Microsoft Endpoint Manager admin center. For more information, see [Tenant attach: ConfigMgr client details in the admin center (preview)](../../configmgr/tenant-attach/client-details.md).

## Week of June 22, 2020

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### App management

#### Newly available protected apps for Intune<!-- 7248952 -->
The following protected apps are now available:
- BlueJeans Video Conferencing
- Cisco Jabber for Intune
- Tableau Mobile for Intune
- ZERO for Intune

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Monitor and troubleshoot

#### Use Endpoint analytics to improve user productivity and reduce IT support costs<!-- 5653063 --> 
During the next week, this feature will be rolled out. Endpoint analytics aims to improve user productivity and reduce IT support costs by providing insights into the user experience. The insights enable IT to optimize the end-user experience with proactive support and to detect regressions to the user experience by assessing user impact of configuration changes. For more information, see [Endpoint analytics preview](https://aka.ms/uea).

#### Proactively remediate end user device issues using script packages<!-- 5933328 -->
You can create and run script packages on end user devices to proactively find and fix the top support issues in your organization. Deploying script packages will help you reduce support calls. Choose to create your own script packages or deploy one of the script packages we've written and used in our environment to reduce support tickets. Intune allows you to see the status of your deployed script packages and to monitor the detection and remediation results. In [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Reports** > **Endpoint analytics** > **Proactive remediations**. For more information, see [Proactive remediations](https://aka.ms/uea_prs).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device security

#### Use Microsoft Defender ATP in compliance policies for Android<!-- 4425686  -->

You can now use Intune to [onboard Android devices to Microsoft Defender Advanced Threat Protection](../protect/advanced-threat-protection-configure.md#onboard-devices) (MicrosoftDefender ATP). After your enrolled devices are onboarded, your compliance polices for Android can use the *threat level* signals from Microsoft Defender ATP. These are the same signals that you could previously use for Windows 10 devices.

#### Configure Defender ATP web protection for Android devices<!-- 6185563  -->

When you use Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP) for Android devices, you can [configure Microsoft Defender ATP web protection](../protect/advanced-threat-protection-manage-android.md) to disable the phishing scan feature, or prevent the scan from using VPN.

Depending on how your Android device enrolls with Intune, the following options are available:

- Android device administrator - Use custom OMA-URI settings to disable the web protection feature, or disable only the use of VPNs during scans.
- Android Enterprise work profile - Use an app configuration profile and the configuration designer to disable all web protection capabilities.

<!-- ########################## -->
## Week of June 15, 2020  (2006 Service release)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### App management  

#### Telecommunications data transfer protection for managed apps<!-- 6884491  -->
When a hyperlinked phone number is detected in a protected app, Intune will check whether a protection policy has been applied that allows the number to be transferred to a dialer app. You can choose how to handle this type of content transfer when it is initiated from a policy managed app. When creating an app protection policy in Microsoft Endpoint Manager, select a managed app option from the **Send org data to other apps**, then select an option from **Transfer telecommunications data to**. For more information about this data protection setting, see [Android app protection policy settings in Microsoft Intune](../apps/app-protection-policy-settings-android.md) and [iOS app protection policy settings](../apps/app-protection-policy-settings-ios.md). 

#### Unified delivery of Azure AD Enterprise and Office Online applications in the Company Portal<!-- 7414033  -->
On the **Customization** pane of Intune, you can select to **Hide** or **Show** both **Azure AD Enterprise applications** and **Office Online applications** in the Company Portal. Each end-user will see their entire application catalog from the chosen Microsoft service. By default, each additional app source will be set to **Hide**. This feature will first take effect in the Company Portal website, with support in the Windows Company Portal expected to follow. In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Tenant administration** > **Customization** to find this configuration setting. For related information, see [How to customize the Intune Company Portal apps, Company Portal website, and Intune app](../apps/company-portal-app.md).

#### Improvements to the Company Portal for macOS enrollment experience<!-- 6444452  -->
The Company Portal for macOS enrollment experience has a simpler enrollment process that aligns more closely with the Company Portal for iOS enrollment experience. Device users will  see:  
- A sleeker user interface.  
- An improved enrollment checklist.  
- Clearer instructions about how to enroll their devices.  
- Improved troubleshooting options.  

For more information about the Company Portal, see [How to customize the Intune Company Portal apps, Company Portal website, and Intune app](../apps/company-portal-app.md).

#### Improvements to Devices page of iOS/iPadOS and macOS Company Portals<!-- 6055001 -->
We've made changes to the Company Portal **Devices** page to improve the app experience for iOS/iPadOS and Mac users. In addition to creating a more modern look and feel, we reorganized the device details under a a single column with defined section headers so that it's easier for users to see their device status. We also added clearer messaging and  troubleshooting steps for users whose devices fall out of compliance. For more information about Company Portal, see [How to customize the Intune Company Portal apps, Company Portal website, and Intune app](../apps/company-portal-app.md). To manually sync a device, see [Sync your iOS device manually](../user-help/sync-your-device-manually-ios.md).  

#### Cloud setting for iOS/iPadOS Company Portal app<!-- 7071303  -->
A new **Cloud** setting for the iOS/iPadOS Company Portal allows users to redirect their authentication towards the appropriate cloud for your organization. By default, the setting is configured to **Automatic**, which directs authentication towards the cloud automatically detected by the user's device. If authentication for your organization must be redirected towards a cloud other than the cloud that is automatically detected (such as Public or Government), your users can manually select the appropriate cloud by selecting the **Settings** app > **Company Portal** > **Cloud**. Your users should only change the **Cloud** setting from **Automatic** if they are signing in from another device and the appropriate cloud is not automatically detected by their device. 

#### Duplicate Apple VPP tokens<!-- 7101606  -->
Apple VPP tokens with the same **Token Location** are now marked as **Duplicate** and can be synced again when the duplicate token has been removed. You can still assign and revoke licenses for tokens that are marked as duplicate. However, licenses for new apps and books purchased may not be reflected once a token is marked as duplicate. To find Apple VPP tokens for your tenant, from [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Tenant administration** > **Connectors and tokens** > **Apple VPP Tokens**. For more information about VPP tokens, see [How to manage iOS and macOS apps purchased through Apple Volume Purchase Program with Microsoft Intune](../apps/vpp-apps-ios.md).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device configuration

#### Add multiple root certificates for EAP-TLS authentication in Wi-Fi profiles on macOS devices<!-- 2077871  -->

On macOS devices, you can create a Wi-Fi profile, and select the Extensible Authentication Protocol (EAP) authentication type  (**Devices** > **Configuration profiles** > **Create profile** > **macOS** for platform > **Wi-Fi** for profile > **Wi-Fi type** set to Enterprise).

When you set the **EAP Type** to **EAP-TLS**, **EAP-TTLS**, or **PEAP** authentication,  you can add multiple root certificates. Previously, you could only add one root certificate.

For more information on the settings you can configure, see [Add Wi-Fi settings for macOS devices in Microsoft Intune](../configuration/wi-fi-settings-macos.md).

Applies to:
- macOS

#### Use PKCS certificates with Wi-Fi profiles on Windows 10 and newer devices<!-- 3246388   -->
You can authenticate Windows Wi-Fi profiles with SCEP certificates (**Device configuration** > **Profiles** > **Create profile** > **Windows 10 and later** for platform > **Wi-Fi** for profile type > **Enterprise** > **EAP type**). Now, you can use PKCS certificates with your Windows Wi-Fi profiles. This feature allows users to authenticate Wi-Fi profiles using new or existing PKCS certificate profiles in your tenant. 

For more information on the Wi-Fi settings you can configure, see [Add Wi-Fi settings for Windows 10 and later devices in Intune](../configuration/wi-fi-settings-windows.md).

Applies to:
- Windows 10 and newer

#### Wired network device configuration profiles for macOS devices<!-- 3508686  -->
A new macOS device configuration profile is available that configures wired networks (**Devices** > **Configuration profiles** > **Create profile** > **macOS** for platform > **Wired Network** for profile). Use this feature to create 802.1x profiles to manage wired networks, and deploy these wired networks to your macOS devices.

For more information in this feature, see [Wired networks on macOS devices](../configuration/wired-networks-configure.md).

Applies to:
- macOS

#### Use Microsoft Launcher as the default launcher for fully managed Android Enterprise devices<!-- 4927976   -->
On Android Enterprise device owner devices, you can set Microsoft Launcher as the default launcher for fully managed devices (**Devices** > **Configuration profiles** > **Create profile** > **Android Enterprise** for platform > **Device owner** > **Device restrictions** for profile > **Device experience**). To configure all other Microsoft Launcher settings, use [app configuration policies](../apps/configure-microsoft-launcher.md). 

Also, there are some other UI updates, including **Dedicated devices** being renamed to **Device experience**.

To see all the settings you can restrict, see [Android Enterprise device settings to allow or restrict features using Intune](../configuration/device-restrictions-android-for-work.md). 

Applies to:
- Android Enterprise device owner fully managed devices (COBO)

#### Use Autonomous Single App Mode settings to configure the iOS Company Portal app to be a sign in/sign out app<!-- 7055619   -->
On iOS/iPadOS devices, you can configure apps to run in autonomous single app mode (ASAM). Now, the Company Portal app supports ASAM, and can be configured to be a "sign in/sign out" app. In this mode, users must sign in to the Company Portal app to use other apps and the Home screen button on the device. When they sign out of the Company Portal app, the device returns to single app mode, and locks on the Company Portal app.

To configure the Company Portal to be in ASAM, go to **Devices** > **Configuration profiles** > **Create profile** > **iOS/iPadOS** for platform > **Device restrictions** for profile > **Autonomous Single App Mode**.

For more information, see [Autonomous single app mode (ASAM)](../configuration/device-restrictions-ios.md#autonomous-single-app-mode-asam) and [single app mode](https://support.apple.com/guide/mdm/single-app-mode-mdm80a981/1/web/1) (opens Apple's web site).

Applies to:
- iOS/iPadOS

#### Configure content caching on macOS devices<!-- 7106872   -->
On macOS devices, you can create a configuration profile that configures content caching (**Devices** > **Configuration profiles** > **Create profile** > **macOS** for platform > **Device features** for profile). Use these settings to delete cache, allow shared cache, set a cache limit on the disk, and more.

For more information on content caching, see [ContentCaching](https://developer.apple.com/documentation/devicemanagement/contentcaching) (opens Apple's web site).

To see the settings you can configure, go to [macOS device feature settings in Intune](../configuration/macos-device-features-settings.md).

Applies to:
- macOS

#### Add new schema settings, and search for existing schema settings using OEMConfig on Android Enterprise<!-- 6394386   -->
In Intune, you can use OEMConfig to manage settings on Android Enterprise devices (**Devices** > **Configuration profiles** > **Create profile** > **Android Enterprise** for platform > **OEMConfig** for profile). When you use the **Configuration designer**, the properties in the app schema are shown. Now, in the **Configuration designer**, you can:

- Add new settings to the app schema.
- Search for new and existing settings in the app schema.

For more information on OEMConfig profiles in Intune, see [Use and manage Android Enterprise devices with OEMConfig in Microsoft Intune](../configuration/android-oem-configuration-overview.md).

Applies to:
- Android Enterprise

#### Block Shared iPad temporary sessions on Shared iPad devices<!-- 6613794  -->
In Intune, there's a new **Block Shared iPad temporary sessions** setting that blocks temporary sessions on Shared iPad devices (**Devices** > **Configuration profiles** > **Create profile** > **iOS/iPadOS** for platform > **Device restrictions** for profile type > **Shared iPad**). When enabled, end users can't use the Guest account. They must sign in to the device with their Managed Apple ID and password. 

For more information, see [iOS and iPadOS device settings to allow or restrict features](../configuration/device-restrictions-ios.md).

Applies to:
- Shared iPad devices running iOS/iPadOS 13.4 and newer

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device enrollment

#### Bring-your-own-devices can use VPN to deploy<!--5015344  -->
The new  Autopilot profile **Skip Domain Connectivity Check** toggle lets you deploy Hybrid Azure AD Join devices without access to your corporate network using your own 3rd party Win32 VPN client. To see the new toggle, go to [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Devices**  > **Windows** > **Windows enrollment** > **Deployment profiles** > **Create profile** > **Out-of-box experience (OOBE)**.

#### Enrollment Status Page profiles can be set to device groups<!--3952138 -->
Previously, Enrollment Status Page (ESP) profiles could only be targeted to user groups. Now you can also set them to target device groups. For more information, see [Set up an Enrollment Status Page](../enrollment/windows-enrollment-status.md).

#### Automated Device Enrollment sync errors<!-- 6988214 -->
New errors will be reported for iOS/iPadOS and macOS devices, including
- Invalid characters in the phone number or if that field is empty. 
- Invalid or empty configuration name for the profile. 
- Invalid/expired cursor value or if no cursor is found.
- Rejected or expired token. 
- The department field is empty or the length is too long. 
- Profile is not found by Apple and a new one needs to be created. 
- A count of removed Apple Business Manager devices will be added to the overview page where you see the status of your devices.

#### Shared iPads for Business<!--6367326   -->
You can use Intune and Apple Business Manager to easily and securely set up Shared iPad so that multiple employees can share devices. Apple's [Shared iPad](https://developer.apple.com/education/shared-ipad/) provides a personalized experience for multiple users while preserving user data. Using a Managed Apple ID, users can access their apps, data, and settings after signing into any Shared iPad in their organization. Shared iPad works with federated identities.

To see this feature, go to [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Devices** > **iOS** > **iOS enrollment** > **Enrollment program tokens** > **choose a token** > **Profiles** > **Create profile** > **iOS**. On the **Management Settings** page, select **Enroll without User Affinity** and you'll see the **Shared iPad** option.

Requires: iPadOS 13.4 and later. This release added support for temporary sessions with Shared iPad so that users can access a device without a Managed Apple ID. Upon logout, the device erases all user data so that the device is immediately ready for use, eliminating the need for a device wipe. 

#### Updated user interface for Apple's Automated Device Enrollment<!--7430322 -->
The user interface has been updated to replace Apple's Device Enrollment Program to Automated Device Enrollment to reflect Apple terminology.


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

#### Device remote lock pin available for macOS<!--7281557   -->
The availability for macOS device remote lock pins has been increased from 7 days to 30 days.

#### Change primary user on co-managed devices<!--7319183  -->
You can change a device's primary user for co-managed Windows devices. For more information on how to find and change it, see [Find the primary user of an Intune device](../remote-actions/find-primary-user.md). This feature will be rolling out gradually over the next few weeks.

#### Setting the Intune primary user also sets the Azure AD owner property<!--7319227 -->
This new feature automatically sets the owner property on newly-enrolled Hybrid Azure AD joined devices at the same time that the Intune primary user is set. For more information on the primary user, see [Find the primary user of an Intune device](../remote-actions/find-primary-user.md).

This is a change to the enrollment process and only applies to newly enrolled devices. For existing Hybrid Azure AD Joined devices, you must manually update the Azure AD Owner property. To do this, you can use the [Change primary user feature](../remote-actions/find-primary-user.md#change-a-devices-primary-user) or [a script](https://github.com/microsoftgraph/powershell-intune-samples/tree/master/ManagedDevices).

When Windows 10 devices become Hybrid Azure Azure Directory Joined, the first user of the device becomes the primary user in Endpoint Manager.  Currently, the user isn't set on the corresponding Azure AD device object. This causes an inconsistency when comparing the *owner* property from an Azure AD portal with the *primary user* property in Microsoft Endpoint Manager admin center. The Azure AD owner property is used for securing access to BitLocker recovery keys. The property isn't populated on Hybrid Azure AD Joined devices. This limitation prevents set up of self-service of BitLocker recovery from Azure AD. This upcoming feature solves this limitation.


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device security

#### Hide the recovery key from users during FileVault 2 encryption for macOS devices<!-- 5459801  -->
We've added a new setting to the *FileVault* category within the [macOS Endpoint Protection](../protect/endpoint-protection-macos.md#filevault) template: **Hide recovery key**. This setting hides the personal key from the end user during FileVault 2 encryption. 

To view the personal recovery key of an encrypted macOS device, the device user can go to any of the following locations and click on *get recovery key* for the macOS device: 

- The iOS/iPadOS company portal app
- The Intune app
- The company portal website
- The Android company portal app

#### Support for S/MIME signing and encryption certificates with Outlook on Android Fully Managed<!--5896415   -->
You can now use certificates for S/MIME signing and encryption with Outlook on devices that run Android Enterprise Fully Managed.

This expands on the support added last month for other Android versions (Support for S/MIME signing and encryption certificates with Outlook on Android). You can provision these certificates by using SCEP and PKCS imported certificate profiles.

For more information about this support, see [Sensitivity labeling and protection in Outlook for iOS and Android](/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/sensitive-labeling-and-protection-outlook-for-ios-android) in the Exchange documentation.

#### Add a link to your company portal support website to emails for noncompliance<!-- 7225498    -->
When you [configure a notification message template](../protect/actions-for-noncompliance.md#create-a-notification-message-template) for sending email notifications for noncompliance, use the new setting **Company Portal Website Link** to automatically include a link to your Company Portal website. With this option set to *Enable*, users with noncompliant devices who receive email based on this template can use the link to open a website to learn more about why their device isn’t compliant. 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Licensing

#### Admins no longer require an Intune license to access Microsoft Endpoint Manager admin console<!--1335430 -->
You can now set a tenant-wide toggle that removes the Intune license requirement for admins to access the MEM admin console and query graph APIs. Once you remove the license requirement, you can never reinstate it. 


> [!Note]
> Some actions, including the Teamviewer Connector flow, still require an Intune license to complete.


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Scripts 

#### Availability of Shell scripts on macOS devices<!-- 7134839  -->
Shell scripts for macOS devices are now available for Government Cloud and China customers. For more information about shell scripts, see [Use shell scripts on macOS devices in Intune](../apps/macos-shell-scripts.md).



<!-- ########################## -->
## Week of June 8, 2020   

### App management  

#### Updates to informational screen in Company Portal for iOS/iPadOS <!--7032452 -->
An informational screen in Company Portal for iOS/iPadOS has been updated to better explain what an admin can see and do on devices. These clarifications are only about corporate-owned devices. Only the text has been updated, no actual modifications have been made to what the admin can see or do on user devices. To see the updated screens, go to [UI updates for Intune end-user apps](./whats-new-app-ui.md).

#### Updated Android APP Conditional Launch end-user experience<!-- 5736084 -->
The 2006 release of the Android Company Portal has changes that build on the updates from the 2005 release. In 2005, we rolled out an update where end users of Android devices that are issued a warn, block, or wipe by an app protection policy see a full page message describing the reason for the warn, block, or wipe and the steps to remediate the issues. In 2006, first-time users of Android apps assigned an app protection policy will be taken through a guided flow to remediate issues that cause their app access to be blocked. 

<!-- ########################## -->
## Week of May 25, 2020

### App management

#### Windows 32-bit (x86) apps on ARM64 devices<!-- 5477661 -->
Windows 32-bit (x86) apps that are deployed as available to ARM64 devices will now be displayed in the Company Portal. For more information about Windows 32-bit apps, see [Win32 app management](../apps/apps-win32-app-management.md).

#### Windows Company Portal app icon<!-- 7114635 -->
The icon for the Windows Company Portal app has been updated. For more information about the Company Portal, see [How to customize the Intune Company Portal apps, Company Portal website, and Intune app](../apps/company-portal-app.md).


<!-- ########################## -->
## Week of May 18, 2020

### App management  

#### Update to icons in Company Portal app for iOS/iPadOS and macOS<!--6057697 -->
We've updated the icons in Company Portal to create a more modern look and feel that's supported on dual screen devices and aligns with the Microsoft Fluent Design System. To see the updated icons, go to [UI updates for Intune end-user apps](./whats-new-app-ui.md). 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device security

#### Use Endpoint detection and response policy to onboard devices to Defender ATP<!-- 7130165  -->

Use endpoint security [policy for Endpoint detection and response](../protect/endpoint-security-edr-policy.md) (EDR) to onboard and configure devices for your deployment of Microsoft Defender Advanced Threat Protection (Defender ATP). EDR supports policy for Windows devices managed by Intune (MDM), and a separate policy for Windows devices managed by Configuration Manager. 

To use the policy for Configuration Manager devices, you must [set up Configuration Manager to support the EDR policy](../protect/tenant-attach-intune.md). Set up includes:

- Configure your Configuration manager for *tenant attach*.
- Install an in-console update for Configuration Manager to enable support for the EDR policies. This update applies only to hierarchies that have enabled *tenant attach*.
- Synchronize your device collections form your hierarchy to the Microsoft Endpoint Manager admin center.


<!-- ########################## -->
## Week of May 11, 2020 (2005 Service release)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### App management

#### Customize self-service device actions in the Company Portal<!--4393379 -->
You can customize the available self-service device actions that are shown to end-users in the Company Portal app and website. To help prevent unintended device actions, you can configure these settings for the Company Portal app by selecting **Tenant Administration** > **Customization**. The following actions are available:
- Hide **Remove** button on corporate Windows device.
- Hide **Reset** button on corporate Windows devices.
- Hide **Reset** button on corporate iOS devices.
- Hide **Remove** button on corporate iOS devices.
For more information, see [User self-service device actions from the Company Portal](../apps/company-portal-app.md#user-self-service-device-actions-from-the-company-portal).

#### Auto update VPP available apps<!-- 3640511  -->
Apps that are published as Volume Purchase Program (VPP) available apps will be automatically updated when **Automatic App Updates** is enabled for the VPP token. Previously, VPP available apps did not automatically update. Instead, end-users had to go to the Company Portal and reinstall the app if a newer version was available. Required apps continue to support automatic updates.




#### Android Company Portal user experience<!-- 5736084  -->
In the 2005 release of Android Company Portal, end-users of Android devices that are issued a warn, block, or wipe by an app protection policy will see a new user experience. Instead of the current dialog experience, end-users will see a full page message describing the reason for the warn, block, or wipe and the steps to remediate the issue. For more information, see [App protection experience for Android devices](../apps/app-protection-policy.md#app-protection-experience-for-android-devices) and [Android app protection policy settings in Microsoft Intune](../apps/app-protection-policy-settings-android.md).

#### Support for multiple accounts in Company Portal for macOS<!-- 5779449  -->
The Company Portal on macOS devices now caches user accounts, making sign-in easier. Users no longer need to sign into the Company Portal every time they launch the application. Additionally, the Company Portal will display an account picker if multiple user accounts are cached, so that users don't have to enter their user name. 

#### Newly available protected apps<!-- 7060934   -->
The following protected apps are now available:
- Board Papers
- Breezy for Intune
- Hearsay Relate for Intune
- ISEC7 Mobile Exchange Delegate for Intune
- Lexmark for Intune
- Meetio Enterprise
- Microsoft Whiteboard
- Now® Mobile - Intune
- Qlik Sense Mobile 
- ServiceNow® Agent - Intune
- ServiceNow® Onboarding - Intune
- Smartcrypt for Intune
- Tact for Intune
- Zero - email for attorneys

For more information about protected apps, see [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md).

#### Search the Intune docs from the Company Portal<!-- 1736480   -->
You can now search the Intune documentation directly from the Company Portal for macOS app. In the menu bar, select **Help** > **Search** and enter the key words of your search to quickly find answers to your questions.

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device configuration

#### Improvements to OEMConfig support for Zebra Technologies devices<!-- 4184154 -->
Intune fully supports all features provided by Zebra OEMConfig. Customers managing Zebra Technologies devices with Android Enterprise and OEMConfig can deploy multiple OEMConfig profiles to one device. Customers can also view rich reporting about the status of their Zebra OEMConfig profiles.

For more information, see [Deploy multiple OEMConfig profiles to Zebra devices in Microsoft Intune](../configuration/oemconfig-zebra-android-devices.md).

There is no change in OEMConfig behavior for other OEMs.

Applies to:
- Android Enterprise
- Zebra Technologies devices that support OEMConfig. For specific details on support, contact Zebra.

#### Configure system extensions on macOS devices<!-- 6255624 -->
On macOS devices, you can create a kernel extensions profile to configure settings at the kernel-level (**Devices** > **Configuration profiles** > **macOS** for platform > **Kernel extensions** for profile). Apple is eventually deprecating kernel extensions, and replacing them with system extensions in a future release.

System extensions run in the user space, and don’t have access to the kernel. The goal is to increase security and provide more end user control, while limiting attacks at the kernel level. Both kernel extensions and system extensions allow users to install app extensions that extend the native capabilities of the operating system.

In Intune, you can configure both kernel extensions and system extensions (**Devices** > **Configuration profiles** > **macOS** for platform > **System extensions** for profile). Kernel extensions apply to 10.13.2 and newer. System extensions apply to 10.15 and newer. From macOS 10.15 to macOS 10.15.4, kernel extensions and system extensions can run side-by-side. 

To learn about these extensions on macOS devices, see [Add macOS extensions](../configuration/kernel-extensions-overview-macos.md).

Applies to:
- macOS 10.15 and newer

#### Configure app and process privacy preferences on macOS devices<!-- 2934232   --> 
With the release of macOS Catalina 10.15, Apple added new security and privacy enhancements. By default, applications and processes are unable to access specific data without user consent. If users don't provide consent, the applications and processes may fail to function. Intune is adding support for settings that enable IT administrators to allow or disallow data access consent on behalf of end-users on devices running macOS 10.14 and later. These settings will ensure that applications and processes continue to function properly, and reduce the number of prompts. 

For more information on the settings you can manage, see [macOS privacy preferences](../configuration/device-restrictions-macos.md#privacy-preferences).

Applies to:
- macOS 10.14 and newer

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device enrollment

#### Enrollment restrictions support scope tags<!--4209550  -->
You can now assign scope tags to enrollment restrictions. To do so, go to [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Devices** > **Enrollment restrictions** > **Create restriction**. Create either type of restriction and you'll see the **Scope tags** page. For more information, see [Set enrollment restrictions](../enrollment/enrollment-restrictions-set.md).

#### Autopilot support for HoloLens 2 devices<!--6305220  -->
Windows Autopilot now supports HoloLens 2 devices. For more information on using Autopilot for HoloLens, see [Windows Autopilot for HoloLens 2](/hololens/hololens2-autopilot).

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

#### Use sync remote action in bulk for iOS<!--6440956  idmiss-->
You can now use the sync remote action on up to 100 iOS devices at a time. To see this feature, go to [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Devices** > **All devices** > **Bulk device actions**. 

#### Automated device sync interval down to 12 hours<!--3077535  -->
For Apple's Automated Device Enrollment, the automated device sync interval between Intune and Apple Business Manager has been reduced from 24 hours to 12 hours. For more information on sync, see [Sync managed devices](../enrollment/device-enrollment-program-enroll-ios.md#sync-managed-devices).


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device security

#### Derived credentials support for DISA Purebred on Android devices<!-- 6939073     -->
You can now use *DISA Purebred* as a [derived credentials](../protect/derived-credentials.md) provider on Android Enterprise fully managed devices. Support includes retrieving a derived credential for DISA Purebred. You can use a derived credential for app authentication, Wi-Fi, VPN, or S/MIME signing and/or encryption with apps that support it. 

#### Send push notifications as an action for noncompliance <!-- 1733150   -->
You can now configure an [action for noncompliance](../protect/actions-for-noncompliance.md#available-actions-for-noncompliance) that sends a push notification to a user when their device fails to meet conditions of a compliance policy. The new action is **Send push notification to end user**, and is supported on Android and iOS devices.

When users select the push notification on their device, the Company Portal or Intune app opens to display details about why they are noncompliant.

#### Endpoint security content and new features<!-- 5720009 5892558, 7130145, 5653324, 7140602  -->

The documentation for Intune [Endpoint Security](../protect/endpoint-security.md) is now available. In the endpoint security node of the Microsoft Endpoint Manager admin center you can:

- Create and deploy focused security policies to your managed devices
- Configure integration with Microsoft Defender Advanced Threat Protection, and manage security tasks help remediate risks for at-risk devices as identified by your ATP team
- Configure security baselines
- Manage device compliance and conditional access policies
- View compliance status for all your devices from both Intune and Configuration Manager when Configuration Manager is configured for client attach.

In addition to the availability of content, the following are new for Endpoint Security this month:

- [**Endpoint security policies**](../protect/endpoint-security-policy.md) **are out of** ***preview*** and are now ready to use in production environments, as *generally available*, with two exceptions:

  - In a new *public preview*, you can use the [**Microsoft Defender Firewall rules** profile](../protect/endpoint-security-firewall-policy.md#firewall-profiles) for Windows 10 Firewall policy. With each instance of this profile you can configure up to 150 firewall rules to compliment your Microsoft Defender Firewall profiles. 
  - Account protection security policy remains in preview. 

- You can now [**create a duplicate of endpoint security policies**](../protect/endpoint-security-policy.md#duplicate-a-policy). Duplicates keep the settings configuration of the original policy, but get a new name. Then new policy instance doesn't include any assignments to groups until you edit the new policy instance to add them. You can duplicate the following policies:
  - Antivirus
  - Disk encryption
  - Firewall
  - Endpoint detection and response
  - Attack surface reduction
  - Account protection

- You can now [**create a duplicate of a security baseline**](../protect/security-baselines.md#duplicate-a-security-baseline). Duplicates keep the settings configuration of the original baseline, but get a new name. The new baseline instance doesn't include any assignments to groups until you edit the new baseline instance to add them.

- A new report for endpoint security antivirus policy is available: [**Windows 10 unhealthy endpoints**](../protect/endpoint-security-antivirus-policy.md#windows-10-unhealthy-endpoints). This report is a new page you can select when your viewing your endpoint security antivirus policy. The report displays the antivirus status of your MDM-managed Windows 10 devices.  

#### Support for S/MIME signing and encryption certificates with Outlook on Android<!-- 7207474  -->
You can now use certificates for S/MIME signing and encryption with Outlook on Android. With this support, you can provision these certificates by using SCEP, PKCS, and PKCS imported certificate profiles. The following Android platforms are supported:

- Android Enterprise Work Profile
- Android Device Administrator

Support for Android Enterprise Fully Managed devices is coming soon.

For more information about this support, see [Sensitivity labeling and protection in Outlook for iOS and Android](/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/sensitive-labeling-and-protection-outlook-for-ios-android) in the Exchange documentation.


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Monitor and troubleshoot

#### Device reports UI update<!-- 6269408 -->
The reports overview pane will now provide a **Summary** and a **Reports** tab. In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Reports**, then select the **Reports** tab to see the available report types. For related information, see [Intune reports](reports.md).


<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Scripting

#### macOS script support<!-- 6376978  -->
Script support for macOS is now generally available. In addition, we have added support for both user assigned scripts and macOS devices that have been enrolled with Apple's Automated Device Enrollment (formerly Device Enrollment Program). For more information, see [Use shell scripts on macOS devices in Intune](../apps/macos-shell-scripts.md).


<!-- ########################## -->
## Week of May 4, 2020  

### Company Portal for Android guides users to get apps after work profile enrollment <!-- 6103999 -->
We've improved the in-app guidance in Company Portal to make it easier for users to find and install apps. After they enroll in work profile management, users will get a message explaining how to find suggested apps in the badged version of Google Play. The last step in [Enroll device with Android profile](../user-help/enroll-device-android-work-profile.md) has been updated to show the new message. Users will also see a new **Get Apps** link in the Company Portal drawer on the left. To make way for these new and improved experiences, the **APPS** tab was removed. To see the updated screens, go to [UI updates for Intune end-user apps](./whats-new-app-ui.md). 

<!-- ########################## -->
## Week of April 20, 2020

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### Device management

#### Microsoft Endpoint Manager tenant attach: Device sync and device actions<!-- 6317104, CM3555758  -->
Microsoft Endpoint Manager is bringing together Configuration Manager and Intune into a single console. Starting in Configuration Manager version 2002, you can upload your Configuration Manager devices to the cloud service and take actions on them in the admin center. For more information, see [Microsoft Endpoint Manager tenant attach: Device sync and device actions](../../configmgr/tenant-attach/device-sync-actions.md). 

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### App management

#### Microsoft Office 365 ProPlus rename<!-- 6368143 -->
Microsoft Office 365 ProPlus is being renamed to **Microsoft 365 Apps for enterprise**. To learn more, see [Name change for Office 365 ProPlus](/deployoffice/name-change). In our documentation, we'll commonly refer to it as Microsoft 365 Apps. In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), you can find the apps suite by selecting **Apps** > **Windows** > **Add**. For information about adding apps, see [Add apps to Microsoft Intune](../apps/apps-add.md).

<!-- ########################## -->
## Week of April 13, 2020 (2004 Service release)

<!-- vvvvvvvvvvvvvvvvvvvvvv -->
### App management

#### Manage S/MIME settings for Outlook on Android Enterprise devices<!-- 6517085   -->
You can use app configuration policies to manage the S/MIME setting for Outlook on devices that run Android Enterprise. You can also choose whether or not to allow the device users to enable or disable S/MIME in Outlook settings. To use app configuration policies for Android, in the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) go to **Apps** > **App configuration policies** > **Add** > **Managed devices**. For more information about configuring settings for Outlook, see [Microsoft Outlook configuration settings](../apps/app-configuration-policies-outlook.md).

#### Pre-release testing for Managed Google Play apps<!-- 2681933  -->
Organizations that are using [Google Play's closed test tracks for app pre-release testing](https://support.google.com/googleplay/android-developer/answer/3131213) can manage these tracks with Intune. You can selectively assign apps that are published to Google Play's pre-production tracks to pilot groups in order to perform testing. In Intune, you can see whether an app has a pre-production build test track published to it, as well as be able to assign that track to Azure AD user or device groups. This feature is available for all of our currently supported Android Enterprise scenarios (work profile, fully managed, and dedicated). In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), you can add a Managed Google Play app by selecting **Apps** > **Android** > **Add**. For more information, see [Working with Managed Google Play Closed Testing Tracks](../apps/apps-add-android-for-work.md#working-with-managed-google-play-closed-testing-tracks).

#### Microsoft Teams is now included in Microsoft 365 for macOS<!-- 5903936  -->
Users who are assigned Microsoft 365 for macOS in Microsoft Endpoint Manager will now receive Microsoft Teams in addition to the existing Microsoft 365 apps (Word, Excel, PowerPoint, Outlook, and OneNote). Intune will recognize the existing Mac devices that have the other Office for macOS apps installed, and will attempt to install Microsoft Teams the next time the device checks in with Intune. In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), you can find the **Office 365 Suite** for macOS by selecting **Apps** > **macOS** > **Add**. For more information, see [Assign Office 365 to macOS devices with Microsoft Intune](../apps/apps-add-office365-macos.md).

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
For more information, see [Delete an ADE token from Intune](../enrollment/device-enrollment-program-enroll-ios.md#delete-an-automated-device-enrollment-token-from-intune).

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

Derived credentials rely on the use of a Personal Identity Verification (PIV) or Common Access Card (CAC) card, like a smart card. To get a derived credential for their mobile device, users start in the Microsoft Intune app and follow an enrollment workflow that is unique to the provider you use. Common to all providers is the requirement to use a smart card on a computer to authenticate to the derived credential provider. That provider then issues a certificate to the device that's derived from the user's smart card.

You can use derived credentials as the authentication method for device configuration profiles for VPN and WiFi. You can also use them for app authentication, and S/MIME signing and encryption for applications that support it.

Intune now supports the following derived credential providers with Android:
- Entrust Datacard
- Intercede

A third provider, DISA Purebred, will be available for Android in a future release.

#### Microsoft Edge security baseline is now Generally Available<!--6586139 -->

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
When you create a profile for Android or Android Enterprise devices, the experience in the Endpoint Management admin center is updated. This change impacts the following device configuration profiles (**Devices** > **Configuration Profiles** > **Create profile** > **Android device administrator** or **Android Enterprise** for platform):

- Device restrictions: Android device administrator
- Device restrictions: Android Enterprise device owner
- Device restrictions: Android Enterprise work profile

For more information on the device restrictions you can configure, see [Android device administrator](../configuration/device-restrictions-android.md) and [Android Enterprise](../configuration/device-restrictions-android-for-work.md).

### Improved user interface experience when creating configuration profiles on iOS/iPadOS and macOS devices<!-- 5569002 5568997 -->
When you create a profile for iOS or macOS devices, the experience in the Endpoint Management admin center is updated. This change impacts the following device configuration profiles (**Devices** > **Configuration Profiles** > **Create profile** > **iOS/iPadOS** or **macOS** for platform):

- Custom: iOS/iPadOS, macOS
- Device features: iOS/iPadOS, macOS
- Device restrictions: iOS/iPadOS, macOS
- Endpoint protection: macOS
- Extensions: macOS
- Preference file: macOS

### Hide from user configuration setting in device features on macOS devices<!-- 6524869 -->

When you create a device features configuration profile on macOS devices, there's a new **Hide from user configuration** setting (**Devices** > **Configuration profiles** > **Create profile** > **macOS** for platform > **Device features** for profile > **Login items**).

This feature sets an app's hide checkmark in the **Users & Groups** login items apps list on macOS devices. Existing profiles show this setting within the list as unconfigured. To configure this setting, administrators can update existing profiles.

When set to **Hide**, the hide checkbox is checked for the app, and users can't change it. It also hides the app from users after users sign in to their devices.

> [!div class="mx-imgBorder"]
> ![Hide apps on macOS devices after users sign in to the device in Microsoft Intune and Endpoint Manager](./media/whats-new/macos-hide-checkmark-users-groups-login-items-apps-list.png)

For more information on the setting you can configure, see [macOS device feature settings](../configuration/macos-device-features-settings.md).

This feature applies to:

- macOS

<!-- ########################## -->
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

#### Guide users from Android device administrator management to work profile management<!--5857738   -->
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
Additional device inventory properties are available using the Intune Data Warehouse. The following properties are now exposed via the [devices](../developer/reports-ref-devices.md#devices) beta collection:
- `ethernetMacAddress` -  The unique network identifier of this device.
- `model` - The device model.
- `office365Version` - The version of Microsoft 365 that is installed on the device.
- `windowsOsEdition` - The Operating System version.

The following properties are now exposed via the [devicePropertyHistory](../developer/reports-ref-devices.md#devicepropertyhistories) beta collection:
- `physicalMemoryInBytes` - The physical memory in bytes.
- `totalStorageSpaceInBytes` - Total storage capacity in bytes.

For more information, see [Microsoft Intune Data Warehouse API](../developer/reports-nav-intune-data-warehouse.md).

#### Help and support workflow update to support additional services<!-- 5654170   -->
We've updated the Help and support page in the Microsoft Endpoint Manager admin center where you now [choose the management type you use](get-support.md#options-to-access-help-and-support). With this change you'll be able to select from the following management types:

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
    - **Antivirus** - Manage [Antivirus policy settings](../protect/antivirus-microsoft-defender-settings-macos.md) for macOS to manage [Microsoft Defender ATP for Mac](/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac).

  - Windows 10 and later:
    - **Microsoft Defender Antivirus** - Manage [Antivirus policy settings](../protect/antivirus-microsoft-defender-settings-windows.md) for cloud protection, Antivirus exclusions, remediation, scan options, and more.

      The Antivirus profile for *Microsoft Defender Antivirus* is an exception that introduces a new instance of settings that are found as part of a device restriction profile. These new Antivirus settings:

        - Are the same settings as found in device restrictions, but support a third option for configuration that's not available when configured as a device restriction.
        - Apply to devices that are co-managed with Configuration Manager, when the [co-management workload slider](/configmgr/comanage/how-to-switch-workloads) for Endpoint Protection is set to Intune.

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
Microsoft Endpoint Manager is bringing together Configuration Manager and Intune into a single console. Starting in Configuration Manager technical preview version 2002.2, you can upload your Configuration Manager devices to the cloud service and take actions on them in the admin center. For more information, see [Features in Configuration Manager technical preview version 2002.2](/configmgr/core/get-started/2020/technical-preview-2002-2#bkmk_attach).

Review the [Configuration Manager technical preview article](/configmgr/core/get-started/technical-preview) before installing this update. This article familiarizes you with the general requirements and limitations for using a technical preview, how to update between versions, and how to provide feedback.

#### Bulk remote actions<!--4576882-->
You can now issue bulk commands for the following remote actions: restart, rename, Autopilot reset, wipe, and delete. To see the new bulk actions, go to [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Devices** > **All devices** > **Bulk actions**.

#### All devices list improved search, sort, and filter<!--6179023-->
The All devices list has been improved for better performance, searching, sorting, and filtering. For more information, see [this Support Tip](https://techcommunity.microsoft.com/t5/intune-customer-success/support-tip-changes-in-all-devices-list-and-reporting-in-intune/ba-p/1220946).  

### App management  
####  Improved sign-in experience in Company Portal for Android    
We've updated the layout of several sign-in screens in the Company Portal app for Android to make the experience more modern, simple, and clean for users. For a look at the improvements, see [What's New in the app UI](./whats-new-app-ui.md).

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
Intune provides an easy way to deploy the Microsoft Defender Advanced Threat Protection (ATP) app for macOS to managed Mac devices. For more information, see [Add Microsoft Defender ATP to macOS devices using Microsoft Intune](../apps/apps-advanced-threat-protection-macos.md) and [Microsoft Defender Advanced Threat Protection for Mac](/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac).  

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

## What's New archive
For previous months, see the [What's New archive](whats-new-archive.md).

## Notices

[!INCLUDE [Intune notices](../includes/intune-notices.md)]
