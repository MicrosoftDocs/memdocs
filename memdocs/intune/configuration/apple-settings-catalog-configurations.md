---
# Required metadata
title: Apple configuration list for Intune settings catalog
description: Use the Microsoft Intune settings catalog to add, configure, or restrict features on Apple devices. This article lists and describes the settings you can configure.
author: beflamm
ms.author: beflamm
manager: dougeby
ms.topic: reference
ms.date: 09/23/2024
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium

# optional metadata
#ROBOTS:
#audience:
ms.reviewer: beflamm, mandia
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
---

# Apple device configuration list in the Intune settings catalog

This article lists and describes the Apple configurations you can manage using a settings catalog policy in Microsoft Intune. 

This articles applies to:

- iOS/iPadOS
- macOS

## Before you begin

- At a minimum, sign into the Intune admin center as a member of the **Policy and Profile Manager** role. For more information on the built-in Intune roles, go to [Role-based access control (RBAC) with Microsoft Intune](../fundamentals/role-based-access-control.md).
- Create a [settings catalog policy](settings-catalog.md).

### How to use this article
This article covers the two types of configurations from Apple's MDM protocol:

- Apple declarative configurations
- Apple MDM payloads

Each section can have links to other documents:
- **Apple platform guides**: The Apple Platform Deployment and Security guides that cover deployment and security features of Apple technology
- **Apple developer**: The developer documentation outlines the device management API that gets updated with every OS release
- **Apple YAML**: Apple GitHub repository that contains setting definitions which are ingested into the settings catalog. Use this to see requirements like applicable OS version, enrollment types, and if supervision is required
- **Intune documentation**: Intune guides for scenario-based configuration like setting up Platform Single Sign On or deploying declarative software updates
- **Known issues**: Updated list of known issues related to each configuration

To aid with manual policy migration, configurations that are in both device configuration templates and settings catalog have a section that maps the template setting to its equivalent in the settings catalog. 

> [!IMPORTANT]
> It's recommended to create all new policies using the settings catalog where possible. Some of the existing device configuration templates are no longer being updated. In a future Intune release, they will be migrated to use the settings catalog policy type and the ability to create new templates will be deprecated. These templates include:
> 
> - Device features 
> - Device restrictions 
> - Endpoint protection (Deprecated) 
> - Extensions (Deprecated)
>   
> Policies that should still be created using templates include:
> 
> - Derived credential
> - Email
> - PKCS certificate
> - PKCS imported certificate
> - SCEP certificate
> - Trusted certificate
> - VPN
> - Wi-Fi
> - Wired network

## Apple declarative configurations

This section is specific to the configurations that are under the Declarative Device Management (DDM) category in the settings catalog. You can learn more about DDM on Apple's website: https://support.apple.com/guide/deployment/depb1bab77f8/1/web/1.0
	
### Passcode
Use the passcode configuration to require that devices have a password or passcode that meet your organization's requirements. This configuration is located in the **Declarative Device Management (DDM)** category of the settings catalog. You can learn more about Passcode through the below documentation:

