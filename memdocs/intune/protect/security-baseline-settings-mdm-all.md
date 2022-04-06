---
# required metadata

title: Intune security baselines settings for Windows 10/11 MDM
titleSuffix: Microsoft Intune
description: Review the defaults and available settings for the different versions of the Windows MDM security baseline that you can manage with Microsoft Intune.
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/06/2022
ms.topic: conceptual
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


# Security baseline settings Windows 10 and later with Intune

View the security baseline settings that Microsoft Intune supports for devices that run Windows 10 and Windows 11. The default values for settings in this baseline represent the recommended configuration for applicable devices. Defaults for one baseline might not match defaults from other security baselines, or from other versions of this baseline.

- To learn about using security baselines with Intune and how to upgrade the baseline version in your security baseline profiles, see [Use security baselines](security-baselines.md).
- The most recent baseline version is **Security Baseline for Windows 10 and later for November 2021**

::: zone pivot="november-2021"

**Security Baseline for Windows 10 and later for November 2021**  

::: zone-end
::: zone pivot="mdm-december-2020"

**Security Baseline for Windows 10 and later for December 2020**  

::: zone-end
::: zone pivot="mdm-sept-2020"

**Security Baseline for Windows 10 and later for August 2020**  

::: zone-end
::: zone pivot="mdm-sept-2020,mdm-december-2020,november-2021"

This version of the security baseline replaces previous versions. Profiles that were created prior to the availability of this baseline version:

- Are now read-only. You can continue to use those profiles, but can't edit them to change their configuration.
- Can be updated to the latest version. After you update to the current baseline version, you can edit the profile to modify settings.

To understand what's changed with this version of the baseline from previous versions, use the [Compare baselines](../protect/security-baselines.md#compare-baseline-versions) action that's available when viewing the *Versions* pane for this baseline. Be sure to select the version of the baseline that you want to view.

