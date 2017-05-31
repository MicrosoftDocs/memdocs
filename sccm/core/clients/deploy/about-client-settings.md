---
title: "Client settings | Microsoft Docs"
description: "Choose client settings by using the admin console in System Center Configuration Manager."
ms.custom: na
ms.date: 03/24/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f7560876-8084-4570-aeab-7fd44f4ba737
caps.latest.revision: 15
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
---
# About client settings in System Center Configuration Manager

*Applies to: System Center Configuration Manager (current branch)*

All client settings in System Center Configuration Manager are managed in the Configuration Manager console from the **Client Settings** node in the **Administration** workspace. Configuration Manager comes with a set of default settings. When you change the default client settings, these settings are applied to all clients in the hierarchy. You can also configure custom client settings, which override the default client settings when you assign these to collections. For information about how to configure client settings, see [How to configure client settings in System Center Configuration Manager](../../../core/clients/deploy/configure-client-settings.md).  

Many of the client settings are self-explanatory. Others are described here.  

## Background Intelligent Transfer Service  

-   **Limit the maximum network bandwidth for BITS background transfers**  

   When this option is **True** or **Yes**, the clients will use BITS bandwidth throttling.  

-   **Throttling window start time**  

   Specify the local start time for the BITS throttling window.  

-   **Throttling window end time**  

   Specify the local end time for the BITS throttling window. If equal to **Throttling window start time**, BITS throttling is always enabled.  

-   **Maximum transfer rate during throttling window (Kbps)**  

   Specify the maximum transfer rate that clients can use during the window.  

-   **Allow BITS downloads outside the throttling window**  

   Choose this option to allow Configuration Manager clients to use separate BITS settings outside the specified window.  

-   **Maximum transfer rate outside the throttling window (Kbps)**  

   Specify the maximum transfer rate that clients will use outside the BITS throttling window, when you have chosen to allow BITS throttling outside the window.  

## Client cache settings

