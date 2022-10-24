---
title: Manage clients
titleSuffix: Configuration Manager
description: Learn how to manage clients in Configuration Manager.
ms.date: 02/16/2022
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
author: sheetg09
ms.author: sheetg
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# How to manage clients in Configuration Manager

*Applies to: Configuration Manager (current branch)*

When the Configuration Manager client installs on a device and successfully assigns to a site, you see the device in the **Assets and Compliance** workspace in the **Devices** node, and in one or more collections in the **Device Collections** node. Select the device or a collection, and then run management operations. However, there are other ways to manage the client, which might involve other workspaces in the console, or tasks outside of the console.

> [!NOTE]
> If you install the Configuration Manager client, but it hasn't yet successfully assigned to a site, it might not display in the console. After the client assigns to a site, update collection membership, and then refresh the console view.
>
> A device can also display in the console when the Configuration Manager client isn't installed. This behavior happens if the site discovers a device but the client isn't installed and assigned.
>
> Mobile devices managed with the [Exchange Server connector](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md) or [on-premises MDM](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md) don't install the Configuration Manager client.
>
> To manage a device from the console, use the **Client** column in the **Devices** node to determine whether the client is installed.

## Manage clients from the **Devices** node

Depending on the device type, some of these options might not be available.

1. In the Configuration Manager console, go to the **Assets and Compliance** workspace, and select the **Devices** node.

2. Select one or more devices, and then select one of these client management tasks from the ribbon. You can also right-click the device.

### Import user device affinity

Configure the associations between users and devices, so you can efficiently deploy software to users.

For more information, see [Link users and devices with user device affinity](../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).

### Import computer information

Launch the **Import Computer Information Wizard** to import new computer information into the Configuration Manager database. You can import multiple computers using a file, or specify information for a single computer.

### Add selected items

Provides the following options:

- **Add selected items to existing device collection**: Opens the **Select Collection** dialog box. Select the collection to which you want to add this device. The device is included in this collection by using a **Direct** membership rule.

- **Add selected items to new device collection**: Opens the **Create Device Collection Wizard** where you can create a new collection. The selected collection is included in this collection by using a **Direct** membership rule.

For more information, see [How to create collections](collections/create-collections.md).

### Install client

Opens the **Install Client Wizard**. This wizard uses client push installation to install or reinstall the Configuration Manager client on the selected device.

> [!TIP]
> There are many different ways to install the Configuration Manager client. Although the Client Push wizard offers a convenient client installation method from the console, this method has many dependencies and isn't suitable for all environments. For more information about the dependencies, see [Prerequisites for deploying clients to Windows computers](../deploy/prerequisites-for-deploying-clients-to-windows-computers.md#client-push-installation). For more information about the other client installation methods, see [Client installation methods](../deploy/plan/client-installation-methods.md).

For more information, see [How to install Configuration Manager clients by using client push](../deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush).

### Run script

Opens the **Run Script** wizard to run a PowerShell script on the selected device.

For more information, see [Create and run PowerShell scripts](../../../apps/deploy-use/create-deploy-scripts.md).

### Install application

Install an application to a device in real time. This feature can help reduce the need for separate collections for every application.

Starting in version 2111, select the **Install Application Group** action for an app group.<!-- 10992210 -->

For more information, see [Install applications for a device](../../../apps/deploy-use/install-app-for-device.md).

### Reassign site

Reassign one or more clients, including managed mobile devices, to another primary site in the hierarchy. You can individually reassign clients or select more than one to reassign them in bulk.

### Client settings - Resultant client settings

When you deploy multiple client settings to the same device, the prioritization and combination of settings is complex. Use this option to view the resultant set of client settings deployed to this device.

For more information, see [How to configure client settings](../deploy/configure-client-settings.md).

### Start

- Run **Resource Explorer** to see the hardware and software inventory information from a Windows client. For more information, see the following articles:

  - [How to use Resource Explorer to view hardware inventory](inventory/use-resource-explorer-to-view-hardware-inventory.md)

  - [How to use Resource Explorer to view software inventory](inventory/use-resource-explorer-to-view-software-inventory.md)

- Remotely administer the device by using **Remote Control**, **Remote Assistance**, or **Remote Desktop Client**. For more information, see [How to remotely administer a Windows client computer](remote-control/remotely-administer-a-windows-client-computer.md).

### Approve

When the client communicates with site systems using HTTP and a self-signed certificate, you must approve these clients to identify them as trusted computers. By default, the site configuration automatically approves clients from the same Active Directory forest, trusted forests, and connected Azure Active Directory (Azure AD) tenants<!-- MEMDocs#318 -->. This default behavior means that you don't have to manually approve each client. Manually approve workgroup computers or clients from an untrusted forest that you trust, and any other unapproved computers that you trust.

