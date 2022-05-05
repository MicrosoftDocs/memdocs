---
# required metadata

title: Settings list for the Windows 10/11 MDM security baseline in Microsoft Intune
titleSuffix: Microsoft Intune
description: View a list of the settings in the Microsoft Intune security baseline for Windows 10/11 MDM security. This list includes the default values for settings as found in the default configuration of the baseline.
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/03/2022
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
zone_pivot_groups: windows-mdm-versions

# optional metadata

#ROBOTS:

#audience:

ms.reviewer: laarrizz 
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: 
  - M365-identity-device-management
  - highpri
---


# Settings in the Windows 10/11 MDM security baseline in Intune 

View the settings that are part of the Windows 10/11 MDM security baseline that you can deploy with Microsoft Intune. This article details the settings in the available versions of the baseline and the default values for each setting. The default baseline configuration represents the recommended configuration for applicable devices. Defaults for one baseline might not match defaults from other security baselines, or from other versions of this baseline.

- To learn about using security baselines with Intune and how to upgrade the baseline version in your security baseline profiles, see [Use security baselines](security-baselines.md).
- The most recent baseline version is **Security Baseline for Windows 10 and later for November 2021**

Each version of a security baseline replaces previous versions. Profiles that were created prior to the availability of a baseline version:

- Will be read-only. You can continue to use those profiles, but can't edit them to change their configuration.
- Can be updated to the latest version. After you update to the current baseline version, you can edit the profile to modify settings.

To understand what's changed with a new version of a baseline from previous versions, use the [Compare baselines](../protect/security-baselines.md#compare-baseline-versions) action. This action is available when you view the *Versions* pane for a baseline. Be sure to select the version of the baseline that you want to view.

To update a security baseline profile to the latest version of that baseline, see [Change the baseline version for a profile](../protect/security-baselines-configure.md#change-the-baseline-version-for-a-profile).

Each versions list of settings identifies:

- The setting name as found in the baseline profile
- The baselines default configuration for the setting, which is the recommended configuration.
- The *Learn more* link from the setting, if the setting's information text includes one. When present, the link opens on-line content that describes how the setting is implemented. This content is usually the CSP content from Windows.

## [November 2021](#tab/nov-2021)

**Security Baseline for Windows 10 and later for November 2021**

### Above Lock

- **Voice activate apps from locked screen**:  
  Baseline default: *Disabled*  
  [Learn More](/windows/client-management/mdm/policy-csp-privacy)

- **Block display of toast notifications**:  
  Baseline default: *Yes*  
  [Learn More](/windows/client-management/mdm/policy-csp-abovelock#abovelock-allowtoasts)  

## App Runtime

- **Microsoft accounts optional for Microsoft store apps**:  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-appruntime#appruntime-allowmicrosoftaccountstobeoptional)
  
  
## Application Management

- **Block app installations with elevated privileges**:  
  Baseline default: *Yes*  
  [Learn more](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-msialwaysinstallwithelevatedprivileges)

- **Block user control over installations**:  
  Baseline default: *Yes*  
  [Learn more](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-msiallowusercontroloverinstall)

- **Block game DVR (desktop only)**:  
  Baseline default: *Yes*  
  [Learn more](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-allowgamedvr)

## Audit

Audit settings configure the events that are generated for the conditions of the setting.

- **Account Logon Audit Credential Validation (Device)**:  
  Baseline default: *Success and Failure*

- **Account Logon Audit Kerberos Authentication Service (Device)**:  
  Baseline default: *None*

- **Account Logon Logoff Audit Account Lockout (Device)**:  
  Baseline default: *Failure*

- **Account Logon Logoff Audit Group Membership (Device)**:  
  Baseline default: *Success*

- **Account Logon Logoff Audit Logon (Device)**:  
  Baseline default: *Success and Failure*

- **Audit Other Logon Logoff Events (Device)**:  
  Baseline default: *Success and Failure*

- **Audit Special Logon (Device)**:  
  Baseline default: *Success*

- **Audit Security Group Management (Device)**:  
  Baseline default: *Success*

- **Audit User Account Management (Device)**:  
  Baseline default: *Success and Failure*

- **Detailed Tracking Audit PNP Activity (Device)**:  
  Baseline default: *Success*

- **Detailed Tracking Audit Process Creation (Device)**:  
  Baseline default: *Success*

- **Object Access Audit Detailed File Share (Device)**:  
  Baseline default: *Failure*

- **Audit File Share Access (Device)**:  
  Baseline default: *Success and Failure*

- **Object Access Audit Other Object Access Events (Device)**:  
  Baseline default: *Success and Failure*

- **Object Access Audit Removable Storage (Device)**:  
  Baseline default: *Success and Failure*

- **Audit Authentication Policy Change (Device)**:  
  Baseline default: *Success*

- **Policy Change Audit MPSSVC Rule Level Policy Change (Device)**:  
  Baseline default: *Success and Failure*

- **Policy Change Audit Other Policy Change Events (Device)**:  
  Baseline default: *Failure*

- **Audit Changes to Audit Policy (Device)**:  
  Baseline default: *Success*

- **Privilege Use Audit Sensitive Privilege Use (Device)**:    Baseline default: *Success and Failure*

- **System Audit Other System Events (Device)**:  
Baseline default: *Success and Failure*

- **System Audit Security State Change (Device)**:  
  Baseline default: *Success*

- **Audit Security System Extension (Device)**:  
  Baseline default: *Success*

- **System Audit System Integrity (Device)**:  
  Baseline default: *Success and Failure*

## Auto Play

- **Auto play default auto run behavior**:  
  Baseline default: *Do not execute*  
  [Learn more](/windows/client-management/mdm/policy-csp-autoplay#autoplay-setdefaultautorunbehavior)

- **Auto play mode**:  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-autoplay#autoplay-turnoffautoplay)

- **Block auto play for non-volume devices**:  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-autoplay#autoplay-disallowautoplayfornonvolumedevices) 

## BitLocker

- **BitLocker removable drive policy**:  
  Baseline default: *Configure*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067140)

  - **Block write access to removable data-drives not protected by BitLocker**:  
    Baseline default: *Yes*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=872540)

## Browser

- **Block Password Manager**:  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067128)

- **Require SmartScreen for Microsoft Edge Legacy**:  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067029)

- **Block malicious site access**:  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067040)

- **Block unverified file download**:  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067023)

- **Prevent user from overriding certificate errors**:  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067126)

## Connectivity

- **Configure secure access to UNC paths**:  
  Baseline default: *Configure Windows to only allow access to the specified UNC paths after fulfilling additional security requirements*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067243)

  - **Hardened UNC path list**:  
    *Not configured by default. Manually add one or more hardened UNC paths.*

- **Block downloading of print drivers over HTTP**:  
  Baseline default: Enabled
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067141)

**Block Internet download for web publishing and online ordering wizards**:  
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067136)

## Credentials Delegation

- **Remote host delegation of non-exportable credentials**:  
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067103)

## Credentials UI

- **Enumerate administrators**:  
  Baseline default: *Disabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067021)

## Data Protection

- **Block direct memory access**:  
  Baseline default: Yes  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067031)

## Device Guard

- **Virtualization based security**:  
  Baseline default: *Enable VBS with secure boot*

- **Enable virtualization based security**:  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067066)

- **Launch system guard**:  
  Baseline default: *Enabled*

- **Turn on credential guard**:  
  Baseline default: *Enable with UEFI lock*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=872424)

## Device Installation


- **Block hardware device installation by setup classes**:  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067048)

  - **Remove matching hardware devices**:  
    Baseline default: *Yes*

  - **Block list**:  
    *Not configured by default. Manually add one or more Identifiers.*







## [December 2020](#tab/dec-2020)

**Security Baseline for Windows 10 and later for December 2020**

### Above Lock

- **Voice activate apps from locked screen**:  
  Baseline default: *Disabled*  
  [Learn More](/windows/client-management/mdm/policy-csp-privacy)

- **Block display of toast notifications**:  
  Baseline default: *Yes*  
  [Learn More](/windows/client-management/mdm/policy-csp-abovelock#abovelock-allowtoasts)  

## App Runtime

- **Microsoft accounts optional for Microsoft store apps**:  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-appruntime#appruntime-allowmicrosoftaccountstobeoptional)
  
  
## Application Management

- **Block app installations with elevated privileges**:  
  Baseline default: *Yes*  
  [Learn more](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-msialwaysinstallwithelevatedprivileges)

- **Block user control over installations**:  
  Baseline default: *Yes*  
  [Learn more](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-msiallowusercontroloverinstall)

- **Block game DVR (desktop only)**:  
  Baseline default: *Yes*  
  [Learn more](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-allowgamedvr)

## Audit

Audit settings configure the events that are generated for the conditions of the setting.

- **Account Logon Audit Credential Validation (Device)**:  
  Baseline default: *Success and Failure*

- **Account Logon Audit Kerberos Authentication Service (Device)**:  
  Baseline default: *None*

- **Account Logon Logoff Audit Account Lockout (Device)**:  
  Baseline default: *Failure*

- **Account Logon Logoff Audit Group Membership (Device)**:  
  Baseline default: *Success*

- **Account Logon Logoff Audit Logon (Device)**:  
  Baseline default: *Success and Failure*

- **Audit Other Logon Logoff Events (Device)**:  
  Baseline default: *Success and Failure*

- **Audit Special Logon (Device)**:  
  Baseline default: *Success*

- **Audit Security Group Management (Device)**:  
  Baseline default: *Success*

- **Audit User Account Management (Device)**:  
  Baseline default: *Success and Failure*

- **Detailed Tracking Audit PNP Activity (Device)**:  
  Baseline default: *Success*

- **Detailed Tracking Audit Process Creation (Device)**:  
  Baseline default: *Success*

- **Object Access Audit Detailed File Share (Device)**:  
  Baseline default: *Failure*

- **Audit File Share Access (Device)**:  
  Baseline default: *Success and Failure*

- **Object Access Audit Other Object Access Events (Device)**:  
  Baseline default: *Success and Failure*

- **Object Access Audit Removable Storage (Device)**:  
  Baseline default: *Success and Failure*

- **Audit Authentication Policy Change (Device)**:  
  Baseline default: *Success*

- **Policy Change Audit MPSSVC Rule Level Policy Change (Device)**:  
  Baseline default: *Success and Failure*

- **Policy Change Audit Other Policy Change Events (Device)**:  
  Baseline default: *Failure*

- **Audit Changes to Audit Policy (Device)**:  
  Baseline default: *Success*

- **Privilege Use Audit Sensitive Privilege Use (Device)**:    Baseline default: *Success and Failure*

- **System Audit Other System Events (Device)**:  
Baseline default: *Success and Failure*

- **System Audit Security State Change (Device)**:  
  Baseline default: *Success*

- **Audit Security System Extension (Device)**:  
  Baseline default: *Success*

- **System Audit System Integrity (Device)**:  
  Baseline default: *Success and Failure*

## Auto Play

- **Auto play default auto run behavior**:  
  Baseline default: *Do not execute*  
  [Learn more](/windows/client-management/mdm/policy-csp-autoplay#autoplay-setdefaultautorunbehavior)

- **Auto play mode**:  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-autoplay#autoplay-turnoffautoplay)

- **Block auto play for non-volume devices**:  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-autoplay#autoplay-disallowautoplayfornonvolumedevices) 

## BitLocker

- **BitLocker removable drive policy**:  
  Baseline default: *Configure*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067140)

  - **Block write access to removable data-drives not protected by BitLocker**:  
    Baseline default: *Yes*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=872540)

## Browser

- **Block Password Manager**:  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067128)

- **Require SmartScreen for Microsoft Edge Legacy**:  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067029)

- **Block malicious site access**:  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067040)

- **Block unverified file download**:  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067023)

- **Prevent user from overriding certificate errors**:  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067126)

## Connectivity

- **Configure secure access to UNC paths**:  
  Baseline default: *Configure Windows to only allow access to the specified UNC paths after fulfilling additional security requirements*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067243)

  - **Hardened UNC path list**:  
    *Not configured by default. Manually add one or more hardened UNC paths.*

- **Block downloading of print drivers over HTTP**:  
  Baseline default: Enabled
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067141)

**Block Internet download for web publishing and online ordering wizards**:  
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067136)

## Credentials Delegation

- **Remote host delegation of non-exportable credentials**:  
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067103)

## Credentials UI

- **Enumerate administrators**:  
  Baseline default: *Disabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067021)

## Data Protection

- **Block direct memory access**:  
  Baseline default: Yes  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067031)

## Device Guard

- **Virtualization based security**:  
  Baseline default: *Enable VBS with secure boot*

- **Enable virtualization based security**:  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067066)

- **Launch system guard**:  
  Baseline default: *Enabled*

- **Turn on credential guard**:  
  Baseline default: *Enable with UEFI lock*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=872424)

### Device Installation

- **Block hardware device installation by setup classes**:  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067048)

  - **Remove matching hardware devices**:  
    Baseline default: *Yes*

  - **Block list**:  
    *Not configured by default. Manually add one or more Identifiers.*














## [August 2020](#tab/aug-2020)

**Security Baseline for Windows 10 and later for August 2020**

- **Voice activate apps from locked screen**:  
  Baseline default: *Disabled*  
  [Learn More](/windows/client-management/mdm/policy-csp-privacy)

- **Block display of toast notifications**:  
  Baseline default: *Yes*  
  [Learn More](/windows/client-management/mdm/policy-csp-abovelock#abovelock-allowtoasts)  

### App Runtime

- **Microsoft accounts optional for Microsoft store apps**:  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-appruntime#appruntime-allowmicrosoftaccountstobeoptional)

### Application Management

- **Block app installations with elevated privileges**:  
  Baseline default: *Yes*  
  [Learn more](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-msialwaysinstallwithelevatedprivileges)

- **Block user control over installations**:  
  Baseline default: *Yes*  
  [Learn more](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-msiallowusercontroloverinstall)

- **Block game DVR (desktop only)**:  
  Baseline default: *Yes*  
  [Learn more](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-allowgamedvr)

### Audit

Audit settings configure the events that are generated for the conditions of the setting.

- **Account Logon Audit Credential Validation (Device)**:  
  Baseline default: *Success and Failure*

- **Account Logon Audit Kerberos Authentication Service (Device)**:  
  Baseline default: *None*

- **Account Logon Logoff Audit Account Lockout (Device)**:  
  Baseline default: *Failure*

- **Account Logon Logoff Audit Group Membership (Device)**:  
  Baseline default: *Success*

- **Account Logon Logoff Audit Logon (Device)**:  
  Baseline default: *Success and Failure*

- **Audit Other Logon Logoff Events (Device)**:  
  Baseline default: *Success and Failure*

- **Audit Special Logon (Device)**:  
  Baseline default: *Success*

- **Audit Security Group Management (Device)**:  
  Baseline default: *Success*

- **Audit User Account Management (Device)**:  
  Baseline default: *Success and Failure*

- **Detailed Tracking Audit PNP Activity (Device)**:  
  Baseline default: *Success*

- **Detailed Tracking Audit Process Creation (Device)**:  
  Baseline default: *Success*

- **Object Access Audit Detailed File Share (Device)**:  
  Baseline default: *Failure*

- **Audit File Share Access (Device)**:  
  Baseline default: *Success and Failure*

- **Object Access Audit Other Object Access Events (Device)**:  
  Baseline default: *Success and Failure*

- **Object Access Audit Removable Storage (Device)**:  
  Baseline default: *Success and Failure*

- **Audit Authentication Policy Change (Device)**:  
  Baseline default: *Success*

- **Policy Change Audit MPSSVC Rule Level Policy Change (Device)**:  
  Baseline default: *Success and Failure*

- **Policy Change Audit Other Policy Change Events (Device)**:  
  Baseline default: *Failure*

- **Audit Changes to Audit Policy (Device)**:  
  Baseline default: *Success*

- **Privilege Use Audit Sensitive Privilege Use (Device)**:    Baseline default: *Success and Failure*

- **System Audit Other System Events (Device)**:  
  Baseline default: *Success and Failure*

- **System Audit Security State Change (Device)**:  
  Baseline default: *Success*

- **Audit Security System Extension (Device)**:  
  Baseline default: *Success*

- **System Audit System Integrity (Device)**:  
  Baseline default: *Success and Failure*

### Auto Play

- **Auto play default auto run behavior**:  
  Baseline default: *Do not execute*  
  [Learn more](/windows/client-management/mdm/policy-csp-autoplay#autoplay-setdefaultautorunbehavior)

- **Auto play mode**:  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-autoplay#autoplay-turnoffautoplay)

- **Block auto play for non-volume devices**:  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-autoplay#autoplay-disallowautoplayfornonvolumedevices) 

### BitLocker

- **BitLocker removable drive policy**:  
  Baseline default: *Configure*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067140)

  - **Block write access to removable data-drives not protected by BitLocker**:  
    Baseline default: *Yes*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=872540)

### Browser

- **Block Password Manager**:  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067128)

- **Require SmartScreen for Microsoft Edge Legacy**:  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067029)

- **Block malicious site access**:  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067040)

- **Block unverified file download**:  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067023)

- **Prevent user from overriding certificate errors**:  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067126)

### Connectivity

- **Configure secure access to UNC paths**:  
  Baseline default: *Configure Windows to only allow access to the specified UNC paths after fulfilling additional security requirements*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067243)

  - **Hardened UNC path list**:  
    *Not configured by default. Manually add one or more hardened UNC paths.*

- **Block downloading of print drivers over HTTP**:  
  Baseline default: Enabled
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067141)

**Block Internet download for web publishing and online ordering wizards**:  
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067136)

## Credentials Delegation

- **Remote host delegation of non-exportable credentials**:  
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067103)

### Credentials UI

- **Enumerate administrators**:  
  Baseline default: *Disabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067021)

### Data Protection

- **Block direct memory access**:  
  Baseline default: Yes  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067031)

### Device Guard

- **Virtualization based security**:  
  Baseline default: *Enable VBS with secure boot*

- **Enable virtualization based security**:  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067066)

- **Launch system guard**:  
  Baseline default: *Enabled*

- **Turn on credential guard**:  
  Baseline default: *Enable with UEFI lock*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=872424)

### Device Installation

