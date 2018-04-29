---
title: "Manage clients"
titleSuffix: "Configuration Manager"
description: "Learn how to manage clients in System Center Configuration Manager."
ms.date: 12/21/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 3986a992-c175-4b6f-922e-fc561e3d7cb7
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# How to manage clients in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

When the Configuration Manager client installs on a device and successfully assigns to a site, you see the device in the **Assets and Compliance** workspace in the **Devices** node, and in one or more collections in the **Device Collections** node. When you select the device or a collection, you can perform management operations. However, there are other ways to manage the client, which might involve other workspaces in the console, or tasks outside of the console.  

> [!NOTE]  
>  If the Configuration Manager client is installed but hasn't yet successfully assigned to a site, it might not display in the console. After the client assigns to a site, update collection membership and refresh the console view.  
>   
>  Additionally, a device can also display in the console when the Configuration Manager client is not installed. This behavior happens if the device is discovered but the client is not installed and assigned. 
>
> Mobile devices managed by using the Exchange Server connector and devices enrolled to Microsoft Intune do not install the Configuration Manager client.  
>   
>  Use the **Client** column in the Configuration Manager console to determine whether the client is installed so that you can manage it from the console.  

##  <a name="BKMK_ManagingClients_DevicesNode"></a> Manage Clients from the Devices Node  

Depending on the device type, some of these options might not be available.  

1.  In the Configuration Manager console, choose **Assets and Compliance** >  **Devices**.  

