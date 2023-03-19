---
title: Client settings
titleSuffix: Configuration Manager
description: Learn about the default and custom settings for controlling client behaviors
ms.date: 03/28/2022
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: reference
author: baladelli
ms.author: baladell
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# About client settings in Configuration Manager

*Applies to: Configuration Manager (current branch)*

Manage all client settings in the Configuration Manager console from the **Client Settings** node in the **Administration** workspace. Configuration Manager comes with a set of default settings. When you change the default client settings, these settings are applied to all clients in the hierarchy. You can also configure custom client settings, which override the default client settings when you assign them to collections. For more information, see [How to configure client settings](configure-client-settings.md).

The following sections describe settings and options in further detail.

## Background Intelligent Transfer Service (BITS)  

### Limit the maximum network bandwidth for BITS background transfers

When this option is **Yes**, clients use BITS bandwidth throttling. To configure the other settings in this group, you must enable this setting.

### Throttling window start time

Specify the local start time for the BITS throttling window.  

### Throttling window end time

Specify the local end time for the BITS throttling window. If the end time is equal to the **Throttling window start time**, BITS throttling is always enabled.  

### Maximum transfer rate during throttling window (Kbps)

Specify the maximum transfer rate that clients can use during the window.  

### Allow BITS downloads outside the throttling window

Allow clients to use separate BITS settings outside the specified window.  

### Maximum transfer rate outside the throttling window (Kbps)

Specify the maximum transfer rate that clients can use outside the BITS throttling window.  



## Client cache settings

### Configure BranchCache

Set up the client computer for [Windows BranchCache](../../plan-design/configs/support-for-windows-features-and-networks.md#bkmk_branchcache
). To allow BranchCache caching on the client, set **Enable BranchCache** to **Yes**.

- **Enable BranchCache**: Enables BranchCache on client computers.

- **Maximum BranchCache cache size (percentage of disk)**: The percentage of the disk that you allow BranchCache to use.

> [!TIP]
> If you set **Configure BranchCache** to **No**, then Configuration Manager doesn't configure any BranchCache settings.
>
> To disable BranchCache, set **Configure BranchCache** to **Yes**, and then set **Enable BranchCache** to **No**.<!-- 6244852 -->

### Configure client cache size

The Configuration Manager client cache on Windows computers stores temporary files used to install applications and programs. If this option is set to **No**, the default size is 5,120 MB.

If you choose **Yes**, then specify:

- **Maximum cache size (MB)**
- **Maximum cache size (percentage of disk)**: The client cache size expands to the maximum size in megabytes (MB), or the percentage of the disk, whichever is less.

### Enable as peer cache source

Enables [peer cache](../../plan-design/hierarchy/client-peer-cache.md) for Configuration Manager clients. Choose **Yes**, and then specify the port through which the client communicates with the peer computer.

- **Port for initial network broadcast** (default UDP 8004): Configuration Manager uses this port in Windows PE or the full Windows OS. The task sequence engine in Windows PE sends the broadcast to get content locations before it starts the task sequence.<!--SCCMDocs issue 910-->

