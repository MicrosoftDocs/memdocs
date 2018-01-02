---
title: "Client settings"
titleSuffix: "Configuration Manager"
description: "Choose client settings by using the admin console in System Center Configuration Manager."
ms.custom: na
ms.date: 12/29/2017
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
author: aczechowski
ms.author: aaroncz
manager: angrobe
---
# About client settings in System Center Configuration Manager

*Applies to: System Center Configuration Manager (current branch)*

Manage all client settings in the Configuration Manager console from the **Client Settings** node in the **Administration** workspace. Configuration Manager comes with a set of default settings. When you change the default client settings, these settings are applied to all clients in the hierarchy. You can also configure custom client settings, which override the default client settings when you assign these settings to collections. For more information, see [How to configure client settings](../../../core/clients/deploy/configure-client-settings.md).  
 

## Background Intelligent Transfer Service  

-   **Limit the maximum network bandwidth for BITS background transfers**   </br>
   When this option is **Yes**, clients use BITS bandwidth throttling. To configure the other settings in this group, you must enable this setting. 

-   **Throttling window start time**   </br>
   Specify the local start time for the BITS throttling window.  

-   **Throttling window end time**   </br>
   Specify the local end time for the BITS throttling window. If equal to **Throttling window start time**, BITS throttling is always enabled.  

-   **Maximum transfer rate during throttling window (Kbps)** </br>
    Specifies the maximum transfer rate that clients can use during the window.  

-   **Allow BITS downloads outside the throttling window**   </br>
   Allow clients to use separate BITS settings outside the specified window.  

-   **Maximum transfer rate outside the throttling window (Kbps)**   </br>
   Specify the maximum transfer rate that clients use outside the BITS throttling window.  



## Client cache settings

