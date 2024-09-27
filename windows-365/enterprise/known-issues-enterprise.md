---
title: Known issues for Windows 365 Enterprise and Frontline
description: Learn about known issues for Windows 365 Enterprise.
keywords:
ms.author: erikje
author: ErikjeMS
manager: dougeby
ms.date: 7/09/2024
audience: Admin
ms.topic: troubleshooting
ms.service: windows-365
ms.subservice: windows-365-enterprise
ms.localizationpriority: high
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: ivivano
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: get-started
ms.collection:
- M365-identity-device-management
- tier2
---

# Known issues: Windows 365 Enterprise and Frontline

The following items are known issues for Windows 365 Enterprise.

## First-time Cloud PC sign-in triggers Impossible Travel Location alert

When using Conditional Access, a user who signs in to a Cloud PC for the first time might trigger an impossible travel location alert.

**Troubleshooting steps**: [Follow these steps to investigate risk](/entra/id-protection/howto-identity-protection-investigate-risk) to verify that the activity matches the expected behavior for the user, based on their physical location and the location of the Cloud PC.

## Watermarking support in Windows 365

Watermarking support is configured on session hosts and enforced by the Remote Desktop client. The settings for Watermarking support can be configured via Group Policy (GPO) or the Intune Settings Catalog. The default for the QR code embedded content setting doesn't allow administrators to look up device information from leaked images for Cloud PCs.  

**Troubleshooting steps**: Ensure that the QR code embedded content setting is configured to **Device ID** either in the GPO or in the Intune Settings Catalog for the Intune Configuration profile used to configure Watermarking support.