- **Port for content download from peer** (default TCP 8003): Configuration Manager automatically configures Windows Firewall rules to allow this traffic. If you use a different firewall, you must manually configure rules to allow this traffic.  

    For more information, see [Ports used for connections](../../plan-design/hierarchy/ports.md#BKMK_PortsClient-ClientWakeUp).  

### Minimum duration before cached content can be removed (minutes)

<!--4485509-->
Specify the minimum time for the Configuration Manager client to keep cached content. This client setting defines the minimum amount of time Configuration Manager agent should wait before it can remove content from the cache in case more space is needed.

By default this value is 1,440 minutes (24 hours).
The maximum value for this setting is 10,080 minutes (one week).

This setting gives you greater control over the client cache on different types of devices. You might reduce the value on clients that have small hard drives and don't need to keep existing content before another deployment runs.

## Client policy  

### Client policy polling interval (minutes)

Specifies how frequently the following Configuration Manager clients download client policy:

- Windows computers (for example, desktops, servers, laptops)  
- Mobile devices that Configuration Manager enrolls  
- Mac computers  

This value is 60 minutes by default. Reducing this value causes clients to poll the site more frequently. With many clients, this behavior can have a negative impact on the site performance. The [size and scale guidance](../../plan-design/configs/size-and-scale-numbers.md) is based on the default value. Increasing this value causes clients to poll the site less often. Any changes to client policies, including new deployments, take longer for clients to download and process.<!-- SCCMDocs issue 823 -->

### Enable user policy on clients

When you set this option to **Yes**, and use [user discovery](../../servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser), then clients receive applications and programs targeted to the signed-in user.

If this setting is **No**, users don't receive required applications that you deploy to users. Users also don't receive any other management tasks in user policies.

This setting applies to users when their computer is on either the intranet or the internet. It must be **Yes** if you also want to enable user policies on the internet.

### Enable user policy requests from internet clients

Set this option to **Yes** for users to receive the user policy on internet-based computers. The following requirements also apply:  

- The client and site are configured for [internet-based client management](../manage/plan-internet-based-client-management.md) or a [cloud management gateway](../manage/cmg/overview.md).  

- The **Enable user policy on clients** setting is **Yes**.  

- The internet-based management point successfully authenticates the user by using Windows authentication (Kerberos or NTLM). For more information, see [Considerations for client communications from the internet](../../plan-design/hierarchy/communications-between-endpoints.md#BKMK_clientspan).  

- The cloud management gateway successfully authenticates the user by using Azure Active Directory. For more information, see [Prerequisites to deploy user-available applications](../../../apps/plan-design/prerequisites-deploy-user-available-apps.md).

If you set this option to **No**, or any of the previous requirements aren't met, then a computer on the internet only receives computer policies. If this setting is **No**, but **Enable user policy on clients** is **Yes**, users don't receive user policies until the computer is connected to the intranet.  

> [!NOTE]  
> For internet-based client management, application approval requests from users don't require user policies or user authentication. The cloud management gateway doesn't support application approval requests.  

### Enable user policy for multiple user sessions

<!--4737447-->

By default, this setting is disabled. Even if you enable user policies, the client disables them by default on any device that allows multiple concurrent active user sessions. For example, terminal servers or Windows Enterprise multi-session in [Azure Virtual Desktop](../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md#azure-virtual-desktop).

The client only disables user policy when it detects this type of device during a new installation. For an existing client of this type that you update to a later client version, the previous behavior persists. On an existing device, it configures the user policy setting even if it detects that the device allows multiple user sessions.

If you require user policy in this scenario, and accept any potential performance impact, enable this client setting.


## Cloud services

### Allow access to cloud distribution point

Set this option to **Yes** for clients to obtain content from a content-enabled CMG. This setting doesn't require the device to be internet-based.

### Automatically register new Windows 10 or later domain joined devices with Azure Active Directory

When you configure Azure Active Directory (Azure AD) to support hybrid join, Configuration Manager configures Windows 10 or later devices for this functionality. For more information, see [How to configure hybrid Azure AD joined devices](/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup).

### Enable clients to use a cloud management gateway

By default, all internet-roaming clients use any available [cloud management gateway](../manage/cmg/overview.md). An example of when to configure this setting to **No** is to scope usage of the service, such as during a pilot project or to save costs.



## Compliance settings  

### Enable compliance evaluation on clients

Set this option to **Yes** to configure the other settings in this group.

### Schedule compliance evaluation

Select **Schedule** to create the default schedule for configuration baseline deployments. This value is configurable for each baseline in the **Deploy Configuration Baseline** dialog box.  

### Enable User Data and Profiles

Choose **Yes** if you want to deploy [user data and profiles](../../../compliance/deploy-use/create-user-data-and-profiles-configuration-items.md) configuration items.

## Script Execution Timeout (seconds)

Starting in version 2207, you can define a **Script Execution Timeout (seconds)**. The timeout value can be set from a minimum of 60 seconds to a maximum of 600 seconds. This new setting allows you more flexibility for configuration items when you need to run scripts that may exceed the default of 60 seconds. <!--14120481-->
## Computer agent  

### User notifications for required deployments

For more information about the following three settings, see [User notifications for required deployments](../../../apps/plan-design/user-notifications.md):

- **Deployment deadline greater than 24 hours, remind user every (hours)**
- **Deployment deadline less than 24 hours, remind user every (hours)**
- **Deployment deadline less than 1 hour, remind user every (minutes)**

### Legacy settings for the application catalog

The following client settings still appear in the Computer Agent group, but the functionality is no longer supported:

- Default Application Catalog website point
- Add default Application Catalog website to Internet Explorer trusted sites zone
- Allow Silverlight applications to run in elevated trust mode

For more information, see [Removed and deprecated features](../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md).

### Organization name displayed in Software Center

Type the name that users see in Software Center. This branding information helps users to identify this application as a trusted source. For more information about the priority of this setting, see [Branding Software Center](../../../apps/plan-design/plan-for-software-center.md#brand-software-center).  

### Use new Software Center

The default setting is **Yes**.

The previous version of Software Center and the application catalog are no longer supported.

### Enable communication with Health Attestation Service

Set this option to **Yes** for Windows 10 or later devices to use [Health attestation](../../servers/manage/health-attestation.md). When you enable this setting, the following setting is also available for configuration.

### Use on-premises Health Attestation Service

Set this option to **Yes** for devices to use an on-premises service. Set to **No** for devices to use the Microsoft cloud-based service.  

### Install permissions

Configure how users can install software, software updates, and task sequences:  

- **All Users**: Users with any permission except Guest.  

- **Only Administrators**: Users must be a member of the local Administrators group.  

- **Only Administrators and primary users**: Users must be a member of the local Administrators group, or a primary user of the computer.  

- **No Users**: No users signed in to a client computer can install software, software updates, and task sequences. Required deployments for the computer always install at the deadline. Users can't install software from Software Center.  

### Suspend BitLocker PIN entry on restart

If computers require BitLocker PIN entry, then this option bypasses the requirement to enter a PIN when the computer restarts after a software installation.  

- **Always**: Configuration Manager temporarily suspends BitLocker after it has installed software that requires a restart, and it restarts the computer. This setting only applies when Configuration Manager restarts the computer. This setting doesn't suspend the requirement to enter the BitLocker PIN when the user restarts the computer. The BitLocker PIN entry requirement resumes after Windows startup.

- **Never**: Configuration Manager doesn't suspend BitLocker after it has installed software that requires a restart. In this scenario, the software installation can't finish until the user enters the PIN to complete the standard startup process and load Windows.

### Additional software manages the deployment of applications and software updates

Enable this option only if one of the following conditions applies:  

- You use a vendor solution that requires this setting to be enabled.  

- You use the Configuration Manager software development kit (SDK) to manage client agent notifications, and the installation of applications and software updates.  

> [!WARNING]
> If you choose this option when neither of these conditions apply, the client doesn't install software updates and required applications. This setting doesn't prevent users from installing available software from Software Center, including applications, packages, and task sequences.
>
> When you enable this setting, toast notifications for new software or required software don't occur on clients. <!--6347668-->

### PowerShell execution policy

Configure how Configuration Manager clients can run Windows PowerShell scripts. You might use these scripts for detection in configuration items for compliance settings. You might also send the scripts in a deployment as a standard script.  

- **Bypass**: The Configuration Manager client bypasses the Windows PowerShell configuration on the client computer, so that unsigned scripts can run.  

- **Restricted**: The Configuration Manager client uses the current PowerShell configuration on the client computer. This configuration determines whether unsigned scripts can run.  

- **All Signed**: The Configuration Manager client runs scripts only if a trusted publisher has signed them. This restriction applies independently from the current PowerShell configuration on the client computer.  

This option requires at least Windows PowerShell version 2.0. The default is **All Signed**.  

> [!TIP]  
> If unsigned scripts fail to run because of this client setting, Configuration Manager reports this error in the following ways:  
>
> - The **Monitoring** workspace in the console displays deployment status error ID **0x87D00327**. It also displays the description **Script is not signed**.  
> - Reports display the error type **Discovery Error**. Then reports display either error code **0x87D00327** and the description **Script is not signed**, or error code **0x87D00320** and the description **The script host has not been installed yet**. An example report is: **Details of errors of configuration items in a configuration baseline for an asset**.  
> - The **DcmWmiProvider.log** file displays the message **Script is not signed (Error: 87D00327; Source: CCM)**.  

### Show notifications for new deployments

Choose **Yes** to display a notification for deployments available for less than a week. This message appears each time the client agent starts.

### Disable deadline randomization

After the deployment deadline, this setting determines whether the client uses an activation delay of up to two hours to install required software updates. By default, the activation delay is disabled. 

For virtual desktop infrastructure (VDI) scenarios, this delay helps distribute the CPU processing and data transfer for a host machine with multiple virtual machines. Even if you don't use VDI, having many clients installing the same updates at the same time can negatively increase CPU usage on the site server. This behavior can also slow down distribution points, and significantly reduce the available network bandwidth.  

If clients must install required software updates at the deployment deadline without delay, then configure this setting to **Yes**.

> [!IMPORTANT]
> Disabling randomization only applies to manual software update deployments. The setting doesn't apply to automatic deployment rules for software updates or for other deployments such as applications. <!--9388804-->

### Grace period for enforcement after deployment deadline (hours)

If you want to give users more time to install required application or software update deployments beyond the deadline, set a value for this option. This grace period is for a computer turned off for an extended time, and the user needs to install many application or update deployments. For example, this setting is helpful if a user returns from vacation, and has to wait for a long time while the client installs overdue application deployments.

Set a grace period of 0 to 120 hours. Use this setting along with the deployment property **Delay enforcement of this deployment according to user preferences**. For more information, see [Deploy applications](../../../apps/deploy-use/deploy-applications.md#delay-enforcement-with-a-grace-period).

### Enable Endpoint analytics data collection

Enables local data collection on the client for upload to Endpoint analytics. Set to **Yes** to configure devices for local data collection. Set to **No** to disable local data collection. For more information, see [Enroll Configuration Manager devices into Endpoint analytics](../../../../analytics/enroll-configmgr.md).

## Computer restart

For more information about these settings, see [Device restart notifications](device-restart-notifications.md).<!-- 7182335 -->

## Delivery Optimization

<!-- 1324696 -->
You use Configuration Manager boundary groups to define and regulate content distribution across your corporate network and to remote offices. [Windows Delivery Optimization](/windows/deployment/update/waas-delivery-optimization) is a cloud-based, peer-to-peer technology to share content between Windows devices. Configure Delivery Optimization to use your boundary groups when sharing content among peers.

> [!NOTE]
>
> - Delivery Optimization is only available on Windows 10 or later clients.
> - Internet access to the Delivery Optimization cloud service is a requirement to utilize its peer-to-peer functionality. For information about the needed internet endpoints, see [Frequently asked questions for Delivery Optimization](/windows/deployment/update/waas-delivery-optimization#frequently-asked-questions).
> - When using a CMG for content storage, the content for third-party updates won't download to clients if the **Download delta content when available** [client setting](#allow-clients-to-download-delta-content-when-available) is enabled. <!--6598587-->

### Use Configuration Manager Boundary Groups for Delivery Optimization Group ID

Choose **Yes** to apply the boundary group identifier as the Delivery Optimization group identifier on the client. When the client communicates with the Delivery Optimization cloud service, it uses this identifier to locate peers with the content. Enabling this setting also sets the Delivery Optimization download mode to the Group (2) option on targeted clients.

> [!Note]
> Microsoft recommends allowing the client to configure this setting via local policy rather than group policy. This allows the boundary group identifier to be set as the Delivery Optimization group identifier on the client. For more information, see [Delivery Optimization](../../plan-design/hierarchy/fundamental-concepts-for-content-management.md#delivery-optimization).

### Enable devices managed by Configuration Manager to use Microsoft Connected Cache servers for content download

<!--3555764-->
Choose **Yes** to allow clients to download content from an on-premises distribution point that you enable as a Microsoft Connected Cache server. For more information, see [Microsoft Connected Cache in Configuration Manager](../../plan-design/hierarchy/microsoft-connected-cache.md).

## Endpoint Protection

> [!Tip]
> In addition to the following information, you can find details about using Endpoint Protection client settings in [Example scenario: Using Endpoint Protection to protect computers from malware](../../../protect/deploy-use/scenarios-endpoint-protection.md).

### Manage Endpoint Protection client on client computers

Choose **Yes** if you want to manage existing Endpoint Protection and Windows Defender clients on computers in your hierarchy.  

Choose this option if you've already installed the Endpoint Protection client, and want to manage it with Configuration Manager. This separate installation includes a scripted process that uses a Configuration Manager application or package and program. Windows 10 or later devices don't need to have the Endpoint Protection agent installed. However, those devices will still need **Manage Endpoint Protection client on client computers** enabled. <!--503654-->

### Install Endpoint Protection client on client computers

Choose **Yes** to install and enable the Endpoint Protection client on client computers that aren't already running the client. Windows 10 or later clients don't need to have the Endpoint Protection agent installed.  

> [!NOTE]  
> If the Endpoint Protection client is already installed, choosing **No** doesn't uninstall the Endpoint Protection client. To uninstall the Endpoint Protection client, set the **Manage Endpoint Protection client on client computers** client setting to **No**. Then, deploy a package and program to uninstall the Endpoint Protection client.  

### Allow Endpoint Protection client installation and restarts outside maintenance windows. Maintenance windows must be at least 30 minutes long for client installation

Set this option to **Yes** to override typical installation behaviors with maintenance windows. This setting meets business requirements for the priority of system maintenance for security purposes.

### For Windows Embedded devices with write filters, commit Endpoint Protection client installation (requires restarts)

Choose **Yes** to disable the write filter on the Windows Embedded device, and restart the device. This action commits the installation on the device.  

If you choose **No**, the client installs on a temporary overlay that clears when the device restarts. In this scenario, the Endpoint Protection client doesn't fully install until another installation commits changes to the device. This configuration is the default.  

### Suppress any required computer restarts after the Endpoint Protection client is installed

Choose **Yes** to suppress a computer restart after the Endpoint Protection client installs.  

> [!IMPORTANT]  
> If the Endpoint Protection client requires a computer restart and this setting is **No**, then the computer restarts regardless of any configured maintenance windows.  

### Allowed period of time users can postpone a required restart to complete the Endpoint Protection installation (hours)

If a restart is necessary after the Endpoint Protection client installs, this setting specifies the number of hours that users can postpone the required restart. This setting requires that you disable the following setting: **Suppress any required computer restarts after the Endpoint Protection client is installed**.

### Disable alternate sources (such as Microsoft Windows Update, Microsoft Windows Server Update Services, or UNC shares) for the initial definition update on client computers

Choose **Yes** if you want Configuration Manager to install only the initial definition update on client computers. This setting can be helpful to avoid unnecessary network connections, and reduce network bandwidth, during the initial installation of the definition update.  



## Enrollment

### Polling interval for mobile device legacy clients

Select **Set Interval** to specify the length of time, in minutes or hours, that legacy mobile devices poll for policy. These devices include macOS.

### Polling interval for modern devices (minutes)

Enter the number of minutes that modern devices poll for policy. This setting is for Windows devices that are managed through on-premises mobile device management (MDM).

### Allow users to enroll mobile devices and Mac computers

To enable user-based enrollment of legacy devices, set this option to **Yes**, and then configure the following setting:

- **Enrollment profile**: Select **Set Profile** to create or select an enrollment profile. For more information, see [Configure client settings for enrollment](deploy-clients-to-macs.md#configure-client-settings).

### Allow users to enroll modern devices

To enable user-based enrollment of modern devices, set this option to **Yes**, and then configure the following setting:

- **Modern device enrollment profile**: Select **Set Profile** to create or select an enrollment profile. For more information, see [Create an enrollment profile that allows users to enroll modern devices](../../../mdm/get-started/set-up-device-enrollment-on-premises-mdm.md#bkmk_createProf).



## Hardware inventory  

### Enable hardware inventory on clients

By default, this setting is **Yes**. For more information, see [Introduction to hardware inventory](../manage/inventory/introduction-to-hardware-inventory.md).

### Hardware inventory schedule

Select **Schedule** to adjust the frequency that clients run the hardware inventory cycle. By default, this cycle occurs every seven days.

### Maximum random delay (minutes)

Specify the maximum number of minutes for the Configuration Manager client to randomize the hardware inventory cycle from the defined schedule. This randomization across all clients helps load-balance inventory processing on the site server. You can specify any value between 0 and 480 minutes. By default, this value is set to 240 minutes (4 hours).

### Maximum custom MIF file size (KB)

Specify the maximum size, in kilobytes (KB), allowed for each custom Management Information Format (MIF) file that the client collects during a hardware inventory cycle. The Configuration Manager hardware inventory agent doesn't process any custom MIF files that exceed this size. You can specify a size of 1 KB to 5,120 KB. By default, this value is set to 250 KB. This setting doesn't affect the size of the regular hardware inventory data file.  

> [!NOTE]  
> This setting is available only in the default client settings.  

### Hardware inventory classes

Select **Set Classes** to extend the hardware information that you collect from clients without manually editing the sms_def.mof file. For more information, see [How to configure hardware inventory](../manage/inventory/configure-hardware-inventory.md).  

### Collect MIF files

Use this setting to specify whether to collect MIF files from Configuration Manager clients during hardware inventory.  

For a MIF file to be collected by hardware inventory, it must be in the correct location on the client computer. By default, the files are located in the following paths:  

- **IDMIF files** should be in the Windows\System32\CCM\Inventory\Idmif folder.

- **NOIDMIF files** should be in the Windows\System32\CCM\Inventory\Noidmif folder.

> [!NOTE]  
> This setting is available only in the default client settings.

## Metered internet connections

Manage how Windows 8 and later computers use metered internet connections to communicate with Configuration Manager. Internet providers sometimes charge by the amount of data that you send and receive when you're on a metered internet connection.

> [!NOTE]
> The configured client setting isn't applied in the following scenarios:
>
> - If the computer is on a roaming data connection, the Configuration Manager client doesn't perform any tasks that require data to be transferred to Configuration Manager sites.  
> - If the Windows network connection properties are configured as non-metered, the Configuration Manager client behaves as if the connection is non-metered, and so transfers data to the site.  

### Client communication on metered internet connections

Choose one of the following options for this setting:

- **Allow**: All client communications are allowed over the metered internet connection, unless the client device is using a roaming data connection.

- **Limit**: The client only communicates over the metered internet connection for the following behaviors:

  - Download client policy

  - Send client state messages

  - Request software installs from Software Center

  - Download additional policy and content for required deployments at the installation deadline

    > [!NOTE]
    > On an application deployment, enable the option to **Allow clients on a metered Internet connection to download content after the installation deadline**. This option is only available for deployments with a purpose of **Required**. For more information, see [Deploy applications](../../../apps/deploy-use/deploy-applications.md).<!-- 8510020 -->

  If the client reaches the data transfer limit for the metered internet connection, the client no longer communicates with the site.

- **Block**: When the device is on a metered internet connection, the Configuration Manager client doesn't try to communicate with the site. This option is the default.

> [!IMPORTANT]
> The client always permits software installations from Software Center, regardless of the metered internet connection settings. If the user requests a software installation while the device is on a metered network, Software Center honors the user's intent.<!-- MEMDocs#285 -->

Client install and update both work when you configure this client setting to **Allow** or **Limit**. This behavior allows the client to stay current, but still manage the client communication on a metered network. You can control this behavior during client install with the ccmsetup parameter `/AllowMetered`. For more information, see [About client installation parameters and properties](../../clients/deploy/about-client-installation-properties.md#allowmetered).<!--6976145-->

## Power management  

### Allow power management of devices

Set this option to **Yes** to enable power management on clients. For more information, see [Introduction to power management](../manage/power/introduction-to-power-management.md).

### Allow users to exclude their device from power management

Choose **Yes** to let users of Software Center exclude their computer from any configured power management settings.  

### Allow network wake-up

When you enable this setting, the client configures the power settings on the computer to allow the network adapter to wake up the device. If you disable this setting, the computer's network adapter can't wake up the device.

### Enable wake-up proxy

Specify **Yes** to supplement the site's Wake On LAN setting, when it's configured for unicast packets.  

For more information about wake-up proxy, see [Plan how to wake up clients](plan/plan-wake-up-clients.md).  

> [!WARNING]  
> Don't enable wake-up proxy in a production network without first understanding how it works and evaluating it in a test environment.  

Then, configure the following additional settings as needed:

- **Wake-up proxy port number (UDP)**: The port number that clients use to send wake-up packets to sleeping computers. Keep the default port 25536, or change the number to a value of your choice.  

- **Wake On LAN port number (UDP)**: Keep the default value of 9, unless you've changed the Wake On LAN (UDP) port number on the **Ports** tab of the site **Properties**.  

    > [!IMPORTANT]  
    > This number must match the number in the site **Properties**. If you change this number in one place, it isn't automatically updated in the other place.  

- **Windows Defender Firewall exception for wake-up proxy**: The Configuration Manager client automatically configures the wake-up proxy port number on devices that run Windows Defender Firewall. Select **Configure** to specify the firewall profiles.  

    If clients run a different firewall, manually configure it to allow the **Wake-up proxy port number (UDP)**.  

- **IPv6 prefixes if required for DirectAccess or other intervening network devices. Use a comma to specify multiple entries**: Enter the necessary IPv6 prefixes for wake-up proxy to function on your network.



## Remote tools  

### Enable Remote Control on clients, and Firewall exception profiles

Select **Configure** to enable the Configuration Manager remote control feature. Optionally, configure firewall settings to allow remote control to work on client computers.  

Remote control is disabled by default.  

> [!IMPORTANT]  
> If you don't configure firewall settings, remote control might not work correctly.  

### Users can change policy or notification settings in Software Center

Choose whether users can change remote control options from within Software Center.  

### Allow Remote Control of an unattended computer

Choose whether an admin can use remote control to access a client computer that is logged off or locked. Only a logged-on and unlocked computer can be remotely controlled when this setting is disabled.  

### Prompt user for Remote Control permission

Choose whether the client computer shows a message asking for the user's permission before allowing a remote control session.  

### Prompt user for permission to transfer content from shared clipboard

Before transferring content from the shared clipboard in a remote control session, allow your users the opportunity to accept or deny file transfers. Users only need to grant permission once per session. The viewer can't give themselves permission to transfer the file.

### Grant Remote Control permission to local Administrators group

Choose whether local admins on the server that starts the remote control connection can establish remote control sessions to client computers.  

### Access level allowed

Specify the level of remote control access to allow. Choose from the following settings:  

- **No Access**
- **View Only**
- **Full Control**  

### Permitted viewers of Remote Control and Remote Assistance

Select **Set Viewers** to specify the names of the Windows users who can establish remote control sessions to client computers.  

### Show session notification icon on taskbar

Configure this setting to **Yes** to show an icon on the client's Windows taskbar to indicate an active remote control session.  

### Show session connection bar

Set this option to **Yes** to show a high-visibility session connection bar on clients, to indicate an active remote control session.  

### Play a sound on client

Set this option to use sound to indicate when a remote control session is active on a client computer. Select one of the following options:

- **No sound**
- **Beginning and end of session** (default)
- **Repeatedly during session**  

### Manage unsolicited Remote Assistance settings

Configure this setting to **Yes** to let Configuration Manager manage unsolicited Remote Assistance sessions.  

In an unsolicited Remote Assistance session, the user at the client computer didn't request assistance to start the session.  

### Manage solicited Remote Assistance settings

Set this option to **Yes** to let Configuration Manager manage solicited Remote Assistance sessions.  

In a solicited Remote Assistance session, the user at the client computer sent a request to the admin for remote assistance.  

### Level of access for Remote Assistance

Choose the level of access to assign to Remote Assistance sessions that are started in the Configuration Manager console. Select one of the following options:

- **None** (default)
- **Remote Viewing**
- **Full Control**

> [!NOTE]  
> The user at the client computer must always grant permission for a Remote Assistance session to occur.  

### Manage Remote Desktop settings

Set this option to **Yes** to let Configuration Manager manage Remote Desktop sessions for computers.  

### Allow permitted viewers to connect by using Remote Desktop connection

Set this option to **Yes** to add users specified in the permitted viewer list to the Remote Desktop local user group on clients.  

### Require network level authentication on computers that run Windows Vista operating system and later versions

Set this option to **Yes** to use network-level authentication (NLA) to establish Remote Desktop connections to client computers. NLA initially requires fewer remote computer resources, because it finishes user authentication before it establishes a Remote Desktop connection. Using NLA is a more secure configuration. NLA helps protect the computer from malicious users or software, and it reduces the risk from denial-of-service attacks.  



## Software Center

### Select the user portal

<!--CMADO-3601237,INADO-4297660-->
If you deploy the Company Portal to co-managed devices, configure this setting to **Company Portal**. This setting makes sure that notifications from Configuration Manager and Intune both launch the Company Portal. If a Configuration Manager notification is for a scenario that the Company Portal doesn't support, selecting the notification launches Software Center.

If you install the Company Portal on a co-managed device, but configure this setting to **Software Center**, then notifications from Configuration Manager launch Software Center. Notifications from Intune launch the Company Portal. This behavior may be confusing to users to interact with different portals.

The behavior of the Company Portal depends upon your co-management workload configuration. For more information, see [Use the Company Portal app on co-managed devices](../../../comanage/company-portal.md).

### Select these new settings to specify company information

Set this option to **Yes**, and then select **Customize** to configure Software Center settings for your organization. This action opens the **Software Center Customization** window.

### Software Center settings

#### Software Center Customization - General

- **Company name**: Specify the organization name that users see in Software Center.

- **Color scheme for Software Center**: Select the primary color that Software Center uses. You can choose from 48 basic colors, or define a custom color. By default, this color is Microsoft blue (Red: 0, Green: 120, Blue: 212).

- **Foreground color for Software Center**: Starting in version 2103, configure a custom color for the foreground font. By default, this color is white (Red: 255, Green: 255, Blue: 255). For some customers, their brand color doesn't work well with the default white font color for a selected item. This setting better supports these customers and improves accessibility.<!--8655575-->

- **Select a logo for Software Center**: Enable this setting, and then **Browse** to select an image to appear in Software Center. The logo for Software Center has the following requirements:

  - A JPG, PNG, or BMP file.
  - Dimensions of 400 x 100 pixels.
  - A maximum file size of 750 KB.
  - No spaces in the file name.

- **Select a logo for notifications**: Starting in version 2111, enable this setting to display a logo with notifications on devices running Windows 10 or later.<!--4993167--> Because of how the image is used, it's separate from the Software Center logo. The logo for notifications has the following requirements:

  - A JPG, PNG, or BMP file.
  - Square aspect ratio. For example, 100 x 100 pixels.
  - A maximum file size of 2 MB.
  - No spaces in the file name.

- **Hide unapproved applications in Software Center**: When you enable this option, user-available applications that require approval are hidden in Software Center.<!--1355146-->

- **Hide installed applications in Software Center**: When you enable this option, applications that are already installed no longer show in the **Applications** tab. This option is enabled by default. Installed applications are still available for review under the **Installation Status** tab.<!--1357592-->

- **Hide Application Catalog link in Software Center**: Enable this setting. The application catalog is no longer supported. This link would appear on the **Installation Status** tab of Software Center.<!--1358214-->

#### Software Center Customization - Tabs

<!--4063773-->

Choose which tabs should be visible in Software Center. To move a tab to **Visible tabs** list, select **Add**. To move it to the **Hidden tabs** list, select **Remove**. To change the order of the tabs in Software Center, select **Move Up** or **Move Down**.

Default tabs:

- **Applications**
- **Updates**
- **Operating Systems**
- **Installation Status**
- **Device Compliance**
- **Options**

You can also add up to five custom tabs:

1. Select **Add tab**.
2. Specify the **Tab name** and **Content URL** for your custom tab. Configuration Manager doesn't validate this URL.

Select **Delete Tab** to remove a custom tab. Select **Edit tab** to change the configuration of a custom tab.

> [!IMPORTANT]
> Some website features may not work in a custom tab in Software Center. Make sure to test the results before deploying this to clients.<!--519659-->
>
> Specify only trusted or intranet website addresses when you add a custom tab.<!--SCCMDocs issue 1575-->

##### Display custom tabs with Microsoft Edge WebView2 runtime

<!--9142301,8655543-->

_Applies to version 2103 and later_

Enable this option for Software Center to use the Microsoft Edge WebView2 browser control. The WebView2 browser control provides improved security and user experience. For example, more websites should work with these custom tabs without displaying script errors or security warnings.

If it's not already installed, the Configuration Manager client installs the **Microsoft Edge WebView2 runtime (fixed version)** on the device. The installer is over 100 MB in size. If you need to enable this setting on a large number of clients, and are concerned about the effect of network usage, predeploy the WebView2 runtime as an application. Use the software distribution features of Configuration Manager to better control the content distribution and timing of software installation.<!-- 12769440 -->

> [!NOTE]
> - If the client device isn't running .NET Framework version 4.6.2 or later, it falls back to use the Internet Explorer browser control. Starting in version 2107, the client requires .NET version 4.6.2, and version 4.8 is recommended.<!--10402814--> For more information, see [Prerequisites for deploying clients to Windows computers](prerequisites-for-deploying-clients-to-windows-computers.md#more-details-about-microsoft-net).
> - When using custom tabs in certain circumstances, you may encounter the following exception:  `Could not load type 'System.Runtime.InteropServices.Architecture' from assembly 'mscorlib Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089'`. To work around the issue, update .NET Framework to version 4.7.1 or later for the client. <!--12109686-->

If you don't enable this option, Software Center uses the Windows built-in Internet Explorer browser control.

#### Software Center Customization - Defaults
<!--3612112-->

- Configure the **Default application filter** as either **All** or only **Required** applications. By default, it shows all applications.

  Software Center always uses your default setting. Users can change this filter, but Software Center doesn't persist their preference.

- Set the **Default application view** as either **Tile view** or **List view**. By default, it uses the tile view.

  If a user changes this configuration, Software Center persists the user's preference in the future.

For more information on the appearance of these settings, see the [Software Center user guide](../../understand/software-center.md#applications).

## Software deployment  

### Schedule re-evaluation for deployments

Configure a schedule for when Configuration Manager reevaluates the requirement rules for all deployments. The default value is every seven days.  

> [!IMPORTANT]  
> This setting is more invasive to the local client than it is to the network or site server. A more aggressive reevaluation schedule negatively affects the performance of your network and client computers. Microsoft doesn't recommend setting a lower value than the default. If you change this value, closely monitor performance.  

Start this action from a client as follows: in the **Configuration Manager** control panel, from the **Actions** tab, select **Application Deployment Evaluation Cycle**.  



## Software inventory  

### Enable software inventory on clients

This option is set to **Yes** by default. For more information, see [Introduction to software inventory](../manage/inventory/introduction-to-software-inventory.md).

### Schedule software inventory and file collection

Select **Schedule** to adjust the frequency that clients run the software inventory and file collection cycles. By default, this cycle occurs every seven days.

### Inventory reporting detail

Specify one of the following levels of file information to inventory:

- **File only**
- **Product only**
- **Full details** (default)

### Inventory these file types

If you want to specify the types of file to inventory, select **Set Types**, and then configure the following options:  

> [!NOTE]  
> If multiple custom client settings are applied to a computer, the inventory that each setting returns is merged.  

- Select **New** to add a new file type to inventory. Then specify the following information in the **Inventoried File Properties** dialog box:  

    - **Name**: Provide a name for the file that you want to inventory. Use an asterisk (`*`) wildcard to represent any string of text, and a question mark (`?`) to represent any single character. For example, if you want to inventory all files with the extension .doc, specify the file name `*.doc`.  

    - **Location**: Select **Set** to open the **Path Properties** dialog box. Configure software inventory to search all client hard disks for the specified file, search a specified path (for example, `C:\Folder`), or search for a specified variable (for example, `%windir%`). You can also search all subfolders under the specified path.  

    - **Exclude encrypted and compressed files**: When you choose this option, any compressed or encrypted files aren't inventoried.  

    - **Exclude files in the Windows folder**: When you choose this option, any files in the Windows folder and its subfolders aren't inventoried.  

    Select **OK** to close the **Inventoried File Properties** dialog box. Add all the files that you want to inventory, and then select **OK** to close the **Configure Client Setting** dialog box.  

### Collect files

If you want to collect files from client computers, select **Set Files**, and then configure the following settings:  

> [!NOTE]  
> If multiple custom client settings are applied to a computer, the inventory that each setting returns is merged.  

- In the **Configure Client Setting** dialog box, select **New** to add a file to be collected.  

- In the **Collected File Properties** dialog box, provide the following information:  

    - **Name**: Provide a name for the file that you want to collect. Use an asterisk (`*`) wildcard to represent any string of text, and a question mark (`?`) to represent any single character.  

    - **Location**: Select **Set** to open the **Path Properties** dialog box. Configure software inventory to search all client hard disks for the file that you want to collect, search a specified path (for example, `C:\Folder`), or search for a specified variable (for example, `%windir%`). You can also search all subfolders under the specified path.  

    - **Exclude encrypted and compressed files**: When you choose this option, any compressed or encrypted files aren't collected.  

    - **Stop file collection when the total size of the files exceeds (KB)**: Specify the file size, in kilobytes (KB), after which the client stops collecting the specified files.  

    > [!NOTE]  
    > The site server collects the five most recently changed versions of collected files, and stores them in the `<ConfigMgr installation directory>\Inboxes\Sinv.box\Filecol` directory. If a file hasn't changed since the last software inventory cycle, the file isn't collected again.  
    >
    > Software inventory doesn't collect files larger than 20 MB.  
    >
    > The value **Maximum size for all collected files (KB)** in the **Configure Client Setting** dialog box shows the maximum size for all collected files. When this size is reached, file collection stops. Any files already collected are retained and sent to the site server.  

    > [!IMPORTANT]
    > If you configure software inventory to collect many large files, this configuration might negatively affect the performance of your network and site server.  

    For information about how to view collected files, see [How to use Resource Explorer to view software inventory](../manage/inventory/use-resource-explorer-to-view-software-inventory.md).  

    Select **OK** to close the **Collected File Properties** dialog box. Add all the files that you want to collect, and then select **OK** to close the **Configure Client Setting** dialog box.  

### Set Names

The software inventory agent retrieves manufacturer and product names from file header information. These names aren't always standardized in the file header information. When you view software inventory in Resource Explorer, different versions of the same manufacturer or product name can appear. To standardize these display names, select **Set Names**, and then configure the following settings:  

- **Name type**: Software inventory collects information about both manufacturers and products. Choose whether you want to configure display names for a **Manufacturer** or a **Product**.  

- **Display name**: Specify the display name that you want to use in place of the names in the **Inventoried names** list. To specify a new display name, select **New**.  

- **Inventoried names**: To add an inventoried name, select **New**. This name is replaced in software inventory by the name chosen in the **Display name** list. You can add multiple names to replace.  



## Software Metering

### Enable software metering on clients

This setting is set to **Yes** by default. For more information, see [Software metering](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md#configure-software-metering).

### Schedule data collection

Select **Schedule** to adjust the frequency that clients run the software metering cycle. By default, this cycle occurs every seven days.



## Software updates  

### Enable software updates on clients

Use this setting to enable software updates on Configuration Manager clients. When you disable this setting, Configuration Manager removes existing deployment policies from clients. When you re-enable this setting, the client downloads the current deployment policy.  

> [!IMPORTANT]  
> When you disable this setting, compliance policies that rely on software updates will no longer function.  

### Software update scan schedule

Select **Schedule** to specify how often the client starts a compliance assessment scan. This scan determines the state for software updates on the client (for example, required or installed). For more information about compliance assessment, see [Software updates compliance assessment](../../../sum/understand/software-updates-introduction.md#BKMK_SUMCompliance).  

By default, this scan uses a simple schedule to start every seven days. You can create a custom schedule. You can specify an exact start day and time, use Universal Coordinated Time (UTC) or the local time, and configure the recurring interval for a specific day of the week.  

> [!NOTE]  
> If you specify an interval of less than one day, Configuration Manager automatically defaults to one day.  

> [!WARNING]  
> The actual start time on client computers is the start time plus a random amount of time, up to two hours. This randomization prevents client computers from initiating the scan and simultaneously connecting to the active software update point.  

### Schedule deployment re-evaluation

Select **Schedule** to configure how often the software updates client agent reevaluates software updates for installation status on Configuration Manager client computers. When previously installed software updates are no longer found on clients but are still required, the client reinstalls the software updates.

Adjust this schedule based on company policy for software update compliance, and whether users can uninstall software updates. Every deployment re-evaluation cycle results in network and client computer processor activity. By default, this setting uses a simple schedule to start the deployment re-evaluation scan every seven days.  

> [!NOTE]  
> If you specify an interval of less than one day, Configuration Manager automatically defaults to one day.  

### Allow user proxy for software update scans
<!--8379199-->
*(Introduced in version 2010)*

Beginning with the September 2020 cumulative update, HTTP-based WSUS servers will be secure by default. A client scanning for updates against an HTTP-based WSUS will no longer be allowed to leverage a user proxy by default. Set this option to **Yes** to allow these connections if you require a user proxy despite the security trade-offs. By default, this setting is set to **No**. For more information about the changes for scanning WSUS, see [September 2020 changes to improve security for Windows devices scanning WSUS](https://go.microsoft.com/fwlink/?linkid=2144403). To ensure that the best security protocols are in place, we highly recommend that you use the TLS/SSL protocol to help [secure your software update infrastructure](../../../sum/get-started/software-update-point-ssl.md).

### Enforce TLS certificate pinning for Windows Update client for detecting updates
<!--8913032-->
*(Introduced in version 2103)*

Further increase the security of HTTPS scans against WSUS by enforcing certificate pinning. To use certificate pinning, ensure your WSUS server is enabled for TLS/SSL, and add the certificates for the WSUS servers to the new `WindowsServerUpdateServices` certificate store on your clients. For more information about certificate pinning for devices scanning HTTPS-configured WSUS servers, see [secure your software update infrastructure](../../../sum/get-started/software-update-point-ssl.md). The following settings are available starting in Configuration Manager version 2103:
- **No**: Don't enable enforcement of TLS certificate pinning for WSUS scanning
- **Yes**: Enables enforcement of TLS certificate pinning for devices during WSUS scanning (default)

### When any software update deployment deadline is reached, install all other software update deployments with deadline coming within a specified period of time

Set this option to **Yes** to install all software updates from required deployments with deadlines occurring within a specified period of time. When a required software update deployment reaches a deadline, the client starts installation for the software updates in the deployment. This setting determines whether to install software updates from other required deployments that have a deadline within the specified time.  

Use this setting to speed up installation for required software updates. This setting also has the potential to increase client security, decrease notifications to the user, and decrease client restarts. By default, this setting is set to **No**.  

### Period of time for which all pending deployments with deadline in this time will also be installed

Use this setting to specify the period of time for the previous setting. You can enter a value from 1 to 23 hours, and from 1 to 365 days. By default, this setting is configured for seven days.  

### Allow clients to download delta content when available

Set this option to **Yes** to allow clients to use delta content files. This setting allows the Windows Update Agent on the device to determine what content is needed and selectively download it.

- Before enabling this client setting, ensure Delivery Optimization is configured appropriately for your environment. For more information, see [Windows Delivery Optimization](../../../sum/deploy-use/optimize-windows-10-update-delivery.md#windows-delivery-optimization) and the [Delivery Optimization client setting](#delivery-optimization).

- This client setting replaces **Enable installation of Express installation files on clients**. Set this option to **Yes** to allow clients to use express installation files. For more information, see [Manage Express installation files for Windows 10 updates](../../../sum/deploy-use/manage-express-installation-files-for-windows-10-updates.md).

- When this option is set, delta download is used for all Windows update installation files, not just express installation files.

  When using a CMG for content storage, the content for third-party updates won't download to clients if the **Download delta content when available** client setting is enabled. <!--6598587-->

### Port that clients use to receive requests for delta content

This setting configures the local port for the HTTP listener to download delta content. It's set to 8005 by default. You don't need to open this port in the client firewall.

> [!NOTE]
>This client setting replaces **Port used to download content for Express installation files**.

### If content is unavailable from distribution points in the current boundary group, immediately fallback to a neighbor or the site default

*(Introduced in version 2010)*

If delta content is unavailable from distribution points in the current boundary group, you can allow immediate fallback to a neighbor or the site default boundary group distribution points. This setting is useful when using delta content for software updates since the timeout setting per download job is 5 minutes. The following options are available:

- **Yes**: For delta content, the client doesn't wait to reach the fallback time (in minutes) defined by the [Boundary Group relationship](../../servers/deploy/configure/boundary-group-procedures.md#configure-fallback-behavior). Clients immediately fall back to a neighbor or the site default content distribution points when both of the following conditions are met:
      - Delta content is unavailable from distribution points in the current boundary group.
      - The software update deployment allows fallback.

- **No** (default): The client honors the fallback time (in minutes) defined by the [Boundary Group relationship](../../servers/deploy/configure/boundary-group-procedures.md#configure-fallback-behavior) when it's allowed on the software update deployment. Delta download content may fail with a timeout even if the update content is available on a neighbor or the site default distribution point group.

> [!NOTE]
> This setting is for delta content only.
### Enable management of the Office 365 Client Agent

When you set this option to **Yes**, it enables the configuration of Microsoft 365 Apps installation settings. It also enables downloading files from Office Content Delivery Networks (CDNs), and deploying the files as an application in Configuration Manager. For more information, see [Manage Microsoft 365 Apps](../../../sum/deploy-use/manage-office-365-proplus-updates.md).

### Enable update notifications from Microsoft 365 Apps
<!--10628998-->
*(Introduced in version 2111)*

You can configure the end-user experience for Microsoft 365 Apps updates. This client setting allows you to enable or disable notifications from Microsoft 365 Apps for these updates. The following options are available for the setting:

- **No**: Doesn't display Microsoft 365 Apps updates notifications from Microsoft 365 Apps (default)
- **Yes**: Displays Microsoft 365 Apps updates notifications from Microsoft 365 Apps

Which notifications are displayed to the user about updates for Microsoft 365 Apps is also determined by the settings for per deployment notifications from Software Center. If the deployment's user notifications from Software Center are disabled (found on the [**User Experience** page for the deployment](../../../sum/deploy-use/manually-deploy-software-updates.md#BKMK_4DeployUpdateGroup)), then the end user won't receive any notifications from either Software Center or Microsoft 365 Apps, regardless of how notifications from Microsoft 365 Apps are set. If notifications from both Software Center and Microsoft 365 Apps are enabled, then the end user will receive notifications from Software Center and Microsoft 365 Apps. Below is a chart of which notifications for Microsoft 365 Apps updates are displayed to the end user for these settings:</br></br>  

| &nbsp; | **Display** per deployment Software Center notifications| **Hide** per deployment Software Center notifications|
|---|---|--|
| Enable update notifications from Microsoft 365 Apps: **Yes** | User receives notifications from Software Center </br></br> User receives notifications from Microsoft 365 Apps| No notifications from Software Center </br></br> No notifications from Microsoft 365 Apps |
| Enable update notifications from Microsoft 365 Apps: **No** | User receives notifications from Software Center </br></br> No notifications from Microsoft 365 Apps | No notifications from Software Center </br></br> No notifications from Microsoft 365 Apps |

### <a name="bkmk_SUMMaint"></a> Enable installation of software updates in "All deployments" maintenance window when "Software Update" maintenance window is available

When you set this option to **Yes**, and the client has at least one "Software Update" maintenance window defined, software updates will install during an "All deployments" maintenance window.

By default, this setting is set to **No**. This value uses the same behavior as before: if both types exist, it ignores the window. <!--2839307-->

> [!NOTE]
> This setting also applies to maintenance windows that you configure to apply to **Task sequences**.<!-- SCCMDocs-pr #4596 -->
>
> If the client only has an **All deployments** window available, it still installs software updates or task sequences in that window.

#### Maintenance window example

For example, you configure the following maintenance windows:

- **All deployment**: 02:00 - 04:00
- **Software updates**: 04:00 - 06:00

By default, the client only installs software updates during the second maintenance window. It ignores the maintenance window for all deployments in this scenario. When you change this setting to **Yes**, the client installs software updates between 02:00 - 06:00.

### <a name="bkmk_thread-priority"></a> Specify thread priority for feature updates

<!--3734525-->
You can adjust the priority with which supported versions of Windows 10 or later clients install a feature update through [Windows servicing](../../../osd/deploy-use/manage-windows-as-a-service.md). This setting has no impact on Windows in-place upgrade task sequences.

This client setting provides the following options:

- **Not Configured**: Configuration Manager doesn't change the setting. Admins can pre-stage their own setupconfig.ini file. This value is the default.

- **Normal**: Windows Setup uses more system resources and updates faster. It uses more processor time, so the total installation time is shorter, but the user's outage is longer.  

  Configures the setupconfig.ini file on the device with the `/Priority Normal` [Windows setup command-line option](/windows-hardware/manufacture/desktop/windows-setup-command-line-options).

- **Low**: You can continue to work on the device while it downloads and updates in the background. The total installation time is longer, but the user's outage is shorter. You may need to increase the update max run time to avoid a time-out when you use this option.  

   Removes the `/Priority` [Windows setup command-line option](/windows-hardware/manufacture/desktop/windows-setup-command-line-options) from the setupconfig.ini file.

### Enable third party software updates

When you set this option to **Yes**, it sets the policy for **Allow signed updates for an intranet Microsoft update service location** and installs the signing certificate to the Trusted Publisher store on the client.

### <a name="bkmk_du"></a>Enable Dynamic Update for feature updates
<!--4062619-->
Use this setting to configure [Dynamic Update for Windows](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/The-benefits-of-Windows-10-Dynamic-Update/ba-p/467847). Dynamic Update installs language packs, features on demand, drivers, and cumulative updates during Windows setup by directing the client to download these updates from the internet. When this setting is set to either **Yes** or **No**, Configuration Manager modifies the [setupconfig](/windows-hardware/manufacture/desktop/windows-setup-command-line-options) file that is used during feature update installation.

- **Not Configured** - The default value. No changes are made to the setupconfig file.
  - Dynamic Update is enabled by default on all supported versions of Windows 10 or later.
    - For Windows 10, version 1803 and earlier, Dynamic Update checks the device's WSUS server for approved dynamic updates. In Configuration Manager environments, dynamic updates are never directly approved in the WSUS server so these devices don't install them.
    - Starting with Windows 10, version 1809, Dynamic Update uses the device's internet connection to get dynamic updates from Microsoft Update. These dynamic updates aren't published for WSUS use.
- **Yes** - Enables Dynamic Update.
- **No** - Disables Dynamic Update.

### <a name="bkmk_fserv"></a>Enable features introduced via servicing are off by default.

<!--16834520-->
To learn more about the settings: “Enable features introduced via servicing are off by default”, please read this [blog](https://techcommunity.microsoft.com/t5/windows-it-pro-blog/commercial-control-for-continuous-innovation/ba-p/3737575). The post describes the Commercial control for continuous innovation in Windows. The setting for this policy is now integrated with the Configuration Manager 2303. More information on the Commercial control timeline and versions of Windows 11 supported by the setting can be found in the blog.

- **Not Configured** - The default value, then features that are shipped via a monthly quality update (servicing) will remain off until the feature update that includes these features is installed.
  - Enable features introduced via servicing are off by default on all supported versions of Windows 11 22621.1344 or later.
- **Yes** - Enables Feature Update, then all features available in the latest monthly quality update installed will be on.
- **No** - Disables Feature Update, then features that are shipped via a monthly quality update (servicing) will remain off until the feature update that includes these features is installed.

## State Messaging

### State message reporting cycle (minutes)

Specifies how often clients report state messages. This setting is 15 minutes by default.



## User and device affinity  

### User device affinity usage threshold (minutes)

Specify the number of minutes before Configuration Manager creates a user device affinity mapping. By default, this value is 2880 minutes (two days).

### User device affinity usage threshold (days)

Specify the number of days over which the client measures the threshold for usage-based device affinity. By default, this value is 30 days.

> [!NOTE]  
> For example, you specify **User device affinity usage threshold (minutes)** as **60** minutes, and **User device affinity usage threshold (days)** as **5** days. Then the user must use the device for 60 minutes over a period of 5 days to create automatic affinity with the device.  

### Automatically configure user device affinity from usage data

Choose **Yes** to create automatic user device affinity based on the usage information that Configuration Manager collects.  

### Allow user to define their primary devices
<!--3485366-->
When this setting is **Yes**, users can identify their own primary devices in Software Center. For more information, see the [Software Center user guide](../../understand/software-center.md#work-information).

> [!NOTE]
> Default values are:
> - User device affinity usage threshold (minutes): 2880
> - User device affinity usage threshold (days): 30
> - Automatically configure user device affinity from usage data: No
> - Allow user to define their primary devices: No

## Windows Diagnostic Data

> [!IMPORTANT]
> This group was previously called **Windows Analytics**. Microsoft retired the Windows Analytics service on January 31, 2020. For more information, see [KB 4521815: Windows Analytics retirement on January 31, 2020](https://support.microsoft.com/help/4521815/windows-analytics-retirement).
>
> Desktop Analytics is the evolution of Windows Analytics. Use Desktop Analytics to manage Windows diagnostic data settings. For more information, see [What is Desktop Analytics](../../../desktop-analytics/overview.md).