To update a security baseline profile to the latest version of that baseline, see [Change the baseline version for a profile](../protect/security-baselines-configure.md#change-the-baseline-version-for-a-profile).

::: zone-end
::: zone pivot="mdm-sept-2020,mdm-december-2020,november-2021"

## Above Lock

- **Voice activate apps from locked screen**:  
  Specifies whether or not the user can interact with a voice assistant using speech while the system is locked. If you enable or don’t configure this setting, the user can interact with voice assistant using speech while the system is locked. If you disable this setting, the system will need to be unlocked for the user to interact using speech.  
  [Learn More](/windows/client-management/mdm/policy-csp-privacy)

- **Block display of toast notifications**:  
  Block toast notifications above the device lock screen.  
  [Learn More](/windows/client-management/mdm/policy-csp-abovelock#abovelock-allowtoasts)

## App Runtime

For more information, see [Policy CSP - AppRuntime](/windows/client-management/mdm/policy-csp-appruntime) in the Windows documentation.

- **Microsoft accounts optional for Windows Store apps**:  
  This policy setting lets you control whether Microsoft accounts are optional for Windows Store apps that require an account to sign in. This policy only affects Windows Store apps that support it. If you enable this policy setting, Windows Store apps that typically require a Microsoft account to sign in will allow users to sign in with an enterprise account instead. If you disable or don't configure this policy setting, users must sign in with a Microsoft account.  
  [Learn more](/windows/client-management/mdm/policy-csp-appruntime#appruntime-allowmicrosoftaccountstobeoptional)
  
  **Default**: Enabled

## Application Management

For more information, see [Policy CSP - ApplicationManagement](/windows/client-management/mdm/policy-csp-applicationmanagement) in the Windows documentation.
 
- **Block app installations with elevated privileges**:
  This policy setting directs Windows Installer to use elevated permissions when it installs any program on the system. If you enable this policy setting, privileges are extended to all programs. This enables users to install programs that require access to directories that the user might not have permission to view or change, including directories on highly restricted computers.  
  [Learn more](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-msialwaysinstallwithelevatedprivileges)

  **Default**: Yes.

- **Block user control over installations**:  
  This policy prevents users from changing the installation options typically reserved for system administrators, such as entering the directory to install the files. When set to Not configured (default), Intune doesn't change or update this setting. By default, Windows Installer might prevent users from changing these installation options, and some of the Windows Installer security features are bypassed.  
  [Learn more](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-msiallowusercontroloverinstall)

  **Default**: Yes

- **Block game DVR (desktop only)**:  
  Configures whether recording and broadcasting of games is allowed.  
  [Learn more](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-allowgamedvr)

  **Default**: Yes

## Audit

- **Account Logon Audit Credential Validation (Device)**:  
  This policy setting allows you to audit events generated by validation tests on user account logon credentials. Events in this subcategory occur only on the computer that is authoritative for those credentials. For domain accounts, the domain controller is authoritative. For local accounts, the local computer is authoritative.

  **Default**: Success and Failure

- **Account Logon Audit Kerberos Authentication Service (Device)**:  
  This policy setting allows you to audit events generated by Kerberos authentication ticket-granting ticket (TGT) requests. If you configure this policy setting, an audit event is generated after a Kerberos authentication TGT request. Success audits record successful requests and Failure audits record unsuccessful requests. If you don't configure this policy setting, no audit event is generated after a Kerberos authentication TGT request.

  **Default**: None

- **Account Logon Logoff Audit Account Lockout (Device)**:  

  **Default**: Failure

- **Account Logon Logoff Audit Group Membership (Device)**:  
  This policy allows you to audit the group membership information in the user's logon token. Events in this subcategory are generated on the computer on which a logon session is created. For an interactive logon, the security audit event is generated on the computer that the user logged on to. For a network logon, such as accessing a shared folder on the network, the security audit event is generated on the computer hosting the resource. When this setting is configured, one or more security audit events are generated for each successful logon. You must also enable the Audit Logon setting under Advanced Audit Policy Configuration\System Audit Policies\Logon/Logoff. Multiple events are generated if the group membership information can't fit in a single security audit event.

  **Default**: Success

- **Account Logon Logoff Audit Logon (Device)**:  
  This policy setting allows you to audit events generated by user account logon attempts on the computer. Events in this subcategory are related to the creation of logon sessions and occur on the computer that was accessed. For an interactive logon, the security audit event is generated on the computer that the user account logged on to. For a network logon, such as accessing a shared folder on the network, the security audit event is generated on the computer hosting the resource. The following events are included: Successful logon attempts. Failed logon attempts. Logon attempts using explicit credentials. This event is generated when a process attempts to log on an account by explicitly specifying that accounts credentials. This most commonly occurs in batch logon configurations, such as scheduled tasks or when using the RUNAS command. Security identifiers (SIDs) were filtered and not allowed to log on.

  **Default**: Success and Failure

- **Audit Other Logon Logoff Events (Device)**:  
  This policy setting allows you to audit other events related to logon/logoff, that aren't covered in the *Logon/Logoff* policy setting such as the following: Terminal Services session disconnections. New Terminal Services sessions. Locking and unlocking a workstation. Invoking a screen saver. Dismissal of a screen saver. Detection of a Kerberos replay attack, in which a Kerberos request was received twice with identical information. This condition could be caused by network misconfiguration. Access to a wireless network granted to a user or computer account. Access to a wired 802.1x network granted to a user or computer account.

  **Default**: Success and Failure

- **Audit Special Logon (Device)**:  
  This policy setting allows you to audit events generated by special logons such as the following: The use of a special logon, which is a logon that has administrator-equivalent privileges and can be used to elevate a process to a higher level. A logon by a member of a Special Group. Special Groups enable you to audit events generated when a member of a certain group has logged on to your network. You can configure a list of group security identifiers (SIDs) in the registry. If any of those SIDs are added to a token during logon and the subcategory is enabled, an event is logged. For more information about this feature, see article 947223 in the Microsoft Knowledge Base (https://go.microsoft.com/fwlink/?LinkId=121697).

  **Default**: Success

- **Audit Security Group Management (Device)**:  
  This policy setting allows you to audit events generated by changes to security groups such as the following: Security group is created, changed, or deleted. Member is added or removed from a security group. Group type is changed. If you configure this policy setting, an audit event is generated when an attempt to change a security group is made. Success audits record successful attempts and Failure audits record unsuccessful attempts. If you don't configure this policy setting, no audit event is generated when a security group changes.

  **Default**: Success

- **Audit User Account Management (Device)**:  
  This policy setting allows you to audit changes to user accounts. Events include the following: A user account is created, changed, deleted; renamed, disabled, enabled, locked out, or unlocked. A user account???s password is set or changed. A security identifier (SID) is added to the SID History of a user account. The Directory Services Restore Mode password is configured. Permissions on administrative user accounts are changed. Credential Manager credentials are backed up or restored. If you configure this policy setting, an audit event is generated when an attempt to change a user account is made. Success audits record successful attempts and Failure audits record unsuccessful attempts. If you don't configure this policy setting, no audit event is generated when a user account changes.

  **Default**: Success and Failure

- **Detailed Tracking Audit PNP Activity (Device)**:  
  This policy setting allows you to audit when plug and play detects an external device. If you configure this policy setting, an audit event is generated whenever plug and play detects an external device. Only Success audits are recorded for this category. If you don't configure this policy setting, no audit event is generated when an external device is detected by plug and play.

  **Default**: Success

- **Detailed Tracking Audit Process Creation (Device)**:  
  This policy setting allows you to audit events generated when a process is created or starts. The name of the application or user that created the process is also audited. If you configure this policy setting, an audit event is generated when a process is created. Success audits record successful attempts and Failure audits record unsuccessful attempts. If you don't configure this policy setting, no audit event is generated when a process is created.

  **Default**: Success

- **Object Access Audit Detailed File Share (Device)**:  
  This policy setting allows you to audit attempts to access files and folders on a shared folder. The Detailed File Share setting logs an event every time a file or folder is accessed, whereas the File Share setting only records one event for any connection established between a client and file share. Detailed File Share audit events include detailed information about the permissions or other criteria used to grant or deny access. If you configure this policy setting, an audit event is generated when an attempt is made to access a file or folder on a share. The administrator can specify whether to audit only successes, only failures, or both successes and failures. Note: There are no system access control lists (SACLs) for shared folders. If this policy setting is enabled, access to all shared files and folders on the system is audited.

  **Default**: Failure

- **Audit File Share Access (Device)**:  
  This policy setting allows you to audit attempts to access a shared folder. If you configure this policy setting, an audit event is generated when an attempt is made to access a shared folder. If this policy setting is defined, the administrator can specify whether to audit only successes, only failures, or both successes and failures. Note: There are no system access control lists (SACLs) for shared folders. If this policy setting is enabled, access to all shared folders on the system is audited.

  **Default**: Success and Failure

- **Object Access Audit Other Object Access Events (Device)**:  
  This policy setting allows you to audit events generated by the management of task scheduler jobs or COM+ objects. For scheduler jobs, the following are audited: Job created. Job deleted. Job enabled. Job disabled. Job updated. For COM+ objects, the following are audited: Catalog object added. Catalog object updated. Catalog object deleted.

  **Default**: Success and Failure

- **Object Access Audit Removable Storage (Device)**:  
  This policy setting allows you to audit user attempts to access file system objects on a removable storage device. A security audit event is generated only for all objects for all types of access requested. If you configure this policy setting, an audit event is generated each time an account accesses a file system object on a removable storage. Success audits record successful attempts and Failure audits record unsuccessful attempts. If you don't configure this policy setting, no audit event is generated when an account accesses a file system object on a removable storage.

  **Default**: Success and Failure

- **Audit Authentication Policy Change (Device)**:  
  This policy setting allows you to audit events generated by changes to the authentication policy such as the following: Creation of forest and domain trusts. Modification of forest and domain trusts. Removal of forest and domain trusts. Changes to Kerberos policy under Computer Configuration\Windows Settings\Security Settings\Account Policies\Kerberos Policy. Granting of any of the following user rights to a user or group: Access This Computer From the Network. Allow Logon Locally. Allow Logon Through Terminal Services. Logon as a Batch Job. Logon a Service. Namespace collision. For example, when a new trust has the same name as an existing namespace name. If you configure this policy setting, an audit event is generated when an attempt to change the authentication policy is made. Success audits record successful attempts and Failure audits record unsuccessful attempts. If you don't configure this policy setting, no audit event is generated when the authentication policy is changed. Note: The security audit event is logged when the group policy is applied. It doesn't occur at the time when the settings are modified.

  **Default**: Success

- **Policy Change Audit MPSSVC Rule Level Policy Change (Device)**:  
  This policy setting allows you to audit events generated by changes in policy rules used by the Microsoft Protection Service (MPSSVC). This service is used by Windows Firewall. Events include the following: Reporting of active policies when Windows Firewall service starts. Changes to Windows Firewall rules. Changes to Windows Firewall exception list. Changes to Windows Firewall settings. Rules ignored or not applied by Windows Firewall Service. Changes to Windows Firewall Group Policy settings. If you configure this policy setting, an audit event is generated by attempts to change policy rules used by the MPSSVC. Success audits record successful attempts and Failure audits record unsuccessful attempts. If you don't configure this policy setting, no audit event is generated by changes in policy rules used by the MPSSVC.

  **Default**: Success and Failure

- **Policy Change Audit Other Policy Change Events (Device)**:  
  This policy setting allows you to audit events generated by other security policy changes that aren't audited in the policy change category, such as the following: Trusted Platform Module (TPM) configuration changes. Kernel-mode cryptographic self tests. Cryptographic provider operations. Cryptographic context operations or modifications. Applied Central Access Policies (CAPs) changes. Boot Configuration Data (BCD) modifications.

  **Default**: Failure

- **Audit Changes to Audit Policy (Device)**:  
  This policy setting allows you to audit changes in the security audit policy settings such as the following: Settings permissions and audit settings on the Audit Policy object. Changes to the system audit policy. Registration of security event sources. De-registration of security event sources. Changes to the per-user audit settings. Changes to the value of CrashOnAuditFail. Changes to the system access control list on a file system or registry object. Changes to the Special Groups list. Note: System access control list (SACL) change auditing is done when a SACL for an object changes and the policy change category is enabled. Discretionary access control list (DACL) and ownership changes are audited when object access auditing is enabled and the object's SACL is configured for auditing of DACL/Owner change.

  **Default**: Success

- **Privilege Use Audit Sensitive Privilege Use (Device)**:  
  This policy setting allows you to audit events generated when sensitive privileges (user rights) are used such as the following: A privileged service is called. One of the following privileges are called: Act as part of the operating system. Back up files and directories. Create a token object. Debug programs. Enable computer and user accounts to be trusted for delegation. Generate security audits. Impersonate a client after authentication. Load and unload device drivers. Manage auditing and security log. Modify firmware environment values. Replace a process-level token. Restore files and directories. Take ownership of files or other objects. If you configure this policy setting, an audit event is generated when sensitive privilege requests are made. Success audits record successful requests and Failure audits record unsuccessful requests. If you don't configure this policy setting, no audit event is generated when sensitive privilege requests are made.

  **Default**: Success and Failure

- **System Audit Other System Events (Device)**:  
  This policy setting allows you to audit any of the following events: Startup and shutdown of the Windows Firewall service and driver. Security policy processing by the Windows Firewall Service. Cryptography key file and migration operations.

  **Default**: Success and Failure

- **System Audit Security State Change (Device)**:  
  This policy setting allows you to audit any of the following events: Startup and shutdown of the Windows Firewall service and driver. Security policy processing by the Windows Firewall Service. Cryptography key file and migration operations.

  **Default**: Success

- **Audit Security System Extension (Device)**:  
  This policy setting allows you to audit events related to security system extensions or services such as the following: A security system extension, such as an authentication, notification, or security package is loaded and is registered with the Local Security Authority (LSA). It is used to authenticate logon attempts, submit logon requests, and any account or password changes. Examples of security system extensions are Kerberos and NTLM. A service is installed and registered with the Service Control Manager. The audit log contains information about the service name, binary, type, start type, and service account. If you configure this policy setting, an audit event is generated when an attempt is made to load a security system extension. Success audits record successful attempts and Failure audits record unsuccessful attempts. If you don't configure this policy setting, no audit event is generated when an attempt is made to load a security system extension.

  **Default**: Success

- **System Audit System Integrity (Device)**:  
  This policy setting allows you to audit events that violate the integrity of the security subsystem, such as the following: Events that could not be written to the event log because of a problem with the auditing system. A process that uses a local procedure call (LPC) port that isn't valid in an attempt to impersonate a client by replying, reading, or writing to or from a client address space. The detection of a Remote Procedure Call (RPC) that compromises system integrity. The detection of a hash value of an executable file that isn't valid as determined by Code Integrity. Cryptographic operations that compromise system integrity.

  **Default**: Success and Failure

## Auto Play

For more information, see [Policy CSP - Autoplay](/windows/client-management/mdm/policy-csp-autoplay) in the Windows documentation.

- **Auto play default auto run behavior**:  
  This setting affects the default behavior for Autorun commands. Autorun commands are stored in autorun.inf files and can launch installation programs or other routines. When *Enabled*, Administrators can change the default autorun behavior on a device that runs Windows Vista or later. Behavior can be set to: a) completely disable autorun commands, or b) revert back to pre-Windows Vista behavior of automatically executing the autorun command. When set to *Disabled* or *Not Configured*, devices that run Windows Vista or later prompt the user as to whether an autorun command should run.  
  [Learn more](/windows/client-management/mdm/policy-csp-autoplay#autoplay-setdefaultautorunbehavior)

  **Default**: Do not execute

- **Auto play mode**:  
  This policy setting allows you to turn off the Autoplay feature. Autoplay begins reading from a drive as soon as you insert media in the drive. As a result, the setup file of programs and the music on audio media start immediately. With Windows XP SP2 and earlier, Autoplay is disabled by default on removable drives, such as the floppy disk drive (but not the CD-ROM drive), and on network drives. Starting with Windows XP SP2, Autoplay is enabled for removable drives as well, including Zip drives and some USB mass storage devices. If you enable this policy setting, Autoplay is disabled on CD-ROM and removable media drives, or disabled on all drives. This policy setting disables Autoplay on additional types of drives. You can't use this setting to enable Autoplay on drives on which it's disabled by default. If you disable or don't configure this policy setting, AutoPlay is enabled. Note: This policy setting appears in both the Computer Configuration and User Configuration folders. If the policy settings conflict, the policy setting in Computer Configuration takes precedence over the policy setting in User Configuration.  
  [Learn more](/windows/client-management/mdm/policy-csp-autoplay#autoplay-turnoffautoplay)

  **Default**: Disabled

- **Block auto play for non-volume devices**:  
  This policy setting disallows AutoPlay for MTP devices like cameras or phones. If you enable this policy setting, AutoPlay isn't allowed for MTP devices like cameras or phones. If you disable or don't configure this policy setting, AutoPlay is enabled for non-volume devices.  
  [Learn more](/windows/client-management/mdm/policy-csp-autoplay#autoplay-disallowautoplayfornonvolumedevices)

  **Default**: Enabled

## BitLocker

For more information, see [Policy CSP - BitLocker](/windows/client-management/mdm/policy-csp-bitlocker) in the Windows documentation.

- **BitLocker removable drive policy**:  
  This policy setting is used to control the encryption method and cipher strength. The values of this policy determine the strength of the cipher that BitLocker uses for encryption. Enterprises may want to control the encryption level for increased security (AES-256 is stronger than AES-128). If you enable this setting, you can configure an encryption algorithm and key cipher strength for fixed data drives, operating system drives, and removable data drives individually. For fixed and operating system drives, we recommend that you use the XTS-AES algorithm. For removable drives, you should use AES-CBC 128-bit or AES-CBC 256-bit if the drive is used in other devices that aren't running Windows 10 version 1511 or later, or Windows 11. Changing the encryption method has no effect if the drive is already encrypted or if encryption is in progress. In these cases, this policy setting is ignored.  
  [Learn more](/windows/security/information-protection/bitlocker/bitlocker-group-policy-settings)

  **Default**: Configure

  For BitLocker removable drive policy, configure the following setting:

  - **Block write access to removable data-drives not protected by BitLocker**:  
    **Default**: Yes

## Browser

For more information, see [Policy CSP - Browser](/windows/client-management/mdm/policy-csp-browser) in the Windows documentation.

- **Require SmartScreen for Microsoft Edge**:  
  Microsoft Edge uses Microsoft Defender SmartScreen (turned on) to protect users from potential phishing scams and malicious software by default. Also, by default, users can't disable (turn off) Microsoft Defender SmartScreen. Enabling this policy turns off Microsoft Defender SmartScreen and prevent users from turning it on. Don't configure this policy to let users choose to turn Microsoft defender SmartScreen on or off.  
  [Learn more](/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen)

  **Default**: Yes

- **Block malicious site access**:  
  By default, Microsoft Edge allows users to bypass (ignore) the Microsoft Defender SmartScreen warnings about potentially malicious sites, allowing them to continue to the site. With this policy though, you can configure Microsoft Edge to prevent users from bypassing the warnings, blocking them from continuing to the site.  
  [Learn more](/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverride)
  
  **Default**: Yes
  
- **Block unverified file download**:  
  By default, Microsoft Edge allows users to bypass (ignore) the Microsoft Defender SmartScreen warnings about potentially malicious files, allowing them to continue downloading the unverified file(s). Enabling this policy prevents users from bypassing the warnings, blocking them from downloading of the unverified file(s).  
  [Learn more](/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverrideforfiles)
  
  **Default**: Yes
  
- **Block Password Manager**:  
  By default, Microsoft Edge uses Password Manager automatically, allowing users to manager passwords locally. Disabling this policy restricts Microsoft Edge from using Password Manager. Don't configure this policy if you want to let users choose to save and manage passwords locally using Password Manager.  
  [Learn more](/windows/client-management/mdm/policy-csp-browser#browser-allowpasswordmanager)
  
  **Default**: Yes
  
- **Prevent user from overriding certificate errors**:  
  This policy setting prevents the user from ignoring Secure Sockets Layer/Transport Layer Security (SSL/TLS) certificate errors that interrupt browsing (such as "expired", "revoked", or "name mismatch" errors) in Internet Explorer. If you enable this policy setting, the user can't continue browsing. If you disable or don't configure this policy setting, the user can choose to ignore certificate errors and continue browsing.  
  [Learn more](/windows/client-management/mdm/policy-csp-browser#browser-preventcerterroroverrides)
  
  **Default**: Yes

## Connectivity

For more information, see [Policy CSP - Connectivity](/windows/client-management/mdm/policy-csp-connectivity) in the Windows documentation.

- **Block Internet download for web publishing and online ordering wizards**:  
  This policy setting specifies whether Windows should download a list of providers for the web publishing and online ordering wizards. These wizards allow users to select from a list of companies that provide services such as online storage and photographic printing. By default, Windows displays providers downloaded from a Windows website in addition to providers specified in the registry. If you enable this policy setting, Windows doesn't download providers, and only the service providers that are cached in the local registry display. If you disable or don't configure this policy setting, a list of providers downloads when the user uses the web publishing or online ordering wizards. For more information that includes details on specifying service providers in the registry, see the documentation for the web publishing and online ordering wizards.  
  [Learn more](/windows/client-management/mdm/policy-csp-connectivity#connectivity-disableinternetdownloadforwebpublishingandonlineorderingwizards)
  
  **Default**: Enabled

- **Configure secure access to UNC paths**:  
  This policy setting configures secure access to UNC paths. If you enable this policy, Windows only allows access to the specified UNC paths after fulfilling additional security requirements.  
  [Learn more](/windows/client-management/mdm/policy-csp-connectivity#connectivity-hardeneduncpaths)

  **Default**: Configure Windows to only allow access to the specified UNC paths after fulfilling additional security requirements.

  When *Configure Windows to only allow access to the specified UNC paths after fulfilling additional security requirements* is selected, you can configure the *Hardened UNC path list*.

- **Hardened UNC path list**:  
  Select **Add** to specify additional security flags and server paths.

- **Block downloading of print drivers over HTTP**:  
  This policy setting specifies whether to allow this client to download print driver packages over HTTP. To set up HTTP printing, non-inbox drivers need to be downloaded over HTTP. Note: This policy setting doesn't prevent the client from printing to printers on the Intranet or the Internet over HTTP. It only prohibits downloading drivers that aren't already installed locally. If you enable this policy setting, print drivers can't be downloaded over HTTP. If you disable or don't configure this policy setting, users can download print drivers over HTTP.  
  [Learn more](/windows/client-management/mdm/policy-csp-connectivity#connectivity-disabledownloadingofprintdriversoverhttp)
  
  **Default**: Enabled

## Credentials Delegation

For more information, see [Policy CSP - CredentialsDelegation](/windows/client-management/mdm/policy-csp-credentialsdelegation) in the Windows documentation.

- **Remote host delegation of non-exportable credentials**:  
  Remote host allows delegation of non-exportable credentials. When using credential delegation, devices provide an exportable version of credentials to the remote host, which exposes users to the risk of credential theft from attackers on the remote host. If you enable this policy setting, the host supports Restricted Admin or Remote Credential Guard mode. If you disable or don't configure this policy setting, Restricted Administration and Remote Credential Guard mode aren't supported. User will always need to pass their credentials to the host.  
  [Learn more](/windows/client-management/mdm/policy-csp-credentialsdelegation#credentialsdelegation-remotehostallowsdelegationofnonexportablecredentials)
  
  **Default**: Enabled

## Credentials UI

For more information, see [Policy CSP - CredentialsUI](/windows/client-management/mdm/policy-csp-credentialsui) in the Windows documentation.

- **Enumerate administrators**:  
  This policy setting controls whether administrator accounts display when a user attempts to elevate a running application. By default, administrator accounts aren't displayed when the user attempts to elevate a running application. If you enable this policy setting, all local administrator accounts on the PC display so the user can choose one and enter the correct password. If you disable this policy setting, users will always be required to type a user name and password to elevate.  
  [Learn more](/windows/client-management/mdm/policy-csp-credentialsui#credentialsui-enumerateadministrators)

  **Default**: Disabled

## Data Protection

For more information, see [Policy CSP - DataProtection](/windows/client-management/mdm/policy-csp-dataprotection) in the Windows documentation.

- **Block direct memory access**:  
  This policy setting allows you to block direct memory access (DMA) for all hot pluggable PCI downstream ports until a user logs into Windows. Once a user logs in, Windows will enumerate the PCI devices connected to the host plug PCI ports. Every time the user locks the machine, DMA is blocked on hot plug PCI ports with no children devices until the user logs in again. Devices that were already enumerated when the machine was unlocked will continue to function until unplugged. This policy setting is only enforced when BitLocker or device encryption is enabled.  
  [Learn more](/windows/client-management/mdm/policy-csp-dataprotection#dataprotection-allowdirectmemoryaccess)

  **Default**: Yes

## Device Guard

For more information, see [Policy CSP - DeviceGuard](/windows/client-management/mdm/policy-csp-deviceguard) in the Windows documentation.

- **Turn on credential guard**:  
  This setting lets users turn on Credential Guard with virtualization-based security to help protect credentials at next reboot.  
  [Learn more](/windows/client-management/mdm/policy-csp-deviceguard#deviceguard-lsacfgflags)

  **Default**: Enable with UEFI lock

- **Virtualization based security**:  
  Turns on virtualization-based security (VBS) at the next reboot. Virtualization based security uses the Windows Hypervisor to provide support for security services.

  **Default**: Enable VBS with secure boot

- **Enable virtualization based security**:  
  Turns on virtualization-based security (VBS) at the next reboot. Virtualization-based security uses the Windows Hypervisor to provide support for security services.  
  [Learn more](/windows/client-management/mdm/policy-csp-deviceguard#deviceguard-enablevirtualizationbasedsecurity)
  
  **Default**: Yes

- **Launch system guard**:  
  Enables Secure Launch if supported by hardware.

  **Default**: Enabled

## Device Installation

::: zone-end
::: zone pivot="mdm-december-2020,november-2021"

- **Block hardware device installation by setup classes**:  
  This policy setting allows you to specify a list of device setup class globally unique identifiers (GUIDs) for device drivers that Windows is prevented from installing. This policy setting takes precedence over any other policy setting that allows Windows to install a device. If you block installation, Windows is prevented from installing or updating device drivers whose device setup class GUIDs appear in the list you create. If you enable this policy setting on a remote desktop server, the policy setting affects redirection of the specified devices from a remote desktop client to the remote desktop server. If you allow installation, Windows can install and update devices as allowed or prevented by other policy settings.  
  [Learn more](/windows/client-management/mdm/policy-csp-deviceinstallation#deviceinstallation-allowinstallationofmatchingdevicesetupclassess)

  **Default**: Yes
  
  When *Yes* is selected, the following settings are available.

  - **Remove matching hardware devices**:  
    This setting is available only when *Block hardware device installation by setup classes* is set to *Yes*.

    **Default**: Yes

  - **Block list**
    Manage a list of device setup class globally unique identifiers that for device drivers that Windows is prevented from installing.
 
::: zone-end
::: zone pivot="mdm-sept-2020"

For more information, see [Policy CSP - DeviceInstallation](/windows/client-management/mdm/policy-csp-deviceinstallation) in the Windows documentation.

- **Hardware device installation by device identifiers**:  
  This policy setting allows you to specify a list of Plug and Play hardware IDs and compatible IDs for devices that Windows is prevented from installing. This policy setting takes precedence over any other policy setting that allows Windows to install a device. If you enable this policy setting, Windows can't install a device whose hardware ID or compatible ID appears in the list you create. If you enable this policy setting on a remote desktop server, the policy setting affects redirection of the specified devices from a remote desktop client to the remote desktop server. If you disable or don't configure this policy setting, devices can install and update as allowed or prevented by other policy settings.  
  [Learn more](/windows/client-management/mdm/policy-csp-deviceinstallation#deviceinstallation-preventinstallationofmatchingdeviceids)

  **Default**: Block hardware device installation

  When *Block hardware device installation* is selected, the following settings are available.

  - **Remove matching hardware devices**:  
    This setting is available only when *Hardware device installation by device identifiers* is set to *Block hardware device installation*.

    **Default**: Yes

  - **Hardware device identifiers that are blocked**:  
    This setting is available only when *Hardware device installation by device identifiers* is set to *Block hardware device installation*.

    **Default**: Yes

- **Hardware device installation by setup classes**:  
  This policy setting allows you to specify a list of device setup class globally unique identifiers (GUIDs) for device drivers that Windows is prevented from installing. This policy setting takes precedence over any other policy setting that allows Windows to install a device. If you enable this policy setting, Windows can't install or update device drivers whose device setup class GUIDs appear in the list you create. If you enable this policy setting on a remote desktop server, the policy setting affects redirection of the specified devices from a remote desktop client to the remote desktop server. If you disable or don't configure this policy setting, Windows can install and update devices as allowed or prevented by other policy settings.  
  [Learn more](/windows/client-management/mdm/policy-csp-deviceinstallation#deviceinstallation-preventinstallationofmatchingdevicesetupclasses)

  **Default**: Block hardware device installation

  When *Block hardware device installation* is selected, the following settings are available.

  - **Remove matching hardware devices**:  
    This setting is available only when *Hardware device installation by setup classes* is set to *Block hardware device installation*.

    **Default**: *No default configuration*

  - **Hardware device identifiers that are blocked**:  
    This setting is available only when *Hardware device installation by setup classes* is set to *Block hardware device installation*.

    **Default**: *No default configuration*

::: zone-end
::: zone pivot="mdm-sept-2020,mdm-december-2020,november-2021"

## Device Lock

For more information, see [Policy CSP - DeviceLock](/windows/client-management/mdm/policy-csp-devicelock) in the Windows documentation.

- **Require password**:  
  Specifies whether device lock is enabled.  
  [Learn more](/windows/client-management/mdm/policy-csp-devicelock#devicelock-devicepasswordenabled)  

  **Default**: Yes
  
  When *Require password* is set to *Yes*, the following settings are available.

  - **Required password**:  
    Determines the type of PIN or password required.  
    [Learn more](/windows/client-management/mdm/policy-csp-devicelock#devicelock-alphanumericdevicepasswordrequired)

    **Default**: Alphanumeric

  - **Password expiration (days)**:  
    The Maximum password age policy setting determines how long (in days) that a password can be used before the system requires the user to change it. You can set passwords to expire after a number of days between 1 and 999, or you can specify that passwords never expire by setting the number of days to 0. If Maximum password age is between 1 and 999 days, the minimum password age must be less than the maximum password age. If Maximum password age is set to 0, Minimum password age can be any value between 0 and 998 days.  
    [Learn more](/windows/security/threat-protection/security-policy-settings/maximum-password-age)

    **Default**: 60

  - **Password minimum character set count**:  
    The number of complex element types (uppercase and lowercase letters, numbers, and punctuation) required for a strong PIN or password. PIN enforces the following behavior for desktop and mobile devices: 1 - Digits only 2 - Digits and lowercase letters are required 3 - Digits, lowercase letters, and uppercase letters are required. Not supported in desktop Microsoft accounts and domain accounts. 4 - Digits, lowercase letters, uppercase letters, and special characters are required. Not supported in desktop.  
    [Learn more](/windows/client-management/mdm/policy-csp-devicelock#devicelock-mindevicepasswordcomplexcharacters)

    **Default**: 3

  - **Prevent reuse of previous passwords**:  
    Specifies how many passwords are stored in the history that can't be used. The value includes the user's current password. For example, with a setting of *1* the user can't reuse their current password when choosing a new password. A setting of *5* means that a user can't set their new password to their current password or any of their previous four passwords.  
    [Learn more](/windows/client-management/mdm/policy-csp-devicelock#devicelock-devicepasswordhistory)

    **Default**: 24

  - **Minimum password length**:  
    The Minimum password length policy setting determines the least number of characters that can make up a password for a user account. You can set a value of between 1 and 14 characters, or you can establish that no password is required by setting the number of characters to 0.  
    [Learn more](/windows/security/threat-protection/security-policy-settings/minimum-password-length)

    **Default**: 8


  - **Number of sign-in failures before wiping device**:  
    The number of authentication failures allowed before the device is wiped. A value of 0 disables device wipe functionality.  
    [Learn more](/windows/client-management/mdm/policy-csp-devicelock#devicelock-maxdevicepasswordfailedattempts)

    **Default**: 10

  - **Block simple passwords**:  
    Specifies whether PINs or passwords such as "1111" or "1234" are allowed. For the desktop, it also controls the use of picture passwords.  
    [Learn more](/windows/client-management/mdm/policy-csp-devicelock#devicelock-allowsimpledevicepassword)

    **Default**: Yes  
    *A setting of Yes prevents use of simple passwords.*

- **Password minimum age in days**:  
  The Minimum password age policy setting determines the how long (in days) that a password must be used before the user can change it. You can set a value between 1 and 998 days, or you can allow password changes immediately by setting the number of days to 0. The minimum password age must be less than the Maximum password age, unless the maximum password age is set to 0, indicating that passwords will never expire. If the maximum password age is set to 0, the minimum password age can be set to any value between 0 and 998.  
  [Learn more](/windows/client-management/mdm/policy-csp-devicelock#devicelock-minimumpasswordage)

  **Default**: 1

- **Prevent use of camera**:  
  Disables the lock screen camera toggle switch in PC Settings and prevents a camera from being invoked on the lock screen. By default, users can enable invocation of an available camera on the lock screen. If you enable this setting, users can't enable or disable lock screen camera access in PC Settings, and the camera can't be invoked on the lock screen.  
  [Learn more](/windows/client-management/mdm/policy-csp-devicelock#devicelock-preventenablinglockscreencamera)

  **Default**: Enabled

- **Prevent slide show**:  
  Disables the lock screen slide show settings in PC Settings and prevents a slide show from playing on the lock screen. By default, users can enable a slide show that will run after they lock the machine. If you enable this setting, users can't modify slide show settings in PC Settings, and no slide show can start.  
  [Learn more](/windows/client-management/mdm/policy-csp-devicelock#devicelock-preventlockscreenslideshow)

  **Default**: Enabled *A setting of Enabled prevents slide shows from running.*

## DMA Guard

For more information, see [Policy CSP - DmaGuard](/windows/client-management/mdm/policy-csp-dmaguard) in the Windows documentation.

- **Enumeration of external devices incompatible with Kernel DMA Protection**:  
  This policy is intended to provide additional security against external DMA capable devices. It allows for more control over the enumeration of external DMA capable devices incompatible with DMA Remapping/device memory isolation and sandboxing. This policy only takes effect when Kernel DMA Protection is supported and enabled by the system firmware. Kernel DMA Protection is a platform feature that can't be controlled via policy or by end user. It has to be supported by the system at the time of manufacturing. To check if the system supports Kernel DMA Protection, check the Kernel DMA Protection field in the Summary page of MSINFO32.exe.  
  [Learn more](/windows/client-management/mdm/policy-csp-dmaguard#dmaguard-deviceenumerationpolicy)

  **Default**: Block all

## Event Log Service

For more information, see [Policy CSP - EventLogService](/windows/client-management/mdm/policy-csp-eventlogservice) in the Windows documentation.

- **Application log maximum file size in KB**:  
  This policy setting specifies the maximum size of the log file in kilobytes. If you enable this policy setting, you can configure the maximum log file size to be between 1 megabyte (1024 kilobytes) and 2 terabytes (2147483647 kilobytes) in kilobyte increments. If you disable or don't configure this policy setting, the maximum size of the log file is set to the locally configured value. This value can be changed by the local administrator using the Log Properties dialog and it defaults to 20 megabytes.  
  [Learn more](/windows/client-management/mdm/policy-csp-eventlogservice#eventlogservice-specifymaximumfilesizeapplicationlog)

  **Default**: 32768

- **Security log maximum file size in KB**:  
  This policy setting specifies the maximum size of the log file in kilobytes. If you enable this policy setting, you can configure the maximum log file size to be between 1 megabyte (1024 kilobytes) and 2 terabytes (2147483647 kilobytes) in kilobyte increments. If you disable or don't configure this policy setting, the maximum size of the log file is set to the locally configured value. This value can be changed by the local administrator using the Log Properties dialog and it defaults to 20 megabytes.  
  [Learn more](/windows/client-management/mdm/policy-csp-eventlogservice#eventlogservice-specifymaximumfilesizesecuritylog)

   **Default**: 196608

- **System log maximum file size in KB**:  
  This policy setting specifies the maximum size of the log file in kilobytes. If you enable this policy setting, you can configure the maximum log file size to be between 1 megabyte (1024 kilobytes) and 2 terabytes (2147483647 kilobytes) in kilobyte increments. If you disable or don't configure this policy setting, the maximum size of the log file is set to the locally configured value. This value can be changed by the local administrator using the Log Properties dialog and it defaults to 20 megabytes.  
  [Learn more](/windows/client-management/mdm/policy-csp-eventlogservice#eventlogservice-specifymaximumfilesizesystemlog)

  **Default**: 32768

## Experience

For more information, see [Policy CSP - Experience](/windows/client-management/mdm/policy-csp-experience) in the Windows documentation.

- **Block Windows Spotlight**:  
  Allows IT admins to turn off (block) all Windows Spotlight Features. This includes Window spotlight on lock screen, Windows Tips, Microsoft consumer features, and other related features.  
  [Learn more](/windows/client-management/mdm/policy-csp-experience#experience-allowwindowsspotlight)

  **Default**: Yes

  When *Block Windows Spotlight* is set to *Not configured*, Windows Spotlight isn't blocked on devices, and you can then configure the following settings to block selected items for Windows Spotlight:

  - **Block third-party suggestions in Windows Spotlight**:  
    Specifies whether to allow app and content suggestions from third-party software publishers in Windows spotlight features like lock screen spotlight, suggested apps in the Start menu, and Windows tips. Users may still see suggestions for Microsoft features, apps, and services.  
    [Learn more](/windows/client-management/mdm/policy-csp-experience#experience-allowthirdpartysuggestionsinwindowsspotlight)

    **Default**: Not configured

  - **Block consumer specific features**:  
    Allows IT admins to turn on experiences that are typically for consumers only, such as Start suggestions, Membership notifications, Post-OOBE app install, and redirect tiles.  
    [Learn more](/windows/client-management/mdm/policy-csp-experience#experience-allowwindowsconsumerfeatures)

    **Default**: Not configured

::: zone-end
::: zone pivot="mdm-sept-2020"

## Exploit Guard

For more information, see [Policy CSP - ExploitGuard](/windows/client-management/mdm/policy-csp-exploitguard) in the Windows documentation.

- **Upload XML**:  
  Enables the IT admin to push out a configuration that represents the desired system and application mitigation options to all the devices in the organization. The configuration is represented by an XML. Exploit protection helps protect devices from malware that use exploits to spread and infect. You use the Windows Security app or PowerShell to create a set of mitigations (known as a configuration). You can then export this configuration as an XML file and share it with multiple machines on your network so they all have the same set of mitigation settings. You can also convert and import an existing EMET configuration XML file into an exploit protection configuration XML.  
  [Learn more](/windows/client-management/mdm/policy-csp-exploitguard#exploitguard-exploitprotectionsettings)

  **Default**: *Sample xml is provided*

::: zone-end
::: zone pivot="mdm-sept-2020,mdm-december-2020,november-2021"

## File Explorer

For more information, see [Policy CSP - FileExplorer](/windows/client-management/mdm/policy-csp-fileexplorer) in the Windows documentation.  

- **Block data execution prevention**:  
  Disabling data execution prevention can allow certain legacy plug-in applications to function without terminating Explorer.  
  [Learn more](/windows/client-management/mdm/policy-csp-fileexplorer#fileexplorer-turnoffdataexecutionpreventionforexplorer)  

  **Default**: Disabled

- **Block heap termination on corruption**:  
  Disabling heap termination on corruption can allow certain legacy plug-in applications to function without terminating Explorer immediately, although Explorer may still terminate unexpectedly later.  
  [Learn more](/windows/client-management/mdm/policy-csp-fileexplorer#fileexplorer-turnoffheapterminationoncorruption)

  **Default**: Disabled

## Firewall

For more information, see [2.2.2 FW_PROFILE_TYPE]( /openspecs/windows_protocols/ms-fasp/7704e238-174d-4a5e-b809-5f3787dd8acc) in the Windows Protocols documentation.

- **Firewall profile domain**:  
  Specifies the profiles to which the rule belongs: Domain, Private, Public. This value represents the profile for networks that are connected to domains.  
  [Learn more](/openspecs/windows_protocols/ms-fasp/7704e238-174d-4a5e-b809-5f3787dd8acc)

  - **Inbound connections blocked**:  
    **Default**: Yes

  - **Outbound connections required**:  
    **Default**: Yes

  - **Inbound notifications blocked**:  
    **Default**: Yes

  - **Firewall enabled**:  
    **Default**: Allowed

- **Firewall profile public**:  
  Specifies the profiles to which the rule belongs: Domain, Private, Public. This value represents the profile for public networks. These networks are classified as public by the administrators in the server host. The classification happens the first time the host connects to the network. Usually these networks are those at airports, coffee shops, and other public places where the peers in the network or the network administrator aren't trusted.  
  [Learn more](/openspecs/windows_protocols/ms-fasp/7704e238-174d-4a5e-b809-5f3787dd8acc)

  - **Inbound connections blocked**:  
    **Default**: Yes

  - **Outbound connections required**:  
    **Default**: Yes

  - **Inbound notifications blocked**:  
    **Default**: Yes

  - **Firewall enabled**:  
    **Default**: Allowed

  - **Connection security rules from group policy not merged**:  
    **Default**: Yes

  - **Policy rules from group policy not merged**:  
    **Default**: Yes

- **Firewall profile private**:  
  Specifies the profiles to which the rule belongs: Domain, Private, Public. This value represents the profile for private networks.  
  [Learn more](/openspecs/windows_protocols/ms-fasp/7704e238-174d-4a5e-b809-5f3787dd8acc)

  - **Inbound connections blocked**:  
    **Default**: Yes

  - **Outbound connections required**:  
    **Default**: Yes

  - **Inbound notifications blocked**:  
    **Default**: Yes

  - **Firewall enabled**:  
    **Default**: Allowed

## Internet Explorer

For more information, see [Policy CSP - InternetExplorer](/windows/client-management/mdm/policy-csp-internetexplorer) in the Windows documentation.

- **Internet Explorer restricted zone updates to status bar via script**:  
  This policy setting allows you to manage whether a script is allowed to update the status bar within the zone.

  - *If you enable this policy setting*, scripts are allowed to update the status bar.
  - *If you disable or don't configure this policy setting*, scripts aren't allowed to update the status bar.

  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-restrictedsiteszoneallowupdatestostatusbarviascript)

  **Default**: Disabled

- **Internet Explorer internet zone drag and drop or copy and paste files**:  
  This policy setting allows you to manage whether users can drag files or copy and paste files from a source within the zone. If you enable this policy setting, users can drag files or copy and paste files from this zone automatically. If you select Prompt in the drop-down box, users are queried to choose whether to drag or copy files from this zone. If you disable this policy setting, users are prevented from dragging files or copying and pasting files from this zone. If you don't configure this policy setting, users can drag files or copy and paste files from this zone automatically.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-internetzoneallowdraganddropcopyandpastefiles)

  **Default**: Disable

- **Internet Explorer restricted zone .NET Framework reliant components**:  
  Use this policy setting to manage whether .NET Framework components that aren't signed with Authenticode can be executed from Internet Explorer. These components include managed controls referenced from an object tag and managed executables referenced from a link. If you enable this policy setting, Internet Explorer will execute unsigned managed components. If you select Prompt in the drop-down box, Internet Explorer will prompt the user to determine whether to execute unsigned managed components. If you disable this policy setting, Internet Explorer won't execute unsigned managed components. If you don't configure this policy setting, Internet Explorer will not execute unsigned managed components.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-restrictedsiteszoneallownetframeworkreliantcomponents)

  **Default**: Disable

- **Internet Explorer local machine zone do not run antimalware against Active X controls**:  
  This policy setting determines whether Internet Explorer runs antimalware programs against ActiveX controls, to check if they're safe to load on pages. If you enable this policy setting, Internet Explorer won't check with your antimalware program to see if it's safe to create an instance of the ActiveX control. If you disable this policy setting, Internet Explorer always checks with your antimalware program to see if it's safe to create an instance of the ActiveX control. If you don't configure this policy setting, Internet Explorer won't check with your antimalware program to see if it's safe to create an instance of the ActiveX control. Users can turn this behavior on or off, using Internet Explorer Security settings.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-localmachinezonedonotrunantimalwareagainstactivexcontrols)

  **Default**: Disabled

- **Internet Explorer internet zone access to data sources**:  
  This policy setting allows you to manage whether Internet Explorer can access data from another security zone using the Microsoft XML Parser (MSXML) or ActiveX Data Objects (ADO). If you enable this policy setting, users can load a page in the zone that uses MSXML or ADO to access data from another site in the zone. If you select Prompt in the drop-down box, users are queried to choose whether to allow a page to load in the zone that uses MSXML or ADO to access data from another site in the zone. If you disable this policy setting, users can't load a page in the zone that uses MSXML or ADO to access data from another site in the zone. If you don't configure this policy setting, users can't load a page in the zone that uses MSXML or ADO to access data from another site in the zone.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-internetzoneallowaccesstodatasources)  

  **Default**: Disable

- **Internet Explorer restricted zone drag content from different domains within windows**:  
  This policy setting allows you to set options for dragging content from one domain to a different domain when the source and destination are in the same window. If you enable this policy setting and click Enable, users can drag content from one domain to a different domain when the source and destination are in the same window. Users can't change this setting. If you enable this policy setting and click Disable, users can't drag content from one domain to a different domain when the source and destination are in the same window. Users can't change this setting in the Internet Options dialog. In Internet Explorer 10, if you disable this policy setting or don't configure it, users can't drag content from one domain to a different domain when the source and destination are in the same window. Users can change this setting in the Internet Options dialog. In Internet Explorer 9 and earlier versions, if you disable this policy setting or don't configure it, users can drag content from one domain to a different domain when the source and destination are in the same window. Users can't change this setting in the Internet Options dialog.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-restrictedsiteszoneenabledraggingofcontentfromdifferentdomainswithinwindows)  

  **Default**: Disabled

- **Internet Explorer certificate address mismatch warning**:  
  This policy setting allows you to turn on the certificate address mismatch security warning. When this policy setting is on, the user is warned when visiting Secure HTTP (HTTPS) websites that present certificates issued for a different website address. This warning helps prevent spoofing attacks. If you enable this policy setting, the certificate address mismatch warning always appears. If you disable or don't configure this policy setting, the user can choose whether the certificate address mismatch warning appears (by using the Advanced page in the Internet Control panel).  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-allowcertificateaddressmismatchwarning)  

  **Default**: Enabled

- **Internet Explorer restricted zone less privileged sites**:  
  This policy setting allows you to manage whether Web sites from less privileged zones, such as Internet sites, can navigate into this zone. If you enable this policy setting, Web sites from less privileged zones can open new windows in, or navigate into, this zone. The security zone will run without the added layer of security that is provided by the Protection from Zone Elevation security feature. If you select Prompt in the drop-down box, a warning is issued to the user that potentially risky navigation is about to occur. If you disable this policy setting, possibly harmful navigation is prevented. The Internet Explorer security feature is on in this zone as set by Protection from Zone Elevation feature control. If you don't configure this policy setting, possibly harmful navigation is prevented. The Internet Explorer security feature is on in this zone as set by Protection from Zone Elevation feature control.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-internetzoneallowlessprivilegedsites)

  **Default**: Disable

- **Internet Explorer restricted zone automatic prompt for file downloads**:  
  This policy setting determines whether users are prompted for non user-initiated file downloads. Regardless of this setting, users will receive file download dialogs for user-initiated downloads. If you enable this setting, users will receive a file download dialog for automatic download attempts. If you disable or don't configure this setting, file downloads that aren't user-initiated are blocked, and users will see the Notification bar instead of the file download dialog. Users can then click the Notification bar to allow the file download prompt.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-restrictedsiteszoneallowautomaticpromptingforfiledownloads)

  **Default**: Disabled

- **Internet Explorer internet zone .NET Framework reliant components**:  
  This policy setting allows you to manage whether .NET Framework components that aren't signed with Authenticode can be executed from Internet Explorer. These components include managed controls referenced from an object tag and managed executables referenced from a link. If you enable this policy setting, Internet Explorer will execute unsigned managed components. If you select Prompt in the drop-down box, Internet Explorer will prompt the user to determine whether to execute unsigned managed components. If you disable this policy setting, Internet Explorer won't execute unsigned managed components. If you don't configure this policy setting, Internet Explorer will execute unsigned managed components.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-internetzoneallownetframeworkreliantcomponents)

  **Default**: Disable

- **Internet Explorer internet zone allow only approved domains to use tdc ActiveX controls**:  
  This policy setting controls if the user can run the TDC ActiveX control on websites. If you enable this policy setting, the TDC ActiveX control won't run from websites in this zone. If you disable this policy setting, the TDC Active X control will run from all sites in this zone.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-internetzoneallowonlyapproveddomainstousetdcactivexcontrol)

  **Default**: Enabled

- **Internet Explorer restricted zone script initiated windows**:  
  This policy setting allows you to manage restrictions on script-initiated pop-up windows and windows that include the title and status bars. If you enable this policy setting, Windows Restrictions security won't apply in this zone. The security zone runs without the added layer of security provided by this feature. If you disable this policy setting, the possible harmful actions contained in script-initiated pop-up windows and windows that include the title and status bars can't run. This Internet Explorer security feature is on in this zone as dictated by the Scripted Windows Security Restrictions feature control setting for the process. If you don't configure this policy setting, the possible harmful actions contained in script-initiated pop-up windows and windows that include the title and status bars can't run. This Internet Explorer security feature is on in this zone as dictated by the Scripted Windows Security Restrictions feature control setting for the process.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-restrictedsiteszoneallowscriptinitiatedwindows)

  **Default**: Disabled

- **Internet Explorer internet zone include local path when uploading files to server**:  
  This policy setting controls if local path information gets sent when the user is uploading a file via an HTML form. If the local path information is sent, some information may be unintentionally revealed to the server. For instance, files sent from the user's desktop may contain the user name as a part of the path. If you enable this policy setting, path information is sent when the user is uploading a file via an HTML form. If you disable this policy setting, path information is removed when the user is uploading a file via an HTML form. If you don't configure this policy setting, the user can choose whether path information gets sent when they upload a file via an HTML form. By default, path information is sent.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-internetzoneincludelocalpathwhenuploadingfilestoserver)

  **Default**: Disabled

- **Internet Explorer disable processes in enhanced protected mode**:  
  This policy setting determines whether Internet Explorer 11 uses 64-bit processes (for greater security) or 32-bit processes (for greater compatibility) when running in Enhanced Protected Mode on 64-bit versions of Windows. Important: Some ActiveX controls and toolbars may not be available when 64-bit processes are used. If you enable this policy setting, Internet Explorer 11 will use 64-bit tab processes when running in Enhanced Protected Mode on 64-bit versions of Windows. If you disable this policy setting, Internet Explorer 11 will use 32-bit tab processes when running in Enhanced Protected Mode on 64-bit versions of Windows. If you don't configure this policy setting, users can turn this feature on or off using Internet Explorer settings. This feature is turned off by default.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-disableprocessesinenhancedprotectedmode)

  **Default**: Enabled

- **Internet Explorer ignore certificate errors**:  
  This policy setting prevents the user from ignoring Secure Sockets Layer/Transport Layer Security (SSL/TLS) certificate errors that interrupt browsing (such as "expired", "revoked", or "name mismatch" errors) in Internet Explorer. If you enable this policy setting, the user can't continue browsing. If you disable or don't configure this policy setting, the user can ignore certificate errors and continue browsing.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-disableignoringcertificateerrors)

  **Default**: Disabled

- **Internet Explorer internet zone loading of XAML files**:  
  This policy setting allows you to manage the loading of Extensible Application Markup Language (XAML) files. XAML is an XML-based declarative markup language commonly used for creating rich user interfaces and graphics that take advantage of the Windows Presentation Foundation. If you enable this policy setting and set the drop-down box to Enable, XAML files are automatically loaded inside Internet Explorer. The user can't change this behavior. If you set the drop-down box to Prompt, the user is prompted for loading XAML files. If you disable this policy setting, XAML files aren't loaded inside Internet Explorer. The user can't change this behavior. If you don't configure this policy setting, the user can decide whether to load XAML files inside Internet Explorer.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-internetzoneallowloadingofxamlfiles)

  **Default**: Disable

- **Internet Explorer internet zone automatic prompt for file downloads**:  
  This policy setting determines whether users are prompted for non user-initiated file downloads. Regardless of this setting, users will receive file download dialogs for user-initiated downloads. If you enable this setting, users will receive a file download dialog for automatic download attempts. If you disable or don't configure this setting, file downloads that aren't user-initiated are blocked, and users will see the Notification bar instead of the file download dialog. Users can then click the Notification bar to allow the file download prompt.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-internetzoneallowautomaticpromptingforfiledownloads)

  **Default**: Disabled

- **Internet Explorer restricted zone security warning for potentially unsafe files**:  
  This policy setting controls if the "Open File - Security Warning" message appears when the user tries to open executable files or other potentially unsafe files (from an intranet file share by using File Explorer, for example). If you enable this policy setting and set the drop-down box to Enable, these files open without a security warning. If you set the drop-down box to Prompt, a security warning appears before the files open. If you disable this policy setting, these files don't open. If you don't configure this policy setting, the user can configure how the computer handles these files. By default, these files are blocked in the Restricted zone, enabled in the Intranet and Local Computer zones, and set to prompt in the Internet and Trusted zones.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-restrictedsiteszoneshowsecuritywarningforpotentiallyunsafefiles)

  **Default**: Disable

- **Internet Explorer internet zone cross site scripting filter**:  
  This policy controls if the Cross-Site Scripting (XSS) Filter will detect and prevent cross-site script injections into websites in this zone. If you enable this policy setting, the XSS Filter is on for sites in this zone, and the XSS Filter attempts to block cross-site script injections. If you disable this policy setting, the XSS Filter is turned off for sites in this zone, and Internet Explorer permits cross-site script injections.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-internetzoneenablecrosssitescriptingfilter)

  **Default**: Enabled

- **Internet Explorer fallback to SSL3**:  
  This policy setting allows you to block an insecure fallback to SSL 3.0. When this policy is enabled, Internet Explorer will attempt to connect to sites using SSL 3.0 or below when TLS 1.0 or greater fails. To prevent a man-in-the-middle attack, we recommend you don't allow insecure fallback. This policy doesn't affect which security protocols are enabled. If you disable this policy, system defaults are used.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-allowfallbacktossl3)

  **Default**: No sites

- **Internet Explorer encryption support**:  
  This policy setting allows you to turn off support for Transport Layer Security (TLS) 1.0, TLS 1.1, TLS 1.2, Secure Sockets Layer (SSL) 2.0, or SSL 3.0 in the browser. TLS and SSL are protocols that help protect communication between the browser and the target server. When the browser attempts to set up a protected communication with the target server, the browser and server negotiate which protocol and version to use. The browser and server attempt to match each other's list of supported protocols and versions, and they select the most preferred match. If you enable this policy setting, the browser negotiates or doesn't negotiate an encryption tunnel by using the encryption methods that you select from the drop-down list. If you disable or don't configure this policy setting, the user can select which encryption method the browser supports.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-disableencryptionsupport)

  **Default**: 2 items:  TLS v1.1 and TLS v1.2  
  *Select the down arrow to display options that you can select for this setting.*

- **Internet Explorer locked down internet zone smart screen**:  
  This policy setting controls whether SmartScreen Filter scans pages in this zone for malicious content. If you enable this policy setting, SmartScreen Filter scans pages in this zone for malicious content. If you disable this policy setting, SmartScreen Filter doesn't scan pages in this zone for malicious content. If you don't configure this policy setting, the user can choose whether SmartScreen Filter scans pages in this zone for malicious content. Note: In Internet Explorer 7, this policy setting controls whether Phishing Filter scans pages in this zone for malicious content.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-lockeddowninternetzoneallowsmartscreenie)

  **Default**: Enabled

- **Internet Explorer restricted zone launch applications and files in an iFrame**:  
  This policy setting allows you to manage whether applications may be run and files may be downloaded from an IFRAME reference in the HTML of the pages in this zone. If you enable this policy setting, users can run applications and download files from IFRAMEs on the pages in this zone without user intervention. If you select Prompt in the drop-down box, users are queried to choose whether to run applications and download files from IFRAMEs on the pages in this zone. If you disable this policy setting, users can't run applications and download files from IFRAMEs on the pages in this zone. If you don't configure this policy setting, users can't run applications and download files from IFRAMEs on the pages in this zone.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-restrictedsiteszonelaunchingapplicationsandfilesiniframe)

  **Default**: Disable

- **Internet Explorer bypass smart screen warnings about uncommon files**:  
  This policy setting determines whether the user can bypass warnings from SmartScreen Filter. SmartScreen Filter warns the user about executable files that Internet Explorer users don't commonly download from the Internet. If you enable this policy setting, SmartScreen Filter warnings block the user. If you disable or don't configure this policy setting, the user can bypass SmartScreen Filter warnings.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-disablebypassofsmartscreenwarningsaboutuncommonfiles)

  **Default**: Disabled

- **Internet Explorer internet zone popup blocker**:  
  This policy setting allows you to manage whether unwanted pop-up windows appear. Pop-up windows that are opened when the end user clicks a link aren't blocked. If you enable this policy setting, most unwanted pop-up windows are prevented from appearing. If you disable this policy setting, pop-up windows aren't prevented from appearing. If you don't configure this policy setting, most unwanted pop-up windows are prevented from appearing.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-internetzoneusepopupblocker)

  **Default**: Enable

- **Internet Explorer processes consistent MIME handling**:  
  Internet Explorer contains dynamic binary behaviors: components that encapsulate specific functionality for the HTML elements to which they're attached. This policy setting controls whether the Binary Behavior Security Restriction setting is prevented or allowed. If you enable this policy setting, binary behaviors are prevented for the File Explorer and Internet Explorer processes. If you disable this policy setting, binary behaviors are allowed for the File Explorer and Internet Explorer processes. If you don't configure this policy setting, binary behaviors are prevented for the File Explorer and Internet Explorer processes.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-consistentmimehandlinginternetexplorerprocesses)  

  **Default**: Enabled

- **Internet Explorer restricted zone java permissions**:  
  This policy setting allows you to manage permissions for Java applets. If you enable this policy setting, you can choose options from the drop-down box. Custom, to control permissions settings individually. Low Safety enables applets to do all operations. Medium Safety enables applets to run in their sandbox (an area in memory outside of which the program can't make calls), plus capabilities like scratch space (a safe and secure storage area on the client computer) and user-controlled file I/O. High Safety enables applets to run in their sandbox. Disable Java to prevent any applets from running. If you disable this policy setting, Java applets can't run. If you don't configure this policy setting, Java applets are disabled.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-restrictedsiteszonejavapermissions)

  **Default**: Disable java

- **Internet Explorer Active X controls in protected mode**:  
  This policy setting prevents ActiveX controls from running in Protected Mode when Enhanced Protected Mode is enabled. When a user has an ActiveX control installed that isn't compatible with Enhanced Protected Mode and a website attempts to load the control, Internet Explorer notifies the user and gives the option to run the website in regular Protected Mode. This policy setting disables this notification and forces all websites to run in Enhanced Protected Mode. Enhanced Protected Mode provides additional protection against malicious websites by using 64-bit processes on 64-bit versions of Windows. For computers running at least Windows 8, Enhanced Protected Mode also limits the locations Internet Explorer can read from in the registry and the file system. When Enhanced Protected Mode is enabled, and a user comes across a website that attempts to load an ActiveX control that isn't compatible with Enhanced Protected Mode, Internet Explorer notifies the user and gives the option to disable Enhanced Protected Mode for that particular website. If you enable this policy setting, Internet Explorer won't give the user the option to disable Enhanced Protected Mode. All Protected Mode websites will run in Enhanced Protected Mode. If you disable or don't configure this policy setting, Internet Explorer notifies users and provides an option to run websites with incompatible ActiveX controls in regular Protected Mode.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-donotallowactivexcontrolsinprotectedmode)

  **Default**: Disabled

- **Internet Explorer restricted zone loading of XAML files**:  
  This policy setting allows you to manage the loading of Extensible Application Markup Language (XAML) files. XAML is an XML-based declarative markup language commonly used for creating rich user interfaces and graphics that take advantage of the Windows Presentation Foundation. If you enable this policy setting and set the drop-down box to Enable, XAML files are automatically loaded inside Internet Explorer. The user can't change this behavior. If you set the drop-down box to Prompt, the user is prompted for loading XAML files. If you disable this policy setting, XAML files aren't loaded inside Internet Explorer. The user can't change this behavior. If you don't configure this policy setting, the user can decide whether to load XAML files inside Internet Explorer.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-restrictedsiteszoneallowloadingofxamlfiles)

  **Default**: Disable

- **Internet Explorer processes scripted window security restrictions**:  
  Internet Explorer allows scripts to programmatically open, resize, and reposition windows of various types. The Window Restrictions security feature restricts popup windows and prohibits scripts from displaying windows in which the title and status bars aren't visible to the user or obfuscate other Windows' title and status bars. If you enable this policy setting, scripted windows are restricted for all processes. If you disable or don't configure this policy setting, scripted windows aren't restricted.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-scriptedwindowsecurityrestrictionsinternetexplorerprocesses)

  **Default**: Enabled

- **Internet Explorer restricted zone run Active X controls and plugins**:  
  This policy setting allows you to manage whether ActiveX controls and plug-ins can run on pages from the specified zone. If you enable this policy setting, controls and plug-ins can run without user intervention. If you selected Prompt in the drop-down box, users are asked to choose whether to allow the controls or plug-in to run. If you disable this policy setting, controls and plug-ins are prevented from running. If you don't configure this policy setting, controls and plug-ins are prevented from running.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-restrictedsiteszonerunactivexcontrolsandplugins)

  **Default**: Disable

- **Internet Explorer restricted zone script Active X controls marked safe for scripting**:  
  This policy setting allows you to manage whether an ActiveX control marked safe for scripting can interact with a script. If you enable this policy setting, script interaction can occur automatically without user intervention. If you select Prompt in the drop-down box, users are queried to choose whether to allow script interaction. If you disable this policy setting, script interaction is prevented from occurring. If you don't configure this policy setting, script interaction is prevented from occurring.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-restrictedsiteszonescriptactivexcontrolsmarkedsafeforscripting)

  **Default**: Disable

- **Internet Explorer restricted zone logon options**:  
  This policy setting allows you to manage settings for sign-in options. If you enable this policy setting, you can choose from the following sign-in options.

  - *Anonymous*  - Use anonymous sign-in to disable HTTP authentication and use the guest account only for the Common Internet File System (CIFS) protocol.

  - *Prompt* - Use prompt for user name and password to query users for user IDs and passwords. After a user is queried, these values can be used silently for the rest of the session.

  - *Automatic sign in only in Intranet zone* - Use this option to query users for user IDs and passwords in other zones. After a user is queried, these values can be used silently for the rest of the session.

  - *Automatic sign in with current user name and password*- Use this option to attempt sign in using Windows NT Challenge Response (also known as NTLM authentication). If the server supports Windows NT Challenge Response, the sign in uses the user's network user name and password for sign in. If the server doesn't support Windows NT Challenge Response, the user is queried to provide the user name and password.

  If you disable this policy setting, sign-in is set to *Automatic sign in only in Intranet zone*. If you don't configure this policy setting, sign-in is set to *Prompt* for username and password.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-restrictedsiteszonelogonoptions)

  **Default**: Anonymous

- **Internet Explorer trusted zone initialize and script Active X controls not marked as safe**:  
  This policy setting allows you to manage ActiveX controls not marked as safe. If you enable this policy setting, ActiveX controls run, loaded with parameters, and scripted without setting object safety for untrusted data or scripts. This setting isn't recommended, except for secure and administered zones. This setting causes both unsafe and safe controls to be initialized and scripted, ignoring the Script ActiveX controls marked safe for scripting option. If you enable this policy setting and select Prompt in the drop-down box, users are queried whether to allow the control to load with parameters or scripted. If you disable this policy setting, ActiveX controls that can't be made safe aren't loaded with parameters or scripted. If you don't configure this policy setting, users are queried whether to allow the control to load with parameters or scripted.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-internetzoneinitializeandscriptactivexcontrolsnotmarkedsafe)

  **Default**: Disable

- **Internet Explorer check server certificate revocation**:  
  This policy setting allows you to manage whether Internet Explorer will check revocation status of servers' certificates. Certificates are revoked when they're compromised or no longer valid, and this option protects users from submitting confidential data to a site that may be fraudulent or not secure. If you enable this policy setting, Internet Explorer will check to see if server certificates have been revoked. If you disable this policy setting, Internet Explorer won't check server certificates to see if they've been revoked. If you don't configure this policy setting, Internet Explorer won't check server certificates to see if they've been revoked.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-checkservercertificaterevocation)

  **Default**: Enabled

- **Internet Explorer internet zone less privileged sites**:  
  This policy setting allows you to manage whether Web sites from less privileged zones, such as Restricted Sites, can navigate into this zone. If you enable this policy setting, Web sites from less privileged zones can open new windows in, or navigate into, this zone. The security zone will run without the added layer of security that is provided by the Protection from Zone Elevation security feature. If you select Prompt in the drop-down box, a warning is issued to the user that potentially risky navigation is about to occur. If you disable this policy setting, possibly harmful navigation is prevented. The Internet Explorer security feature is on in this zone as set by Protection from Zone Elevation feature control. If you don't configure this policy setting, Web sites from less privileged zones can open new windows in, or navigate into, this zone.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-internetzoneallowlessprivilegedsites)

  **Default**: Disable

- **Internet Explorer restricted zone file downloads**:  
  This policy setting allows you to manage whether file downloads are permitted from the zone. This option gets determined by the zone of the page with the link causing the download, not the zone from which the file is delivered. If you enable this policy setting, files can be downloaded from the zone. If you disable this policy setting, files are prevented from being downloaded from the zone. If you don't configure this policy setting, files are prevented from being downloaded from the zone.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-restrictedsiteszoneallowfiledownloads)

  **Default**: Disable

- **Internet Explorer internet zone run .NET Framework reliant components signed with Authenticode**:  
  This policy setting allows you to manage whether .NET Framework components that are signed with Authenticode can be executed from Internet Explorer. These components include managed controls referenced from an object tag and managed executables referenced from a link. If you enable this policy setting, Internet Explorer will execute signed managed components. If you select Prompt in the drop-down box, Internet Explorer will prompt the user to determine whether to execute signed managed components. If you disable this policy setting, Internet Explorer won't execute signed managed components. If you don't configure this policy setting, Internet Explorer won't execute signed managed components.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-internetzonerunnetframeworkreliantcomponentssignedwithauthenticode)

  **Default**: Disable

- **Internet Explorer prevent per user installation of Active X controls**:  
  This policy setting allows you to prevent the installation of ActiveX controls on a per-user basis. If you enable this policy setting, ActiveX controls can't be installed on a per-user basis. If you disable or don't configure this policy setting, ActiveX controls can be installed on a per-user basis.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-preventperuserinstallationofactivexcontrols)

  **Default**: Enabled

- **Internet Explorer prevent managing smart screen filter**:  
  This policy setting prevents the user from managing SmartScreen Filter, which warns the user if the website they visit is known for fraudulent attempts to gather personal information through "phishing," or is known to host malware. If you enable this policy setting, the user isn't prompted to turn on SmartScreen Filter. All website addresses that aren't on the filters allowlist are sent automatically to Microsoft without prompting the user. If you disable or don't configure this policy setting, the user gets prompted to decide whether to turn on SmartScreen Filter during the first-run experience.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-preventmanagingsmartscreenfilter)

  **Default**: Enable

- **Internet Explorer processes MIME sniffing safety feature**:  
  This policy setting determines whether Internet Explorer MIME sniffing will prevent promotion of a file of one type to a more dangerous file type. If you enable this policy setting, MIME sniffing will never promote a file of one type to a more dangerous file type. If you disable this policy setting, Internet Explorer processes will allow a MIME sniff promoting a file of one type to a more dangerous file type. If you don't configure this policy setting, MIME sniffing will never promote a file of one type to a more dangerous file type.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-mimesniffingsafetyfeatureinternetexplorerprocesses)

  **Default**: Enabled

- **Internet Explorer restricted zone download signed Active X controls**:  
  This policy setting allows you to manage whether users may download signed ActiveX controls from a page in the zone. If you enable this policy, users can download signed controls without user intervention. If you select Prompt in the drop-down box, users are queried whether to download controls signed by publishers who aren't trusted. Code signed by trusted publishers is silently downloaded. If you disable the policy setting, signed controls can't download. If you don't configure this policy setting, users are queried whether to download controls signed by publishers who aren't trusted. Code signed by trusted publishers is silently downloaded.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-restrictedsiteszonedownloadsignedactivexcontrols)

  **Default**: Disable

- **Internet Explorer auto complete**:  
  This Auto-Complete feature can remember and suggest User names and passwords on Forms. If you enable this setting, the user can't change "User name and passwords on forms" or "prompt me to save passwords". The Auto Complete feature for User names and passwords on Forms is turned on. Decide whether to select "prompt me to save passwords". If you disable this setting the user can't change "User name and passwords on forms" or "prompt me to save passwords". The Auto Complete feature for User names and passwords on Forms is turned off. The user also can't opt to be prompted to save passwords. If you don't configure this setting, the user has the freedom of turning on Auto complete for User name and passwords on forms and the option of prompting to save passwords. To display this option, the users open the Internet Options dialog box, click the Contents Tab, and click the Settings button.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-allowautocomplete)

  **Default**: Disabled

- **Internet Explorer internet zone allow VBscript to run**:  
  This policy setting lets you decide whether VBScript can run on pages in specific Internet Explorer zones. Options include:

  - *Enable* - VBScript runs on pages in specific zones, without any interaction.

  - *Prompt* - Employees are prompted whether to allow VBScript to run in the zone.

  - *Disable* - VBScript is prevented from running in the zone. If you disable or don't configure this policy setting, VBScript runs without any interaction in the specified zone.

  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-internetzoneallowvbscripttorunininternetexplorer)

  **Default**: Disable

- **Internet Explorer restricted zone allow only approved domains to use tdc Active X controls**:  
  This policy setting controls if the user can run the TDC ActiveX control on websites. If you enable this policy setting, the TDC ActiveX control won't run from websites in this zone. If you disable this policy setting, the TDC Active X control will run from all sites in this zone.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-restrictedsiteszoneallowonlyapproveddomainstousetdcactivexcontrol)

  **Default**: Enabled

- **Internet Explorer trusted zone do not run antimalware against Active X controls**:  
  This policy setting determines whether Internet Explorer runs antimalware programs against ActiveX controls, to check if they're safe to load on pages. If you enable this policy setting, Internet Explorer won't check with your antimalware program to see if it's safe to create an instance of the ActiveX control. If you disable this policy setting, Internet Explorer always checks with your antimalware program to see if it's safe to create an instance of the ActiveX control. If you don't configure this policy setting, Internet Explorer always checks with your antimalware program to see if it's safe to create an instance of the ActiveX control. Users can turn this behavior on or off, using Internet Explorer Security settings.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-trustedsiteszonedonotrunantimalwareagainstactivexcontrols)

  **Default**: Disabled

- **Internet Explorer local machine zone java permissions**:  
  This policy setting allows you to manage permissions for Java applets. If you enable this policy setting, you can choose options from the drop-down box. Custom, to control permissions settings individually. Low Safety enables applets to do all operations. Medium Safety enables applets to run in their sandbox (an area in memory outside of which the program can't make calls), plus capabilities like scratch space (a safe and secure storage area on the client computer) and user-controlled file I/O. High Safety enables applets to run in their sandbox. Disable Java to prevent any applets from running. If you disable this policy setting, Java applets can't run. If you don't configure this policy setting, the permission is set to Medium Safety.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-localmachinezonejavapermissions)

  **Default**: Disable java

- **Internet Explorer intranet zone do not run antimalware against Active X controls**:  
  This policy setting determines whether Internet Explorer runs antimalware programs against ActiveX controls, to check if they're safe to load on pages. If you enable this policy setting, Internet Explorer won't check with your antimalware program to see if it's safe to create an instance of the ActiveX control. If you disable this policy setting, Internet Explorer always checks with your antimalware program to see if it's safe to create an instance of the ActiveX control. If you don't configure this policy setting, Internet Explorer won't check with your antimalware program to see if it's safe to create an instance of the ActiveX control. Users can turn this behavior on or off, using Internet Explorer Security settings.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-intranetzonedonotrunantimalwareagainstactivexcontrols)

  **Default**: Disabled

- **Internet Explorer restricted zone scriptlets**:  
  This policy setting allows you to manage whether the user can run scriptlets. If you enable this policy setting, the user can run scriptlets. If you disable this policy setting, the user can't run scriptlets. If you don't configure this policy setting, the user can enable or disable scriptlets.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-restrictedsiteszoneallowscriptlets)

  **Default**: Disabled

- **Internet Explorer processes notification bar**:  
  This policy setting allows you to manage whether the Notification bar displays for Internet Explorer processes when file or code installs are restricted. By default, the Notification bar displays for Internet Explorer processes. If you enable this policy setting, the Notification bar displays for the Internet Explorer Processes. If you disable this policy setting, the Notification bar won't be displayed for Internet Explorer processes. If you don't configure this policy setting, the Notification bar doesn't display for Internet Explorer Processes.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-notificationbarinternetexplorerprocesses)

  **Default**: Enabled

- **Internet Explorer internet zone download signed ActiveX controls**:  
  This policy setting allows you to manage whether users may download signed ActiveX controls from a page in the zone. If you enable this policy, users can download signed controls without user intervention. If you select Prompt in the drop-down box, users are queried whether to download controls signed by publishers who aren't trusted. Code signed by trusted publishers is silently downloaded. If you disable the policy setting, signed controls can't download. If you don't configure this policy setting, users are queried whether to download controls signed by publishers who aren't trusted. Code signed by trusted publishers is silently downloaded.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-internetzonedownloadsignedactivexcontrols)

  **Default**: Disable

- **Internet Explorer restricted zone smart screen**:  
  This policy setting controls whether SmartScreen Filter scans pages in this zone for malicious content. If you enable this policy setting, SmartScreen Filter scans pages in this zone for malicious content. If you disable this policy setting, SmartScreen Filter doesn't scan pages in this zone for malicious content. If you don't configure this policy setting, the user can choose whether SmartScreen Filter scans pages in this zone for malicious content. Note: In Internet Explorer 7, this policy setting controls whether Phishing Filter scans pages in this zone for malicious content.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-restrictedsiteszoneallowsmartscreenie)

  **Default**: Enabled

- **Internet Explorer remove run this time button for outdated Active X controls**:  
  This policy setting allows you to stop users from seeing the "Run this time" button and from running specific outdated ActiveX controls in Internet Explorer. If you enable this policy setting, users won't see the "Run this time" button on the warning message that appears when Internet Explorer blocks an outdated ActiveX control. If you disable or don't configure this policy setting, users will see the "Run this time" button on the warning message that appears when Internet Explorer blocks an outdated ActiveX control. Clicking this button lets the user run the outdated ActiveX control once. For more information, see "Outdated ActiveX Controls" in the Internet Explorer TechNet library.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-removerunthistimebuttonforoutdatedactivexcontrols)

  **Default**: Enabled

- **Internet Explorer internet zone launch applications and files in an iframe**:  
  This policy setting allows you to manage whether applications can run and if files can download from an IFRAME reference in the HTML of the pages in this zone. If you enable this policy setting, users can run applications and download files from IFRAMEs on the pages in this zone without user intervention. If you select Prompt in the drop-down box, users are queried to choose whether to run applications and download files from IFRAMEs on the pages in this zone. If you disable this policy setting, users can't run applications and download files from IFRAMEs on the pages in this zone. If you don't configure this policy setting, users are queried to choose whether to run applications and download files from IFRAMEs on the pages in this zone.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-internetzonelaunchingapplicationsandfilesiniframe)

  **Default**: Disable

- **Internet Explorer restricted zone navigate windows and frames across different domains**:  
  This policy setting allows you to set options for dragging content from one domain to a different domain when the source and destination are in different windows. If you enable this policy setting and click Enable, users can drag content from one domain to a different domain when the source and destination are in different windows. Users can't change this setting. If you enable this policy setting and click Disable, users can't drag content from one domain to a different domain when both the source and destination are in different windows. Users can't change this setting. In Internet Explorer 10, if you disable this policy setting or don't configure it, users can't drag content from one domain to a different domain when the source and destination are in different windows. Users can change this setting in the Internet Options dialog. In Internet Explorer 9 and earlier versions, if you disable this policy or don't configure it, users can drag content from one domain to a different domain when the source and destination are in different windows. Users can't change this setting.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-restrictedsiteszoneenabledraggingofcontentfromdifferentdomainsacrosswindows)

  **Default**: Disable

- **Internet Explorer internet zone smart screen**:  
  This policy setting controls whether SmartScreen Filter scans pages in this zone for malicious content. If you enable this policy setting, SmartScreen Filter scans pages in this zone for malicious content. If you disable this policy setting, SmartScreen Filter doesn't scan pages in this zone for malicious content. If you don't configure this policy setting, the user can choose whether SmartScreen Filter scans pages in this zone for malicious content. Note: In Internet Explorer 7, this policy setting controls whether Phishing Filter scans pages in this zone for malicious content.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-internetzoneallowsmartscreenie)

  **Default**: Enabled

- **Internet Explorer locked down trusted zone java permissions**:  
  This policy setting allows you to manage permissions for Java applets. If you enable this policy setting, you can choose options from the drop-down box. Custom, to control permissions settings individually. Low Safety enables applets to do all operations. Medium Safety enables applets to run in their sandbox (an area in memory outside of which the program can't make calls), plus capabilities like scratch space (a safe and secure storage area on the client computer) and user-controlled file I/O. High Safety enables applets to run in their sandbox. Disable Java to prevent any applets from running. If you disable this policy setting, Java applets can't run. If you don't configure this policy setting, Java applets are disabled.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-lockeddowntrustedsiteszonejavapermissions)

  **Default**: Disable java

- **Internet Explorer check signatures on downloaded programs**:  
  This policy setting allows you to manage whether Internet Explorer checks for digital signatures (which identifies the publisher of signed software and verifies it hasn't been modified or tampered with) on user computers before downloading executable programs. If you enable this policy setting, Internet Explorer will check the digital signatures of executable programs and display their identities before downloading them to user computers. If you disable this policy setting, Internet Explorer won't check the digital signatures of executable programs or display their identities before downloading them to user computers. If you don't configure this policy, Internet Explorer won't check the digital signatures of executable programs or display their identities before downloading them to user computers.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-checksignaturesondownloadedprograms)

  **Default**: Enabled

- **Internet Explorer restricted zone scripting of web browser controls**:  
  This policy setting determines whether a page can control embedded WebBrowser controls via script. If you enable this policy setting, script access to the WebBrowser control is allowed. If you disable this policy setting, script access to the WebBrowser control isn't allowed. If you don't configure this policy setting, the user can enable or disable script access to the WebBrowser control. By default, script access to the WebBrowser control is allowed only in the Local Machine and Intranet zones.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-restrictedsiteszoneallowscriptingofinternetexplorerwebbrowsercontrols)

  **Default**: Disabled

- **Internet Explorer restricted zone cross site scripting filter**:  
  This policy controls if the Cross-Site Scripting (XSS) Filter will detect and prevent cross-site script injections into websites in this zone. If you enable this policy setting, the XSS Filter is on for sites in this zone, and the XSS Filter attempts to block cross-site script injections. If you disable this policy setting, the XSS Filter is turned off for sites in this zone, and Internet Explorer permits cross-site script injections.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-restrictedsiteszoneenablecrosssitescriptingfilter)

  **Default**: Enabled

- **Internet Explorer restricted zone binary and script behaviors**:  
  This policy setting allows you to manage dynamic binary and script behaviors: components that encapsulate specific functionality for HTML elements to which they were attached. If you enable this policy setting, binary and script behaviors are available. If you select Administrator approved in the drop-down box, only behaviors listed in the Admin-approved Behaviors under Binary Behaviors Security Restriction policy are available. If you disable this policy setting, binary and script behaviors aren't available unless applications have implemented a custom security manager. If you don't configure this policy setting, binary and script behaviors aren't available unless applications have implemented a custom security manager.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-restrictedsiteszoneallowbinaryandscriptbehaviors)

  **Default**: Disable

- **Internet Explorer security settings check**:  
  This policy setting turns off the Security Settings Check feature, which checks Internet Explorer security settings to determine when the settings put Internet Explorer at risk. If you enable this policy setting, the feature is turned off. If you disable or don't configure this policy setting, the feature is turned on.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-disablesecuritysettingscheck)

  **Default**: Enabled

- **Internet Explorer internet zone security warning for potentially unsafe files**:  
  This policy setting controls if the "Open File - Security Warning" message appears when the user tries to open executable files or other potentially unsafe files (from an intranet file share by using File Explorer, for example). If you enable this policy setting and set the drop-down box to Enable, these files open without a security warning. If you set the drop-down box to Prompt, a security warning appears before the files open. If you disable this policy setting, these files don't open. If you don't configure this policy setting, the user can configure how the computer handles these files. By default, these files are blocked in the Restricted zone, enabled in the Intranet and Local Computer zones, and set to prompt in the Internet and Trusted zones.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-internetzoneshowsecuritywarningforpotentiallyunsafefiles)

  **Default**: Prompt

- **Internet Explorer intranet zone java permissions**:  
  This policy setting allows you to manage permissions for Java applets. If you enable this policy setting, you can choose options from the drop-down box. Custom, to control permissions settings individually. Low Safety enables applets to do all operations. Medium Safety enables applets to run in their sandbox (an area in memory outside of which the program can't make calls), plus capabilities like scratch space (a safe and secure storage area on the client computer) and user-controlled file I/O. High Safety enables applets to run in their sandbox. Disable Java to prevent any applets from running. If you disable this policy setting, Java applets can't run. If you don't configure this policy setting, the permission is set to Medium Safety.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-intranetzonejavapermissions)

  **Default**: High safety

- **Internet Explorer block outdated Active X controls**:  
  This policy setting determines whether Internet Explorer blocks specific outdated ActiveX controls. Outdated ActiveX controls are never blocked in the Intranet Zone. If you enable this policy setting, Internet Explorer stops blocking outdated ActiveX controls. If you disable or don't configure this policy setting, Internet Explorer continues to block specific outdated ActiveX controls. For more information, see "Outdated ActiveX Controls" in the Internet Explorer TechNet library.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-donotblockoutdatedactivexcontrols)

  **Default**: Enabled

- **Internet Explorer restricted zone popup blocker**:  
  This policy setting allows you to manage whether unwanted pop-up windows appear. Pop-up windows that are opened when the end user clicks a link aren't blocked. If you enable this policy setting, most unwanted pop-up windows are prevented from appearing. If you disable this policy setting, pop-up windows aren't prevented from appearing. If you don't configure this policy setting, most unwanted pop-up windows are prevented from appearing.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-restrictedsiteszoneusepopupblocker)

  **Default**: Enable

- **Internet Explorer processes MK protocol security restriction**:  
  The MK Protocol Security Restriction policy setting reduces attack surface area by preventing the MK protocol. Resources hosted on the MK protocol will fail. If you enable this policy setting, the MK Protocol is prevented for File Explorer and Internet Explorer, and resources hosted on the MK protocol will fail. If you disable this policy setting, applications can use the MK protocol API. Resources hosted on the MK protocol will work for the File Explorer and Internet Explorer processes. If you don't configure this policy setting, the MK Protocol is prevented for File Explorer and Internet Explorer, and resources hosted on the MK protocol will fail.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-mkprotocolsecurityrestrictioninternetexplorerprocesses)

  **Default**: Enabled

- **Internet Explorer trusted zone java permissions**:  
  This policy setting allows you to manage permissions for Java applets. If you enable this policy setting, you can choose options from the drop-down box. Custom, to control permissions settings individually. Low Safety enables applets to do all operations. Medium Safety enables applets to run in their sandbox (an area in memory outside of which the program can't make calls), plus capabilities like scratch space (a safe and secure storage area on the client computer) and user-controlled file I/O. High Safety enables applets to run in their sandbox. Disable Java to prevent any applets from running. If you disable this policy setting, Java applets can't run. If you don't configure this policy setting, the permission is set to Low Safety.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-trustedsiteszonejavapermissions)

  **Default**: High safety

- **Internet Explorer restricted zone scripting of java applets**:  
  This policy setting allows you to manage whether applets are exposed to scripts within the zone. If you enable this policy setting, scripts can access applets automatically without user intervention. If you select Prompt in the drop-down box, users are queried to choose whether to allow scripts to access applets. If you disable this policy setting, scripts are prevented from accessing applets. If you don't configure this policy setting, scripts are prevented from accessing applets.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-restrictedsiteszonescriptingofjavaapplets)

  **Default**: Disable

- **Internet Explorer locked down restricted zone java permissions**:  
  This policy setting allows you to manage permissions for Java applets. If you enable this policy setting, you can choose options from the drop-down box. Custom, to control permissions settings individually. Low Safety enables applets to do all operations. Medium Safety enables applets to run in their sandbox (an area in memory outside of which the program can't make calls), plus capabilities like scratch space (a safe and secure storage area on the client computer) and user-controlled file I/O. High Safety enables applets to run in their sandbox. Disable Java to prevent any applets from running. If you disable this policy setting, Java applets can't run. If you don't configure this policy setting, Java applets are disabled.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-lockeddownrestrictedsiteszonejavapermissions)

  **Default**: Disable java

- **Internet Explorer internet zone allow only approved domains to use ActiveX controls**:  
  This policy setting controls if the user is prompted to allow ActiveX controls to run on websites other than the website that installed the ActiveX control. If you enable this policy setting, the user is prompted before ActiveX controls can run from websites in this zone. The user can choose to allow the control to run from the current site or from all sites. If you disable this policy setting, the user doesn't see the per-site ActiveX prompt, and ActiveX controls can run from all sites in this zone.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-internetzoneallowonlyapproveddomainstouseactivexcontrols)

  **Default**: Enabled

- **Internet Explorer include all network paths**:  
  Internet Explorer include all network paths.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-includeallnetworkpaths)

  **Default**: Disabled

- **Internet Explorer internet zone protected mode**:  
  This policy setting allows you to turn on Protected Mode. Protected Mode helps protect Internet Explorer from exploited vulnerabilities by reducing the locations that Internet Explorer can write to in the registry and the file system. If you enable this policy setting, Protected Mode is turned on. The user can't turn off Protected Mode. If you disable this policy setting, Protected Mode is turned off. The user can't turn on Protected Mode. If you don't configure this policy setting, the user can turn on or turn off Protected Mode.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-internetzoneenableprotectedmode)

  **Default**: Enable

- **Internet Explorer internet zone initialize and script Active X controls not marked as safe**:  
  This policy setting allows you to manage ActiveX controls not marked as safe. If you enable this policy setting, ActiveX controls run, loaded with parameters, and scripted without setting object safety for untrusted data or scripts. This setting isn't recommended, except for secure and administered zones. This setting causes both unsafe and safe controls to be initialized and scripted, ignoring the Script ActiveX controls marked safe for scripting option. If you enable this policy setting and select Prompt in the drop-down box, users are queried whether to allow the control to load with parameters or scripted. If you disable this policy setting, ActiveX controls that can't be made safe aren't loaded with parameters or scripted. If you don't configure this policy setting, ActiveX controls that can't be made safe aren't loaded with parameters or scripted.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-internetzoneinitializeandscriptactivexcontrolsnotmarkedsafe)

  **Default**: Disable

- **Internet Explorer locked down restricted zone smart screen**:  
  This policy setting controls whether SmartScreen Filter scans pages in this zone for malicious content. If you enable this policy setting, SmartScreen Filter scans pages in this zone for malicious content. If you disable this policy setting, SmartScreen Filter doesn't scan pages in this zone for malicious content. If you don't configure this policy setting, the user can choose whether SmartScreen Filter scans pages in this zone for malicious content. Note: In Internet Explorer 7, this policy setting controls whether Phishing Filter scans pages in this zone for malicious content.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-restrictedsiteszoneallowsmartscreenie)

  **Default**: Enabled

- **Internet Explorer crash detection**:  
  This policy setting allows you to manage the crash detection feature of add-on Management. If you enable this policy setting, a crash in Internet Explorer will exhibit behavior found in Windows XP Professional Service Pack 1 and earlier, namely to invoke Windows Error Reporting. All policy settings for Windows Error Reporting continue to apply. If you disable or don't configure this policy setting, the crash detection feature for add-on management is functional.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-disablecrashdetection)

  **Default**: Disabled

- **Internet Explorer internet zone java permissions**:  
  This policy setting allows you to manage permissions for Java applets. If you enable this policy setting, you can choose options from the drop-down box. Custom, to control permissions settings individually. Low Safety enables applets to do all operations. Medium Safety enables applets to run in their sandbox (an area in memory outside of which the program can't make calls), plus capabilities like scratch space (a safe and secure storage area on the client computer) and user-controlled file I/O. High Safety enables applets to run in their sandbox. Disable Java to prevent any applets from running. If you disable this policy setting, Java applets can't run. If you don't configure this policy setting, the permission is set to High Safety.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-internetzonejavapermissions)

  **Default**: Disable java

- **Internet Explorer restricted zone active scripting**:  
  This policy setting allows you to manage whether script code on pages in the zone is run. If you enable this policy setting, script code on pages in the zone can run automatically. If you select Prompt in the drop-down box, users are queried to choose whether to allow script code on pages in the zone to run. If you disable this policy setting, script code on pages in the zone is prevented from running. If you don't configure this policy setting, script code on pages in the zone is prevented from running.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-restrictedsiteszoneallowactivescripting)

  **Default**: Disable

- **Internet Explorer internet zone logon options**:  
  This policy setting allows you to manage settings for sign-in options. If you enable this policy setting, you can choose from the following sign-in options. Anonymous log on to disable HTTP authentication and use the guest account only for the Common Internet File System (CIFS) protocol. Prompt for user name and password to query users for user IDs and passwords. After a user is queried, these values can be used silently for the remainder of the session. Automatic log on only in Intranet zone to query users for user IDs and passwords in other zones. After a user is queried, these values can be used silently for the rest of the session. Automatic sign in with current user name and password to attempt log on using Windows NT Challenge Response (also known as NTLM authentication). If the server supports Windows NT Challenge Response, the sign-in uses the user's network user name and password for log-on. If the server doesn't support Windows NT Challenge Response, the user is queried to provide the user name and password. If you disable this policy setting, sign-in is set to Automatic log on only in Intranet zone. If you don't configure this policy setting, sign-in is set to Automatic sign in only in Intranet zone.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-internetzonelogonoptions)

  **Default**: Prompt

- **Internet Explorer restricted zone allow VBScript to run**:  
  This policy setting allows you to manage whether VBScript can run on pages from the specified zone in Internet Explorer. If you selected Enable in the drop-down box, VBScript can run without user intervention. If you selected Prompt in the drop-down box, users are asked to choose whether to allow VBScript to run. If you selected Disable in the drop-down box, VBScript is prevented from running. If you don't configure or disable this policy setting, VBScript is prevented from running.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-restrictedsiteszoneallowvbscripttorunininternetexplorer)

  **Default**: Disable

- **Internet Explorer internet zone drag content from different domains across windows**:  
  This policy setting allows you to set options for dragging content from one domain to a different domain when the source and destination are in different windows. If you enable this policy setting and click Enable, users can drag content from one domain to a different domain when the source and destination are in different windows. Users can't change this setting. If you enable this policy setting and click Disable, users can't drag content from one domain to a different domain when both the source and destination are in different windows. Users can't change this setting. In Internet Explorer 10, if you disable this policy setting or don't configure it, users can't drag content from one domain to a different domain when the source and destination are in different windows. Users can change this setting in the Internet Options dialog. In Internet Explorer 9 and earlier versions, if you disable this policy or don't configure it, users can drag content from one domain to a different domain when the source and destination are in different windows. Users can't change this setting.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-internetzoneenabledraggingofcontentfromdifferentdomainsacrosswindows)

  **Default**: Disabled

- **Internet Explorer intranet zone initialize and script Active X controls not marked as safe**:  
  This policy setting allows you to manage ActiveX controls not marked as safe. If you enable this policy setting, ActiveX controls run, loaded with parameters, and scripted without setting object safety for untrusted data or scripts. This setting isn't recommended, except for secure and administered zones. This setting causes both unsafe and safe controls to be initialized and scripted, ignoring the Script ActiveX controls marked safe for scripting option. If you enable this policy setting and select Prompt in the drop-down box, users are queried whether to allow the control to load with parameters or scripted. If you disable this policy setting, ActiveX controls that can't be made safe aren't loaded with parameters or scripted. If you don't configure this policy setting, ActiveX controls that can't be made safe aren't loaded with parameters or scripted.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-intranetzoneinitializeandscriptactivexcontrols)

  **Default**: Disable

- **Internet Explorer download enclosures**:  
  This policy setting prevents the user from having enclosures (file attachments) downloaded from a feed to the user's computer. If you enable this policy setting, the user can't set the Feed Sync Engine to download an enclosure through the Feed property page. A developer can't change the download setting through the Feed APIs. If you disable or don't configure this policy setting, the user can set the Feed Sync Engine to download an enclosure through the Feed property page. A developer can change the download setting through the Feed APIs.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-disableenclosuredownloading)

  **Default**: Disabled

- **Internet Explorer restricted zone download unsigned Active X controls**:  
  This policy setting allows you to manage whether users may download unsigned ActiveX controls from the zone. Such code is potentially harmful, especially when coming from an untrusted zone. If you enable this policy setting, users can run unsigned controls without user intervention. If you select Prompt in the drop-down box, users are queried to choose whether to allow the unsigned control to run. If you disable this policy setting, users can't run unsigned controls. If you don't configure this policy setting, users can't run unsigned controls.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-restrictedsiteszonedownloadunsignedactivexcontrols)

  **Default**: Disable

- **Internet Explorer internet zone drag content from different domains within windows**:  
  This policy setting allows you to manage whether users may download unsigned ActiveX controls from the zone. Such code is potentially harmful, especially when coming from an untrusted zone. If you enable this policy setting, users can run unsigned controls without user intervention. If you select Prompt in the drop-down box, users are queried to choose whether to allow the unsigned control to run. If you disable this policy setting, users can't run unsigned controls. If you don't configure this policy setting, users can't run unsigned controls.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-internetzoneenabledraggingofcontentfromdifferentdomainswithinwindows)

  **Default**: Disabled

- **Internet Explorer processes restrict Active X install**:  
  This policy setting enables applications hosting the Web Browser Control to block automatic prompting of ActiveX control installation. If you enable this policy setting, the Web Browser Control will block automatic prompting of ActiveX control installation for all processes. If you disable or don't configure this policy setting, the Web Browser Control won't block automatic prompting of ActiveX control installation for all processes.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-restrictactivexinstallinternetexplorerprocesses)

  **Default**: Enabled

- **Internet Explorer internet zone scriptlets**:  
  This policy setting allows you to manage whether the user can run scriptlets. If you enable this policy setting, the user can run scriptlets. If you disable this policy setting, the user can't run scriptlets. If you don't configure this policy setting, the user can enable or disable scriptlets.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-internetzoneallowscriptlets)

  **Default**: Disable

- **Internet Explorer restricted zone drag and drop or copy and paste files**:  
  This policy setting allows you to manage whether users can drag files or copy and paste files from a source within the zone. If you enable this policy setting, users can drag files or copy and paste files from this zone automatically. If you select Prompt in the drop-down box, users are queried to choose whether to drag or copy files from this zone. If you disable this policy setting, users are prevented from dragging files or copying and pasting files from this zone. If you don't configure this policy setting, users are queried to choose whether to drag or copy files from this zone.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-restrictedsiteszoneallowdraganddropcopyandpastefiles)

  **Default**: Disable

- **Internet Explorer software when signature is invalid**:  
  This policy setting allows you to manage whether software, such as ActiveX controls and file downloads, can be installed or run by the user even though the signature is invalid. An invalid signature might indicate that someone has tampered with the file. If you enable this policy setting, users are prompted to install or run files with an invalid signature. If you disable this policy setting, users can't run or install files with an invalid signature. If you don't configure this policy, users can choose to run or install files with an invalid signature.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-allowsoftwarewhensignatureisinvalid)

  **Default**: Disabled

- **Internet Explorer restricted zone copy and paste via script**:  
  This policy setting allows you to manage whether scripts can do a clipboard operation (for example, cut, copy, and paste) in a specified region. If you enable this policy setting, a script can do a clipboard operation. If you select Prompt in the drop-down box, users are queried as to whether to do clipboard operations. If you disable this policy setting, a script can't do a clipboard operation. If you don't configure this policy setting, a script can't do a clipboard operation.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-restrictedsiteszoneallowcopypasteviascript)

  **Default**: Disable

- **Internet Explorer restricted zone drag content from different domains across windows**:  
  This policy setting allows you to set options for dragging content from one domain to a different domain when the source and destination are in different windows. If you enable this policy setting and click Enable, users can drag content from one domain to a different domain when the source and destination are in different windows. Users can't change this setting. If you enable this policy setting and click Disable, users can't drag content from one domain to a different domain when both the source and destination are in different windows. Users can't change this setting. In Internet Explorer 10, if you disable this policy setting or don't configure it, users can't drag content from one domain to a different domain when the source and destination are in different windows. Users can change this setting in the Internet Options dialog. In Internet Explorer 9 and earlier versions, if you disable this policy or don't configure it, users can drag content from one domain to a different domain when the source and destination are in different windows. Users can't change this setting.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-restrictedsiteszoneenabledraggingofcontentfromdifferentdomainsacrosswindows)

  **Default**: Disabled

- **Internet Explorer users adding sites**:  
  Prevents users from adding or removing sites from security zones. A security zone is a group of Web sites with the same security level. If you enable this policy, the site management settings for security zones are disabled. (To see the site management settings for security zones, in the Internet Options dialog box, click the Security tab, and then click the Sites button.) If you disable this policy or don't configure it, users can add Web sites to or remove sites from the Trusted Sites and Restricted Sites zones, and alter settings for the Local Intranet zone. This policy prevents users from changing site management settings for security zones established by the administrator. Note: The "Disable the Security page" policy (located in \User Configuration\Administrative Templates\Windows Components\Internet Explorer\Internet Control Panel), which removes the Security tab from the interface, takes precedence over this policy. If it's enabled, this policy is ignored. Also, see the "Security zones: Use only machine settings" policy.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-donotallowuserstoaddsites)

  **Default**: Disabled

- **Internet Explorer internet zone script initiated windows**:  
  This policy setting allows you to manage restrictions on script-initiated pop-up windows and windows that include the title and status bars. If you enable this policy setting, Windows Restrictions security won't apply in this zone. The security zone runs without the added layer of security provided by this feature. If you disable this policy setting, the possible harmful actions contained in script-initiated pop-up windows and windows that include the title and status bars can't run. This Internet Explorer security feature is on in this zone as dictated by the Scripted Windows Security Restrictions feature control setting for the process. If you don't configure this policy setting, the possible harmful actions contained in script-initiated pop-up windows and windows that include the title and status bars can't run. This Internet Explorer security feature is on in this zone as dictated by the Scripted Windows Security Restrictions feature control setting for the process.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-internetzoneallowscriptinitiatedwindows)

  **Default**: Disabled

- **Internet Explorer security zones use only machine settings**:  
  Applies security zone information to all users of the same computer. A security zone is a group of Web sites with the same security level. If you enable this policy, changes that the user makes to a security zone will apply to all users of that computer. If you disable this policy or don't configure it, users of the same computer can establish their own security zone settings. Use this policy to ensure that security zone settings apply uniformly to the same computer and don't vary from user to user. Also, see the "Security zones: don't allow users to change policies" policy.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-securityzonesuseonlymachinesettings)

  **Default**: Enabled

- **Internet Explorer locked down local machine zone java permissions**:  
  This policy setting allows you to manage permissions for Java applets. If you enable this policy setting, you can choose options from the drop-down box. Custom, to control permissions settings individually. Low Safety enables applets to do all operations. Medium Safety enables applets to run in their sandbox (an area in memory outside of which the program can't make calls), plus capabilities like scratch space (a safe and secure storage area on the client computer) and user-controlled file I/O. High Safety enables applets to run in their sandbox. Disable Java to prevent any applets from running. If you disable this policy setting, Java applets can't run. If you don't configure this policy setting, Java applets are disabled.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-lockeddownlocalmachinezonejavapermissions)

  **Default**: Disable java

- **Internet Explorer restricted zone do not run antimalware against Active X controls**:  
  This policy setting determines whether Internet Explorer runs antimalware programs against ActiveX controls, to check if they're safe to load on pages. If you enable this policy setting, Internet Explorer won't check with your antimalware program to see if it's safe to create an instance of the ActiveX control. If you disable this policy setting, Internet Explorer always checks with your antimalware program to see if it's safe to create an instance of the ActiveX control. If you don't configure this policy setting, Internet Explorer always checks with your antimalware program to see if it's safe to create an instance of the ActiveX control. Users can turn this behavior on or off, using Internet Explorer Security settings.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-restrictedsiteszonedonotrunantimalwareagainstactivexcontrols)

  **Default**: Disabled

- **Internet Explorer restricted zone run .NET Framework reliant components signed with Authenticode**:  
  This policy setting allows you to manage whether .NET Framework components that are signed with Authenticode can be executed from Internet Explorer. These components include managed controls referenced from an object tag and managed executables referenced from a link. If you enable this policy setting, Internet Explorer will execute signed managed components. If you select Prompt in the drop-down box, Internet Explorer will prompt the user to determine whether to execute signed managed components. If you disable this policy setting, Internet Explorer won't execute signed managed components. If you don't configure this policy setting, Internet Explorer won't execute signed managed components.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-restrictedsiteszonerunnetframeworkreliantcomponentssignedwithauthenticode)

  **Default**: Disable

- **Internet Explorer restricted zone access to data sources**:  
  This policy setting allows you to manage whether Internet Explorer can access data from another security zone using the Microsoft XML Parser (MSXML) or ActiveX Data Objects (ADO). If you enable this policy setting, users can load a page in the zone that uses MSXML or ADO to access data from another site in the zone. If you select Prompt in the drop-down box, users are queried to choose whether to allow a page to load in the zone that uses MSXML or ADO to access data from another site in the zone. If you disable this policy setting, users can't load a page in the zone that uses MSXML or ADO to access data from another site in the zone. If you don't configure this policy setting, users can't load a page in the zone that uses MSXML or ADO to access data from another site in the zone.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-restrictedsiteszoneallowaccesstodatasources)

  **Default**: Disable

- **Internet Explorer internet zone don't run antimalware against ActiveX controls**:  
  This policy setting determines whether Internet Explorer runs antimalware programs against ActiveX controls, to check if they're safe to load on pages. If you enable this policy setting, Internet Explorer won't check with your antimalware program to see if it's safe to create an instance of the ActiveX control. If you disable this policy setting, Internet Explorer always checks with your antimalware program to see if it's safe to create an instance of the ActiveX control. If you don't configure this policy setting, Internet Explorer always checks with your antimalware program to see if it's safe to create an instance of the ActiveX control. Users can turn this behavior on or off, using Internet Explorer Security settings.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-internetzonedonotrunantimalwareagainstactivexcontrols)

  **Default**: Disabled

- **Internet Explorer internet zone copy and paste via script**:  
  This policy setting allows you to manage whether scripts can do a clipboard operation (for example, cut, copy, and paste) in a specified region. If you enable this policy setting, a script can do a clipboard operation. If you select Prompt in the drop-down box, users are queried as to whether to do clipboard operations. If you disable this policy setting, a script can't do a clipboard operation. If you don't configure this policy setting, a script can do a clipboard operation.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-internetzoneallowcopypasteviascript)

  **Default**: Disable