- **Hardware device installation by device identifiers**:  
  Baseline default: *Block hardware device installation*
  [Learn more](/windows/client-management/mdm/policy-csp-deviceinstallation#deviceinstallation-preventinstallationofmatchingdeviceids)

  - **Remove matching hardware devices**:  
    Baseline default: *Yes*

  - **Hardware device identifiers that are blocked**:  
    Baseline default: *Yes*

- **Hardware device installation by setup classes**:  
  Baseline default: *Block hardware device installation*
  [Learn more](/windows/client-management/mdm/policy-csp-deviceinstallation#deviceinstallation-preventinstallationofmatchingdevicesetupclasses)

  - **Remove matching hardware devices**:  
    Baseline default:  *No default configuration*

  - **Hardware device identifiers that are blocked**:  
    Baseline default: *No default configuration*

















::: zone pivot="mdm-sept-2020,mdm-december-2020,november-2021"

## Device Lock

For more information, see [Policy CSP - DeviceLock](/windows/client-management/mdm/policy-csp-devicelock) in the Windows documentation.

- **Require password**:  
  Specifies whether device lock is enabled.  
  [Learn more](/windows/client-management/mdm/policy-csp-devicelock#devicelock-devicepasswordenabled)  

  - Baseline default:  Yes
  
  When *Require password* is set to *Yes*, the following settings are available.

  - **Required password**:  
    Determines the type of PIN or password required.  
    [Learn more](/windows/client-management/mdm/policy-csp-devicelock#devicelock-alphanumericdevicepasswordrequired)

    - Baseline default:  Alphanumeric

  - **Password expiration (days)**:  
    The Maximum password age policy setting determines how long (in days) that a password can be used before the system requires the user to change it. You can set passwords to expire after a number of days between 1 and 999, or you can specify that passwords never expire by setting the number of days to 0. If Maximum password age is between 1 and 999 days, the minimum password age must be less than the maximum password age. If Maximum password age is set to 0, Minimum password age can be any value between 0 and 998 days.  
    [Learn more](/windows/security/threat-protection/security-policy-settings/maximum-password-age)

    - Baseline default:  60

  - **Password minimum character set count**:  
    The number of complex element types (uppercase and lowercase letters, numbers, and punctuation) required for a strong PIN or password. PIN enforces the following behavior for desktop and mobile devices: 1 - Digits only 2 - Digits and lowercase letters are required 3 - Digits, lowercase letters, and uppercase letters are required. Not supported in desktop Microsoft accounts and domain accounts. 4 - Digits, lowercase letters, uppercase letters, and special characters are required. Not supported in desktop.  
    [Learn more](/windows/client-management/mdm/policy-csp-devicelock#devicelock-mindevicepasswordcomplexcharacters)

    - Baseline default:  3

  - **Prevent reuse of previous passwords**:  
    Specifies how many passwords are stored in the history that can't be used. The value includes the user's current password. For example, with a setting of *1* the user can't reuse their current password when choosing a new password. A setting of *5* means that a user can't set their new password to their current password or any of their previous four passwords.  
    [Learn more](/windows/client-management/mdm/policy-csp-devicelock#devicelock-devicepasswordhistory)

    - Baseline default:  24

  - **Minimum password length**:  
    The Minimum password length policy setting determines the least number of characters that can make up a password for a user account. You can set a value of between 1 and 14 characters, or you can establish that no password is required by setting the number of characters to 0.  
    [Learn more](/windows/security/threat-protection/security-policy-settings/minimum-password-length)

    - Baseline default:  8


  - **Number of sign-in failures before wiping device**:  
    The number of authentication failures allowed before the device is wiped. A value of 0 disables device wipe functionality.  
    [Learn more](/windows/client-management/mdm/policy-csp-devicelock#devicelock-maxdevicepasswordfailedattempts)

    - Baseline default:  10

  - **Block simple passwords**:  
    Specifies whether PINs or passwords such as "1111" or "1234" are allowed. For the desktop, it also controls the use of picture passwords.  
    [Learn more](/windows/client-management/mdm/policy-csp-devicelock#devicelock-allowsimpledevicepassword)

    - Baseline default:  Yes  
    *A setting of Yes prevents use of simple passwords.*

- **Password minimum age in days**:  
  The Minimum password age policy setting determines how long (in days) that a password must be used before the user can change it. You can set a value between 1 and 998 days, or you can allow password changes immediately by setting the number of days to 0. The minimum password age must be less than the Maximum password age, unless the maximum password age is set to 0, indicating that passwords will never expire. If the maximum password age is set to 0, the minimum password age can be set to any value between 0 and 998.  
  [Learn more](/windows/client-management/mdm/policy-csp-devicelock#devicelock-minimumpasswordage)

  - Baseline default:  1

- **Prevent use of camera**:  
  Disables the lock screen camera toggle switch in PC Settings and prevents a camera from being invoked on the lock screen. By default, users can enable invocation of an available camera on the lock screen. If you enable this setting, users can't enable or disable lock screen camera access in PC Settings, and the camera can't be invoked on the lock screen.  
  [Learn more](/windows/client-management/mdm/policy-csp-devicelock#devicelock-preventenablinglockscreencamera)

  - Baseline default:  Enabled

- **Prevent slide show**:  
  Disables the lock screen slide show settings in PC Settings and prevents a slide show from playing on the lock screen. By default, users can enable a slide show that will run after they lock the machine. If you enable this setting, users can't modify slide show settings in PC Settings, and no slide show can start.  
  [Learn more](/windows/client-management/mdm/policy-csp-devicelock#devicelock-preventlockscreenslideshow)

  - Baseline default:  Enabled. 
![Note] A setting of Enabled prevents slide shows from running.

## DMA Guard

For more information, see [Policy CSP - DmaGuard](/windows/client-management/mdm/policy-csp-dmaguard) in the Windows documentation.

- **Enumeration of external devices incompatible with Kernel DMA Protection**:  
  This policy is intended to provide additional security against external DMA capable devices. It allows for more control over the enumeration of external DMA capable devices incompatible with DMA Remapping/device memory isolation and sandboxing. This policy only takes effect when Kernel DMA Protection is supported and enabled by the system firmware. Kernel DMA Protection is a platform feature that can't be controlled via policy or by end user. It has to be supported by the system at the time of manufacturing. To check if the system supports Kernel DMA Protection, check the Kernel DMA Protection field in the Summary page of MSINFO32.exe.  
  [Learn more](/windows/client-management/mdm/policy-csp-dmaguard#dmaguard-deviceenumerationpolicy)

  - Baseline default:  Block all

## Event Log Service

For more information, see [Policy CSP - EventLogService](/windows/client-management/mdm/policy-csp-eventlogservice) in the Windows documentation.

- **Application log maximum file size in KB**:  
  This policy setting specifies the maximum size of the log file in kilobytes. If you enable this policy setting, you can configure the maximum log file size to be between 1 megabyte (1024 kilobytes) and 2 terabytes (2147483647 kilobytes) in kilobyte increments. If you disable or don't configure this policy setting, the maximum size of the log file is set to the locally configured value. This value can be changed by the local administrator using the Log Properties dialog and it defaults to 20 megabytes.  
  [Learn more](/windows/client-management/mdm/policy-csp-eventlogservice#eventlogservice-specifymaximumfilesizeapplicationlog)

  - Baseline default:  32768

- **Security log maximum file size in KB**:  
  This policy setting specifies the maximum size of the log file in kilobytes. If you enable this policy setting, you can configure the maximum log file size to be between 1 megabyte (1024 kilobytes) and 2 terabytes (2147483647 kilobytes) in kilobyte increments. If you disable or don't configure this policy setting, the maximum size of the log file is set to the locally configured value. This value can be changed by the local administrator using the Log Properties dialog and it defaults to 20 megabytes.  
  [Learn more](/windows/client-management/mdm/policy-csp-eventlogservice#eventlogservice-specifymaximumfilesizesecuritylog)

   - Baseline default:  196608

- **System log maximum file size in KB**:  
  This policy setting specifies the maximum size of the log file in kilobytes. If you enable this policy setting, you can configure the maximum log file size to be between 1 megabyte (1024 kilobytes) and 2 terabytes (2147483647 kilobytes) in kilobyte increments. If you disable or don't configure this policy setting, the maximum size of the log file is set to the locally configured value. This value can be changed by the local administrator using the Log Properties dialog and it defaults to 20 megabytes.  
  [Learn more](/windows/client-management/mdm/policy-csp-eventlogservice#eventlogservice-specifymaximumfilesizesystemlog)

  - Baseline default:  32768

## Experience

For more information, see [Policy CSP - Experience](/windows/client-management/mdm/policy-csp-experience) in the Windows documentation.

- **Block Windows Spotlight**:  
  Allows IT admins to turn off (block) all Windows Spotlight Features. This includes Window spotlight on lock screen, Windows Tips, Microsoft consumer features, and other related features.  
  [Learn more](/windows/client-management/mdm/policy-csp-experience#experience-allowwindowsspotlight)

  - Baseline default:  Yes

  When *Block Windows Spotlight* is set to *Not configured*, Windows Spotlight isn't blocked on devices, and you can then configure the following settings to block selected items for Windows Spotlight:

  - **Block third-party suggestions in Windows Spotlight**:  
    Specifies whether to allow app and content suggestions from third-party software publishers in Windows spotlight features like lock screen spotlight, suggested apps in the Start menu, and Windows tips. Users may still see suggestions for Microsoft features, apps, and services.  
    [Learn more](/windows/client-management/mdm/policy-csp-experience#experience-allowthirdpartysuggestionsinwindowsspotlight)

    - Baseline default:  Not configured

  - **Block consumer specific features**:  
    Allows IT admins to turn on experiences that are typically for consumers only, such as Start suggestions, Membership notifications, Post-OOBE app install, and redirect tiles.  
    [Learn more](/windows/client-management/mdm/policy-csp-experience#experience-allowwindowsconsumerfeatures)

    - Baseline default:  Not configured

::: zone-end
::: zone pivot="mdm-sept-2020"

## Exploit Guard

For more information, see [Policy CSP - ExploitGuard](/windows/client-management/mdm/policy-csp-exploitguard) in the Windows documentation.

- **Upload XML**:  
  Enables the IT admin to push out a configuration that represents the desired system and application mitigation options to all the devices in the organization. The configuration is represented by an XML. Exploit protection helps protect devices from malware that use exploits to spread and infect. You use the Windows Security app or PowerShell to create a set of mitigations (known as a configuration). You can then export this configuration as an XML file and share it with multiple machines on your network so they all have the same set of mitigation settings. You can also convert and import an existing EMET configuration XML file into an exploit protection configuration XML.  
  [Learn more](/windows/client-management/mdm/policy-csp-exploitguard#exploitguard-exploitprotectionsettings)

  - Baseline default:  *Sample xml is provided*

::: zone-end
::: zone pivot="mdm-sept-2020,mdm-december-2020,november-2021"

## File Explorer

For more information, see [Policy CSP - FileExplorer](/windows/client-management/mdm/policy-csp-fileexplorer) in the Windows documentation.  

- **Block data execution prevention**:  
  Disabling data execution prevention can allow certain legacy plug-in applications to function without terminating Explorer.  
  [Learn more](/windows/client-management/mdm/policy-csp-fileexplorer#fileexplorer-turnoffdataexecutionpreventionforexplorer)  

  - Baseline default:  Disabled

- **Block heap termination on corruption**:  
  Disabling heap termination on corruption can allow certain legacy plug-in applications to function without terminating Explorer immediately, although Explorer may still terminate unexpectedly later.  
  [Learn more](/windows/client-management/mdm/policy-csp-fileexplorer#fileexplorer-turnoffheapterminationoncorruption)

  - Baseline default:  Disabled

## Firewall

For more information, see [2.2.2 FW_PROFILE_TYPE]( /openspecs/windows_protocols/ms-fasp/7704e238-174d-4a5e-b809-5f3787dd8acc) in the Windows Protocols documentation.

- **Firewall profile domain**:  
  Specifies the profiles to which the rule belongs: Domain, Private, Public. This value represents the profile for networks that are connected to domains.  
  [Learn more](/openspecs/windows_protocols/ms-fasp/7704e238-174d-4a5e-b809-5f3787dd8acc)

  - **Inbound connections blocked**:  
    - Baseline default:  Yes

  - **Outbound connections required**:  
    - Baseline default:  Yes

  - **Inbound notifications blocked**:  
    - Baseline default:  Yes

  - **Firewall enabled**:  
    - Baseline default:  Allowed

- **Firewall profile public**:  
  Specifies the profiles to which the rule belongs: Domain, Private, Public. This value represents the profile for public networks. These networks are classified as public by the administrators in the server host. The classification happens the first time the host connects to the network. Usually these networks are those at airports, coffee shops, and other public places where the peers in the network or the network administrator aren't trusted.  
  [Learn more](/openspecs/windows_protocols/ms-fasp/7704e238-174d-4a5e-b809-5f3787dd8acc)

  - **Inbound connections blocked**:  
    - Baseline default:  Yes

  - **Outbound connections required**:  
    - Baseline default:  Yes

  - **Inbound notifications blocked**:  
    - Baseline default:  Yes

  - **Firewall enabled**:  
    - Baseline default:  Allowed

  - **Connection security rules from group policy not merged**:  
    - Baseline default:  Yes

  - **Policy rules from group policy not merged**:  
    - Baseline default:  Yes

- **Firewall profile private**:  
  Specifies the profiles to which the rule belongs: Domain, Private, Public. This value represents the profile for private networks.  
  [Learn more](/openspecs/windows_protocols/ms-fasp/7704e238-174d-4a5e-b809-5f3787dd8acc)

  - **Inbound connections blocked**:  
    - Baseline default:  Yes

  - **Outbound connections required**:  
    - Baseline default:  Yes

  - **Inbound notifications blocked**:  
    - Baseline default:  Yes

  - **Firewall enabled**:  
    - Baseline default:  Allowed

## Internet Explorer

For more information, see [Policy CSP - InternetExplorer](/windows/client-management/mdm/policy-csp-internetexplorer) in the Windows documentation.

- **Internet Explorer restricted zone updates to status bar via script**:  
  This policy setting allows you to manage whether a script is allowed to update the status bar within the zone.

  - *If you enable this policy setting*, scripts are allowed to update the status bar.
  - *If you disable or don't configure this policy setting*, scripts aren't allowed to update the status bar.

  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-restrictedsiteszoneallowupdatestostatusbarviascript)

  - Baseline default:  Disabled

- **Internet Explorer internet zone drag and drop or copy and paste files**:  
  This policy setting allows you to manage whether users can drag files or copy and paste files from a source within the zone. If you enable this policy setting, users can drag files or copy and paste files from this zone automatically. If you select Prompt in the drop-down box, users are queried to choose whether to drag or copy files from this zone. If you disable this policy setting, users are prevented from dragging files or copying and pasting files from this zone. If you don't configure this policy setting, users can drag files or copy and paste files from this zone automatically.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-internetzoneallowdraganddropcopyandpastefiles)

  - Baseline default:  Disable

- **Internet Explorer restricted zone .NET Framework reliant components**:  
  Use this policy setting to manage whether .NET Framework components that aren't signed with Authenticode can be executed from Internet Explorer. These components include managed controls referenced from an object tag and managed executables referenced from a link. If you enable this policy setting, Internet Explorer will execute unsigned managed components. If you select Prompt in the drop-down box, Internet Explorer will prompt the user to determine whether to execute unsigned managed components. If you disable this policy setting, Internet Explorer won't execute unsigned managed components. If you don't configure this policy setting, Internet Explorer will not execute unsigned managed components.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-restrictedsiteszoneallownetframeworkreliantcomponents)

  - Baseline default:  Disable

- **Internet Explorer local machine zone do not run antimalware against Active X controls**:  
  This policy setting determines whether Internet Explorer runs antimalware programs against ActiveX controls, to check if they're safe to load on pages. If you enable this policy setting, Internet Explorer won't check with your antimalware program to see if it's safe to create an instance of the ActiveX control. If you disable this policy setting, Internet Explorer always checks with your antimalware program to see if it's safe to create an instance of the ActiveX control. If you don't configure this policy setting, Internet Explorer won't check with your antimalware program to see if it's safe to create an instance of the ActiveX control. Users can turn this behavior on or off, using Internet Explorer Security settings.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-localmachinezonedonotrunantimalwareagainstactivexcontrols)

  - Baseline default:  Disabled

- **Internet Explorer internet zone access to data sources**:  
  This policy setting allows you to manage whether Internet Explorer can access data from another security zone using the Microsoft XML Parser (MSXML) or ActiveX Data Objects (ADO). If you enable this policy setting, users can load a page in the zone that uses MSXML or ADO to access data from another site in the zone. If you select Prompt in the drop-down box, users are queried to choose whether to allow a page to load in the zone that uses MSXML or ADO to access data from another site in the zone. If you disable this policy setting, users can't load a page in the zone that uses MSXML or ADO to access data from another site in the zone. If you don't configure this policy setting, users can't load a page in the zone that uses MSXML or ADO to access data from another site in the zone.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-internetzoneallowaccesstodatasources)  

  - Baseline default:  Disable

- **Internet Explorer restricted zone drag content from different domains within windows**:  
  This policy setting allows you to set options for dragging content from one domain to a different domain when the source and destination are in the same window. If you enable this policy setting and click Enable, users can drag content from one domain to a different domain when the source and destination are in the same window. Users can't change this setting. If you enable this policy setting and click Disable, users can't drag content from one domain to a different domain when the source and destination are in the same window. Users can't change this setting in the Internet Options dialog. In Internet Explorer 10, if you disable this policy setting or don't configure it, users can't drag content from one domain to a different domain when the source and destination are in the same window. Users can change this setting in the Internet Options dialog. In Internet Explorer 9 and earlier versions, if you disable this policy setting or don't configure it, users can drag content from one domain to a different domain when the source and destination are in the same window. Users can't change this setting in the Internet Options dialog.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-restrictedsiteszoneenabledraggingofcontentfromdifferentdomainswithinwindows)  

  - Baseline default:  Disabled

- **Internet Explorer certificate address mismatch warning**:  
  This policy setting allows you to turn on the certificate address mismatch security warning. When this policy setting is on, the user is warned when visiting Secure HTTP (HTTPS) websites that present certificates issued for a different website address. This warning helps prevent spoofing attacks. If you enable this policy setting, the certificate address mismatch warning always appears. If you disable or don't configure this policy setting, the user can choose whether the certificate address mismatch warning appears (by using the Advanced page in the Internet Control panel).  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-allowcertificateaddressmismatchwarning)  

  - Baseline default:  Enabled

- **Internet Explorer restricted zone less privileged sites**:  
  This policy setting allows you to manage whether Web sites from less privileged zones, such as Internet sites, can navigate into this zone. If you enable this policy setting, Web sites from less privileged zones can open new windows in, or navigate into, this zone. The security zone will run without the added layer of security that is provided by the Protection from Zone Elevation security feature. If you select Prompt in the drop-down box, a warning is issued to the user that potentially risky navigation is about to occur. If you disable this policy setting, possibly harmful navigation is prevented. The Internet Explorer security feature is on in this zone as set by Protection from Zone Elevation feature control. If you don't configure this policy setting, possibly harmful navigation is prevented. The Internet Explorer security feature is on in this zone as set by Protection from Zone Elevation feature control.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-internetzoneallowlessprivilegedsites)

  - Baseline default:  Disable

- **Internet Explorer restricted zone automatic prompt for file downloads**:  
  This policy setting determines whether users are prompted for non user-initiated file downloads. Regardless of this setting, users will receive file download dialogs for user-initiated downloads. If you enable this setting, users will receive a file download dialog for automatic download attempts. If you disable or don't configure this setting, file downloads that aren't user-initiated are blocked, and users will see the Notification bar instead of the file download dialog. Users can then click the Notification bar to allow the file download prompt.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-restrictedsiteszoneallowautomaticpromptingforfiledownloads)

  - Baseline default:  Disabled

- **Internet Explorer internet zone .NET Framework reliant components**:  
  This policy setting allows you to manage whether .NET Framework components that aren't signed with Authenticode can be executed from Internet Explorer. These components include managed controls referenced from an object tag and managed executables referenced from a link. If you enable this policy setting, Internet Explorer will execute unsigned managed components. If you select Prompt in the drop-down box, Internet Explorer will prompt the user to determine whether to execute unsigned managed components. If you disable this policy setting, Internet Explorer won't execute unsigned managed components. If you don't configure this policy setting, Internet Explorer will execute unsigned managed components.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-internetzoneallownetframeworkreliantcomponents)

  - Baseline default:  Disable

- **Internet Explorer internet zone allows only approved domains to use tdc ActiveX controls**:  
  This policy setting controls if the user can run the TDC ActiveX control on websites. If you enable this policy setting, the TDC ActiveX control won't run from websites in this zone. If you disable this policy setting, the TDC Active X control will run from all sites in this zone.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-internetzoneallowonlyapproveddomainstousetdcactivexcontrol)

  - Baseline default:  Enabled

- **Internet Explorer restricted zone script initiated windows**:  
  This policy setting allows you to manage restrictions on script-initiated pop-up windows and windows that include the title and status bars. If you enable this policy setting, Windows Restrictions security won't apply in this zone. The security zone runs without the added layer of security provided by this feature. If you disable this policy setting, the possible harmful actions contained in script-initiated pop-up windows and windows that include the title and status bars can't run. This Internet Explorer security feature is on in this zone as dictated by the Scripted Windows Security Restrictions feature control setting for the process. If you don't configure this policy setting, the possible harmful actions contained in script-initiated pop-up windows and windows that include the title and status bars can't run. This Internet Explorer security feature is on in this zone as dictated by the Scripted Windows Security Restrictions feature control setting for the process.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-restrictedsiteszoneallowscriptinitiatedwindows)

  - Baseline default:  Disabled

- **Internet Explorer internet zone include local path when uploading files to server**:  
  This policy setting controls if local path information gets sent when the user is uploading a file via an HTML form. If the local path information is sent, some information may be unintentionally revealed to the server. For instance, files sent from the user's desktop may contain the user name as a part of the path. If you enable this policy setting, path information is sent when the user is uploading a file via an HTML form. If you disable this policy setting, path information is removed when the user is uploading a file via an HTML form. If you don't configure this policy setting, the user can choose whether path information gets sent when they upload a file via an HTML form. By default, path information is sent.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-internetzoneincludelocalpathwhenuploadingfilestoserver)

  - Baseline default:  Disabled

- **Internet Explorer disable processes in enhanced protected mode**:  
  This policy setting determines whether Internet Explorer 11 uses 64-bit processes (for greater security) or 32-bit processes (for greater compatibility) when running in Enhanced Protected Mode on 64-bit versions of Windows. Important: Some ActiveX controls and toolbars may not be available when 64-bit processes are used. If you enable this policy setting, Internet Explorer 11 will use 64-bit tab processes when running in Enhanced Protected Mode on 64-bit versions of Windows. If you disable this policy setting, Internet Explorer 11 will use 32-bit tab processes when running in Enhanced Protected Mode on 64-bit versions of Windows. If you don't configure this policy setting, users can turn this feature on or off using Internet Explorer settings. This feature is turned off by default.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-disableprocessesinenhancedprotectedmode)

  - Baseline default:  Enabled

- **Internet Explorer ignore certificate errors**:  
  This policy setting prevents the user from ignoring Secure Sockets Layer/Transport Layer Security (SSL/TLS) certificate errors that interrupt browsing (such as "expired", "revoked", or "name mismatch" errors) in Internet Explorer. If you enable this policy setting, the user can't continue browsing. If you disable or don't configure this policy setting, the user can ignore certificate errors and continue browsing.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-disableignoringcertificateerrors)

  - Baseline default:  Disabled

- **Internet Explorer internet zone loading of XAML files**:  
  This policy setting allows you to manage the loading of Extensible Application Markup Language (XAML) files. XAML is an XML-based declarative markup language commonly used for creating rich user interfaces and graphics that take advantage of the Windows Presentation Foundation. If you enable this policy setting and set the drop-down box to Enable, XAML files are automatically loaded inside Internet Explorer. The user can't change this behavior. If you set the drop-down box to Prompt, the user is prompted for loading XAML files. If you disable this policy setting, XAML files aren't loaded inside Internet Explorer. The user can't change this behavior. If you don't configure this policy setting, the user can decide whether to load XAML files inside Internet Explorer.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-internetzoneallowloadingofxamlfiles)

  - Baseline default:  Disable

- **Internet Explorer internet zone automatic prompt for file downloads**:  
  This policy setting determines whether users are prompted for non user-initiated file downloads. Regardless of this setting, users will receive file download dialogs for user-initiated downloads. If you enable this setting, users will receive a file download dialog for automatic download attempts. If you disable or don't configure this setting, file downloads that aren't user-initiated are blocked, and users will see the Notification bar instead of the file download dialog. Users can then click the Notification bar to allow the file download prompt.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-internetzoneallowautomaticpromptingforfiledownloads)

  - Baseline default:  Disabled

- **Internet Explorer restricted zone security warning for potentially unsafe files**:  
  This policy setting controls if the "Open File - Security Warning" message appears when the user tries to open executable files or other potentially unsafe files (from an intranet file share by using File Explorer, for example). If you enable this policy setting and set the drop-down box to Enable, these files open without a security warning. If you set the drop-down box to Prompt, a security warning appears before the files open. If you disable this policy setting, these files don't open. If you don't configure this policy setting, the user can configure how the computer handles these files. By default, these files are blocked in the Restricted zone, enabled in the Intranet and Local Computer zones, and set to prompt in the Internet and Trusted zones.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-restrictedsiteszoneshowsecuritywarningforpotentiallyunsafefiles)

  - Baseline default:  Disable

- **Internet Explorer internet zone cross site scripting filter**:  
  This policy controls if the Cross-Site Scripting (XSS) Filter will detect and prevent cross-site script injections into websites in this zone. If you enable this policy setting, the XSS Filter is on for sites in this zone, and the XSS Filter attempts to block cross-site script injections. If you disable this policy setting, the XSS Filter is turned off for sites in this zone, and Internet Explorer permits cross-site script injections.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-internetzoneenablecrosssitescriptingfilter)

  - Baseline default:  Enabled

- **Internet Explorer fallback to SSL3**:  
  This policy setting allows you to block an insecure fallback to SSL 3.0. When this policy is enabled, Internet Explorer will attempt to connect to sites using SSL 3.0 or below when TLS 1.0 or greater fails. To prevent a man-in-the-middle attack, we recommend you don't allow insecure fallback. This policy doesn't affect which security protocols are enabled. If you disable this policy, system defaults are used.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-allowfallbacktossl3)

  - Baseline default:  No sites

- **Internet Explorer encryption support**:  
  This policy setting allows you to turn off support for Transport Layer Security (TLS) 1.0, TLS 1.1, TLS 1.2, Secure Sockets Layer (SSL) 2.0, or SSL 3.0 in the browser. TLS and SSL are protocols that help protect communication between the browser and the target server. When the browser attempts to set up a protected communication with the target server, the browser and server negotiate which protocol and version to use. The browser and server attempt to match each other's list of supported protocols and versions, and they select the most preferred match. If you enable this policy setting, the browser negotiates or doesn't negotiate an encryption tunnel by using the encryption methods that you select from the drop-down list. If you disable or don't configure this policy setting, the user can select which encryption method the browser supports.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-disableencryptionsupport)

  - Baseline default:  2 items:  TLS v1.1 and TLS v1.2  
  *Select the down arrow to display options that you can select for this setting.*

- **Internet Explorer locked down internet zone smart screen**:  
  This policy setting controls whether SmartScreen Filter scans pages in this zone for malicious content. If you enable this policy setting, SmartScreen Filter scans pages in this zone for malicious content. If you disable this policy setting, SmartScreen Filter doesn't scan pages in this zone for malicious content. If you don't configure this policy setting, the user can choose whether SmartScreen Filter scans pages in this zone for malicious content. Note: In Internet Explorer 7, this policy setting controls whether Phishing Filter scans pages in this zone for malicious content.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-lockeddowninternetzoneallowsmartscreenie)

  - Baseline default:  Enabled

- **Internet Explorer restricted zone launch applications and files in an iFrame**:  
  This policy setting allows you to manage whether applications may be run and files may be downloaded from an IFRAME reference in the HTML of the pages in this zone. If you enable this policy setting, users can run applications and download files from IFRAMEs on the pages in this zone without user intervention. If you select Prompt in the drop-down box, users are queried to choose whether to run applications and download files from IFRAMEs on the pages in this zone. If you disable this policy setting, users can't run applications and download files from IFRAMEs on the pages in this zone. If you don't configure this policy setting, users can't run applications and download files from IFRAMEs on the pages in this zone.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-restrictedsiteszonelaunchingapplicationsandfilesiniframe)

  - Baseline default:  Disable

- **Internet Explorer bypass smart screen warnings about uncommon files**:  
  This policy setting determines whether the user can bypass warnings from SmartScreen Filter. SmartScreen Filter warns the user about executable files that Internet Explorer users don't commonly download from the Internet. If you enable this policy setting, SmartScreen Filter warnings block the user. If you disable or don't configure this policy setting, the user can bypass SmartScreen Filter warnings.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-disablebypassofsmartscreenwarningsaboutuncommonfiles)

  - Baseline default:  Disabled

- **Internet Explorer internet zone popup blocker**:  
  This policy setting allows you to manage whether unwanted pop-up windows appear. Pop-up windows that are opened when the end user clicks a link aren't blocked. If you enable this policy setting, most unwanted pop-up windows are prevented from appearing. If you disable this policy setting, pop-up windows aren't prevented from appearing. If you don't configure this policy setting, most unwanted pop-up windows are prevented from appearing.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-internetzoneusepopupblocker)

  - Baseline default:  Enable

- **Internet Explorer processes consistent MIME handling**:  
  Internet Explorer contains dynamic binary behaviors: components that encapsulate specific functionality for the HTML elements to which they're attached. This policy setting controls whether the Binary Behavior Security Restriction setting is prevented or allowed. If you enable this policy setting, binary behaviors are prevented for the File Explorer and Internet Explorer processes. If you disable this policy setting, binary behaviors are allowed for the File Explorer and Internet Explorer processes. If you don't configure this policy setting, binary behaviors are prevented for the File Explorer and Internet Explorer processes.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-consistentmimehandlinginternetexplorerprocesses)  

  - Baseline default:  Enabled

- **Internet Explorer restricted zone java permissions**:  
  This policy setting allows you to manage permissions for Java applets. If you enable this policy setting, you can choose options from the drop-down box. Custom, to control permissions settings individually. Low Safety enables applets to do all operations. Medium Safety enables applets to run in their sandbox (an area in memory outside of which the program can't make calls), plus capabilities like scratch space (a safe and secure storage area on the client computer) and user-controlled file I/O. High Safety enables applets to run in their sandbox. Disable Java to prevent any applets from running. If you disable this policy setting, Java applets can't run. If you don't configure this policy setting, Java applets are disabled.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-restrictedsiteszonejavapermissions)

  - Baseline default:  Disable java

- **Internet Explorer Active X controls in protected mode**:  
  This policy setting prevents ActiveX controls from running in Protected Mode when Enhanced Protected Mode is enabled. When a user has an ActiveX control installed that isn't compatible with Enhanced Protected Mode and a website attempts to load the control, Internet Explorer notifies the user and gives the option to run the website in regular Protected Mode. This policy setting disables this notification and forces all websites to run in Enhanced Protected Mode. Enhanced Protected Mode provides additional protection against malicious websites by using 64-bit processes on 64-bit versions of Windows. For computers running at least Windows 8, Enhanced Protected Mode also limits the locations Internet Explorer can read from in the registry and the file system. When Enhanced Protected Mode is enabled, and a user comes across a website that attempts to load an ActiveX control that isn't compatible with Enhanced Protected Mode, Internet Explorer notifies the user and gives the option to disable Enhanced Protected Mode for that particular website. If you enable this policy setting, Internet Explorer won't give the user the option to disable Enhanced Protected Mode. All Protected Mode websites will run in Enhanced Protected Mode. If you disable or don't configure this policy setting, Internet Explorer notifies users and provides an option to run websites with incompatible ActiveX controls in regular Protected Mode.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-donotallowactivexcontrolsinprotectedmode)

  - Baseline default:  Disabled

- **Internet Explorer restricted zone loading of XAML files**:  
  This policy setting allows you to manage the loading of Extensible Application Markup Language (XAML) files. XAML is an XML-based declarative markup language commonly used for creating rich user interfaces and graphics that take advantage of the Windows Presentation Foundation. If you enable this policy setting and set the drop-down box to Enable, XAML files are automatically loaded inside Internet Explorer. The user can't change this behavior. If you set the drop-down box to Prompt, the user is prompted for loading XAML files. If you disable this policy setting, XAML files aren't loaded inside Internet Explorer. The user can't change this behavior. If you don't configure this policy setting, the user can decide whether to load XAML files inside Internet Explorer.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-restrictedsiteszoneallowloadingofxamlfiles)

  - Baseline default:  Disable

- **Internet Explorer processes scripted window security restrictions**:  
  Internet Explorer allows scripts to programmatically open, resize, and reposition windows of various types. The Window Restrictions security feature restricts popup windows and prohibits scripts from displaying windows in which the title and status bars aren't visible to the user or obfuscate other Windows' title and status bars. If you enable this policy setting, scripted windows are restricted for all processes. If you disable or don't configure this policy setting, scripted windows aren't restricted.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-scriptedwindowsecurityrestrictionsinternetexplorerprocesses)

  - Baseline default:  Enabled

- **Internet Explorer restricted zone run Active X controls and plugins**:  
  This policy setting allows you to manage whether ActiveX controls and plug-ins can run on pages from the specified zone. If you enable this policy setting, controls and plug-ins can run without user intervention. If you selected Prompt in the drop-down box, users are asked to choose whether to allow the controls or plug-in to run. If you disable this policy setting, controls and plug-ins are prevented from running. If you don't configure this policy setting, controls and plug-ins are prevented from running.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-restrictedsiteszonerunactivexcontrolsandplugins)

  - Baseline default:  Disable

- **Internet Explorer restricted zone script Active X controls marked safe for scripting**:  
  This policy setting allows you to manage whether an ActiveX control marked safe for scripting can interact with a script. If you enable this policy setting, script interaction can occur automatically without user intervention. If you select Prompt in the drop-down box, users are queried to choose whether to allow script interaction. If you disable this policy setting, script interaction is prevented from occurring. If you don't configure this policy setting, script interaction is prevented from occurring.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-restrictedsiteszonescriptactivexcontrolsmarkedsafeforscripting)

  - Baseline default:  Disable

- **Internet Explorer restricted zone logon options**:  
  This policy setting allows you to manage settings for sign-in options. If you enable this policy setting, you can choose from the following sign-in options.

  - *Anonymous*  - Use anonymous sign-in to disable HTTP authentication and use the guest account only for the Common Internet File System (CIFS) protocol.

  - *Prompt* - Use prompt for user name and password to query users for user IDs and passwords. After a user is queried, these values can be used silently for the rest of the session.

  - *Automatic sign in only in Intranet zone* - Use this option to query users for user IDs and passwords in other zones. After a user is queried, these values can be used silently for the rest of the session.

  - *Automatic sign in with current user name and password* - Use this option to attempt sign in using Windows NT Challenge Response (also known as NTLM authentication). If the server supports Windows NT Challenge Response, the user's network user name and password are used for sign-in. If the server doesn't support Windows NT Challenge Response, the user is queried to provide the user name and password.

  If you disable this policy setting, sign-in is set to *Automatic sign in only in Intranet zone*. If you don't configure this policy setting, sign-in is set to *Prompt* for username and password.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-restrictedsiteszonelogonoptions)

  - Baseline default:  Anonymous

- **Internet Explorer trusted zone initialize and script Active X controls not marked as safe**:  
  This policy setting allows you to manage ActiveX controls not marked as safe. If you enable this policy setting, ActiveX controls run, loaded with parameters, and scripted without setting object safety for untrusted data or scripts. This setting isn't recommended, except for secure and administered zones. This setting causes both unsafe and safe controls to be initialized and scripted, ignoring the Script ActiveX controls marked safe for scripting option. If you enable this policy setting and select Prompt in the drop-down box, users are queried whether to allow the control to load with parameters or scripted. If you disable this policy setting, ActiveX controls that can't be made safe aren't loaded with parameters or scripted. If you don't configure this policy setting, users are queried whether to allow the control to load with parameters or scripted.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-internetzoneinitializeandscriptactivexcontrolsnotmarkedsafe)

  - Baseline default:  Disable

- **Internet Explorer check server certificate revocation**:  
  This policy setting allows you to manage whether Internet Explorer will check revocation status of servers' certificates. Certificates are revoked when they're compromised or no longer valid, and this option protects users from submitting confidential data to a site that may be fraudulent or not secure. If you enable this policy setting, Internet Explorer will check to see if server certificates have been revoked. If you disable this policy setting, Internet Explorer won't check server certificates to see if they've been revoked. If you don't configure this policy setting, Internet Explorer won't check server certificates to see if they've been revoked.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-checkservercertificaterevocation)

  - Baseline default:  Enabled

- **Internet Explorer internet zone less privileged sites**:  
  This policy setting allows you to manage whether Web sites from less privileged zones, such as Restricted Sites, can navigate into this zone. If you enable this policy setting, Web sites from less privileged zones can open new windows in, or navigate into, this zone. The security zone will run without the added layer of security that is provided by the Protection from Zone Elevation security feature. If you select Prompt in the drop-down box, a warning is issued to the user that potentially risky navigation is about to occur. If you disable this policy setting, possibly harmful navigation is prevented. The Internet Explorer security feature is on in this zone as set by Protection from Zone Elevation feature control. If you don't configure this policy setting, Web sites from less privileged zones can open new windows in, or navigate into, this zone.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-internetzoneallowlessprivilegedsites)

  - Baseline default:  Disable

- **Internet Explorer restricted zone file downloads**:  
  This policy setting allows you to manage whether file downloads are permitted from the zone. This option gets determined by the zone of the page with the link causing the download, not the zone from which the file is delivered. If you enable this policy setting, files can be downloaded from the zone. If you disable this policy setting, files are prevented from being downloaded from the zone. If you don't configure this policy setting, files are prevented from being downloaded from the zone.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-restrictedsiteszoneallowfiledownloads)

  - Baseline default:  Disable

- **Internet Explorer internet zone run .NET Framework reliant components signed with Authenticode**:  
  This policy setting allows you to manage whether .NET Framework components that are signed with Authenticode can be executed from Internet Explorer. These components include managed controls referenced from an object tag and managed executables referenced from a link. If you enable this policy setting, Internet Explorer will execute signed managed components. If you select Prompt in the drop-down box, Internet Explorer will prompt the user to determine whether to execute signed managed components. If you disable this policy setting, Internet Explorer won't execute signed managed components. If you don't configure this policy setting, Internet Explorer won't execute signed managed components.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-internetzonerunnetframeworkreliantcomponentssignedwithauthenticode)

  - Baseline default:  Disable

- **Internet Explorer prevent per user installation of Active X controls**:  
  This policy setting allows you to prevent the installation of ActiveX controls on a per-user basis. If you enable this policy setting, ActiveX controls can't be installed on a per-user basis. If you disable or don't configure this policy setting, ActiveX controls can be installed on a per-user basis.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-preventperuserinstallationofactivexcontrols)

  - Baseline default:  Enabled

- **Internet Explorer prevent managing smart screen filter**:  
  This policy setting prevents the user from managing SmartScreen Filter, which warns the user if the website they visit is known for fraudulent attempts to gather personal information through "phishing," or is known to host malware. If you enable this policy setting, the user isn't prompted to turn on SmartScreen Filter. All website addresses that aren't on the filters allowlist are sent automatically to Microsoft without prompting the user. If you disable or don't configure this policy setting, the user gets prompted to decide whether to turn on SmartScreen Filter during the first-run experience.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-preventmanagingsmartscreenfilter)

  - Baseline default:  Enable

- **Internet Explorer processes MIME sniffing safety feature**:  
  This policy setting determines whether Internet Explorer MIME sniffing will prevent promotion of a file of one type to a more dangerous file type. If you enable this policy setting, MIME sniffing will never promote a file of one type to a more dangerous file type. If you disable this policy setting, Internet Explorer processes will allow a MIME sniff promoting a file of one type to a more dangerous file type. If you don't configure this policy setting, MIME sniffing will never promote a file of one type to a more dangerous file type.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-mimesniffingsafetyfeatureinternetexplorerprocesses)

  - Baseline default:  Enabled

- **Internet Explorer restricted zone download signed Active X controls**:  
  This policy setting allows you to manage whether users may download signed ActiveX controls from a page in the zone. If you enable this policy, users can download signed controls without user intervention. If you select Prompt in the drop-down box, users are queried whether to download controls signed by publishers who aren't trusted. Code signed by trusted publishers is silently downloaded. If you disable the policy setting, signed controls can't download. If you don't configure this policy setting, users are queried whether to download controls signed by publishers who aren't trusted. Code signed by trusted publishers is silently downloaded.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-restrictedsiteszonedownloadsignedactivexcontrols)

  - Baseline default:  Disable

- **Internet Explorer auto complete**:  
  This Auto-Complete feature can remember and suggest User names and passwords on Forms. If you enable this setting, the user can't change "User name and passwords on forms" or "prompt me to save passwords". The Auto Complete feature for User names and passwords on Forms is turned on. Decide whether to select "prompt me to save passwords". If you disable this setting the user can't change "User name and passwords on forms" or "prompt me to save passwords". The Auto Complete feature for User names and passwords on Forms is turned off. The user also can't opt to be prompted to save passwords. If you don't configure this setting, the user has the freedom of turning on Auto complete for User name and passwords on forms and the option of prompting to save passwords. To display this option, the users open the Internet Options dialog box, click the Contents Tab, and click the Settings button.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-allowautocomplete)

  - Baseline default:  Disabled

- **Internet Explorer internet zone allows VBscript to run**:  
  This policy setting lets you decide whether VBScript can run on pages in specific Internet Explorer zones. Options include:

  - *Enable* - VBScript runs on pages in specific zones, without any interaction.

  - *Prompt* - Employees are prompted whether to allow VBScript to run in the zone.

  - *Disable* - VBScript is prevented from running in the zone. If you disable or don't configure this policy setting, VBScript runs without any interaction in the specified zone.

  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-internetzoneallowvbscripttorunininternetexplorer)

  - Baseline default:  Disable

- **Internet Explorer restricted zone allows only approved domains to use tdc Active X controls**:  
  This policy setting controls if the user can run the TDC ActiveX control on websites. If you enable this policy setting, the TDC ActiveX control won't run from websites in this zone. If you disable this policy setting, the TDC Active X control will run from all sites in this zone.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-restrictedsiteszoneallowonlyapproveddomainstousetdcactivexcontrol)

  - Baseline default:  Enabled

- **Internet Explorer trusted zone do not run antimalware against Active X controls**:  
  This policy setting determines whether Internet Explorer runs antimalware programs against ActiveX controls, to check if they're safe to load on pages. If you enable this policy setting, Internet Explorer won't check with your antimalware program to see if it's safe to create an instance of the ActiveX control. If you disable this policy setting, Internet Explorer always checks with your antimalware program to see if it's safe to create an instance of the ActiveX control. If you don't configure this policy setting, Internet Explorer always checks with your antimalware program to see if it's safe to create an instance of the ActiveX control. Users can turn this behavior on or off, using Internet Explorer Security settings.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-trustedsiteszonedonotrunantimalwareagainstactivexcontrols)

  - Baseline default:  Disabled

