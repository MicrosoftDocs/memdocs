---
title: "Manage clients | Microsoft Docs"
description: "Learn how to manage clients in System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3986a992-c175-4b6f-922e-fc561e3d7cb7
caps.latest.revision: 17
author: Mtillmanms.author: mtillmanmanager: angrobe

---
# How to manage clients in System Center Configuration Manager*Applies to: System Center Configuration Manager (Current Branch)*
When a System Center Configuration Manager client is installed and successfully assigned to a Configuration Manager site, you will see the device in the **Assets and Compliance** workspace in the **Devices** node, and in one or more collections in the **Device Collections** node. When you select the device or collection that contains the device, you can select various management operations. However, there are also other ways to manage the client, which might involve other workspaces in the console, or tasks that don't use the Configuration Manager console.  

 Use this topic for overview information for the tasks that can manage a Configuration Manager client from the **Assets and Compliance** workspace, as well as more detailed information about additional tasks to help you manage the Configuration Manager client. For information about how to configure the client, see [How to configure client settings in System Center Configuration Manager](../../../core/clients/deploy/configure-client-settings.md)  

> [!NOTE]  
>  A Configuration Manager client might be installed but not displayed in the Configuration Manager console. This scenario can happen if the client hasn't yet successfully assigned to a site, or the console must be refreshed or a collection membership updated.  
>   
>  Additionally, a device can also display in the console when the Configuration Manager client is not installed. This scenario can happen if the device is discovered but the Configuration Manager client is not installed and assigned. Mobile devices that are managed by using the Exchange Server connector do not install the Configuration Manager client. Additionally, devices that are enrolled by Microsoft Intune do not install the Configuration Manager client.  
>   
>  Use the **Client** column in the Configuration Manager console to determine whether the Configuration Manager client is installed so that you can manage it from the Configuration Manager console.  

##  <a name="BKMK_ManagingClients_DevicesNode"></a> Manage Clients from the Devices Node  
 Use the following procedure and table to manage one or more devices from the **Devices** node in the **Assets and Compliance** workspace.  

> [!IMPORTANT]  
>  Depending on the device type, some of these options might not be available.  

#### To manage clients from the Devices node  

1.  In the Configuration Manager console, click **Assets and Compliance**.  

2.  In the **Assets and Compliance** workspace, click **Devices**.  