- **Internet Explorer use Active X installer service**:  
  This policy setting allows you to specify how ActiveX controls are installed. If you enable this policy setting, ActiveX controls are installed only if the ActiveX Installer Service is present and has been configured to allow the installation of ActiveX controls. If you disable or don't configure this policy setting, ActiveX controls, including per-user controls, are installed through the standard installation process.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-specifyuseofactivexinstallerservice)

  **Default**: Enabled

- **Internet Explorer processes protection from zone elevation**:  
  Internet Explorer places restrictions on each Web page it opens. The restrictions are dependent upon the location of the Web page (Internet, Intranet, Local Machine zone, and so on). For example, Web pages on the local computer have the fewest security restrictions and are in the Local Machine zone, making the Local Machine security zone a prime target for malicious users. If you enable this policy setting, any zone can be protected from zone elevation for all processes. If you disable or don't configure this policy setting, processes other than Internet Explorer or those listed in the Process List receive no such protection.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-protectionfromzoneelevationinternetexplorerprocesses)

  **Default**: Enabled

- **Internet Explorer internet zone download unsigned ActiveX controls**:  
  This policy setting allows you to manage whether users may download unsigned ActiveX controls from the zone. Such code is potentially harmful, especially when coming from an untrusted zone. If you enable this policy setting, users can run unsigned controls without user intervention. If you select Prompt in the drop-down box, users are queried to choose whether to allow the unsigned control to run. If you disable this policy setting, users can't run unsigned controls. If you don't configure this policy setting, users can't run unsigned controls.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-internetzonedownloadunsignedactivexcontrols)

  **Default**: Disable