For more information, see [Administrative template for Azure Virtual Desktop](/azure/virtual-desktop/administrative-template?tabs=intune#configure-the-administrative-template).

[!INCLUDE [Missing start menu and taskbar when using iPad and the Remote Desktop app to access a Cloud PC](../includes/known-issues.md)]

## In-place Windows upgrade may change computer name

Upgrading an existing Cloud PC between release versions of Windows 10 to Windows 11 may cause the computer name to be changed to a name with a prefix of "pps" while leaving the Intune device name unchanged.

**Troubleshooting steps**: Find and manage the Cloud PC in Microsoft Intune by using the unchanged Intune device name, either through the **Devices > All devices** list or the **Devices > Windows 365 > All Cloud PCs** list.

## Windows 365 provisioning fails<!--38483005-->

Windows 365 provisioning failures may occur because both:

- the Desired State Configuration (DSC) extension isn't signed and
- the PowerShell Execution policy is set to Allsigned in the Group Policy Object (GPO)

**Troubleshooting steps**:

1. Did the Azure network connection (ANC) fail with the following error: `"An internal error occurred. The virtual machine deployment timed out."`?
2. If yes, review the related GPO. Is PowerShell Execution set to AllSigned?
3. If it is, either remove the GPO or reset the PowerShell Execution to Unrestricted.
4. Retry the ANC health check. If the check succeeds, retry provisioning.

## Cloud PC reports as not compliant for compliance policy

The following device compliance settings report as **Not applicable** when being evaluated for a Cloud PC:

- **Trusted Platform Module (TPM)**
- **Require encryption of data storage on device.**

The following device compliance settings may report as **Not Compliant** when being evaluated for a Cloud PC:

- **Require BitLocker**
- **Require Secure Boot to be enabled on the device.** Cloud PC support for [Secure boot](/windows-hardware/design/device-experiences/oem-secure-boot) functionality is now available to all customers.

**Troubleshooting steps to enable secure boot on the Cloud PC**:

1. [Reprovision](reprovision-cloud-pc.md) the specific Cloud PC.

**Troubleshooting steps to remove not compliant settings**:

1. [Create a filter for all Cloud PCs](create-filter.md#create-a-filter-for-all-cloud-pcs).
2. For any existing device compliance policies that both evaluate to a Cloud PC and contain either of the **Not Compliant** settings, use this new filter to exclude Cloud PCs from the policy assignment.
3. Create a new device compliance policy without either of the **Not Compliant** settings and use this new filter to include Cloud PCs for the policy assignment.

## Single sign-on users see a dialog to allow remote desktop connection during the connection attempt <!--42499792-->

When enabling single sign-on, a prompt appears to authenticate to Microsoft Entra ID and allow the Remote Desktop connection when launching a connection to a new Cloud PC. Microsoft Entra remembers up to 15 devices for 30 days before prompting again. If you see this dialog, select **Yes** to connect.

To prevent this dialog from being shown, you can create a pre-consented device group. Follow the instructions to [configure a target device group](/azure/virtual-desktop/configure-single-sign-on#configure-the-target-device-groups) to get started.

<a name='single-sign-on-user-connections-are-being-denied-through-azure-ad-conditional-access---42317382--'></a>

## Single sign-on user connections are being denied through Microsoft Entra Conditional Access <!--42317382-->

**Possible cause**: To log in through single sign-on, the remote desktop client requests an access token to the **Microsoft Remote Desktop** app in Microsoft Entra, which may be the cause of the failed connection.

**Troubleshooting**: To [troubleshoot sign-in problems](/azure/active-directory/conditional-access/troubleshoot-conditional-access), follow the steps.

## Single sign-on users are immediately disconnected when the Cloud PC locks

When single sign-on isn't used, users can see the Cloud PC lock screen and enter credentials to unlock their Windows session. However, when single sign-on is used, the Cloud PC fully disconnects the session so that:

1. Users can use passwordless authentication to unlock their Cloud PC.
2. Conditional Access policies and multifactor authentication can be enforced when unlocking the Cloud PC.

<a name='single-sign-on-users-arent-asked-to-reauthenticate-to-azure-ad-when-connecting-from-an-unmanaged-device---35593334--'></a>

## Single sign-on users aren't asked to reauthenticate to Microsoft Entra ID when connecting from an unmanaged device <!--35593334-->

When using single sign-on, all authentication behavior (including supported credential types and sign-in frequency) is driven through Microsoft Entra ID.

**Troubleshooting**: To enforce periodic reauthentication through Microsoft Entra ID, create a Conditional Access policy using the [sign-in frequency control](set-conditional-access-policies.md#configure-sign-in-frequency).

## I don’t see the Cloud PC reports on the Intune admin center Devices > Overview page

If you turned on the **Use Devices preview** setting in the Intune admin center, the **Cloud PC performance (preview)** tab, **Cloud PCs with connection quality issues** report, and **Cloud PCs with low utilization** report aren't on the **Overview** page.

**Troubleshooting steps**: Turn off the **Use Devices preview** toggle in the upper right corner of the **Devices** > **Overview** page.

## Cloud PC is stuck in a restart loop after a restore or resize action

**Possible cause**: This issue might occur for Cloud PCs provisioned before July 2022 that use either:

- MSFT Attack Surface Reduction rules (for example, Manage attack surface reduction settings with endpoint security policies in Microsoft Intune | Microsoft Learn), or
- Third party solutions that block the install language script execution during the post-provisioning process.  

Cloud PCs provisioned after July 2022 don’t encounter this issue.

**Troubleshooting steps**: Determine the root cause:

1. Search the Windows Event log. If the system shows the following reboot event (1074), continue to step 2.

  ```
  The process C:\WINDOWS\system32\wbem\wmiprvse.exe (<CPC Name>) has initiated the restart of computer <CPC Name> on behalf of user NT AUTHORITY\SYSTEM for the following reason: Application: Maintenance (Planned)
  Reason Code: 0x80040001
  Shutdown Type: restart
  Comment: DSC is restarting the computer.
  ```

2. Run `Get-DscConfigurationStatus` in an elevated command window. If the result shows a reboot pending for a job, continue to step 3.
3. Run `Get-DscConfiguration` in an elevated command window. If the results show the DSC that installs the language, continue to the **Resolution** section.

**Resolution**: To stop the restart loop, try either of these options:

- Remove the ASR policies, or switch policies to Audit mode, and then apply the new policies to the Cloud PC.
- In an elevated command window, run the following command to reboot the job:

    `Remove-DSCConfiguration -Stage Pending,Current,Previous -Verbose`

## Cloud PC connection issues for GCC High government customers<!--47633105-->

Some GCC High government customers whose resources are deployed to `microsoft.us`` environments may encounter issues connecting to their Cloud PC using web clients or the Safari browser.

**Possible cause**: The issue occurs when the web client or the Safari browser blocks third-party cookies. Third-party cookies are cookies set by a domain other than the one you're visiting.  

For GCC High customers with resources deployed to `microsoft.us` environments, the `microsoft.us` cookies are considered third-party cookies by the web client or the Safari browser. This consideration is because the web client/Safari browser uses the Cloud PC’s domain name, which is different from `microsoft.us`, to determine the first-party domain. If the web client/Safari browser blocks third-party cookies, it prevents the `microsoft.us` cookies from:

- being stored.
- used for authentication and authorization.

As a result, you can’t connect to your Cloud PC session.

**Troubleshooting steps**: Allow third-party cookies from `microsoft.us` in your:

- Web client or Safari browser settings, or
- Group Policy.

This change lets the web client/Safari browser store and use the `microsoft.us` cookies for connecting to your Cloud PC session.  

## Windows Security reports Memory Integrity is off. Your device may be vulnerable.<!--48643259-->

Windows Security reports *Memory Integrity is off. Your device may be vulnerable.*

In the Cloud PC's Windows Systems Information, you might also see that the Virtualization-based security (VBS) row shows **Enabled but not running**.

This issue can be caused when nested virtualization is turned *ON*. When nested virtualization is turned on it requires a running nested hypervisor, which inhibits Direct Memory Access Protections. DMA protections are required when running VBS.

**Troubleshooting steps**:

Make sure that:

- Nested virtualization turned *OFF* for the Cloud PC.
- Policies have VBS enabled with DMA protection.

Another option is to not require DMA for VBS because they're incompatible with each other.

## Teams isn’t enforcing screen capture protection<!-- 49423094 -->

When screen capture protection is enabled, Teams on Windows 365 Cloud PCs isn’t enforcing screen capture protection.

**Troubleshooting steps**:

- Confirm that the WebRTC version is up-to-date.
- Confirm that the screen capture protection policy is configured correctly to have client and server selected:

  1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **Configuration** > choose the policy.
  2. Under  **Configuration settings**, make sure the following is chosen: **Windows Components** > **Remote Desktop Services** > **Remote Desktop Session Host** > **Azure Virtual Desktop**:
      - **Enable screen capture protection** = Enable
      - **Screen Capture Protection Options** = Block screen capture on client and server

## Windows 365 scope tags and nested groups

Windows 365 doesn't support nested security groups. If you apply a scope tag to the top of a nested security group, Cloud PCs in inner nested groups aren't assigned scope tags.

**Troubleshooting steps**:

Apply the scope tag individually to each group in the nested security group.

## Windows 365 doesn't support editing of scope tags for individual Cloud PCs

Windows 365 user interface and Graph API don't support editing of scope tags for individual Cloud PCs.

**Troubleshooting steps**:

Edit scope tags for individual Cloud PCs on Intune's **All Devices** blade to sync the scope tag associations to the Windows 365 service.

## Scope tags for custom images can't be edited

Scope tags applied to custom images can't be edited or directly added by top-level admins.

**Troubleshooting steps**:

When scoped admins create custom images, those custom images are tagged with the same scope tags that are associated with the scoped admin.  

For example, if an admin scoped with the scope tag “Scope Tag A” creates a custom image, the created custom image is automatically tagged with “Scope Tag A”.  

## WebRTC Redirector Service missing from latest Windows 365 Cloud PC gallery images

The May 21, 2024 updates for Cloud PC gallery images are missing the WebRTC Redirector Service. Without this component, Teams media redirection doesn't work.

This applies to the following gallery images:

- Windows 11 23H2 with Microsoft 365 apps
- Windows 11 22H2 with Microsoft 365 apps

**Troubleshooting steps**

For newly provisioned Cloud PCs, verify WebRTC is available. If it’s not, you can use either of the following options:

- To add the WebRTC Redirector Service app to the list of apps to install by default onto Cloud PCs, follow the steps: [Add Microsoft 365 Apps to Windows 10/11 devices with Microsoft Intune](/mem/intune/apps/apps-add-office365).

- To add the WebRTC Redirector Service app to an individual Cloud PC, follow the steps: [install the Remote Desktop WebRTC Redirector Service](/azure/virtual-desktop/teams-on-avd#install-the-remote-desktop-webrtc-redirector-service). To get the most up-to-date installer, use this link: [https://aka.ms/msrdcwebrtcsvc/msi]( https://aka.ms/msrdcwebrtcsvc/msi).

## Next steps

[Troubleshoot Windows 365 Enterprise Cloud PC](troubleshooting.md)
