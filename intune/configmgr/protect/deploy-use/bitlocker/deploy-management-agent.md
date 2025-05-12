---
title: Deploy BitLocker management
titleSuffix: Configuration Manager
description: Deploy the BitLocker management agent to Configuration Manager clients and the recovery service to management points
ms.date: 12/01/2021
ms.service: configuration-manager
ms.subservice: protect
ms.topic: how-to
author: BalaDelli
ms.author: baladell
manager: apoorvseth
ms.localizationpriority: medium
ms.reviewer: mstewart,aaroncz 
ms.collection: tier3
---

# Deploy BitLocker management

*Applies to: Configuration Manager (current branch)*

<!--3601034-->

BitLocker management in Configuration Manager includes the following components:

- **BitLocker management agent**: Configuration Manager enables this agent on a device when you [create a policy](#create-a-policy) and [deploy it to a collection](#deploy-a-policy).

- **Recovery service**: The server component that receives BitLocker recovery data from clients. For more information, see [Recovery service](recovery-service.md).

Before you create and deploy BitLocker management policies:

- Review the [prerequisites](../../plan-design/bitlocker-management.md#prerequisites)

- If necessary, [encrypt recovery keys](encrypt-recovery-data.md) in the site database

## Create a policy

When you create and deploy this policy, the Configuration Manager client enables the BitLocker management agent on the device.

> [!NOTE]
> To create a BitLocker management policy, you need the **Full Administrator** role in Configuration Manager.

1. In the Configuration Manager console, go to the **Assets and Compliance** workspace, expand **Endpoint Protection**, and select the **BitLocker Management** node.

1. In the ribbon, select **Create BitLocker Management Control Policy**.

1. On the **General** page, specify a name and optional description. Select the components to enable on clients with this policy:  

    - **Operating System Drive**: Manage whether the OS drive is encrypted

    - **Fixed Drive**: Manage encryption for other data drives in a device

    - **Removable Drive**: Manage encryption for drives that you can remove from a device, like a USB key

    - **Client Management**: Manage the key recovery service backup of BitLocker Drive Encryption recovery information  

1. On the **Setup** page, configure the following global settings for BitLocker Drive Encryption:

    > [!NOTE]
    > Configuration Manager applies these settings when you enable BitLocker. If the drive is already encrypted or is in progress, any change to these policy settings doesn't change the drive encryption on the device.
    >
    > If you disable or don't configure these settings, BitLocker uses the default encryption method (AES 128-bit).

    - For Windows 8.1 devices, enable the option for **Drive encryption method and cipher strength**. Then select the encryption method.

    - For Windows 10 or later devices, enable the option for **Drive encryption method and cipher strength (Windows 10 or later)**. Then individually select the encryption method for OS drives, fixed data drives, and removable data drives.

    For more information on these and other settings on this page, see [Settings reference - Setup](../../tech-ref/bitlocker/settings.md#setup).

1. On the **Operating System Drive** page, specify the following settings:  

    - **Operating System Drive Encryption Settings**: If you enable this setting, the user has to protect the OS drive, and BitLocker encrypts the drive. If you disable it, the user can't protect the drive.  

    On devices with a compatible TPM, two types of authentication methods can be used at startup to provide added protection for encrypted data. When the computer starts, it can use only the TPM for authentication, or it can also require the entry of a personal identification number (PIN). Configure the following settings:

    - **Select protector for operating system drive**: Configure it to use a TPM and PIN, or just the TPM.

    - **Configure minimum PIN length for startup**: If you require a PIN, this value is the shortest length the user can specify. The user enters this PIN when the computer boots to unlock the drive. By default, the minimum PIN length is `4`.

    For more information on these and other settings on this page, see [Settings reference - OS drive](../../tech-ref/bitlocker/settings.md#os-drive).

1. On the **Fixed Drive** page, specify the following settings:

    - **Fixed data drive encryption**: If you enable this setting, BitLocker requires users to put all fixed data drives under protection. It then encrypts the data drives. When you enable this policy, either enable auto-unlock or the settings for **Fixed data drive password policy**.

    - **Configure auto-unlock for fixed data drive**: Allow or require BitLocker to automatically unlock any encrypted data drive. To use auto-unlock, also require BitLocker to encrypt the OS drive.

    For more information on these and other settings on this page, see [Settings reference - Fixed drive](../../tech-ref/bitlocker/settings.md#fixed-drive).

1. On the **Removable Drive** page, specify the following settings:

    - **Removable data drive encryption**: When you enable this setting, and allow users to apply BitLocker protection, the Configuration Manager client saves recovery information about removable drives to the recovery service on the management point. This behavior allows users to recover the drive if they forget or lose the protector (password).

    - **Allow users to apply BitLocker protection on removable data drives**: Users can turn on BitLocker protection for a removable drive.

    - **Removable data drive password policy**: Use these settings to set the constraints for passwords to unlock BitLocker-protected removable drives.

    For more information on these and other settings on this page, see [Settings reference - Removable drive](../../tech-ref/bitlocker/settings.md#removable-drive).

1. On the **Client Management** page, specify the following settings:

    > [!IMPORTANT]
    > For versions of Configuration Manager prior to 2103, if you don't have a management point with an HTTPS-enabled website, don't configure this setting. For more information, see [Recovery service](recovery-service.md).

    - **Configure BitLocker Management Services**: When you enable this setting, Configuration Manager automatically and silently backs up key recovery information in the site database. If you disable or don't configure this setting, Configuration Manager doesn't save key recovery information.

        - **Select BitLocker recovery information to store**: Configure it to use a recovery password and key package, or just a recovery password.

        - **Allow recovery information to be stored in plain text**: Without a BitLocker management encryption certificate, Configuration Manager stores the key recovery information in plain text. For more information, see [Encrypt recovery data in the database](encrypt-recovery-data.md).

    For more information on these and other settings on this page, see [Settings reference - Client management](../../tech-ref/bitlocker/settings.md#client-management).

1. Complete the wizard.

To change the settings of an existing policy, choose it in the list, and select **Properties**.

When you create more than one policy, you can configure their relative priority. If you deploy multiple policies to a client, it uses the priority value to determine its settings.

Starting in version 2006, you can use Windows PowerShell cmdlets for this task. For more information, see [New-CMBlmSetting](/powershell/module/configurationmanager/new-cmblmsetting).

## Deploy a policy

1. Choose an existing policy in the **BitLocker Management** node. In the ribbon, select **Deploy**.

1. Select a device collection as the target of the deployment.

1. If you want the device to potentially encrypt or decrypt its drives at any time, select the option to **Allow remediation outside the maintenance window**. If the collection has any maintenance windows, it still remediates this BitLocker policy.

1. Configure a **Simple** or **Custom** schedule. The client evaluates its compliance based on the settings specified in the schedule.

1. Select **OK** to deploy the policy.

You can create multiple deployments of the same policy. To view additional information about each deployment, select the policy in the **BitLocker Management** node, and then in the details pane, switch to the **Deployments** tab. You can also use Windows PowerShell cmdlets for this task. For more information, see [New-CMSettingDeployment](/powershell/module/configurationmanager/new-cmsettingdeployment).

> [!IMPORTANT]
> If a remote desktop protocol (RDP) connection is active, the MBAM client doesn't start BitLocker Drive Encryption actions. Close all remote console connections and sign in to a console session with a domain user account. Then BitLocker Drive Encryption begins and the client uploads recovery keys and packages. If you sign in with a local user account, BitLocker Drive Encryption doesn't start.
>
> You can use RDP to remotely connect to the console session of the device with the `/admin` switch. For example: `mstsc.exe /admin /v:<IP address of device>`
>
> A _console session_ is either when you're at the computer's physical console, or a remote connection that's the same as if you're at the computer's physical console.

## Monitor

View basic compliance statistics about the policy deployment in the details pane of the **BitLocker Management** node:

- Compliance count
- Failure count
- Non-compliance count

Switch to the **Deployments** tab to see compliance percentage and recommended action. Select the deployment, then in the ribbon, select **View Status**. This action switches the view to the **Monitoring** workspace, **Deployments** node. Similar to the deployment of other configuration policy deployments, you can see more detailed compliance status in this view.

To understand why clients are reporting not compliant with the BitLocker management policy, see [Non-compliance codes](../../tech-ref/bitlocker/non-compliance-codes.md).

For more troubleshooting information, see [Troubleshoot BitLocker](../../tech-ref/bitlocker/troubleshoot.md).

Use the following logs to monitor and troubleshoot:

### Client logs

- MBAM event log: in the Windows Event Viewer, browse to **Applications and Services** > **Microsoft** > **Windows** > **MBAM**.  For more information, see [About BitLocker event logs](../../tech-ref/bitlocker/about-event-logs.md) and [Client event logs](../../tech-ref/bitlocker/client-event-logs.md).

- **BitlockerManagementHandler.log** and **BitlockerManagement_GroupPolicyHandler.log** in client logs path, `%WINDIR%\CCM\Logs` by default

### Management point logs (recovery service)

- Recovery service event log: in the Windows Event Viewer, browse to **Applications and Services** > **Microsoft** > **Windows** > **MBAM-Web**. For more information, see [About BitLocker event logs](../../tech-ref/bitlocker/about-event-logs.md) and [Server event logs](../../tech-ref/bitlocker/server-event-logs.md).

- Recovery service trace logs: `<Default IIS Web Root>\Microsoft BitLocker Management Solution\Logs\Recovery And Hardware Service\trace*.etl`

## Migration considerations

If you currently use Microsoft BitLocker Administration and Monitoring (MBAM), you can seamlessly migrate management to Configuration Manager. When you deploy BitLocker management policies in Configuration Manager, clients automatically upload recovery keys and packages to the Configuration Manager recovery service.

> [!IMPORTANT]
> When you migrate from stand-alone MBAM to Configuration Manager BitLocker management, if you require existing functionality of stand-alone MBAM, don't reuse stand-alone MBAM servers or components with Configuration Manager BitLocker management. If you reuse these servers, stand-alone MBAM will stop working when Configuration Manager BitLocker management installs its components on those servers. Don't run the MBAMWebSiteInstaller.ps1 script to set up the BitLocker portals on stand-alone MBAM servers. When you set up Configuration Manager BitLocker management, use separate servers.

### Group policy

- The BitLocker management settings are fully compatible with MBAM group policy settings. If devices receive both group policy settings and Configuration Manager policies, configure them to match.

  > [!NOTE]
  > If a group policy setting exists for standalone MBAM, it will override the equivalent setting attempted by Configuration Manager. Standalone MBAM uses domain group policy, while Configuration Manager sets local policies for BitLocker management. Domain policies will override the local Configuration Manager BitLocker management policies. If the standalone MBAM domain group policy doesn't match the Configuration Manager policy, Configuration Manager BitLocker management will fail. For example, if a domain group policy sets the standalone MBAM server for key recovery services, Configuration Manager BitLocker management can't set the same setting for the management point. This behavior causes clients to not report their recovery keys to the Configuration Manager BitLocker management key recovery service on the management point.

- Configuration Manager doesn't implement all MBAM group policy settings. If you configure more settings in group policy, the BitLocker management agent on Configuration Manager clients honors these settings.

  > [!IMPORTANT]
  > Don't set a group policy for a setting that Configuration Manager BitLocker management already specifies. Only set group policies for settings that don't currently exist in Configuration Manager BitLocker management. Configuration Manager version 2002 has feature parity with standalone MBAM. With Configuration Manager version 2002 and later, in most instances there should be no reason to set domain group policies to configure BitLocker policies. To prevent conflicts and problems, avoid use of group policies for BitLocker. Configure all settings through Configuration Manager BitLocker management policies.

### TPM password hash

- Previous MBAM clients don't upload the TPM password hash to Configuration Manager. The client only uploads the TPM password hash once.

- If you need to migrate this information to the Configuration Manager recovery service, clear the TPM on the device. After it restarts, it uploads the new TPM password hash to the recovery service.

> [!NOTE]
> Uploading of the TPM password hash mainly pertains to versions of Windows before Windows 10. Windows 10 or later by default doesn't save the TPM password hash, so these devices don't normally upload it. For more information, see [About the TPM owner password](/windows/security/information-protection/tpm/change-the-tpm-owner-password#about-the-tpm-owner-password).

### Re-encryption

Configuration Manager doesn't re-encrypt drives that are already protected with BitLocker Drive Encryption. If you deploy a BitLocker management policy that doesn't match the drive's current protection, it reports as non-compliant. The drive is still protected.

For example, you used MBAM to encrypt the drive with the AES-XTS 128 encryption algorithm, but the Configuration Manager policy requires AES-XTS 256. The drive is non-compliant with the policy, even though the drive is encrypted.

To work around this behavior, first disable BitLocker on the device. Then deploy a new policy with the new settings.

## Co-management and Intune

<!-- SCCMDocs#2321 -->

The Configuration Manager client handler for BitLocker is co-management aware. If the device is co-managed, and you switch the [Endpoint Protection workload](../../../comanage/workloads.md#endpoint-protection) to Intune, then the Configuration Manager client ignores its BitLocker policy. The device gets Windows encryption policy from Intune.

> [!NOTE]
> Switching encryption management authorities while maintaining the desired encryption algorithm doesn't require any additional actions on the client. However, if you switch encryption management authorities and the desired encryption algorithm also changes, you will need to plan for [re-encryption](#re-encryption).

For more information about managing BitLocker with Intune, see the following articles:

- [Use device encryption with Intune](../../../../intune-service/protect/encrypt-devices.md)
- [Troubleshoot BitLocker policies in Microsoft Intune](/troubleshoot/mem/intune/troubleshoot-bitlocker-policies)

## Next steps

[About the BitLocker recovery service](recovery-service.md)

[Set up BitLocker reports and portals](setup-websites.md)