- **Internet Explorer internet zone navigate windows and frames across different domains**:  
  This policy setting allows you to manage the opening of windows and frames and access of applications across different domains. If you enable this policy setting, users can open windows and frames from other domains and access applications from other domains. If you select Prompt in the drop-down box, users are queried whether to allow windows and frames to access applications from other domains. If you disable this policy setting, users can't open windows and frames to access applications from different domains. If you don't configure this policy setting, users can open windows and frames from other domains and access applications from other domains.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-internetzoneenabledraggingofcontentfromdifferentdomainsacrosswindows)

  **Default**: Disable

- **Internet Explorer internet zone updates to status bar via script**:  
  This policy setting allows you to manage whether a script can update the status bar within the zone. If you enable this policy setting, scripts can update the status bar. If you disable or don't configure this policy setting, script isn't allowed to update the status bar.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-internetzoneallowupdatestostatusbarviascript)

  **Default**: Disabled

- **Internet Explorer restricted zone include local path when uploading files to server**:  
  This policy setting controls if local path information is sent when the user is uploading a file via an HTML form. If the local path information is sent, some information may be unintentionally revealed to the server. For instance, files sent from the user's desktop may contain the user name as a part of the path. If you enable this policy setting, path information is sent when the user is uploading a file via an HTML form. If you disable this policy setting, path information is removed when the user is uploading a file via an HTML form. If you don't configure this policy setting, the user can choose whether path information is sent when they're uploading a file via an HTML form. By default, path information is sent.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-restrictedsiteszoneincludelocalpathwhenuploadingfilestoserver)

  **Default**: Disabled