- **Internet Explorer local machine zone java permissions**:  
  This policy setting allows you to manage permissions for Java applets. If you enable this policy setting, you can choose options from the drop-down box. Custom, to control permissions settings individually. Low Safety enables applets to do all operations. Medium Safety enables applets to run in their sandbox (an area in memory outside of which the program can't make calls), plus capabilities like scratch space (a safe and secure storage area on the client computer) and user-controlled file I/O. High Safety enables applets to run in their sandbox. Disable Java to prevent any applets from running. If you disable this policy setting, Java applets can't run. If you don't configure this policy setting, the permission is set to Medium Safety.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-localmachinezonejavapermissions)

  - Baseline default:  Disable java

- **Internet Explorer intranet zone do not run antimalware against Active X controls**:  
  This policy setting determines whether Internet Explorer runs antimalware programs against ActiveX controls, to check if they're safe to load on pages. If you enable this policy setting, Internet Explorer won't check with your antimalware program to see if it's safe to create an instance of the ActiveX control. If you disable this policy setting, Internet Explorer always checks with your antimalware program to see if it's safe to create an instance of the ActiveX control. If you don't configure this policy setting, Internet Explorer won't check with your antimalware program to see if it's safe to create an instance of the ActiveX control. Users can turn this behavior on or off, using Internet Explorer Security settings.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-intranetzonedonotrunantimalwareagainstactivexcontrols)

  - Baseline default:  Disabled

- **Internet Explorer restricted zone scriptlets**:  
  This policy setting allows you to manage whether the user can run scriptlets. If you enable this policy setting, the user can run scriptlets. If you disable this policy setting, the user can't run scriptlets. If you don't configure this policy setting, the user can enable or disable scriptlets.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-restrictedsiteszoneallowscriptlets)

  - Baseline default:  Disabled