3.  Select one or more devices, and then select one of these client management tasks from the ribbon, or by right-clicking the device:  

    -   **Manage user device affinity information**  

         Configure the associations between users and devices, so you can efficiently deploy software to users.  

         See [Link users and devices with user device affinity in System Center Configuration Manager](../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)  

    -   **Add the device to a new or existing collection**  

         Add the device to a collection with a direct rule.  

    -   **Install and reinstall the client by using the Client Push wizard**  

         Install and reinstall the Configuration Manager client to repair or reconfigure it. This option includes site configuration settings and client.msi properties that you set for client push installation.  

        > [!TIP]  
        >  There are many different ways to install (and reinstall) the Configuration Manager client. Although the Client Push wizard offers a convenient client installation method because you can run it from the console, this method has many dependencies and is not suitable for all environments. For more information about the dependencies, see [Prerequisites for deploying clients to Windows computers in System Center Configuration Manager](../../../core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers.md). For more information about the other client installation methods, see [Client installation methods in System Center Configuration Manager](../../../core/clients/deploy/plan/client-installation-methods.md).  

         See [How to Install Configuration Manager Clients by Using Client Push](../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush).  

    -   **Reassign Site**  

         Reassign one or more clients, including managed mobile devices, to another primary site in the hierarchy. Clients can be reassigned individually or can be multi-selected and reassigned in bulk to a new site.  

    -   **Remotely administer the client**  

         Run Resource Explorer to see the hardware and software inventory information from a Windows client. Remotely administer the device by using Remote Control, Remote Assistance, or Remote Desktop.  

         See [How to use Resource Explorer to view hardware inventory](../../../core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md) and [How to use Resource Explorer to view software inventory](../../../core/clients/manage/inventory/use-resource-explorer-to-view-software-inventory.md).  

         See [How to remotely administer a Windows client computer](../../../core/clients/manage/remote-control/remotely-administer-a-windows-client-computer.md).  

    -   **Approve a client**  

         When the client communicates with site systems using HTTP and a self-signed certificate, you must approve these clients to identify them as trusted computers. By default, the site configuration automatically approves clients from the same Active Directory forest and trusted forests so you do not have to manually approve each client. However, you must manually approve workgroup computers that you trust, and any other unapproved computers that you trust.  

        > [!WARNING]  
        >  Although some management functions might work for unapproved clients, this is an unsupported scenario for Configuration Manager.  

         You do not have to approve clients that always communicate to site systems using HTTPS, or clients that use a PKI certificate when they communicate to site systems using HTTP. These clients establish trust by using the PKI certificates.  

    -   **Block or unblock a client**  

         Block a client that you no longer trust. Blocking prevents the client from receiving policy, and prevents site systems from communicating with the client.  

        > [!WARNING]  
        >  Blocking a client only prevents communication from the client to Configuration Manager site systems and does not prevent communication to other devices. In addition, when the client communicates to site systems by using HTTP instead of HTTPS, there are some security limitations.  

         You can also unblock a client that is blocked. 

         See [Determine whether to block clients in System Center Configuration Manager](../../../core/clients/deploy/plan/determine-whether-to-block-clients.md).  

    -   **Clear a required PXE deployment**  

         Redeploy required PXE deployments for the computer.  

         See [Use PXE to deploy Windows over the network with System Center Configuration Manager](../../../osd/deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

    -   **Manage the client properties**  

         View the discovery data and deployments targeted for the client. You can also configure variables that task sequences use to deploy an operating system to the device.  

    -   **Delete the client**  

        > [!WARNING]  
        >  Do not delete a client if you want to uninstall the Configuration Manager client or remove it from a collection.  

         The **Delete** action manually deletes the client record from the Configuration Manager database and typically, you should not use this action except in troubleshooting scenarios. If you delete the client record but the client is still installed and communicating with the site, Heartbeat Discovery recreates the client record. The client record reappears in the Configuration Manager console, although the client history and any previous associations are lost.  

        > [!NOTE]  
        >  When you delete a mobile device client that was enrolled by Configuration Manager, this action also revokes the PKI certificate that was issued to the mobile device and this certificate is then rejected by the management point, even if IIS does not check the CRL. Certificates on mobile device legacy clients are not revoked when you delete these clients.  

         To uninstall the client, see [Uninstall the Configuration Manager Client](#BKMK_UninstalClient).  

         To assign the client to a new primary site, see [How to assign clients to a site in System Center Configuration Manager](../../../core/clients/deploy/assign-clients-to-a-site.md).  

         To remove the client from a collection, reconfigure the collection properties. See [How to manage collections in System Center Configuration Manager](../../../core/clients/manage/collections/manage-collections.md).  

    -   **Wipe a mobile device**  

         You can wipe mobile devices that support the wipe command.  

         This action permanently removes all data on the mobile device, including personal settings and personal data. Typically, this action resets the mobile device back to factory defaults. Wipe a mobile device when the mobile device is no longer trusted. For example, if the device is lost or stolen.  

        > [!TIP]  
        >  Check the manufacturer's documentation for more information about how the mobile device processes a remote wipe command.  

         There is often a delay until the mobile device receives the wipe command:  

        -   If the mobile device is enrolled by Configuration Manager or by Microsoft Intune, the client receives the command when it  downloads its client policy.  

        -   If the mobile device is managed by the Exchange Server connector, it receives the command when it synchronizes with Exchange.  

         You can use the **Wipe Status** column to monitor when the device receives the wipe command. Until the device sends a wipe acknowledgment to Configuration Manager, you can cancel the wipe command.  

    -   **Retire a mobile device**  

         The **Retire** option is supported only by mobile devices enrolled by Microsoft Intune or on\-premises mobile device management.  

         For more information, see [Help protect your data with remote wipe, remote lock, or passcode reset using System Center Configuration Manager](../../../mdm/deploy-use/wipe-lock-reset-devices.md).  

    -   **Change the ownership of a device**  

         If a device is not domain-joined and does not have the Configuration Manager client installed, use this option to change the ownership to **Company** or **Personal**.  

         You can use this value in application requirements to control deployments, and to control how much inventory is collected from users' devices.  

        You may need to add the **Device Owner** column to the view by right-clicking any column heading and choosing it.

         For more information, see [Hybrid mobile device management (MDM) with System Center Configuration Manager and Microsoft Intune](../../../mdm/understand/hybrid-mobile-device-management.md).  

##  <a name="BKMK_ManagingClients_DeviceCollectionsNode"></a> Manage clients from the Device Collections node  
  Many of the tasks that are available for devices in the **Devices** node are also available on collections. The console automatically applies the operation to all eligible devices in the collection. This action on an entire collection generates additional network packets and increases CPU usage on the site server.  

  Consider the following before you perform collection-level tasks. Once started, you cannot stop the task from the console. 
 - How many devices are in the collection?
 - Are the devices connected by low-bandwidth network connections?
 - How much time does this task need to complete for all the devices?

#### To manage clients from the Device Collections node  

1.  In the Configuration Manager console, choose **Assets and Compliance** > **Device Collections**.  

3.  Select a collection, and then select one of the following client management tasks from the ribbon, or by right-clicking the collection. These client management tasks can *only* be performed at the collection level.  

    -   **Scan computers for malware and download antimalware definition files.**  

         See [Endpoint Protection in System Center Configuration Manager](../../../protect/deploy-use/endpoint-protection.md).  

    -   **Deploy software, configuration baselines, and task sequences.**  

         See:  

        -   [Deploy software updates in System Center Configuration Manager](../../../sum/deploy-use/deploy-software-updates.md)  

        -   [Plan for and configure compliance settings in System Center Configuration Manager](../../../compliance/plan-design/plan-for-and-configure-compliance-settings.md)  

    -   **Configure power management settings.**  

         See [How to create and apply power plans in System Center Configuration Manager](../../../core/clients/manage/power/create-and-apply-power-plans.md). Power plans can only be used with computers that run Windows.  

    -   **Notify computers to download policy as soon as possible.**  

         Use client notification to notify the selected Windows clients to download computer policy as soon as possible outside the client policy polling interval.  

         Client notification tasks are displayed in the **Client Operations** node in the **Monitoring** workspace.  


## Restart clients
Beginning with version 1710, you can use the Configuration Manager console to identify clients that require a restart. Then use a client notification action to restart them.

> [!Tip]
> You must also upgrade clients to version 1710 for this capability to function. We recommend that you enable automatic client upgrade to keep your clients up to date with minimal administrative overhead. For more information, see [Use automatic client upgrade](/sccm/core/clients/manage/upgrade/upgrade-clients-for-windows-computers#use-automatic-client-upgrade).

To identify devices that are pending a restart, go to the **Assets and Compliance** workspace in the Configuration Manager console and select the **Devices** node. Then view the status for each device in the details pane in a new column named **Pending Restart**. Each device has one or more of the following values: 
 - **No**: there is no pending restart
 - **Configuration Manager**: this value comes from the client reboot coordinator component (RebootCoordinator.log)
 - **File rename**: this value comes from Windows reporting a pending file rename operation (HKLM\SYSTEM\CurrentControlSet\Control\Session Manager, PendingFileRenameOperations)
 - **Windows Update**: this value comes from the Windows Update Agent reporting a pending restart is required for one or more updates (HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\WindowsUpdate\Auto Update\RebootRequired)
 - **Add or remove feature**: this value comes from the Windows component-based servicing reporting the addition or removal of a Windows feature requires a restart (HKLM\Software\Microsoft\Windows\CurrentVersion\Component Based Servicing\Reboot Pending)

**To create the client notification to restart a device:**
1.	Locate the device you want to restart within a collection in the **Device Collections** node of the console.
2.	Right-click on the device, select **Client Notification**, and then select **Restart**. An information window opens about the restart. Click **OK** to confirm the restart request.

When the notification is received by a client, a **Software Center** notification window opens to inform the user about the restart. By default, the restart occurs after 90 minutes. You can modify the restart time by configuring [client settings](/sccm/core/clients/deploy/configure-client-settings). Settings for the restart behavior are found on the [Computer restart](/sccm/core/clients/deploy/about-client-settings#computer-restart) tab of the default settings.


##  <a name="BKMK_ClientCache"></a> Configure the Client Cache for Configuration Manager Clients  
The client cache stores temporary files for when clients install applications and programs. Software updates also use the client cache, but always attempt to download to the cache regardless of the size setting. Configure the cache settings, such as size and location, when you manually install the client, when you use client push installation, or after installation.

Beginning with Configuration Manager version 1606, you can specify the cache folder size using client settings in the Configuration Manager console.   

 The default location for the Configuration Manager client cache is %*windir*%\ccmcache and the default disk space is 5120 MB.  

> [!IMPORTANT]  
>  Do not encrypt the folder used for the client cache. Configuration Manager cannot download content to an encrypted folder.  

### About client cache  

The Configuration Manager client downloads the content for required software soon after it receives the deployment but waits to run it until the deployment scheduled time. At the scheduled time, the Configuration Manager client checks to see whether the content is available in the cache. If content is in the cache and it is the correct version, the client uses the cached content. When the required version of the content changes, or if the client deletes the content to make room for another package, the client downloads the content to the cache again.  

If the client attempts to download content for a program or application that is greater than the size of the cache, the deployment fails because of insufficient cache size. The client generates status message 10050 for insufficient cache size. If you increase the cache size later, the result is:  

-   For a required program: The client does not automatically retry to download the content. Redeploy the package and program to the client.  
-   For a required application: The client automatically retries to download the content when it downloads its client policy.  

If the client attempts to download a package that is less than the size of the cache but the cache is full, all required deployments keep retrying until the cache space is available, the download times out, or the retry count reaches its limit. If the cache size is increased later, the Configuration Manager client attempts to download the package again during the next retry interval. The client tries to download the content every four hours until it has tried 18 times.  

Cached content is not automatically deleted but remains in the cache for at least one day after the client used that content. If you configure the package properties with the option to persist content in the client cache, the client does not automatically delete the package content from the cache. If the cache space is used by packages downloaded within the last 24 hours and the client must download new packages, you can either increase the cache size or choose the option to delete persisted cache content.  

 Use the following procedures to configure the client cache during manual client installation, or after the client is installed.  

### To configure the client cache when you install clients by using manual client installation  

Run the CCMSetup.exe command from the install source location and specify the following properties that you require, and separated by spaces:  

   -   DISABLECACHEOPT  

    -   SMSCACHEDIR  

    -   SMSCACHEFLAGS  

    -   SMSCACHESIZE  

        > [!NOTE]
        > For version 1606, use the cache size settings available in **Client Settings** in the Configuration Manager console instead of SMSCACHESIZE. For more information, see [Client cache settings](../../../core/clients/deploy/about-client-settings.md#client-cache-settings).

For more information about how to use these command-line properties for CCMSetup.exe, see [About client installation properties](../../../core/clients/deploy/about-client-installation-properties.md).  

### To configure the client cache folder when you install clients by using client push installation  

1.  In the Configuration Manager console, choose **Administration** > **Site Configuration** > **Sites**.  

3.  Select the appropriate site, and on the **Home** tab, in the **Settings** group, choose **Client Installation Settings** > **Installation Properties tab**.  

5.  Specify the following properties, separated by spaces:  

    -   DISABLECACHEOPT  

    -   SMSCACHEDIR  

    -   SMSCACHEFLAGS  

    -   SMSCACHESIZE  

        > [!NOTE]
        > For version 1606, use the cache size settings available in **Client Settings** in the Configuration Manager console instead of SMSCACHESIZE. For more information, see [Client cache settings](../../../core/clients/deploy/about-client-settings.md#client-cache-settings).

       For more information about how to use these command-line properties for CCMSetup.exe, see [About client installation properties](../../../core/clients/deploy/about-client-installation-properties.md).  

### To configure the client cache folder on the client computer  

1.  On the client computer, navigate to **Configuration Manager** in Control Panel, and double-click to open the properties.  

2.  On the **Cache** tab set the space and location properties. The default location is *%windir%*\ccmcache.  

3.  To delete the files in the cache folder, choose **Delete Files**.  

### To configure client cache size in Client Settings

Adjust the size of the client cache without having to reinstall the client by configuring the cache size in the Configuration Manager console using Client Settings.  

1. In the Configuration Manager console, go to **Administration** > **Client Settings**.

2. Double-click **Default Client Settings**.
  You can also create custom client settings to apply the cache size more selectively. For more information on default and customer client settings, see [How to configure client settings in System Center Configuration Manager](../../../core/clients/deploy/configure-client-settings.md).

 3. Choose **Client Cache Settings** and choose **Yes** for **Configure client cache size**, then use either the **MB** or **percentage of disk settings**. Cache is adjusted to whichever size is less.

     The Configuration Manager client will configure the cache size with these settings when the next client policy is downloaded.



##  <a name="BKMK_UninstalClient"></a> Uninstall the Configuration Manager Client  
 You can uninstall the Windows Configuration Manager client software from a computer by using **CCMSetup.exe** with the **/Uninstall** property. Run CCMSetup.exe on an individual computer from the command prompt or deploy a package and program to uninstall the client for a collection of computers.  

> [!WARNING]  
>  You cannot uninstall the Configuration Manager client from a mobile device. If you must remove the Configuration Manager client from a mobile device, you must wipe the device, which deletes all data on the mobile device.  

#### To uninstall the Configuration Manager client from the command prompt  

1.  Open a Windows command prompt and change the folder to the location in which CCMSetup.exe is located.  

2.  Type **Ccmsetup.exe /uninstall**, and then press **Enter.**  

> [!NOTE]  
>  The uninstall process displays no results on the screen. To verify that client uninstallation has succeeded, examine the log file **CCMSetup.log** in the folder *%windir%\ ccmsetup* on the client computer.  

##  <a name="BKMK_ConflictingRecords"></a> Manage Conflicting Records for Configuration Manager Clients  
 Configuration Manager uses the hardware identifier to attempt to identify clients that might be duplicates and alert you to the conflicting records. For example, if you reinstall a computer, the hardware identifier would be the same but the GUID used by Configuration Manager might be changed.  

 Configuration Manager automatically resolves conflicts by using Windows authentication of the computer account or a PKI certificate from a trusted source. However, when Configuration Manager cannot resolve the conflict of duplicate hardware identifiers, a hierarchy setting determines whether to merge the records automatically, or allows you to determine the behavior. If you decide to manually manage duplicate records, you must manually resolve the conflicting records in the Configuration Manager console.  


#### To change the hierarchy setting for managing conflicting records  

1.  In the Configuration Manager console, choose **Administration** > **Site Configuration** > **Sites** > **Hierarchy Settings**
2.  On the **Client Approval and Conflicting Records** tab, choose either **Automatically resolve conflicting records**, or  **Manually resolve conflicting records**.  

#### To manually resolve conflicting records  

1.  In the Configuration Manager console, choose **Monitoring** > **System Status** > **Conflicting Records**.  

3.  Select one or more conflicting records, and then choose **Conflicting Record**.  

4.  Select one of the following options:  

    -   **Merge** to combine the newly detected record with the existing client record.  

    -   **New** to create a new record for the conflicting client record.  

    -   **Block** to create a new record for the conflicting client record, but mark it as blocked.  

## Manage duplicate hardware identifiers
Providing a list of hardware identifiers that Configuration Manager ignores for the purpose of PXE boot and client registration, helps to address two common issues.

1. Many new devices, like the Surface Pro 3, do not include an onboard Ethernet port. Technicians use a USB-to-Ethernet adapter to establish a wired connection for purposes of operating system deployment. However, these adapters are often shared due to cost and general usability. Because the MAC address of this adapter is used to identify the device, reusing the adapter becomes problematic without additional administrator actions between each deployment. To reuse the adapter in this scenario, exclude its MAC address.
2. While the SMBIOS attribute should be unique, some specialty hardware devices have duplicate identifiers. Exclude this duplicate identifier and rely on the unique MAC address of each device.

#### To add hardware identifiers for Configuration Manager to ignore  
1. In the Configuration Manager console, go to **Administration** > **Overview** > **Site Configuration** > **Sites**.
2. On the **Home** tab, in the **Sites** group, choose **Hierarchy Settings**.
3. On the **Client Approval and Conflicting Records** tab, choose **Add** in the **Duplicate hardware identifiers** section to add new hardware identifiers.

##  <a name="BKMK_PolicyRetrieval"></a> Initiate Policy Retrieval for a Configuration Manager Client  
 A Windows Configuration Manager client downloads its client policy on a schedule that you configure as a client setting. However, there might be occasions when you want to initiate on-demand policy retrieval from the client, for example, for troubleshooting or testing.  

You can initiate policy retrieval using:


- [Client notification](#initiate-client-policy-retrieval-using-client-notification)
- [The **Actions** tab on the client](#manually-initiate-client-policy-retrieval-on-the-actions-tab-of-the-configuration-manager-client)
- [A script](#manually-initiate-client-policy-retrieval-by-script)

> [!NOTE]  
>   
>  For information about policy retrieval for clients that run Linux and UNIX, see [Computer policy for Linux and UNIX servers](../../../core/clients/manage/manage-clients-for-linux-and-unix-servers.md#BKMK_PolicyforLnU).  

#### Initiate client policy retrieval using client notification  

1.  In the Configuration Manager console, choose **Assets and Compliance** > **Device Collections**.  

3.  Select the device collection containing the computers that you want to download policy. On the **Home** tab, in the **Collections** group, choose **Client Notification** > **Download Computer Policy**.  

    > [!NOTE]  
    >  You can also use client notification to initiate policy retrieval for one of more selected devices that are displayed in a temporary collection node under the **Devices** node.  

#### Manually initiate client policy retrieval on the Actions tab of the Configuration Manager client  

1.  Select **Configuration Manager** in the Control Panel of the computer.  

2.  On the **Actions** tab, choose **Machine Policy Retrieval & Evaluation Cycle** to initiate the computer policy, and then choose **Run Now**.  

4.  Choose **OK** to confirm the prompt.  

5.  Repeat steps 3 and 4 for any other actions that you require, such as **User Policy Retrieval & Evaluation Cycle** for user client settings.  

#### Manually initiate client policy retrieval by script  

1.  Open a text editor, such as Notepad.  

2.  Copy and insert the following sample Visual Basic Scripting Edition code into the file:  

    ```  
    on error resume next  

    dim oCPAppletMgr 'Control Applet manager object.  
    dim oClientAction 'Individual client action.  
    dim oClientActions 'A collection of client actions.  

    'Get the Control Panel manager object.  
    set  oCPAppletMgr=CreateObject("CPApplet.CPAppletMgr")  
    if err.number <> 0 then  
        Wscript.echo "Couldn't create control panel application manager"  
        WScript.Quit  
    end if  

    'Get a collection of actions.  
    set oClientActions=oCPAppletMgr.GetClientActions  
    if err.number<>0 then  
        wscript.echo "Couldn't get the client actions"  
        set oCPAppletMgr=nothing  
        WScript.Quit  
    end if  

    'Display each client action name and perform it.  
    For Each oClientAction In oClientActions  

        if oClientAction.Name = "Request & Evaluate Machine Policy" then  
            wscript.echo "Performing action " + oClientAction.Name   
            oClientAction.PerformAction  
        end if  
    next  

    set oClientActions=nothing  
    set oCPAppletMgr=nothing  
    ```  

3.  Save the file with a .vbs extension.  

4.  On the client computer, run the file using one of the following methods:  

    -   Navigate to the file by using Windows Explorer, and double-click the script file.  

    -   Open a command prompt, and type: **cscript &lt;path\filename.vbs>**.  

5.  Choose **OK** in the **Windows Script Host** dialog box.  
