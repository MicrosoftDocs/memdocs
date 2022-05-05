---
# required metadata

title: Settings list for the Windows 10/11 MDM security baselines in Microsoft Intune
titleSuffix: Microsoft Intune
description: View the settings list from the Microsoft Intune security baseline for Windows 10/11 MDM security. This list includes the default values for settings as found in the default configuration of the baseline.
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


# List of the settings in the Windows 10/11 MDM security baseline in Intune

This article is a reference for the settings that are available in the different versions of the Windows 10/11 MDM security baseline that you can deploy with Microsoft Intune. You can use the tabs below to select and view the current baseline version as well as a few older versions that might still be in use.

For each setting you'll see the settings default configuration, which is also the recommended configuration for that setting from the relevant security team. Because the products and the security landscape evolves, the recommended defaults for one baseline version might not match the defaults you find in other versions of the same baseline, or for the same setting found in a different baseline, such as the Defender for Endpoint baseline.  

When a new baseline version releases, it replaces the previous version.  Profiles that were created prior to the availability of a new baseline version:

- Become read-only. You can continue to use those profiles, but can't edit them to change their configuration.
- Can be updated to the latest version. After you update to the current baseline version, you can edit the profile to modify settings.

To learn more about using security baselines, see [Use security baselines](security-baselines.md). In that article you'll also find information about how to:

- [Compare baselines](../protect/security-baselines.md#compare-baseline-versions) to discover what's changed from version to version. 
- [Change the baseline version for a profile](../protect/security-baselines-configure.md#change-the-baseline-version-for-a-profile) to update a profile to use the latest version of that baseline. 

## [November 2021](#tab/nov-2021)

**Security Baseline for Windows 10 and later for November 2021**

## Above Lock

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
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067141)

- **Block Internet download for web publishing and online ordering wizards**:  
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

## Device Lock

- **Require password**:  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067049)  

  - **Required password**:  
    Baseline default: *Alphanumeric*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=2067027)

  - **Password expiration (days)**:  
    Baseline default: *60*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=2067028)

  - **Password minimum character set count**:  
    Baseline default: *3*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=2067055)

  - **Prevent reuse of previous passwords**:  
    Baseline default: *24*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=2066795)

  - **Minimum password length**:  
    Baseline default: *8*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=2067024)

  - **Number of sign-in failures before wiping device**:  
    Baseline default: *10*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=2067030)

  - **Block simple passwords**:  
    Baseline default: *Yes*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=2067127)

- **Password minimum age in days**:  
  Baseline default: *1*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067022)

- **Prevent use of camera**:  
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067052)

- **Prevent slide show**:  
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067105)

## DMA Guard

- **Enumeration of external devices incompatible with Kernel DMA Protection**:  
  Baseline default: *Block all*

## Event Log Service

- **Application log maximum file size in KB**:  
  Baseline default: *32768*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067125)

- **System log maximum file size in KB**:  
  Baseline default: *32768*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2066798)

- **Security log maximum file size in KB**:  
  Baseline default: *196608*  
  [Learn more](/https://go.microsoft.com/fwlink/?linkid=2067042)

## Experience

- **Block Windows Spotlight**:  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067037)

  - **Block third-party suggestions in Windows Spotlight**:  
    Baseline default: *Not configured*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=2067045)

  - **Block consumer specific features**:  
    Baseline default: *Not configured*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=2067054)














## [December 2020](#tab/dec-2020)

**Security Baseline for Windows 10 and later for December 2020**

## Above Lock

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
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067141)

- **Block Internet download for web publishing and online ordering wizards**:  
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

## Device Lock

- **Require password**:  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067049)  

  - **Required password**:  
    Baseline default: *Alphanumeric*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=2067027)

  - **Password expiration (days)**:  
    Baseline default: *60*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=2067028)

  - **Password minimum character set count**:  
    Baseline default: *3*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=2067055)

  - **Prevent reuse of previous passwords**:  
    Baseline default: *24*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=2066795)

  - **Minimum password length**:  
    Baseline default: *8*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=2067024)

  - **Number of sign-in failures before wiping device**:  
    Baseline default: *10*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=2067030)

  - **Block simple passwords**:  
    Baseline default: *Yes*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=2067127)

- **Password minimum age in days**:  
  Baseline default: *1*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067022)

- **Prevent use of camera**:  
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067052)

- **Prevent slide show**:  
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067105)

## DMA Guard

- **Enumeration of external devices incompatible with Kernel DMA Protection**:  
  Baseline default: *Block all*

## Event Log Service

- **Application log maximum file size in KB**:  
  Baseline default: *32768*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067125)

- **System log maximum file size in KB**:  
  Baseline default: *32768*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2066798)

- **Security log maximum file size in KB**:  
  Baseline default: *196608*  
  [Learn more](/https://go.microsoft.com/fwlink/?linkid=2067042)

## Experience

- **Block Windows Spotlight**:  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067037)

  - **Block third-party suggestions in Windows Spotlight**:  
    Baseline default: *Not configured*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=2067045)

  - **Block consumer specific features**:  
    Baseline default: *Not configured*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=2067054)












## [August 2020](#tab/aug-2020)

**Security Baseline for Windows 10 and later for August 2020**

## Above Lock

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
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067141)

- **Block Internet download for web publishing and online ordering wizards**:  
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

## Exploit Guard

- **Upload XML**:  
  Baseline default: *Sample xml is provided*
  [Learn more](/windows/client-management/mdm/policy-csp-exploitguard#exploitguard-exploitprotectionsettings)














## File Explorer

- **Block data execution prevention**:  
  Baseline default: *Disabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067043)

- **Block heap termination on corruption**:  
  Baseline default: *Disabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067107)

## Firewall

For more information, see [2.2.2 FW_PROFILE_TYPE](https://go.microsoft.com/fwlink/?linkid=2066796) in the Windows Protocols documentation.

- **Firewall profile domain**:  
  Baseline default: *Configure*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2066796)

  - **Inbound connections blocked**:  
    Baseline default: *Yes*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=872564)

  - **Outbound connections required**:  
    Baseline default: *Yes*  
    [Learn more](https://aka.ms/intune-firewall-outboundaction)

  - **Inbound notifications blocked**:  
    Baseline default: *Yes*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=872563)

  - **Firewall enabled**:  
    Baseline default: *Allowed*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=872558)

- **Firewall profile private**:  
  Baseline default: *Configure*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067041)

  - **Inbound connections blocked**:  
    Baseline default: *Yes*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=872564)

  - **Outbound connections required**:  
    Baseline default: *Yes*  
    [Learn more](https://aka.ms/intune-firewall-outboundaction)

  - **Inbound notifications blocked**:  
    Baseline default: *Yes*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=872563)

  - **Firewall enabled**:  
    Baseline default: *Allowed*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=872558)

- **Firewall profile public**:  
  Baseline default: *Configure*  
  [Learn more](/openspecs/windows_protocols/ms-fasp/7704e238-174d-4a5e-b809-5f3787dd8acc)

  - **Inbound connections blocked**:  
    Baseline default: *Yes*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=872564)

  - **Outbound connections required**:  
    Baseline default: *Yes*  
    [Learn more](https://aka.ms/intune-firewall-outboundaction)

  - **Inbound notifications blocked**:  
    Baseline default: *Yes*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=872563)

  - **Firewall enabled**:  
    Baseline default: *Allowed*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=872558)

  - **Connection security rules from group policy not merged**:  
    Baseline default: *Yes*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=872568)

  - **Policy rules from group policy not merged**:  
    Baseline default: *Yes*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=872567)

## Internet Explorer

- **Internet Explorer encryption support**:  
  Baseline default: 2 items:  *TLS v1.1* and *TLS v1.2*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067057)

- **Internet Explorer prevent managing smart screen filter**:  
  Baseline default: *Enable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067135)

- **Internet Explorer restricted zone script Active X controls marked safe for scripting**:  
  Baseline default: *Disable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067062)

- **Internet Explorer restricted zone file downloads**:  
  Baseline default: *Disable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067038)

- **Internet Explorer certificate address mismatch warning**:  
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067153)  

- **Internet Explorer enhanced protected mode**:  
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067158)

- **Internet Explorer fallback to SSL3**:  
  Baseline default: *No sites*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067118)

- **Internet Explorer software when signature is invalid**:  
  Baseline default: *Disabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067201)

- **Internet Explorer check server certificate revocation**:  
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067046)

- **Internet Explorer check signatures on downloaded programs**:  
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067051)

