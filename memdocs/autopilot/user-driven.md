---
title: Windows Autopilot User-Driven Mode
description: With Windows Autopilot user-driven mode, you can configure devices to deploy to a ready-to-use state without requiring help from IT personnel.
keywords: mdm, setup, windows, windows 10, oobe, manage, deploy, autopilot, ztd, zero-touch, partner, msfb, intune
ms.prod: w10
ms.mktglfcycl: deploy
ms.localizationpriority: medium
ms.sitesec: library
ms.pagetype: deploy
audience: itpro
author: aczechowski
ms.author: aaroncz
ms.reviewer: jubaptis
manager: dougeby
ms.date: 09/02/2021
ms.collection:
  - M365-modern-desktop
  - highpri
ms.topic: how-to
---


# Windows Autopilot user-driven mode

**Applies to**

- Windows 10, version 1809 or later
- Windows 11

Windows Autopilot user-driven mode lets you configure new Windows devices to automatically transform them from their factory state to a ready-to-use state. This process doesn't require that IT personnel touch the device.

The process is very simple. Devices can be shipped or distributed to the end user directly with the following instructions:

1. Unbox the device, plug it in, and turn it on.
2. Choose a language (only required when multiple languages are installed), locale, and keyboard.
3. Connect it to a wireless or wired network with internet access. If using wireless, the user must establish the Wi-Fi link.
4. Specify your e-mail address and password for your organization account.

The rest of the process is automated. The device will:

1. Join the organization.
2. Enroll in Intune (or another MDM service)
3. Get configured as defined by the organization.

Any additional prompts during the Out-of-Box Experience (OOBE) can be suppressed; see [Configuring Autopilot Profiles](profiles.md) for options that are available.

> [!IMPORTANT]
> If you are using Active Directory Federation Services (ADFS), there is a [known issue](known-issues.md) that can enable the end user to sign in with a different account than the one that is assigned to that device.

Windows Autopilot user-driven mode supports Azure AD and Hybrid Azure AD joined devices. For more information about these two join options, see [What is a device identity](/azure/active-directory/devices/overview).

The process flow completed during the user-driven process are as follows:

1. After connecting to a network, the device downloads a Windows Autopilot profile. The profile defines the settings used for the device. For example, define the prompts suppressed during OOBE.
2. Windows checks for critical OOBE updates. If updates are available, they're automatically installed (rebooting if necessary).
3. The user is prompted for Azure Active Directory credentials. This customized user experience shows the Azure AD tenant name, logo, and sign-in text.
4.  The device joins Azure Active Directory or Active Directory, depending on the Windows Autopilot profile settings.
5. The device enrolls in Intune (or other configured MDM services). Depending on your organizational needs, this enrollment occurs:
    - during the Azure Active Directory join process using MDM auto-enrollment
    - or before the Active Directory join process.
