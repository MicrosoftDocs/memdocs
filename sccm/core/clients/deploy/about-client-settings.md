---
title: "Client settings | Microsoft Docs"
description: "Select client settings by using the admin console in System Center Configuration Manager."
ms.custom: na
ms.date: 11/18/2016
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
author: Mtillmanms.author: mtillmanmanager: angrobe
---
# About client settings in System Center Configuration Manager*Applies to: System Center Configuration Manager (Current Branch)*
All client settings in System Center Configuration Manager are managed in the Configuration Manager console from the **Client Settings** node in the **Administration** workspace. A set of default settings is supplied with Configuration Manager. When you modify the default client settings, these settings are applied to all clients in the hierarchy. You can also configure custom client settings, which override the default client settings when you assign these to collections. For information about how to configure client settings, see [How to configure client settings in System Center Configuration Manager](../../../core/clients/deploy/configure-client-settings.md).  

 Many of the client settings are self-explanatory. Use the following sections for more information about the client settings that might require some information before you configure them.  

## Background Intelligent Transfer  

-   **Limit the maximum network bandwidth for BITS background transfers**  

   If this option is configured as **True** or **Yes**, BITS bandwidth throttling will be used by Configuration Manager clients.  

-   **Throttling window start time**  

   Specify the start time in local time that the BITS throttling window will begin.  

-   **Throttling window end time**  

   Specify the end time in local time that the BITS throttling window will end. If this value is the same as the **Throttling window start time**, BITS throttling is always enabled.  

-   **Maximum transfer rate during throttling window (Kbps)**  

   Specify the maximum transfer rate in (Kbps) that can be used by Configuration Manager clients during the specified BITS throttling window.  

-   **Allow BITS downloads outside the throttling window**  

   Select this option to allow BITS downloads outside of the throttling window. This option allows Configuration Manager clients to use separate BITS settings outside of the specified window.  

-   **Maximum transfer rate outside the throttling window (Kbps)**  

   Specify the maximum transfer rate in (Kbps) that will be used by Configuration Manager clients when outside of the specified BITS throttling window. This option can be configured only when you have selected to allow BITS throttling outside of the specified window.  

## Client Cache Settings

