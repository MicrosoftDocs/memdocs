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
ms.date: 03/21/2022
ms.collection:
  - M365-modern-desktop
  - highpri
ms.topic: how-to
---


# Windows Autopilot user-driven mode

**Applies to**

Currently supported versions of:

- Windows 10
- Windows 11

Windows Autopilot user-driven mode lets you configure new Windows devices to automatically transform them from their factory state to a ready-to-use state. This process doesn't require that IT personnel touch the device.

The process is simple. Devices can be shipped or distributed to the end user directly with the following instructions:

1. Unbox the device, plug it in, and turn it on.
2. If it uses multiple languages, choose a language, locale, and keyboard.
3. Connect it to a wireless or wired network with internet access. If using wireless, first connect to the wi-fi network.
4. Specify your e-mail address and password for your organization account.

The rest of the process is automated. The device does the following steps:

1. Join the organization.
2. Enroll in Microsoft Intune or another MDM service.
3. Get configured as defined by the organization.

You can suppress any other prompts during the out-of-box experience (OOBE). For more information on the available options, see [Configuring Autopilot profiles](profiles.md).

> [!IMPORTANT]
> If you use Active Directory Federation Services (ADFS), there's a [known issue](known-issues.md) that can enable the end user to sign in with a different account than the one that's assigned to that device.

Windows Autopilot user-driven mode supports Azure Active Directory (Azure AD) and hybrid Azure AD-joined devices. For more information about these two join options, see [What is a device identity](/azure/active-directory/devices/overview).

The steps of the user-driven process are as follows:

1. After connecting to a network, the device downloads a Windows Autopilot profile. The profile defines the settings used for the device. For example, define the prompts suppressed during OOBE.

1. Windows checks for critical OOBE updates. If updates are available, they're automatically installed. If necessary, the device restarts.

1. The user is prompted for Azure AD credentials. This customized user experience shows the Azure AD tenant name, logo, and sign-in text.

1. The device joins Azure AD or Active Directory, depending on the Windows Autopilot profile settings.

1. The device enrolls to Intune or another configured MDM service. Depending on your organizational needs, this enrollment occurs either:

    - During the Azure AD-join process using MDM auto-enrollment.

    - Before the Active Directory-join process.

1. If configured, it displays the [enrollment status page](enrollment-status.md) (ESP).

1. After the device configuration tasks complete, the user is signed into Windows using the credentials they previously provided. If the device restarts during the device ESP process, the user must reenter their credentials. These details don't persist after restart.

1. After sign-in, the enrollment status page displays for user-targeted configuration tasks.

If any issues are found during this process, see [Windows Autopilot troubleshooting](troubleshooting.md).

For more information on the available join options, see the following sections:

- [Azure AD join](#user-driven-mode-for-azure-ad-join) is available if devices don't need to join an on-premises Active Directory domain.
- [Hybrid Azure AD join](#user-driven-mode-for-hybrid-azure-ad-join) is available for devices that need to join both Azure AD and your on-premises Active Directory domain.

## User-driven mode for Azure AD join

To complete a user-driven deployment using Windows Autopilot, follow these preparation steps:

1. Make sure that the users who will be performing user-driven mode deployments can join devices to Azure AD. For more information, see [Configure device settings](/azure/active-directory/devices/device-management-azure-portal#configure-device-settings) in the Azure AD documentation.

1. Create an Autopilot profile for user-driven mode with the desired settings.

    - In Intune, this mode is explicitly chosen when you create the profile.

    - In Microsoft Store for Business and Partner Center, user-driven mode is the default.

1. If you use Intune, create a device group in Azure AD, and assign the Autopilot profile to that group.

For each device that you'll deploy using user-driven deployment, these extra steps are needed:

- Add the device to Windows Autopilot. You can do this step in two ways:

  - Automatically by an OEM or partner when you purchase the device.

  - Manually as described in [Adding devices to Windows Autopilot](add-devices.md).

- Assign an Autopilot profile to the device:

  - If you use Intune and Azure AD dynamic device groups, this assignment can be done automatically.

  - If you use Intune and Azure AD static device groups, manually add the device to the device group.

  - If you use other methods, like Microsoft Store for Business or Partner Center, manually assign an Autopilot profile to the device.

> [!TIP]
> If the intended end-state of the device is co-management, you can configure device enrollment in Intune to enable co-management, which happens during the Autopilot process. This behavior directs the workload authority in an orchestrated manner between Configuration Manager and Intune. For more information, see [How to enroll with Autopilot](../configmgr/comanage/autopilot-enrollment.md).<!-- Intune 11300628 -->

## User-driven mode for hybrid Azure AD join

Windows Autopilot requires that devices be Azure AD-joined. If you have an on-premises Active Directory environment, you can join devices to your on-premises domain. To join the devices, configure Autopilot devices to be [hybrid-joined to Azure AD](/azure/active-directory/devices/hybrid-azuread-join-plan).

> [!Tip]
> As we talk with our customers that are using Microsoft Endpoint Manager to deploy, manage, and secure their client devices, we often get questions regarding co-managing devices and hybrid Azure AD-joined devices. Many customers confuse these two topics. Co-management is a management option, while Azure AD is an identity option. For more information, see [Understanding hybrid Azure AD and co-management scenarios](https://techcommunity.microsoft.com/t5/microsoft-endpoint-manager-blog/understanding-hybrid-azure-ad-join-and-co-management/ba-p/2221201). This blog post aims to clarify hybrid Azure AD join and co-management, how they work together, but aren't the same thing.
>
> You can't deploy the Configuration Manager client while provisioning a new computer in Windows Autopilot user-driven mode for hybrid Azure AD join. This limitation is due to the identity change of the device during the Azure AD-join process. Deploy the Configuration Manager client after the Autopilot process. See [Client installation methods in Configuration Manager](../configmgr/core/clients/deploy/plan/client-installation-methods.md) for alternative options for installing the client.<!-- CMADO-10205503 -->

### Requirements for user-driven mode with hybrid Azure AD

- Create a Windows Autopilot profile for user-driven mode.

  In the Autopilot profile, under **Join to Azure AD as**, select **Hybrid Azure AD joined**.

- If you use Intune, you need a device group in Azure AD. Assign the Windows Autopilot profile to the group.

- If you use Intune, create and assign a Domain Join profile. A Domain Join configuration profile includes on-premises Active Directory domain information.

- The device needs to access the internet. For more information, see the [networking requirements](networking-requirements.md).

- Install the Intune Connector for Active Directory.

  > [!NOTE]
  > The Intune Connector joins the device to the on-premises domain. Users don't need permissions to join devices to the on-premises domain. This behavior assumes that you configure the connector for this action on the user's behalf. For more information, see [Increase the computer account limit in the Organizational Unit](windows-autopilot-hybrid.md#increase-the-computer-account-limit-in-the-organizational-unit).

- If you use a proxy, enable and configure the WPAD Proxy settings option.

In addition to these core requirements for user-driven hybrid Azure AD-join, the following extra requirements apply to on-premises devices:

- The device has a supported version of Windows 10 or Windows 11.

- The device is connected to the internal network and has access to an Active Directory domain controller.

  - It needs to resolve the DNS records for the domain and the domain controllers.

  - It needs to communicate with the domain controller to authenticate the user.

### User-driven mode for hybrid Azure AD join with VPN support (preview)

Devices joined to Active Directory require connectivity to an Active Directory domain controller for many activities. These activities include validating the user's credentials when they sign-in, and applying group policy settings. The Autopilot user-driven process for hybrid Azure AD-joined devices validates that the device can contact a domain controller by pinging that domain controller.

With the addition of VPN support for this scenario, you can configure the hybrid Azure AD join process to skip the connectivity check. This change doesn't eliminate the need for communicating with a domain controller. Instead, to allow connection to the organization's network, Intune delivers the needed VPN configuration before the user attempts to sign in to Windows.

#### Requirements for user-driven mode with hybrid Azure AD and VPN

In addition to the [core requirements](#requirements-for-user-driven-mode-with-hybrid-azure-ad) for user-driven mode with hybrid Azure AD join, the following extra requirements apply to a remote scenario with VPN support:

- A supported version of Windows 10 or Windows 11.

- In the hybrid Azure AD join profile for Autopilot, enable the following option: **Skip domain connectivity check**.

- A VPN configuration with one of the following options:

  - Can be deployed with Intune, and lets the user manually establish a VPN connection from the Windows sign-in screen.

  - Automatically establishes a VPN connection as needed.

The specific VPN configuration required depends on the VPN software and authentication being used. For third-party VPN solutions, this configuration typically involves deploying a Win32 app via Intune Management Extensions. This app would include the VPN client software and any specific connection information. For example, VPN endpoint host names. For configuration details specific to that provider, see your VPN provider's documentation.

> [!NOTE]
> The VPN requirements aren't specific to Autopilot. For example, if you've already implemented a VPN configuration to enable remote password resets, that same configuration can be used with Windows Autopilot. This configuration would allow a user to sign in to Windows with a new password when not on the organization's network. Once the user has signed in to cache their credentials, subsequent sign-in attempts don't need connectivity since Windows uses the cached credentials.

If the VPN software requires certificate authentication, use Intune to also deploy the required device certificate. This deployment can be done using the Intune certificate enrollment capabilities, targeting the certificate profiles to the device.

Some configurations aren't supported because they aren't applied until the user signs into Windows:

- User certificates
- Non-Microsoft UWP VPN plug-ins from the Windows Store

#### Validation

Before you attempt a hybrid Azure AD join using VPN, it's important to confirm that a user-driven mode for hybrid Azure AD join process works on your internal network. This test simplifies troubleshooting by making sure the core process works before adding the VPN configuration.

Next, confirm that you can use Intune to deploy the VPN configuration and its requirements. Test these components with an existing device that's already hybrid Azure AD-joined. For example, some VPN clients create a per-machine VPN connection as part of the installation process. Validate the configuration using the following steps:

1. Verify that at least one per-machine VPN connection has been created.

    ```powershell
    Get-VpnConnection -AllUserConnection
    ```

1. Attempt to manually start the VPN connection.

    ```command
    RASDIAL.EXE "ConnectionName"
    ```

1. Sign out of Windows. Verify that you can see the "VPN connection" icon on the Windows sign-in page.

1. Move the device off the internal network and try to establish the connection using the icon on the Windows sign-in page. Sign into an account that doesn't have cached credentials.

For VPN configurations that automatically connect, the validation steps may be different.

> [!NOTE]
> You can use an always-on VPN for this scenario. For more information, see [Deploy always-on VPN](/windows-server/remote/remote-access/vpn/always-on-vpn/deploy/always-on-vpn-deploy-deployment).
>
> Intune can't currently deploy this per-machine VPN profile.

## Next steps

[Deploy hybrid Azure AD joined devices using Intune and Windows Autopilot](windows-autopilot-hybrid.md)

[How to enroll with Autopilot](../configmgr/comanage/autopilot-enrollment.md)

[Try out Autopilot hybrid join over VPN in your Azure lab](https://techcommunity.microsoft.com/t5/core-infrastructure-and-security/trying-out-autopilot-hybrid-join-over-vpn-in-your-azure-lab/ba-p/1606723)