6. If configured, the [enrollment status page](enrollment-status.md) (ESP) will be displayed.
7. After the device configuration tasks complete, the user is signed into Windows using the credentials they previously provided. (If the device reboots during the device ESP process, the user must reenter their credentials as these details aren't persisted across reboots.)
8. After sign-in, the enrollment status page displays for user-targeted configuration tasks.

If any issues are found during this process, see the [Windows Autopilot Troubleshooting](troubleshooting.md) documentation.

For more information on the available join options, see the following sections:

- [Azure Active Directory join](#user-driven-mode-for-azure-active-directory-join) is available if devices don't need to be joined to an on-prem Active Directory domain.
- [Hybrid Azure Active Directory join](#user-driven-mode-for-hybrid-azure-active-directory-join) is available for devices that must be joined to both Azure Active Directory and your on-prem Active Directory domain.

## User-driven mode for Azure Active Directory join

To complete a user-driven deployment using Windows Autopilot, follow these preparation steps:

1. Make sure that the users who will be performing user-driven mode deployments can join devices to Azure Active Directory. For more information, see [Configure device settings](/azure/active-directory/device-management-azure-portal#configure-device-settings) in the Azure Active Directory documentation.
2. Create an Autopilot profile for user-driven mode with the desired settings. In Microsoft Intune, this mode is explicitly chosen when creating the profile. With Microsoft Store for Business and Partner Center, user-driven mode is the default and doesn't need to be selected.
3. If using Intune, create a device group in Azure Active Directory and assign the Autopilot profile to that group.

For each device that will be deployed using user-driven deployment, these additional steps are needed:

- Make sure that the device has been added to Windows Autopilot. Adding a device to Windows Autopilot can be done in two ways:
  - Automatically by an OEM or partner at the time the device is purchased
  - Manual harvesting as described in [Adding devices to Windows Autopilot](add-devices.md).
- Ensure an Autopilot profile has been assigned to the device:
 - If using Intune and Azure Active Directory dynamic device groups, this assignment can be done automatically.
 - If using Intune and Azure Active Directory static device groups, manually add the device to the device group.
 - If using other methods (for example, Microsoft Store for Business or Partner Center), manually assign an Autopilot profile to the device.

## User-driven mode for hybrid Azure Active Directory join

Windows Autopilot requires that devices be Azure Active Directory joined. If you have an on-premises Active Directory environment, you can join devices to your on-premises domain. To join the devices, you must configure Autopilot devices to be [hybrid-joined to Azure Active Directory (Azure AD)](/azure/active-directory/devices/hybrid-azuread-join-plan). 

### Requirements

To perform a user-driven hybrid Azure AD joined deployment using Windows Autopilot:

- A Windows Autopilot profile for user-driven mode must be created and 
    - **Hybrid Azure AD joined** must be specified as the selected option under **Join to Azure AD as** in the Autopilot profile.
- If using Intune, a device group in Azure Active Directory must exist with the Windows Autopilot profile assigned to that group.
- If using Intune, create and assign a Domain Join profile. A Domain Join configuration profile includes on-premises Active Directory domain information
- The device must be able to access the Internet. For more information, see the Windows Autopilot [networking requirements](networking-requirements.md).
- The Intune Connector for Active Directory must be installed.
    - Note: The Intune Connector will perform an on-prem AD join. Therefore, users don't need on-prem AD-join permission. This assumes the Connector is [configured to perform this action](/intune/windows-autopilot-hybrid#increase-the-computer-account-limit-in-the-organizational-unit) on the user's behalf. 
- If using Proxy, WPAD Proxy settings option must be enabled and configured.

In addition to the core requirements for user driven Hybrid Azure AD Join mentioned above, the following additional requirements apply to an on-prem scenario:

- The device must be running Windows 10, version 1809 or later. 
- The device must have access to an Active Directory domain controller. It must be connected to the organization's network. It must be able to resolve the DNS records for the AD domain and the AD domain controller. It must be able to communicate with the domain controller to authenticate the user.

## User-driven mode for hybrid Azure Active Directory join with VPN support (Preview)

> [!Tip]
> As we talk with our customers that are using Microsoft Endpoint Manager to deploy, manage, and secure their client devices, we often get questions regarding co-managing devices and hybrid Azure Active Directory (Azure AD) joined devices. Many customers confuse these two topics. Co-management is a management option, while Azure AD is an identity option. For more information, see [Understanding hybrid Azure AD and co-management scenarios](https://techcommunity.microsoft.com/t5/microsoft-endpoint-manager-blog/understanding-hybrid-azure-ad-join-and-co-management/ba-p/2221201). This blog post aims to clarify hybrid Azure AD join and co-management, how they work together, but aren't the same thing.
>
> You can't deploy the Configuration Manager client while provisioning a new computer in Windows Autopilot user-driven mode for hybrid Azure AD join. This limitation is due to the identity change of the device during the Azure AD-join process. Deploy the Configuration Manager client after the Autopilot process. See [Client installation methods in Configuration Manager](../configmgr/core/clients/deploy/plan/client-installation-methods.md) for alternative options for installing the client.<!-- CMADO-10205503 -->

Devices joined to Active Directory require connectivity to an Active Directory domain controller for many activities. These activities include user sign-in (validating the user's credentials) and Group Policy application. As a result, the Windows Autopilot user-driven Hybrid Azure AD Join process would validate that the device is able to contact an Active Directory domain controller by pinging that domain controller.

With the addition of VPN support for this scenario, you can configure the Hybrid Azure AD Join process to skip the connectivity check. This doesn't eliminate the need for communicating with an Active Directory domain controller. Instead, to allow connection to the organization's network, Intune delivers the needed VPN configuration before the user attempts to sign in to Windows. 

### Requirements

In addition to the core requirements for user driven hybrid Azure AD join mentioned above, the following additional requirements apply to a remote scenario of Hybrid Azure AD Join with VPN support:

- A supported version of Windows:
  - Windows 10 version 1903 + December 10 Cumulative update (KB4530684, OS build 18362.535) or higher
  - Windows 10 version 1909 + December 10 Cumulative update (KB4530684, OS build 18363.535) or higher
  - Windows 10 version 2004 or later
  - Windows 11
- Enable the **Skip domain connectivity check** toggle in the Hybrid Azure AD Join Autopilot profile.
- A VPN configuration that:
  - Can be deployed with Intune and lets the user manually establish a VPN connection from the Windows logon screen, or
  - One that automatically establishes a VPN connection as needed.

The specific VPN configuration required depends on the VPN software and authentication being used. For third-party (non-Microsoft) VPN solutions, this typically would involve deploying a Win32 app (containing the VPN client software itself and any specific connection information, for example: VPN endpoint host names) via Intune Management Extensions. Consult your VPN provider's documentation for configuration details specific to that provider.

> [!NOTE]
> The VPN requirements aren't specific to Windows Autopilot. For example, if you have already implemented a VPN configuration to enable remote password resets, where a user needs to log on to Windows with a new password when not on the organization's network, that same configuration can be used with Windows Autopilot. Once the user has signed in to cache their credentials, subsequent log-on attempts don't need connectivity since the cached credentials can be used. 

In cases where certificate authentication is required by the VPN software, the needed machine certificate should also be deployed via Intune. This deployment can be done using the Intune certificate enrollment capabilities, targeting the certificate profiles to the device.

User certificates aren't supported because they can't be deployed until the user logs in. Also, because they aren't installed until after the user signs in, non-Microsoft UWP VPN plug-ins delivered from the Windows Store aren't supported.

### Validation

Before you attempt a hybrid Azure AD Join using VPN, it's important to confirm that a user-driven Hybrid Azure AD Join process can be performed on the organization's network. This confirmation simplifies troubleshooting by making sure the core process works before adding the additional VPN configuration required.

Next, validate that the VPN configuration (Win32 app, certs, and any other requirements) can be deployed using Intune to an existing device that has already been hybrid Azure AD joined. For example, some VPN clients create a per-machine VPN connection as part of the installation process. So, you can validate the configuration using steps like these:

- From PowerShell, verify that at least one per-machine VPN connection has been created using the "Get-VpnConnection -AllUserConnection" command.
- Attempt to manually start the VPN connection using the command: RASDIAL.EXE "ConnectionName"
- Log out and verify that the "VPN connection" icon can be seen on the Windows logon page.
- Move the device off the corporate network and try to establish the connection using the icon on the Windows logon page. Sign into an account that doesn't have cached credentials.

For VPN configurations that automatically connect, the validation steps may be different.

> [!NOTE]
> Always On VPN can be used for this scenario. For more information, see the [Deploy Always On VPN](/windows-server/remote/remote-access/vpn/always-on-vpn/deploy/always-on-vpn-deploy-deployment) documentation. Note that Intune can't yet deploy the needed per-machine VPN profile.

To validate the process, ensure the needed Windows 10 cumulative update has been installed on Windows 10 1903 or Windows 10 1909. You can manually install the update during OOBE by first downloading the latest cumulative from https://catalog.update.microsoft.com. Follow these steps:

1. Press Shift-F10 to open a command prompt.
2. Insert a USB key containing the downloaded update.
3. Install the update using the command (substituting the real file name): WUSA.EXE _filename_.msu /quiet
4. Reboot the computer using the command: shutdown.exe /r /t 0

Or, you can start Windows Update to install the latest updates:

1. Press Shift-F10 to open a command prompt.
2. Run the command "start ms-settings:"
3. Navigate to the "Update & Security" node and check for updates.
4. Reboot after the updates are installed.

### Step-by-step instructions

[Deploy hybrid Azure AD joined devices using Intune and Windows Autopilot](windows-autopilot-hybrid.md)

## Related topics

[Trying Out Autopilot Hybrid Join Over VPN In Your Azure Lab](https://techcommunity.microsoft.com/t5/core-infrastructure-and-security/trying-out-autopilot-hybrid-join-over-vpn-in-your-azure-lab/ba-p/1606723)