- **Configure BranchCache**

  Beginning in version 1606, use this setting to set up the client computer for [BranchCache](/sccm/core/plan-design/configs/support-for-windows-features-and-networks#branchcache). To allow BranchCache caching on the client, set **Enable BranchCache** to **Yes**.

- **Configure client cache size**

  The client cache on Windows computers stores temporary files used to install applications and programs. Choose **Yes** to specify **Maximum cache size** (megabytes or percentage of disk). If this option is **No**, the default size is 5,120 MB.

## Client policy  

-   **Client policy polling interval (minutes)**  

   Specify how frequently the following Configuration Manager clients download client policy:  

  -   Windows computers (for example, desktops, servers, laptops)  

  -   Mobile devices that Configuration Manager enrolls  

  -   Mac computers  

  -   Computers that run Linux or UNIX  

-   **Enable user policy polling on clients**  

   When you set this option to **True** or **Yes**, and Configuration Manager has [discovered the user](../../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser), clients on computers receive applications and programs that are targeted to the logged-on user.  

   Because the Application Catalog receives the list of available software for users from the site server, this setting does not have to be **True** or **Yes** for users to see and request applications from the Application Catalog. But if this setting is **False** or **No**, the following will not work when users use the Application Catalog:  

  -   Users cannot install the applications that they see in the Application Catalog.  

  -   Users will not see notifications about their application approval requests. Instead, they must refresh the Application Catalog and check the approval status.  

  -   Users will not receive revisions and updates for applications that are published to the Application Catalog. But they will see changes to application information in the Application Catalog.  

  -   If you remove an application deployment after the client has installed the application from the Application Catalog, clients continue to check that the application is installed for up to 2 days.  

   In addition, when this setting is **False** or **No**, users will not receive required applications that you deploy to users or any other management tasks in user policies.  

   This setting applies to users when their computer is on the intranet and the Internet. It must be **True** or **Yes** if you also want to enable user policies on the Internet.  

-   **Enable user policy requests from Internet clients**  

   When the client and site are configured for Internet-based client management and you set this option as **True** or **Yes** and both of the following conditions apply, users receive the user policy when their computer is on the Internet:  

  -   The **Enable user policy polling on clients** client setting is **True**, or **Enable user policy on clients** is **Yes**.  

  -   The Internet-based management point successfully authenticates the user by using Windows authentication (Kerberos or NTLM).  

   If you leave this option as **False** or **No**, or if either of the conditions fails, a computer on the Internet will receive computer policies only. In this scenario, users can still see, request, and install applications from an Internet-based Application Catalog. If this setting is **False** or **No** but **Enable user policy polling on clients** is **True** or **Enable user policy on clients** is **Yes**, users will not receive user policies until the computer is connected to the intranet.  

   For more information about managing clients on the Internet, see  [Considerations for client communications from the Internet or an untrusted forest](../../../core/plan-design/hierarchy/communications-between-endpoints.md#BKMK_clientspan) in [Communications between endpoints in System Center Configuration Manager](../../../core/plan-design/hierarchy/communications-between-endpoints.md).  

  > [!NOTE]  
  >  Application approval requests from users do not require user policies or user authentication.  

##  Compliance settings  

-   **Schedule compliance evaluation**  

     Choose **Schedule** to create the default schedule that will be shown to users when they deploy a configuration baseline. This value can be configured for each baseline in the **Deploy Configuration Baseline** dialog box.  

-   **Enable User Data and Profiles**  

     Choose **Yes** if you want to deploy [user data and profiles](../../../compliance/deploy-use/create-user-data-and-profiles-configuration-items.md) configuration items to Windows 8 computers in your hierarchy.  

## Computer agent  

-   **Default Application Catalog website point**  

     Configuration Manager uses this setting to connect users to the Application Catalog from Software Center. You can specify a server that hosts the Application Catalog website point by its NetBIOS name or FQDN, specify automatic detection, or specify a URL for customized deployments. In most cases, automatic detection is the best choice because it offers the following benefits:  

    -   Clients are automatically given an Application Catalog website point from their site, if their site has an Application Catalog website point.  

    -   Application Catalog website points on the intranet that are configured for HTTPS are given preference over those that aren't configured for HTTPS. This helps protect against a rogue server.

    -   When clients are configured for intranet-based and Internet-based client management, they will be given an Internet-based Application Catalog website point when they are on the Internet and an intranet-based Application Catalog website point when they are on the intranet.  

     Automatic detection does not guarantee that clients will be given an Application Catalog website point that is closest to them. You might decide not to use **Automatically detect** for the following reasons:  

     -   You want to manually configure the closest server for clients or ensure that they do not connect to a server across a slow network connection.  

     -   You want to control which clients connect to which server. This might be for testing, performance, or business reasons.  

     -   You do not want to wait up to 25 hours or for a network change for clients to be configured with a different Application Catalog website point.  

     If you specify the Application Catalog website point rather than use automatic detection, specify the NetBIOS name rather than the intranet FQDN. This helps reduce the likelihood that users will be prompted for credentials when they connect to the Application Catalog on the intranet. To use the NetBIOS name, the following conditions must apply:  

     -   The NetBIOS name is specified in the Application Catalog website point properties.  

     -   You use WINS, or all clients are in the same domain as the Application Catalog website point.  

     -   The Application Catalog website point is configured for HTTP client connections, or it is configured for HTTPS client connections and the web server certificate has the NetBIOS name.  

     Typically, users are prompted for credentials when the URL has an FQDN but not when the URL is a NetBIOS name. Expect users to be always prompted when they connect from the Internet, because this connection must use the Internet FQDN. When users are prompted for credentials when they are on the Internet, ensure that the server that runs the Application Catalog website point can connect to a domain controller for the user’s account so that the user can be authenticated by using Kerberos.  

    > [!NOTE]  
    >  How automatic detection works:  
    >   
    >  The client makes a service location request to a management point. If there is an Application Catalog website point in the same site as the client, this server is given to the client as the Application Catalog server to use. When more than one Application Catalog website point is available in the site, an HTTPS-enabled server takes precedence over a server that is not enabled for HTTPS. After this filtering, all clients are given one of the servers to use as the Application Catalog; Configuration Manager does not load-balance between multiple servers. When the client’s site does not have an Application Catalog website point, the management point nondeterministically returns an Application Catalog website point from the hierarchy.  
    >   
    >  When the client is on the intranet, if the chosen Application Catalog website point is configured with a NetBIOS name for the Application Catalog URL, clients are given this NetBIOS name instead of the intranet FQDN. When the client is detected to be on the Internet, only the Internet FQDN is given to the client.  
    >   
    >  The client makes this service location request every 25 hours or whenever it detects a network change. For example, if the client moves from the intranet to the Internet, and the client can locate an Internet-based management point, the Internet-based management point gives Internet-based Application Catalog website point servers to clients.  

-   **Add default Application Catalog website to Internet Explorer trusted sites zone**  

     If this option is **True** or **Yes**, the current default Application Catalog website URL is automatically added to the trusted sites zone in Internet Explorer on clients.  

     This setting ensures that the Internet Explorer setting for Protected Mode is not enabled. If Protected Mode is enabled, the Configuration Manager client might not be able to install applications from the Application Catalog. By default, the trusted sites zone also supports user logon for the Application Catalog, which requires Windows authentication.  

     If you leave this option as **False**, Configuration Manager clients might not be able to install applications from the Application Catalog unless these Internet Explorer settings are configured in another zone for the Application Catalog URL that clients use.  

    > [!NOTE]  
    >  Whenever Configuration Manager adds a default Application Catalog to the trusted sites zone, Configuration Manager removes a previous default Application Catalog URL that Configuration Manager added before it adds a new entry.  
    >   
    >  Configuration Manager cannot add the URL if it is already specified in one of the security zones. In this scenario, you must either remove the URL from the other zone or manually configure the required Internet Explorer settings.  

-   **Allow Silverlight applications to run in elevated trust mode**  

     This setting must be **Yes** if users run the Configuration Manager client and use the Application Catalog.  

     If you change this setting, it takes effect when users next load their browser or refresh their currently opened browser window.  

     For more information about this setting, see [Certificates for Microsoft Silverlight 5, and elevated trust mode required for the application catalog](../../../apps/plan-design/security-and-privacy-for-application-management.md#BKMK_CertificatesSilverlight5) in [Security and privacy for application management in System Center Configuration Manager](../../../apps/plan-design/security-and-privacy-for-application-management.md).  

-   **Organization Name displayed in Software Center**  

     Type the name that users see in Software Center. This branding information helps users to identify this application as a trusted source.  

-   **Use new Software Center**  

     If enabled, all client computers targeted by these client settings will use the new Software Center. Software Center shows user-available apps that were previously accessible only in the Silverlight-dependent Application Catalog.  

     The Application Catalog website point and Application Catalog web service point site system roles are still required for user-available apps to appear in Software Center.  

     For more information, see [Plan for and configure application management in System Center Configuration Manager](../../../apps/plan-design/plan-for-and-configure-application-management.md).  

-   **Install Permissions**  

    > [!WARNING]  
    >  This setting applies to the Application Catalog and Software Center. This setting has no effect when users use the company portal.  

     Configure how users can initiate the installation of software, software updates, and task sequences:  

    -   **All Users**: Users logged on to a client computer with any permission except Guest can initiate the installation of software, software updates, and task sequences.  

    -   **Only Administrators**: Users logged on to a client computer must be a member of the local Administrators group to initiate the installation of software, software updates, and task sequences.  

    -   **Only Administrators and primary users**: Users logged on to a client computer must be a member of the local Administrators group or a primary user of the computer to initiate the installation of software, software updates, and task sequences.  

    -   **No Users**: No users logged on to a client computer can initiate the installation of software, software updates, and task sequences. Required deployments for the computer are always installed at the deadline. Users cannot initiate the installation of software from the Application Catalog or Software Center.  

-   **Suspend BitLocker PIN entry on restart**  

     If the BitLocker PIN entry is configured on computers, this option can bypass the requirement to enter a PIN when the computer restarts after a software installation.  

    -   **Always**: Configuration Manager temporarily suspends BitLocker after it has installed software that requires a restart and initiated a restart of the computer. This setting applies only to a computer restart that is initiated by Configuration Manager and does not suspend the requirement to enter the BitLocker PIN when the user restarts the computer. The BitLocker PIN entry requirement is resumed after Windows startup.

    -   **Never**: Configuration Manager does not suspend BitLocker on the next computer startup after it has installed software that requires a restart. In this scenario, the software installation cannot finish until the user enters the PIN to complete the standard startup process and load Windows.

-   **Additional software manages the deployment of applications and software updates**  

     Enable this option only if one of the following conditions apply:  

    -   You use a vendor solution that requires this setting to be enabled.  

    -   You use the Configuration Manager software development kit (SDK) to manage client agent notifications and the installation of applications and software updates.  

    > [!WARNING]  
    >  If you choose this option when neither of these conditions applies, software updates and required applications will not be installed on clients. This setting does not prevent users from installing applications from the Application Catalog, or prevent packages, programs, and task sequences from being installed on client computers.  

-   **PowerShell execution policy**  

     Configure how Configuration Manager clients can run Windows PowerShell scripts. These scripts are often used for detection in configuration items for compliance settings. They can also be sent in a deployment as a standard script.  

    -   **Bypass**: The Configuration Manager client bypasses the Windows PowerShell configuration on the client computer so that unsigned scripts can run.  

    -   **Restricted**: The Configuration Manager client uses the current Windows PowerShell configuration on the client computer. This configuration determines whether unsigned scripts can run.  

    -   **All Signed**: The Configuration Manager client runs scripts only if a trusted publisher has signed them. This restriction applies independently from the current Windows PowerShell configuration on the client computer.  

     This option requires at least Windows PowerShell version 2.0. The default is **All Signed**.  

    > [!TIP]  
    >  If unsigned scripts fail to run because of this client setting, Configuration Manager reports this error in the following ways:  
    >   
    > -   Error ID **0X87D00327** and the description of **Script is not signed** as a deployment status error in the **Monitoring** workspace of the Configuration Manager console.  
    > -   Error codes and descriptions of **0X87D00327** and **Script is not signed** or **0X87D00320** and **The script host has not been installed yet** with the error type of **Discovery Error** in reports. An example is **Details of errors of configuration items in a configuration baseline for an asset**.  
    > -   The message **Script is not signed (Error: 87D00327; Source: CCM)** in the **DcmWmiProvider.log** file.  

-   **Disable deadline randomization**  

     This setting determines whether the client uses an activation delay of up to 2 hours to install required software updates when the deadline is reached. By default, the activation delay is disabled.  

     For virtual desktop infrastructure (VDI) scenarios, this delay can help to distribute the CPU processing and data transfer for a computer that has multiple virtual machines that run the Configuration Manager client. Even if you do not use VDI, if many clients install the same updates at the same time, this can negatively increase CPU usage on the site server. It can also slow down distribution points and significantly reduce the available network bandwidth.  

     If required software updates must be installed without delay when the configured deadline is reached, choose **Yes** for this setting.  

-   **Grace period for enforcement after deployment deadline (hours)**

	 In some cases, you might want to give users more time to install required application deployments or software updates beyond any deadlines you configured. This might typically be required when a computer has been turned off for an extended period of time and needs to install a large number of application or update deployments. For example, if a user has just returned from vacation, they might have to wait for a long while as overdue application deployments are installed. To help solve this problem, you can define an enforcement grace period by deploying Configuration Manager client settings to a collection.

     You can set a grace period of 1 to 120 hours. This setting is used in conjunction with the deployment property **Delay enforcement of this deployment according to user preferences**. For more details, see [Deploy applications](/sccm/apps/deploy-use/deploy-applications).

##  Computer restart  
 When you specify these computer restart settings, ensure that the value for the restart temporary notification interval and the value for the final countdown interval are shorter in duration than the shortest maintenance window that is applied to the computer.  

 For more information about maintenance windows, see [How to use maintenance windows in System Center Configuration Manager](../../../core/clients/manage/collections/use-maintenance-windows.md).  

##  Endpoint Protection  

-   **Manage Endpoint Protection client on client computers**  

     Choose **True** or **Yes** if you want to manage existing Endpoint Protection clients on computers in your hierarchy.  

     Choose this option if you have already installed the Endpoint Protection client and want to manage it with Configuration Manager.  

     Additionally, choose this option if you want to create a script to uninstall an existing antimalware solution, install the Endpoint Protection client, and deploy this script by using a Configuration Manager application or package and program.  

-   **Install Endpoint Protection client on client computers**  

     Choose **True** or **Yes** to install and enable the Endpoint Protection client on client computers where it is not already installed.  

    > [!NOTE]  
    >  If the Endpoint Protection client is already installed, choosing **False** or **No** will not uninstall the Endpoint Protection client. To uninstall the Endpoint Protection client, set the **Manage Endpoint Protection client on client computers** client setting to **False** or **No**. Then, deploy a package and program to uninstall the Endpoint Protection client.  

-   **For Windows Embedded devices with write filters, commit Endpoint Protection client installation (requires restart)**  

     Choose **Yes** to disable the write filter on the Windows Embedded device and restart the device. This commits the installation on the device.  

     If **No** is specified, the client is installed on a temporary overlay that is cleared when the device is restarted. In this scenario, the Endpoint Protection client is not committed until another installation commits changes to the device. This is the default setting.  

-   **Suppress any required computer restarts after the Endpoint Protection client is installed**  

     Choose **True** or **Yes** to suppress a computer restart if it is required after the Endpoint Protection client is installed.  

    > [!IMPORTANT]  
    >  If the Endpoint Protection client requires a computer restart and this setting is **False**, the restart will occur regardless of any maintenance windows that have been configured.  

-   **Allowed period of time users can postpone a required restart to complete the Endpoint Protection installation (hours)**  

     Specify the number of hours that users can postpone a computer restart if this is required after the Endpoint Protection client is installed. This option can be configured only if the **Suppress any required computer restarts after the Endpoint Protection client is installed** option is **False**.  

-   **Disable alternate sources (like Windows Update, Microsoft Windows Server Update Services, or UNC shares) for the initial definition update on client computers**  

     Choose **True** or **Yes** if you want Configuration Manager to install only the initial definition update on client computers. This setting can be helpful to avoid unnecessary network connections and reduce network bandwidth during the initial installation of the definition update.  

##  Hardware inventory  

-   **Maximum custom MIF file size (KB)**  

     Specify the maximum size, in kilobytes, allowed for each custom Management Information Format (MIF) file that will be collected from a client during a hardware inventory cycle. If any MIF files exceed this size, the Configuration Manager hardware inventory will not process them. You can specify a size of 1 to 5,000 KB. By default, this value is set to 250 KB. This setting does not affect the size of the regular hardware inventory data file.  

    > [!NOTE]  
    >  This setting is available only in the default client settings.  

-   **Hardware inventory classes**  

     In Configuration Manager, you can extend the hardware information that you collect from clients without manually editing the sms_def.mof file. Choose **Set Classes** if you want to extend Configuration Manager hardware inventory. For more information, see [How to configure hardware inventory in System Center Configuration Manager](../../../core/clients/manage/inventory/configure-hardware-inventory.md).  

-   **Collect MIF files**  

     Use this setting to specify whether to collect MIF files from Configuration Manager clients during hardware inventory.  

     For a MIF file to be collected by hardware inventory, it must in the correct location on the client computer. By default, the files are located as follows:  

    -   IDMIF files should be in the Windows\System32\CCM\Inventory\Idmif folder.  

    -   NOIDMIF files should be in the Windows\System32\CCM\Inventory\Noidmif folder.  

    > [!NOTE]  
    >  This setting is available only in the default client settings.

-   **Maximum random delay**

	The collection of hardware information is randomized by up to four hours so that the operation doesn't take place simultaneously on all clients. You can set the maximum delay in order to constrain the time during which the operation takes place.      

##  Metered Internet connections  
 You can manage how Windows 8 client computers communicate with Configuration Manager sites when they use metered Internet connections. Internet providers sometimes charge by the amount of data that you send and receive when you are on a metered Internet connection.  

> [!NOTE]  
>  The configured client setting is not applied to Windows 8 client computers in the following scenarios:  
>   
> -   The computer is on a roaming data connection: The Configuration Manager client does not perform any tasks that require data to be transferred to Configuration Manager sites.  
> -   The Windows network connection properties are configured as non-metered: The Configuration Manager client behaves as if this is a non-metered Internet connection and so transfers data to the Configuration Manager sites.  

-   **Client communication on metered Internet connections**  

     From the drop-down list, choose one of the following for Windows 8 client computers:  

    -   **Allow**: All client communications are allowed over the metered Internet connection unless the client device is using a roaming data connection.  

    -   **Limit**: Only the following client communications are allowed over the metered Internet connection:  

        -   Client policy retrieval  

        -   Client state messages to send to the site  

        -   Software installation requests by using the Application Catalog  

        -   Required deployments (when the installation deadline is reached)  

        > [!IMPORTANT]  
        >  If a user initiates a software installation from Software Center or the Application Catalog, these are always permitted, regardless of the metered Internet connection settings.  

         If the data transfer limit is reached for the metered Internet connection, the client no longer tries to communicate with Configuration Manager sites.  

    -   **Block**: The Configuration Manager client does not try to communicate with Configuration Manager sites when it is on a metered Internet connection. This is the default value.  

##  Power management  

-   **Allow users to exclude their device from power management**  

     From the drop-down list, choose **True** or **Yes** to let users of Software Center exclude their computer from any configured power management settings.  

-   **Enable wake-up proxy**  

     Specify **Yes** to supplement the site’s Wake On LAN setting when it is configured for unicast packets.  

     For more information about wake-up proxy, see [Plan how to wake up clients in System Center Configuration Manager](../../../core/clients/deploy/plan/plan-wake-up-clients.md).  

    > [!WARNING]  
    >  Do not enable wake-up proxy in a production network without first understanding how it works and evaluating it in a test environment.  

-   **Wake-up proxy port number (UDP)**  

     Keep the default value for the port number that managed computers use to send wake-up packets to sleeping computers. Or, change the number to a value of your choice.  

     The port number specified here is automatically configured for clients that run Windows Firewall when you use the **Windows Firewall exception for wake-up proxy** option. If clients run a different firewall, you must manually configure it to allow the UDP port number that is specified for this setting.  

-   **Wake On LAN port number (UDP)**  

     Keep the default value of 9, unless you have changed the Wake On LAN (UDP) port number on the **Ports** tab of the site **Properties**.  

    > [!IMPORTANT]  
    >  This number must match the number in the site **Properties**. If you change this number in one place, it isn't automatically updated in the other place.  

##  Remote tools  

-   **Enable Remote Control on clients** and **Firewall exception profiles**  

     Choose whether Configuration Manager remote control is enabled for all client computers that receive these client settings. Choose **Configure** to enable remote control. Optionally, configure firewall settings to allow remote control to work on client computers.  

     Remote control is disabled by default.  

    > [!IMPORTANT]  
    >  If firewall settings are not configured, remote control might not work correctly.  

-   **Users can change policy or notification settings in Software Center**  

     Choose whether users can change remote control options from within Software Center.  

-   **Allow Remote Control of an unattended computer**  

     Choose whether an admin can use remote control to access a client computer that is logged off or locked. Only a logged-on and unlocked computer can be remotely controlled when this setting is disabled.  

-   **Prompt user for Remote Control permission**  

     Choose whether the client computer will show a message that asks for the user's permission before allowing a remote control session.  

-   **Grant Remote Control permission to local Administrators group**  

     Choose whether local admins on the server that initiates the remote control connection can establish remote control sessions to client computers.  

-   **Access level allowed**  

     Specify the level of remote control access that will be allowed. You can choose from:  

    -   Full control  

    -   View only  

    -   None  

-   **Permitted viewers**  

     Choose **Set Viewers** to open the **Configure Client Setting** dialog box and specify the names of the Windows users who can establish remote control sessions to client computers.  

-   **Show session notification icon on taskbar**  

     Choose this option to show an icon on the taskbar of client computers to indicate that a remote control session is active.  

-   **Show session connection bar**  

     Choose this option to show a high-visibility session connection bar on client computers to indicate that a remote control session is active.  

-   **Play a sound on client**  

     Choose this option to use sound to indicate when a remote control session is active on a client computer. You can play a sound when the session connects or disconnects, or you can play a sound repeatedly during the session.  

-   **Manage unsolicited Remote Assistance settings**  

     Choose this option to let Configuration Manager manage unsolicited remote assistance sessions.  

     In an unsolicited remote assistance session, the user at the client computer did not request assistance to initiate the session.  

-   **Manage solicited Remote Assistance settings**  

     Choose this option to let Configuration Manager manage solicited remote assistance sessions.  

     In a solicited remote assistance session, the user at the client computer sent a request to the admin for remote assistance.  

-   **Level of access for Remote Assistance**  

     Choose the level of access to assign to remote assistance sessions that are initiated in the Configuration Manager console.  

    > [!NOTE]  
    >  The user at the client computer must always grant permission for a Remote Assistance session to occur.  

-   **Manage Remote Desktop settings**  

     Choose this option to let Configuration Manager manage Remote Desktop sessions for computers.  

-   **Allow permitted viewers to connect by using Remote Desktop connection**  

     Choose this option to let users specified in the permitted viewer list to be added to the Remote Desktop local user group on client computers.  

-   **Require network level authentication on computers that run Windows Vista operating system and later versions**  

     Choose this more secure option if you want to use network-level authentication to establish Remote Desktop connections to client computers that run Windows Vista or later. Network-level authentication requires fewer remote computer resources initially because it finishes user authentication before it establishes a Remote Desktop connection. This method is more secure because it can help protect the computer from malicious users or software, and it reduces the risk from denial-of-service attacks.  

## Software deployment  

-   **Schedule re-evaluation for deployments**  

     Configure a schedule for when Configuration Manager re-evaluates the requirement rules for all deployments. The default value is every 7 days.  

    > [!IMPORTANT]  
    >  We recommend that you do not change this value to a lower value than the default. Doing that might negatively affect the performance of your network and client computers.  

     You can also initiate this action from a Configuration Manager client computer by choosing the action **Application Deployment Evaluation Cycle** from the **Actions** tab of **Configuration Manager** in Control Panel.  

##  Software inventory  

-   **Inventory reporting detail**  

     Specify the level of file information to inventory. You can inventory details about the file, details about the product associated with the file, or all information about the file.  

-   **Inventory these file types**  

     If you want to specify the types of file to inventory, choose **Set Types** and then configure the following in the **Configure Client Setting** dialog box:  

    > [!NOTE]  
    >  If multiple custom client settings are applied to a computer, the inventory that each setting returns will be merged.  

    -   Choose the **New** icon to add a new file type to inventory. Then, specify the following information in the **Inventoried File Properties** dialog box:  

        -   **Name**: Provide a name for the file that you want to inventory. You can use the **\** character to represent any string of text and the **?** character to represent any single character. For example, if you want to inventory all files with the extension .doc, specify the file name **\*.doc**.  

        -   **Location**: Choose **Set** to open the **Path Properties** dialog box. You can configure software inventory to search all client hard disks for the specified file, search a specified path (for example, **C:\Folder**), or search for a specified variable (for example, *%windir%*). You can also search all subfolders under the specified path.  

        -   **Exclude encrypted and compressed files**: When you choose this option, any files that have been compressed or encrypted will not be inventoried.  

        -   **Exclude files in the Windows folder**: When you choose this option, any files in the Windows folder and its subfolders will not be inventoried.  

    -   Choose **OK** to close the **Inventoried File Properties** dialog box.  

    -   Add all the files that you want to inventory, and then choose **OK** to close the **Configure Client Setting** dialog box.  

-   **Collect files**  

     If you want to collect files from client computers, choose **Set Files** and then configure the following:  

    > [!NOTE]  
    >  If multiple custom client settings are applied to a computer, the inventory that each setting returns will be merged.  

    -   In the **Configure Client Setting** dialog box, choose the **New** icon to add a file to be collected.  

    -   In the **Collected File Properties** dialog box, provide the following information:  

        -   **Name**: Provide a name for the file that you want to collect. You can use the **\** character to represent any string of text and the **?** character to represent any single character.  

        -   **Location**: Choose **Set** to open the **Path Properties** dialog box. You can configure software inventory to search all client hard disks for the file that you want to collect, search a specified path (for example, **C:\Folder**), or search for a specified variable (for example, *%windir%*). You can also search all subfolders under the specified path.  

        -   **Exclude encrypted and compressed files**: When you choose this option, any files that have been compressed or encrypted will not be collected.  

        -   **Stop file collection when the total size of the files exceeds (KB)**: Specify the file size (in kilobytes) after which no more of the files specified under **Name** will be collected.  

          > [!NOTE]  
          >  The site server collects the five most recently changed versions of collected files and stores them in the *&lt;ConfigMgr installation directory\>*\Inboxes\Sinv.box\Filecol directory. If a file has not changed since the last software inventory was collected, the file will not be collected again.  
          >   
          >  Software inventory does not collect files larger than 20 MB.  
          >   
          >  The value **Maximum size for all collected files (KB)** in the **Configure Client Setting** dialog box shows the maximum size for all collected files. When this size is reached, file collection will stop. Any files already collected are retained and sent to the site server.  

          > [!IMPORTANT]
          >  If you configure software inventory to collect many large files, this might negatively affect the performance of your network and site server.  

        For information about how to view collected files, see [How to use Resource Explorer to view software inventory in System Center Configuration Manager](../../../core/clients/manage/inventory/use-resource-explorer-to-view-software-inventory.md).  

    -   Choose **OK** to close the **Collected File Properties** dialog box.  

    -   Add all the files that you want to collect, and then choose **OK** to close the **Configure Client Setting** dialog box.  

-   **Set Names**  

     During software inventory, manufacturer names and product names are retrieved from the header information of files installed on clients in the site. Because these names are not always standardized in the file header information, when you view software inventory information in Resource Explorer or run queries, different versions of the same manufacturer or product name can sometimes appear. If you want to standardize these display names, choose **Set Names** and then configure the following in the **Configure Client Setting** dialog box:  

    -   **Name type**: Software inventory collects information about both manufacturers and products. From the drop-down list, choose whether you want to configure display names for a **Manufacturer** or a **Product**.  

    -   **Display name**: Specify the display name that you want to use in place of the names in the **Inventoried names** list. You can choose the **New** icon to specify a new display name.  

    -   **Inventoried names**: Choose the **New** icon to add a new inventoried name that will be replaced in software inventory by the name chosen in the **Display name** list. You can add multiple names that will be replaced.  

##  Software updates  

-   **Enable software updates on clients**  

     Use this setting to enable software updates on Configuration Manager clients. When you disable this setting, Configuration Manager removes existing deployment policies from client. When you re-enable this setting, the client downloads the current deployment policy.  

    > [!IMPORTANT]  
    >  When you disable this setting, NAP and compliance settings policies that rely on the device setting for software updates will no longer function.  

-   **Software update scan schedule**  

     Use this setting to specify how often the client initiates a software update compliance assessment scan. The compliance assessment scan determines the state for software updates on the client (for example, required or installed). For more information about compliance assessment, see [Software updates compliance assessment](../../../sum/understand/software-updates-introduction.md#BKMK_SUMCompliance).  

     By default, a simple schedule is used and the compliance scan is initiated every 7 days. You can choose to create a custom schedule to specify an exact start day and time, choose whether to use UTC or the local time, and configure the recurring interval for a specific day of the week.  

    > [!NOTE]  
    >  If you specify an interval of less than 1 day, Configuration Manager will automatically default to 1 day.  

    > [!WARNING]  
    >  The actual start time on client computers is the start time plus a random amount of time up to 2 hours. This prevents client computers from initiating the scan and connecting to Windows Server Update Services (WSUS) on the active software update point server at the same time.  

-   **Schedule deployment re-evaluation**  

     Use this setting to configure how often the Software Updates Client Agent re-evaluates software updates for installation status on Configuration Manager client computers. When software updates that were previously installed are no longer found on client computers and are still required, they are reinstalled.

     The deployment re-evaluation schedule should be adjusted based on company policy for software update compliance, whether users have the ability to uninstall software updates, and so on. Remember that every deployment re-evaluation cycle results in some network and client computer CPU activity. By default, a simple schedule is used and the deployment re-evaluation scan is initiated every 7 days.  

    > [!NOTE]  
    >  If you specify an interval of less than 1 day, Configuration Manager will automatically default to 1 day.  

-   **When any software update deadline is reached, install all other software update deployments with deadline coming within a specified period of time**  

     Use this setting to install all software updates in required deployments that have deadlines that will occur within a specified period of time. When a deadline is reached for a required software update deployment, installation is initiated on clients for the software updates in the deployment. This setting determines whether to also initiate the installation for software updates defined in other required deployments that have a configured deadline within the specified period of time.  

     Use this setting to expedite software update installation for required software updates, potentially increase security, potentially decrease display notifications, and potentially decrease system restarts on client computers. By default, this setting is not enabled.  

-   **Period of time for which all pending deployments with deadline in this time will also be installed**  

     Use this setting to specify the timeframe for the previous setting. You can enter a value from 1 to 23 hours and from 1 to 365 days. By default, this setting is configured for 7 days.  

-   **Enable installation of Express installation files on clients**

-   **Port used to download content for Express installation files**

-   **Enable management of the Office 365 Client Again**
    Use this setting to enable the management of the Office 365 Client Agent. When you set the value to **Yes**, it allows you to configure Office 365 installation settings, download files from Office Content Delivery Networks (CDNs), and deploy the files as an application in Configuration Manager.

##  User and device affinity  

-   **User device affinity usage threshold (minutes)**  

     Specify the number of minutes before Configuration Manager creates a user device affinity mapping.  

-   **User device affinity usage threshold (days)**  

     Specify the number of days over which the usage-based affinity threshold is measured.  

    > [!NOTE]  
    >  For example, if **User device affinity usage threshold (minutes)** is specified as **60** minutes and **User device affinity usage threshold (days)** is specified as **5** days, the user must use the device for 60 minutes over a period of 5 days to automatically create a user device affinity.  

-   **Automatically configure user device affinity from usage data**  

     Choose **True** or **Yes** to let Configuration Manager automatically create user device affinities based on the usage information that is collected.  

##  Mobile devices  

-   **Mobile device enrollment profile**  

     Before you can configure this setting, you must first set to **True** the mobile device user setting **Allow users to enroll mobile devices**. Then you can choose **Set Profile** to specify an enrollment profile that has information about the certificate template to use during the enrollment process, the site that has an enrollment point and enrollment proxy point, and the site that will manage the device after the enrollment.  

    > [!IMPORTANT]  
    >  Ensure that you have configured a certificate template to use for mobile device enrollment before you configure this option.  

##  Enrollment  

-   **Mobile device enrollment profile**  

     Before you can configure this setting, you must first set to **Yes** the enrollment user setting **Allow users to enroll mobile devices and Mac computers**. Then you can choose **Set Profile** to specify an enrollment profile that has information about the certificate template to use during the enrollment process, the site that has an enrollment point and enrollment proxy point, and the site that will manage the device after the enrollment.  

    > [!IMPORTANT]  
    >  Ensure that you have configured a certificate template to use for mobile device enrollment or for Mac client certificate enrollment before you configure this option.  

## User and device affinity  

-   **Allow user to define their primary devices**  

     Specify whether users are allowed to identify their own primary devices on the **My Devices** tab of the Application Catalog.  