- **Internet Explorer processes consistent MIME handling**:  
  Baseline default: *Enable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067144)  

- **Internet Explorer bypass smart screen warnings**:  
  Baseline default: *Disabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067159)

- **Internet Explorer bypass smart screen warnings about uncommon files**:  
  Baseline default: *Disable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067068)

- **Internet Explorer crash detection**:  
  Baseline default: *Disabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067094)

- **Internet Explorer download enclosures**:  
  Baseline default: *Disabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067245)

- **Internet Explorer ignore certificate errors**:  
  Baseline default: *Disabled*
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067071)

- **Internet Explorer disable processes in enhanced protected mode**:  
  Baseline default: *Enabled*
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067149)

- **Internet Explorer security settings check**:  
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067182)

- **Internet Explorer Active X controls in protected mode**:  
  Baseline default: *Disabled*
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067145)

- **Internet Explorer users adding sites**:  
  Baseline default: *Disabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067167)

- **Internet Explorer users changing policies**:  
  Baseline default: *Disabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067155)

- **Internet Explorer block outdated Active X controls**:  
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067203)

- **Internet Explorer include all network paths**:  
  Baseline default: *Disabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067090)

- **Internet Explorer internet zone access to data sources**:  
  Baseline default: *Disabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067078)  

- **Internet Explorer internet zone automatic prompt for file downloads**:  
  Baseline default: *Disabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067117)

- **Internet Explorer internet zone copy and paste via script**:  
  Baseline default: *Disable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067084)

- **Internet Explorer internet zone drag and drop or copy and paste files**:  
  Baseline default: *Disabled*.  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067076)

- **Internet Explorer internet zone less privileged sites**:  
  Baseline default: *Disable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067109)

- **Internet Explorer internet zone loading of XAML files**:  
  Baseline default: *Disable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067147)

- **Internet Explorer internet zone .NET Framework reliant components**:  
  Baseline default: *Disabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067073)

- **Internet Explorer internet zone allow only approved domains to use ActiveX controls**:  
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067091)

- **Internet Explorer internet zone allow only approved domains to use tdc ActiveX controls**:  
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067151)

- **Internet Explorer internet zone scripting of web browser controls**:  
  Baseline default: *Disabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067157)

- **Internet Explorer internet zone script initiated windows**:  
  Baseline default: *Disabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067088)

- **Internet Explorer internet zone scriptlets**:  
  Baseline default: *Disable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067176)

- **Internet Explorer internet zone smart screen**:  
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067047)

- **Internet Explorer internet zone updates to status bar via script**:  
  Baseline default: *Disabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067087)

- **Internet Explorer internet zone user data persistence**:  
  Baseline default: *Disabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067156)

- **Internet Explorer internet zone allow VBscript to run**:  
  Baseline default: *Disable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067119)

- **Internet Explorer internet zone do not run antimalware against ActiveX controls**:  
  Baseline default: *Disabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067162)

- **Internet Explorer internet zone download signed ActiveX controls**:  
  Baseline default: *Disable*Baseline default: *Disable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067064)

- **Internet Explorer internet zone download unsigned ActiveX controls**:  
  Baseline default: *Disable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067325)

- **Internet Explorer internet zone cross site scripting filter**:  
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067053)

- **Internet Explorer internet zone drag content from different domains across windows**:  
  Baseline default: *Disabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067093)

- **Internet Explorer internet zone drag content from different domains within windows**:  
 Baseline default: *Disabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067095)

- **Internet Explorer internet zone protected mode**:  
  Baseline default: *Enable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067171)

- **Internet Explorer internet zone include local path when uploading files to server**:  
  Baseline default: *Disabled*
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067072)

- **Internet Explorer internet zone initialize and script Active X controls not marked as safe**:  
  Baseline default: *Disable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067170)

- **Internet Explorer internet zone java permissions**:  
  Baseline default: *Disable java*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067174)

- **Internet Explorer internet zone launch applications and files in an iframe**:  
  Baseline default: *Disable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067020)

- **Internet Explorer internet zone logon options**:  
  Baseline default: *Prompt*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067194)

- **Internet Explorer internet zone navigate windows and frames across different domains**:  
  Baseline default: *Disable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067083)

- **Internet Explorer internet zone run .NET Framework reliant components signed with Authenticode**:  
  Baseline default: *Disable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067033)

- **Internet Explorer internet zone security warning for potentially unsafe files**:  
  Baseline default: *Prompt*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067204)

- **Internet Explorer internet zone popup blocker**:  
  Baseline default: *Enable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067069)

- **Internet Explorer intranet zone do not run antimalware against Active X controls**:  
  Baseline default: *Disabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067138)

- **Internet Explorer intranet zone initialize and script Active X controls not marked as safe**:  
  Baseline default: *Disable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067175)

- **Internet Explorer intranet zone java permissions**:  
  Baseline default: *High safety*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067206)

- **Internet Explorer local machine zone do not run antimalware against Active X controls**:  
  Baseline default: *Disabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067152)

- **Internet Explorer local machine zone java permissions**:  
  TBaseline default: *Disable java*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067113)

- **Internet Explorer locked down internet zone smart screen**:  
  Baseline default: *Enabled*.  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067059)

- **Internet Explorer locked down intranet zone java permissions**:  
  Baseline default: *Disable java*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067082)

- **Internet Explorer locked down local machine zone java permissions**:  
  Baseline default: *Disable java*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067253)

- **Internet Explorer locked down restricted zone smart screen**:  
 Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067092)

- **Internet Explorer locked down restricted zone java permissions**:  
  Baseline default: *Disable Java*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067181)

- **Internet Explorer locked down trusted zone java permissions**:  
  Baseline default: *Disable java*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067142)

- **Internet Explorer processes MIME sniffing safety feature**:  
  Baseline default: *Enable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067124)

- **Internet Explorer processes MK protocol security restriction**:  
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067179)

- **Internet Explorer processes notification bar**:  
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067139)

- **Internet Explorer prevent per user installation of Active X controls**:  
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067058)

- **Internet Explorer processes protection from zone elevation**:  
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067160)

- **Internet Explorer remove run this time button for outdated Active X controls**:  
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067123)

- **Internet Explorer processes restrict Active X install**:  
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067250)

- **Internet Explorer restricted zone access to data sources**:  
  Baseline default: *Disable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067161)

- **Internet Explorer restricted zone active scripting**:  
  Baseline default: *Disable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067172)

- **Internet Explorer restricted zone automatic prompt for file downloads**:  
  Baseline default: *Disabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067150)

- **Internet Explorer restricted zone binary and script behaviors**:  
  Baseline default: *Disable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067224)

- **Internet Explorer restricted zone copy and paste via script**:  
  Baseline default: *Disable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067165)

- **Internet Explorer restricted zone drag and drop or copy and paste files**:  
  Baseline default: *Disable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067096)

- **Internet Explorer restricted zone less privileged sites**:  
  Baseline default: *Disabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067148)

- **Internet Explorer restricted zone loading of XAML files**:  
  Baseline default: *Disable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067070)

- **Internet Explorer restricted zone meta refresh**:  
  Baseline default: *Disabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067154)

- **Internet Explorer restricted zone .NET Framework reliant components**:  
   Baseline default: *Disabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067077)

- **Internet Explorer restricted zone allow only approved domains to use Active X controls**:  
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067233)

- **Internet Explorer restricted zone allow only approved domains to use tdc Active X controls**:  
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067032)

- **Internet Explorer restricted zone scripting of web browser controls**:  
  Baseline default: *Disabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067098)

- **Internet Explorer restricted zone script initiated windows**:  
  Baseline default: *Disabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067075)

- **Internet Explorer restricted zone scriptlets**:  
  Baseline default: *Disabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067112)

- **Internet Explorer restricted zone smart screen**:  
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067034)

- **Internet Explorer restricted zone updates to status bar via script**:  
  Baseline default: *Disabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067074)

- **Internet Explorer restricted zone user data persistence**:  
  Baseline default: *Disabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067081)

- **Internet Explorer restricted zone allow vbscript to run**:  
  Baseline default: *Disable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067173)

- **Internet Explorer restricted zone do not run antimalware against Active X controls**:  
  Baseline default: *Disabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067089)

- **Internet Explorer restricted zone download signed Active X controls**:  
  Baseline default: *Disable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067120)

- **Internet Explorer restricted zone download unsigned Active X controls**:  
 Baseline default: *Disable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067177)