- **Internet Explorer processes notification bar**:  
  This policy setting allows you to manage whether the Notification bar displays for Internet Explorer processes when file or code installs are restricted. By default, the Notification bar displays for Internet Explorer processes. If you enable this policy setting, the Notification bar displays for the Internet Explorer Processes. If you disable this policy setting, the Notification bar won't be displayed for Internet Explorer processes. If you don't configure this policy setting, the Notification bar doesn't display for Internet Explorer Processes.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-notificationbarinternetexplorerprocesses)

  - Baseline default:  Enabled

- **Internet Explorer internet zone download signed ActiveX controls**:  
  This policy setting allows you to manage whether users may download signed ActiveX controls from a page in the zone. If you enable this policy, users can download signed controls without user intervention. If you select Prompt in the drop-down box, users are queried whether to download controls signed by publishers who aren't trusted. Code signed by trusted publishers is silently downloaded. If you disable the policy setting, signed controls can't download. If you don't configure this policy setting, users are queried whether to download controls signed by publishers who aren't trusted. Code signed by trusted publishers is silently downloaded.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-internetzonedownloadsignedactivexcontrols)

  - Baseline default:  Disable

- **Internet Explorer restricted zone smart screen**:  
  This policy setting controls whether SmartScreen Filter scans pages in this zone for malicious content. If you enable this policy setting, SmartScreen Filter scans pages in this zone for malicious content. If you disable this policy setting, SmartScreen Filter doesn't scan pages in this zone for malicious content. If you don't configure this policy setting, the user can choose whether SmartScreen Filter scans pages in this zone for malicious content. Note: In Internet Explorer 7, this policy setting controls whether Phishing Filter scans pages in this zone for malicious content.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-restrictedsiteszoneallowsmartscreenie)

  - Baseline default:  Enabled

- **Internet Explorer remove run this time button for outdated Active X controls**:  
  This policy setting allows you to stop users from seeing the "Run this time" button and from running specific outdated ActiveX controls in Internet Explorer. If you enable this policy setting, users won't see the "Run this time" button on the warning message that appears when Internet Explorer blocks an outdated ActiveX control. If you disable or don't configure this policy setting, users will see the "Run this time" button on the warning message that appears when Internet Explorer blocks an outdated ActiveX control. Clicking this button lets the user run the outdated ActiveX control once. For more information, see "Outdated ActiveX Controls" in the Internet Explorer TechNet library.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-removerunthistimebuttonforoutdatedactivexcontrols)

  - Baseline default:  Enabled

- **Internet Explorer internet zone launch applications and files in an iframe**:  
  This policy setting allows you to manage whether applications can run and if files can download from an IFRAME reference in the HTML of the pages in this zone. If you enable this policy setting, users can run applications and download files from IFRAMEs on the pages in this zone without user intervention. If you select Prompt in the drop-down box, users are queried to choose whether to run applications and download files from IFRAMEs on the pages in this zone. If you disable this policy setting, users can't run applications and download files from IFRAMEs on the pages in this zone. If you don't configure this policy setting, users are queried to choose whether to run applications and download files from IFRAMEs on the pages in this zone.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-internetzonelaunchingapplicationsandfilesiniframe)

  - Baseline default:  Disable

- **Internet Explorer restricted zone navigate windows and frames across different domains**:  
  This policy setting allows you to set options for dragging content from one domain to a different domain when the source and destination are in different windows. If you enable this policy setting and click Enable, users can drag content from one domain to a different domain when the source and destination are in different windows. Users can't change this setting. If you enable this policy setting and click Disable, users can't drag content from one domain to a different domain when both the source and destination are in different windows. Users can't change this setting. In Internet Explorer 10, if you disable this policy setting or don't configure it, users can't drag content from one domain to a different domain when the source and destination are in different windows. Users can change this setting in the Internet Options dialog. In Internet Explorer 9 and earlier versions, if you disable this policy or don't configure it, users can drag content from one domain to a different domain when the source and destination are in different windows. Users can't change this setting.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-restrictedsiteszoneenabledraggingofcontentfromdifferentdomainsacrosswindows)

  - Baseline default:  Disable

- **Internet Explorer internet zone smart screen**:  
  This policy setting controls whether SmartScreen Filter scans pages in this zone for malicious content. If you enable this policy setting, SmartScreen Filter scans pages in this zone for malicious content. If you disable this policy setting, SmartScreen Filter doesn't scan pages in this zone for malicious content. If you don't configure this policy setting, the user can choose whether SmartScreen Filter scans pages in this zone for malicious content. Note: In Internet Explorer 7, this policy setting controls whether Phishing Filter scans pages in this zone for malicious content.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-internetzoneallowsmartscreenie)

  - Baseline default:  Enabled

- **Internet Explorer locked down trusted zone java permissions**:  
  This policy setting allows you to manage permissions for Java applets. If you enable this policy setting, you can choose options from the drop-down box. Custom, to control permissions settings individually. Low Safety enables applets to do all operations. Medium Safety enables applets to run in their sandbox (an area in memory outside of which the program can't make calls), plus capabilities like scratch space (a safe and secure storage area on the client computer) and user-controlled file I/O. High Safety enables applets to run in their sandbox. Disable Java to prevent any applets from running. If you disable this policy setting, Java applets can't run. If you don't configure this policy setting, Java applets are disabled.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-lockeddowntrustedsiteszonejavapermissions)

  - Baseline default:  Disable java

- **Internet Explorer check signatures on downloaded programs**:  
  This policy setting allows you to manage whether Internet Explorer checks for digital signatures (which identifies the publisher of signed software and verifies it hasn't been modified or tampered with) on user computers before downloading executable programs. If you enable this policy setting, Internet Explorer will check the digital signatures of executable programs and display their identities before downloading them to user computers. If you disable this policy setting, Internet Explorer won't check the digital signatures of executable programs or display their identities before downloading them to user computers. If you don't configure this policy, Internet Explorer won't check the digital signatures of executable programs or display their identities before downloading them to user computers.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-checksignaturesondownloadedprograms)

  - Baseline default:  Enabled

- **Internet Explorer restricted zone scripting of web browser controls**:  
  This policy setting determines whether a page can control embedded WebBrowser controls via script. If you enable this policy setting, script access to the WebBrowser control is allowed. If you disable this policy setting, script access to the WebBrowser control isn't allowed. If you don't configure this policy setting, the user can enable or disable script access to the WebBrowser control. By default, script access to the WebBrowser control is allowed only in the Local Machine and Intranet zones.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-restrictedsiteszoneallowscriptingofinternetexplorerwebbrowsercontrols)

  - Baseline default:  Disabled

- **Internet Explorer restricted zone cross site scripting filter**:  
  This policy controls if the Cross-Site Scripting (XSS) Filter will detect and prevent cross-site script injections into websites in this zone. If you enable this policy setting, the XSS Filter is on for sites in this zone, and the XSS Filter attempts to block cross-site script injections. If you disable this policy setting, the XSS Filter is turned off for sites in this zone, and Internet Explorer permits cross-site script injections.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-restrictedsiteszoneenablecrosssitescriptingfilter)

  - Baseline default:  Enabled

- **Internet Explorer restricted zone binary and script behaviors**:  
  This policy setting allows you to manage dynamic binary and script behaviors: components that encapsulate specific functionality for HTML elements to which they were attached. If you enable this policy setting, binary and script behaviors are available. If you select Administrator approved in the drop-down box, only behaviors listed in the Admin-approved Behaviors under Binary Behaviors Security Restriction policy are available. If you disable this policy setting, binary and script behaviors aren't available unless applications have implemented a custom security manager. If you don't configure this policy setting, binary and script behaviors aren't available unless applications have implemented a custom security manager.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-restrictedsiteszoneallowbinaryandscriptbehaviors)

  - Baseline default:  Disable

- **Internet Explorer security settings check**:  
  This policy setting turns off the Security Settings Check feature, which checks Internet Explorer security settings to determine when the settings put Internet Explorer at risk. If you enable this policy setting, the feature is turned off. If you disable or don't configure this policy setting, the feature is turned on.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-disablesecuritysettingscheck)

  - Baseline default:  Enabled

- **Internet Explorer internet zone security warning for potentially unsafe files**:  
  This policy setting controls if the "Open File - Security Warning" message appears when the user tries to open executable files or other potentially unsafe files (from an intranet file share by using File Explorer, for example). If you enable this policy setting and set the drop-down box to Enable, these files open without a security warning. If you set the drop-down box to Prompt, a security warning appears before the files open. If you disable this policy setting, these files don't open. If you don't configure this policy setting, the user can configure how the computer handles these files. By default, these files are blocked in the Restricted zone, enabled in the Intranet and Local Computer zones, and set to prompt in the Internet and Trusted zones.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-internetzoneshowsecuritywarningforpotentiallyunsafefiles)

  - Baseline default:  Prompt

- **Internet Explorer intranet zone java permissions**:  
  This policy setting allows you to manage permissions for Java applets. If you enable this policy setting, you can choose options from the drop-down box. Custom, to control permissions settings individually. Low Safety enables applets to do all operations. Medium Safety enables applets to run in their sandbox (an area in memory outside of which the program can't make calls), plus capabilities like scratch space (a safe and secure storage area on the client computer) and user-controlled file I/O. High Safety enables applets to run in their sandbox. Disable Java to prevent any applets from running. If you disable this policy setting, Java applets can't run. If you don't configure this policy setting, the permission is set to Medium Safety.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-intranetzonejavapermissions)

  - Baseline default:  High safety

- **Internet Explorer block outdated Active X controls**:  
  This policy setting determines whether Internet Explorer blocks specific outdated ActiveX controls. Outdated ActiveX controls are never blocked in the Intranet Zone. If you enable this policy setting, Internet Explorer stops blocking outdated ActiveX controls. If you disable or don't configure this policy setting, Internet Explorer continues to block specific outdated ActiveX controls. For more information, see "Outdated ActiveX Controls" in the Internet Explorer TechNet library.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-donotblockoutdatedactivexcontrols)

  - Baseline default:  Enabled

- **Internet Explorer restricted zone popup blocker**:  
  This policy setting allows you to manage whether unwanted pop-up windows appear. Pop-up windows that are opened when the end user clicks a link aren't blocked. If you enable this policy setting, most unwanted pop-up windows are prevented from appearing. If you disable this policy setting, pop-up windows aren't prevented from appearing. If you don't configure this policy setting, most unwanted pop-up windows are prevented from appearing.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-restrictedsiteszoneusepopupblocker)

  - Baseline default:  Enable

- **Internet Explorer processes MK protocol security restriction**:  
  The MK Protocol Security Restriction policy setting reduces attack surface area by preventing the MK protocol. Resources hosted on the MK protocol will fail. If you enable this policy setting, the MK Protocol is prevented for File Explorer and Internet Explorer, and resources hosted on the MK protocol will fail. If you disable this policy setting, applications can use the MK protocol API. Resources hosted on the MK protocol will work for the File Explorer and Internet Explorer processes. If you don't configure this policy setting, the MK Protocol is prevented for File Explorer and Internet Explorer, and resources hosted on the MK protocol will fail.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-mkprotocolsecurityrestrictioninternetexplorerprocesses)

  - Baseline default:  Enabled

- **Internet Explorer trusted zone java permissions**:  
  This policy setting allows you to manage permissions for Java applets. If you enable this policy setting, you can choose options from the drop-down box. Custom, to control permissions settings individually. Low Safety enables applets to do all operations. Medium Safety enables applets to run in their sandbox (an area in memory outside of which the program can't make calls), plus capabilities like scratch space (a safe and secure storage area on the client computer) and user-controlled file I/O. High Safety enables applets to run in their sandbox. Disable Java to prevent any applets from running. If you disable this policy setting, Java applets can't run. If you don't configure this policy setting, the permission is set to Low Safety.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-trustedsiteszonejavapermissions)

  - Baseline default:  High safety

- **Internet Explorer restricted zone scripting of java applets**:  
  This policy setting allows you to manage whether applets are exposed to scripts within the zone. If you enable this policy setting, scripts can access applets automatically without user intervention. If you select Prompt in the drop-down box, users are queried to choose whether to allow scripts to access applets. If you disable this policy setting, scripts are prevented from accessing applets. If you don't configure this policy setting, scripts are prevented from accessing applets.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-restrictedsiteszonescriptingofjavaapplets)

  - Baseline default:  Disable

- **Internet Explorer locked down restricted zone java permissions**:  
  This policy setting allows you to manage permissions for Java applets. If you enable this policy setting, you can choose options from the drop-down box. Custom, to control permissions settings individually. Low Safety enables applets to do all operations. Medium Safety enables applets to run in their sandbox (an area in memory outside of which the program can't make calls), plus capabilities like scratch space (a safe and secure storage area on the client computer) and user-controlled file I/O. High Safety enables applets to run in their sandbox. Disable Java to prevent any applets from running. If you disable this policy setting, Java applets can't run. If you don't configure this policy setting, Java applets are disabled.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-lockeddownrestrictedsiteszonejavapermissions)

  - Baseline default:  Disable Java

- **Internet Explorer internet zone allows only approved domains to use ActiveX controls**:  
  This policy setting controls if the user is prompted to allow ActiveX controls to run on websites other than the website that installed the ActiveX control. If you enable this policy setting, the user is prompted before ActiveX controls can run from websites in this zone. The user can choose to allow the control to run from the current site or from all sites. If you disable this policy setting, the user doesn't see the per-site ActiveX prompt, and ActiveX controls can run from all sites in this zone.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-internetzoneallowonlyapproveddomainstouseactivexcontrols)

  - Baseline default:  Enabled

- **Internet Explorer includes all network paths**:  
  Internet Explorer includes all network paths.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-includeallnetworkpaths)

  - Baseline default:  Disabled

- **Internet Explorer internet zone protected mode**:  
  This policy setting allows you to turn on Protected Mode. Protected Mode helps protect Internet Explorer from exploited vulnerabilities by reducing the locations that Internet Explorer can write to in the registry and the file system. If you enable this policy setting, Protected Mode is turned on. The user can't turn off Protected Mode. If you disable this policy setting, Protected Mode is turned off. The user can't turn on Protected Mode. If you don't configure this policy setting, the user can turn on or turn off Protected Mode.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-internetzoneenableprotectedmode)

  - Baseline default:  Enable

- **Internet Explorer internet zone initialize and script Active X controls not marked as safe**:  
  This policy setting allows you to manage ActiveX controls not marked as safe. If you enable this policy setting, ActiveX controls run, loaded with parameters, and scripted without setting object safety for untrusted data or scripts. This setting isn't recommended, except for secure and administered zones. This setting causes both unsafe and safe controls to be initialized and scripted, ignoring the Script ActiveX controls marked safe for scripting option. If you enable this policy setting and select Prompt in the drop-down box, users are queried whether to allow the control to load with parameters or scripted. If you disable this policy setting, ActiveX controls that can't be made safe aren't loaded with parameters or scripted. If you don't configure this policy setting, ActiveX controls that can't be made safe aren't loaded with parameters or scripted.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-internetzoneinitializeandscriptactivexcontrolsnotmarkedsafe)

  - Baseline default:  Disable

- **Internet Explorer locked down restricted zone smart screen**:  
  This policy setting controls whether SmartScreen Filter scans pages in this zone for malicious content. If you enable this policy setting, SmartScreen Filter scans pages in this zone for malicious content. If you disable this policy setting, SmartScreen Filter doesn't scan pages in this zone for malicious content. If you don't configure this policy setting, the user can choose whether SmartScreen Filter scans pages in this zone for malicious content. Note: In Internet Explorer 7, this policy setting controls whether Phishing Filter scans pages in this zone for malicious content.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-restrictedsiteszoneallowsmartscreenie)

  - Baseline default:  Enabled