- **Internet Explorer processes restrict file download**:  
  This policy setting enables applications hosting the Web Browser Control to block automatic prompting of file downloads that aren't user initiated. If you enable this policy setting, the Web Browser Control will block automatic prompting of file downloads that aren't user initiated for all processes. If you disable this policy setting, the Web Browser Control won't block automatic prompting of file downloads that aren't user initiated for all processes.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-restrictfiledownloadinternetexplorerprocesses)

  **Default**: Enabled

- **Internet Explorer restricted zone allow only approved domains to use Active X controls**:  
  This policy setting controls if the user is prompted to allow ActiveX controls to run on websites other than the website that installed the ActiveX control. If you enable this policy setting, the user is prompted before ActiveX controls can run from websites in this zone. The user can choose to allow the control to run from the current site or from all sites. If you disable this policy setting, the user doesn't see the per-site ActiveX prompt, and ActiveX controls can run from all sites in this zone.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-restrictedsiteszoneallowonlyapproveddomainstouseactivexcontrols)

  **Default**: Enabled

- **Internet Explorer restricted zone initialize and script Active X controls not marked as safe**:  
  This policy setting allows you to manage ActiveX controls not marked as safe. If you enable this policy setting, ActiveX controls run, loaded with parameters, and scripted without setting object safety for untrusted data or scripts. This setting isn't recommended, except for secure and administered zones. This setting causes both unsafe and safe controls to be initialized and scripted, ignoring the Script ActiveX controls marked safe for scripting option. If you enable this policy setting and select Prompt in the drop-down box, users are queried whether to allow the control to load with parameters or scripted. If you disable this policy setting, ActiveX controls that can't be made safe aren't loaded with parameters or scripted. If you don't configure this policy setting, ActiveX controls that can't be made safe aren't loaded with parameters or scripted.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-restrictedsiteszoneinitializeandscriptactivexcontrols)

  **Default**: Disable