- **Internet Explorer restricted zone cross site scripting filter**:  
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067178)

- **Internet Explorer restricted zone drag content from different domains across windows**:  
  Baseline default: *Disabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067166)

- **Internet Explorer restricted zone drag content from different domains within windows**:  
  Baseline default: *Disabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067079)  

- **Internet Explorer restricted zone include local path when uploading files to server**:  
  Baseline default: *Disabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067085)

- **Internet Explorer restricted zone initialize and script Active X controls not marked as safe**:  
  Baseline default: *Disable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067097)

- **Internet Explorer restricted zone java permissions**:  
  Baseline default: *Disable java*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067132)

- **Internet Explorer restricted zone launch applications and files in an iFrame**:  
  Baseline default: *Disable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067061)

- **Internet Explorer restricted zone logon options**:  
  Baseline default: *Anonymous*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067110)

- **Internet Explorer restricted zone navigate windows and frames across different domains**:  
  Baseline default: *Disable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067050)

- **Internet Explorer restricted zone run Active X controls and plugins**:  
  Baseline default: *Disable*.  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067114)

- **Internet Explorer restricted zone run .NET Framework reliant components signed with Authenticode**:  
  Baseline default: *Disable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067169)

- **Internet Explorer restricted zone scripting of java applets**:  
  Baseline default: *Disable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067202)

- **Internet Explorer restricted zone security warning for potentially unsafe files**:  
  Baseline default: *Disable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2066797)

- **Internet Explorer restricted zone protected mode**:  
  Baseline default: *Enable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067080)

- **Internet Explorer restricted zone popup blocker**:  
  Baseline default: *Enable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067180)

- **Internet Explorer processes restrict file download**:  
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067164)

- **Internet Explorer processes scripted window security restrictions**:  
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067146)

- **Internet Explorer security zones use only machine settings**:  
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067086)

- **Internet Explorer use Active X installer service**:  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-specifyuseofactivexinstallerservice)

- **Internet Explorer trusted zone do not run antimalware against Active X controls**:  
  Baseline default: *Disabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067115)

- **Internet Explorer trusted zone initialize and script Active X controls not marked as safe**:  
  Baseline default: *Disable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067137)

- **Internet Explorer trusted zone java permissions**:  
  Baseline default: *High safety*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067200)

- **Internet Explorer auto complete**:  
  Baseline default: *Disabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067122)


















## Local Policies Security Options

For more information, see [Policy CSP - LocalPoliciesSecurityOptions](/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions) in the Windows documentation.