3.  Select one or more devices, and then select one of the following client management tasks from the ribbon, or by right-clicking the device:  

    -   **Manage user device affinity information**  

         Allows you to configure the associations between users and devices, which enables you to efficiently deploy software to users.  

         See [Link users and devices with user device affinity in System Center Configuration Manager](../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)  

    -   **Add the device to a new or existing collection**  

         Use these collection-related actions to quickly add the selected device to a collection, by using a direct rule.  

         [Operations and maintenance for collections in System Center Configuration Manager](../../../core/clients/manage/collections/operations-and-maintenance-for-collections.md)  

    -   **Install and reinstall the client by using the Client Push wizard**  

         The Client Push wizard offers an efficient way to install and reinstall the Configuration Manager client to repair it or to reconfigure it on computers that run Windows with site configuration options and with any additional client.msi properties that you have specified for client push installation.  

        > [!TIP]  
        >  There are many different ways to install (and reinstall) the Configuration Manager client. Although the Client Push wizard offers a convenient client installation method because you can run it from the console, this client installation method has many dependencies and is not suitable for all environments. If you cannot successfully install the client by using client push, there are many other client installation methods that you can use. For more information about the dependencies, see [Prerequisites for deploying clients to Windows computers in System Center Configuration Manager](../../../core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers.md). For more information about the other client installation methods, see [Client installation methods in System Center Configuration Manager](../../../core/clients/deploy/plan/client-installation-methods.md).  

         See [How to Install Configuration Manager Clients by Using Client Push](../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush).  

    -   **Reassign Site**  

         Reassign one or more clients, including managed mobile devices, to another primary site in the hierarchy. Clients can be reassigned individually or can be multi-selected and reassigned in bulk to a new site.  

    -   **Remotely administer the client**  

         You can run Resource Explorer to see the hardware and software inventory information from a Windows client, and remotely administer it by using Remote Control, Remote Assistance, or Remote Desktop.  

         See [How to use Resource Explorer to view hardware inventory in System Center Configuration Manager](../../../core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md) and [How to use Resource Explorer to view software inventory in System Center Configuration Manager](../../../core/clients/manage/inventory/use-resource-explorer-to-view-software-inventory.md).  

         See [How to remotely administer a Windows client computer by using System Center Configuration Manager](../../../core/clients/manage/remote-control/remotely-administer-a-windows-client-computer.md).  

    -   **Approve a client**  

         When the client communicates with site systems by using HTTP and a self-signed certificate, you must approve these clients to identify them as trusted computers. By default, the site configuration automatically approves clients from the same Active Directory forest and trusted forests so you do not have to manually approve each client. However, you must manually approve workgroup computers that you trust and any other computers that you trust but are not approved.  

        > [!WARNING]  
        >  Although some management functions might work for unapproved clients, this is an unsupported scenario for Configuration Manager.  

         You do not have to approve clients that always communicate to site systems by using HTTPS rather than HTTP, or clients that use a PKI certificate when they communicate to site systems by using HTTP. These clients establish trust with Configuration Manager by using the PKI certificates.  

    -   **Block or unblock a client**  

         Block a client that you no longer trust, to prevent it from receiving client policy and to prevent Configuration Manager site systems from communicating with it.  

        > [!WARNING]  
        >  Blocking a client only prevents communication from the client to Configuration Manager site systems and does not prevent communication to other devices. In addition, when the client communicates to site systems by using HTTP instead of HTTPS, there are some security limitations.  

         If you later change your mind, you can unblock a client that has been blocked. However, if you unblock an Intel AMT-based computer that was provisioned for AMT when it was blocked, you must take additional steps before you can manage that computer again out of band.  

         See [Determine whether to block clients in System Center Configuration Manager](../../../core/clients/deploy/plan/determine-whether-to-block-clients.md).  

    -   **Clear a required PXE deployment**  

         Use this option to redeploy any required PXE deployments for the selected computer.  

         See [Use PXE to deploy Windows over the network with System Center Configuration Manager](../../../osd/deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

    -   **Manage the client properties**  

         You can view the discovery data and deployments targeted for the client. You can also configure any variables that task sequences use to deploy an operating system to the device.  

    -   **Delete the client**  

        > [!WARNING]  
        >  Do not delete a client if you want to uninstall the Configuration Manager client or remove it from a collection.  

         The **Delete** action manually deletes the client record from the Configuration Manager database and typically, you should not use this action unless it is for troubleshooting scenarios. If you delete the client record and the Configuration Manager client is still installed and communicating with Configuration Manager, Heartbeat Discovery will recreate the client record and it will reappear in the Configuration Manager console, although the client history and any previous associations will be lost.  

        > [!NOTE]  
        >  When you delete a mobile device client that was enrolled by Configuration Manager, this action also revokes the PKI certificate that was issued to the mobile device and this certificate is then rejected by the management point, even if IIS does not check the CRL. Certificates on mobile device legacy clients are not revoked when you delete these clients.  

         To uninstall the client, see [Uninstall the Configuration Manager Client](#BKMK_UninstalClient).  

         To assign the client to a new primary site, see [How to assign clients to a site in System Center Configuration Manager](../../../core/clients/deploy/assign-clients-to-a-site.md).  

         To remove the client from a collection, reconfigure the collection properties. See [How to manage collections in System Center Configuration Manager](../../../core/clients/manage/collections/manage-collections.md).  

    -   **Wipe a mobile device**  

         You can wipe mobile devices that support the wipe command.  

         This action permanently removes all data on the mobile device, which includes personal settings and personal data. Typically, this action resets the mobile device back to factory defaults. Wipe a mobile device when the mobile device is no longer trusted; for example, it has been lost or stolen.  

        > [!TIP]  
        >  Check the manufacturer's documentation for more information about how the mobile device processes a remote wipe command.  

         When you send a wipe request, there is often a delay until the mobile device receives the wipe command:  

        -   If the mobile device is enrolled by Configuration Manager or by Microsoft Intune, the client receives the wipe command when it next downloads its client policy.  

        -   If the mobile device is managed by the Exchange Server connector, the mobile device receives the wipe command when it next synchronizes with Exchange.  

         You can use the **Wipe Status** column to monitor when the mobile device receives the wipe command. Until the mobile device sends a wipe acknowledgment to Configuration Manager, you can cancel the wipe command.  

    -   **Retire a mobile device**  

         The **Retire** option is supported only by mobile devices that are enrolled by Intune or by On\-premises Mobile Device Management.  

         For more information, see [Help protect your data with remote wipe, remote lock, or passcode reset using System Center Configuration Manager](../../../mdm/deploy-use/wipe-lock-reset-devices.md).  

    -   **Change the ownership of a device**  

         You can change the ownership of devices to **Company** or **Personal** if a device is not domain-joined and does not have the Configuration Manager client installed.  

         You can use this value in application requirements to control deployments and you can also use this configuration to control how much inventory is collected from users' devices.  

        To see the ownership value in the devices list, you may need to add the column to the view by right-clicking any column heading and choosing **Device Owner**.

         For more information, see [Hybrid mobile device management (MDM) with System Center Configuration Manager and Microsoft Intune](../../../mdm/plan-design/hybrid-mobile-device-management.md).  

##  <a name="BKMK_ManagingClients_DeviceCollectionsNode"></a> Manage Clients from the Device Collections Node  
 Use the following procedure and table to manage devices in a collection from the **Device Collections** node in the **Assets and Compliance** workspace.  

 Many of the client management tasks that you can perform when you select a single device or multiple devices from the **Devices** node can also be performed at the collection level. This has the advantage of automatically applying the management task to all eligible devices in the collection. Although this can be a convenient method to manage multiple clients at the same time, it can also generate a lot of network packets and increase the CPU usage on the site server.  

 There are also some client management tasks that can only be performed at the collection level, which are listed in the following table.  

 Before you perform collection-level client management tasks, consider how many devices are in the collection, whether they are connected by low-bandwidth network connections, and how long the task will take to complete for all the devices. When you perform a client management task, you cannot stop it from the console.  

#### To manage clients from the Device Collections node  

1.  In the Configuration Manager console, click **Assets and Compliance**.  

2.  In the **Assets and Compliance** workspace, click **Device Collections**.  

3.  Select a collection, and then select one of the following client management tasks from the ribbon, or by right-clicking the collection:  

    -   **Scan computers for malware and download antimalware definition files.**  

         See [Endpoint Protection in System Center Configuration Manager](../../../protect/deploy-use/endpoint-protection.md).  

    -   **Deploy software, configuration baselines, and task sequences.**  

         For more information about deploying software and configuration baselines, see the following:  

        -   [Deploy software updates in System Center Configuration Manager](../../../sum/deploy-use/deploy-software-updates.md)  

        -   [Plan for and configure compliance settings in System Center Configuration Manager](../../../compliance/plan-design/plan-for-and-configure-compliance-settings.md)  

    -   **Configure power management settings.**  

         See [How to create and apply power plans in System Center Configuration Manager](../../../core/clients/manage/power/create-and-apply-power-plans.md). Power plans can only be used with computers that run Windows.  

    -   **Notify computers to download policy as soon as possible.**  

         Use client notification to notify the selected Windows clients to download computer policy as soon as possible outside the configured client policy polling interval.  

         Client notification tasks are displayed in the **Client Operations** node in the **Monitoring** workspace.  

##  <a name="BKMK_ClientCache"></a> Configure the Client Cache for Configuration Manager Clients  
 You can configure the location and amount of disk space that Windows Configuration Manager clients use to store temporary files for when they install applications and programs. Software updates also use the client cache, but software updates are not restricted by the configured cache size and will always attempt to download to the cache. You can configure the client cache settings when you install the Configuration Manager client manually, when you use client push installation, or after the client is installed.

In Configuration Manager version 1606, you can specify the cache folder size using client settings in the Configuration Manager console.   

 The default location for the Configuration Manager client cache is %*windir*%\ccmcache and the default disk space is 5120 MB.  

> [!IMPORTANT]  
>  Do not encrypt the folder used for the client cache. Configuration Manager cannot download content to an encrypted folder.  

### About client cache  

The Configuration Manager client downloads the content for required software soon after it receives the deployment but waits to run it until the deployment scheduled time. At the scheduled time, the Configuration Manager client checks to see whether the content is available in the cache. If content is in the cache and it is the correct version, the client always uses this cached content. However, when the required version of the content has changed or if the content was deleted to make room for another package, the content is downloaded to the cache again.  

If the client attempts to download content for a program or application that is greater than the size of the cache, the deployment fails because of insufficient cache size and Configuration Manager generates status message ID 10050. If the cache size is increased later, the download retry behavior is different for a required program and a required application:  

-   For a required program: The client does not automatically retry to download the content. You must redeploy the package and program to the client.  
-   For a required application: Because an application deployment is state-based, the client automatically retries to download the content when it next downloads its client policy.  

If the client attempts to download a package that is less than the size of the cache but the cache is currently full, all required deployments keep retrying until the cache space is available, until the download times out, or until the retry limit is reached for the cache space failure. If the cache size is increased later, the Configuration Manager client attempts to download the package again during the next retry interval. The client tries to download the content every four hours until it has tried 18 times.  

Cached content is not automatically deleted but remains in the cache for at least one day after the client used that content. If you configure the package properties with the option to persist content in the client cache, the client does not automatically delete the package content from the cache. If the client cache space is used by packages that have been downloaded within the last 24 hours and the client must download new packages, you can either increase the client cache size or choose the delete option to delete persisted cache content.  

 Use the following procedures to configure the client cache during manual client installation, or after the client is installed.  

### To configure the client cache when you install clients by using manual client installation  

Run the CCMSetup.exe command from the install source location and specify the following properties that you require, and separated by spaces:  

   -   DISABLECACHEOPT  

    -   SMSCACHEDIR  

    -   SMSCACHEFLAGS  

    -   SMSCACHESIZE  

        > [!NOTE]
        > For version 1606, use the cache size settings available in **Client Settings** in the Configuration Manager console instead of SMSCACHESIZE. For more information see [Client Cache Settings](../../../core/clients/deploy/about-client-settings.md#Client-Cache-Settings).

For more information about how to use these command line properties for CCMSetup.exe, see [About client installation properties in System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md).  

### To configure the client cache folder when you install clients by using client push installation  

1.  In the Configuration Manager console, click **Administration.**  

2.  In the **Administration** workspace, expand **Site Configuration**, and then click **Sites**.  

3.  In the **Sites** list, select the site for which you want to configure automatic site-wide client push installation.  

4.  On the **Home** tab, in the **Settings** group, click **Client Installation Settings**, and then click the **Installation Properties tab**.  

5.  On the **Installation Properties** tab, specify the following properties that you require, and separate them by using spaces:  

    -   DISABLECACHEOPT  

    -   SMSCACHEDIR  

    -   SMSCACHEFLAGS  

    -   SMSCACHESIZE  

        > [!NOTE]
        > For version 1606, use the cache size settings available in **Client Settings** in the Configuration Manager console instead of SMSCACHESIZE. For more information see [Client Cache Settings](../../../core/clients/deploy/about-client-settings.md#Client-Cache-Settings).

       For more information about how to use these command line properties for CCMSetup.exe, see [About client installation properties in System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md).  

6.  Click **OK** to save the properties that you have specified.  

### To configure the client cache folder on the client computer  

1.  On the client computer, navigate to **Configuration Manager** in Control Panel, and then double-click to open the properties.  

2.  Click the **Cache** tab.  

3.  Specify the disk space to reserve for the client cache.  

4.  To change the location of the client cache folder, click **Change Location**, and then specify the new location. The default location is *%windir%*\ccmcache.  

5.  To delete the files currently stored in the client cache folder, click **Delete Files**.  

6.  Click **OK** to close **Configuration Manager Properties**.  

### To configure client cache size in Client Settings

Beginning in version 1606, you can adjust the size of the client cache folder without having to reinstall the client. To do this, you configure client cache size in the Configuration Manager console using Client Settings.  

1. In the Configuration Manager console, go to **Administration** > **Client Settings**.

2. Double-click **Default Client Settings**.
  You can also create custom client settings to apply the cache size more selectively. For more information on default and customer client settings, see [How to configure client settings in System Center Configuration Manager](../../../core/clients/deploy/configure-client-settings.md).

 3. Click **Client Cache Settings** and choose **Yes** for **Configure client cache size**.

 4. Adjust the maximum cache size using either the **MB** or **percentage of disk settings**. Cache is adjusted to whichever size is less.

 5. Click **OK**.

    The Configuration Manager client will configure the cache size with these settings when the next client policy is downloaded.

##  <a name="BKMK_UninstalClient"></a> Uninstall the Configuration Manager Client  
 You can uninstall the Windows Configuration Manager client software from a computer by using **CCMSetup.exe** with the **/Uninstall** property. Run CCMSetup.exe on an individual computer from the command prompt or deploy a package and program to uninstall the client for a collection of computers.  

> [!WARNING]  
>  You cannot uninstall the Configuration Manager client from a mobile device. If you must remove the Configuration Manager client from a mobile device, you must wipe the device, which deletes all data on the mobile device.  

 Use the following procedure to uninstall the Configuration Manager client from computers.  

#### To uninstall the Configuration Manager client from the command prompt  

1.  Open a Windows command prompt and change the folder to the location in which CCMSetup.exe is located.  

2.  Type **Ccmsetup.exe /uninstall**, and then press **Enter.**  

> [!NOTE]  
>  The uninstall process is silent and displays no results on the screen. To verify that client uninstallation has succeeded, examine the log file **CCMSetup.log** in the folder *%windir%\ ccmsetup* folder on the client computer.  

##  <a name="BKMK_ConflictingRecords"></a> Manage Conflicting Records for Configuration Manager Clients  
 Configuration Manager uses the hardware ID to attempt to identify clients that might be duplicates and alert you to the conflicting records. For example, if you reinstall a computer, the hardware ID would be the same but the GUID used by Configuration Manager might be changed.  

 When Configuration Manager can resolve a conflict by using Windows authentication of the computer account or a PKI certificate from a trusted source, the conflict is automatically resolved for you. However, when Configuration Manager cannot resolve the conflict, it uses a hierarchy setting that either automatically merges the records when it detects duplicate hardware IDs (the default setting), or allows you to decide when to merge, block, or create new client records. If you decide to manually manage duplicate records, you must manually resolve the conflicting records by using the Configuration Manager console.  

#### To change the hierarchy setting for managing conflicting records  

1.  In the Configuration Manager console, click **Administration.**  

2.  In the **Administration** workspace, expand **Site Configuration**, and then click **Sites**.  

3.  In the **Sites** group, click **Hierarchy Settings**, and then click the **Client Approval and Conflicting Records** tab.  

4.  Click either **Automatically resolve conflicting records** to automatically merge conflicting records, or click **Manually resolve conflicting records**, and then click **OK**.  

    > [!NOTE]  
    >  When Configuration Manager can resolve the conflict by using the computer account or a PKI certificate, this setting is ignored and the conflict is automatically resolved.  

#### To manually resolve conflicting records  

1.  In the Configuration Manager console, click **Monitoring.**  

2.  In the **Monitoring** workspace, expand **System Status**, and then click **Conflicting Records**.  

3.  In the results pane, select one or more conflicting records, and then click **Conflicting Record**.  

4.  In the **Conflicting Record** dialog box, select one of the following, and then click **OK**:  

    -   **Merge** to combine the newly detected record with the existing client record, creating one unified record.  

    -   **New** to create a new record for the conflicting client record.  

    -   **Block** to create a new record for the conflicting client record, but mark it as blocked.  

##  <a name="BKMK_PolicyRetrieval"></a> Initiate Policy Retrieval for a Configuration Manager Client  
 A Windows Configuration Manager client downloads its client policy on a schedule that you configure as a client setting. However, there might be occasions when you want to initiate ad-hoc policy retrieval from the client; for example, in a troubleshooting scenario or when you are testing.  

 Use the following procedures to initiate ad-hoc policy retrieval from the client outside its scheduled polling interval, either by using the **Actions** tab on the Configuration Manager client or by running a script on the computer. You must be logged on to the client computer with local administrative rights to perform these procedures.  

> [!NOTE]  
>  You can use client notification to initiate client policy retrieval outside the scheduled client policy polling interval.  
>   
>  You can manage clients that run Linux and UNIX. For information about policy retrieval for clients that run Linux and UNIX, see [Computer policy for Linux and UNIX servers](../../../core/clients/manage/manage-clients-for-linux-and-unix-servers.md#BKMK_PolicyforLnU).  

#### To initiate client policy retrieval by using client notification  

1.  In the Configuration Manager console, click **Assets and Compliance**.  

2.  In the **Assets and Compliance** workspace, click **Device Collections**.  

3.  Select the device collection containing the computers that you want to download policy and then, in the **Home** tab, in the **Collections** group, click **Client Notification** and then click **Download Computer Policy**.  

    > [!NOTE]  
    >  You can also use client notification to initiate policy retrieval for one of more selected devices that are displayed in a temporary collection node under the **Devices** node.  

#### To manually initiate client policy retrieval by using the Actions tab on the Configuration Manager client  

1.  Select **Configuration Manager** in the Control Panel of the computer.  

2.  Click the **Actions** tab.  

3.  Click **Machine Policy Retrieval & Evaluation Cycle** to initiate the computer policy, and then click **Run Now**.  

4.  Click **OK** to confirm the prompt.  

5.  Repeat steps 3 and 4 for any other actions that you require, such as **User Policy Retrieval & Evaluation Cycle** for user client settings.  

6.  Click **OK** to close **Configuration Manager Properties**.  

#### To manually initiate client policy retrieval by using a script  

1.  Open a text editor, such as Notepad.  

2.  Copy and insert the following into the file:  

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

5.  Click **OK** in the **Windows Script Host** dialog box.  