- **Internet Explorer crash detection**:  
  This policy setting allows you to manage the crash detection feature of add-on Management. If you enable this policy setting, a crash in Internet Explorer will exhibit behavior found in Windows XP Professional Service Pack 1 and earlier, namely to invoke Windows Error Reporting. All policy settings for Windows Error Reporting continue to apply. If you disable or don't configure this policy setting, the crash detection feature for add-on management is functional.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-disablecrashdetection)

  - Baseline default:  Disabled

- **Internet Explorer internet zone java permissions**:  
  This policy setting allows you to manage permissions for Java applets. If you enable this policy setting, you can choose options from the drop-down box. Custom, to control permissions settings individually. Low Safety enables applets to do all operations. Medium Safety enables applets to run in their sandbox (an area in memory outside of which the program can't make calls), plus capabilities like scratch space (a safe and secure storage area on the client computer) and user-controlled file I/O. High Safety enables applets to run in their sandbox. Disable Java to prevent any applets from running. If you disable this policy setting, Java applets can't run. If you don't configure this policy setting, the permission is set to High Safety.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-internetzonejavapermissions)

  - Baseline default:  Disable java

- **Internet Explorer restricted zone active scripting**:  
  This policy setting allows you to manage whether script code on pages in the zone is run. If you enable this policy setting, script code on pages in the zone can run automatically. If you select Prompt in the drop-down box, users are queried to choose whether to allow script code on pages in the zone to run. If you disable this policy setting, script code on pages in the zone is prevented from running. If you don't configure this policy setting, script code on pages in the zone is prevented from running.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-restrictedsiteszoneallowactivescripting)

  - Baseline default:  Disable

- **Internet Explorer internet zone logon options**:  
  This policy setting allows you to manage settings for sign-in options. If you enable this policy setting, you can choose from the following sign-in options. Anonymous log on to disable HTTP authentication and use the guest account only for the Common Internet File System (CIFS) protocol. Prompt for user name and password to query users for user IDs and passwords. After a user is queried, these values can be used silently for the remainder of the session. Automatic log on only in Intranet zone to query users for user IDs and passwords in other zones. After a user is queried, these values can be used silently for the rest of the session. Automatic sign in with current user name and password to attempt log on using Windows NT Challenge Response (also known as NTLM authentication). If the server supports Windows NT Challenge Response, the sign-in uses the user's network user name and password for log-on. If the server doesn't support Windows NT Challenge Response, the user is queried to provide the user name and password. If you disable this policy setting, sign-in is set to Automatic log on only in Intranet zone. If you don't configure this policy setting, sign-in is set to Automatic sign in only in Intranet zone.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-internetzonelogonoptions)

  - Baseline default:  Prompt

- **Internet Explorer restricted zone allows VBScript to run**:  
  This policy setting allows you to manage whether VBScript can run on pages from the specified zone in Internet Explorer. If you selected Enable in the drop-down box, VBScript can run without user intervention. If you selected Prompt in the drop-down box, users are asked to choose whether to allow VBScript to run. If you selected Disable in the drop-down box, VBScript is prevented from running. If you don't configure or disable this policy setting, VBScript is prevented from running.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-restrictedsiteszoneallowvbscripttorunininternetexplorer)

  - Baseline default:  Disable

- **Internet Explorer internet zone drag content from different domains across windows**:  
  This policy setting allows you to set options for dragging content from one domain to a different domain when the source and destination are in different windows. If you enable this policy setting and click Enable, users can drag content from one domain to a different domain when the source and destination are in different windows. Users can't change this setting. If you enable this policy setting and click Disable, users can't drag content from one domain to a different domain when both the source and destination are in different windows. Users can't change this setting. In Internet Explorer 10, if you disable this policy setting or don't configure it, users can't drag content from one domain to a different domain when the source and destination are in different windows. Users can change this setting in the Internet Options dialog. In Internet Explorer 9 and earlier versions, if you disable this policy or don't configure it, users can drag content from one domain to a different domain when the source and destination are in different windows. Users can't change this setting.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-internetzoneenabledraggingofcontentfromdifferentdomainsacrosswindows)

  - Baseline default:  Disabled

- **Internet Explorer intranet zone initialize and script Active X controls not marked as safe**:  
  This policy setting allows you to manage ActiveX controls not marked as safe. If you enable this policy setting, ActiveX controls run, loaded with parameters, and scripted without setting object safety for untrusted data or scripts. This setting isn't recommended, except for secure and administered zones. This setting causes both unsafe and safe controls to be initialized and scripted, ignoring the Script ActiveX controls marked safe for scripting option. If you enable this policy setting and select Prompt in the drop-down box, users are queried whether to allow the control to load with parameters or scripted. If you disable this policy setting, ActiveX controls that can't be made safe aren't loaded with parameters or scripted. If you don't configure this policy setting, ActiveX controls that can't be made safe aren't loaded with parameters or scripted.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-intranetzoneinitializeandscriptactivexcontrols)

  - Baseline default:  Disable

- **Internet Explorer download enclosures**:  
  This policy setting prevents the user from having enclosures (file attachments) downloaded from a feed to the user's computer. If you enable this policy setting, the user can't set the Feed Sync Engine to download an enclosure through the Feed property page. A developer can't change the download setting through the Feed APIs. If you disable or don't configure this policy setting, the user can set the Feed Sync Engine to download an enclosure through the Feed property page. A developer can change the download setting through the Feed APIs.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-disableenclosuredownloading)

  - Baseline default:  Disabled

- **Internet Explorer restricted zone download unsigned Active X controls**:  
  This policy setting allows you to manage whether users may download unsigned ActiveX controls from the zone. Such code is potentially harmful, especially when coming from an untrusted zone. If you enable this policy setting, users can run unsigned controls without user intervention. If you select Prompt in the drop-down box, users are queried to choose whether to allow the unsigned control to run. If you disable this policy setting, users can't run unsigned controls. If you don't configure this policy setting, users can't run unsigned controls.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-restrictedsiteszonedownloadunsignedactivexcontrols)

  - Baseline default:  Disable

- **Internet Explorer internet zone drag content from different domains within windows**:  
  This policy setting allows you to manage whether users may download unsigned ActiveX controls from the zone. Such code is potentially harmful, especially when coming from an untrusted zone. If you enable this policy setting, users can run unsigned controls without user intervention. If you select Prompt in the drop-down box, users are queried to choose whether to allow the unsigned control to run. If you disable this policy setting, users can't run unsigned controls. If you don't configure this policy setting, users can't run unsigned controls.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-internetzoneenabledraggingofcontentfromdifferentdomainswithinwindows)

  - Baseline default:  Disabled

- **Internet Explorer processes restrict Active X install**:  
  This policy setting enables applications hosting the Web Browser Control to block automatic prompting of ActiveX control installation. If you enable this policy setting, the Web Browser Control will block automatic prompting of ActiveX control installation for all processes. If you disable or don't configure this policy setting, the Web Browser Control won't block automatic prompting of ActiveX control installation for all processes.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-restrictactivexinstallinternetexplorerprocesses)

  - Baseline default:  Enabled

- **Internet Explorer internet zone scriptlets**:  
  This policy setting allows you to manage whether the user can run scriptlets. If you enable this policy setting, the user can run scriptlets. If you disable this policy setting, the user can't run scriptlets. If you don't configure this policy setting, the user can enable or disable scriptlets.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-internetzoneallowscriptlets)

  - Baseline default:  Disable

- **Internet Explorer restricted zone drag and drop or copy and paste files**:  
  This policy setting allows you to manage whether users can drag files or copy and paste files from a source within the zone. If you enable this policy setting, users can drag files or copy and paste files from this zone automatically. If you select Prompt in the drop-down box, users are queried to choose whether to drag or copy files from this zone. If you disable this policy setting, users are prevented from dragging files or copying and pasting files from this zone. If you don't configure this policy setting, users are queried to choose whether to drag or copy files from this zone.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-restrictedsiteszoneallowdraganddropcopyandpastefiles)

  - Baseline default:  Disable

- **Internet Explorer software when signature is invalid**:  
  This policy setting allows you to manage whether software, such as ActiveX controls and file downloads, can be installed or run by the user even though the signature is invalid. An invalid signature might indicate that someone has tampered with the file. If you enable this policy setting, users are prompted to install or run files with an invalid signature. If you disable this policy setting, users can't run or install files with an invalid signature. If you don't configure this policy, users can choose to run or install files with an invalid signature.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-allowsoftwarewhensignatureisinvalid)

  - Baseline default:  Disabled

- **Internet Explorer restricted zone copy and paste via script**:  
  This policy setting allows you to manage whether scripts can do a clipboard operation (for example, cut, copy, and paste) in a specified region. If you enable this policy setting, a script can do a clipboard operation. If you select Prompt in the drop-down box, users are queried as to whether to do clipboard operations. If you disable this policy setting, a script can't do a clipboard operation. If you don't configure this policy setting, a script can't do a clipboard operation.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-restrictedsiteszoneallowcopypasteviascript)

  - Baseline default:  Disable

- **Internet Explorer restricted zone drag content from different domains across windows**:  
  This policy setting allows you to set options for dragging content from one domain to a different domain when the source and destination are in different windows. If you enable this policy setting and click Enable, users can drag content from one domain to a different domain when the source and destination are in different windows. Users can't change this setting. If you enable this policy setting and click Disable, users can't drag content from one domain to a different domain when both the source and destination are in different windows. Users can't change this setting. In Internet Explorer 10, if you disable this policy setting or don't configure it, users can't drag content from one domain to a different domain when the source and destination are in different windows. Users can change this setting in the Internet Options dialog. In Internet Explorer 9 and earlier versions, if you disable this policy or don't configure it, users can drag content from one domain to a different domain when the source and destination are in different windows. Users can't change this setting.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-restrictedsiteszoneenabledraggingofcontentfromdifferentdomainsacrosswindows)

  - Baseline default:  Disabled

- **Internet Explorer users adding sites**:  
  Prevents users from adding or removing sites from security zones. A security zone is a group of Web sites with the same security level. If you enable this policy, the site management settings for security zones are disabled. (To see the site management settings for security zones, in the Internet Options dialog box, click the Security tab, and then click the Sites button.) If you disable this policy or don't configure it, users can add Web sites to or remove sites from the Trusted Sites and Restricted Sites zones, and alter settings for the Local Intranet zone. This policy prevents users from changing site management settings for security zones established by the administrator. Note: The "Disable the Security page" policy (located in \User Configuration\Administrative Templates\Windows Components\Internet Explorer\Internet Control Panel), which removes the Security tab from the interface, takes precedence over this policy. If it's enabled, this policy is ignored. Also, see the "Security zones: Use only machine settings" policy.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-donotallowuserstoaddsites)

  - Baseline default:  Disabled

- **Internet Explorer internet zone script initiated windows**:  
  This policy setting allows you to manage restrictions on script-initiated pop-up windows and windows that include the title and status bars. If you enable this policy setting, Windows Restrictions security won't apply in this zone. The security zone runs without the added layer of security provided by this feature. If you disable this policy setting, the possible harmful actions contained in script-initiated pop-up windows and windows that include the title and status bars can't run. This Internet Explorer security feature is on in this zone as dictated by the Scripted Windows Security Restrictions feature control setting for the process. If you don't configure this policy setting, the possible harmful actions contained in script-initiated pop-up windows and windows that include the title and status bars can't run. This Internet Explorer security feature is on in this zone as dictated by the Scripted Windows Security Restrictions feature control setting for the process.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-internetzoneallowscriptinitiatedwindows)

  - Baseline default:  Disabled

- **Internet Explorer security zones use only machine settings**:  
  Applies security zone information to all users of the same computer. A security zone is a group of Web sites with the same security level. If you enable this policy, changes that the user makes to a security zone will apply to all users of that computer. If you disable this policy or don't configure it, users of the same computer can establish their own security zone settings. Use this policy to ensure that security zone settings apply uniformly to the same computer and don't vary from user to user. Also, see the "Security zones: don't allow users to change policies" policy.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-securityzonesuseonlymachinesettings)

  - Baseline default:  Enabled

- **Internet Explorer locked down local machine zone java permissions**:  
  This policy setting allows you to manage permissions for Java applets. If you enable this policy setting, you can choose options from the drop-down box. Custom, to control permissions settings individually. Low Safety enables applets to do all operations. Medium Safety enables applets to run in their sandbox (an area in memory outside of which the program can't make calls), plus capabilities like scratch space (a safe and secure storage area on the client computer) and user-controlled file I/O. High Safety enables applets to run in their sandbox. Disable Java to prevent any applets from running. If you disable this policy setting, Java applets can't run. If you don't configure this policy setting, Java applets are disabled.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-lockeddownlocalmachinezonejavapermissions)

  - Baseline default:  Disable java

- **Internet Explorer restricted zone do not run antimalware against Active X controls**:  
  This policy setting determines whether Internet Explorer runs antimalware programs against ActiveX controls, to check if they're safe to load on pages. If you enable this policy setting, Internet Explorer won't check with your antimalware program to see if it's safe to create an instance of the ActiveX control. If you disable this policy setting, Internet Explorer always checks with your antimalware program to see if it's safe to create an instance of the ActiveX control. If you don't configure this policy setting, Internet Explorer always checks with your antimalware program to see if it's safe to create an instance of the ActiveX control. Users can turn this behavior on or off, using Internet Explorer Security settings.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-restrictedsiteszonedonotrunantimalwareagainstactivexcontrols)

  - Baseline default:  Disabled

- **Internet Explorer restricted zone run .NET Framework reliant components signed with Authenticode**:  
  This policy setting allows you to manage whether .NET Framework components that are signed with Authenticode can be executed from Internet Explorer. These components include managed controls referenced from an object tag and managed executables referenced from a link. If you enable this policy setting, Internet Explorer will execute signed managed components. If you select Prompt in the drop-down box, Internet Explorer will prompt the user to determine whether to execute signed managed components. If you disable this policy setting, Internet Explorer won't execute signed managed components. If you don't configure this policy setting, Internet Explorer won't execute signed managed components.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-restrictedsiteszonerunnetframeworkreliantcomponentssignedwithauthenticode)

  - Baseline default:  Disable

- **Internet Explorer restricted zone access to data sources**:  
  This policy setting allows you to manage whether Internet Explorer can access data from another security zone using the Microsoft XML Parser (MSXML) or ActiveX Data Objects (ADO). If you enable this policy setting, users can load a page in the zone that uses MSXML or ADO to access data from another site in the zone. If you select Prompt in the drop-down box, users are queried to choose whether to allow a page to load in the zone that uses MSXML or ADO to access data from another site in the zone. If you disable this policy setting, users can't load a page in the zone that uses MSXML or ADO to access data from another site in the zone. If you don't configure this policy setting, users can't load a page in the zone that uses MSXML or ADO to access data from another site in the zone.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-restrictedsiteszoneallowaccesstodatasources)

  - Baseline default:  Disable

- **Internet Explorer internet zone don't run antimalware against ActiveX controls**:  
  This policy setting determines whether Internet Explorer runs antimalware programs against ActiveX controls, to check if they're safe to load on pages. If you enable this policy setting, Internet Explorer won't check with your antimalware program to see if it's safe to create an instance of the ActiveX control. If you disable this policy setting, Internet Explorer always checks with your antimalware program to see if it's safe to create an instance of the ActiveX control. If you don't configure this policy setting, Internet Explorer always checks with your antimalware program to see if it's safe to create an instance of the ActiveX control. Users can turn this behavior on or off, using Internet Explorer Security settings.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-internetzonedonotrunantimalwareagainstactivexcontrols)

  - Baseline default:  Disabled

- **Internet Explorer internet zone copy and paste via script**:  
  This policy setting allows you to manage whether scripts can do a clipboard operation (for example, cut, copy, and paste) in a specified region. If you enable this policy setting, a script can do a clipboard operation. If you select Prompt in the drop-down box, users are queried as to whether to do clipboard operations. If you disable this policy setting, a script can't do a clipboard operation. If you don't configure this policy setting, a script can do a clipboard operation.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-internetzoneallowcopypasteviascript)

  - Baseline default:  Disable

- **Internet Explorer use Active X installer service**:  
  This policy setting allows you to specify how ActiveX controls are installed. If you enable this policy setting, ActiveX controls are installed only if the ActiveX Installer Service is present and has been configured to allow the installation of ActiveX controls. If you disable or don't configure this policy setting, ActiveX controls, including per-user controls, are installed through the standard installation process.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-specifyuseofactivexinstallerservice)

  - Baseline default:  Enabled

- **Internet Explorer processes protection from zone elevation**:  
  Internet Explorer places restrictions on each Web page it opens. The restrictions are dependent upon the location of the Web page (Internet, Intranet, Local Machine zone, and so on). For example, Web pages on the local computer have the fewest security restrictions and are in the Local Machine zone, making the Local Machine security zone a prime target for malicious users. If you enable this policy setting, any zone can be protected from zone elevation for all processes. If you disable or don't configure this policy setting, processes other than Internet Explorer or those listed in the Process List receive no such protection.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-protectionfromzoneelevationinternetexplorerprocesses)

  - Baseline default:  Enabled

- **Internet Explorer internet zone download unsigned ActiveX controls**:  
  This policy setting allows you to manage whether users may download unsigned ActiveX controls from the zone. Such code is potentially harmful, especially when coming from an untrusted zone. If you enable this policy setting, users can run unsigned controls without user intervention. If you select Prompt in the drop-down box, users are queried to choose whether to allow the unsigned control to run. If you disable this policy setting, users can't run unsigned controls. If you don't configure this policy setting, users can't run unsigned controls.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-internetzonedownloadunsignedactivexcontrols)

  - Baseline default:  Disable