| Apple Platform Guides | Apple Developer | Apple YAML | Intune documentation
| -------  | ------- | ------- | ------- |
| <ul><li>[Passcodes and passwords](https://support.apple.com/guide/security/sec20230a10d/web)</li><li>[Passcode declarative configuration](https://support.apple.com/guide/deployment/depf72b010a8/1/web/1.0)</li></ul>| [Passcode](https://developer.apple.com/documentation/devicemanagement/passcode)| [Passcode](https://github.com/apple/device-management/blob/release/declarative/declarations/configurations/passcode.settings.yaml)

#### Known issues
- None

### Software Update
Use the Software Update configuration to enforce an update to install at a specific time. This configuration is located in the **Declarative Device Management (DDM)** category of the settings catalog. You can learn more about this configuration through the below documentation:

| Apple Platform Guides | Apple Developer | Apple YAML | Intune documentation
| -------  | ------- | ------- | ------- |
| <ul><li>[Software Update declarative configuration](https://support.apple.com/guide/deployment/depca14ecd4d/1/web/1.0)</li><li>[Installing and enforcing software updates](https://support.apple.com/guide/deployment/depd30715cbb/web)</li></ul>| [Software Update Enforcement Specific](https://developer.apple.com/documentation/devicemanagement/softwareupdateenforcementspecific)| [Software Update Enforcement Specific](https://github.com/apple/device-management/blob/release/declarative/declarations/configurations/softwareupdate.enforcement.specific.yaml)| [Use the settings catalog to configure managed software updates](../protect/managed-software-updates-ios-macos.md) |

#### Known issues
- None

## Apple MDM payload settings

This section is specific to Apple payloads that use the standard MDM channel. A list of these payloads is available on [Apple's website.](https://support.apple.com/guide/deployment/dep5370d089/web)

### FileVault 

Use FileVault configurations to manage disk encryption on macOS devices. These configurations are located in the **Full Disk Encryption** category of the settings catalog. You can learn more about FileVault through the below documentation:

| Apple Platform Guides | Apple Developer | Apple YAML | Intune documentation
| -------  | ------- | ------- | ------- |
| <ul><li>[Introduction to FileVault](https://support.apple.com/guide/deployment/dep82064ec40/web)</li><li>[FileVault payload for Apple devices](https://support.apple.com/guide/deployment/dep32bf53500/web)| <ul><li>[FDEFileVault](https://developer.apple.com/documentation/devicemanagement/fdefilevault)</li><li>[FDEFileVaultOptions](https://developer.apple.com/documentation/devicemanagement/fdefilevaultoptions)</li><li>[FDERecoveryKeyEscrow](https://developer.apple.com/documentation/devicemanagement/fderecoverykeyescrow)</li></ul>|<ul><li>[FileVault](https://github.com/apple/device-management/blob/release/mdm/profiles/com.apple.MCX.FileVault2.yaml)</li><li>[FileVault Options](https://github.com/apple/device-management/blob/release/mdm/profiles/com.apple.MCX(FileVault2).yaml)</li><li>[FileVault Recovery Key Escrow](https://github.com/apple/device-management/blob/release/mdm/profiles/com.apple.security.FDERecoveryKeyEscrow.yaml)</li></ul> | [Encrypt macOS devices (Microsoft Learn)](../protect/encrypt-devices-filevault.md)| 

#### Known issues
- [FileVault failing to enable on macOS devices during Setup Assistant](https://techcommunity.microsoft.com/t5/intune-customer-success/known-issue-filevault-failing-to-enable-on-macos-devices-during/ba-p/4180523)

#### Intune device configuration template to settings catalog mapping

| Endpoint protection template | Settings catalog category| Settings catalog setting |
| -------- | ------- | ------- |
| Enable FileVault  | Full Disk Encryption > FileVault | Enable |
| Escrow location description of personal recovery key | Full Disk Encryption > FileVault Recovery Key Escrow | Location
| Personal recovery key rotation | Full Disk Encryption > FileVault | Recovery Key Rotation In Months |
| Hide recovery key  | Full Disk Encryption > FileVault | Show Recovery Key |
| Disable prompt at sign out | Full Disk Encryption > FileVault | Defer Dont Ask At User Logout |
| Number of times allowed to bypass | Full Disk Encryption > FileVault | Defer Force At User Login Max Bypass Attempts |

### Firewall

Use the Firewall configuration to manage the native macOS application firewall. This configuration is located in the **Security** category of the settings catalog. You can learn more about Firewall through the below documentation:

| Apple Platform Guides | Apple Developer | Apple YAML |
| -------- | ------- | ------- | 
| <ul><li>[Firewall security in macOS](https://support.apple.com/guide/security/seca0e83763f/web) </li><li>[Firewall payload](https://support.apple.com/guide/deployment/dep8d306275f/web)</li></ul> | [Firewall](https://developer.apple.com/documentation/devicemanagement/firewall) | [Firewall (YAML)](https://github.com/apple/device-management/blob/release/mdm/profiles/com.apple.security.firewall.yaml) | 

#### Known issues
- [macOS devices using stealth mode turn non-compliant after upgrading to macOS 15](https://techcommunity.microsoft.com/t5/intune-customer-success/known-issue-macos-devices-using-stealth-mode-turn-non-compliant/ba-p/4250583)

#### Intune device configuration template to settings catalog mapping

| Endpoint protection template | Settings catalog category| Settings catalog setting |
| -------- | ------- | ------- |
| Enable Firewall  | Networking > Firewall | Enable Firewall |
| Block all incoming connections | Networking > Firewall | Block All Incoming
| Apps allowed | Networking > Firewall | Applications (Allowed = True) |
| Apps blocked  | Networking > Firewall | Applications (Allowed = False) |
| Enable stealth mode | Networking > Firewall | Enable Stealth Mode |
	
### System Policy Control (Gatekeeper)
Use the System Policy Control payload to configure Gatekeeper settings. This configuration is located in the **System Policy Control** category of the settings catalog. You can learn more about System Policy Control through the below documentation:

| Apple Platform Guides | Apple Developer | Apple YAML |
| -------- | ------- | ------- | 
| <ul><li>[Gatekeeper and runtime protection](https://support.apple.com/guide/security/sec5599b66df/web) </li><li>[Security MDM payload](https://support.apple.com/guide/deployment/dep61dc030/web)</li></ul>| [SystemPolicyControl](https://developer.apple.com/documentation/devicemanagement/systempolicycontrol)  | [System Policy Control](https://github.com/apple/device-management/blob/release/mdm/profiles/com.apple.systempolicy.control.yaml) | 

#### Known issues
- None

#### Intune device configuration template to settings catalog mapping

| Endpoint protection template | Settings catalog category| Settings catalog setting |
| -------- | ------- | ------- |
| Do not allow user to override Gatekeeper  | System Policy Control > System Policy Control | Enable Assessment |
| Allow apps downloaded from these locations | System Policy Control > System Policy Control | Allow Identified Developers |
	
### System Extensions
Use the System Extensions payload to configure system extensions to be automatically loaded or prevent users from approving specific extensions. This configuration is located in the **System Configuration** category of the settings catalog. You can learn more about System Extensions through the below documentation:

| Apple Platform Guides | Apple Developer | Apple YAML |
| -------- | ------- | ------- | 
| <ul><li>[System and kernel extensions](https://support.apple.com/guide/deployment/system-and-kernel-extensions-in-macos-depa5fb8376f/web) </li><li> [System Extensions](https://support.apple.com/guide/deployment/dep5d1584ca4/web)</li></ul>| [System Extensions](https://developer.apple.com/documentation/devicemanagement/systemextensions) | [System Extensions](https://github.com/apple/device-management/blob/release/mdm/profiles/com.apple.system-extension-policy.yaml)|

#### Known issues
- None

#### Intune device configuration template to settings catalog mapping
| Extensions template | Settings catalog category| Settings catalog setting |
| -------- | ------- | ------- |
| Block User Overrides  | System Configuration > System Extensions | Allow User Overrides |
| Allowed team identifiers | System Configuration > System Extensions | Allowed Team Identifiers
| Allowed system extensions | System Configuration > System Extensions | Allowed System Extensions 
| Allowed system extension types  | System Configuration > System Extensions | Allowed System Extension Types |