- **Internet Explorer users changing policies**:  
  Prevents users from changing security zone settings. A security zone is a group of Web sites with the same security level. If you enable this policy, the Custom Level button and security-level slider on the Security tab in the Internet Options dialog box are disabled. If you disable this policy or don't configure it, users can change the settings for security zones. This policy prevents users from changing security zone settings established by the administrator. Note: The "Disable the Security page" policy (located in \User Configuration\Administrative Templates\Windows Components\Internet Explorer\Internet Control Panel), which removes the Security tab from Internet Explorer in Control Panel, takes precedence over this policy. If it's enabled, this policy is ignored. Also, see the "Security zones: Use only machine settings" policy.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-donotallowuserstochangepolicies)

  **Default**: Disabled

- **Internet Explorer restricted zone protected mode**:  
  This policy setting allows you to turn on Protected Mode. Protected Mode helps protect Internet Explorer from exploited vulnerabilities by reducing the locations that Internet Explorer can write to in the registry and the file system. If you enable this policy setting, Protected Mode is turned on. The user can't turn off Protected Mode. If you disable this policy setting, Protected Mode is turned off. The user can't turn on Protected Mode. If you don't configure this policy setting, the user can turn on or turn off Protected Mode.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-restrictedsiteszoneturnonprotectedmode)

  **Default**: Enable

- **Internet Explorer internet zone user data persistence**:  
  This policy setting allows you to manage the preservation of information in the browser's history, in favorites, in an XML store, or directly within a Web page saved to disk. When a user returns to a persisted page, the state of the page can be restored if this policy setting is appropriately configured. If you enable this policy setting, users can preserve information in the browser's history, in favorites, in an XML store, or directly within a Web page saved to disk. If you disable this policy setting, users can't preserve information in the browser's history, in favorites, in an XML store, or directly within a Web page saved to disk. If you don't configure this policy setting, users can preserve information in the browser's history, in favorites, in an XML store, or directly within a Web page saved to disk.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-internetzoneallowuserdatapersistence)

  **Default**: Disabled

- **Internet Explorer internet zone scripting of web browser controls**:  
  This policy setting determines whether a page can control embedded WebBrowser controls via script. If you enable this policy setting, script access to the WebBrowser control is allowed. If you disable this policy setting, script access to the WebBrowser control isn't allowed. If you don't configure this policy setting, the user can enable or disable script access to the WebBrowser control. By default, script access to the WebBrowser control is allowed only in the Local Machine and Intranet zones.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-internetzoneallowscriptingofinternetexplorerwebbrowsercontrols)

  **Default**: Disabled

- **Internet Explorer restricted zone user data persistence**:  
  This policy setting allows you to manage the preservation of information in the browser's history, in favorites, in an XML store, or directly within a Web page saved to disk. When a user returns to a persisted page, the state of the page can be restored if this policy setting is appropriately configured. If you enable this policy setting, users can preserve information in the browser's history, in favorites, in an XML store, or directly within a Web page saved to disk. If you disable this policy setting, users can't preserve information in the browser's history, in favorites, in an XML store, or directly within a Web page saved to disk. If you don't configure this policy setting, users can't preserve information in the browser's history, in favorites, in an XML store, or directly within a Web page saved to disk.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-restrictedsiteszoneallowuserdatapersistence)

  **Default**: Disabled

- **Internet Explorer locked down intranet zone java permissions**:  
  This policy setting allows you to manage permissions for Java applets. If you enable this policy setting, you can choose options from the drop-down box. Custom, to control permissions settings individually. Low Safety enables applets to do all operations. Medium Safety enables applets to run in their sandbox (an area in memory outside of which the program can't make calls), plus capabilities like scratch space (a safe and secure storage area on the client computer) and user-controlled file I/O. High Safety enables applets to run in their sandbox. Disable Java to prevent any applets from running. If you disable this policy setting, Java applets can't run. If you don't configure this policy setting, Java applets are disabled.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-lockeddownintranetjavapermissions)

  **Default**: Disable java

- **Internet Explorer enhanced protected mode**:  
  Enhanced Protected Mode provides additional protection against malicious websites by using 64-bit processes on 64-bit versions of Windows. For computers running at least Windows 8, Enhanced Protected Mode also limits the locations Internet Explorer can read from in the registry and the file system. If you enable this policy setting, Enhanced Protected Mode is turned on. Any zone that has Protected Mode enabled will use Enhanced Protected Mode. Users can't disable Enhanced Protected Mode. If you disable this policy setting, Enhanced Protected Mode is turned off. Any zone that has Protected Mode enabled will use the version of Protected Mode introduced in Internet Explorer 7 for Windows Vista. If you don't configure this policy, users can turn on or turn off Enhanced Protected Mode on the Advanced tab of the Internet Options dialog.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-allowenhancedprotectedmode)

  **Default**: Enabled

- **Internet Explorer bypass smart screen warnings**:  
  This policy setting determines whether the user can bypass warnings from SmartScreen Filter. SmartScreen Filter warns the user about executable files that Internet Explorer users don't commonly download from the Internet. If you enable this policy setting, SmartScreen Filter warnings block the user. If you disable or don't configure this policy setting, the user can bypass SmartScreen Filter warnings.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-disablebypassofsmartscreenwarnings)

  **Default**: Disabled

- **Internet Explorer restricted zone meta refresh**:  
  This policy setting allows you to manage whether a user's browser can be redirected to another Web page if the author of the Web page uses the Meta Refresh setting (tag) to redirect browsers to another Web page. If you enable this policy setting, a user's browser that loads a page containing an active Meta Refresh setting can be redirected to another Web page. If you disable this policy setting, a user's browser that loads a page containing an active Meta Refresh setting can't be redirected to another Web page. If you don't configure this policy setting, a user's browser that loads a page containing an active Meta Refresh setting can't be redirected to another Web page.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-restrictedsiteszoneallowmetarefresh)

  **Default**: Disabled

## Local Policies Security Options

For more information, see [Policy CSP - LocalPoliciesSecurityOptions](/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions) in the Windows documentation.