- **Configure BranchCache** </br>
  Use this setting to set up the client computer for [Windows BranchCache](/sccm/core/plan-design/configs/support-for-windows-features-and-networks#branchcache). To allow BranchCache caching on the client, set **Enable BranchCache** to **Yes**.

    - **Enable BranchCache** </br>
    Enables BranchCache on client computers.

    - **Maximum BranchCache cache size (percentage of disk)** </br>
    The percentage of the disk that you allow BranchCache to use. 

- **Configure client cache size** </br>
  The Configuration Manager client cache on Windows computers stores temporary files used to install applications and programs. If this option is **No**, the default size is 5,120 MB.</br>
    Choose **Yes**, then specify:
	- **Maximum cache size (MB)**
	- **Maximum cache size (percentage of disk)** </br>
    The client cache size expands to the maximum size in megabytes (MB) or the percentage of the disk, *whichever is less*. 

- **Enable Configuration Manager client in full OS to share content** </br>
    Enables [peer cache](/sccm/core/plan-design/hierarchy/client-peer-cache) for Configuration Manager clients. Choose **Yes**, then specify port information by which the client communicates with the peer computer. 
    - **Port for initial network broadcast** (default 8004)
    - **Port for content download from peer** (default 8003) </br>
    Configuration Manager automatically configures Windows Firewall rules to allow this traffic. If you use a different firewall, you must manually configure rules to allow this traffic.




## Client policy  

-   **Client policy polling interval (minutes)    Specifies how frequently the following Configuration Manager clients download client policy:  
      -   Windows computers (for example, desktops, servers, laptops)  
      -   Mobile devices that Configuration Manager enrolls  
      -   Mac computers  
      -   Computers that run Linux or UNIX  

-   **Enable user policy on clients**   </br>
   When you set this option to **Yes**, and use [user discovery](../../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser), then clients receive applications and programs targeted to the logged-on user.  

    The Application Catalog receives the list of available software for users from the site server. Thus this setting does not have to be **Yes** for users to see and request applications from the Application Catalog. If this setting is **No**, the following behaviors do not work when users use the Application Catalog:  

      -   Users cannot install the applications that they see in the Application Catalog.  

      -   Users do not see notifications about their application approval requests. Instead, they must refresh the Application Catalog and check the approval status.  

      -   Users do not receive revisions and updates for applications that are published to the Application Catalog. Users do see changes to application information in the Application Catalog.  

      -   If you remove an application deployment after the client installs the application from the Application Catalog, clients continue to check that the application is installed for up to two days.  

    In addition, when this setting is **No**, users do not receive required applications that you deploy to users. Users also do not receive any other management tasks in user policies.  

    This setting applies to users when their computer is on the intranet and the Internet. It must be **Yes** if you also want to enable user policies on the Internet.  

-   **Enable user policy requests from Internet clients**   </br>
   Configure this setting to **Yes** for users to receive the user policy on Internet-based computers. The following requirements must also apply:  

      -   The client and site are configured for Internet-based client management

      -   The **Enable user policy on clients** setting is **Yes**  

      -   The Internet-based management point successfully authenticates the user by using Windows authentication (Kerberos or NTLM)  

       If you set this option as **No**, or any of the previous requirements are not met, then a computer on the Internet only receives computer policies. In this scenario, users can still see, request, and install applications from an Internet-based Application Catalog. If this setting is **No**, but **Enable user policy on clients** is **Yes**, users do not receive user policies until the computer is connected to the intranet.  

       For more information about managing clients on the Internet, see [Considerations for client communications from the Internet or an untrusted forest](../../../core/plan-design/hierarchy/communications-between-endpoints.md#BKMK_clientspan).  

      > [!NOTE]  
      >  Application approval requests from users do not require user policies or user authentication.  


## Cloud Services

-   **Allow access to cloud distribution point** </br>
    Configure this setting to **Yes** for clients to obtain content from a cloud distribution point. This setting does not require the device to be Internet-based.

-    **Automatically register new Windows 10 domain joined devices with Azure Active Directory** </br> 
    When you configure Azure Active Directory to support hybrid join, then Configuration Manager configures Windows 10 devices for this functionality. For more information, see [How to configure hybrid Azure Active Directory joined devices](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup).

-   **Enable clients to use a cloud management gateway** </br>
    By default, all Internet-roaming clients use any available [cloud management gateway](/sccm/core/clients/manage/plan-cloud-management-gateway). An example of when to configure this setting to **No** is to scope usage of the service, such as during a pilot project or to save costs.



##  Compliance settings  

-   **Enable compliance evaluation on clients** </br>
    Configure this setting to **Yes** to configure the other settings in this group.
 
-   **Schedule compliance evaluation**   </br>
     Click **Schedule** to create the default schedule for configuration baseline deployments. This value is configurable for each baseline in the **Deploy Configuration Baseline** dialog box.  

-   **Enable User Data and Profiles**   </br>
     Choose **Yes** if you want to deploy [user data and profiles](../../../compliance/deploy-use/create-user-data-and-profiles-configuration-items.md) configuration items.



## Computer agent  
-   User notifications for required deployments </br>
    For more information about the following three settings, see [User notifications for required deployments](/sccm/apps/deploy-use/deploy-applications#user-notifications-for-required-deployments):
    -   **Deployment deadline greater than 24 hours, remind user every (hours)**
    -   **Deployment deadline less than 24 hours, remind user every (hours)**  </br>
    -   **Deployment deadline less than 1 hour, remind user every (minutes)**  </br>

-   **Default Application Catalog website point**   </br>
     Configuration Manager uses this setting to connect users to the Application Catalog from Software Center. Click **Set Website** to specify a server that hosts the Application Catalog website point. Enter its NetBIOS name or FQDN, specify automatic detection, or specify a URL for customized deployments. In most cases, automatic detection is the best choice because it offers the following benefits:  

    -   If the site has an Application Catalog website point, then clients are automatically given an Application Catalog website point from their site.  

    -   The client prefers HTTPS-enabled Application Catalog website points on the intranet over HTTP-only servers. This capability helps protect against a rogue server.

    -   The management point gives Internet-based clients an Internet-based Application Catalog website point. The management point gives intranet-based clients an intranet-based Application Catalog website point.  

     Automatic detection does not guarantee that clients are given the closest Application Catalog website point. You might decide not to use **Automatically detect** for the following reasons:  

     -   You want to manually configure the closest server for clients or ensure that they do not connect to a server across a slow network connection.  

     -   You want to control which clients connect to which server. This configuration might be for testing, performance, or business reasons.  

     -   You do not want to wait up to 25 hours or for a network change for clients to use a different Application Catalog website point.  

     If you specify the Application Catalog website point rather than use automatic detection, specify the NetBIOS name rather than the intranet FQDN. This configuration reduces the likelihood that the web browser prompts users for credentials when they access an intranet-based Application Catalog. To use the NetBIOS name, the following conditions must apply:  

     -   The NetBIOS name is specified in the Application Catalog website point properties.  

     -   You use WINS, or all clients are in the same domain as the Application Catalog website point.  

     -   You configure the Application Catalog website point for HTTP client connections, or configure the server for HTTPS and the web server certificate has the NetBIOS name.  

     Typically, users are prompted for credentials when the URL has an FQDN but not when the URL is a NetBIOS name. Expect users to be always prompted when they connect from the Internet, because this connection must use the Internet FQDN. When using an Internet-based client and the web browser prompts users for credentials, ensure that the Application Catalog website point can connect to a domain controller for the user’s account. This configuration allows the user to authenticate by using Kerberos.  

    > [!NOTE]  
    >  How automatic detection works:  
    >   
    >  The client makes a service location request to a management point. If there is an Application Catalog website point in the same site as the client, this server is given to the client as the Application Catalog server to use. When more than one Application Catalog website point is available in the site, an HTTPS-enabled server takes precedence over a server that is not enabled for HTTPS. After this filtering, all clients are given one of the servers to use as the Application Catalog; Configuration Manager does not load-balance between multiple servers. When the client’s site does not have an Application Catalog website point, the management point nondeterministically returns an Application Catalog website point from the hierarchy.  
    >   
    >  For intranet-based clients, if you configure the Application Catalog website point with a NetBIOS name for the Application Catalog URL, the management point gives clients this NetBIOS name instead of the intranet FQDN. For Internet-based clients, the management point only gives the Internet FQDN to the client.  
    >   
    >  The client makes this service location request every 25 hours or whenever it detects a network change. For example, if the client moves from the intranet to the Internet, and the client locates an Internet-based management point, the Internet-based management point gives Internet-based Application Catalog website point servers to clients.  

-   **Add default Application Catalog website to Internet Explorer trusted sites zone**   </br>
     If this option is **Yes**, the client automatically adds the current default Application Catalog website URL to the Internet Explorer trusted sites zone.  

     This setting ensures that the Internet Explorer setting for Protected Mode is not enabled. If Protected Mode is enabled, the Configuration Manager client might not be able to install applications from the Application Catalog. By default, the trusted sites zone also supports user logon for the Application Catalog, which requires Windows authentication.  

     If you leave this option as **No**, Configuration Manager clients might not be able to install applications from the Application Catalog. An alternative method is to configure these Internet Explorer settings in another zone for the Application Catalog URL that clients use.  

    > [!NOTE]  
    >  Whenever Configuration Manager adds a default Application Catalog to the trusted sites zone, Configuration Manager removes any previously added Application Catalog URL.  
    >   
    >  If the URL is already specified in one of the security zones, then Configuration Manager cannot add the URL. In this scenario, you must either remove the URL from the other zone or manually configure the required Internet Explorer settings.  

-   **Allow Silverlight applications to run in elevated trust mode**   </br>
     This setting must be **Yes** for users to use the Application Catalog .  

     If you change this setting, it takes effect when users next load their browser or refresh their currently opened browser window.  

     For more information about this setting, see [Certificates for Microsoft Silverlight 5, and elevated trust mode required for the application catalog](../../../apps/plan-design/security-and-privacy-for-application-management.md#BKMK_CertificatesSilverlight5).  

-   **Organization name displayed in Software Center**   </br>
     Type the name that users see in Software Center. This branding information helps users to identify this application as a trusted source.  

-   **Use new Software Center**   </br>
     If you configure this client setting to **Yes**, then all client computers use the new Software Center. Software Center shows user-available apps that were previously accessible only in the Application Catalog. The Application Catalog requires Silverlight, which is not a prerequisite for the new Software Center.   

     The Application Catalog website point and Application Catalog web service point site system roles are still required for user-available apps to appear in Software Center.  

     For more information, see [Plan for and configure application management](../../../apps/plan-design/plan-for-and-configure-application-management.md).  

-   **Enable communication with Health Attestation Service**  </br>
    Configure this setting to **Yes** for Windows 10 devices to use [Health attestation](/sccm/core/servers/manage/health-attestation). When you enable this setting, the following setting is also available for configuration.

    -   **Use on-premises Health Attestation Service** </br>
        Configure this setting to **Yes** for devices to use an on-premises service. Configure this setting to **No** for devices to use Microsoft's cloud-based service.  

-   **Install Permissions**   </br>
    > [!WARNING]  
    >  This setting applies to the Application Catalog and Software Center. This setting has no effect when users use the Company Portal.  

     Configure how users can initiate the installation of software, software updates, and task sequences:  

    -   **All Users**: Users with any permission except Guest  

    -   **Only Administrators**: Users must be a member of the local Administrators group  

    -   **Only Administrators and primary users**: Users must be a member of the local Administrators group, or a primary user of the computer  

    -   **No Users**: No users logged on to a client computer can initiate the installation of software, software updates, and task sequences. Required deployments for the computer always install at the deadline. Users cannot initiate the installation of software from the Application Catalog or Software Center.  

-   **Suspend BitLocker PIN entry on restart**  </br>
     If computers require BitLocker PIN entry, then this option bypasses the requirement to enter a PIN when the computer restarts after a software installation.  

    -   **Always**: Configuration Manager temporarily suspends BitLocker after it has installed software that requires a restart and initiated a restart of the computer. This setting applies only to a computer restart initiated by Configuration Manager. This setting does not suspend the requirement to enter the BitLocker PIN when the user restarts the computer. The BitLocker PIN entry requirement resumes after Windows startup.

    -   **Never**: Configuration Manager does not suspend BitLocker on the next computer startup after it has installed software that requires a restart. In this scenario, the software installation cannot finish until the user enters the PIN to complete the standard startup process and load Windows.

-   **Additional software manages the deployment of applications and software updates**  </br>
     Enable this option only if one of the following conditions apply:  

    -   You use a vendor solution that requires this setting to be enabled.  

    -   You use the Configuration Manager software development kit (SDK) to manage client agent notifications and the installation of applications and software updates.  

    > [!WARNING]  
    >  If you choose this option when neither of these conditions apply, the client does not install software updates and required applications. This setting does not prevent users from installing applications from the Application Catalog, or the installation of packages, programs, and task sequences.  

-   **PowerShell execution policy**  </br>
     Configure how Configuration Manager clients can run Windows PowerShell scripts. These scripts are often used for detection in configuration items for compliance settings. They can also be sent in a deployment as a standard script.  

    -   **Bypass**: The Configuration Manager client bypasses the Windows PowerShell configuration on the client computer so that unsigned scripts can run.  

    -   **Restricted**: The Configuration Manager client uses the current Windows PowerShell configuration on the client computer. This configuration determines whether unsigned scripts can run.  

    -   **All Signed**: The Configuration Manager client runs scripts only if a trusted publisher has signed them. This restriction applies independently from the current Windows PowerShell configuration on the client computer.  

     This option requires at least Windows PowerShell version 2.0. The default is **All Signed**.  

    > [!TIP]  
    >  If unsigned scripts fail to run because of this client setting, Configuration Manager reports this error in the following ways:  
    >   
    > -   The **Monitoring** workspace in the console displays deployment status error ID **0x87D00327** and description **Script is not signed**  
    > -   Reports display error type **Discovery Error**, and then either error code **0x87D00327** and description **Script is not signed**, or error code **0x87D00320** and description **The script host has not been installed yet**. An example report is **Details of errors of configuration items in a configuration baseline for an asset**.  
    > -   The **DcmWmiProvider.log** file displays the message **Script is not signed (Error: 87D00327; Source: CCM)**.  

-   **Show notifications for new deployments**  </br>
     Choose **Yes** to display a notification for deployments available less than a week.  This message displays each time the client agent starts.

-   **Disable deadline randomization**  </br>
     After the deployment deadline, this setting determines whether the client uses an activation delay of up to two hours to install required software updates. By default, the activation delay is disabled.  

     For virtual desktop infrastructure (VDI) scenarios, this delay helps distribute the CPU processing and data transfer for a host machine with multiple virtual machines. Even if you do not use VDI, many clients installing the same updates at the same time can negatively increase CPU usage on the site server. This behavior can also slow down distribution points, and significantly reduce the available network bandwidth.  

     If clients must install required software updates at the deployment deadline without delay, then configure this setting to **Yes**. 

-   **Grace period for enforcement after deployment deadline (hours)** </br>
	 If you want to give users more time to install required application or software update deployments beyond the deadline, then configure this setting to **Yes**. This grace period is for a computer turned off for an extended time, and the user needs to install many application or update deployments. For example, if a user returns from vacation, and has to wait for a long time while the client installs overdue application deployments. 

     Set a grace period of 1 to 120 hours. Use this setting along with the deployment property **Delay enforcement of this deployment according to user preferences**. For more information, see [Deploy applications](/sccm/apps/deploy-use/deploy-applications).



##  Computer restart  
 The following settings must be shorter in duration than the shortest maintenance window applied to the computer.  

 For more information about maintenance windows, see [How to use maintenance windows in System Center Configuration Manager](../../../core/clients/manage/collections/use-maintenance-windows.md).  

-   **Display a temporary notification to the user that indicates the interval before the user is logged off or the computer restarts (minutes)**
-   **Display a dialog box that the user cannot close, which displays the countdown interval before the user is logged off or the computer restarts (minutes)**



##  Endpoint Protection  
>  [!Tip]   
> In addition to the following information, you can find additional details about using Endpoint Protection client settings in [Example scenario: Using System Center Endpoint Protection to protect computers from malware in System Center Configuration Manager](/sccm/protect/deploy-use/scenarios-endpoint-protection).

-   **Manage Endpoint Protection client on client computers**  </br>
     Choose **Yes** if you want to manage existing Endpoint Protection and Windows Defender clients on computers in your hierarchy.  

     Choose this option if you have already installed the Endpoint Protection client and want to manage it with Configuration Manager.  This separate installation includes a scripted process using a Configuration Manager application or package and program.

-   **Install Endpoint Protection client on client computers**   </br>
     Choose **Yes** to install and enable the Endpoint Protection client on client computers not already running the client.  

    > [!NOTE]  
    >  If the Endpoint Protection client is already installed, choosing **No** does not uninstall the Endpoint Protection client. To uninstall the Endpoint Protection client, set the **Manage Endpoint Protection client on client computers** client setting to **No**. Then, deploy a package and program to uninstall the Endpoint Protection client.  

-   **Automatically remove previously installed antimalware software before Endpoint Protection is installed** </br>
    Configure this setting to **Yes** for the Endpoint Protection client to attempt to uninstall other antimalware applications. Multiple antimalware clients on the same device can conflict and impact system performance.

-   **Allow Endpoint Protection client installation and restarts outside maintenance windows. Maintenance windows must be at least 30 minutes long for client installation** </br>
    Configure this setting to **Yes** to override typical installation behaviors with maintenance windows. This setting meets business requirements for the priority of system maintenance for security purposes. 

-   **For Windows Embedded devices with write filters, commit Endpoint Protection client installation (requires restarts)**  </br>
     Choose **Yes** to disable the write filter on the Windows Embedded device and restart the device. This action commits the installation on the device.  

     If you configure this setting to **No**, then the client installs on a temporary overlay that clears when the device restarts. In this scenario, the Endpoint Protection client does not fully install until another installation commits changes to the device. This configuration is the default.  

-   **Suppress any required computer restarts after the Endpoint Protection client is installed**  </br>
     Choose **Yes** to suppress a computer restart if necessary after the Endpoint Protection client installs.  

    > [!IMPORTANT]  
    >  If the Endpoint Protection client requires a computer restart and this setting is **No**, then the computer restarts regardless of any configured maintenance windows.  

-   **Allowed period of time users can postpone a required restart to complete the Endpoint Protection installation (hours)**  </br>
     If a restart is necessary after the Endpoint Protection client installs, this setting specifies the number of hours that users can postpone the required restart. This setting requires the **Suppress any required computer restarts after the Endpoint Protection client is installed** setting is **No**.  

-   **Disable alternate sources (such as Microsoft Windows Update, Microsoft Windows Server Update Services, or UNC shares) for the initial definition update on client computers**  </br>
     Choose **Yes** if you want Configuration Manager to install only the initial definition update on client computers. This setting can be helpful to avoid unnecessary network connections and reduce network bandwidth during the initial installation of the definition update.  



##  Enrollment

-   **Polling interval for mobile device legacy clients** </br>
    Click **Set Interval** to specify the length of time, in minutes or hours, that legacy mobile devices poll for policy. These devices include platforms such as Windows CE, Mac OS X, and Unix or Linux.

-   **Polling interval for modern devices (minutes)** </br>
    Enter the number of minutes that modern devices poll for policy. This setting is for Windows 10 devices managed via on-premises mobile device management.

-   **Allow users to enroll mobile devices and Mac computers** </br>
    To enable user-based enrollment of legacy devices, configure this setting to **Yes**, and then configure the following setting:

    -   **Enrollment profile** </br>
        Click **Set Profile** to create or select an enrollment profile. For more information, see [Configure client settings for enrollment](/sccm/core/clients/deploy/deploy-clients-to-macs#configure-client-settings-for-enrollment).

-   **Allow users to enroll modern devices** </br>
    To enable user-based enrollment of modern devices, configure this setting to **Yes**, and then configure the following setting:

    -   **Modern device enrollment profile** </br>
        Click **Set Profile** to create or select an enrollment profile. For more information, see [Create an enrollment profile that allows users to enroll modern devices](/sccm/mdm/get-started/set-up-device-enrollment-on-premises-mdm#bkmk_createProf).



##  Hardware inventory  

-   **Enable hardware inventory on clients** </br>
    This setting is set to **Yes** by default. For more information, see [Introduction to hardware inventory](/sccm/core/clients/manage/inventory/introduction-to-hardware-inventory).

-   **Hardware inventory schedule** </br>
    Click **Schedule** to adjust the frequency that clients run the hardware inventory cycle. By default, this cycle occurs every seven days.

-   **Maximum random delay (minutes)** </br>
    Specify the maximum number of minutes for the Configuration Manager client to randomize the hardware inventory cycle from the defined schedule. This randomization across all clients helps load balance inventory processing on the site server. You can specify a value of 0 to 480 minutes. By default, this value is set to 240 minutes (four hours).

-   **Maximum custom MIF file size (KB)**  </br>
     Specify the maximum size, in kilobytes (KB), allowed for each custom Management Information Format (MIF) file that the client collects during a hardware inventory cycle. The Configuration Manager hardware inventory agent does not process any custom MIF files that exceed this size. You can specify a size of 1 KB to 5,120 KB. By default, this value is set to 250 KB. This setting does not affect the size of the regular hardware inventory data file.  

    > [!NOTE]  
    >  This setting is available only in the default client settings.  

-   **Hardware inventory classes**  </br>
     Click **Set Classes** to extend the hardware information that you collect from clients without manually editing the sms_def.mof file. For more information, see [How to configure hardware inventory](../../../core/clients/manage/inventory/configure-hardware-inventory.md).  

-   **Collect MIF files**  </br>
     Use this setting to specify whether to collect MIF files from Configuration Manager clients during hardware inventory.  

     For a MIF file to be collected by hardware inventory, it must be in the correct location on the client computer. By default, the files are located in the following paths:  

    -   **IDMIF files** should be in the Windows\System32\CCM\Inventory\Idmif folder 

    -   **NOIDMIF files** should be in the Windows\System32\CCM\Inventory\Noidmif folder

    > [!NOTE]  
    >  This setting is available only in the default client settings.

   

##  Metered Internet connections  
 Manage how Windows 8 and later computers use metered Internet connections to communicate with Configuration Manager. Internet providers sometimes charge by the amount of data that you send and receive when you are on a metered Internet connection.  

> [!NOTE]  
>  The configured client setting is not applied in the following scenarios:  
>   
> -   The computer is on a roaming data connection: The Configuration Manager client does not perform any tasks that require data to be transferred to Configuration Manager sites.  
> -   The Windows network connection properties are configured as non-metered: The Configuration Manager client behaves as if the connection is non-metered, and so transfers data to the site.  

-   **Client communication on metered Internet connections**  </br>
     Choose one of the following options for this setting:  

    -   **Allow**: All client communications are allowed over the metered Internet connection unless the client device is using a roaming data connection.  

    -   **Limit**: Only the following client communications are allowed over the metered Internet connection:  

        -   Client policy retrieval  

        -   Client state messages to send to the site  

        -   Software installation requests by using the Application Catalog  

        -   Required deployments (when the installation deadline is reached)  

        > [!IMPORTANT]  
        >  The client always permits software installations from Software Center or the Application Catalog, regardless of the metered Internet connection settings.  

         If the data transfer limit is reached for the metered Internet connection, the client no longer tries to communicate with Configuration Manager sites.  

    -   **Block**: The Configuration Manager client does not try to communicate with Configuration Manager sites when it is on a metered Internet connection. This option is the default.  



##  Power management  

-   **Allow power management of devices** </br>
    Configure this setting to **Yes** to enable power management on clients. For more information, see [Introduction to power management](/sccm/core/clients/manage/power/introduction-to-power-management).

-   **Allow users to exclude their device from power management**  </br>
     Choose **Yes** to let users of Software Center exclude their computer from any configured power management settings.  

-   **Enable wake-up proxy** </br> 
     Specify **Yes** to supplement the site’s Wake On LAN setting when it is configured for unicast packets.  

     For more information about wake-up proxy, see [Plan how to wake up clients in System Center Configuration Manager](../../../core/clients/deploy/plan/plan-wake-up-clients.md).  

    > [!WARNING]  
    >  Do not enable wake-up proxy in a production network without first understanding how it works and evaluating it in a test environment.  

    Then configure the following additional settings as needed:

    -   **Wake-up proxy port number (UDP)**  </br>
         The port number that clients use to send wake-up packets to sleeping computers. Keep the default port 25536, or change the number to a value of your choice.  

    -   **Wake On LAN port number (UDP)** </br> 
         Keep the default value of 9, unless you have changed the Wake On LAN (UDP) port number on the **Ports** tab of the site **Properties**.  

        > [!IMPORTANT]  
        >  This number must match the number in the site **Properties**. If you change this number in one place, it isn't automatically updated in the other place.  

    -   **Windows Defender Firewall exception for wake-up proxy** </br>
         The Configuration Manager client automatically configures the wake-up proxy port number on devices that run Windows Defender Firewall. Click **Configure** to specify the desired firewall profiles.

        If clients run a different firewall, you must manually configure it to allow the **Wake-up proxy port number (UDP)**.  
        
    -   **IPv6 prefixes if required for DirectAccess or other intervening network devices. Use a comma to specify multiple entries** </br>
        Enter the necessary IPv6 prefixes for wake-up proxy to function on your network.



##  Remote tools  

-   **Enable Remote Control on clients** and **Firewall exception profiles**  </br>
     Click **Configure** to enable the Configuration Manager remote control feature. Optionally, configure firewall settings to allow remote control to work on client computers.  

     Remote control is disabled by default.  

    > [!IMPORTANT]  
    >  If firewall settings are not configured, remote control might not work correctly.  

-   **Users can change policy or notification settings in Software Center**  </br>
     Choose whether users can change remote control options from within Software Center.  

-   **Allow Remote Control of an unattended computer**  </br>
     Choose whether an admin can use remote control to access a client computer that is logged off or locked. Only a logged-on and unlocked computer can be remotely controlled when this setting is disabled.  

-   **Prompt user for Remote Control permission**  </br>
     Choose whether the client computer shows a message asking for the user's permission before allowing a remote control session.  

-   **Prompt user for permission to transfer content from shared clipboard** </br>
    Allow your users the opportunity to accept or deny file transfers before transferring content from the shared clipboard in a remote control session. Users only need to grant permission once per session, and the viewer does not have the ability to give themselves permission to proceed with the file transfer.

-   **Grant Remote Control permission to local Administrators group**  </br>
     Choose whether local admins on the server that initiates the remote control connection can establish remote control sessions to client computers.  

-   **Access level allowed**  </br>
     Specify the level of remote control access to allow. Choose from the following settings:  
    - **No Access**
    - **View Only**
    - **Full Control**  

-   **Permitted viewers of Remote Control and Remote Assistance**  </br>
     Click **Set Viewers** to specify the names of the Windows users who can establish remote control sessions to client computers.  

-   **Show session notification icon on taskbar**  </br>
     Configure this setting to **Yes** to show an icon on the client's Windows taskbar to indicate an active remote control session.  

-   **Show session connection bar**  </br>
     Configure this setting to **Yes** to show a high-visibility session connection bar on clients to indicate an active remote control session.  

-   **Play a sound on client**  </br>
     Configure this setting to use sound to indicate when a remote control session is active on a client computer. Select one of the following options:
    - **No sound**
    - **Beginning and send of session** (default)
    - **Repeatedly during session**  

-   **Manage unsolicited Remote Assistance settings**  </br>
     Configure this setting to **Yes** to let Configuration Manager manage unsolicited Remote Assistance sessions.  

     In an unsolicited Remote Assistance session, the user at the client computer did not request assistance to initiate the session.  

-   **Manage solicited Remote Assistance settings**  </br>
     Configure this setting to **Yes** to let Configuration Manager manage solicited Remote Assistance sessions.  

     In a solicited Remote Assistance session, the user at the client computer sent a request to the admin for remote assistance.  

-   **Level of access for Remote Assistance**  </br>
     Choose the level of access to assign to Remote Assistance sessions that are initiated in the Configuration Manager console.  Select one of the following options:
    - **None** (default)
    - **Remote Viewing**
    - **Full Control**

    > [!NOTE]  
    >  The user at the client computer must always grant permission for a Remote Assistance session to occur.  

-   **Manage Remote Desktop settings**  </br>
     Configure this setting to **Yes** to let Configuration Manager manage Remote Desktop sessions for computers.  

-   **Allow permitted viewers to connect by using Remote Desktop connection**  </br>
     Configure this setting to **Yes** to add users specified in the permitted viewer list to the Remote Desktop local user group on clients.  

-   **Require network level authentication on computers that run Windows Vista operating system and later versions**  </br>
     Configure this setting to **Yes** to use network-level authentication (NLA) to establish Remote Desktop connections to client computers. NLA initially requires fewer remote computer resources because it finishes user authentication before it establishes a Remote Desktop connection. Using NLA is a more secure configuration. NLA helps protect the computer from malicious users or software, and it reduces the risk from denial-of-service attacks.  



## Software Center

-   **Select these new settings to specify company information** </br>
    Configure this setting to **Yes**, and then specify the following settings to brand Software Center for your organization:

    - **Company name** </br>
        Enter the organization name that users see in Software Center.
    - **Color scheme for Software Center** </br>
        Click **Select Color** to define primary color used by Software Center.
    - **Select a logo for Software Center** </br>
        Click **Browse** to select an image to display in Software Center. The logo must be a JPEG or PNG of 400 x 100 pixels with a maximum size of 750 KB.

-   Software Center tab visibility </br>
    Configure the additional settings in this group to **Yes** to make the following tabs visible in Software Center:
    - **Applications**
    - **Updates**
    - **Operating Systems**
    - **Installation Status**
    - **Device Compliance**
    - **Options**

    For example, if your organization does not use compliance policies and you want to hide the Device Compliance tab in Software Center, configure the **Enable Device Compliance tab** setting to **No**.



## Software deployment  

-   **Schedule re-evaluation for deployments**  </br>
     Configure a schedule for when Configuration Manager re-evaluates the requirement rules for all deployments. The default value is every seven days.  

    > [!IMPORTANT]  
    >  We recommend that you do not change this value to a lower value than the default. A more aggressive re-evaluation schedule negatively affects the performance of your network and client computers.  

     Initiate this action from a client by choosing the **Application Deployment Evaluation Cycle** from the **Actions** tab of the **Configuration Manager** control panel.  



##  Software inventory  

-   **Enable software inventory on clients** </br>
    This setting is set to **Yes** by default. For more information, see [Introduction to software inventory](/sccm/core/clients/manage/inventory/introduction-to-software-inventory).

-   **Schedule software inventory and file collection** </br>
    Click **Schedule** to adjust the frequency that clients run the software inventory and file collection cycles. By default, this cycle occurs every seven days.

-   **Inventory reporting detail**  </br>
     Specify one of the following levels of file information to inventory:
    - **File only**
    - **Product only**
    - **Full details** (default)

-   **Inventory these file types**  </br>
     If you want to specify the types of file to inventory, click **Set Types**, and then configure the following options:  

    > [!NOTE]  
    >  If multiple custom client settings are applied to a computer, the inventory that each setting returns is merged.  

    -   Click the **New** icon to add a new file type to inventory. Then specify the following information in the **Inventoried File Properties** dialog box:  

        -   **Name**: Provide a name for the file that you want to inventory. Use an asterisk (**&#42;**) wildcard to represent any string of text and a question mark (**?**) to represent any single character. For example, if you want to inventory all files with the extension .doc, specify the file name **\*.doc**.  

        -   **Location**: Click **Set** to open the **Path Properties** dialog box. Configure software inventory to search all client hard disks for the specified file, search a specified path (for example, **C:\Folder**), or search for a specified variable (for example, *%windir%*). You can also search all subfolders under the specified path.  

        -   **Exclude encrypted and compressed files**: When you choose this option, any compressed or encrypted files are not inventoried.  

        -   **Exclude files in the Windows folder**: When you choose this option, any files in the Windows folder and its subfolders are not inventoried.  

    -   Click **OK** to close the **Inventoried File Properties** dialog box.  

    -   Add all the files that you want to inventory, and then click **OK** to close the **Configure Client Setting** dialog box.  

-   **Collect files**  </br>
     If you want to collect files from client computers, click **Set Files** and then configure the following settings:  

    > [!NOTE]  
    >  If multiple custom client settings are applied to a computer, the inventory that each setting returns is merged.  

    -   In the **Configure Client Setting** dialog box, click the **New** icon to add a file to be collected.  

    -   In the **Collected File Properties** dialog box, provide the following information:  

        -   **Name**: Provide a name for the file that you want to collect. Use an asterisk (**&#42;**) wildcard to represent any string of text and a question mark (**?**) to represent any single character.  

        -   **Location**: Click **Set** to open the **Path Properties** dialog box. Configure software inventory to search all client hard disks for the file that you want to collect, search a specified path (for example, **C:\Folder**), or search for a specified variable (for example, *%windir%*). You can also search all subfolders under the specified path.  

        -   **Exclude encrypted and compressed files**: When you choose this option, any compressed or encrypted files are not collected.  

        -   **Stop file collection when the total size of the files exceeds (KB)**: Specify the file size, in kilobytes (KB), after which the client stops collecting the specified files.  

          > [!NOTE]  
          >  The site server collects the five most recently changed versions of collected files and stores them in the *&lt;ConfigMgr installation directory\>*\Inboxes\Sinv.box\Filecol directory. If a file has not changed since the last software inventory cycle, the file is not collected again.  
          >   
          >  Software inventory does not collect files larger than 20 MB.  
          >   
          >  The value **Maximum size for all collected files (KB)** in the **Configure Client Setting** dialog box shows the maximum size for all collected files. When this size is reached, file collection stops. Any files already collected are retained and sent to the site server.  

          > [!IMPORTANT]
          >  If you configure software inventory to collect many large files, this configuration might negatively affect the performance of your network and site server.  

        For information about how to view collected files, see [How to use Resource Explorer to view software inventory](../../../core/clients/manage/inventory/use-resource-explorer-to-view-software-inventory.md).  

    -   Click **OK** to close the **Collected File Properties** dialog box.  

    -   Add all the files that you want to collect, and then click **OK** to close the **Configure Client Setting** dialog box.  

-   **Set Names**  </br>
     The software inventory agent retrieves manufacturer and product names from file header information. These names are not always standardized in the file header information. When you view software inventory in Resource Explorer, different versions of the same manufacturer or product name can appear. To standardize these display names, click **Set Names** and then configure the following settings:  

    -   **Name type**: Software inventory collects information about both manufacturers and products. Choose whether you want to configure display names for a **Manufacturer** or a **Product**.  

    -   **Display name**: Specify the display name that you want to use in place of the names in the **Inventoried names** list. Click the **New** icon to specify a new display name.  

    -   **Inventoried names**: Click the **New** icon to add an inventoried name. This name is replaced in software inventory by the name chosen in the **Display name** list. You can add multiple names to replace.  



##  Software Metering

-   **Enable software metering on clients** </br>
    This setting is set to **Yes** by default. For more information, see [Software metering](/sccm/apps/deploy-use/monitor-app-usage-with-software-metering#configure-software-metering).

-   **Schedule data collection** </br>
    Click **Schedule** to adjust the frequency that clients run the software metering cycle. By default, this cycle occurs every seven days.



##  Software updates  

-   **Enable software updates on clients**  </br>
     Use this setting to enable software updates on Configuration Manager clients. When you disable this setting, Configuration Manager removes existing deployment policies from client. When you re-enable this setting, the client downloads the current deployment policy.  

    > [!IMPORTANT]  
    >  When you disable this setting, compliance policies that rely on software updates will no longer function.  

-   **Software update scan schedule**  </br>
     Click **Schedule** to specify how often the client initiates a compliance assessment scan. This scan determines the state for software updates on the client (for example, required or installed). For more information about compliance assessment, see [Software updates compliance assessment](../../../sum/understand/software-updates-introduction.md#BKMK_SUMCompliance).  

     By default, this scan uses a simple schedule to initiate every seven days. You can create a custom schedule to specify an exact start day and time, use Universal Coordinated Time (UTC) or the local time, and configure the recurring interval for a specific day of the week.  

    > [!NOTE]  
    >  If you specify an interval of less than one day, Configuration Manager automatically defaults to one day.  

    > [!WARNING]  
    >  The actual start time on client computers is the start time plus a random amount of time up to two hours. This randomization prevents client computers from initiating the scan and simultaneously connecting to the active software update point.  

-   **Schedule deployment re-evaluation**  </br>
     Click **Schedule** to configure how often the software updates client agent re-evaluates software updates for installation status on Configuration Manager client computers. When previously installed software updates are no longer found on clients but are still required, the client reinstalls the software updates.

     Adjust this schedule based on company policy for software update compliance and whether users can uninstall software updates. Every deployment re-evaluation cycle results in network and client computer processor activity. By default, this setting uses a simple schedule to initiate the deployment re-evaluation scan every seven days.  

    > [!NOTE]  
    >  If you specify an interval of less than one day, Configuration Manager automatically defaults to one day.  

-   **When any software update deployment deadline is reached, install all other software update deployments with deadline coming within a specified period of time**  </br>
     Configure this setting to **Yes** to install all software updates from required deployments with deadlines occurring within a specified period of time. When a required software update deployment reaches a deadline, the client initiates installation for the software updates in the deployment. This setting determines whether to install software updates from other required deployments that have a deadline within the specified time.  

     Use this setting to expedite installation for required software updates. This setting also potentially increases client security, potentially decreases end-user notifications, and potentially decreases client restarts. By default, this setting is set to **No** thus not enabled.  

-   **Period of time for which all pending deployments with deadline in this time will also be installed**  </br>
     Use this setting to specify the period of time for the previous setting. You can enter a value from 1 to 23 hours and from 1 to 365 days. By default, this setting is configured for seven days.  

-   **Enable installation of Express installation files on clients** </br>
    Configure this setting to **Yes** to allow clients to use express installation files. For more information, see [Manage Express installation files for Windows 10 updates](/sccm/sum/deploy-use/manage-express-installation-files-for-windows-10-updates).

    -   **Port used to download content for Express installation files** </br>
        This setting configures the local port for the HTTP listener to download express content. It is set to 8005 by default. You do not need to open this port in the client firewall.

-   **Enable management of the Office 365 Client Agent** </br>
    Use this setting to enable the management of the Office 365 Client Agent. When you set the value to **Yes**, it enables the configuration of Office 365 installation settings, downloading files from Office Content Delivery Networks (CDNs), and deploying the files as an application in Configuration Manager. For more information, see [Manage Office 365 ProPlus](/sccm/sum/deploy-use/manage-office-365-proplus-updates).



## State Messaging

-   **State message reporting cycle (minutes)  Specifies how often clients report state messages. This setting is 15 minutes by default.



##  User and device affinity  

-   **User device affinity usage threshold (minutes)**  </br>
     Specify the number of minutes before Configuration Manager creates a user device affinity mapping.  By default this value is 2880 minutes (two days).

-   **User device affinity usage threshold (days)**  </br>
     Specify the number of days over which the client measures the threshold for usage-based device affinity.  By default this value is 30 days.

    > [!NOTE]  
    >  For example, you specify **User device affinity usage threshold (minutes)** as **60** minutes and **User device affinity usage threshold (days)** as **5** days. Then the user must use the device for 60 minutes over a period of five days to create automatic affinity with the device.  

-   **Automatically configure user device affinity from usage data**  </br>
     Choose **Yes** to create automatic user device affinity based on the usage information that Configuration Manager collects.  

-   **Allow user to define their primary devices** </br>
    When this setting is **Yes** then users can identify their own primary devices in Software Center.



## Windows Analytics

For more information on these settings, see [Configure Clients to report data to Windows Analytics](/sccm/core/clients/manage/monitor-windows-analytics#configure-clients-to-report-data-to-windows-analytics).
    