> [!IMPORTANT]
> Although some management functions might work for unapproved clients, this is an unsupported scenario for Configuration Manager.

You don't have to approve clients that always communicate to site systems using HTTPS, or clients that use a PKI certificate when they communicate to site systems using HTTP. These clients establish trust by using the PKI certificates.

### Block or unblock

Block a client that you no longer trust. Blocking prevents the client from receiving policy, and prevents site systems from communicating with the client.

> [!IMPORTANT]
> Blocking a client only prevents communication from the client to Configuration Manager site systems. It doesn't prevent communication to other devices. When the client communicates to site systems by using HTTP instead of HTTPS, there are some security limitations.

You can also unblock a client that is blocked.

For more information, see [Determine whether to block clients](../deploy/plan/determine-whether-to-block-clients.md).

<!-- Change Category is a hybrid action -->

### Clear required PXE deployments

You can redeploy a required PXE deployment by clearing the status of the last PXE deployment assigned to a Configuration Manager collection or a computer. This action resets the status of that deployment and reinstalls the most recent required deployments.

For more information, see [Use PXE to deploy Windows over the network](../../../osd/deploy-use/use-pxe-to-deploy-windows-over-the-network.md).

### Client notification

For more information, see [Client notifications](client-notification.md#client-notification).

### Endpoint Protection

For more information, see [Client notifications](client-notification.md#endpoint-protection).

### Edit primary users

View users of this device in the last 90 days, or specify the primary users of this device.

For more information, see [Link users and devices with user device affinity](../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).

### Wipe a mobile device

You can wipe mobile devices that support the wipe command. This action permanently removes all data on the mobile device, including personal settings and personal data. Typically, this action resets the mobile device back to factory defaults. Wipe a mobile device when it's no longer trusted. For example, if the device is lost or stolen.

> [!TIP]
> Check the manufacturer's documentation for more information about how the mobile device processes a remote wipe command.

There's often a delay until the mobile device receives the wipe command:

- If the mobile device is enrolled by Configuration Manager, the client receives the command when it downloads its client policy.

- If the mobile device is managed by the Exchange Server connector, it receives the command when it synchronizes with Exchange.

To monitor when the device receives the wipe command, use the **Wipe Status** column. Until the device sends a wipe acknowledgment to Configuration Manager, you can cancel the wipe command.

### Retire a mobile device

The **Retire** option is supported only by mobile devices enrolled by on-premises MDM.

For more information, see [Help protect your data with remote wipe, remote lock, or passcode reset](../../../mdm/deploy-use/wipe-lock-reset-devices.md).

### Change ownership

If a device isn't domain-joined and doesn't have the Configuration Manager client installed, use this option to change the ownership to **Company** or **Personal**.

You can use this value in application requirements to control deployments, and to control how much inventory is collected from users' devices.

You may need to add the **Device Owner** column to the view by right-clicking any column heading and choosing it.

### Delete

> [!WARNING]
> Don't delete a client if you want to uninstall the Configuration Manager client or remove it from a collection.

The **Delete** action manually removes the client record from the Configuration Manager database. Only use this action to troubleshoot a problem. If you delete the object, but the client is still installed and communicating with the site, Heartbeat Discovery recreates the client record. It reappears in the Configuration Manager console, although the client history and any previous associations are lost.

> [!NOTE]
> When you delete a mobile device client that was enrolled by Configuration Manager, this action also revokes the issued PKI certificate. This certificate is then rejected by the management point, even if IIS doesn't check the certificate revocation list (CRL).
>
> Certificates on mobile device legacy clients are not revoked when you delete these clients.

To uninstall the client, see [Uninstall the Configuration Manager client](#uninstall-the-client).

To assign the client to a new primary site, see [How to assign clients to a site](../deploy/assign-clients-to-a-site.md).

To remove the client from a collection, reconfigure the collection properties. For more information, see [How to manage collections](collections/manage-collections.md).

### Refresh

Refresh the console view with the latest data in the database. For example, if a device appears in the list from discovery, but doesn't show as installed. After you install the client and make sure it's assigned to the site, select **Refresh**.

### Properties

View the discovery data and deployments targeted for the client.

Switch to the **Variables** tab to configure variables that task sequences use to deploy an OS to the device. For more information, see [Create task sequence variables for devices and collections](../../../osd/understand/using-task-sequence-variables.md#bkmk_set-coll-var).

Starting in version 2111, switch to the **Custom properties** tab to manually set custom properties on the device for reporting or to create collections. For more information, see [Custom properties for devices](../../../develop/adminservice/custom-properties.md).

## Manage clients from the **Device Collections** node

Many of the tasks that are available for devices in the **Devices** node are also available on collections. The console automatically applies the operation to all eligible devices in the collection. This action on an entire collection generates more network packets and increases CPU usage on the site server.

Consider the following questions before you run collection-level tasks. Once started, you can't stop the task from the console.

- How many devices are in the collection?
- Are the devices connected by low-bandwidth network connections?
- How much time does this task need to complete for all the devices?

For more information, see [How to manage collections](collections/manage-collections.md).

## Restart clients

Use the Configuration Manager console to identify clients that require a restart. Then use a client notification action to restart them.

> [!Tip]
> Enable automatic client upgrade to keep your clients up-to-date with less effort. For more information, see [About automatic client upgrade](upgrade/upgrade-clients-for-windows-computers.md#bkmk_autoupdate).

To identify devices that are pending a restart, go to the **Assets and Compliance** workspace in the Configuration Manager console and select the **Devices** node. Then view the status for each device in the details pane in a new column named **Pending Restart**. Each device has one or more of the following values:

- **No**: there's no pending restart
- **Configuration Manager**: this value comes from the client reboot coordinator component (RebootCoordinator.log)
- **File rename**: this value comes from Windows reporting a pending file rename operation (`HKLM\SYSTEM\CurrentControlSet\Control\Session Manager, PendingFileRenameOperations`)
- **Windows Update**: this value comes from the Windows Update Agent reporting a pending restart is required for one or more updates (`HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\WindowsUpdate\Auto Update\RebootRequired`)
- **Add or remove feature**: this value comes from the Windows component-based servicing reporting the addition or removal of a Windows feature requires a restart (`HKLM\Software\Microsoft\Windows\CurrentVersion\Component Based Servicing\Reboot Pending`)

### Create the client notification to restart a device

1. Select the device you want to restart within a collection in the **Device Collections** node of the console.
2. In the ribbon, select **Client Notification**, and then select **Restart**. An information window opens about the restart. Select **OK** to confirm the restart request.

When the notification is received by a client, a **Software Center** notification window opens to inform the user about the restart. By default, the restart occurs after 90 minutes. You can modify the restart time by configuring [client settings](../deploy/configure-client-settings.md). Settings for the restart behavior are found on the [Computer restart](../deploy/about-client-settings.md#computer-restart) tab of the default settings.

## Configure the client content cache

The client cache stores temporary files for when clients install applications and programs. Software updates also use the client cache, but always attempt to download to the cache whatever the size setting. Configure the cache settings, such as size and location, when you manually install the client, when you use client push installation, or after installation.

For more information, see [Configure the client content cache](configure-client-cache.md).

## Uninstall the client

You can uninstall the Configuration Manager client software from a computer by using **CCMSetup.exe** with the `/Uninstall` property. Run CCMSetup.exe on an individual computer from the command prompt, or deploy a package to uninstall the client for a collection of computers.

> [!NOTE]
> You can't uninstall the Configuration Manager client from a mobile device. If you must remove the Configuration Manager client from a mobile device, you must wipe the device, which deletes all data on the mobile device.

1. Open a Windows command prompt as an administrator. Change the folder to the location in which CCMSetup.exe is located, for example: `cd %windir%\ccmsetup`

2. Run the following command: `CCMSetup.exe /uninstall`

> [!TIP]
> The uninstall process displays no results on the screen. To verify that the client successfully uninstalls, see the following log file: `%windir%\ccmsetup\logs\CCMSetup.log`
>
> If you need to wait for the uninstall process to complete before doing something else, run `Wait-Process CCMSetup` in PowerShell. This command can pause a script until the CCMSetup process completes.

Starting in version 2111, when you uninstall the client it also removes the client bootstrap, ccmsetup.msi, if it exists.<!-- 12425149 -->

## Manage conflicting records

Configuration Manager uses the hardware identifier to attempt to identify clients that might be duplicates and alert you to the conflicting records. For example, if you reinstall a computer, the hardware identifier would be the same but the GUID used by Configuration Manager might be changed.

Configuration Manager automatically resolves conflicts by using Windows authentication of the computer account or a PKI certificate from a trusted source. When Configuration Manager can't resolve the conflict of duplicate hardware identifiers, a hierarchy setting determines the behavior.

### Change the hierarchy setting for managing conflicting records

1. In the Configuration Manager console, go to the **Administration** workspace, expand **Site Configuration**, and select the **Sites** node.

1. In the ribbon, select **Hierarchy Settings**.

1. Switch to the **Client Approval and Conflicting Records** tab, and select one of the following options:

    - **Automatically resolve conflicting records**
    - **Manually resolve conflicting records**

### Manually resolve conflicting records

1. In the Configuration Manager console, go to the **Monitoring** workspace, expand **System Status**, and select the **Conflicting Records** node.

1. Select one or more conflicting records, and then choose **Conflicting Record**.

1. Select one of the following options:

    - **Merge**: Combine the newly detected record with the existing client record.

    - **New**: Create a new record for the conflicting client record.

    - **Block**: Create a new record for the conflicting client record, but mark it as blocked.

## Manage duplicate hardware identifiers

You can provide a list of hardware identifiers that Configuration Manager ignores for PXE boot and client registration. This list helps to address two common issues:

1. Many new devices don't include an onboard Ethernet port. Technicians use a USB-to-Ethernet adapter to establish a wired connection for purposes of OS deployment. These adapters are often shared because of cost and general usability. The site uses the MAC address of this adapter to identify the device. So reusing the adapter becomes problematic without other administrator actions between each deployment. To reuse the adapter in this scenario, exclude its MAC address.

2. While the SMBIOS attribute should be unique, some specialty hardware devices have duplicate identifiers. Exclude this duplicate identifier and rely on the unique MAC address of each device.

Use the following process to add hardware identifiers for Configuration Manager to ignore:

1. In the Configuration Manager console, go to the **Administration** workspace, expand **Site Configuration**, and select the **Sites** node.

2. On the **Home** tab of the ribbon, in the **Sites** group, choose **Hierarchy Settings**.

3. Switch to the **Client Approval and Conflicting Records** tab. To add new hardware identifiers, choose **Add** in the **Duplicate hardware identifiers** section.

### PowerShell for duplicate hardware IDs

You can use the following PowerShell cmdlets to automate the management of duplicate hardware identifiers:<!-- 4852819 -->

- [Get-CMDuplicateHardwareIdGuid](/powershell/module/configurationmanager/get-cmduplicatehardwareidguid)
- [New-CMDuplicateHardwareIdGuid](/powershell/module/configurationmanager/new-cmduplicatehardwareidguid)
- [Remove-CMDuplicateHardwareIdGuid](/powershell/module/configurationmanager/remove-cmduplicatehardwareidguid)
- [Get-CMDuplicateHardwareIdMacAddress](/powershell/module/configurationmanager/get-cmduplicatehardwareidmacaddress)
- [New-CMDuplicateHardwareIdMacAddress](/powershell/module/configurationmanager/new-cmduplicatehardwareidmacaddress)
- [Remove-CMDuplicateHardwareIdMacAddress](/powershell/module/configurationmanager/remove-cmduplicatehardwareidmacaddress)

## Start policy retrieval

A Configuration Manager client downloads its client policy on a schedule that you configure as a client setting. You can also start on-demand policy retrieval from the client. For example, for troubleshooting or testing situations.

- [Client notification](#start-client-policy-retrieval-with-client-notification)
- [The client control panel](#start-client-policy-retrieval-from-the-configuration-manager-client-control-panel)
- [Support Center](#start-client-policy-retrieval-with-support-center-client-tools)
- [A script](#start-client-policy-retrieval-by-script)

### Start client policy retrieval with client notification

1. In the Configuration Manager console, go to the **Assets and Compliance** workspace, and select **Devices**.

1. Select the device that you want to download policy. On the **Home** tab of the ribbon, in the **Device** group, select **Client Notification**, and then choose **Download Computer Policy**.

    > [!NOTE]
    > You can also use client notification to start policy retrieval for all devices in a collection.

### Start client policy retrieval from the Configuration Manager client control panel

1. Open the **Configuration Manager** control panel on the computer.

2. Switch to the **Actions** tab. Select **Machine Policy Retrieval & Evaluation Cycle** to start the computer policy, and then select **Run Now**.

3. Select **OK** to confirm the prompt.

4. Repeat the previous steps for any other actions. For example, **User Policy Retrieval & Evaluation Cycle** for user client settings.

### Start client policy retrieval with Support Center Client Tools

Use Support Center Client Tools to request and view client policy. For more information, see [Support Center reference](../../support/support-center-ui-reference.md#policy-tab-client-tools).

### Start client policy retrieval by script

1. Open a script editor, such as Notepad or Windows PowerShell ISE.

2. Copy and insert the following sample PowerShell code<!-- SCCMDocs#1591 --> into the file:

    ```PowerShell
    $trigger = "{00000000-0000-0000-0000-000000000021}"
    Invoke-WmiMethod -Namespace root\ccm -Class sms_client -Name TriggerSchedule $trigger
    ```

    > [!TIP]
    > For more information about the schedule IDs, see [Message IDs](../../support/send-schedule-tool.md#bkmk_sendschedule-guids).

3. Save the file with a `.ps1` extension.

4. Run the script on the client.

## Next steps

[Configure the content cache for clients](configure-client-cache.md)

[Client notification](client-notification.md)