- **Restrict anonymous access to named pipes and shares**:  
  When enabled, this security setting restricts anonymous access to shares and pipes to the settings for: (1) Named pipes that can be accessed anonymously (2) Shares that can be accessed anonymously.  
  [Learn more](/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions#localpoliciessecurityoptions-networkaccess-restrictanonymousaccesstonamedpipesandshares)

Baseline default: *Yes*

- **Minimum session security for NTLM SSP based servers**:  
  This security setting allows a server to require the negotiation of 128-bit encryption and NTLMv2 session security. These values are dependent on the LAN Manager Authentication Level security setting value. The options are: Require NTLMv2 session security: The connection will fail if message integrity isn't negotiated. Require 128-bit encryption. The connection will fail if strong encryption (128-bit) isn't negotiated.  
  [Learn more](/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions#localpoliciessecurityoptions-networksecurity-minimumsessionsecurityforntlmsspbasedservers)

Baseline default: *Require NTLM V2 and 128 bit encryption*

- **Minutes of lock screen inactivity until screen saver activates**:  
  Windows notices inactivity of a logon session, and if the amount of inactive time exceeds the inactivity limit, then the screen saver will run, locking the session.  
  [Learn more](/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions#localpoliciessecurityoptions-interactivelogon-machineinactivitylimit)

Baseline default: *15*

- **Require client to always digitally sign communications**:  
  This security setting determines whether all secure channel traffic initiated by the domain member must be signed or encrypted. When a computer joins a domain, a computer account is created. After that, when the system starts, it uses the computer account password to create a secure channel with a domain controller for its domain. This secure channel is used to do operations such as NTLM pass through authentication, LSA SID/name Lookup and more. This setting determines if all secure channel traffic initiated by the domain member meets minimum security requirements. Specifically it determines whether all secure channel traffic started by the domain member must be signed or encrypted. If this policy is enabled, then the secure channel won't be established unless either signing or encryption of all secure channel traffic is negotiated. If this policy is disabled, then encryption and signing of all secure channel traffic is negotiated with the Domain Controller in which case the level of signing and encryption depends on the version of the Domain Controller and the settings of the following two policies: Domain member: Digitally encrypt secure channel data (when possible) Domain member: Digitally sign secure channel data (when possible).  
  [Learn more](/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions#localpoliciessecurityoptions-microsoftnetworkclient-digitallysigncommunicationsalways)

Baseline default: *Yes*

- **Authentication level**:  
  This security setting determines which challenge/response authentication protocol is used for network logons. This choice affects the level of authentication protocol used by clients, the level of session security negotiated, and the level of authentication accepted by servers as follows:

  - *Send LM and NTLM responses* - Clients use LM and NTLM authentication and never use NTLMv2 session security; domain controllers accept LM, NTLM, and NTLMv2 authentication.

  - *Send LM and NTLM - NTLMv2 if negotiated* - Clients use LM and NTLM authentication and use NTLMv2 session security if the server supports it. Domain controllers accept LM, NTLM, and NTLMv2 authentication.

  - *Send NTLM response only* - Clients use NTLM authentication only and use NTLMv2 session security if the server supports it; domain controllers accept LM, NTLM, and NTLMv2 authentication.

  - *Send NTLMv2 response only* - Clients use NTLMv2 authentication only and use NTLMv2 session security if the server supports it; domain controllers accept LM, NTLM, and NTLMv2 authentication.

  - *Send NTLMv2 response only. Refuse LM* - Clients use NTLMv2 authentication only and use NTLMv2 session security if the server supports it. Domain controllers refuse LM (accept only NTLM and NTLMv2 authentication).

  - *Send NTLMv2 response only. Refuse LM and NTLM* - Clients use NTLMv2 authentication only and use NTLMv2 session security if the server supports it. Domain controllers refuse LM and NTLM (accept only NTLMv2 authentication).

  [Learn more](/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions#localpoliciessecurityoptions-networksecurity-lanmanagerauthenticationlevel)

Baseline default: *Send NTLMv2 response only. Refuse LM and NTLM*

- **Prevent clients from sending unencrypted passwords to third party SMB servers**:  
  If this security setting is enabled, the Server Message Block (SMB) redirector can send plaintext passwords to non-Microsoft SMB servers that don't support password encryption during authentication. Sending unencrypted passwords is a security risk.  
  [Learn more](/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions#localpoliciessecurityoptions-microsoftnetworkclient-sendunencryptedpasswordtothirdpartysmbservers)

Baseline default: *Yes*

- **Require server digitally signing communications always**:  
  This security setting determines whether the SMB client attempts to negotiate SMB packet signing. The server message block (SMB) protocol provides the basis for Microsoft file and print sharing and many other networking operations, such as remote Windows administration. To prevent man-in-the-middle attacks that modify SMB packets in transit, the SMB protocol supports the digital signing of SMB packets. This policy setting determines whether the SMB client component attempts to negotiate SMB packet signing when it connects to an SMB server. If this setting is enabled, the Microsoft network client will ask the server to do SMB packet signing upon session setup. If packet signing has been enabled on the server, packet signing is negotiated. If this policy is disabled, the SMB client will never negotiate SMB packet signing.  
  [Learn more](/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions#localpoliciessecurityoptions-microsoftnetworkserver-digitallysigncommunicationsalways)

Baseline default: *Yes*

- **Administrator elevation prompt behavior**:  
  This policy setting controls the behavior of the elevation prompt for administrators. The options are:

  - *Elevate without prompting* - Allows privileged accounts to do an operation that requires elevation without requiring consent or credentials. Note: Use this option only in the most constrained environments.

  - *Prompt for credentials on the secure desktop* - When an operation requires elevation of privilege, the user is prompted on the secure desktop to enter a privileged user name and password. If the user enters valid credentials, the operation continues with the user's highest available privilege.

  - *Prompt for consent on the secure desktop* - When an operation requires elevation of privilege, the user is prompted on the secure desktop to select either Permit or Deny. If the user selects Permit, the operation continues with the user's highest available privilege.

  - *Prompt for credentials* - When an operation requires elevation of privilege, the user is prompted to enter an administrative user name and password. If the user enters valid credentials, the operation continues with the applicable privilege.

  - *Prompt for consent* - When an operation requires elevation of privilege, the user is prompted to select either Permit or Deny. If the user selects Permit, the operation continues with the user's highest available privilege.

  - *Prompt for consent for non-Windows binaries* - When an operation for a non-Microsoft application requires elevation of privilege, the user is prompted on the secure desktop to select either Permit or Deny. If the user selects Permit, the operation continues with the user's highest available privilege.

  [Learn more](/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions#localpoliciessecurityoptions-useraccountcontrol-behavioroftheelevationpromptforadministrators)

Baseline default: *Prompt for consent on the secure desktop*

- **Minimum session security for NTLM SSP based clients**:  
  This security setting allows a client to require the negotiation of 128-bit encryption and NTLMv2 session security. These values are dependent on the LAN Manager Authentication Level security setting value. The options are:

  - *Require NTLMv2 session security* - The connection will fail if NTLMv2 protocol isn't negotiated.

  - *Require 128-bit encryption* - The connection will fail if strong encryption (128-bit) isn't negotiated.

  - *Require NTLMv2 and 128-bit encryption*.

  [Learn more](/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions#localpoliciessecurityoptions-networksecurity-minimumsessionsecurityforntlmsspbasedclients)

Baseline default: *Require NTLM V2 128 encryption*

- **Smart card removal behavior**:  
  This security setting determines what happens when the smart card for a logged-on user is removed from the smart card reader. The options are:

  - *No action*.

  - *Lock Workstation* - The workstation is locked when the smart card is removed, allowing users to leave the area, take their smart card with them, and still maintain a protected session.

  - *Force Logoff* - the user is automatically logged off when the smart card is removed.

  - *Disconnect Remote Desktop session* - Removal of the smart card disconnects the session without logging the user off. This allows the user to insert the smart card and resume the session later, or at another smart card reader-equipped computer, without having to log on again. If the session is local, this policy functions identically to Lock Workstation.

  [Learn more](/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions#localpoliciessecurityoptions-interactivelogon-smartcardremovalbehavior)

Baseline default: *Lock workstation*

- **Block anonymous enumeration of SAM accounts and shares**:  
  This security setting determines whether to allow anonymous enumeration of SAM accounts and shares. Windows allows anonymous users to do certain activities, such as enumerating the names of domain accounts and network shares. This is convenient, for example, when an administrator wants to grant access to users in a trusted domain that doesn't maintain a reciprocal trust. If you don't want to allow anonymous enumeration of SAM accounts and shares, then set this policy to *Yes*.  
  [Learn more](/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions#localpoliciessecurityoptions-networkaccess-donotallowanonymousenumerationofsamaccountsandshares)

Baseline default: *Yes*

- **Block remote logon with blank password**:  
  This security setting determines whether local accounts that aren't password protected can be used to log on from locations other than the physical computer console. If enabled, local accounts that aren't password protected must use the computer's keyboard to log on.

  *Warning*: Computers that aren't in physically secure locations should always enforce strong password policies for all local user accounts. Otherwise, anyone with physical access to the computer can log on by using a user account that doesn't have a password. This is especially important for portable computers.

  If you apply this security policy to the Everyone group, no one can log on through Remote Desktop Services. This setting doesn't affect logons that use domain accounts. It's possible for applications that use remote interactive logons to bypass this setting.  
  [Learn more](/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions#localpoliciessecurityoptions-accounts-limitlocalaccountuseofblankpasswordstoconsolelogononly)

Baseline default: *Yes*

- **Standard user elevation prompt behavior**:  
  This policy setting controls the behavior of the elevation prompt for standard users.

  - *Automatically deny elevation requests* - When an operation requires elevation of privilege, a configurable access denied error message is displayed. An enterprise that is running desktops as standard user may choose this setting to reduce help desk calls.

  - *Prompt for credentials on the secure desktop* - When an operation requires elevation of privilege, the user is prompted on the secure desktop to enter a different user name and password. If the user enters valid credentials, the operation continues with the applicable privilege.

  - *Prompt for credentials* - When an operation requires elevation of privilege, the user is prompted to enter an administrative user name and password. If the user enters valid credentials, the operation continues with the applicable privilege.

  [Learn more](/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions#localpoliciessecurityoptions-useraccountcontrol-behavioroftheelevationpromptforstandardusers)

Baseline default: *Automatically deny elevation requests*

- **Require admin approval mode for administrators**:  
  This policy setting controls the behavior of all User Account Control (UAC) policy settings for the computer. If you change this policy setting, you must restart your computer. The options are:

  - *Not configured* - Admin Approval Mode and all related UAC policy settings are disabled. Note: If this policy setting is disabled, the Security Center notifies you that the overall security of the operating system has been reduced.

  - *Yes* - Admin Approval Mode is enabled. This policy must be enabled and the related UAC policy settings must be set appropriately to allow the built-in Administrator account and all other users who are members of the Administrators group to run in Admin Approval Mode.

  [Learn more](/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions#localpoliciessecurityoptions-useraccountcontrol-useadminapprovalmode)

Baseline default: *Yes*

- **Prevent anonymous enumeration of SAM accounts**:  
  This security setting determines what additional permissions are granted for anonymous connections to the computer. Windows allows anonymous users to do certain activities, such as enumerating the names of domain accounts and network shares. This is convenient, for example, when an administrator wants to grant access to users in a trusted domain that doesn't maintain a reciprocal trust. This security option allows additional restrictions to be placed on anonymous connections as follows:

  - *Yes* - Don't allow enumeration of SAM accounts. This option replaces Everyone with Authenticated Users in the security permissions for resources.

  - *Not configured* - No additional restrictions. Rely on default permissions.

  [Learn more](/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions#localpoliciessecurityoptions-networkaccess-donotallowanonymousenumerationofsamaccounts)

Baseline default: Yes

- **Allow remote calls to security accounts manager**:  
  This policy setting allows you to restrict remote rpc connections to SAM. If not selected, the default security descriptor is used.  
  [Learn more](/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions#localpoliciessecurityoptions-networkaccess-restrictclientsallowedtomakeremotecallstosam)

Baseline default: *O:BAG:BAD:(A;;RC;;;BA)*

- **Use admin approval mode**:  
  This policy setting controls the behavior of Admin Approval Mode for the built-in Administrator account. The options are:

  - *Yes* - The built-in Administrator account uses Admin Approval Mode. By default, any operation that requires elevation of privilege will prompt the user to approve the operation.

  - *Not Configured* - The built-in Administrator account runs all applications with full administrative privilege.

  [Learn more](/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions#localpoliciessecurityoptions-useraccountcontrol-runalladministratorsinadminapprovalmode)

Baseline default: *Yes*
  
- **Only allow UI access applications for secure locations**:  
  This policy setting controls whether User Interface Accessibility (UIAccess or UIA) programs can automatically disable the secure desktop for elevation prompts used by a standard user.

  - *Yes* - UIA programs, including Windows Remote Assistance, automatically disable the secure desktop for elevation prompts. If you don't disable the "User Account Control: Switch to the secure desktop when prompting for elevation" policy setting, the prompts appear on the interactive user's desktop instead of the secure desktop.

  - *Not Configured*: - The secure desktop can be disabled only by the user of the interactive desktop or by disabling the "User Account Control: Switch to the secure desktop when prompting for elevation" policy setting.

  [Learn more](/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions#localpoliciessecurityoptions-useraccountcontrol-onlyelevateuiaccessapplicationsthatareinstalledinsecurelocations)

Baseline default: *Yes*

- **Detect application installations and prompt for elevation**:  
  This policy setting controls the behavior of application installation detection for the computer. The options are:

  - *Enabled* - When an application installation package is detected that requires elevation of privilege, the user is prompted to enter an administrative user name and password. If the user enters valid credentials, the operation continues with the applicable privilege.

  - *Disabled* - Application installation packages aren't detected and prompted for elevation. Enterprises that are running standard user desktops and use delegated installation technologies such as Group Policy Software Installation or Systems Management Server (SMS) should disable this policy setting. In this case, installer detection is unnecessary.

  [Learn more](/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions#localpoliciessecurityoptions-useraccountcontrol-detectapplicationinstallationsandpromptforelevation)

Baseline default: *Yes*

- **Prevent storing LAN manager hash value on next password change**:  
  This security setting determines if, at the next password change, the LAN Manager (LM) hash value for the new password is stored. The LM hash is relatively weak and prone to attack, as compared with the cryptographically stronger Windows NT hash. Because the LM hash is stored on the local computer in the security database, the passwords can be compromised if the security database is attacked.  
  [Learn more](/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions#localpoliciessecurityoptions-networksecurity-donotstorelanmanagerhashvalueonnextpasswordchange)

Baseline default: *Yes*

- **Virtualize file and registry write failures to per user locations**:  
  This policy setting controls whether application write failures are redirected to defined registry and file system locations. This policy setting mitigates applications that run as administrator and write run-time application data to *%ProgramFiles%*, *%Windir%*, *%Windir%\system32*, or *HKLM\Software*.  
  [Learn more](/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions#localpoliciessecurityoptions-useraccountcontrol-virtualizefileandregistrywritefailurestoperuserlocations)

Baseline default: *Yes*

## Microsoft Defender

For more information, see [Policy CSP - Defender](/windows/client-management/mdm/policy-csp-defender) in the Windows documentation.

- **Block Adobe Reader from creating child processes**:  
This rule prevents attacks by blocking Adobe Reader from creating additional processes. Through social engineering or exploits, malware can download and launch additional payloads and break out of Adobe Reader. By blocking child processes from being generated by Adobe Reader, malware attempting to use it as a vector are prevented from spreading.
[Learn more](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction)

Baseline default: *Enable*

- **Block Office communication apps launch in a child process**:  
  [Protect devices from exploits](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction)

Baseline default: *Enable*

- **Enter how often (0-24 hours) to check for security intelligence updates**  
  CSP: [Defender/SignatureUpdateInterval](/windows/client-management/mdm/policy-csp-defender)
  
  Specify how often to check for new signatures. A value of 1 is one hour, 2 is two hours, and so on.

Baseline default: *4*

- **Scan type**  
  CSP: [Defender/ScanParameter](/windows/client-management/mdm/policy-csp-defender#defender-scanparameter)

  Specify the scan type to use for a schedule scan

Baseline default: *Quick scan*

- **Defender schedule scan day**:  
  Defender schedule scan day.

Baseline default: *Everyday*
















::: zone pivot="mdm-sept-2020,mdm-december-2020,november-2021"


::: zone-end
::: zone pivot="mdm-december-2020,november-2021"

- **Defender scan start time**:  
  Defender schedule scan time.

Baseline default: Not configured

::: zone-end
::: zone pivot="mdm-sept-2020,mdm-december-2020,november-2021"

- **Cloud-delivered protection level**:  
  CSP: [Defender/CloudBlockLevel](/windows/client-management/mdm/policy-csp-defender#defender-cloudblocklevel)

  Specify the level of cloud-delivered protection. Not Configured uses the default Microsoft Defender Antivirus blocking level and provides strong detection without increasing the risk of detecting legitimate files. High applies a strong level of detection. High + uses the High level and applies addition protection measures (may impact client performance). Zero tolerance blocks all unknown executables. While unlikely, setting to High may cause some legitimate files to be detected. 

Baseline default: Not Configured

- **Scan network files**:  
  CSP: [Defender/AllowScanningNetworkFiles](/windows/client-management/mdm/policy-csp-defender#defender-allowscanningnetworkfiles)

  When set to Yes, Microsoft Defender will scan network files. When set to Not configured, the client will return to default with is disabling scanning of network files.

Baseline default: Yes

- **Turn on real-time protection**  
  CSP: [Defender/AllowRealtimeMonitoring](/windows/client-management/mdm/policy-csp-defender#defender-allowrealtimemonitoring)

  When this setting is set to Yes, real-time monitoring will be enforced and the user can't disable it. When set to Not configured, the setting is returned to client default, which is on, but the user can change it. To disable real-time monitoring, use a custom URI.

Baseline default: Yes  

::: zone-end
::: zone pivot="november-2021"

- **Scan scripts that are used in Microsoft browsers**  
  CSP [Defender/AllowScriptScanning](/windows/client-management/mdm/policy-csp-defender#defender-allowscriptscanning)

  When this setting is set to Yes, the Windows Defender Script Scanning functionality will be enforced and the user cannot turn them off. When set to Not configured, the setting is returned to client default which is to enable script scanning, however the user can turn it off.

Baseline default: Yes

::: zone-end
::: zone pivot="mdm-sept-2020,mdm-december-2020,november-2021"

- **Scan archive files**:  
  CSP: [Defender/AllowArchiveScanning](/windows/client-management/mdm/policy-csp-defender#defender-allowarchivescanning)
  
  When set to Yes, archive files such as ZIP or CAB file scanning will be enforced. When set to Not configured, the setting will be returned back to client default, which is to scan archived files, however the user may disable this.

Baseline default: Yes

- **Turn on behavior monitoring**:  
  CSP: [Defender/AllowBehaviorMonitoring](/windows/client-management/mdm/policy-csp-defender#defender-allowbehaviormonitoring)

  When this setting is set to Yes, behavior monitoring will be enforced and the user can't disable it. When set to Not configured, the setting is returned to client default, which is on, but the user can change it. To disable real-time monitoring, use a custom URI.

Baseline default: Yes

- **Turn on cloud-delivered protection**:  
  CSP: [Defender/AllowCloudProtection](/windows/client-management/mdm/policy-csp-defender#defender-allowcloudprotection)

  When set to Yes, Defender will send information to Microsoft about any problems it finds. If set to Not configured, the client will return to default, which enables the feature but allows the user to disable it.

Baseline default: Yes

- **Scan incoming mail messages**:  
  CSP: [Defender/AllowEmailScanning](/windows/client-management/mdm/policy-csp-defender#defender-allowemailscanning)

  When set to Yes, e-mail mailbox and mail files such as PST, DBX, MNX, MIME and BINHEX will be scanned. When Not configured, the setting will return to client default of e-mail files not being scanned.

Baseline default: Yes

- **Scan removable drives during a full scan**:  
  CSP: [Defender/AllowFullScanRemovableDriveScanning](/windows/client-management/mdm/policy-csp-defender#defender-allowfullscanremovabledrivescanning)

  When set to Yes, during a full scan removable drives (for example, USB flash drives) will be scanned. When set to Not Configured, the setting will return to client default, which scans removable drives, however the user can disable this.
Baseline default: Yes  

- **Block Office applications from injecting code into other processes**:  
  [Protect devices from exploits](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction)

  When set to Yes, Office applications will be blocked from injecting code into other processes. When set to Audit only, Windows events will be raised instead of blocking. Setting to Not Configured will return the setting to Windows default, which is off. This Attack Surface Reduction (ASR) rule is controlled via the following GUID: 75668C1F-73B5-4CF0-BB93-3ECF5CB7CC84

Baseline default:  Block

- **Block Office applications from creating executable content**  
  [Protect devices from exploits](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction)

  When set to Yes, Office applications will not be allowed to create executable content. When set to Audit only, Windows events will be raised instead of blocking. Setting to Not Configured will return the setting to Windows default, which is off. This ASR rule is controlled via the following GUID: 3B576869-A4EC-4529-8536-B80A7769E899

Baseline default:  Block

- **Block all Office applications from creating child processes**  
  [Protect devices from exploits](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction)

  When set to Audit mode, Windows events will be raised instead of blocking. Setting to Not Configured will return the setting to Windows default, which is off. This ASR rule is controlled via the following GUID: D4F940AB-401B-4EFC-AADC-AD5F3C50688A

Baseline default:  Block

- **Block Win32 API calls from Office macro**:  
  [Protect devices from exploits](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction)

  When set to Yes, Office macro's will be blocked from using Win32 API calls. When set to Audit only, Windows events will be raised instead of blocking. Setting to Not Configured will return the setting to Windows default, which is off. This ASR rule is controlled via the following GUID: 92E97FA1-2EDF-4476-BDD6-9DD0B4DDDC7B
  
Baseline default: Block

- **Block execution of potentially obfuscated scripts (js/vbs/ps)**:  
  [Protect devices from exploits](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction)

  When set to yes, Defender will block execution of obfuscated scripts. When set to Audit only, Windows events will be raised instead of blocking. Setting to Not Configured will return the setting to Windows default, which is off. This ASR rule is controlled via the following GUID: 5BEB7EFE-FD9A-4556-801D-275E5FFC04CC
  
Baseline default: Block

- **Block JavaScript or VBScript from launching downloaded executable content**:  
  [Protect devices from exploits](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction)

  When set to Yes, Defender will block Javascript or VBScript files that have been downloaded from the Internet from being executed. When set to Audit only, Windows events will be raised instead of blocking. Setting to Not Configured will return the setting to Windows default, which is off. This attack surface reduction (ASR) rule is controlled via the following GUID: D3E037E1-3EB8-44C8-A917-57927947596D
  
Baseline default: Block

- **Block executable content download from email and webmail clients**:  
  [Block executable content download from email and webmail clients](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction)

  When set to Yes, executable content downloaded from email and webmail clients will be blocked. When set to Audit only, Windows events will be raised instead of blocking. Setting to Not Configured will return the setting to Windows default, which is off.

Baseline default: Block

- **Prevent credential stealing type**:  
  [Protect devices from exploits](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction)
  
  When set to Yes, attempts to steal credentials via lsass.exe will be blocked. When set to Audit only, Windows events will be raised instead of blocking. Setting to Not Configured will return the setting to Windows default, which is off. This ASR rule is controlled via the following GUID: 9e6c4e1f-7d60-472f-ba1a-a39ef669e4b2

Baseline default: Enable

- **Defender potentially unwanted app action**:  
  CSP: [Defender/PUAProtection](/windows/client-management/mdm/policy-csp-defender#defender-puaprotection)+

  The potentially unwanted application (PUA) protection feature in Microsoft Defender Antivirus can identify and block PUAs from downloading and installing on endpoints in your network. These applications aren't considered viruses, malware, or other types of threats, but might do actions on endpoints that adversely affect their performance or use. PUA can also refer to applications that are considered to have a poor reputation. Typical PUA behavior includes: Various types of software bundling Ad injection into web browsers Driver and registry optimizers that detect issues, request payment to fix the errors, but remain on the endpoint and make no changes or optimizations (also known as "rogue antivirus" programs). These applications can increase the risk of your network being infected with malware, cause malware infections to be harder to identify, and can waste IT resources in cleaning up the applications.

Baseline default: Block

- **Block untrusted and unsigned processes that run from USB**:  
  [Protect devices from exploits](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction)
  
  When set to Yes, untrusted/unsigned processes executing from a USB drive will be blocked. When set to Audit only, Windows events will be raised instead of blocking. Setting to Not Configured will return the setting to Windows default, which is off. This ASR rule is controlled via the following GUID: b2b3f03d-6a65-4f7b-a9c7-1c7ef74a9ba4

Baseline default: Block

- **Enable network protection**:  
  [Defender/EnableNetworkProtection](/windows/client-management/mdm/policy-csp-defender#defender-enablenetworkprotection)

  When set to Yes, network protection will be enabled for all users on the system. Network protection protects employees from accessing phishing scams, and malicious content on the Internet. This includes third-party browsers. Setting this to Audit only, users will not be blocked from dangerous domains however Windows events will be raised instead. Setting this to Not Configured will return the setting to Windows default, which is disabled.

Baseline default: Enable

- **Defender sample submission consent type**:  
  [Defender/SubmitSamplesConsent](/windows/client-management/mdm/policy-csp-defender#defender-submitsamplesconsent)

  Checks for the user consent level in Microsoft Defender to send data. If the required consent has already been granted, Microsoft Defender submits them. If not, and if the user has specified never to ask, the UI is launched to ask for user consent (when Defender/AllowCloudProtection is allowed) before sending data.

Baseline default: Send safe samples automatically

## MS Security Guide

For more information, see [Policy CSP - MSSecurityGuide](/windows/client-management/mdm/policy-csp-mssecurityguide) in the Windows documentation.

- **Apply UAC restrictions to local accounts on network logon**:  
  [Learn more](/windows/client-management/mdm/policy-csp-mssecurityguide#mssecurityguide-applyuacrestrictionstolocalaccountsonnetworklogon)

Baseline default: Enabled

- **SMB v1 client driver start configuration**:  
  [Learn more](/windows/client-management/mdm/policy-csp-mssecurityguide#mssecurityguide-configuresmbv1clientdriver)

Baseline default: Disabled driver

- **SMB v1 server**:  
  [Learn more](/windows/client-management/mdm/policy-csp-mssecurityguide#mssecurityguide-configuresmbv1server)

Baseline default: Disabled

- **Digest authentication**:  
  [Learn more](/windows/client-management/mdm/policy-csp-mssecurityguide#mssecurityguide-wdigestauthentication)

Baseline default: Disabled

- **Structured exception handling overwrite protection**:  
  [Learn more](/windows/client-management/mdm/policy-csp-mssecurityguide#mssecurityguide-enablestructuredexceptionhandlingoverwriteprotection)

Baseline default: Enabled

## MSS Legacy

For more information, see [Policy CSP - MSSLegacy](/windows/client-management/mdm/policy-csp-msslegacy) in the Windows documentation.

- **Network IP source routing protection level**:  
  [Learn more](/windows/client-management/mdm/policy-csp-msslegacy#msslegacy-ipsourceroutingprotectionlevel)

Baseline default: Highest protection  

- **Network ignore NetBIOS name release requests except from WINS servers**:  
  [Learn more](/windows/client-management/mdm/policy-csp-msslegacy#msslegacy-allowthecomputertoignorenetbiosnamereleaserequestsexceptfromwinsservers)

Baseline default: Enabled

- **Network IPv6 source routing protection level**:  
  [Learn more](/windows/client-management/mdm/policy-csp-msslegacy#msslegacy-ipv6sourceroutingprotectionlevel)

Baseline default: Highest protection

- **Network ICMP redirects override OSPF generated routes**:  
  [Learn more](/windows/client-management/mdm/policy-csp-msslegacy#msslegacy-allowicmpredirectstooverrideospfgeneratedroutes)

Baseline default: Disabled

## Power

For more information, see [Policy CSP - Power](/windows/client-management/mdm/policy-csp-power) in the Windows documentation.

- **Require password on wake while plugged in**:  
  This policy setting specifies if the user is prompted for a password when the system resumes from sleep. If you enable or don't configure this policy setting, the user is prompted for a password when the system resumes from sleep. If you disable this policy setting, the user isn't prompted for a password when the system resumes from sleep.  
  [Learn more](/windows/client-management/mdm/policy-csp-power#power-requirepasswordwhencomputerwakespluggedin)

Baseline default: Enabled

- **Standby states when sleeping while on battery**:  
  This policy setting manages if Windows can use standby states when putting the computer in a sleep state. If you enable or don't configure this policy setting, Windows uses standby states to put the computer in a sleep state. If you disable this policy setting, standby states (S1-S3) aren't allowed.  
  [Learn more](/windows/client-management/mdm/policy-csp-power#power-standbytimeoutonbattery)

Baseline default: Disabled

- **Standby states when sleeping while plugged in**:  
  This policy setting manages if Windows can use standby states when putting the computer in a sleep state. If you enable or don't configure this policy setting, Windows uses standby states to put the computer in a sleep state. If you disable this policy setting, standby states (S1-S3) aren't allowed.  
  [Learn more](/windows/client-management/mdm/policy-csp-power#power-standbytimeoutpluggedin)

Baseline default: Disabled

- **Require password on wake while on battery**:  
  This policy setting specifies if the user is prompted for a password when the system resumes from sleep. If you enable or don't configure this policy setting, the user is prompted for a password when the system resumes from sleep. If you disable this policy setting, the user isn't prompted for a password when the system resumes from sleep.  
  [Learn more](/windows/client-management/mdm/policy-csp-power#power-requirepasswordwhencomputerwakesonbattery)

Baseline default: Enabled

## Remote Assistance

For more information, see [Policy CSP - RemoteAssistance](/windows/client-management/mdm/policy-csp-remoteassistance#remoteassistance-solicitedremoteassistance) in the Windows documentation.

- **Remote Assistance solicited**:  
  This policy setting allows you to turn on or turn off Solicited (Ask for) Remote Assistance on this computer.
  
  - *If you enable this policy setting*, users on this computer can use email or file transfer to ask someone for help. Also, users can use instant messaging programs to allow connections to this computer, and you can configure additional Remote Assistance settings.

  - *If you disable this policy setting*, users on this computer can't use email or file transfer to ask someone for help. Also, users can't use instant messaging programs to allow connections to this computer.

  - *If you don't configure this policy setting*, users can turn on or turn off Solicited (Ask for) Remote Assistance themselves in System Properties in Control Panel. Users can also configure Remote Assistance settings.

  If you enable this policy setting, you have two ways to allow helpers to provide Remote Assistance: "Allow helpers to only view the computer" or "Allow helpers to remotely control the computer." The "Maximum ticket time" policy setting sets a limit on the amount of time that a Remote Assistance invitation created by using email or file transfer can remain open. The "Select the method for sending email invitations" setting specifies which email standard to use to send Remote Assistance invitations. Depending on your email program, you can use either the *Mailto* standard (the invitation recipient connects through an Internet link) or the SMAPI (Simple MAPI) standard (the invitation is attached to your email message). This policy setting isn't available in Windows Vista because SMAPI is the only method supported. If you enable this policy setting, you should also enable appropriate firewall exceptions to allow Remote Assistance communications.  
  [Learn more](/windows/client-management/mdm/policy-csp-remoteassistance#remoteassistance-solicitedremoteassistance)

Baseline default: Disable Remote Assistance

## Remote Desktop Services

For more information, see [Policy CSP - RemoteDesktopServices](/windows/client-management/mdm/policy-csp-remotedesktopservices) in the Windows documentation.

- **Block password saving**:  
  Controls whether passwords can be saved on this computer from Remote Desktop Connection. If you enable this setting the password saving checkbox in Remote Desktop Connection is disabled and users can't save passwords. When a user opens an RDP file using Remote Desktop Connection and saves their settings, any password that previously existed in the RDP file are deleted. If you disable this setting or leave it not configured, the user can save passwords using Remote Desktop Connection.  
  [Learn more](/windows/client-management/mdm/policy-csp-remotedesktopservices#remotedesktopservices-donotallowpasswordsaving)

 Baseline default: Enabled

- **Secure RPC communication**:  
  Specifies whether a Remote Desktop Session Host server requires secure RPC communication with all clients or allows unsecured communication. You can use this setting to strengthen the security of RPC communication with clients by allowing only authenticated and encrypted requests. If the status is set to Enabled, Remote Desktop Services accepts requests from RPC clients that support secure requests, and doesn't allow unsecured communication with untrusted clients. If the status is set to Disabled, Remote Desktop Services always requests security for all RPC traffic. However, unsecured communication is allowed for RPC clients that don't respond to the request. If the status is set to Not Configured, unsecured communication is allowed. Note: The RPC interface is used for administering and configuring Remote Desktop Services.  
  [Learn more](/windows/client-management/mdm/policy-csp-remotedesktopservices#remotedesktopservices-requiresecurerpccommunication)

Baseline default: Enabled

- **Block drive redirection**:  
  This policy setting specifies whether to prevent the mapping of client drives in a Remote Desktop Services session (drive redirection). By default, an RD Session Host server maps client drives automatically upon connection. Mapped drives appear in the session folder tree in File Explorer or Computer in the format *\<driveletter>* on *\<computername>*. You can use this policy setting to override this behavior. If you enable this policy setting, client drive redirection isn't allowed in Remote Desktop Services sessions, and Clipboard file copy redirection isn't allowed on computers running Windows Server 2003, Windows 8, and Windows XP. If you disable this policy setting, client drive redirection is always allowed. Also, Clipboard file copy redirection is always allowed if Clipboard redirection is allowed. If you don't configure this policy setting, client drive redirection and Clipboard file copy redirection aren't specified at the Group Policy level.  
  [Learn more](/windows/client-management/mdm/policy-csp-remotedesktopservices#remotedesktopservices-donotallowdriveredirection)

Baseline default: Enabled

- **Prompt for password upon connection**:  
  This policy setting specifies whether Remote Desktop Services always prompts the client for a password upon connection. You can use this setting to enforce a password prompt for users logging on to Remote Desktop Services, even if they already provided the password in the Remote Desktop Connection client. By default, Remote Desktop Services allows users to automatically log on by entering a password in the Remote Desktop Connection client. If you enable this policy setting, users can't automatically log on to Remote Desktop Services by supplying their passwords in the Remote Desktop Connection client. they're prompted for a password to log on. If you disable this policy setting, users can always log on to Remote Desktop Services automatically by supplying their passwords in the Remote Desktop Connection client. If you don't configure this policy setting, automatic logon isn't specified at the Group Policy level.  
  [Learn more](/windows/client-management/mdm/policy-csp-remotedesktopservices#remotedesktopservices-promptforpassworduponconnection)

Baseline default: Enabled

- **Remote desktop services client connection encryption level**:  
  Specifies whether to require the use of a specific encryption level to secure communications between client computers and RD Session Host servers during Remote Desktop Protocol (RDP) connections. This policy only applies when you're using native RDP encryption. However, native RDP encryption (as opposed to SSL encryption) isn't recommended. This policy doesn't apply to SSL encryption. If you enable this policy setting, all communications between clients and RD Session Host servers during remote connections must use the encryption method specified in this setting. By default, the encryption level is set to High. The following encryption methods are available:

  - *High* - The High setting encrypts data sent from the client to the server and from the server to the client by using strong 128-bit encryption. Use this encryption level in environments that contain only 128-bit clients (for example, clients that run Remote Desktop Connection). Clients that don't support this encryption level can't connect to RD Session Host servers.

  - *Client Compatible* - The Client Compatible setting encrypts data sent between the client and the server at the maximum key strength supported by the client. Use this encryption level in environments that include clients that don't support 128-bit encryption.

  - *Low* - The Low setting encrypts only data sent from the client to the server by using 56-bit encryption.  
  
  If you disable or don't configure this setting, the encryption level to be used for remote connections to RD Session Host servers isn't enforced through Group Policy. Important FIPS compliance can be configured through the System cryptography. Use FIPS-compliant algorithms for encryption, hashing, and signing settings in Group Policy (under Computer Configuration\Windows Settings\Security Settings\Local Policies\Security Options.) The FIPS-compliant setting encrypts and decrypts data sent from the client to the server and from the server to the client, with the Federal Information Processing Standard (FIPS) 140 encryption algorithms, by using Microsoft cryptographic modules. Use this encryption level when communications between clients and RD Session Host servers requires the highest level of encryption.  
  [Learn more](/windows/client-management/mdm/policy-csp-remotedesktopservices#remotedesktopservices-clientconnectionencryptionlevel)

Baseline default: High

## Remote Management

For more information, see [Policy CSP - RemoteManagement](/windows/client-management/mdm/policy-csp-remotemanagement) in the Windows documentation.

- **Block storing run as credentials**:  
  Client basic authentication.  
  [Learn more](/windows/client-management/mdm/policy-csp-remotemanagement#remotemanagement-disallowstoringofrunascredentials)

Baseline default: Enabled

- **Basic authentication**:  
  This policy setting allows you to manage whether the Windows Remote Management (WinRM) service accepts Basic authentication from a remote client. If you enable this policy setting, the WinRM service accepts Basic authentication from a remote client. If you disable or don't configure this policy setting, the WinRM service doesn't accept Basic authentication from a remote client.  
  [Learn more](/windows/client-management/mdm/policy-csp-remotemanagement#remotemanagement-allowbasicauthentication-service)

Baseline default: Disabled

- **Block client digest authentication**:  
  This policy setting allows you to manage whether the Windows Remote Management (WinRM) client uses Digest authentication. If you enable this policy setting, the WinRM client doesn't use Digest authentication. If you disable or don't configure this policy setting, the WinRM client uses Digest authentication.  
  [Learn more](/windows/client-management/mdm/policy-csp-remotemanagement#remotemanagement-disallownegotiateauthenticationclient)

Baseline default: Enabled

- **Unencrypted traffic**:  
  This policy setting allows you to manage whether the Windows Remote Management (WinRM) service sends and receives unencrypted messages over the network. If you enable this policy setting, the WinRM client sends and receives unencrypted messages over the network. If you disable or don't configure this policy setting, the WinRM client sends or receives only encrypted messages over the network.  
  [Learn more](/windows/client-management/mdm/policy-csp-remotemanagement#remotemanagement-allowunencryptedtraffic-service)

Baseline default: Disabled

- **Client unencrypted traffic**:  
  This policy setting allows you to manage whether the Windows Remote Management (WinRM) client sends and receives unencrypted messages over the network. If you enable this policy setting, the WinRM client sends and receives unencrypted messages over the network. If you disable or don't configure this policy setting, the WinRM client sends or receives only encrypted messages over the network.  
  [Learn more](/windows/client-management/mdm/policy-csp-remotemanagement#remotemanagement-allowunencryptedtraffic-client)

Baseline default: Disabled

- **Client basic authentication**:  
  This policy setting allows you to manage whether the Windows Remote Management (WinRM) client uses Basic authentication. If you enable this policy setting, the WinRM client uses Basic authentication. If WinRM is configured to use HTTP transport, the user name and password are sent over the network as clear text. If you disable or don't configure this policy setting, the WinRM client doesn't use Basic authentication.  
  [Learn more](/windows/client-management/mdm/policy-csp-remotemanagement#remotemanagement-allowbasicauthentication-client)

Baseline default: Disabled

## Remote Procedure Call

For more information, see [Policy CSP - RemoteProcedureCall](/windows/client-management/mdm/policy-csp-remoteprocedurecall) in the Windows documentation.

- **RPC unauthenticated client options**:  
  This policy setting controls how the RPC server runtime handles unauthenticated RPC clients connecting to RPC servers. This policy setting impacts all RPC applications. In a domain environment, use this policy setting with caution as it can impact a wide range of functionality including group policy processing itself. Reverting a change to this policy setting can require manual intervention on each affected machine. Don't apply this policy setting to a domain controller. If you disable this policy setting, the RPC server runtime uses the value of "Authenticated" on Windows Client, and the value of "None" on Windows Server versions that support this policy setting. If you don't configure this policy setting, it remains disabled. The RPC server runtime behaves as though it was enabled with the value of "Authenticated" used for Windows Client and the value of "None" used for Server SKUs that support this policy setting. If you enable this policy setting, it directs the RPC server runtime to restrict unauthenticated RPC clients connecting to RPC servers running on a machine. A client is considered an authenticated client if it uses a named pipe to communicate with the server or if it uses RPC Security. RPC Interfaces that have specifically requested to be accessible by unauthenticated clients may be exempt from this restriction, depending on the selected value for this policy setting.

  - *None* allows all RPC clients to connect to RPC Servers running on the machine on which the policy setting is applied.

  - *Authenticated* allows only authenticated RPC Clients (per the definition above) to connect to RPC Servers running on the machine on which the policy setting is applied. Exemptions are granted to interfaces that have requested them.

  - *Authenticated without exceptions* allows only authenticated RPC Clients (per the definition above) to connect to RPC Servers running on the machine on which the policy setting is applied. No exceptions are allowed. Note: This policy setting won't be applied until the system is rebooted.

  [Learn more](/windows/client-management/mdm/policy-csp-remoteprocedurecall#remoteprocedurecall-rpcendpointmapperclientauthentication)

Baseline default: Authenticated

## Search

For more information, see [Policy CSP - Search](/windows/client-management/mdm/policy-csp-search) in the Windows documentation.

- **Disable indexing encrypted items**:  
  Allows or disallows the indexing of items. This switch is for the Windows Search Indexer, which controls whether it will index items that are encrypted, such as the Windows Information Protection (WIP) protected files. When the policy is enabled, WIP protected items are indexed and the metadata about them are stored in an unencrypted location. The metadata includes things like file path and date modified. When the policy is disabled, the WIP protected items aren't indexed and don't show up in the results in Cortana or file explorer. There may also be a performance impact on photos and Groove apps if there are many WIP protected media files on the device.  
  [Learn more]( https://go.microsoft.com/fwlink/?linkid=2067303)

Baseline default: Yes

## Smart Screen

For more information, see [Policy CSP - SmartScreen](/windows/client-management/mdm/policy-csp-smartscreen) in the Windows documentation.

- **Turn on Windows SmartScreen**  
  CSP: [SmartScreen/EnableSmartScreenInShell](/windows/client-management/mdm/policy-csp-smartscreen#smartscreen-enablesmartscreeninshell)

  Setting this to Yes will enforce the use of SmartScreen for all users. Setting this to Not configured will return the setting to Windows default, which is to enable SmartScreen, however users may change this setting. To disable SmartScreen, use a custom URI.

Baseline default: Yes

- **Block users from ignoring SmartScreen warnings**  
  CSP: [SmartScreen/PreventOverrideForFilesInShell](/windows/client-management/mdm/policy-csp-smartscreen#smartscreen-preventoverrideforfilesinshell)

  When set to Yes, SmartScreen is enabled and users can't bypass warnings for files or malicious apps. When set to Not configured, users can ignore SmartScreen warnings for files and malicious apps.  

  This setting requires the 'Turn on Windows SmartScreen' setting be set to Yes.

Baseline default: Yes

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

Baseline default: Good unknown and bad critical

## Wi-Fi

For more information, see [Policy CSP - Wifi](/windows/client-management/mdm/policy-csp-wifi) in the Windows documentation.

- **Block Automatically connecting to Wi-Fi hotspots**:  
  Allow or disallow the device to automatically connect to Wi-Fi hotspots.  
  [Learn more](/windows/client-management/mdm/policy-csp-wifi#wifi-allowautoconnecttowifisensehotspots)

Baseline default: Yes

- **Block Internet sharing**:  
  Specifies whether internet sharing is possible on the device.  
  [Learn more](/windows/client-management/mdm/policy-csp-wifi#wifi-allowinternetsharing)

Baseline default: Yes

## Windows Connection Manager

For more information, see [Policy CSP - WindowsConnectionManager](/windows/client-management/mdm/policy-csp-windowsconnectionmanager) in the Windows documentation.

- **Block connection to non-domain networks**:  
  This policy setting prevents computers from connecting to both a domain-based network and a non-domain based network at the same time. If this policy setting is enabled, the computer responds to automatic and manual network connection attempts based on the following circumstances:

  - *Automatic connection attempts* - When the computer is already connected to a domain-based network, all automatic connection attempts to non-domain networks are blocked. When the computer is already connected to a non-domain based network, automatic connection attempts to domain-based networks are blocked.

  - *Manual connection attempts* - When the computer is already connected to either a non-domain based network or a domain-based network over media other than Ethernet, and a user attempts to create a manual connection to an additional network in violation of this policy setting, the existing network connection disconnects, and the manual connection is allowed. When the computer is already connected to either a non-domain based network or a domain-based network over Ethernet, and a user attempts to create a manual connection to an additional network in violation of this policy setting, the existing Ethernet connection is maintained and the manual connection attempt is blocked.

  If this policy setting isn't configured or is disabled, computers are allowed to connect simultaneously to both domain and non-domain networks.  
  [Learn more](/windows/client-management/mdm/policy-csp-windowsconnectionmanager)

Baseline default: Enabled

## Windows Ink Workspace

For more information, see [Policy CSP - WindowsInkWorkspace](/windows/client-management/mdm/policy-csp-windowsinkworkspace) in the Windows documentation.

- **Ink Workspace**:  
  Specifies whether to allow the user to access the ink workspace.

  - *Disabled* - access to ink workspace is disabled. The feature is turned off.

  - *Enabled* - The Ink Workspace feature is turned on, but the user can't access it above the lock screen.

  - *Not Configured* - The Ink Workspace feature is turned on, and the user can use it above the lock screen.

  [Learn more](/windows/client-management/mdm/policy-csp-windowsinkworkspace#windowsinkworkspace-allowwindowsinkworkspace)

Baseline default: Enabled

## Windows PowerShell

For more information, see [Policy CSP - WindowsPowerShell](/windows/client-management/mdm/policy-csp-windowspowershell) in the Windows documentation.

- **PowerShell script block logging**:  
  This policy setting enables logging of all PowerShell script input to the Microsoft-Windows-PowerShell/Operational event log. If you enable this policy setting, Windows PowerShell will log the processing of commands, script blocks, functions, and scripts - whether invoked interactively, or through automation. If you disable this policy setting, logging of PowerShell script input is disabled. If you enable the Script Block Invocation Logging, PowerShell additionally logs events when invocation of a command, script block, function, or script starts or stops. Enabling Invocation Logging generates a high volume of event logs. Note: This policy setting exists under both Computer Configuration and User Configuration in the Group Policy Editor. The Computer Configuration policy setting takes precedence over the User Configuration policy setting.  
  [Learn more](/windows/client-management/mdm/policy-csp-windowspowershell#windowspowershell-turnonpowershellscriptblocklogging)

Baseline default: Enabled

::: zone-end

## Next steps

- [Learn about security baselines](security-baselines.md)
- [Avoid conflicts](security-baselines.md#avoid-conflicts)
- [Troubleshoot policies and profiles in Intune](/troubleshoot/mem/intune/troubleshoot-policies-in-microsoft-intune)