- **Internet Explorer internet zone navigate windows and frames across different domains**:  
  This policy setting allows you to manage the opening of windows and frames and access of applications across different domains. If you enable this policy setting, users can open windows and frames from other domains and access applications from other domains. If you select Prompt in the drop-down box, users are queried whether to allow windows and frames to access applications from other domains. If you disable this policy setting, users can't open windows and frames to access applications from different domains. If you don't configure this policy setting, users can open windows and frames from other domains and access applications from other domains.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-internetzoneenabledraggingofcontentfromdifferentdomainsacrosswindows)

  - Baseline default:  Disable

- **Internet Explorer internet zone updates to status bar via script**:  
  This policy setting allows you to manage whether a script can update the status bar within the zone. If you enable this policy setting, scripts can update the status bar. If you disable or don't configure this policy setting, script isn't allowed to update the status bar.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-internetzoneallowupdatestostatusbarviascript)

  - Baseline default:  Disabled

- **Internet Explorer restricted zone include local path when uploading files to server**:  
  This policy setting controls if local path information is sent when the user is uploading a file via an HTML form. If the local path information is sent, some information may be unintentionally revealed to the server. For instance, files sent from the user's desktop may contain the user name as a part of the path. If you enable this policy setting, path information is sent when the user is uploading a file via an HTML form. If you disable this policy setting, path information is removed when the user is uploading a file via an HTML form. If you don't configure this policy setting, the user can choose whether path information is sent when they're uploading a file via an HTML form. By default, path information is sent.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-restrictedsiteszoneincludelocalpathwhenuploadingfilestoserver)

  - Baseline default:  Disabled

- **Internet Explorer processes restrict file download**:  
  This policy setting enables applications hosting the Web Browser Control to block automatic prompting of file downloads that aren't user initiated. If you enable this policy setting, the Web Browser Control will block automatic prompting of file downloads that aren't user initiated for all processes. If you disable this policy setting, the Web Browser Control won't block automatic prompting of file downloads that aren't user initiated for all processes.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-restrictfiledownloadinternetexplorerprocesses)

  - Baseline default:  Enabled

- **Internet Explorer restricted zone allows only approved domains to use Active X controls**:  
  This policy setting controls if the user is prompted to allow ActiveX controls to run on websites other than the website that installed the ActiveX control. If you enable this policy setting, the user is prompted before ActiveX controls can run from websites in this zone. The user can choose to allow the control to run from the current site or from all sites. If you disable this policy setting, the user doesn't see the per-site ActiveX prompt, and ActiveX controls can run from all sites in this zone.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-restrictedsiteszoneallowonlyapproveddomainstouseactivexcontrols)

  - Baseline default:  Enabled

- **Internet Explorer restricted zone initialize and script Active X controls not marked as safe**:  
  This policy setting allows you to manage ActiveX controls not marked as safe. If you enable this policy setting, ActiveX controls run, loaded with parameters, and scripted without setting object safety for untrusted data or scripts. This setting isn't recommended, except for secure and administered zones. This setting causes both unsafe and safe controls to be initialized and scripted, ignoring the Script ActiveX controls marked safe for scripting option. If you enable this policy setting and select Prompt in the drop-down box, users are queried whether to allow the control to load with parameters or scripted. If you disable this policy setting, ActiveX controls that can't be made safe aren't loaded with parameters or scripted. If you don't configure this policy setting, ActiveX controls that can't be made safe aren't loaded with parameters or scripted.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-restrictedsiteszoneinitializeandscriptactivexcontrols)

  - Baseline default:  Disable

- **Internet Explorer users changing policies**:  
  Prevents users from changing security zone settings. A security zone is a group of Web sites with the same security level. If you enable this policy, the Custom Level button and security-level slider on the Security tab in the Internet Options dialog box are disabled. If you disable this policy or don't configure it, users can change the settings for security zones. This policy prevents users from changing security zone settings established by the administrator. Note: The "Disable the Security page" policy (located in \User Configuration\Administrative Templates\Windows Components\Internet Explorer\Internet Control Panel), which removes the Security tab from Internet Explorer in Control Panel, takes precedence over this policy. If it's enabled, this policy is ignored. Also, see the "Security zones: Use only machine settings" policy.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-donotallowuserstochangepolicies)

  - Baseline default:  Disabled

- **Internet Explorer restricted zone protected mode**:  
  This policy setting allows you to turn on Protected Mode. Protected Mode helps protect Internet Explorer from exploited vulnerabilities by reducing the locations that Internet Explorer can write to in the registry and the file system. If you enable this policy setting, Protected Mode is turned on. The user can't turn off Protected Mode. If you disable this policy setting, Protected Mode is turned off. The user can't turn on Protected Mode. If you don't configure this policy setting, the user can turn on or turn off Protected Mode.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-restrictedsiteszoneturnonprotectedmode)

  - Baseline default:  Enable

- **Internet Explorer internet zone user data persistence**:  
  This policy setting allows you to manage the preservation of information in the browser's history, in favorites, in an XML store, or directly within a Web page saved to disk. When a user returns to a persisted page, the state of the page can be restored if this policy setting is appropriately configured. If you enable this policy setting, users can preserve information in the browser's history, in favorites, in an XML store, or directly within a Web page saved to disk. If you disable this policy setting, users can't preserve information in the browser's history, in favorites, in an XML store, or directly within a Web page saved to disk. If you don't configure this policy setting, users can preserve information in the browser's history, in favorites, in an XML store, or directly within a Web page saved to disk.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-internetzoneallowuserdatapersistence)

  - Baseline default:  Disabled

- **Internet Explorer internet zone scripting of web browser controls**:  
  This policy setting determines whether a page can control embedded WebBrowser controls via script. If you enable this policy setting, script access to the WebBrowser control is allowed. If you disable this policy setting, script access to the WebBrowser control isn't allowed. If you don't configure this policy setting, the user can enable or disable script access to the WebBrowser control. By default, script access to the WebBrowser control is allowed only in the Local Machine and Intranet zones.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-internetzoneallowscriptingofinternetexplorerwebbrowsercontrols)

  - Baseline default:  Disabled

- **Internet Explorer restricted zone user data persistence**:  
  This policy setting allows you to manage the preservation of information in the browser's history, in favorites, in an XML store, or directly within a Web page saved to disk. When a user returns to a persisted page, the state of the page can be restored if this policy setting is appropriately configured. If you enable this policy setting, users can preserve information in the browser's history, in favorites, in an XML store, or directly within a Web page saved to disk. If you disable this policy setting, users can't preserve information in the browser's history, in favorites, in an XML store, or directly within a Web page saved to disk. If you don't configure this policy setting, users can't preserve information in the browser's history, in favorites, in an XML store, or directly within a Web page saved to disk.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-restrictedsiteszoneallowuserdatapersistence)

  - Baseline default:  Disabled

- **Internet Explorer locked down intranet zone java permissions**:  
  This policy setting allows you to manage permissions for Java applets. If you enable this policy setting, you can choose options from the drop-down box. Custom, to control permissions settings individually. Low Safety enables applets to do all operations. Medium Safety enables applets to run in their sandbox (an area in memory outside of which the program can't make calls), plus capabilities like scratch space (a safe and secure storage area on the client computer) and user-controlled file I/O. High Safety enables applets to run in their sandbox. Disable Java to prevent any applets from running. If you disable this policy setting, Java applets can't run. If you don't configure this policy setting, Java applets are disabled.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-lockeddownintranetjavapermissions)

  - Baseline default:  Disable java

- **Internet Explorer enhanced protected mode**:  
  Enhanced Protected Mode provides additional protection against malicious websites by using 64-bit processes on 64-bit versions of Windows. For computers running at least Windows 8, Enhanced Protected Mode also limits the locations Internet Explorer can read from in the registry and the file system. If you enable this policy setting, Enhanced Protected Mode is turned on. Any zone that has Protected Mode enabled will use Enhanced Protected Mode. Users can't disable Enhanced Protected Mode. If you disable this policy setting, Enhanced Protected Mode is turned off. Any zone that has Protected Mode enabled will use the version of Protected Mode introduced in Internet Explorer 7 for Windows Vista. If you don't configure this policy, users can turn on or turn off Enhanced Protected Mode on the Advanced tab of the Internet Options dialog.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-allowenhancedprotectedmode)

  - Baseline default:  Enabled

- **Internet Explorer bypass smart screen warnings**:  
  This policy setting determines whether the user can bypass warnings from SmartScreen Filter. SmartScreen Filter warns the user about executable files that Internet Explorer users don't commonly download from the Internet. If you enable this policy setting, SmartScreen Filter warnings block the user. If you disable or don't configure this policy setting, the user can bypass SmartScreen Filter warnings.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-disablebypassofsmartscreenwarnings)

  - Baseline default:  Disabled

- **Internet Explorer restricted zone meta refresh**:  
  This policy setting allows you to manage whether a user's browser can be redirected to another Web page if the author of the Web page uses the Meta Refresh setting (tag) to redirect browsers to another Web page. If you enable this policy setting, a user's browser that loads a page containing an active Meta Refresh setting can be redirected to another Web page. If you disable this policy setting, a user's browser that loads a page containing an active Meta Refresh setting can't be redirected to another Web page. If you don't configure this policy setting, a user's browser that loads a page containing an active Meta Refresh setting can't be redirected to another Web page.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-restrictedsiteszoneallowmetarefresh)

  - Baseline default:  Disabled

## Local Policies Security Options

For more information, see [Policy CSP - LocalPoliciesSecurityOptions](/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions) in the Windows documentation.

