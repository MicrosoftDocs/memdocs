---
# required metadata
title: Encrypt Windows devices with BitLocker in Intune 
titleSuffix: Microsoft Intune
description: Use policy from Microsoft Endpoint Manager admin center to encrypt devices with the BitLocker built-in encryption method, and manage the recovery keys for those encrypted devices.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/01/2022
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high

# optional metadata
#audience:
ms.reviewer: annovich
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: 
  - M365-identity-device-management
  - highpri
---

# Manage BitLocker policy for Windows devices with Intune

Use Intune to configure BitLocker Drive Encryption on devices that run Windows 10/11.

BitLocker is available on devices that run Windows 10/11. Some settings for BitLocker require the device have a supported TPM.

Use one of the following policy types to configure BitLocker on your managed devices:

- **[Endpoint security disk encryption policy for BitLocker](#create-an-endpoint-security-policy-for-bitlocker)**. The BitLocker profile in *Endpoint security* is a focused group of settings that is dedicated to configuring BitLocker.

  View the BitLocker settings that are available in [BitLocker profiles from disk encryption policy](../protect/endpoint-security-disk-encryption-profile-settings.md#bitlocker).

- **[Device configuration profile for endpoint protection for BitLocker](#create-an-endpoint-security-policy-for-bitlocker)**. BitLocker settings are one of the available settings categories for Windows 10/11 endpoint protection.

  View the BitLocker settings that are available for [BitLocker in endpoint protection profiles from device configuration policy](../protect/endpoint-protection-windows-10.md#windows-settings).

> [!TIP]
> Intune provides a built-in [encryption report](encryption-monitor.md) that presents details about the encryption status of devices, across all your managed devices. After Intune encrypts a Windows device with BitLocker, you can view and manage BitLocker recovery keys when you view the encryption report.
>
> You can also access important information for BitLocker from your devices, as found in Azure Active Directory (Azure AD).

## Permissions to manage BitLocker

To manage BitLocker in Intune, your account must have the applicable Intune [role-based access control](../fundamentals/role-based-access-control.md) (RBAC) permissions.

Following are the BitLocker permissions, which are part of the Remote tasks category, and the built-in RBAC roles that grant the permission:

- **Rotate BitLocker Keys**
  - Help Desk Operator

## Create and deploy policy

Use one of the following procedures to create the policy type you prefer.

### Create an endpoint security policy for BitLocker

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Endpoint security** > **Disk encryption** > **Create Policy**.

3. Set the following options:
   1. **Platform**: Windows 10/11
   2. **Profile**: BitLocker

   ![Select the BitLocker profile](./media/encrypt-devices/select-windows-bitlocker-es.png)

4. On the **Configuration settings** page, configure settings for BitLocker to meet your business needs.  

   Select **Next**.

5. On the **Scope (Tags)** page, choose **Select scope tags** to open the Select tags pane to assign scope tags to the profile.

   Select **Next** to continue.

6. On the **Assignments** page, select the groups that will receive this profile. For more information on assigning profiles, see Assign user and device profiles.

   Select **Next**.

7. On the **Review + create** page, when you're done, choose **Create**. The new profile is displayed in the list when you select the policy type for the profile you created.

### Create a device configuration profile for BitLocker

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Devices** > **Configuration profiles** > **Create profile**.

3. Set the following options:
   1. **Platform**: Windows 10/11
   2. **Profile type**: Endpoint protection

   ![Select your BitLocker profile](./media/encrypt-devices/select-windows-bitlocker-dc.png)

4. On the **Configuration settings** page, expand **Windows Encryption**.

   :::image type="content" source="./media/encrypt-devices/bitlocker-settings.png" alt-text="Select Windows encryption settings":::

5. Configure settings for BitLocker to meet your business needs.

   If you want to enable BitLocker silently, see [Silently enable BitLocker on devices](#silently-enable-bitlocker-on-devices), in this article for additional prerequisites and the specific setting configurations you must use.

6. Select **Next** to continue.

7. Complete configuration of additional settings, and then save the profile.

## Manage BitLocker

To view information about devices that receive BitLocker policy, see [Monitor disk encryption](../protect/encryption-monitor.md). 

### Silently enable BitLocker on devices

You can configure a BitLocker policy to automatically and silently enable BitLocker on a device. That means that BitLocker enables successfully without presenting any UI to the end user, even when that user isn't a local Administrator on the device. You can use either the BitLocker profile from an endpoint security disk encryption policy, or the endpoint protection template from a device configuration policy.

Devices must meet the following prerequisites, receive applicable settings to silently enable BitLocker, and not have incompatible settings for TPM startup PIN or key.

#### Device Prerequisites

A device must meet the following conditions to be eligible for silently enabling BitLocker:

- If end users sign in to the devices as Administrators, the device must run Windows 10 version 1803 or later, or Windows 11.
- If end users sign in to the devices as Standard Users, the device must run Windows 10 version 1809 or later, or Windows 11.
- The device must be Azure AD Joined or Hybrid Azure AD Joined.
- Device must contain at least TPM (Trusted Platform Module) 1.2.
- The BIOS mode must be set to Native UEFI only.

#### Required settings to silently enable BitLocker

Depending on the type of policy that you use to silently enable BitLocker, configure the following settings.

**Endpoint security disk encryption policy** - Configure the following settings in the BitLocker profile:

- **Hide prompt about third-party encryption** = *Yes*
- **Alow standard users to enable encryption during Autopilot** = *Yes*

**Device configuration policy** - Configure the following settings in the *Endpoint protection* template or a *custom settings* profile:

- **Warning for other disk encryption** = *Block*.
- **Allow standard users to enable encryption during Azure AD Join** = *Allow*

> [!TIP]  
> While the setting labels and options in the following two policy types are different from each other, they both apply the same configuration to Windows encryption CSPs that manage BitLocker on Windows devices.

### Full disk vs Used Space only encryption 

Three settings determine whether an OS drive will be encrypted using used space only or full disk encryption:
- Whether the hardware of the device is [modern standby](/windows-hardware/design/device-experiences/modern-standby) capable
- Whether silent enablement has been configured for BitLocker 
  - ('Warning for other disk encryption' = Block or 'Hide prompt about third-party encryption' = Yes)
- Configuration of the [SystemDrivesEncryptionType](/windows/client-management/mdm/bitlocker-csp) 
  - (Enforce drive encryption type on operating system drives)

Assuming that SystemDrivesEncryptionType has not been configured, the following is the expected behaviour. When silent enablement is configured on a modern standby device, the OS drive will be encrypted using used space only encryption. When silent enablement is configured on a device which is not capable of modern standby, the OS drive will be encrypted using full disk encryption. The result is the same whether you are using an [Endpoint Security disk encryption policy for BitLocker](#create-an-endpoint-security-policy-for-bitlocker) or a [Device Configuration profile for endpoint protection for BitLocker](#create-an-endpoint-security-policy-for-bitlocker). If a different end state is required, the encryption type can be controlled by configuring the SystemDrivesEncryptionType using settings catalog as shown below.

To verify whether the hardware is modern standby capable, run the following command from a command prompt:

```console
powercfg /a
```
If the device supports modern standby, it will show that Standby (S0 Low Power Idle) Network Connected is available

:::image type="content" source="./media/encrypt-devices/docs_bl_powercfg_surface_s0_possible.png" alt-text="Screenshot of command prompt displaying output of powercfg command with Standby state S0 available.":::

If the device does not support modern standby, such as a virtual machine, it will show that Standby (S0 Low Power Idle) Network Connected is not supported

:::image type="content" source="./media/encrypt-devices/docs_bl_powercfg_surface_nos0possible.png" alt-text="Screenshot of command prompt displaying output of powercfg command with Standby state S0 un-available.":::

To verify the encryption type, run the following command from an elevated (admin) command prompt:

```console
manage-bde -status c:
```
The 'Conversion Status' field will reflect the encryption type as either Used Space Only encrypted or Fully Encrypted.

:::image type="content" source="./media/encrypt-devices/docs_bl_usedspaceonly.png" alt-text="Screenshot of administrative command prompt showing output of manage-bde with conversion status reflecting fully encrypted.":::

:::image type="content" source="./media/encrypt-devices/docs_bl_fullyencrypted.png" alt-text="Screenshot of administrative command prompt showing output of manage-bde with conversion status reflecting used space only encryption.":::

To change the disk encryption type between full disk encryption and used space only encryption, leverage the'Enforce drive encryption type on operating system drives' setting within settings catalog.

:::image type="content" source="./media/encrypt-devices/docs_bl_settingscatalog_control_encryption.png" alt-text="Screenshot of Intune settings catalog displaying Enforce drive encryption type on operating system drives setting and drop-down list to select from full or used space only encryption types.":::

#### TPM startup PIN or key

A device **must not require** use of a startup PIN or startup key.

When a TPM startup PIN or startup key is required on a device, BitLocker can't silently enable on the device and instead requires interaction from the end user. Settings to configure the TPM startup PIN or key are available in both the endpoint protection template and the BitLocker policy. By default, these policies do not configure these settings.

Following are the relevant settings for each profile type:

**Endpoint security disk encryption policy** - In the BitLocker profile you'll find the following settings in the *BitLocker - OS Drive Settings* category when *BitLocker system drive policy* is set to *Configure*, and then *Startup authentication required* is set to *Yes*.

- **Compatible TPM startup** - Configure this as *Allowed* or *Required*
- **Compatible TPM startup PIN** - Configure this as *Blocked*
- **Compatible TPM startup key** - Configure this as *Blocked*
- **Compatible TPM startup key and PIN** - Configure this as *Blocked*

**Device configuration policy** - In the endpoint protection template you'l find the following settings in the *Windows Encryption* category:

- **Compatible TPM startup** - Configure this as *Allow TPM* or *Require TPM*
- **Compatible TPM startup PIN** - Configure this as *Do not allow startup PIN with TPM*
- **Compatible TPM startup key** - Configure this as *Do not allow startup Key with TPM*
- **Compatible TPM startup key and PIN** - Configure this as *Do not allow startup Key and PIN with TPM*

> [!WARNING]  
> While neither the endpoint security or device configuration policies configure the TPM settings by default, some versions of the [security baseline for Microsoft Defender for Endpoint](../protect/security-baselines.md#available-security-baselines) will configure both *Compatible TPM startup PIN* and *Compatible TPM startup key* by default. These configurations might block silent enablement of BitLocker.
>
> If you deploy this baseline to devices on which you want to silently enable BitLocker, review your baseline configurations for possible conflicts. To remove conflicts, either reconfigure the settings in the baselines to remove the conflict, or remove applicable devices from receiving the baseline instances that configure TPM settings that block silent enablement of BitLocker.

### View details for recovery keys

Intune provides access to the Azure AD blade for BitLocker so you can view BitLocker Key IDs and recovery keys for your Windows 10/11 devices, from within the Microsoft Endpoint Manager admin center. Support to view recovery keys can also [extend to your tenant-attached devices](#view-recovery-keys-for-tenant-attached devices).

To be accessible, the device must have its keys escrowed to Azure AD.

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Devices** > **All devices**.

3. Select a device from the list, and then under *Monitor*, select **Recovery keys**.

4. Hit **Show Recovery Key**. Selecting this will generate an audit log entry under 'KeyManagement' activity.
  
   When keys are available in Azure AD, the following information is available:
   - BitLocker Key ID
   - BitLocker Recovery Key
   - Drive Type

   When keys aren't in Azure AD, Intune will display *No BitLocker key found for this device*.

> [!NOTE]
> Currently, Azure AD supports a maximum of 200 BitLocker recovery keys per device. If you reach this limit, silent encryption will fail due to the failing backup of recovery keys before starting encryption on the device.

Information for BitLocker is obtained using the [BitLocker configuration service provider](/windows/client-management/mdm/bitlocker-csp) (CSP). BitLocker CSP is supported on Windows 10 version 1703 and later, Windows 10 Pro version 1809 and later, and Windows 11.

IT admins need to have a specific permission within Azure Active Directory to be able to see device BitLocker recovery keys: `microsoft.directory/bitlockerKeys/key/read`. There are some roles within Azure AD that come with this permission, including Cloud Device Administrator, Helpdesk Administrator, etc. For more information on which Azure AD roles have which permissions, see [Azure AD role descriptions](/azure/active-directory/roles/permissions-reference).

All BitLocker recovery key accesses are audited. For more information on Audit Log entries, see [Azure portal audit logs](/azure/active-directory/devices/device-management-azure-portal#audit-logs).

> [!NOTE]
> If you delete the Azure AD object for an Azure AD joined device protected by BitLocker, the next time that device syncs with Azure AD it will remove the key protectors for the operating system volume. Removing the key protector leaves BitLocker in a suspended state on that volume. This is necessary because BitLocker recovery information for Azure AD joined devices is attached to the Azure AD computer object and deleting it may leave you unable to recover from a BitLocker recovery event.

### View recovery keys for tenant-attached devices

When you’ve configured the tenant attach scenario, Microsoft Endpoint Manager can display recovery key data for tenant attached devices.

- To support the display of recovery keys for tenant attached devices, your Configuration Manager sites must run version 2107 or later. For sites that run 2107, you must install an update rollup to support Azure AD joined devices: See [KB11121541](../../configmgr/hotfix/2107/11121541.md).

- To view the recovery keys, your Intune account must have the Intune RBAC permissions to view BitLocker keys, and must be associated with an on-premises user that has the related permissions for Configuration Manager of Collection Role, with Read Permission > Read BitLocker Recovery Key Permission. For more information, see [Configure role-based administration for Configuration Manager](/configmgr/core/servers/deploy/configure/configure-role-based-administration).

### Rotate BitLocker recovery keys

You can use an Intune device action to remotely rotate the BitLocker recovery key of a device that runs Windows 10 version 1909 or later, and Windows 11.

#### Prerequisites

Devices must meet the following prerequisites to support rotation of the BitLocker recovery key:

- Devices must run Windows 10 version 1909 or later, or Windows 11

- Azure AD-joined and Hybrid-joined devices must have support for key rotation enabled via BitLocker policy configuration:

  - **Client-driven recovery password rotation** to *Enable rotation on Azure AD-joined devices* or *Enable rotation on Azure AD and Hybrid-joined devices*
  - **Save BitLocker recovery information to Azure Active Directory** to *Enabled*
  - **Store recovery information in Azure Active Directory before enabling BitLocker** to *Required*

For information about BitLocker deployments and requirements, see the [BitLocker deployment comparison chart](/windows/security/information-protection/bitlocker/bitlocker-deployment-comparison).

#### To rotate the BitLocker recovery key

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Devices** > **All devices**.

3. In the list of devices that you manage, select a device, select **More**, and then select the **BitLocker key rotation** device remote action.

4. On the **Overview** page of the device, select the **BitLocker key rotation**. If you don't see this option, select the ellipsis (**…**) to show additional options, and then select the **BitLocker key rotation** device remote action.

   ![Select the ellipsis to view more options](./media/encrypt-devices/select-more.png)

## Next steps

- [Manage FileVault policy](../protect/encrypt-devices-filevault.md)  
- [Monitor disk encryption](../protect/encryption-monitor.md)
- [Troubleshooting BitLocker policy](/troubleshoot/mem/intune/troubleshoot-bitlocker-policies)
- [Known issues for Enforcing BitLocker policies with Intune](/windows/security/information-protection/bitlocker/ts-bitlocker-intune-issues)
- [BitLocker management for enterprises](/windows/security/information-protection/bitlocker/bitlocker-management-for-enterprises), in the Windows security documentation