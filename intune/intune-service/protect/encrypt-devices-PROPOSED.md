---
title: Encrypt Windows devices with Intune
description: Use Microsoft Intune policy to manage encryption of Windows devices with either BitLocker or Personal Data Encryption.
author: brenduns
ms.author: brenduns
ms.date: 11/24/2025
ms.topic: how-to
ms.reviewer: annovich; aanavath
ms.collection:
- M365-identity-device-management
- highpri
- highseo
- sub-secure-endpoints
---

# Manage Disk Encryption policy for Windows devices with Intune

Use Intune to configure BitLocker encryption on devices that run Windows, and Personal Data Encryption (PDE) on devices that run Windows 11 Version 22H2 or later.

> [!IMPORTANT]
> [!INCLUDE [windows-10-support](../includes/windows-10-support.md)]

> [!TIP]
>
> Some settings for BitLocker require the device have a supported TPM.

To configure encryption on your managed devices, use one of the following policy types:

- **[Endpoint security > Windows encryption policy](#create-an-endpoint-security-policy-for-windows)**. Choose from the following profiles:

  - *BitLocker* - A focused group of settings that are dedicated to configuring BitLocker. For more information, see the [BitLocker CSP](/windows/client-management/mdm/bitlocker-csp).

  - *Personal Data Encryption* - [Personal Data Encryption](/windows/security/operating-system-security/data-protection/personal-data-encryption/) (PDE) differs from BitLocker in that it encrypts files instead of whole volumes and disks. PDE occurs in addition to other encryption methods like BitLocker. Unlike BitLocker that releases data encryption keys at boot, PDE doesn't release data encryption keys until a user signs in using Windows Hello for Business. For more information, see the [PDE CSP](/windows/client-management/mdm/personaldataencryption-csp).

    PDE isn't a replacement for BitLocker; use both for layered security.

- **[Device configuration profile (Settings Catalog)](../configuration/settings-catalog.md)** to configure BitLocker settings with granular control over all BitLocker settings that are available with Intune.

- **[Device configuration profile for Endpoint protection](#create-an-endpoint-security-policy-for-windows)**. The *Endpoint protection* profile is a legacy profile that remains available. This profile also includes BitLocker settings for Windows devices but is no longer updated with no longer updated with more recent BitLocker settings or changes.
  View the BitLocker settings that are available for [BitLocker in endpoint protection profiles from device configuration policy](../protect/endpoint-protection-windows-10.md#windows-settings).

Intune also includes a built-in [encryption report](encryption-monitor.md) that presents details about the encryption status across all your managed devices. The report also supports viewing and managing BitLocker recovery keys for Windows devices encrypted through Intune. The report also includes important information for BitLocker from your devices, as found in Microsoft Entra ID.

> [!IMPORTANT]
>
> Before enabling BitLocker, understand and plan for *recovery options* that meet your organizations needs. For more information, start with [**BitLocker recovery overview**](/windows/security/operating-system-security/data-protection/bitlocker/recovery-overview) in the Windows security documentation.

## Prerequisites

### Licensing

For Windows editions that support BitLocker management, see [Windows edition and licensing requirements](/windows/security/operating-system-security/data-protection/bitlocker/configure?tabs=common#windows-edition-and-licensing-requirements) in the Windows documentation.
 

### Role-based access controls to manage BitLocker

To manage BitLocker in Intune, an account must be assigned an Intune [role-based access control](../fundamentals/role-based-access-control.md) (RBAC) role that includes the **Remote tasks** permission with the **Rotate BitLockerKeys (preview)** right set to **Yes**.

You can add this permission and right to your own [custom RBAC roles](../fundamentals/create-custom-role.md) or use one of the following [built-in RBAC roles](../fundamentals/role-based-access-control-reference.md) that include this right:

- Help Desk Operator
- Endpoint Security Administrator

## Create and deploy policy

Use one of the following procedures to create the policy type you prefer.

### Create an endpoint security policy for Windows

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Endpoint security** > **Disk encryption** > **Create Policy**.

3. Set the following options:
   1. **Platform**: Windows
   2. **Profile**: Choose either *BitLocker* or *Personal Data Encryption*

   :::image type="content" source="./media/encrypt-devices/select-windows-encpryption-profile.png" alt-text="Screen capture of the Windows encryption profile selection surface.":::

4. On the **Configuration settings** page, configure settings for BitLocker to meet your business needs.

   > [!TIP]
   > If you want to enable BitLocker silently without user interaction, see [Silently enable BitLocker on devices](encrypt-devices-silent.md) for specific prerequisites and configuration requirements.

   Select **Next**.

5. On the **Scope (Tags)** page, choose **Select scope tags** to open the Select tags pane to assign scope tags to the profile.

   Select **Next** to continue.

6. On the **Assignments** page, select the groups that receive this profile. For more information on assigning profiles, see Assign user and device profiles.

   Select **Next**.

7. On the **Review + create** page, when you're done, choose **Create**. The new profile is displayed in the list when you select the policy type for the profile you created.

### Create a device configuration profile for Windows encryption

> [!TIP]
>
> The following procedure configures BitLocker through a device configuration template for Endpoint protection. To configure Personal Data Encryption, use the device configuration [settings catalog](../configuration/settings-catalog.md) and the *PDE* category.

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Devices** > **Manage devices** > **Configuration** > On the *Policies* tab, select **Create**.

3. Set the following options:
   1. **Platform**: **Windows 10 and later**
      > [!IMPORTANT]
      > [!INCLUDE [windows-10-support](../includes/windows-10-support.md)]

   2. **Profile type**: Select **Templates** > **Endpoint protection**, and then select **Create**.

   ![Select your BitLocker profile](./media/encrypt-devices/select-windows-bitlocker-dc.png)

4. On the **Configuration settings** page, expand **Windows Encryption**.

   :::image type="content" source="./media/encrypt-devices/bitlocker-settings.png" alt-text="Select Windows encryption settings":::

5. Configure settings for BitLocker to meet your business needs.

   > [!TIP]
   > If you want to enable BitLocker silently without user interaction, see [Silently enable BitLocker on devices](encrypt-devices-silent.md) for specific prerequisites and configuration requirements.

6. Select **Next** to continue.

7. Complete configuration of other settings, and then save the profile.

## Manage BitLocker

The following subjects can help you manage specific tasks through BitLocker policy, and manage recovery keys:

- [Silently enable BitLocker on devices](encrypt-devices-silent.md) - Configure BitLocker to automatically encrypt devices without user interaction
- [Full disk vs Used Space only encryption](#full-disk-vs-used-space-only-encryption)
- [View details for recovery keys](#view-details-for-recovery-keys)
- [View recovery keys for tenant-attached devices](#view-recovery-keys-for-tenant-attached-devices)
- [Rotate BitLocker recovery keys](#rotate-bitlocker-recovery-keys)
- [End user self service recovery key experiences](#self-service-recovery-keys)

To view information about devices that receive BitLocker policy, see [Monitor disk encryption](../protect/encryption-monitor.md).

### Full disk vs Used Space only encryption

Three settings determine whether an OS drive is encrypted by encrypting the used space only, or by full disk encryption:

- Whether the hardware of the device is [modern standby](/windows-hardware/design/device-experiences/modern-standby) capable
- Whether silent enablement has been configured for BitLocker
  - ('Warning for other disk encryption' = Block or 'Hide prompt about third-party encryption' = Yes)
- Configuration of the [SystemDrivesEncryptionType](/windows/client-management/mdm/bitlocker-csp)
  - (Enforce drive encryption type on operating system drives)

Assuming that SystemDrivesEncryptionType isn't configured, the following behavior is expected. When silent enablement is configured on a modern standby device, the OS drive is encrypted using the used space only encryption. When silent enablement is configured on a device that isn't capable of modern standby, the OS drive is encrypted using full disk encryption. The result is the same whether you're using an [Endpoint Security disk encryption policy for BitLocker](#create-an-endpoint-security-policy-for-windows) or a [Device Configuration profile for endpoint protection for BitLocker](#create-a-device-configuration-profile-for-windows-encryption). If a different end state is required, the encryption type can be controlled by configuring the SystemDrivesEncryptionType using settings catalog.

To verify whether the hardware is modern standby capable, run the following command from a command prompt:

```console
powercfg /a
```
If the device supports modern standby, it shows that Standby (S0 Low Power Idle) Network Connected is available

:::image type="content" source="./media/encrypt-devices/docs_bl_powercfg_surface_s0_possible.png" alt-text="Screenshot of command prompt displaying output of powercfg command with Standby state S0 available.":::

If the device doesn't support modern standby, such as a virtual machine, it shows that Standby (S0 Low Power Idle) Network Connected isn't supported

:::image type="content" source="./media/encrypt-devices/docs_bl_powercfg_surface_nos0possible.png" alt-text="Screenshot of command prompt displaying output of powercfg command with Standby state S0 unavailable.":::

To verify the encryption type, run the following command from an elevated (admin) command prompt:

```console
manage-bde -status c:
```

The 'Conversion Status' field reflects the encryption type as either Used Space Only encrypted or Fully Encrypted.

:::image type="content" source="./media/encrypt-devices/docs_bl_usedspaceonly.png" alt-text="Screenshot of administrative command prompt showing output of manage-bde with conversion status reflecting fully encrypted.":::

:::image type="content" source="./media/encrypt-devices/docs_bl_fullyencrypted.png" alt-text="Screenshot of administrative command prompt showing output of manage-bde with conversion status reflecting used space only encryption.":::

To change the disk encryption type between full disk encryption and used space only encryption, use the'Enforce drive encryption type on operating system drives' setting within settings catalog.

:::image type="content" source="./media/encrypt-devices/docs_bl_settingscatalog_control_encryption.png" alt-text="Screenshot of Intune settings catalog displaying Enforce drive encryption type on operating system drives":::

### View details for recovery keys

Intune provides access to the Microsoft Entra node for BitLocker so you can view BitLocker Key IDs and recovery keys for your Windows devices, from within the Microsoft Intune admin center. Support to view recovery keys can also [extend to your tenant-attached devices](#view-recovery-keys-for-tenant-attached-devices).

To be accessible, the device must have its keys escrowed to Microsoft Entra.

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Devices** > **All devices**.

3. Select a device from the list, and then under *Monitor*, select **Recovery keys**.

4. Hit **Show Recovery Key**. Selecting this option generates an audit log entry under 'KeyManagement' activity.

   When keys are available in Microsoft Entra, the following information is available:
   - BitLocker Key ID
   - BitLocker Recovery Key
   - Drive Type

   When keys aren't in Microsoft Entra, Intune displays *No BitLocker key found for this device*.

> [!NOTE]
> Currently, Microsoft Entra ID supports a maximum of 200 BitLocker recovery keys per device. If you reach this limit, silent encryption fails due to the failing backup of recovery keys before starting encryption on the device.

Information for BitLocker is obtained using the [BitLocker configuration service provider](/windows/client-management/mdm/bitlocker-csp) (CSP).

IT admins need to have a specific permission within Microsoft Entra ID to be able to see device BitLocker recovery keys: `microsoft.directory/bitlockerKeys/key/read`. There are some roles within Microsoft Entra ID that come with this permission, including Cloud Device Administrator, Helpdesk Administrator, etc. For more information on which Microsoft Entra roles have which permissions, see [Microsoft Entra built-in roles](/azure/active-directory/roles/permissions-reference).

All BitLocker recovery key accesses are audited. For more information on Audit Log entries, see [Azure portal audit logs](/azure/active-directory/devices/device-management-azure-portal#audit-logs).

> [!NOTE]
> If you delete the Intune object for a Microsoft Entra joined device protected by BitLocker, the deletion triggers an Intune device sync and removes the key protectors for the operating system volume. Removing the key protector leaves BitLocker in a suspended state on that volume. This is necessary because BitLocker recovery information for Microsoft Entra joined devices is attached to the Microsoft Entra computer object and deleting it might leave you unable to recover from a BitLocker recovery event.

### View recovery keys for tenant-attached devices

When you use the tenant attach scenario, Microsoft Intune can display recovery key data for tenant attached devices.

- To support the display of recovery keys for tenant attached devices, your Configuration Manager sites must run version 2107 or later. For sites that run 2107, you must install an update rollup to support Microsoft Entra joined devices: See [KB11121541](../../configmgr/hotfix/2107/11121541.md).

- To view the recovery keys, your Intune account must have the Intune RBAC permissions to view BitLocker keys, and must be associated with an on-premises user that has the related permissions for Configuration Manager of Collection Role, with Read Permission > Read BitLocker Recovery Key Permission. For more information, see [Configure role-based administration for Configuration Manager](/configmgr/core/servers/deploy/configure/configure-role-based-administration).

### Rotate BitLocker recovery keys

You can use an Intune device action to remotely rotate the BitLocker recovery key of a device that runs Windows 10 version 1909 or later, and Windows 11.

> [!IMPORTANT]
> [!INCLUDE [windows-10-support](../includes/windows-10-support.md)]

#### Prerequisites

Devices must meet the following prerequisites to support rotation of the BitLocker recovery key:

- Devices must run Windows 10 version 1909 or later, or Windows 11

- Microsoft Entra joined and Microsoft Entra hybrid joined devices must have support for key rotation enabled via BitLocker policy configuration:

  - **Client-driven recovery password rotation** to *Enable rotation on Microsoft Entra joined devices* or *Enable rotation on Microsoft Entra ID and Microsoft Entra joined hybrid joined devices*
  - **Save BitLocker recovery information to Microsoft Entra ID** to *Enabled*
  - **Store recovery information in Microsoft Entra ID before enabling BitLocker** to *Required*

For information about BitLocker deployments and requirements, see the [BitLocker deployment comparison chart](/windows/security/information-protection/bitlocker/bitlocker-deployment-comparison).

#### To rotate the BitLocker recovery key

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Devices** > **All devices**.

3. In the list of devices that you manage, select a device, and then select the **BitLocker key rotation** remote action. If this option should be available but isn't visible, select the ellipsis (...) and then *BitLocker key rotation*.

4. On the **Overview** page of the device, select the **BitLocker key rotation**. If you don't see this option, select the ellipsis (**…**) to show all options, and then select the **BitLocker key rotation** device remote action.

   ![Select the ellipsis to view more options](./media/encrypt-devices/select-more.png)

### Self service recovery keys

To help end users get their recovery keys without calling the company helpdesk, Intune enables [self service scenarios for the end user through the Company Portal app](../user-help/get-recovery-key-windows.md).

While Intune helps configure policy to define the escrow of BitLocker recovery keys, these keys are stored within Entra ID. These are the capabilities within Entra ID that are helpful to use with self-service BitLocker recovery key access for end users.

1. **Tenant-wide toggle to prevent recovery key access for non-admin users**: This setting determines if users can use self-service to recover their BitLocker keys. The default value is 'No' which allows all users to recover their BitLocker keys. 'Yes' restricts nonadmin users from being able to see the BitLocker keys for their own devices if there are any. [Learn more about this control in Entra ID](/entra/identity/devices/manage-device-identities#configure-device-settings).

2. **Auditing for recovery key access**: Audit Logs within the Entra ID portal show the history of activities within the tenant. Any user recovery key accesses made through the Company Portal website will be logged in Audit Logs under the Key Management category as a "Read BitLocker key" activity type. The user's User Principal Name and other info such as key ID is also logged. [Learn more about audit logs in Entra ID](/entra/identity/monitoring-health/concept-audit-logs).

3. **Entra Conditional Access policy requiring a compliant device to access BitLocker Recovery Key**: With Conditional Access policy (CA), you can restrict the access to certain corporate resources if a device isn't compliant with the "Require compliant device" setting. If this is set up within your organization, and a device fails to meet the Compliance requirements configured in the Intune Compliance policy, that device can't be used to access the BitLocker Recovery Key as it is considered a corporate resource, which is access controlled by CA.

## Next steps

- [Silently enable BitLocker on devices](encrypt-devices-silent.md)
- [Manage FileVault policy](../protect/encrypt-devices-filevault.md)
- [Monitor disk encryption](../protect/encryption-monitor.md)
- [Troubleshooting BitLocker policy](/troubleshoot/mem/intune/troubleshoot-bitlocker-policies)
- [Known issues for Enforcing BitLocker policies with Intune](/windows/security/information-protection/bitlocker/ts-bitlocker-intune-issues)
- [BitLocker management for enterprises](/windows/security/information-protection/bitlocker/bitlocker-management-for-enterprises), in the Windows security documentation
- [Personal Data Encryption overview](/windows/security/operating-system-security/data-protection/personal-data-encryption/)
- [Self service scenarios for the end user through the Company Portal app](../user-help/get-recovery-key-windows.md)