- **Restrict anonymous access to named pipes and shares**:  
  When enabled, this security setting restricts anonymous access to shares and pipes to the settings for: (1) Named pipes that can be accessed anonymously (2) Shares that can be accessed anonymously.  
  [Learn more](/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions#localpoliciessecurityoptions-networkaccess-restrictanonymousaccesstonamedpipesandshares)

  - Baseline default:  Yes

- **Minimum session security for NTLM SSP based servers**:  
  This security setting allows a server to require the negotiation of 128-bit encryption and NTLMv2 session security. These values are dependent on the LAN Manager Authentication Level security setting value. The options are: Require NTLMv2 session security: The connection will fail if message integrity isn't negotiated. Require 128-bit encryption. The connection will fail if strong encryption (128-bit) isn't negotiated.  
  [Learn more](/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions#localpoliciessecurityoptions-networksecurity-minimumsessionsecurityforntlmsspbasedservers)

  - Baseline default:  Require NTLM V2 and 128 bit encryption

- **Minutes of lock screen inactivity until screen saver activates**:  
  Windows notices inactivity of a logon session, and if the amount of inactive time exceeds the inactivity limit, then the screen saver will run, locking the session.  
  [Learn more](/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions#localpoliciessecurityoptions-interactivelogon-machineinactivitylimit)

  - Baseline default:  15

- **Require client to always digitally sign communications**:  
  This security setting determines whether all secure channel traffic initiated by the domain member must be signed or encrypted. When a computer joins a domain, a computer account is created. After that, when the system starts, it uses the computer account password to create a secure channel with a domain controller for its domain. This secure channel is used to do operations such as NTLM pass through authentication, LSA SID/name Lookup and more. This setting determines if all secure channel traffic initiated by the domain member meets minimum security requirements. Specifically it determines whether all secure channel traffic started by the domain member must be signed or encrypted. If this policy is enabled, then the secure channel won't be established unless either signing or encryption of all secure channel traffic is negotiated. If this policy is disabled, then encryption and signing of all secure channel traffic is negotiated with the Domain Controller in which case the level of signing and encryption depends on the version of the Domain Controller and the settings of the following two policies: Domain member: Digitally encrypt secure channel data (when possible) Domain member: Digitally sign secure channel data (when possible).  
  [Learn more](/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions#localpoliciessecurityoptions-microsoftnetworkclient-digitallysigncommunicationsalways)

  - Baseline default:  Yes

- **Authentication level**:  
  This security setting determines which challenge/response authentication protocol is used for network logons. This choice affects the level of authentication protocol used by clients, the level of session security negotiated, and the level of authentication accepted by servers as follows:

  - *Send LM and NTLM responses* - Clients use LM and NTLM authentication and never use NTLMv2 session security; domain controllers accept LM, NTLM, and NTLMv2 authentication.

  - *Send LM and NTLM - NTLMv2 if negotiated* - Clients use LM and NTLM authentication and use NTLMv2 session security if the server supports it. Domain controllers accept LM, NTLM, and NTLMv2 authentication.

  - *Send NTLM response only* - Clients use NTLM authentication only and use NTLMv2 session security if the server supports it; domain controllers accept LM, NTLM, and NTLMv2 authentication.

  - *Send NTLMv2 response only* - Clients use NTLMv2 authentication only and use NTLMv2 session security if the server supports it; domain controllers accept LM, NTLM, and NTLMv2 authentication.

  - *Send NTLMv2 response only. Refuse LM* - Clients use NTLMv2 authentication only and use NTLMv2 session security if the server supports it. Domain controllers refuse LM (accept only NTLM and NTLMv2 authentication).

  - *Send NTLMv2 response only. Refuse LM and NTLM* - Clients use NTLMv2 authentication only and use NTLMv2 session security if the server supports it. Domain controllers refuse LM and NTLM (accept only NTLMv2 authentication).

  [Learn more](/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions#localpoliciessecurityoptions-networksecurity-lanmanagerauthenticationlevel)

  - Baseline default:  Send NTLMv2 response only. Refuse LM and NTLM

- **Prevent clients from sending unencrypted passwords to third party SMB servers**:  
  If this security setting is enabled, the Server Message Block (SMB) redirector can send plaintext passwords to non-Microsoft SMB servers that don't support password encryption during authentication. Sending unencrypted passwords is a security risk.  
  [Learn more](/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions#localpoliciessecurityoptions-microsoftnetworkclient-sendunencryptedpasswordtothirdpartysmbservers)

  - Baseline default:  Yes

- **Require server digitally signing communications always**:  
  This security setting determines whether the SMB client attempts to negotiate SMB packet signing. The server message block (SMB) protocol provides the basis for Microsoft file and print sharing and many other networking operations, such as remote Windows administration. To prevent man-in-the-middle attacks that modify SMB packets in transit, the SMB protocol supports the digital signing of SMB packets. This policy setting determines whether the SMB client component attempts to negotiate SMB packet signing when it connects to an SMB server. If this setting is enabled, the Microsoft network client will ask the server to do SMB packet signing upon session setup. If packet signing has been enabled on the server, packet signing is negotiated. If this policy is disabled, the SMB client will never negotiate SMB packet signing.  
  [Learn more](/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions#localpoliciessecurityoptions-microsoftnetworkserver-digitallysigncommunicationsalways)

  - Baseline default:  Yes

- **Administrator elevation prompt behavior**:  
  This policy setting controls the behavior of the elevation prompt for administrators. The options are:

  - *Elevate without prompting* - Allows privileged accounts to do an operation that requires elevation without requiring consent or credentials. Note: Use this option only in the most constrained environments.

  - *Prompt for credentials on the secure desktop* - When an operation requires elevation of privilege, the user is prompted on the secure desktop to enter a privileged user name and password. If the user enters valid credentials, the operation continues with the user's highest available privilege.

  - *Prompt for consent on the secure desktop* - When an operation requires elevation of privilege, the user is prompted on the secure desktop to select either Permit or Deny. If the user selects Permit, the operation continues with the user's highest available privilege.

  - *Prompt for credentials* - When an operation requires elevation of privilege, the user is prompted to enter an administrative user name and password. If the user enters valid credentials, the operation continues with the applicable privilege.

  - *Prompt for consent* - When an operation requires elevation of privilege, the user is prompted to select either Permit or Deny. If the user selects Permit, the operation continues with the user's highest available privilege.

  - *Prompt for consent for non-Windows binaries* - When an operation for a non-Microsoft application requires elevation of privilege, the user is prompted on the secure desktop to select either Permit or Deny. If the user selects Permit, the operation continues with the user's highest available privilege.

  [Learn more](/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions#localpoliciessecurityoptions-useraccountcontrol-behavioroftheelevationpromptforadministrators)

  - Baseline default:  Prompt for consent on the secure desktop

- **Minimum session security for NTLM SSP based clients**:  
  This security setting allows a client to require the negotiation of 128-bit encryption and NTLMv2 session security. These values are dependent on the LAN Manager Authentication Level security setting value. The options are:

  - *Require NTLMv2 session security* - The connection will fail if NTLMv2 protocol isn't negotiated.

  - *Require 128-bit encryption* - The connection will fail if strong encryption (128-bit) isn't negotiated.

  - *Require NTLMv2 and 128-bit encryption*.

  [Learn more](/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions#localpoliciessecurityoptions-networksecurity-minimumsessionsecurityforntlmsspbasedclients)

  - Baseline default:  Require NTLM V2 128 encryption

- **Smart card removal behavior**:  
  This security setting determines what happens when the smart card for a logged-on user is removed from the smart card reader. The options are:

  - *No action*.

  - *Lock Workstation* - The workstation is locked when the smart card is removed, allowing users to leave the area, take their smart card with them, and still maintain a protected session.

  - *Force Logoff* - the user is automatically logged off when the smart card is removed.

  - *Disconnect Remote Desktop session* - Removal of the smart card disconnects the session without logging the user off. This allows the user to insert the smart card and resume the session later, or at another smart card reader-equipped computer, without having to log on again. If the session is local, this policy functions identically to Lock Workstation.

  [Learn more](/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions#localpoliciessecurityoptions-interactivelogon-smartcardremovalbehavior)

  - Baseline default:  Lock workstation

- **Block anonymous enumeration of SAM accounts and shares**:  
  This security setting determines whether to allow anonymous enumeration of SAM accounts and shares. Windows allows anonymous users to do certain activities, such as enumerating the names of domain accounts and network shares. This is convenient, for example, when an administrator wants to grant access to users in a trusted domain that doesn't maintain a reciprocal trust. If you don't want to allow anonymous enumeration of SAM accounts and shares, then set this policy to *Yes*.  
  [Learn more](/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions#localpoliciessecurityoptions-networkaccess-donotallowanonymousenumerationofsamaccountsandshares)

  - Baseline default:  Yes

- **Block remote logon with blank password**:  
  This security setting determines whether local accounts that aren't password protected can be used to log on from locations other than the physical computer console. If enabled, local accounts that aren't password protected must use the computer's keyboard to log on.

  *Warning*: Computers that aren't in physically secure locations should always enforce strong password policies for all local user accounts. Otherwise, anyone with physical access to the computer can log on by using a user account that doesn't have a password. This is especially important for portable computers.

  If you apply this security policy to the Everyone group, no one can log on through Remote Desktop Services. This setting doesn't affect logons that use domain accounts. It's possible for applications that use remote interactive logons to bypass this setting.  
  [Learn more](/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions#localpoliciessecurityoptions-accounts-limitlocalaccountuseofblankpasswordstoconsolelogononly)

  - Baseline default:  Yes

- **Standard user elevation prompt behavior**:  
  This policy setting controls the behavior of the elevation prompt for standard users.

  - *Automatically deny elevation requests* - When an operation requires elevation of privilege, a configurable access denied error message is displayed. An enterprise that is running desktops as standard user may choose this setting to reduce help desk calls.

  - *Prompt for credentials on the secure desktop* - When an operation requires elevation of privilege, the user is prompted on the secure desktop to enter a different user name and password. If the user enters valid credentials, the operation continues with the applicable privilege.

  - *Prompt for credentials* - When an operation requires elevation of privilege, the user is prompted to enter an administrative user name and password. If the user enters valid credentials, the operation continues with the applicable privilege.

  [Learn more](/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions#localpoliciessecurityoptions-useraccountcontrol-behavioroftheelevationpromptforstandardusers)

  - Baseline default:  Automatically deny elevation requests

- **Require admin approval mode for administrators**:  
  This policy setting controls the behavior of all User Account Control (UAC) policy settings for the computer. If you change this policy setting, you must restart your computer. The options are:

  - *Not configured* - Admin Approval Mode and all related UAC policy settings are disabled. Note: If this policy setting is disabled, the Security Center notifies you that the overall security of the operating system has been reduced.

  - *Yes* - Admin Approval Mode is enabled. This policy must be enabled and the related UAC policy settings must be set appropriately to allow the built-in Administrator account and all other users who are members of the Administrators group to run in Admin Approval Mode.

  [Learn more](/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions#localpoliciessecurityoptions-useraccountcontrol-useadminapprovalmode)

  - Baseline default:  Yes

- **Prevent anonymous enumeration of SAM accounts**:  
  This security setting determines what additional permissions are granted for anonymous connections to the computer. Windows allows anonymous users to do certain activities, such as enumerating the names of domain accounts and network shares. This is convenient, for example, when an administrator wants to grant access to users in a trusted domain that doesn't maintain a reciprocal trust. This security option allows additional restrictions to be placed on anonymous connections as follows:

  - *Yes* - Don't allow enumeration of SAM accounts. This option replaces Everyone with Authenticated Users in the security permissions for resources.

  - *Not configured* - No additional restrictions. Rely on default permissions.

  [Learn more](/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions#localpoliciessecurityoptions-networkaccess-donotallowanonymousenumerationofsamaccounts)

  - Baseline default:  Yes

- **Allow remote calls to security accounts manager**:  
  This policy setting allows you to restrict remote rpc connections to SAM. If not selected, the default security descriptor is used.  
  [Learn more](/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions#localpoliciessecurityoptions-networkaccess-restrictclientsallowedtomakeremotecallstosam)

  - Baseline default:  *O:BAG:BAD:(A;;RC;;;BA)*

- **Use admin approval mode**:  
  This policy setting controls the behavior of Admin Approval Mode for the built-in Administrator account. The options are:

  - *Yes* - The built-in Administrator account uses Admin Approval Mode. By default, any operation that requires elevation of privilege will prompt the user to approve the operation.

  - *Not Configured* - The built-in Administrator account runs all applications with full administrative privilege.

  [Learn more](/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions#localpoliciessecurityoptions-useraccountcontrol-runalladministratorsinadminapprovalmode)

  - Baseline default:  Yes
  
- **Only allow UI access applications for secure locations**:  
  This policy setting controls whether User Interface Accessibility (UIAccess or UIA) programs can automatically disable the secure desktop for elevation prompts used by a standard user.

  - *Yes* - UIA programs, including Windows Remote Assistance, automatically disable the secure desktop for elevation prompts. If you don't disable the "User Account Control: Switch to the secure desktop when prompting for elevation" policy setting, the prompts appear on the interactive user's desktop instead of the secure desktop.

  - *Not Configured*: - The secure desktop can be disabled only by the user of the interactive desktop or by disabling the "User Account Control: Switch to the secure desktop when prompting for elevation" policy setting.

  [Learn more](/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions#localpoliciessecurityoptions-useraccountcontrol-onlyelevateuiaccessapplicationsthatareinstalledinsecurelocations)

  - Baseline default:  Yes

- **Detect application installations and prompt for elevation**:  
  This policy setting controls the behavior of application installation detection for the computer. The options are:

  - *Enabled* - When an application installation package is detected that requires elevation of privilege, the user is prompted to enter an administrative user name and password. If the user enters valid credentials, the operation continues with the applicable privilege.

  - *Disabled* - Application installation packages aren't detected and prompted for elevation. Enterprises that are running standard user desktops and use delegated installation technologies such as Group Policy Software Installation or Systems Management Server (SMS) should disable this policy setting. In this case, installer detection is unnecessary.

  [Learn more](/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions#localpoliciessecurityoptions-useraccountcontrol-detectapplicationinstallationsandpromptforelevation)

  - Baseline default:  Yes

- **Prevent storing LAN manager hash value on next password change**:  
  This security setting determines if, at the next password change, the LAN Manager (LM) hash value for the new password is stored. The LM hash is relatively weak and prone to attack, as compared with the cryptographically stronger Windows NT hash. Because the LM hash is stored on the local computer in the security database, the passwords can be compromised if the security database is attacked.  
  [Learn more](/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions#localpoliciessecurityoptions-networksecurity-donotstorelanmanagerhashvalueonnextpasswordchange)

  - Baseline default:  Yes

- **Virtualize file and registry write failures to per user locations**:  
  This policy setting controls whether application write failures are redirected to defined registry and file system locations. This policy setting mitigates applications that run as administrator and write run-time application data to *%ProgramFiles%*, *%Windir%*, *%Windir%\system32*, or *HKLM\Software*.  
  [Learn more](/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions#localpoliciessecurityoptions-useraccountcontrol-virtualizefileandregistrywritefailurestoperuserlocations)

  - Baseline default:  Yes

## Microsoft Defender

For more information, see [Policy CSP - Defender](/windows/client-management/mdm/policy-csp-defender) in the Windows documentation.

- **Block Adobe Reader from creating child processes**:  
This rule prevents attacks by blocking Adobe Reader from creating additional processes. Through social engineering or exploits, malware can download and launch additional payloads and break out of Adobe Reader. By blocking child processes from being generated by Adobe Reader, malware attempting to use it as a vector are prevented from spreading.
[Learn more](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction)

  - Baseline default:  Enable

- **Block Office communication apps launch in a child process**:  
  [Protect devices from exploits](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction)

  - Baseline default:  Enable

- **Enter how often (0-24 hours) to check for security intelligence updates**  
  CSP: [Defender/SignatureUpdateInterval](/windows/client-management/mdm/policy-csp-defender)
  
  Specify how often to check for new signatures. A value of 1 is one hour, 2 is two hours, and so on.

  - Baseline default:  4

- **Scan type**  
  CSP: [Defender/ScanParameter](/windows/client-management/mdm/policy-csp-defender#defender-scanparameter)

  Specify the scan type to use for a schedule scan

  - Baseline default:  Quick scan

- **Defender schedule scan day**:  
  Defender schedule scan day.

  - Baseline default:  Everyday

::: zone-end
::: zone pivot="mdm-december-2020,november-2021"

- **Defender scan start time**:  
  Defender schedule scan time.

  - Baseline default:  Not configured

::: zone-end
::: zone pivot="mdm-sept-2020,mdm-december-2020,november-2021"

- **Cloud-delivered protection level**:  
  CSP: [Defender/CloudBlockLevel](/windows/client-management/mdm/policy-csp-defender#defender-cloudblocklevel)

  Specify the level of cloud-delivered protection. Not Configured uses the default Microsoft Defender Antivirus blocking level and provides strong detection without increasing the risk of detecting legitimate files. High applies a strong level of detection. High + uses the High level and applies addition protection measures (may impact client performance). Zero tolerance blocks all unknown executables. While unlikely, setting to High may cause some legitimate files to be detected. 

  - Baseline default:  Not Configured

- **Scan network files**:  
  CSP: [Defender/AllowScanningNetworkFiles](/windows/client-management/mdm/policy-csp-defender#defender-allowscanningnetworkfiles)

  When set to Yes, Microsoft Defender will scan network files. When set to Not configured, the client will return to default with is disabling scanning of network files.

  - Baseline default:  Yes

- **Turn on real-time protection**  
  CSP: [Defender/AllowRealtimeMonitoring](/windows/client-management/mdm/policy-csp-defender#defender-allowrealtimemonitoring)

  When this setting is set to Yes, real-time monitoring will be enforced and the user can't disable it. When set to Not configured, the setting is returned to client default, which is on, but the user can change it. To disable real-time monitoring, use a custom URI.

  - Baseline default:  Yes  

::: zone-end
::: zone pivot="november-2021"

- **Scan scripts that are used in Microsoft browsers**  
  CSP [Defender/AllowScriptScanning](/windows/client-management/mdm/policy-csp-defender#defender-allowscriptscanning)

  When this setting is set to Yes, the Windows Defender Script Scanning functionality will be enforced and the user cannot turn them off. When set to Not configured, the setting is returned to client default which is to enable script scanning, however the user can turn it off.

  - Baseline default:  Yes

::: zone-end
::: zone pivot="mdm-sept-2020,mdm-december-2020,november-2021"

- **Scan archive files**:  
  CSP: [Defender/AllowArchiveScanning](/windows/client-management/mdm/policy-csp-defender#defender-allowarchivescanning)
  
  When set to Yes, archive files such as ZIP or CAB file scanning will be enforced. When set to Not configured, the setting will be returned back to client default, which is to scan archived files, however the user may disable this.

  - Baseline default:  Yes

- **Turn on behavior monitoring**:  
  CSP: [Defender/AllowBehaviorMonitoring](/windows/client-management/mdm/policy-csp-defender#defender-allowbehaviormonitoring)

  When this setting is set to Yes, behavior monitoring will be enforced and the user can't disable it. When set to Not configured, the setting is returned to client default, which is on, but the user can change it. To disable real-time monitoring, use a custom URI.

  - Baseline default:  Yes

- **Turn on cloud-delivered protection**:  
  CSP: [Defender/AllowCloudProtection](/windows/client-management/mdm/policy-csp-defender#defender-allowcloudprotection)

  When set to Yes, Defender will send information to Microsoft about any problems it finds. If set to Not configured, the client will return to default, which enables the feature but allows the user to disable it.

  - Baseline default:  Yes

- **Scan incoming mail messages**:  
  CSP: [Defender/AllowEmailScanning](/windows/client-management/mdm/policy-csp-defender#defender-allowemailscanning)

  When set to Yes, e-mail mailbox and mail files such as PST, DBX, MNX, MIME and BINHEX will be scanned. When Not configured, the setting will return to client default of e-mail files not being scanned.

  - Baseline default:  Yes

- **Scan removable drives during a full scan**:  
  CSP: [Defender/AllowFullScanRemovableDriveScanning](/windows/client-management/mdm/policy-csp-defender#defender-allowfullscanremovabledrivescanning)

  When set to Yes, during a full scan removable drives (for example, USB flash drives) will be scanned. When set to Not Configured, the setting will return to client default, which scans removable drives, however the user can disable this.
  - Baseline default:  Yes  

- **Block Office applications from injecting code into other processes**:  
  [Protect devices from exploits](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction)

  When set to Yes, Office applications will be blocked from injecting code into other processes. When set to Audit only, Windows events will be raised instead of blocking. Setting to Not Configured will return the setting to Windows default, which is off. This Attack Surface Reduction (ASR) rule is controlled via the following GUID: 75668C1F-73B5-4CF0-BB93-3ECF5CB7CC84

  - Baseline default:   Block

- **Block Office applications from creating executable content**  
  [Protect devices from exploits](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction)

  When set to Yes, Office applications will not be allowed to create executable content. When set to Audit only, Windows events will be raised instead of blocking. Setting to Not Configured will return the setting to Windows default, which is off. This ASR rule is controlled via the following GUID: 3B576869-A4EC-4529-8536-B80A7769E899

  - Baseline default:   Block

- **Block all Office applications from creating child processes**  
  [Protect devices from exploits](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction)

  When set to Audit mode, Windows events will be raised instead of blocking. Setting to Not Configured will return the setting to Windows default, which is off. This ASR rule is controlled via the following GUID: D4F940AB-401B-4EFC-AADC-AD5F3C50688A

  - Baseline default:   Block

- **Block Win32 API calls from Office macro**:  
  [Protect devices from exploits](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction)

  When set to Yes, Office macro's will be blocked from using Win32 API calls. When set to Audit only, Windows events will be raised instead of blocking. Setting to Not Configured will return the setting to Windows default, which is off. This ASR rule is controlled via the following GUID: 92E97FA1-2EDF-4476-BDD6-9DD0B4DDDC7B
  
  - Baseline default:  Block

- **Block execution of potentially obfuscated scripts (js/vbs/ps)**:  
  [Protect devices from exploits](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction)

  When set to yes, Defender will block execution of obfuscated scripts. When set to Audit only, Windows events will be raised instead of blocking. Setting to Not Configured will return the setting to Windows default, which is off. This ASR rule is controlled via the following GUID: 5BEB7EFE-FD9A-4556-801D-275E5FFC04CC
  
  - Baseline default:  Block

- **Block JavaScript or VBScript from launching downloaded executable content**:  
  [Protect devices from exploits](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction)

  When set to Yes, Defender will block Javascript or VBScript files that have been downloaded from the Internet from being executed. When set to Audit only, Windows events will be raised instead of blocking. Setting to Not Configured will return the setting to Windows default, which is off. This attack surface reduction (ASR) rule is controlled via the following GUID: D3E037E1-3EB8-44C8-A917-57927947596D
  
  - Baseline default:  Block

- **Block executable content download from email and webmail clients**:  
  [Block executable content download from email and webmail clients](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction)

  When set to Yes, executable content downloaded from email and webmail clients will be blocked. When set to Audit only, Windows events will be raised instead of blocking. Setting to Not Configured will return the setting to Windows default, which is off.

  - Baseline default:  Block

- **Prevent credential stealing type**:  
  [Protect devices from exploits](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction)
  
  When set to Yes, attempts to steal credentials via lsass.exe will be blocked. When set to Audit only, Windows events will be raised instead of blocking. Setting to Not Configured will return the setting to Windows default, which is off. This ASR rule is controlled via the following GUID: 9e6c4e1f-7d60-472f-ba1a-a39ef669e4b2

  - Baseline default:  Enable

- **Defender potentially unwanted app action**:  
  CSP: [Defender/PUAProtection](/windows/client-management/mdm/policy-csp-defender#defender-puaprotection)+

  The potentially unwanted application (PUA) protection feature in Microsoft Defender Antivirus can identify and block PUAs from downloading and installing on endpoints in your network. These applications aren't considered viruses, malware, or other types of threats, but might do actions on endpoints that adversely affect their performance or use. PUA can also refer to applications that are considered to have a poor reputation. Typical PUA behavior includes: Various types of software bundling Ad injection into web browsers Driver and registry optimizers that detect issues, request payment to fix the errors, but remain on the endpoint and make no changes or optimizations (also known as "rogue antivirus" programs). These applications can increase the risk of your network being infected with malware, cause malware infections to be harder to identify, and can waste IT resources in cleaning up the applications.

  - Baseline default:  Block

- **Block untrusted and unsigned processes that run from USB**:  
  [Protect devices from exploits](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction)
  
  When set to Yes, untrusted/unsigned processes executing from a USB drive will be blocked. When set to Audit only, Windows events will be raised instead of blocking. Setting to Not Configured will return the setting to Windows default, which is off. This ASR rule is controlled via the following GUID: b2b3f03d-6a65-4f7b-a9c7-1c7ef74a9ba4

  - Baseline default:  Block

- **Enable network protection**:  
  [Defender/EnableNetworkProtection](/windows/client-management/mdm/policy-csp-defender#defender-enablenetworkprotection)

  When set to Yes, network protection will be enabled for all users on the system. Network protection protects employees from accessing phishing scams, and malicious content on the Internet. This includes third-party browsers. Setting this to Audit only, users will not be blocked from dangerous domains however Windows events will be raised instead. Setting this to Not Configured will return the setting to Windows default, which is disabled.

  - Baseline default:  Enable

- **Defender sample submission consent type**:  
  [Defender/SubmitSamplesConsent](/windows/client-management/mdm/policy-csp-defender#defender-submitsamplesconsent)

  Checks for the user consent level in Microsoft Defender to send data. If the required consent has already been granted, Microsoft Defender submits them. If not, and if the user has specified never to ask, the UI is launched to ask for user consent (when Defender/AllowCloudProtection is allowed) before sending data.

  - Baseline default:  Send safe samples automatically

## MS Security Guide

For more information, see [Policy CSP - MSSecurityGuide](/windows/client-management/mdm/policy-csp-mssecurityguide) in the Windows documentation.

- **Apply UAC restrictions to local accounts on network logon**:  
  [Learn more](/windows/client-management/mdm/policy-csp-mssecurityguide#mssecurityguide-applyuacrestrictionstolocalaccountsonnetworklogon)

  - Baseline default:  Enabled

- **SMB v1 client driver start configuration**:  
  [Learn more](/windows/client-management/mdm/policy-csp-mssecurityguide#mssecurityguide-configuresmbv1clientdriver)

  - Baseline default:  Disabled driver

- **SMB v1 server**:  
  [Learn more](/windows/client-management/mdm/policy-csp-mssecurityguide#mssecurityguide-configuresmbv1server)

  - Baseline default:  Disabled

- **Digest authentication**:  
  [Learn more](/windows/client-management/mdm/policy-csp-mssecurityguide#mssecurityguide-wdigestauthentication)

  - Baseline default:  Disabled

- **Structured exception handling overwrite protection**:  
  [Learn more](/windows/client-management/mdm/policy-csp-mssecurityguide#mssecurityguide-enablestructuredexceptionhandlingoverwriteprotection)

  - Baseline default:  Enabled

## MSS Legacy

For more information, see [Policy CSP - MSSLegacy](/windows/client-management/mdm/policy-csp-msslegacy) in the Windows documentation.

- **Network IP source routing protection level**:  
  [Learn more](/windows/client-management/mdm/policy-csp-msslegacy#msslegacy-ipsourceroutingprotectionlevel)

  - Baseline default:  Highest protection  

- **Network ignore NetBIOS name release requests except from WINS servers**:  
  [Learn more](/windows/client-management/mdm/policy-csp-msslegacy#msslegacy-allowthecomputertoignorenetbiosnamereleaserequestsexceptfromwinsservers)

  - Baseline default:  Enabled

- **Network IPv6 source routing protection level**:  
  [Learn more](/windows/client-management/mdm/policy-csp-msslegacy#msslegacy-ipv6sourceroutingprotectionlevel)

  - Baseline default:  Highest protection

- **Network ICMP redirects override OSPF generated routes**:  
  [Learn more](/windows/client-management/mdm/policy-csp-msslegacy#msslegacy-allowicmpredirectstooverrideospfgeneratedroutes)

  - Baseline default:  Disabled

## Power

For more information, see [Policy CSP - Power](/windows/client-management/mdm/policy-csp-power) in the Windows documentation.

- **Require password on wake while plugged in**:  
  This policy setting specifies if the user is prompted for a password when the system resumes from sleep. If you enable or don't configure this policy setting, the user is prompted for a password when the system resumes from sleep. If you disable this policy setting, the user isn't prompted for a password when the system resumes from sleep.  
  [Learn more](/windows/client-management/mdm/policy-csp-power#power-requirepasswordwhencomputerwakespluggedin)

  - Baseline default:  Enabled

- **Standby states when sleeping while on battery**:  
  This policy setting manages if Windows can use standby states when putting the computer in a sleep state. If you enable or don't configure this policy setting, Windows uses standby states to put the computer in a sleep state. If you disable this policy setting, standby states (S1-S3) aren't allowed.  
  [Learn more](/windows/client-management/mdm/policy-csp-power#power-standbytimeoutonbattery)

  - Baseline default:  Disabled

- **Standby states when sleeping while plugged in**:  
  This policy setting manages if Windows can use standby states when putting the computer in a sleep state. If you enable or don't configure this policy setting, Windows uses standby states to put the computer in a sleep state. If you disable this policy setting, standby states (S1-S3) aren't allowed.  
  [Learn more](/windows/client-management/mdm/policy-csp-power#power-standbytimeoutpluggedin)

  - Baseline default:  Disabled

- **Require password on wake while on battery**:  
  This policy setting specifies if the user is prompted for a password when the system resumes from sleep. If you enable or don't configure this policy setting, the user is prompted for a password when the system resumes from sleep. If you disable this policy setting, the user isn't prompted for a password when the system resumes from sleep.  
  [Learn more](/windows/client-management/mdm/policy-csp-power#power-requirepasswordwhencomputerwakesonbattery)

  - Baseline default:  Enabled

## Remote Assistance

For more information, see [Policy CSP - RemoteAssistance](/windows/client-management/mdm/policy-csp-remoteassistance#remoteassistance-solicitedremoteassistance) in the Windows documentation.

- **Remote Assistance solicited**:  
  This policy setting allows you to turn on or turn off Solicited (Ask for) Remote Assistance on this computer.
  
  - *If you enable this policy setting*, users on this computer can use email or file transfer to ask someone for help. Also, users can use instant messaging programs to allow connections to this computer, and you can configure additional Remote Assistance settings.

  - *If you disable this policy setting*, users on this computer can't use email or file transfer to ask someone for help. Also, users can't use instant messaging programs to allow connections to this computer.

  - *If you don't configure this policy setting*, users can turn on or turn off Solicited (Ask for) Remote Assistance themselves in System Properties in Control Panel. Users can also configure Remote Assistance settings.

  If you enable this policy setting, you have two ways to allow helpers to provide Remote Assistance: "Allow helpers to only view the computer" or "Allow helpers to remotely control the computer." The "Maximum ticket time" policy setting sets a limit on the amount of time that a Remote Assistance invitation created by using email or file transfer can remain open. The "Select the method for sending email invitations" setting specifies which email standard to use to send Remote Assistance invitations. Depending on your email program, you can use either the *Mailto* standard (the invitation recipient connects through an Internet link) or the SMAPI (Simple MAPI) standard (the invitation is attached to your email message). This policy setting isn't available in Windows Vista because SMAPI is the only method supported. If you enable this policy setting, you should also enable appropriate firewall exceptions to allow Remote Assistance communications.  
  [Learn more](/windows/client-management/mdm/policy-csp-remoteassistance#remoteassistance-solicitedremoteassistance)

  - Baseline default:  Disable Remote Assistance

## Remote Desktop Services

For more information, see [Policy CSP - RemoteDesktopServices](/windows/client-management/mdm/policy-csp-remotedesktopservices) in the Windows documentation.

- **Block password saving**:  
  Controls whether passwords can be saved on this computer from Remote Desktop Connection. If you enable this setting the password saving checkbox in Remote Desktop Connection is disabled and users can't save passwords. When a user opens an RDP file using Remote Desktop Connection and saves their settings, any password that previously existed in the RDP file are deleted. If you disable this setting or leave it not configured, the user can save passwords using Remote Desktop Connection.  
  [Learn more](/windows/client-management/mdm/policy-csp-remotedesktopservices#remotedesktopservices-donotallowpasswordsaving)

   - Baseline default:  Enabled

- **Secure RPC communication**:  
  Specifies whether a Remote Desktop Session Host server requires secure RPC communication with all clients or allows unsecured communication. You can use this setting to strengthen the security of RPC communication with clients by allowing only authenticated and encrypted requests. If the status is set to Enabled, Remote Desktop Services accepts requests from RPC clients that support secure requests, and doesn't allow unsecured communication with untrusted clients. If the status is set to Disabled, Remote Desktop Services always requests security for all RPC traffic. However, unsecured communication is allowed for RPC clients that don't respond to the request. If the status is set to Not Configured, unsecured communication is allowed. Note: The RPC interface is used for administering and configuring Remote Desktop Services.  
  [Learn more](/windows/client-management/mdm/policy-csp-remotedesktopservices#remotedesktopservices-requiresecurerpccommunication)

  - Baseline default:  Enabled

- **Block drive redirection**:  
  This policy setting specifies whether to prevent the mapping of client drives in a Remote Desktop Services session (drive redirection). By default, an RD Session Host server maps client drives automatically upon connection. Mapped drives appear in the session folder tree in File Explorer or Computer in the format *\<driveletter>* on *\<computername>*. You can use this policy setting to override this behavior. If you enable this policy setting, client drive redirection isn't allowed in Remote Desktop Services sessions, and Clipboard file copy redirection isn't allowed on computers running Windows Server 2003, Windows 8, and Windows XP. If you disable this policy setting, client drive redirection is always allowed. Also, Clipboard file copy redirection is always allowed if Clipboard redirection is allowed. If you don't configure this policy setting, client drive redirection and Clipboard file copy redirection aren't specified at the Group Policy level.  
  [Learn more](/windows/client-management/mdm/policy-csp-remotedesktopservices#remotedesktopservices-donotallowdriveredirection)

  - Baseline default:  Enabled

- **Prompt for password upon connection**:  
  This policy setting specifies whether Remote Desktop Services always prompts the client for a password upon connection. You can use this setting to enforce a password prompt for users logging on to Remote Desktop Services, even if they already provided the password in the Remote Desktop Connection client. By default, Remote Desktop Services allows users to automatically log on by entering a password in the Remote Desktop Connection client. If you enable this policy setting, users can't automatically log on to Remote Desktop Services by supplying their passwords in the Remote Desktop Connection client. they're prompted for a password to log on. If you disable this policy setting, users can always log on to Remote Desktop Services automatically by supplying their passwords in the Remote Desktop Connection client. If you don't configure this policy setting, automatic logon isn't specified at the Group Policy level.  
  [Learn more](/windows/client-management/mdm/policy-csp-remotedesktopservices#remotedesktopservices-promptforpassworduponconnection)

  - Baseline default:  Enabled

- **Remote desktop services client connection encryption level**:  
  Specifies whether to require the use of a specific encryption level to secure communications between client computers and RD Session Host servers during Remote Desktop Protocol (RDP) connections. This policy only applies when you're using native RDP encryption. However, native RDP encryption (as opposed to SSL encryption) isn't recommended. This policy doesn't apply to SSL encryption. If you enable this policy setting, all communications between clients and RD Session Host servers during remote connections must use the encryption method specified in this setting. By default, the encryption level is set to High. The following encryption methods are available:

  - *High* - The High setting encrypts data sent from the client to the server and from the server to the client by using strong 128-bit encryption. Use this encryption level in environments that contain only 128-bit clients (for example, clients that run Remote Desktop Connection). Clients that don't support this encryption level can't connect to RD Session Host servers.

  - *Client Compatible* - The Client Compatible setting encrypts data sent between the client and the server at the maximum key strength supported by the client. Use this encryption level in environments that include clients that don't support 128-bit encryption.

  - *Low* - The Low setting encrypts only data sent from the client to the server by using 56-bit encryption.  
  
  If you disable or don't configure this setting, the encryption level to be used for remote connections to RD Session Host servers isn't enforced through Group Policy. Important FIPS compliance can be configured through the System cryptography. Use FIPS-compliant algorithms for encryption, hashing, and signing settings in Group Policy (under Computer Configuration\Windows Settings\Security Settings\Local Policies\Security Options.) The FIPS-compliant setting encrypts and decrypts data sent from the client to the server and from the server to the client, with the Federal Information Processing Standard (FIPS) 140 encryption algorithms, by using Microsoft cryptographic modules. Use this encryption level when communications between clients and RD Session Host servers requires the highest level of encryption.  
  [Learn more](/windows/client-management/mdm/policy-csp-remotedesktopservices#remotedesktopservices-clientconnectionencryptionlevel)

  - Baseline default:  High

## Remote Management

For more information, see [Policy CSP - RemoteManagement](/windows/client-management/mdm/policy-csp-remotemanagement) in the Windows documentation.

- **Block storing run as credentials**:  
  Client basic authentication.  
  [Learn more](/windows/client-management/mdm/policy-csp-remotemanagement#remotemanagement-disallowstoringofrunascredentials)

  - Baseline default:  Enabled

- **Basic authentication**:  
  This policy setting allows you to manage whether the Windows Remote Management (WinRM) service accepts Basic authentication from a remote client. If you enable this policy setting, the WinRM service accepts Basic authentication from a remote client. If you disable or don't configure this policy setting, the WinRM service doesn't accept Basic authentication from a remote client.  
  [Learn more](/windows/client-management/mdm/policy-csp-remotemanagement#remotemanagement-allowbasicauthentication-service)

  - Baseline default:  Disabled

- **Block client digest authentication**:  
  This policy setting allows you to manage whether the Windows Remote Management (WinRM) client uses Digest authentication. If you enable this policy setting, the WinRM client doesn't use Digest authentication. If you disable or don't configure this policy setting, the WinRM client uses Digest authentication.  
  [Learn more](/windows/client-management/mdm/policy-csp-remotemanagement#remotemanagement-disallownegotiateauthenticationclient)

  - Baseline default:  Enabled

- **Unencrypted traffic**:  
  This policy setting allows you to manage whether the Windows Remote Management (WinRM) service sends and receives unencrypted messages over the network. If you enable this policy setting, the WinRM client sends and receives unencrypted messages over the network. If you disable or don't configure this policy setting, the WinRM client sends or receives only encrypted messages over the network.  
  [Learn more](/windows/client-management/mdm/policy-csp-remotemanagement#remotemanagement-allowunencryptedtraffic-service)

  - Baseline default:  Disabled

- **Client unencrypted traffic**:  
  This policy setting allows you to manage whether the Windows Remote Management (WinRM) client sends and receives unencrypted messages over the network. If you enable this policy setting, the WinRM client sends and receives unencrypted messages over the network. If you disable or don't configure this policy setting, the WinRM client sends or receives only encrypted messages over the network.  
  [Learn more](/windows/client-management/mdm/policy-csp-remotemanagement#remotemanagement-allowunencryptedtraffic-client)

  - Baseline default:  Disabled

- **Client basic authentication**:  
  This policy setting allows you to manage whether the Windows Remote Management (WinRM) client uses Basic authentication. If you enable this policy setting, the WinRM client uses Basic authentication. If WinRM is configured to use HTTP transport, the user name and password are sent over the network as clear text. If you disable or don't configure this policy setting, the WinRM client doesn't use Basic authentication.  
  [Learn more](/windows/client-management/mdm/policy-csp-remotemanagement#remotemanagement-allowbasicauthentication-client)

  - Baseline default:  Disabled

## Remote Procedure Call

For more information, see [Policy CSP - RemoteProcedureCall](/windows/client-management/mdm/policy-csp-remoteprocedurecall) in the Windows documentation.

- **RPC unauthenticated client options**:  
  This policy setting controls how the RPC server runtime handles unauthenticated RPC clients connecting to RPC servers. This policy setting impacts all RPC applications. In a domain environment, use this policy setting with caution as it can impact a wide range of functionality including group policy processing itself. Reverting a change to this policy setting can require manual intervention on each affected machine. Don't apply this policy setting to a domain controller. If you disable this policy setting, the RPC server runtime uses the value of "Authenticated" on Windows Client, and the value of "None" on Windows Server versions that support this policy setting. If you don't configure this policy setting, it remains disabled. The RPC server runtime behaves as though it was enabled with the value of "Authenticated" used for Windows Client and the value of "None" used for Server SKUs that support this policy setting. If you enable this policy setting, it directs the RPC server runtime to restrict unauthenticated RPC clients connecting to RPC servers running on a machine. A client is considered an authenticated client if it uses a named pipe to communicate with the server or if it uses RPC Security. RPC Interfaces that have specifically requested to be accessible by unauthenticated clients may be exempt from this restriction, depending on the selected value for this policy setting.

  - *None* allows all RPC clients to connect to RPC Servers running on the machine on which the policy setting is applied.

  - *Authenticated* allows only authenticated RPC Clients (per the definition above) to connect to RPC Servers running on the machine on which the policy setting is applied. Exemptions are granted to interfaces that have requested them.

  - *Authenticated without exceptions* allows only authenticated RPC Clients (per the definition above) to connect to RPC Servers running on the machine on which the policy setting is applied. No exceptions are allowed. Note: This policy setting won't be applied until the system is rebooted.

  [Learn more](/windows/client-management/mdm/policy-csp-remoteprocedurecall#remoteprocedurecall-rpcendpointmapperclientauthentication)

  - Baseline default:  Authenticated

## Search

For more information, see [Policy CSP - Search](/windows/client-management/mdm/policy-csp-search) in the Windows documentation.

- **Disable indexing encrypted items**:  
  Allows or disallows the indexing of items. This switch is for the Windows Search Indexer, which controls whether it will index items that are encrypted, such as the Windows Information Protection (WIP) protected files. When the policy is enabled, WIP protected items are indexed and the metadata about them are stored in an unencrypted location. The metadata includes things like file path and date modified. When the policy is disabled, the WIP protected items aren't indexed and don't show up in the results in Cortana or file explorer. There may also be a performance impact on photos and Groove apps if there are many WIP protected media files on the device.  
  [Learn more]( https://go.microsoft.com/fwlink/?linkid=2067303)

  - Baseline default:  Yes

## Smart Screen

For more information, see [Policy CSP - SmartScreen](/windows/client-management/mdm/policy-csp-smartscreen) in the Windows documentation.

- **Turn on Windows SmartScreen**  
  CSP: [SmartScreen/EnableSmartScreenInShell](/windows/client-management/mdm/policy-csp-smartscreen#smartscreen-enablesmartscreeninshell)

  Setting this to Yes will enforce the use of SmartScreen for all users. Setting this to Not configured will return the setting to Windows default, which is to enable SmartScreen, however users may change this setting. To disable SmartScreen, use a custom URI.

  - Baseline default:  Yes

- **Block users from ignoring SmartScreen warnings**  
  CSP: [SmartScreen/PreventOverrideForFilesInShell](/windows/client-management/mdm/policy-csp-smartscreen#smartscreen-preventoverrideforfilesinshell)

  When set to Yes, SmartScreen is enabled and users can't bypass warnings for files or malicious apps. When set to Not configured, users can ignore SmartScreen warnings for files and malicious apps.  

  This setting requires the 'Turn on Windows SmartScreen' setting be set to Yes.

  - Baseline default:  Yes

## System

For more information, see [Policy CSP - System](/windows/client-management/mdm/policy-csp-system) in the Windows documentation.

- **System boot start driver initialization**:  
  This policy setting allows you to specify which boot-start drivers are initialized based on a classification determined by an Early Launch Antimalware boot-start driver. The Early Launch Antimalware boot-start driver can return the following classifications for each boot-start driver:

  - *Good* - The driver has been signed and hasn't been tampered with.

  - *Bad* - The driver has been identified as malware. We recommend that you don't allow known bad drivers to be initialized.

  - *Bad, but required for boot* - The driver has been identified as malware, but the computer can't successfully boot without loading this driver.

  - *Unknown* - This driver hasn't been attested to by your malware detection application and hasn't been classified by the Early Launch Antimalware boot-start driver.

  If you enable this policy setting, you can choose which boot-start drivers to initialize the next time the computer is started. If you disable or don't configure this policy setting, the boot start drivers determined to be Good, Unknown, or Bad but Boot Critical are initialized and the initialization of drivers determined to be Bad is skipped. If your malware detection application doesn't include an Early Launch Antimalware boot-start driver or if your Early Launch Antimalware boot-start driver has been disabled, this setting has no effect and all boot-start drivers are initialized.  
  [Learn more](/windows/client-management/mdm/policy-csp-system#system-bootstartdriverinitialization)

  - Baseline default:  Good unknown and bad critical

## Wi-Fi

For more information, see [Policy CSP - Wifi](/windows/client-management/mdm/policy-csp-wifi) in the Windows documentation.

- **Block Automatically connecting to Wi-Fi hotspots**:  
  Allow or disallow the device to automatically connect to Wi-Fi hotspots.  
  [Learn more](/windows/client-management/mdm/policy-csp-wifi#wifi-allowautoconnecttowifisensehotspots)

  - Baseline default:  Yes

- **Block Internet sharing**:  
  Specifies whether internet sharing is possible on the device.  
  [Learn more](/windows/client-management/mdm/policy-csp-wifi#wifi-allowinternetsharing)

  - Baseline default:  Yes

## Windows Connection Manager

For more information, see [Policy CSP - WindowsConnectionManager](/windows/client-management/mdm/policy-csp-windowsconnectionmanager) in the Windows documentation.

- **Block connection to non-domain networks**:  
  This policy setting prevents computers from connecting to both a domain-based network and a non-domain based network at the same time. If this policy setting is enabled, the computer responds to automatic and manual network connection attempts based on the following circumstances:

  - *Automatic connection attempts* - When the computer is already connected to a domain-based network, all automatic connection attempts to non-domain networks are blocked. When the computer is already connected to a non-domain based network, automatic connection attempts to domain-based networks are blocked.

  - *Manual connection attempts* - When the computer is already connected to either a non-domain based network or a domain-based network over media other than Ethernet, and a user attempts to create a manual connection to an additional network in violation of this policy setting, the existing network connection disconnects, and the manual connection is allowed. When the computer is already connected to either a non-domain based network or a domain-based network over Ethernet, and a user attempts to create a manual connection to an additional network in violation of this policy setting, the existing Ethernet connection is maintained and the manual connection attempt is blocked.

  If this policy setting isn't configured or is disabled, computers are allowed to connect simultaneously to both domain and non-domain networks.  
  [Learn more](/windows/client-management/mdm/policy-csp-windowsconnectionmanager)

  - Baseline default:  Enabled

## Windows Ink Workspace

For more information, see [Policy CSP - WindowsInkWorkspace](/windows/client-management/mdm/policy-csp-windowsinkworkspace) in the Windows documentation.

- **Ink Workspace**:  
  Specifies whether to allow the user to access the ink workspace.

  - *Disabled* - access to ink workspace is disabled. The feature is turned off.

  - *Enabled* - The Ink Workspace feature is turned on, but the user can't access it above the lock screen.

  - *Not Configured* - The Ink Workspace feature is turned on, and the user can use it above the lock screen.

  [Learn more](/windows/client-management/mdm/policy-csp-windowsinkworkspace#windowsinkworkspace-allowwindowsinkworkspace)

  - Baseline default:  Enabled

## Windows PowerShell

For more information, see [Policy CSP - WindowsPowerShell](/windows/client-management/mdm/policy-csp-windowspowershell) in the Windows documentation.

- **PowerShell script block logging**:  
  This policy setting enables logging of all PowerShell script input to the Microsoft-Windows-PowerShell/Operational event log. If you enable this policy setting, Windows PowerShell will log the processing of commands, script blocks, functions, and scripts - whether invoked interactively, or through automation. If you disable this policy setting, logging of PowerShell script input is disabled. If you enable the Script Block Invocation Logging, PowerShell additionally logs events when invocation of a command, script block, function, or script starts or stops. Enabling Invocation Logging generates a high volume of event logs. Note: This policy setting exists under both Computer Configuration and User Configuration in the Group Policy Editor. The Computer Configuration policy setting takes precedence over the User Configuration policy setting.  
  [Learn more](/windows/client-management/mdm/policy-csp-windowspowershell#windowspowershell-turnonpowershellscriptblocklogging)

  - Baseline default:  Enabled

::: zone-end

## Next steps

- [Learn about security baselines](security-baselines.md)
- [Avoid conflicts](security-baselines.md#avoid-conflicts)
- [Troubleshoot policies and profiles in Intune](/troubleshoot/mem/intune/troubleshoot-policies-in-microsoft-intune)