- **Configure BranchCache**

  Beginning in version 1606, specify to set up the client computer for BranchCache. To allow BranchCache caching to occur on the client, **Enable BranchCache** must be **Yes**. For understand more about BranchCache, see [Support for Windows features and network](/sccm/core/plan-design/configs/support-for-windows-features-and-networks#branchcache).

- **Enable BranchCache**

  Beginning in version 1606, specify to allow BranchCache caching to occur on the client computer.

- **Maximum BrancheCache cache size (percentage of disk)**

  Beginning in version 1606, specify the maximum size of the BranchCache cache in a percentage of disk size.

- **Configure client cache size**

  The client cache folder is used on Windows computers to store temporary files used to install applications and programs. Beginning in version 1606, select **Yes** to specify the size of the client cache folder using the **Maximum cache size** settings. If set to **No**, the client cache folder defaults to 5120 MB.

  Other client cache properties can be set during client installation. For more information, see [Configure the Client Cache for Configuration Manager Clients](../../../core/clients/manage/manage-clients.md#BKMK_ClientCache).

- **Maximum cache size (MB)**

Beginning in version 1606, specify the maximum size of the client cache folder in megabytes.

- **Maximum cache size (percentage of disk)** (beginning in version 1606)

Beginning in version 1606, specify the maximum size of the client cache folder in a percentage of disk size.

## Client Policy  

-   **Client policy polling interval (minutes)**  

   Specify how frequently the following Configuration Manager clients download client policy:  

  -   Windows computers (for example, desktops, servers, laptops)  

  -   Mobile devices that are enrolled by Configuration Manager  

  -   Mac computers  

  -   Computers that run Linux or UNIX  

-   **Enable user policy polling on clients**  

   When you configure this setting as **True** or **Yes**, and Configuration Manager has discovered the user, Configuration Manager clients on computers receive applications and programs that are targeted to the logged on user. For more information about how to discover users, see  [Active Directory User Discovery in Configuration Manager](../../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser).  

   Because the Application Catalog receives the list of available software for users from the site server, this setting does not have to be configured as **True** or **Yes** for users to see and request applications from the Application Catalog. However, if this setting is **False** or **No**, the following will not work when users use the Application Catalog:  

  -   Users cannot install the applications that they see in the Application Catalog.  

  -   Users will not see notifications about their application approval requests. Instead, they must refresh the Application Catalog and check the approval status.  

  -   Users will not receive revisions and updates for applications that are published to the Application Catalog. However, they will see changes to application information in the Application Catalog.  

  -   If you remove an application deployment after the client has installed the application from the Application Catalog, clients continue to check that the application is installed for up to 2 days.  

   In addition, when this setting is **False** or **No**, users will not receive required applications that you deploy to users or any other management operations that are contained in user policies.  

   This setting applies to users when their computer is on the intranet and the Internet; it must be configured as **True** or **Yes** if you also want to enable user policies on the Internet.  

-   **Enable user policy requests from Internet clients**  

   When the client and site is configured for Internet-based client management and you configure this option as **True** or **Yes** and both of the following conditions apply, users receive user policy when their computer is on the Internet:  

  -   The **Enable user policy polling on clients** client setting is configured as **True** or **Enable user policy on clients** is configured as **Yes**.  

  -   The Internet-based management point successfully authenticates the user by using Windows authentication (Kerberos or NTLM).  

   If you leave this option as **False** or **No**, or if either of the conditions fails, a computer on the Internet will receive computer policies only. In this scenario, users can still see, request, and install applications from an Internet-based Application Catalog. If this setting is **False** or **No** but the **Enable user policy polling on clients** is configured as **True** or **Enable user policy on clients** is configured as **Yes**, users will not receive user policies until the computer is connected to the intranet.  

   For more information about managing clients on the Internet, see  [Considerations for client communications from the Internet or an untrusted forest](../../../core/plan-design/hierarchy/communications-between-endpoints.md#BKMK_clientspan) in [Communications between endpoints in System Center Configuration Manager](../../../core/plan-design/hierarchy/communications-between-endpoints.md).  

  > [!NOTE]  
  >  Application approval requests from users do not require user policies or user authentication.  

##  Compliance Settings  

-   **Schedule compliance evaluation**  

     Click **Schedule** to create the default schedule that will be displayed to users when they deploy a configuration baseline. This value can be configured for each baseline in the **Deploy Configuration Baseline** dialog box.  

-   **Enable User Data and Profiles**  

     Select **Yes** if you want to deploy user data and profiles configuration items to Windows 8 computers in your hierarchy.  

     For more information about user data and profiles, see [How to create user data and profiles configuration items in System Center Configuration Manager](../../../compliance/deploy-use/create-user-data-and-profiles-configuration-items.md).  

## Computer Agent  

-   **Default Application Catalog website point**  

     Configuration Manager uses this setting to connect users to the Application Catalog from Software Center. You can specify a server that hosts the Application Catalog website point by its NetBIOS name or FQDN, specify automatic detection, or specify a URL for customized deployments. In most cases, automatic detection is the best choice because it offers the following benefits:  

    -   Clients are automatically given an Application Catalog website point from their site, if their site contains an Application Catalog website point.  

    -   Protection against a rogue server because Application Catalog website points on the intranet that are configured for HTTPS are given preference over Application Catalog website points that are not configured for HTTPS.  

    -   When clients are configured for intranet and Internet-based client management, they will be given an Internet-based Application Catalog website point when they are on the Internet and an intranet-based Application Catalog website point when they are on the intranet.  

     Automatic detection does not guarantee that clients will be given an Application Catalog website point that is closest to them. You might decide not to use **Automatically detect** for the following reasons:  

    -   You want to manually configure the closest server for clients or ensure that they do not connect to a server across a slow network connection.  

    -   You want to control which clients connect to which server. This might be for testing, performance, or business reasons.  

    -   You do not want to wait up to 25 hours or for a network change for clients to be configured with a different Application Catalog website point.  

     If you specify the Application Catalog website point rather than use automatic detection, specify the NetBIOS name rather than the intranet FQDN to help reduce the likelihood that users will be prompted for credentials when they connect to the Application Catalog on the intranet. To use the NetBIOS name, the following conditions must apply:  

    -   The NetBIOS name is specified in the Application Catalog website point properties.  

    -   You use WINS or all clients are in the same domain as the Application Catalog website point.  

    -   The Application Catalog website point is configured for HTTP client connections or it is configured for HTTPS client connections and the web server certificate contains the NetBIOS name.  

     Typically, users are prompted for credentials when the URL contains an FQDN but not when the URL is a NetBIOS name. Expect users to be always prompted when they connect from the Internet, because this connection must use the Internet FQDN. When users are prompted for credentials when they are on the Internet, ensure that the server that runs the Application Catalog website point can connect to a domain controller for the user’s account so that the user can be authenticated by using Kerberos.  

    > [!NOTE]  
    >  How automatic detection works:  
    >   
    >  The client makes a service location request to a management point. If there is an Application Catalog website point in the same site as the client, this server is given to the client as the Application Catalog server to use. When there is more than one available Application Catalog website point in the site, an HTTPS-enabled server takes precedence over a server that is not enabled for HTTPS. After this filtering, all clients are given one of the servers to use as the Application Catalog; Configuration Manager does not load-balance between multiple servers. When the client’s site does not contain an Application Catalog website point, the management point nondeterministically returns an Application Catalog website point from the hierarchy.  
    >   
    >  When the client is on the intranet, if the selected Application Catalog website point is configured with a NetBIOS name for the Application Catalog URL, clients are given this NetBIOS name instead of the intranet FQDN. When the client is detected to be on the Internet, only the Internet FQDN is given to the client.  
    >   
    >  The client makes this service location request every 25 hours or whenever it detects a network change. For example, if the client moves from the intranet to the Internet, and the client can locate an Internet-based management point, the Internet-based management point gives Internet-based Application Catalog website point servers to clients.  

-   **Add default Application Catalog website to Internet Explorer trusted sites zone**  

     If this option is configured as **True** or **Yes**, the current default Application Catalog website URL is automatically added to the trusted sites zone in Internet Explorer on clients.  

     This setting ensures that the Internet Explorer setting for Protected Mode is not enabled. If Protected Mode is enabled, the Configuration Manager client might not be able to install applications from the Application Catalog. By default, the trusted sites zone also supports user logon for the Application Catalog, which requires Windows authentication.  

     If you leave this option as **False**, Configuration Manager clients might not be able to install applications from the Application Catalog unless these Internet Explorer settings are configured in another zone for the Application Catalog URL that clients use.  

    > [!NOTE]  
    >  Whenever Configuration Manager adds a default Application Catalog to the trusted sites zone, Configuration Manager removes a previous default Application Catalog URL that Configuration Manager added before it adds a new entry.  
    >   
    >  Configuration Manager cannot add the URL if it is already specified in one of the security zones. In this scenario, you must either remove the URL from the other zone, or manually configure the required Internet Explorer settings.  

-   **Allow Silverlight applications to run in elevated trust mode**  

     This setting must be configured as **Yes** if users run the Configuration Manager client and use the Application Catalog.  

     If you change this setting, it takes effect when users next load their browser or refresh their currently opened browser window.  

     For more information about this setting, see [Certificates for Microsoft Silverlight 5, and elevated trust mode required for the application catalog](../../../apps/plan-design/security-and-privacy-for-application-management.md#BKMK_CertificatesSilverlight5) in [Security and privacy for application management in System Center Configuration Manager](../../../apps/plan-design/security-and-privacy-for-application-management.md).  

-   **Organization Name displayed in Software Center**  

     Type the name that users see in Software Center. This branding information helps users to identify this application as a trusted source.  

-   **Use new Software Center**  

     If enabled, all client computers targeted by these client settings will use the new Software Center which displays user-available apps that would previously only be accessible in the Silverlight-dependent Application Catalog.  

     However, the Application Catalog website point and Application Catalog web service point site system roles are still required for user-available apps to appear in Software Center.  

     For more information, see [Plan for and configure application management in System Center Configuration Manager](../../../apps/plan-design/plan-for-and-configure-application-management.md).  

-   **Install Permissions**  

    > [!WARNING]  
    >  This setting applies to the Application Catalog and Software Center. This setting has no effect when users use the company portal.  

     Configure how users can initiate the installation of software, software updates, and task sequences:  

    -   **All Users**: Users logged on to a client computer with any permission except Guest can initiate the installation of software, software updates, and task sequences.  

    -   **Only Administrators**: Users logged on to a client computer must be a member of the local Administrators group to initiate the installation of software, software updates, and task sequences.  

    -   **Only Administrators and primary users**: Users logged on to a client computer must be a member of the local Administrators group or a primary user of the computer to initiate the installation of software, software updates, and task sequences.  

    -   **No Users**: No users logged on to a client computer can initiate the installation of software, software updates, and task sequences. Required deployments for the computer are always installed at the deadline and users cannot initiate the installation of software from the Application Catalog or Software Center.  

-   **Suspend BitLocker PIN entry on restart**  

     If the BitLocker PIN entry is configured on computers, this option can bypass the requirement to enter a PIN when the computer restarts after a software installation.  

    -   **Always**:Configuration Managertemporarily suspends the BitLocker requirement to enter a PIN on the next computer startup after it has installed software that requires a restart and initiated a restart of the computer. This setting applies only to computer restarts that are initiated byConfiguration Managerand does not suspend the requirement to enter the BitLocker PIN when the user restarts the computer. The BitLocker PIN entry requirement is resumed after Windows startup.  

    -   **Never**:Configuration Managerdoes not suspend the BitLocker requirement to enter a PIN on the next computer startup after it has installed software that requires a restart. In this scenario, the software installation cannot finish until the user enters the PIN to complete the standard startup process and load Windows.  

-   **Additional software manages the deployment of applications and software updates**  

     Enable this option only if one of the following conditions apply:  

    -   You use a vendor solution that requires this setting to be enabled.  

    -   You use the Configuration Manager software development kit (SDK) to manage client agent notifications and the installation of applications and software updates.  

    > [!WARNING]  
    >  If you select this option when neither of these conditions apply, software updates and required applications will not install on clients. This setting does not prevent users from installing applications from the Application Catalog, or prevent packages and programs, and task sequences from being installed on client computers.  

-   **PowerShell execution policy**  

     Configure how Configuration Manager clients can run Windows PowerShell scripts. These scripts are often used for detection in configuration items for compliance settings, but can also be sent in a deployment as a standard script.  

    -   **Bypass**: The Configuration Manager client bypasses the Windows PowerShell configuration on the client computer so that unsigned scripts can run.  

    -   **Restricted**: the Configuration Manager client uses the current Windows PowerShell configuration on the client computer, which determines whether unsigned scripts can run.  

    -   **All Signed**: The Configuration Manager client runs scripts only if they are signed by a trusted publisher. This restriction applies independently from the current Windows PowerShell configuration on the client computer.  

     This option requires at least Windows PowerShell version 2.0 and the default is **All Signed**.  

    > [!TIP]  
    >  If unsigned scripts fail to run because of this client setting, Configuration Manager reports this error in the following ways:  
    >   
    >  -   Error ID **0X87D00327** and the description of **Script is not signed** as a deployment status error in the **Monitoring** workspace of the Configuration Manager console.  
    > -   Error codes and descriptions of **0X87D00327** and **Script is not signed** or **0X87D00320** and **The script host has not been installed yet** with the error type of **Discovery Error** in reports, such as **Details of errors of configuration items in a configuration baseline for an asset**.  
    > -   The message **Script is not signed (Error: 87D00327; Source: CCM)** in the **DcmWmiProvider.log** file.  

-   **Disable deadline randomization**  

     This setting determines whether the client uses an activation delay of up to two hours to install required software updates when the deadline is reached. By default, the activation delay is disabled.  

     For virtual desktop infrastructure (VDI) scenarios, this delay can help to distribute the CPU processing and data transfer for a computer that has multiple virtual machines that run the Configuration Manager client. Even if you do not use VDI, if many clients install the same updates at the same time, this can negatively increase CPU usage on the site server, slow down distribution points, and significantly reduce the available network bandwidth.  

     If required software updates must install without delay when the configured deadline is reached, select **Yes** for this setting.  

-   **Grace period for enforcement after deployment deadline (hours)** 
	
	 In some cases, you might want to give users more time to install required application deployments or software updates beyond any deadlines you configured. This might typically be required when a computer has been turned off for an extended period of time and needs to install a large number of application or update deployments. For example, if an end user has just returned from vacation, they might have to wait for a long while as overdue application deployments are installed. To help solve this problem, you can define an enforcement grace period by deploying Configuration Manager client settings to a collection.
	You can set a grace period of between 1 and 120 hours. This setting is used in conjunction with the deployment property **Delay enforcement of this deployment according to user preferences**. For more details, see [Deploy applications](/sccm/apps/deploy-use/deploy-applications)

##  Computer Restart  
 When you specify these computer restart settings, ensure that the value for the restart temporary notification interval and the value for the final countdown interval are shorter in duration than the shortest maintenance window that is applied to the computer.  

 For more information about maintenance windows, see [How to use maintenance windows in System Center Configuration Manager](../../../core/clients/manage/collections/use-maintenance-windows.md).  

##  Endpoint Protection  

-   **Manage Endpoint Protection client on client computers**  

     Select **True** or **Yes** if you want to manage existing Endpoint Protection clients on computers in your hierarchy.  

     Select this option if you have already installed the Endpoint Protection client and want to manage it with Configuration Manager.  

     Additionally, select this option if you want to create a script to uninstall an existing antimalware solution, install the Endpoint Protection client, and deploy this script by using a Configuration Manager application or package and program.  

-   **Install Endpoint Protection client on client computers**  

     Select **True** or **Yes** to install and enable the Endpoint Protection client on client computers where it is not already installed.  

    > [!NOTE]  
    >  If the Endpoint Protection client is already installed, selecting **False** or **No** will not uninstall the Endpoint Protection client. To uninstall the Endpoint Protection client, set the **Manage Endpoint Protection client on client computers** client setting to **False** or **No**, and then deploy a package and program to uninstall the Endpoint Protection client.  

-   **For Windows Embedded devices with write filters, commit Endpoint Protection client installation (requires restart)**  

     Select **Yes** to disable the write filter on the Windows Embedded device and restart the device. This commits the installation on the device.  

     If **No** is specified, the client is installed on a temporary overlay that is cleared when the device is restarted. In this scenario, the Endpoint Protection client is not committed until another installation commits changes to the device. This is the default setting.  

-   **Suppress any required computer restarts after the Endpoint Protection client is installed**  

     Select **True** or **Yes** to suppress a computer restart if it is required after the Endpoint Protection client is installed.  

    > [!IMPORTANT]  
    >  If the Endpoint Protection client requires a computer restart and this setting is configured as **False**, the restart will occur regardless of any maintenance windows that have been configured.  

-   **Allowed period of time users can postpone a required restart to complete the Endpoint Protection installation (hours)**  

     Specify the number of hours that users can postpone a computer restart if this is required after the Endpoint Protection client is installed. This option can only be configured if the **Suppress any required computer restarts after the Endpoint Protection client is installed** option is set to **False**.  

-   **Disable alternate sources (such as Windows Update, Microsoft Windows Server Update Services or UNC shares) for the initial definition update on client computers**  

     Select **True** or **Yes** if you want Configuration Manager to only install the initial definition update on client computers. This setting can be helpful to avoid unnecessary network connections and reduce network bandwidth during the initial installation of the definition update.  

##  Hardware Inventory  

-   **Maximum custom MIF file size (KB)**  

     Specify the maximum size, in kilobyte (KB), allowed for each custom Management Information Format (MIF) file that will be collected from a client during a hardware inventory cycle. If any MIF files exceed this size, they will not be processed by Configuration Manager hardware inventory. You can specify a size between 1 and 5,000 KB. By default, this value is set to 250 KB. This setting does not affect the size of the regular hardware inventory data file.  

    > [!NOTE]  
    >  This setting is only available in the default client settings.  

-   **Hardware inventory classes**  

     In Configuration Manager, you can extend the hardware information that you collect from clients without manually editing the sms_def.mof file. Click **Set Classes** if you want to extend Configuration Manager hardware inventory. For more information, see [How to configure hardware inventory in System Center Configuration Manager](../../../core/clients/manage/inventory/configure-hardware-inventory.md).  

-   **Collect MIF files**  

     Use this setting to specify whether to collect Managed Information Format (MIF) files from Configuration Manager clients during hardware inventory.  

     For a MIF file to be collected by hardware inventory, it must be located in the correct location on the client computer. By default, the files should be located as follows:  

    -   IDMIF files should be located in the Windows\System32\CCM\Inventory\Idmif folder.  

    -   NOIDMIF files should be located in the Windows\System32\CCM\Inventory\Noidmif folder.  

    > [!NOTE]  
    >  This setting is only available in the default client settings.  

##  Metered Internet Connections  
 You can manage how Windows 8 client computers communicate with Configuration Manager sites when they use metered Internet connections. Internet providers sometimes charge by the amount of data that you send and receive when you are on a metered Internet connection.  

> [!NOTE]  
>  The configured client setting is not applied to Windows 8 client computers in the following scenarios:  
>   
>  -   The computer is on a roaming data connection: The Configuration Manager client does not perform any operations that require data to be transferred to Configuration Manager sites.  
> -   The Windows network connection properties is configured as non-metered: The Configuration Manager client behaves as if this is a non-metered Internet connection and so transfers data to the Configuration Manager sites.  

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

         If the data transfer limit is reached for the metered Internet connection, the client no longer attempts to communicate with Configuration Manager sites.  

    -   **Block**: The Configuration Manager client does not attempt to communicate with Configuration Manager sites when it is on a metered Internet connection. This is the default value.  

##  Power Management  

-   **Allow users to exclude their device from power management**  

     From the drop down list, select **True** or **Yes** to allow users of Software Center to exclude their computer from any configured power management settings.  

-   **Enable wake-up proxy**  

     Specify **Yes** to supplement the site’s Wake On LAN setting when it is configured for unicast packets.  

     For more information about wake-up proxy, see [Plan how to wake up clients in System Center Configuration Manager](../../../core/clients/deploy/plan/plan-wake-up-clients.md).  

    > [!WARNING]  
    >  Do not enable wake-up proxy in a production network without first understanding how it works and evaluating it in a test environment.  

-   **Wake-up proxy port number (UDP)**  

     Keep the default value for the port number that manager computers use to send wake-up packets to sleeping computers, or change the number to a value of your choice.  

     The port number specified here is automatically configured for clients that run Windows Firewall when you configure the **Windows Firewall exception for wake-up proxy** option. If clients run a different firewall, you must manually configure it to allow the UDP port number that is specified for this setting.  

-   **Wake On LAN port number (UDP)**  

     Keep the default value of 9, unless you have changed the Wake On LAN (UDP) port number in the site **Properties**, **Ports** tab.  

    > [!IMPORTANT]  
    >  This number must match the number in the site **Properties**. If you change this number in one place, it does not automatically update in the other place.  

##  Remote Tools  

-   **Enable Remote Control on clients** and **Firewall exception profiles**  

     Select whether Configuration Manager remote control is enabled for all client computers that receive these client settings. Click **Configure** to enable remote control and optionally configure firewall settings to allow remote control to work on client computers.  

     Remote control is disabled by default.  

    > [!IMPORTANT]  
    >  If firewall settings are not configured, remote control might not work correctly.  

-   **Users can change policy or notification settings in Software Center**  

     Select whether users can change remote control options from within Software Center.  

-   **Allow Remote Control of an unattended computer**  

     Select whether an administrator can use remote control to access a client computer that is logged off or locked. Only a logged-on and unlocked computer can be remote controlled when this setting is disabled.  

-   **Prompt user for Remote Control permission**  

     Select whether the client computer will display a message asking for the user's permission before allowing a remote control session.  

-   **Grant Remote Control permission to local Administrators group**  

     Select whether local administrators on the server initiating the remote control connection can establish remote control sessions to client computers.  

-   **Access level allowed**  

     Specify the level of remote control access that will be allowed. You can choose from:  

    -   Full control  

    -   View only  

    -   None  

-   **Permitted viewers**  

     Click **Set Viewers** to open the **Configure Client Setting** dialog box and specify the names of the Windows users who can establish remote control sessions to client computers.  

-   **Show session notification icon on taskbar**  

     Select this option to display an icon on the taskbar of client computers to indicate that a remote control session is active.  

-   **Show session connection bar**  

     Select this option to display a high-visibility session connection bar on client computers to indicate that a remote control session is active.  

-   **Play a sound on client**  

     Select this option to use sound to indicate when a remote control session is active on a client computer. You can play a sound when the session connects or disconnects, or you can play a sound repeatedly during the session.  

-   **Manage unsolicited Remote Assistance settings**  

     Select this option to let Configuration Manager manage unsolicited remote assistance sessions.  

     Unsolicited remote assistance sessions are those where the user at the client computer does not request assistance to initiate a session.  

-   **Manage solicited Remote Assistance settings**  

     Select this option to let Configuration Manager manage solicited remote assistance sessions.  

     Solicited remote assistance sessions are those where the user at the client computer sends a request to the administrator for remote assistance.  

-   **Level of access for Remote Assistance**  

     Select the level of access to assign to remote assistance sessions that are initiated in the Configuration Manager console.  

    > [!NOTE]  
    >  The user at the client computer must always grant permission for a Remote Assistance session to occur.  

-   **Manage Remote Desktop settings**  

     Select this option to let Configuration Manager manage Remote Desktop sessions for computers.  

-   **Allow permitted viewers to connect by using Remote Desktop connection**  

     Select this option to let users specified in the permitted viewer list to be added to the Remote Desktop local user group on client computers.  

-   **Require network level authentication on computers that run Windows Vista operating system and later versions**  

     Select this more secure option if you want to use network-level authentication to establish Remote Desktop connections to client computers that run Windows Vista or later. Network-level authentication requires fewer remote computer resources initially because it completes user authentication before it establishes a Remote Desktop connection. This method is more secure because it can help protect the computer from malicious users or software, and it reduces the risk from denial-of-service attacks.  

## Software Deployment  

-   **Schedule re-evaluation for deployments**  

     Configure a schedule for when Configuration Manager re-evaluates the requirement rules for all deployments. The default value is every 7 days.  

    > [!IMPORTANT]  
    >  We recommend that you do not change this value to a lower value than the default as this may negatively affect the performance of your network and client computers.  

     You can also initiate this action from a Configuration Manager client computer by selecting the action **Application Deployment Evaluation Cycle** from the **Actions** tab of **Configuration Manager** in Control Panel.  

##  Software Inventory  

-   **Inventory reporting detail**  

     Specify the level of file information to inventory. You can inventory details about the file only, details about the product associated with the file or you can inventory all information about the file.  

-   **Inventory these file types**  

     If you want to specify the types of file to inventory, click **Set Types** and then configure the following in the **Configure Client Setting** dialog box:  

    > [!NOTE]  
    >  If multiple custom client settings are applied to a computer, the inventory returned by each setting will be merged.  

    -   Click the New icon to add a new file type to inventory, then specify the following information in the **Inventoried File Properties** dialog box:  

    -   **Name** – Provide a name for the file you want to inventory. You can use the **\*** character to represent any string of text and the **?** character to represent any single character. For example, if you want to inventory all files with the extension .doc, specify the filename **\*.doc**.  

    -   **Location** – Click **Set** to open the **Path Properties** dialog box. You can configure software inventory to search all client hard disks for the specified file, search a specified path (for example **C:\Folder**) or a specified variable (for example *%windir%*) and you can also search all subfolders under the specified path.  

    -   **Exclude encrypted and compressed files** – When you select this option, any files that have been compressed or encrypted will not be inventoried.  

    -   **Exclude files in the Windows folder** – When you select this option, any files in the Windows folder and its subfolders will not be inventories.  

    -   Click **OK** to close the **Inventoried File Properties** dialog box.  

    -   Add all of the files you want to inventory and then, click **OK** to close the **Configure Client Setting** dialog box.  

-   **Collect files**  

     If you want to collect files from client computers, click **Set Files** and then configure the following:  

    > [!NOTE]  
    >  If multiple custom client settings are applied to a computer, the inventory returned by each setting will be merged.  

    -   In the **Configure Client Setting** dialog box, click the new icon to add a file to be collected.  

    -   In the **Collected File Properties** dialog box, provide the following information:  

    -   **Name** – Provide a name for the file you want to collect. You can use the **\*** character to represent any string of text and the **?** character to represent any single character.  

    -   **Location** – Click **Set** to open the **Path Properties** dialog box. You can configure software inventory to search all client hard disks for the file you want to collect, search a specified path (for example **C:\Folder**) or a specified variable (for example *%windir%*) and you can also search all subfolders under the specified path.  

    -   **Exclude encrypted and compressed files** – When you select this option, any files that have been compressed or encrypted will not be collected.  

    -   **Stop file collection when the total size of the files exceeds (KB)** – Specify the file size (in KB) after which no more of the files specified under **Name** will be collected.  

        > [!NOTE]  
        >  The site server collects the five most recently changed versions of collected files and stores them in the *&lt;ConfigMgr installation directory\>***\Inboxes\Sinv.box\Filecol** directory. If a file has not changed since the last software inventory was collected, the file will not be collected again.  
        >   
        >  Files larger than 20 MB are not collected by software inventory.  
        >   
        >  The value **Maximum size for all collected files (KB)** in the **Configure Client Setting** dialog box displays the maximum size for all collected files. When this size is reached, file collection will stop. Any files already collected are retained and sent to the site server.  

        > [!IMPORTANT]
        >  If you configure software inventory to collect many large files, this might negatively affect the performance of your network and site server.  

         For information about how to view collected files, see [How to use Resource Explorer to view software inventory in System Center Configuration Manager](../../../core/clients/manage/inventory/use-resource-explorer-to-view-software-inventory.md).  

    -   Click **OK** to close the **Collected File Properties** dialog box.  

    -   Add all of the files you want to collect and then, click **OK** to close the **Configure Client Setting** dialog box.  

-   **Set Names**  

     During software inventory, manufacturer names and product names are retrieved from the header information of files installed on clients in the site. Because these names are not always standardized in the file header information, when you view software inventory information in Resource Explorer or run queries, different versions of the same manufacturer or product name can sometimes appear. If you want to standardize these display names, click **Set Names** and then configure the following in the **Configure Client Setting** dialog box:  

    -   **Name type:** Software inventory collects information about both manufacturers and products. From the drop-down list, select whether you want to configure display names for a **Manufacturer** or a **Product**.  

    -   **Display name:** Specifies the display name you want to use in place of the names in the **Inventoried names** list. You can click the New icon to specify a new display name.  

    -   **Inventoried names:** - Click the New icon to add a new inventoried name which will be replaced in software inventory by the name selected in the **Display name** list. You can add multiple names that will be replaced.  

##  Software Updates  

-   **Enable software updates on clients**  

     Use this setting to enable software updates on Configuration Manager clients. If you clear this setting, Configuration Manager removes existing deployment policies from client. When you re-enable this setting, the client downloads the current deployment policy.  

    > [!IMPORTANT]  
    >  When you clear this setting, NAP and compliance settings policies that rely on the software updates device setting will no longer function.  

-   **Software update scan schedule**  

     Use this setting to specify how often the client initiates a software update compliance assessment scan. The compliance assessment scan determines the state for software updates on the client (for example, required or installed). For more information about compliance assessment, see [Software updates compliance assessment](../../../sum/understand/software-updates-introduction.md#BKMK_SUMCompliance).  

     By default a simple schedule is used and the compliance scan initiates every 7 days. You can choose to create a custom schedule to specify an exact start day and time, choose whether to use UTC or the local time, and configure the recurring interval for a specific day of the week.  

    > [!NOTE]  
    >  If you specify an interval of less than 1 day, Configuration Manager will automatically default to 1 day.  

    > [!WARNING]  
    >  The actual start time on client computers is the start time plus a random amount of time up to 2 hours. This prevents client computers from initiating the scan and connecting to Windows Server Update Services (WSUS) on the active software update point server at the same time.  

-   **Schedule deployment re-evaluation**  

     Use this setting to configure how often the Software Updates Client Agent re-evaluates software updates for installation status on Configuration Manager client computers. When software updates that have been previously installed are no longer found on client computers, and still required, they are reinstalled. The deployment re-evaluation schedule should be adjusted based on company policy for software update compliance, whether users have the ability to uninstall software updates, and so on, and with the consideration that every deployment re-evaluation cycle results in some network and client computer CPU activity. By default, a simple schedule is used and the deployment re-evaluation scan initiates every 7 days.  

    > [!NOTE]  
    >  If you specify an interval of less than 1 day, Configuration Manager will automatically default to 1 day.  

-   **When any software update deadline is reached, install all other software update deployments with deadline coming within a specified period of time**  

     Use this setting to install all software updates in required deployments that have deadlines that will occur within a specified period of time. When a deadline is reached for a required software update deployment, installation initiates on clients for the software updates in the deployment. This setting determines whether to also initiate the installation for software updates defined in other required deployments that have a configured deadline within the specified period of time.  

     Use this setting to expedite software update installation for required software updates, potentially increase security, potentially decrease display notifications, and potentially decrease system restarts on client computers. By default, this setting is not enabled.  

-   **Period of time for which all pending deployments with deadline in this time will also be installed**  

     Use this setting to specify the timeframe for the previous setting. You can enter a value from 1 to 23 hours and from 1 to 365 days. By default, this setting is configured for 7 days.  

##  User and Device Affinity  

-   **User device affinity usage threshold (minutes)**  

     Specify the number of minutes before Configuration Manager creates a user device affinity mapping.  

-   **User device affinity usage threshold (days)**  

     Specify the number of days over which the usage based affinity threshold is measured.  

    > [!NOTE]  
    >  For example, if **User device affinity usage threshold (minutes)** is specified as **60** minutes and **User device affinity usage threshold (days)** is specified at **5** days, the user must use the device for 60 minutes over a period of 5 days to automatically create a user device affinity.  

-   **Automatically configure user device affinity from usage data**  

     Select **True** or **Yes** to enable Configuration Manager to automatically create user device affinities based on the usage information that is collected.  

##  Mobile Devices  

-   **Mobile device enrollment profile**  

     Before you can configure this setting, you must first set to **True** the mobile device user setting **Allow users to enroll mobile devices**. Then you can click **Set Profile** to specify an enrollment profile that contains information about the certificate template to use during the enrollment process, the site that contains an enrollment point and enrollment proxy point, and the site that will manage the device after the enrollment.  

    > [!IMPORTANT]  
    >  Ensure that you have configured a certificate template to use for mobile device enrollment before you configure this option.  

##  Enrollment  

-   **Mobile device enrollment profile**  

     Before you can configure this setting, you must first set to **Yes** the enrollment user setting **Allow users to enroll mobile devices and Mac computers**. Then you can click **Set Profile** to specify an enrollment profile that contains information about the certificate template to use during the enrollment process, the site that contains an enrollment point and enrollment proxy point, and the site that will manage the device after the enrollment.  

    > [!IMPORTANT]  
    >  Ensure that you have configured a certificate template to use for mobile device enrollment or for Mac client certificate enrollment before you configure this option.  

## User and Device Affinity  

-   **Allow user to define their primary devices**  

     Specify whether users are allowed to identify their own primary devices from the Application Catalog, **My Devices** tab.  