- **Restrict anonymous access to named pipes and shares**:  
  When enabled, this security setting restricts anonymous access to shares and pipes to the settings for: (1) Named pipes that can be accessed anonymously (2) Shares that can be accessed anonymously.  
  [Learn more](/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions#localpoliciessecurityoptions-networkaccess-restrictanonymousaccesstonamedpipesandshares)

  **Default**: Yes

- **Minimum session security for NTLM SSP based servers**:  
  This security setting allows a server to require the negotiation of 128-bit encryption and NTLMv2 session security. These values are dependent on the LAN Manager Authentication Level security setting value. The options are: Require NTLMv2 session security: The connection will fail if message integrity isn't negotiated. Require 128-bit encryption. The connection will fail if strong encryption (128-bit) isn't negotiated.  
  [Learn more](/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions#localpoliciessecurityoptions-networksecurity-minimumsessionsecurityforntlmsspbasedservers)

  **Default**: Require NTLM V2 and 128 bit encryption

- **Minutes of lock screen inactivity until screen saver activates**:  
  Windows notices inactivity of a logon session, and if the amount of inactive time exceeds the inactivity limit, then the screen saver will run, locking the session.  
  [Learn more](/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions#localpoliciessecurityoptions-interactivelogon-machineinactivitylimit)

  **Default**: 15

- **Require client to always digitally sign communications**:  
  This security setting determines whether all secure channel traffic initiated by the domain member must be signed or encrypted. When a computer joins a domain, a computer account is created. After that, when the system starts, it uses the computer account password to create a secure channel with a domain controller for its domain. This secure channel is used to do operations such as NTLM pass through authentication, LSA SID/name Lookup and more. This setting determines if all secure channel traffic initiated by the domain member meets minimum security requirements. Specifically it determines whether all secure channel traffic started by the domain member must be signed or encrypted. If this policy is enabled, then the secure channel won't be established unless either signing or encryption of all secure channel traffic is negotiated. If this policy is disabled, then encryption and signing of all secure channel traffic is negotiated with the Domain Controller in which case the level of signing and encryption depends on the version of the Domain Controller and the settings of the following two policies: Domain member: Digitally encrypt secure channel data (when possible) Domain member: Digitally sign secure channel data (when possible).  
  [Learn more](/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions#localpoliciessecurityoptions-microsoftnetworkclient-digitallysigncommunicationsalways)

  **Default**: Yes

- **Authentication level**:  
  This security setting determines which challenge/response authentication protocol is used for network logons. This choice affects the level of authentication protocol used by clients, the level of session security negotiated, and the level of authentication accepted by servers as follows:

  - *Send LM and NTLM responses* - Clients use LM and NTLM authentication and never use NTLMv2 session security; domain controllers accept LM, NTLM, and NTLMv2 authentication.

  - *Send LM and NTLM - NTLMv2 if negotiated* - Clients use LM and NTLM authentication and use NTLMv2 session security if the server supports it. Domain controllers accept LM, NTLM, and NTLMv2 authentication.

  - *Send NTLM response only* - Clients use NTLM authentication only and use NTLMv2 session security if the server supports it; domain controllers accept LM, NTLM, and NTLMv2 authentication.

  - *Send NTLMv2 response only* - Clients use NTLMv2 authentication only and use NTLMv2 session security if the server supports it; domain controllers accept LM, NTLM, and NTLMv2 authentication.

  - *Send NTLMv2 response only. Refuse LM* - Clients use NTLMv2 authentication only and use NTLMv2 session security if the server supports it. Domain controllers refuse LM (accept only NTLM and NTLMv2 authentication).

  - *Send NTLMv2 response only. Refuse LM and NTLM* - Clients use NTLMv2 authentication only and use NTLMv2 session security if the server supports it. Domain controllers refuse LM and NTLM (accept only NTLMv2 authentication).

  [Learn more](/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions#localpoliciessecurityoptions-networksecurity-lanmanagerauthenticationlevel)

  **Default**: Send NTLMv2 response only. Refuse LM and NTLM

- **Prevent clients from sending unencrypted passwords to third party SMB servers**:  
  If this security setting is enabled, the Server Message Block (SMB) redirector can send plaintext passwords to non-Microsoft SMB servers that don't support password encryption during authentication. Sending unencrypted passwords is a security risk.  
  [Learn more](/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions#localpoliciessecurityoptions-microsoftnetworkclient-sendunencryptedpasswordtothirdpartysmbservers)

  **Default**: Yes

- **Require server digitally signing communications always**:  
  This security setting determines whether the SMB client attempts to negotiate SMB packet signing. The server message block (SMB) protocol provides the basis for Microsoft file and print sharing and many other networking operations, such as remote Windows administration. To prevent man-in-the-middle attacks that modify SMB packets in transit, the SMB protocol supports the digital signing of SMB packets. This policy setting determines whether the SMB client component attempts to negotiate SMB packet signing when it connects to an SMB server. If this setting is enabled, the Microsoft network client will ask the server to do SMB packet signing upon session setup. If packet signing has been enabled on the server, packet signing is negotiated. If this policy is disabled, the SMB client will never negotiate SMB packet signing.  
  [Learn more](/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions#localpoliciessecurityoptions-microsoftnetworkserver-digitallysigncommunicationsalways)

  **Default**: Yes

- **Administrator elevation prompt behavior**:  
  This policy setting controls the behavior of the elevation prompt for administrators. The options are:

  - *Elevate without prompting* - Allows privileged accounts to do an operation that requires elevation without requiring consent or credentials. Note: Use this option only in the most constrained environments.

  - *Prompt for credentials on the secure desktop* - When an operation requires elevation of privilege, the user is prompted on the secure desktop to enter a privileged user name and password. If the user enters valid credentials, the operation continues with the user's highest available privilege.

  - *Prompt for consent on the secure desktop* - When an operation requires elevation of privilege, the user is prompted on the secure desktop to select either Permit or Deny. If the user selects Permit, the operation continues with the user's highest available privilege.

  - *Prompt for credentials* - When an operation requires elevation of privilege, the user is prompted to enter an administrative user name and password. If the user enters valid credentials, the operation continues with the applicable privilege.

  - *Prompt for consent* - When an operation requires elevation of privilege, the user is prompted to select either Permit or Deny. If the user selects Permit, the operation continues with the user's highest available privilege.

  - *Prompt for consent for non-Windows binaries* - When an operation for a non-Microsoft application requires elevation of privilege, the user is prompted on the secure desktop to select either Permit or Deny. If the user selects Permit, the operation continues with the user's highest available privilege.

  [Learn more](/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions#localpoliciessecurityoptions-useraccountcontrol-behavioroftheelevationpromptforadministrators)

  **Default**: Prompt for consent on the secure desktop

- **Minimum session security for NTLM SSP based clients**:  
  This security setting allows a client to require the negotiation of 128-bit encryption and NTLMv2 session security. These values are dependent on the LAN Manager Authentication Level security setting value. The options are:

  - *Require NTLMv2 session security* - The connection will fail if NTLMv2 protocol isn't negotiated.

  - *Require 128-bit encryption* - The connection will fail if strong encryption (128-bit) isn't negotiated.

  - *Require NTLMv2 and 128-bit encryption*.

  [Learn more](/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions#localpoliciessecurityoptions-networksecurity-minimumsessionsecurityforntlmsspbasedclients)

  **Default**: Require NTLM V2 128 encryption

- **Smart card removal behavior**:  
  This security setting determines what happens when the smart card for a logged-on user is removed from the smart card reader. The options are:

  - *No action*.

  - *Lock Workstation* - The workstation is locked when the smart card is removed, allowing users to leave the area, take their smart card with them, and still maintain a protected session.

  - *Force Logoff* - the user is automatically logged off when the smart card is removed.

  - *Disconnect Remote Desktop session* - Removal of the smart card disconnects the session without logging the user off. This allows the user to insert the smart card and resume the session later, or at another smart card reader-equipped computer, without having to log on again. If the session is local, this policy functions identically to Lock Workstation.

  [Learn more](/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions#localpoliciessecurityoptions-interactivelogon-smartcardremovalbehavior)

  **Default**: Lock workstation

- **Block anonymous enumeration of SAM accounts and shares**:  
  This security setting determines whether to allow anonymous enumeration of SAM accounts and shares. Windows allows anonymous users to do certain activities, such as enumerating the names of domain accounts and network shares. This is convenient, for example, when an administrator wants to grant access to users in a trusted domain that doesn't maintain a reciprocal trust. If you don't want to allow anonymous enumeration of SAM accounts and shares, then set this policy to *Yes*.  
  [Learn more](/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions#localpoliciessecurityoptions-networkaccess-donotallowanonymousenumerationofsamaccountsandshares)

  **Default**: Yes

- **Block remote logon with blank password**:  
  This security setting determines whether local accounts that aren't password protected can be used to log on from locations other than the physical computer console. If enabled, local accounts that aren't password protected must use the computer's keyboard to log on.

  *Warning*: Computers that aren't in physically secure locations should always enforce strong password policies for all local user accounts. Otherwise, anyone with physical access to the computer can log on by using a user account that doesn't have a password. This is especially important for portable computers.

  If you apply this security policy to the Everyone group, no one can log on through Remote Desktop Services. This setting doesn't affect logons that use domain accounts. It's possible for applications that use remote interactive logons to bypass this setting.  
  [Learn more](/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions#localpoliciessecurityoptions-accounts-limitlocalaccountuseofblankpasswordstoconsolelogononly)

  **Default**: Yes

- **Standard user elevation prompt behavior**:  
  This policy setting controls the behavior of the elevation prompt for standard users.

  - *Automatically deny elevation requests* - When an operation requires elevation of privilege, a configurable access denied error message is displayed. An enterprise that is running desktops as standard user may choose this setting to reduce help desk calls.

  - *Prompt for credentials on the secure desktop* - When an operation requires elevation of privilege, the user is prompted on the secure desktop to enter a different user name and password. If the user enters valid credentials, the operation continues with the applicable privilege.

  - *Prompt for credentials* - When an operation requires elevation of privilege, the user is prompted to enter an administrative user name and password. If the user enters valid credentials, the operation continues with the applicable privilege.

  [Learn more](/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions#localpoliciessecurityoptions-useraccountcontrol-behavioroftheelevationpromptforstandardusers)

  **Default**: Automatically deny elevation requests

- **Require admin approval mode for administrators**:  
  This policy setting controls the behavior of all User Account Control (UAC) policy settings for the computer. If you change this policy setting, you must restart your computer. The options are:

  - *Not configured* - Admin Approval Mode and all related UAC policy settings are disabled. Note: If this policy setting is disabled, the Security Center notifies you that the overall security of the operating system has been reduced.

  - *Yes* - Admin Approval Mode is enabled. This policy must be enabled and the related UAC policy settings must be set appropriately to allow the built-in Administrator account and all other users who are members of the Administrators group to run in Admin Approval Mode.

  [Learn more](/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions#localpoliciessecurityoptions-useraccountcontrol-useadminapprovalmode)

  **Default**: Yes

- **Prevent anonymous enumeration of SAM accounts**:  
  This security setting determines what additional permissions are granted for anonymous connections to the computer. Windows allows anonymous users to do certain activities, such as enumerating the names of domain accounts and network shares. This is convenient, for example, when an administrator wants to grant access to users in a trusted domain that doesn't maintain a reciprocal trust. This security option allows additional restrictions to be placed on anonymous connections as follows:

  - *Yes* - Don't allow enumeration of SAM accounts. This option replaces Everyone with Authenticated Users in the security permissions for resources.

  - *Not configured* - No additional restrictions. Rely on default permissions.

  [Learn more](/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions#localpoliciessecurityoptions-networkaccess-donotallowanonymousenumerationofsamaccounts)

  **Default**: Yes

- **Allow remote calls to security accounts manager**:  
  This policy setting allows you to restrict remote rpc connections to SAM. If not selected, the default security descriptor is used.  
  [Learn more](/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions#localpoliciessecurityoptions-networkaccess-restrictclientsallowedtomakeremotecallstosam)

  **Default**: *O:BAG:BAD:(A;;RC;;;BA)*

- **Use admin approval mode**:  
  This policy setting controls the behavior of Admin Approval Mode for the built-in Administrator account. The options are:

  - *Yes* - The built-in Administrator account uses Admin Approval Mode. By default, any operation that requires elevation of privilege will prompt the user to approve the operation.

  - *Not Configured* - The built-in Administrator account runs all applications with full administrative privilege.

  [Learn more](/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions#localpoliciessecurityoptions-useraccountcontrol-runalladministratorsinadminapprovalmode)

  **Default**: Yes
  
- **Only allow UI access applications for secure locations**:  
  This policy setting controls whether User Interface Accessibility (UIAccess or UIA) programs can automatically disable the secure desktop for elevation prompts used by a standard user.

  - *Yes* - UIA programs, including Windows Remote Assistance, automatically disable the secure desktop for elevation prompts. If you don't disable the "User Account Control: Switch to the secure desktop when prompting for elevation" policy setting, the prompts appear on the interactive user's desktop instead of the secure desktop.

  - *Not Configured*: - The secure desktop can be disabled only by the user of the interactive desktop or by disabling the "User Account Control: Switch to the secure desktop when prompting for elevation" policy setting.

  [Learn more](/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions#localpoliciessecurityoptions-useraccountcontrol-onlyelevateuiaccessapplicationsthatareinstalledinsecurelocations)

  **Default**: Yes

- **Detect application installations and prompt for elevation**:  
  This policy setting controls the behavior of application installation detection for the computer. The options are:

  - *Enabled* - When an application installation package is detected that requires elevation of privilege, the user is prompted to enter an administrative user name and password. If the user enters valid credentials, the operation continues with the applicable privilege.

  - *Disabled* - Application installation packages aren't detected and prompted for elevation. Enterprises that are running standard user desktops and use delegated installation technologies such as Group Policy Software Installation or Systems Management Server (SMS) should disable this policy setting. In this case, installer detection is unnecessary.

  [Learn more](/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions#localpoliciessecurityoptions-useraccountcontrol-detectapplicationinstallationsandpromptforelevation)

  **Default**: Yes

- **Prevent storing LAN manager hash value on next password change**:  
  This security setting determines if, at the next password change, the LAN Manager (LM) hash value for the new password is stored. The LM hash is relatively weak and prone to attack, as compared with the cryptographically stronger Windows NT hash. Because the LM hash is stored on the local computer in the security database, the passwords can be compromised if the security database is attacked.  
  [Learn more](/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions#localpoliciessecurityoptions-networksecurity-donotstorelanmanagerhashvalueonnextpasswordchange)

  **Default**: Yes

- **Virtualize file and registry write failures to per user locations**:  
  This policy setting controls whether application write failures are redirected to defined registry and file system locations. This policy setting mitigates applications that run as administrator and write run-time application data to *%ProgramFiles%*, *%Windir%*, *%Windir%\system32*, or *HKLM\Software*.  
  [Learn more](/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions#localpoliciessecurityoptions-useraccountcontrol-virtualizefileandregistrywritefailurestoperuserlocations)

  **Default**: Yes

## Microsoft Defender

For more information, see [Policy CSP - Defender](/windows/client-management/mdm/policy-csp-defender) in the Windows documentation.

- **Block Adobe Reader from creating child processes**:  
This rule prevents attacks by blocking Adobe Reader from creating additional processes. Through social engineering or exploits, malware can download and launch additional payloads and break out of Adobe Reader. By blocking child processes from being generated by Adobe Reader, malware attempting to use it as a vector are prevented from spreading.
[Learn more](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction)

  **Default**: Enable

- **Block Office communication apps launch in a child process**:  
  [Protect devices from exploits](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction)

  **Default**: Enable

- **Enter how often (0-24 hours) to check for security intelligence updates**  
  CSP: [Defender/SignatureUpdateInterval](/windows/client-management/mdm/policy-csp-defender)
  
  Specify how often to check for new signatures. A value of 1 is one hour, 2 is two hours, and so on.

  **Default**: 4

- **Scan type**  
  CSP: [Defender/ScanParameter](/windows/client-management/mdm/policy-csp-defender#defender-scanparameter)

  Specify the scan type to use for a schedule scan

  **Default**: Quick scan

- **Defender schedule scan day**:  
  Defender schedule scan day.

  **Default**: Everyday

::: zone-end
::: zone pivot="mdm-december-2020,november-2021"

- **Defender scan start time**:  
  Defender schedule scan time.

  **Default**: Not configured

::: zone-end
::: zone pivot="mdm-sept-2020,mdm-december-2020,november-2021"

- **Cloud-delivered protection level**:  
  CSP: [Defender/CloudBlockLevel](/windows/client-management/mdm/policy-csp-defender#defender-cloudblocklevel)

  Specify the level of cloud-delivered protection. Not Configured uses the default Microsoft Defender Antivirus blocking level and provides strong detection without increasing the risk of detecting legitimate files. High applies a strong level of detection. High + uses the High level and applies addition protection measures (may impact client performance). Zero tolerance blocks all unknown executables While unlikely, setting to High may cause some legitimate files to be detected. 

**Default**: Not Configured

- **Scan network files**:  
  CSP: [Defender/AllowScanningNetworkFiles](/windows/client-management/mdm/policy-csp-defender#defender-allowscanningnetworkfiles)

  When set to Yes, Microsoft Defender will scan network files. When set to Not configured, the client will return to default with is disabling scanning of network files.

**Default**: Yes

- **Turn on real-time protection**  
  CSP: [Defender/AllowRealtimeMonitoring](/windows/client-management/mdm/policy-csp-defender#defender-allowrealtimemonitoring)

  When this setting is set to Yes, real-time monitoring will be enforced and the user can't disable it. When set to Not configured, the setting is returned to client default, which is on, but the user can change it. To disable real-time monitoring, use a custom URI.

  **Default**: Yes  

::: zone-end
::: zone pivot="november-2021"

- **Scan scripts that are used in Microsoft browsers**  
  CSP [Defender/AllowScriptScanning](/windows/client-management/mdm/policy-csp-defender#defender-allowscriptscanning)

  When this setting is set to Yes, the Windows Defender Script Scanning functionality will be enforced and the user cannot turn them off. When set to Not configured, the setting is returned to client default which is to enable script scanning, however the user can turn it off.

  **Default**: Yes

::: zone-end
::: zone pivot="mdm-sept-2020,mdm-december-2020,november-2021"

- **Scan archive files**:  
  CSP: [Defender/AllowArchiveScanning](/windows/client-management/mdm/policy-csp-defender#defender-allowarchivescanning)
  
  When set to Yes, archive files such as ZIP or CAB file scanning will be enforced. When set to Not configured, the setting will be returned back to client default, which is to scan archived files, however the user may disable this.

  **Default**: Yes

- **Turn on behavior monitoring**:  
  CSP: [Defender/AllowBehaviorMonitoring](/windows/client-management/mdm/policy-csp-defender#defender-allowbehaviormonitoring)

  When this setting is set to Yes, behavior monitoring will be enforced and the user can't disable it. When set to Not configured, the setting is returned to client default, which is on, but the user can change it. To disable real-time monitoring, use a custom URI.

  **Default**: Yes

- **Turn on cloud-delivered protection**:  
  CSP: [Defender/AllowCloudProtection](/windows/client-management/mdm/policy-csp-defender#defender-allowcloudprotection)

  When set to Yes, Defender will send information to Microsoft about any problems it finds. If set to Not configured, the client will return to default which enables the feature but allows the user to disable it.

  **Default**: Yes

- **Scan incoming mail messages**:  
  CSP: [Defender/AllowEmailScanning](/windows/client-management/mdm/policy-csp-defender#defender-allowemailscanning)

  When set to Yes, e-mail mailbox and mail files such as PST, DBX, MNX, MIME and BINHEX will be scanned. When Not configured, the setting will return to client default of e-mail files not being scanned.

  **Default**: Yes

- **Scan removable drives during a full scan**:  
  CSP: [Defender/AllowFullScanRemovableDriveScanning](/windows/client-management/mdm/policy-csp-defender#defender-allowfullscanremovabledrivescanning)

  When set to Yes, during a full scan removable drives (for example, USB flash drives) will be scanned. When set to Not Configured, the setting will return to client default, which scans removable drives, however the user can disable this.
  **Default**: Yes  

- **Block Office applications from injecting code into other processes**:  
  [Protect devices from exploits](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction)

  When set to Yes, Office applications will be blocked from injecting code into other processes. When set to Audit only, Windows events will be raised instead of blocking. Setting to Not Configured will return the setting to Windows default, which is off. This Attack Surface Reduction (ASR) rule is controlled via the following GUID: 75668C1F-73B5-4CF0-BB93-3ECF5CB7CC84

  **Default**:  Block

- **Block Office applications from creating executable content**  
  [Protect devices from exploits](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction)

  When set to Yes, Office applications will not be allowed to create executable content. When set to Audit only, Windows events will be raised instead of blocking. Setting to Not Configured will return the setting to Windows default, which is off. This ASR rule is controlled via the following GUID: 3B576869-A4EC-4529-8536-B80A7769E899

  **Default**:  Block

- **Block all Office applications from creating child processes**  
  [Protect devices from exploits](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction)

  When set to Audit mode, Windows events will be raised instead of blocking. Setting to Not Configured will return the setting to Windows default, which is off. This ASR rule is controlled via the following GUID: D4F940AB-401B-4EFC-AADC-AD5F3C50688A

  **Default**:  Block

- **Block Win32 API calls from Office macro**:  
  [Protect devices from exploits](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction)

  When set to Yes, Office macro's will be blocked from using Win32 API calls. When set to Audit only, Windows events will be raised instead of blocking. Setting to Not Configured will return the setting to Windows default, which is off. This ASR rule is controlled via the following GUID: 92E97FA1-2EDF-4476-BDD6-9DD0B4DDDC7B
  
  **Default**: Block

- **Block execution of potentially obfuscated scripts (js/vbs/ps)**:  
  [Protect devices from exploits](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction)

  When set to yes, Defender will block execution of obfuscated scripts. When set to Audit only, Windows events will be raised instead of blocking. Setting to Not Configured will return the setting to Windows default, which is off. This ASR rule is controlled via the following GUID: 5BEB7EFE-FD9A-4556-801D-275E5FFC04CC
  
  **Default**: Block

- **Block JavaScript or VBScript from launching downloaded executable content**:  
  [Protect devices from exploits](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction)

  When set to Yes, Defender will block Javascript or VBScript files that have been downloaded from the Internet from being executed. When set to Audit only, Windows events will be raised instead of blocking. Setting to Not Configured will return the setting to Windows default, which is off. This attack surface reduction (ASR) rule is controlled via the following GUID: D3E037E1-3EB8-44C8-A917-57927947596D
  
  **Default**: Block

- **Block executable content download from email and webmail clients**:  
  [Block executable content download from email and webmail clients](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction)

  When set to Yes, executable content downloaded from email and webmail clients will be blocked. When set to Audit only, Windows events will be raised instead of blocking. Setting to Not Configured will return the setting to Windows default, which is off.

  **Default**: Block

- **Prevent credential stealing type**:  
  [Protect devices from exploits](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction)
  
  When set to Yes, attempts to steal credentials via lsass.exe will be blocked. When set to Audit only, Windows events will be raised instead of blocking. Setting to Not Configured will return the setting to Windows default, which is off. This ASR rule is controlled via the following GUID: 9e6c4e1f-7d60-472f-ba1a-a39ef669e4b2

  **Default**: Enable

- **Defender potentially unwanted app action**:  
  CSP: [Defender/PUAProtection](/windows/client-management/mdm/policy-csp-defender#defender-puaprotection)+

  The potentially unwanted application (PUA) protection feature in Microsoft Defender Antivirus can identify and block PUAs from downloading and installing on endpoints in your network. These applications aren't considered viruses, malware, or other types of threats, but might do actions on endpoints that adversely affect their performance or use. PUA can also refer to applications that are considered to have a poor reputation. Typical PUA behavior includes: Various types of software bundling Ad injection into web browsers Driver and registry optimizers that detect issues, request payment to fix the errors, but remain on the endpoint and make no changes or optimizations (also known as "rogue antivirus" programs). These applications can increase the risk of your network being infected with malware, cause malware infections to be harder to identify, and can waste IT resources in cleaning up the applications.

  **Default**: Block

- **Block untrusted and unsigned processes that run from USB**:  
  [Protect devices from exploits](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction)
  
  When set to Yes, untrusted/unsigned processes executing from a USB drive will be blocked. When set to Audit only, Windows events will be raised instead of blocking. Setting to Not Configured will return the setting to Windows default, which is off. This ASR rule is controlled via the following GUID: b2b3f03d-6a65-4f7b-a9c7-1c7ef74a9ba4

  **Default**: Block

- **Enable network protection**:  
  [Defender/EnableNetworkProtection](/windows/client-management/mdm/policy-csp-defender#defender-enablenetworkprotection)

  When set to Yes, network protection will be enabled for all users on the system. Network protection protects employees from accessing phishing scams, and malicious content on the Internet. This includes third-party browsers. Setting this to Audit only, users will not be blocked from dangerous domains however Windows events will be raised instead. Setting this to Not Configured will return the setting to Windows default, which is disabled.

  **Default**: Enable

- **Defender sample submission consent type**:  
  [Defender/SubmitSamplesConsent](/windows/client-management/mdm/policy-csp-defender#defender-submitsamplesconsent)

  Checks for the user consent level in Microsoft Defender to send data. If the required consent has already been granted, Microsoft Defender submits them. If not, (and if the user has specified never to ask), the UI is launched to ask for user consent (when Defender/AllowCloudProtection is allowed) before sending data.

  **Default**: Send safe samples automatically

## MS Security Guide

For more information, see [Policy CSP - MSSecurityGuide](/windows/client-management/mdm/policy-csp-mssecurityguide) in the Windows documentation.

- **Apply UAC restrictions to local accounts on network logon**:  
  [Learn more](/windows/client-management/mdm/policy-csp-mssecurityguide#mssecurityguide-applyuacrestrictionstolocalaccountsonnetworklogon)

  **Default**: Enabled

- **SMB v1 client driver start configuration**:  
  [Learn more](/windows/client-management/mdm/policy-csp-mssecurityguide#mssecurityguide-configuresmbv1clientdriver)

  **Default**: Disabled driver

- **SMB v1 server**:  
  [Learn more](/windows/client-management/mdm/policy-csp-mssecurityguide#mssecurityguide-configuresmbv1server)

  **Default**: Disabled

- **Digest authentication**:  
  [Learn more](/windows/client-management/mdm/policy-csp-mssecurityguide#mssecurityguide-wdigestauthentication)

  **Default**: Disabled

- **Structured exception handling overwrite protection**:  
  [Learn more](/windows/client-management/mdm/policy-csp-mssecurityguide#mssecurityguide-enablestructuredexceptionhandlingoverwriteprotection)

  **Default**: Enabled

## MSS Legacy

For more information, see [Policy CSP - MSSLegacy](/windows/client-management/mdm/policy-csp-msslegacy) in the Windows documentation.

- **Network IP source routing protection level**:  
  [Learn more](/windows/client-management/mdm/policy-csp-msslegacy#msslegacy-ipsourceroutingprotectionlevel)

  **Default**: Highest protection  

- **Network ignore NetBIOS name release requests except from WINS servers**:  
  [Learn more](/windows/client-management/mdm/policy-csp-msslegacy#msslegacy-allowthecomputertoignorenetbiosnamereleaserequestsexceptfromwinsservers)

  **Default**: Enabled

- **Network IPv6 source routing protection level**:  
  [Learn more](/windows/client-management/mdm/policy-csp-msslegacy#msslegacy-ipv6sourceroutingprotectionlevel)

  **Default**: Highest protection

- **Network ICMP redirects override OSPF generated routes**:  
  [Learn more](/windows/client-management/mdm/policy-csp-msslegacy#msslegacy-allowicmpredirectstooverrideospfgeneratedroutes)

  **Default**: Disabled

## Power

For more information, see [Policy CSP - Power](/windows/client-management/mdm/policy-csp-power) in the Windows documentation.

- **Require password on wake while plugged in**:  
  This policy setting specifies if the user is prompted for a password when the system resumes from sleep. If you enable or don't configure this policy setting, the user is prompted for a password when the system resumes from sleep. If you disable this policy setting, the user isn't prompted for a password when the system resumes from sleep.  
  [Learn more](/windows/client-management/mdm/policy-csp-power#power-requirepasswordwhencomputerwakespluggedin)

  **Default**: Enabled

- **Standby states when sleeping while on battery**:  
  This policy setting manages if Windows can use standby states when putting the computer in a sleep state. If you enable or don't configure this policy setting, Windows uses standby states to put the computer in a sleep state. If you disable this policy setting, standby states (S1-S3) aren't allowed.  
  [Learn more](/windows/client-management/mdm/policy-csp-power#power-standbytimeoutonbattery)

  **Default**: Disabled

- **Standby states when sleeping while plugged in**:  
  This policy setting manages if Windows can use standby states when putting the computer in a sleep state. If you enable or don't configure this policy setting, Windows uses standby states to put the computer in a sleep state. If you disable this policy setting, standby states (S1-S3) aren't allowed.  
  [Learn more](/windows/client-management/mdm/policy-csp-power#power-standbytimeoutpluggedin)

  **Default**: Disabled

- **Require password on wake while on battery**:  
  This policy setting specifies if the user is prompted for a password when the system resumes from sleep. If you enable or don't configure this policy setting, the user is prompted for a password when the system resumes from sleep. If you disable this policy setting, the user isn't prompted for a password when the system resumes from sleep.  
  [Learn more](/windows/client-management/mdm/policy-csp-power#power-requirepasswordwhencomputerwakesonbattery)

  **Default**: Enabled

## Remote Assistance

For more information, see [Policy CSP - RemoteAssistance](/windows/client-management/mdm/policy-csp-remoteassistance#remoteassistance-solicitedremoteassistance) in the Windows documentation.

- **Remote Assistance solicited**:  
  This policy setting allows you to turn on or turn off Solicited (Ask for) Remote Assistance on this computer.
  
  - *If you enable this policy setting*, users on this computer can use email or file transfer to ask someone for help. Also, users can use instant messaging programs to allow connections to this computer, and you can configure additional Remote Assistance settings.

  - *If you disable this policy setting*, users on this computer can't use email or file transfer to ask someone for help. Also, users can't use instant messaging programs to allow connections to this computer.

  - *If you don't configure this policy setting*, users can turn on or turn off Solicited (Ask for) Remote Assistance themselves in System Properties in Control Panel. Users can also configure Remote Assistance settings.

  If you enable this policy setting, you have two ways to allow helpers to provide Remote Assistance: "Allow helpers to only view the computer" or "Allow helpers to remotely control the computer." The "Maximum ticket time" policy setting sets a limit on the amount of time that a Remote Assistance invitation created by using email or file transfer can remain open. The "Select the method for sending email invitations" setting specifies which email standard to use to send Remote Assistance invitations. Depending on your email program, you can use either the *Mailto* standard (the invitation recipient connects through an Internet link) or the SMAPI (Simple MAPI) standard (the invitation is attached to your email message). This policy setting isn't available in Windows Vista because SMAPI is the only method supported. If you enable this policy setting, you should also enable appropriate firewall exceptions to allow Remote Assistance communications.  
  [Learn more](/windows/client-management/mdm/policy-csp-remoteassistance#remoteassistance-solicitedremoteassistance)

  **Default**: Disable Remote Assistance

## Remote Desktop Services

For more information, see [Policy CSP - RemoteDesktopServices](/windows/client-management/mdm/policy-csp-remotedesktopservices) in the Windows documentation.

- **Block password saving**:  
  Controls whether passwords can be saved on this computer from Remote Desktop Connection. If you enable this setting the password saving checkbox in Remote Desktop Connection is disabled and users can't save passwords. When a user opens an RDP file using Remote Desktop Connection and saves their settings, any password that previously existed in the RDP file are deleted. If you disable this setting or leave it not configured, the user can save passwords using Remote Desktop Connection.  
  [Learn more](/windows/client-management/mdm/policy-csp-remotedesktopservices#remotedesktopservices-donotallowpasswordsaving)

   **Default**: Enabled

- **Secure RPC communication**:  
  Specifies whether a Remote Desktop Session Host server requires secure RPC communication with all clients or allows unsecured communication. You can use this setting to strengthen the security of RPC communication with clients by allowing only authenticated and encrypted requests. If the status is set to Enabled, Remote Desktop Services accepts requests from RPC clients that support secure requests, and doesn't allow unsecured communication with untrusted clients. If the status is set to Disabled, Remote Desktop Services always requests security for all RPC traffic. However, unsecured communication is allowed for RPC clients that don't respond to the request. If the status is set to Not Configured, unsecured communication is allowed. Note: The RPC interface is used for administering and configuring Remote Desktop Services.  
  [Learn more](/windows/client-management/mdm/policy-csp-remotedesktopservices#remotedesktopservices-requiresecurerpccommunication)

  **Default**: Enabled

- **Block drive redirection**:  
  This policy setting specifies whether to prevent the mapping of client drives in a Remote Desktop Services session (drive redirection). By default, an RD Session Host server maps client drives automatically upon connection. Mapped drives appear in the session folder tree in File Explorer or Computer in the format *\<driveletter>* on *\<computername>*. You can use this policy setting to override this behavior. If you enable this policy setting, client drive redirection isn't allowed in Remote Desktop Services sessions, and Clipboard file copy redirection isn't allowed on computers running Windows Server 2003, Windows 8, and Windows XP. If you disable this policy setting, client drive redirection is always allowed. Also, Clipboard file copy redirection is always allowed if Clipboard redirection is allowed. If you don't configure this policy setting, client drive redirection and Clipboard file copy redirection aren't specified at the Group Policy level.  
  [Learn more](/windows/client-management/mdm/policy-csp-remotedesktopservices#remotedesktopservices-donotallowdriveredirection)

  **Default**: Enabled

- **Prompt for password upon connection**:  
  This policy setting specifies whether Remote Desktop Services always prompts the client for a password upon connection. You can use this setting to enforce a password prompt for users logging on to Remote Desktop Services, even if they already provided the password in the Remote Desktop Connection client. By default, Remote Desktop Services allows users to automatically log on by entering a password in the Remote Desktop Connection client. If you enable this policy setting, users can't automatically log on to Remote Desktop Services by supplying their passwords in the Remote Desktop Connection client. they're prompted for a password to log on. If you disable this policy setting, users can always log on to Remote Desktop Services automatically by supplying their passwords in the Remote Desktop Connection client. If you don't configure this policy setting, automatic logon isn't specified at the Group Policy level.  
  [Learn more](/windows/client-management/mdm/policy-csp-remotedesktopservices#remotedesktopservices-promptforpassworduponconnection)

  **Default**: Enabled

- **Remote desktop services client connection encryption level**:  
  Specifies whether to require the use of a specific encryption level to secure communications between client computers and RD Session Host servers during Remote Desktop Protocol (RDP) connections. This policy only applies when you're using native RDP encryption. However, native RDP encryption (as opposed to SSL encryption) isn't recommended. This policy doesn't apply to SSL encryption. If you enable this policy setting, all communications between clients and RD Session Host servers during remote connections must use the encryption method specified in this setting. By default, the encryption level is set to High. The following encryption methods are available:

  - *High* - The High setting encrypts data sent from the client to the server and from the server to the client by using strong 128-bit encryption. Use this encryption level in environments that contain only 128-bit clients (for example, clients that run Remote Desktop Connection). Clients that don't support this encryption level can't connect to RD Session Host servers.

  - *Client Compatible* - The Client Compatible setting encrypts data sent between the client and the server at the maximum key strength supported by the client. Use this encryption level in environments that include clients that don't support 128-bit encryption.

  - *Low* - The Low setting encrypts only data sent from the client to the server by using 56-bit encryption.  
  
  If you disable or don't configure this setting, the encryption level to be used for remote connections to RD Session Host servers isn't enforced through Group Policy. Important FIPS compliance can be configured through the System cryptography. Use FIPS-compliant algorithms for encryption, hashing, and signing settings in Group Policy (under Computer Configuration\Windows Settings\Security Settings\Local Policies\Security Options.) The FIPS-compliant setting encrypts and decrypts data sent from the client to the server and from the server to the client, with the Federal Information Processing Standard (FIPS) 140 encryption algorithms, by using Microsoft cryptographic modules. Use this encryption level when communications between clients and RD Session Host servers requires the highest level of encryption.  
  [Learn more](/windows/client-management/mdm/policy-csp-remotedesktopservices#remotedesktopservices-clientconnectionencryptionlevel)

  **Default**: High

## Remote Management

For more information, see [Policy CSP - RemoteManagement](/windows/client-management/mdm/policy-csp-remotemanagement) in the Windows documentation.

- **Block storing run as credentials**:  
  Client basic authentication.  
  [Learn more](/windows/client-management/mdm/policy-csp-remotemanagement#remotemanagement-disallowstoringofrunascredentials)

  **Default**: Enabled

- **Basic authentication**:  
  This policy setting allows you to manage whether the Windows Remote Management (WinRM) service accepts Basic authentication from a remote client. If you enable this policy setting, the WinRM service accepts Basic authentication from a remote client. If you disable or don't configure this policy setting, the WinRM service doesn't accept Basic authentication from a remote client.  
  [Learn more](/windows/client-management/mdm/policy-csp-remotemanagement#remotemanagement-allowbasicauthentication-service)

  **Default**: Disabled

- **Block client digest authentication**:  
  This policy setting allows you to manage whether the Windows Remote Management (WinRM) client uses Digest authentication. If you enable this policy setting, the WinRM client doesn't use Digest authentication. If you disable or don't configure this policy setting, the WinRM client uses Digest authentication.  
  [Learn more](/windows/client-management/mdm/policy-csp-remotemanagement#remotemanagement-disallownegotiateauthenticationclient)

  **Default**: Enabled

- **Unencrypted traffic**:  
  This policy setting allows you to manage whether the Windows Remote Management (WinRM) service sends and receives unencrypted messages over the network. If you enable this policy setting, the WinRM client sends and receives unencrypted messages over the network. If you disable or don't configure this policy setting, the WinRM client sends or receives only encrypted messages over the network.  
  [Learn more](/windows/client-management/mdm/policy-csp-remotemanagement#remotemanagement-allowunencryptedtraffic-service)

  **Default**: Disabled

- **Client unencrypted traffic**:  
  This policy setting allows you to manage whether the Windows Remote Management (WinRM) client sends and receives unencrypted messages over the network. If you enable this policy setting, the WinRM client sends and receives unencrypted messages over the network. If you disable or don't configure this policy setting, the WinRM client sends or receives only encrypted messages over the network.  
  [Learn more](/windows/client-management/mdm/policy-csp-remotemanagement#remotemanagement-allowunencryptedtraffic-client)

  **Default**: Disabled

- **Client basic authentication**:  
  This policy setting allows you to manage whether the Windows Remote Management (WinRM) client uses Basic authentication. If you enable this policy setting, the WinRM client uses Basic authentication. If WinRM is configured to use HTTP transport, the user name and password are sent over the network as clear text. If you disable or don't configure this policy setting, the WinRM client doesn't use Basic authentication.  
  [Learn more](/windows/client-management/mdm/policy-csp-remotemanagement#remotemanagement-allowbasicauthentication-client)

  **Default**: Disabled

## Remote Procedure Call

For more information, see [Policy CSP - RemoteProcedureCall](/windows/client-management/mdm/policy-csp-remoteprocedurecall) in the Windows documentation.

- **RPC unauthenticated client options**:  
  This policy setting controls how the RPC server runtime handles unauthenticated RPC clients connecting to RPC servers. This policy setting impacts all RPC applications. In a domain environment, use this policy setting with caution as it can impact a wide range of functionality including group policy processing itself. Reverting a change to this policy setting can require manual intervention on each affected machine. Don't apply this policy setting to a domain controller. If you disable this policy setting, the RPC server runtime uses the value of "Authenticated" on Windows Client, and the value of "None" on Windows Server versions that support this policy setting. If you don't configure this policy setting, it remains disabled. The RPC server runtime behaves as though it was enabled with the value of "Authenticated" used for Windows Client and the value of "None" used for Server SKUs that support this policy setting. If you enable this policy setting, it directs the RPC server runtime to restrict unauthenticated RPC clients connecting to RPC servers running on a machine. A client is considered an authenticated client if it uses a named pipe to communicate with the server or if it uses RPC Security. RPC Interfaces that have specifically requested to be accessible by unauthenticated clients may be exempt from this restriction, depending on the selected value for this policy setting.

  - *None* allows all RPC clients to connect to RPC Servers running on the machine on which the policy setting is applied.

  - *Authenticated* allows only authenticated RPC Clients (per the definition above) to connect to RPC Servers running on the machine on which the policy setting is applied. Exemptions are granted to interfaces that have requested them.

  - *Authenticated without exceptions* allows only authenticated RPC Clients (per the definition above) to connect to RPC Servers running on the machine on which the policy setting is applied. No exceptions are allowed. Note: This policy setting won't be applied until the system is rebooted.

  [Learn more](/windows/client-management/mdm/policy-csp-remoteprocedurecall#remoteprocedurecall-rpcendpointmapperclientauthentication)

  **Default**: Authenticated

## Search

For more information, see [Policy CSP - Search](/windows/client-management/mdm/policy-csp-search) in the Windows documentation.

- **Disable indexing encrypted items**:  
  Allows or disallows the indexing of items. This switch is for the Windows Search Indexer, which controls whether it will index items that are encrypted, such as the Windows Information Protection (WIP) protected files. When the policy is enabled, WIP protected items are indexed and the metadata about them are stored in an unencrypted location. The metadata includes things like file path and date modified. When the policy is disabled, the WIP protected items aren't indexed and don't show up in the results in Cortana or file explorer. There may also be a performance impact on photos and Groove apps if there are many WIP protected media files on the device.  
  [Learn more]( https://go.microsoft.com/fwlink/?linkid=2067303)

  **Default**: Yes

## Smart Screen

For more information, see [Policy CSP - SmartScreen](/windows/client-management/mdm/policy-csp-smartscreen) in the Windows documentation.

- **Turn on Windows SmartScreen**  
  CSP: [SmartScreen/EnableSmartScreenInShell](/windows/client-management/mdm/policy-csp-smartscreen#smartscreen-enablesmartscreeninshell)

  Setting this to Yes will enforce the use of SmartScreen for all users. Setting this to Not configured will return the setting to Windows default, which is to enable SmartScreen, however users may change this setting. To disable SmartScreen, use a custom URI.

  **Default**: Yes

- **Block users from ignoring SmartScreen warnings**  
  CSP: [SmartScreen/PreventOverrideForFilesInShell](/windows/client-management/mdm/policy-csp-smartscreen#smartscreen-preventoverrideforfilesinshell)

  When set to Yes, SmartScreen is enabled and users can't bypass warnings for files or malicious apps. When set to Not configured, users can ignore SmartScreen warnings for files and malicious apps.  

  This setting requires the 'Turn on Windows SmartScreen' setting be set to Yes.

  **Default**: Yes

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

  **Default**: Good unknown and bad critical

## Wi-Fi

For more information, see [Policy CSP - Wifi](/windows/client-management/mdm/policy-csp-wifi) in the Windows documentation.

- **Block Automatically connecting to Wi-Fi hotspots**:  
  Allow or disallow the device to automatically connect to Wi-Fi hotspots.  
  [Learn more](/windows/client-management/mdm/policy-csp-wifi#wifi-allowautoconnecttowifisensehotspots)

  **Default**: Yes

- **Block Internet sharing**:  
  Specifies whether internet sharing is possible on the device.  
  [Learn more](/windows/client-management/mdm/policy-csp-wifi#wifi-allowinternetsharing)

  **Default**: Yes

## Windows Connection Manager

For more information, see [Policy CSP - WindowsConnectionManager](/windows/client-management/mdm/policy-csp-windowsconnectionmanager) in the Windows documentation.

- **Block connection to non-domain networks**:  
  This policy setting prevents computers from connecting to both a domain-based network and a non-domain based network at the same time. If this policy setting is enabled, the computer responds to automatic and manual network connection attempts based on the following circumstances:

  - *Automatic connection attempts* - When the computer is already connected to a domain-based network, all automatic connection attempts to non-domain networks are blocked. When the computer is already connected to a non-domain based network, automatic connection attempts to domain-based networks are blocked.

  - *Manual connection attempts* - When the computer is already connected to either a non-domain based network or a domain-based network over media other than Ethernet, and a user attempts to create a manual connection to an additional network in violation of this policy setting, the existing network connection disconnects, and the manual connection is allowed. When the computer is already connected to either a non-domain based network or a domain-based network over Ethernet, and a user attempts to create a manual connection to an additional network in violation of this policy setting, the existing Ethernet connection is maintained and the manual connection attempt is blocked.

  If this policy setting isn't configured or is disabled, computers are allowed to connect simultaneously to both domain and non-domain networks.  
  [Learn more](/windows/client-management/mdm/policy-csp-windowsconnectionmanager)

  **Default**: Enabled

## Windows Ink Workspace

For more information, see [Policy CSP - WindowsInkWorkspace](/windows/client-management/mdm/policy-csp-windowsinkworkspace) in the Windows documentation.

- **Ink Workspace**:  
  Specifies whether to allow the user to access the ink workspace.

  - *Disabled* - access to ink workspace is disabled. The feature is turned off.

  - *Enabled* - The Ink Workspace feature is turned on, but the user can't access it above the lock screen.

  - *Not Configured* - The Ink Workspace feature is turned on, and the user can use it above the lock screen.

  [Learn more](/windows/client-management/mdm/policy-csp-windowsinkworkspace#windowsinkworkspace-allowwindowsinkworkspace)

  **Default**: Enabled

## Windows PowerShell

For more information, see [Policy CSP - WindowsPowerShell](/windows/client-management/mdm/policy-csp-windowspowershell) in the Windows documentation.

- **PowerShell script block logging**:  
  This policy setting enables logging of all PowerShell script input to the Microsoft-Windows-PowerShell/Operational event log. If you enable this policy setting, Windows PowerShell will log the processing of commands, script blocks, functions, and scripts - whether invoked interactively, or through automation. If you disable this policy setting, logging of PowerShell script input is disabled. If you enable the Script Block Invocation Logging, PowerShell additionally logs events when invocation of a command, script block, function, or script starts or stops. Enabling Invocation Logging generates a high volume of event logs. Note: This policy setting exists under both Computer Configuration and User Configuration in the Group Policy Editor. The Computer Configuration policy setting takes precedence over the User Configuration policy setting.  
  [Learn more](/windows/client-management/mdm/policy-csp-windowspowershell#windowspowershell-turnonpowershellscriptblocklogging)

  **Default**: Enabled

::: zone-end

## Next steps

- [Learn about security baselines](security-baselines.md)
- [Avoid conflicts](security-baselines.md#avoid-conflicts)
- [Troubleshoot policies and profiles in Intune](/troubleshoot/mem/intune/troubleshoot-policies-in-microsoft-intune)
