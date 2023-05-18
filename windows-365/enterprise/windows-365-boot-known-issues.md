---
# required metadata
title: Windows 365 Boot known issues
titleSuffix:
description: Learn about known issues with Windows 365 Boot, including workarounds and updated fixes.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 5/24/2023
ms.topic: troubleshooting
ms.service: windows-365
ms.subservice: 
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: elluthra
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection:
- M365-identity-device-management
- tier2
---

# Windows 365 Boot known issues

This page lists recent known issues with [Windows 365 Boot](windows-365-boot-overview.md).

## Other sign-in options besides username/password are displayed on the sign-in screen

Windows 365 Boot is used with the Shared PC configuration service provider (CSP). This CSP doesn't support sign-in methods other than username/password.

**Troubleshooting steps**:

If you have Windows Hello for Business enabled for the Windows 365 Boot device, you can use Intune to disable it. For more information, see [Enable security keys for Windows sign-in](/azure/active-directory/authentication/howto-authentication-passwordless-security-key-windows#enable-security-keys-for-windows-sign-in).

If the Windows 365 Boot physical device lets users sign in using a convenience PIN, you can turn it off. For more information, see [AllowPINLogon](/windows/client-management/mdm/policy-csp-credentialproviders#allowpinlogon).

## Default credential provider is set to Security Key on the sign-in screen

When the **Use security keys for sign-in** policy setting enabled, it can be configured to be the default credential provider. This policy might result in the user seeing a sign-in for the physical device.  

**Troubleshooting steps**: Check to see if you have this policy setting configured in Intune. For more information on how to check, see [Enable security keys for Windows sign-in](/azure/active-directory/authentication/howto-authentication-passwordless-security-key-windows#enable-security-keys-for-windows-sign-in).

If it's set, exclude your Windows 365 Boot devices from the policy.

## Local device has background apps and previous policy configurations that impact the user’s Windows 365 Boot experience

Windows 365 Boot uses “clean” Windows 11 devices that don't have preconfigured applications or policies assigned to the device.  

**Troubleshooting steps**: Reset the device to a clean state. For more information, see [Windows 365 Boot physical device requirements](windows-365-boot-physical-device-requirements.md).

## Single sign-on users see a dialog to allow remote desktop connection during the connection attempt

When using single sign-on, users are prompted to authenticate to Azure Active Directory (Azure AD) and allow the Remote Desktop connection when launching a connection to a new Cloud PC. Azure AD remembers up to 15 devices for 30 days before prompting again.

**Troubleshooting steps**: If you see this dialog, select **Yes** to connect.

## User can't launch the web browser to sign-in to WI-FI network

Windows 365 Boot is designed for Ethernet connections or WiFi connections managed through the [WiFI CSP](/windows/client-management/mdm/wifi-csp).

**Troubleshooting steps**: Configure the Windows 365 Boot physical device's Wi-Fi profile through Intune. For more information, see [Add Wi-Fi settings for Windows 10/11 devices in Intune](/mem/intune/configuration/wi-fi-settings-windows).

## User sees black screen after using Disconnect/Sign-out/Lock command from Cloud PC

This known issue is under investigation.

**Troubleshooting steps**: Use the Ctrl-Alt-Del shortcut and selecting the **Sign out** option.

## Microsoft Teams calls have poor performance

**Troubleshooting steps**: Make sure Teams optimizations are used as explained in [Microsoft Teams on Cloud PC](teams-on-cloud-pc.md).

## Camera access is denied in Cloud PC

Camera permissions must be granted to the Azure Virtual Desktop (HostApp) application to use your Windows 365 Boot configured device’s camera in Microsoft Teams.

**Troubleshooting steps**:

1. [Remove Windows 365 from the physical device](troubleshoot-windows-365-boot.md#remove-windows-365-boot-from-the-physical-device).
2. On the physical device, open **Settings** > **Privacy & Security** > **Camera** > **Let apps access your camera**.
3. Set **Azure Virtual Desktop (HostApp)** to **On**.
4. [Add Windows 365 Boot back onto the physical device](troubleshoot-windows-365-boot.md#add-windows-365-boot-back-onto-the-physical-device).

## Users can still interact with physical device features like Settings, Task Manager, and Notifications

During [public preview](../public-preview.md), users are mostly unable to access features on their Windows 365 Boot physical devices. However, to assist with troubleshooting, some features aren't blocked.

**Troubleshooting steps**: To learn how to restrict user access to the physical device, see [Restrict user access to Windows 365 Boot physical device](windows-365-boot-restrict-user-access-physical-device.md).

## Users are disconnected from Cloud PC after being idle for too long

 Windows 365 Boot physical devices might sign out users because of screen idle policies applied to the physical device or Cloud PC.

**Troubleshooting steps**: Using an Intune device configuration profile, change or configure the [DeviceLock CSP policy (MaxInactivityTimeDeviceLock)](/windows/client-management/mdm/policy-csp-devicelock?WT.mc_id=Portal-fx#maxinactivitytimedevicelock). Make these changes for both the physical device and the Cloud PC.

## Users see multiple authentication dialogs despite single sign-on being enabled

**Troubleshooting steps**: Check the Windows 365 Provisioning policy associated with the Cloud PC to see if single sign-on is enabled. If it isn't, enable single sign-on for the provisioning policy. This policy change requires reprovisioning the Cloud PC.

Your Conditional Access policies might also be causing other authentication dialogs. For more information, see [Troubleshooting sign-in problems with Conditional Access](/azure/active-directory/conditional-access/troubleshoot-conditional-access).

When using single sign-on, users are prompted to:

- Authenticate to Azure AD
- Allow the Remote Desktop connection when launching a connection to a new Cloud PC.

Azure AD remembers up to 15 devices for 30 days before prompting again.

If you see this dialog, select **Yes** to connect.

## Users see a black screen after sign-on

Windows 365 Boot is configured by using the [CloudDesktop CSP](/windows/client-management/mdm/policy-csp-clouddesktop#boottocloudmode).

**Troubleshooting steps**: If you configured your device for Windows 365 Boot using the [Windows 365 Boot Guided Scenario](windows-365-boot-guide.md):

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Devices** > **Policy** > **Policy sets** > **Manage** > **Policy sets**.
2. Search for the policy sets whose names contain “Boot To Cloud Policy Set”.  One of the results is the policy associated with the Windows 365 Boot device.
3. In the **Device management properties** section, select the Device configuration profile that contains “Boot to Cloud Device Configuration Policy”.
4. Make sure that the “Cloud Desktop” configuration is configured with the **Boot to Cloud Mode** setting set to **Enable Boot to Cloud Desktop**.
5. Select **Device assignment status** and make sure that the configuration policy has been successfully applied to it.
6. If the check-in status isn't successful, see [Troubleshooting policies and profiles in Microsoft Intune](/troubleshoot/mem/intune/device-configuration/troubleshoot-policies-in-microsoft-intune).

If the problem persists, reinstall the physical device's operating system as explained in [Windows 365 Boot physical device requirements](windows-365-boot-physical-device-requirements.md).

## User sees local PC desktop when responding to authentication dialogs

Windows 365 Boot is configured through the [Windowslogon CSP](/windows/client-management/mdm/policy-csp-windowslogon#overrideshellprogram).

**Troubleshooting steps**: If you configured your device for Windows 365 Boot using the [Windows 365 Boot Guided Scenario](windows-365-boot-guide.md):

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Devices** > **Policy** > **Policy sets** > **Manage** > **Policy sets**.
2. Search for the policy sets whose names contain “Boot To Cloud Policy Set”.  One of the results is the policy associated with the Windows 365 Boot device.
3. In the **Device management properties** section, select the Device configuration profile that contains “Boot to Cloud Device Configuration Policy”.
4. Make sure that the "Windows Logon" configuration is configured with the **Override Shell Program** setting set to **Apply Lightweight shell**.
5. Select **Device assignment status** and make sure that the configuration policy has been successfully applied to it.
6. If the check-in status isn't successful, see [Troubleshooting policies and profiles in Microsoft Intune](/troubleshoot/mem/intune/device-configuration/troubleshoot-policies-in-microsoft-intune).

If the problem persists, reinstall the physical device's operating system as explained in [Windows 365 Boot physical device requirements](windows-365-boot-physical-device-requirements.md).

## Error message: Windows 365 cannot connect to the resources it uses to run properly

**Troubleshooting steps**: Check your device’s network connection and try again. If you're using an Azure network connection (ANC) for your Cloud PC, check the ANC status as explained in [Azure network connection status](/windows-365/enterprise/health-checks#azure-network-connection-status).

For more information, see [Troubleshoot Cloud PC connection errors](/windows-365/enterprise/connection-errors).

## Error message: Something is preventing you from using the Windows 365 app” error message

**Troubleshooting steps**: See [Troubleshoot Windows 365 Boot](troubleshoot-windows-365-boot.md).

## User can't connect to their Cloud PC and continues to wait at the transition screen

**Troubleshooting steps**: Make sure that the device has applications that support Windows 365 Boot.

If the applications meet the minimum version requirements, collect diagnostic logs and [contact Microsoft support](troubleshoot-windows-365-boot.md#contact-microsoft-support).

## Error message: Remote Desktop Gateway server is temporarily unavailable

**Troubleshooting steps**: This issue might be a transient issue because of network congestion. Try signing in again after waiting some time. If the issue persists, collect diagnostic logs and [contact Microsoft support](troubleshoot-windows-365-boot.md#contact-microsoft-support).

## Error message: You need to be assigned a Cloud PC

Windows 365 Boot requires users to have a Windows 365 Cloud PC provisioned for them.

**Troubleshooting steps**: Create and assign a Windows 365 provisioning policy. For more information, see [Create provisioning policies](/windows-365/enterprise/create-provisioning-policy).

## When users sign into a device for the first time, they see an error screen

This known issue is related to application registration that is under investigation.

**Troubleshooting steps**: Users should try logging in a second time on the device. In most instances, they should be able to connect to their Windows 365 Cloud PC. If they still see the error screen, contact Microsoft support with the displayed correlation ID.

## Resources created by the Windows 365 Boot guided scenario are showing as “not applicable” in Intune

Resources created by the Windows 365 Boot guided scenario can be applied to both:

- Azure AD joined devices
- hybrid Azure AD joined devices in tenants where certain workloads have been switched to Intune. For hybrid Azure AD joined devices, Windows Update policies, device configuration, and client apps workloads must be switched to Intune.

**Troubleshooting steps**: To determine if your device is hybrid Azure AD joined, see [Using the Azure portal](/azure/active-directory/devices/howto-hybrid-join-verify#using-the-azure-portal). If your device is hybrid Azure AD joined, see [Co-management workloads](/mem/configmgr/comanage/workloads) to see what workloads are configured in your environment.

<!-- ########################## -->
## Next steps

[Troubleshoot Windows 365 Boot](troubleshoot-windows-365-boot.md).
