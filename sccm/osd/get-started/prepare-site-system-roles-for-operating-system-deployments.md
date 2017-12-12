---
title: Prepare site system roles for operating system deployments
titleSuffix: "Configuration Manager"
description: "Configure the site system roles before you deploy operating systems in System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-osd
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 0ef5f3ce-b0e4-4775-b5c2-b245e45b4194
caps.latest.revision: 11
caps.handback.revision: 0
author: aczechowski
ms.author: aaroncz
manager: angrobe

---
# Prepare site system roles for operating system deployments with System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

To deploy operating systems in System Center Configuration Manager, you must first prepare the following site system roles that require specific configurations and considerations.

##  <a name="BKMK_DistributionPoints"></a> Distribution points  
 The distribution point  site system role contains source files for clients to download, such as application content, software updates, operating system images,  and boot images. You can control content distribution by using bandwidth, throttling, and scheduling options.  

 It is important that you have  enough distribution points to support the deployment of operating systems to computers. It's also important that you  and plan for the placement of these distribution points in your hierarchy. You will find most of this planning information in [Manage content and content infrastructure](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md). However, there are some additional planning considerations for distribution points specific to operating system deployment.  

###  <a name="BKMK_AdditionalPlanning"></a> Additional planning considerations for distribution points  
 The following are additional planning things to consider for distribution points:  

-   **How can I  prevent unwanted operating system  deployments?**  

     Configuration Manager does not distinguish site servers from other destination computers in a collection. If you deploy a required task sequence to a collection that contains a site server, the site server runs the task sequence in the same way that any other computer in the collection runs the task sequence. Ensure that your operating system deployment uses a collection that contains the clients that you intend to run the deployment.  

     You can manage the behavior for high-risk task sequence deployments. A high-risk deployment automatically installs on a client and has the potential to cause unwanted results. For example, a task sequence with a purpose of Required that deploys an operating system. To reduce the risk of an unwanted high-risk deployment, you can configure deployment verification settings. For more information, see [Settings to manage high-risk deployments](../../protect/understand/settings-to-manage-high-risk-deployments.md).  

-   **How many computers can receive an operating system image at one time from a single distribution point?**  

     To estimate how many distribution points you need, consider the processing speed and disk I/O of the distribution point, the available bandwidth on the network, and the effect that the size of the image package has on these resources. For example, on a 100 megabyte (MB) Ethernet network, the maximum number of computers that can process a 4 gigabyte (GB) image package in one hour is 11 computers if you do not consider any other server resource factors.  

     `100 Megabits/sec = 12.5 Megabytes/sec = 750 Megabytes/min = 45 Gigabytes/hour = 11 images @ 4GB per image.`  

     If you must deploy an operating system to a specific number of computers within a specific time frame, distribute the image to an appropriate number of distribution points.  

-   **Can I deploy an operating system to a distribution point?**  

     You can deploy an operating system to a distribution point, but the operating system image must be received from a different distribution point.  

###  <a name="BKMK_PXEDistributionPoint"></a> Configuring distribution points to accept PXE requests  
 To deploy operating systems to Configuration Manager clients that make PXE boot requests, you must configure one or more distribution points to accept PXE requests. Once you configure the distribution point, it will respond to PXE boot request and determine the appropriate deployment action to take.

> [!IMPORTANT]  
>  [Windows Deployment Services](../plan-design/infrastructure-requirements-for-operating-system-deployment.md#BKMK_WDS) must be installed on the all PXE-enabled distribution points.  

 Use the following procedure to modify an existing distribution point so that it can accept PXE requests. For information about how to install a new distribution point, see [Install or modify a distribution point](../../core/servers/deploy/configure/install-and-configure-distribution-points.md).  

#### To modify an existing distribution point to accept PXE requests  

1.  In the Configuration Manager console, click **Administration**, expand **Overview** and click **Distribution points**.  

2.  Select the distribution point to configure, and on the **Home** tab in the **Properties** group, click **Properties**.  

3.  On the property page for the distribution point, click the **PXE** tab. and select **Enable PXE support for clients** to enable PXE on this  distribution point.  

4.  Click **Yes** in the **Review Required Ports for PXE** dialog box to  confirm that you want to enable PXE. Configuration Manager automatically configures the default ports on a  Windows firewall. You must manually configure the ports if you use a different firewall.  

    > [!NOTE]  
    >  If WDS and DHCP are installed on the same server, you must configure WDS to listen on a different port (since DHCP listens on the same port). For more information, see [Considerations when you have WDS and DHCP on the same server](../plan-design/infrastructure-requirements-for-operating-system-deployment.md#BKMK_WDSandDHCP).  

5.  Select **Allow this distribution point to respond to incoming PXE requests** to enable WDS so that it responds to incoming PXE service requests. You can use this setting to enable and disable the service without removing the PXE functionality from the distribution point.  

6.  Select **Enable unknown computer support** to deploy operating systems to computers that are not managed by Configuration Manager.  

7.  Select **Require a password when computers use PXE**, and then specify a strong password to provide additional security for your PXE deployment.  

8.  In the **User Device Affinity** list, choose how you want the distribution point to associate users with the destination computer for PXE deployments.  

    -   Select **Do not use user device affinity** to not associate users with the destination computer.  

    -   Select **Allow user device affinity with manual approval** to wait for approval from an administrative user before users are associated with the destination computer.  

    -   Select **Allow user device affinity with automatic approval** to automatically associate users with the destination computer without waiting for approval.  

     For more information, see [Associate users with a destination computer](../get-started/associate-users-with-a-destination-computer.md).  

9. Specify that the distribution point responds to PXE requests from all network interfaces or from specific network interfaces. If you choose to have the distribution point respond to a specific network interfaces, provide the MAC address for each network interface.  

10. Specify, in seconds, how long the delay is for the distribution point before it responds to computer requests when multiple PXE-enabled distribution points are used.  

11. Click **OK** to update the properties of the distribution point.  

###  <a name="BKMK_RamDiskTFTP"></a> Customize the RamDisk TFTP block size and window size on PXE-enabled distribution points  
You can customize the RamDisk TFTP block size, and beginning in Configuration Manager version 1606, the window size for PXE-enabled distribution points. If you have customized your network, it could cause the boot image download to fail with a time-out error because the block or window size is too large. The RamDisk TFTP block size and window size customization allow you to optimize TFTP traffic when using PXE to meet your specific network requirements.   
You will need to test the customized settings in your environment to determine what is most efficient.  

-   **TFTP block size**: The block size is the size of the data packets that are sent by the server to the client that is downloading the file (as discussed in RFC 2347). A larger block size allows the server to send fewer packets, so there are fewer round-trip delays between the server and the client. However, a large block sizes leads to fragmented packets, which most PXE client implementations do not support.  

-   **TFTP window size**: TFTP requires an acknowledgment (ACK) packet for each block of data that is sent. The server does not send the next block in the sequence until it receives the ACK packet for the previous block. TFTP windowing is a feature in Windows Deployment Services that enables you to define how many data blocks it takes to fill a window. The server sends the data blocks back-to-back until the window is filled, and then the client sends an ACK packet. Increasing this window size reduces the number of round-trip delays between the client and server and decreases the overall time that is required to download a boot image.  


#### To modify the RamDisk TFTP window size  

-   Add the following registry key on PXE-enabled distribution points to customize the RamDisk TFTP window size:  

     **Location**: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\DP  
    Name: RamDiskTFTPWindowSize  

     **Type**: REG_DWORD  

     **Value**: &lt;customized window size>  

 The default value is 1 (1 data block fills the window)  

#### To modify the RamDisk TFTP block size  

-   Add the following registry key on PXE-enabled distribution points to customize the RamDisk TFTP window size:  

     **Location**: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\DP  
    Name: RamDiskTFTPBlockSize  

     **Type**: REG_DWORD  

     **Value**: &lt;customized block size>  

 The default value is 4096 (4k).  


###  <a name="BKMK_DPMulticast"></a> Configure distribution points to support multicast  
 Multicast is a network optimization method that you can use on distribution points when multiple clients are likely to download the same operating system image at the same time. When multicast is used, multiple computers can simultaneously download the operating system image as it is multicast by the distribution point, rather than having the distribution point send a copy of the data to each client over a separate connection. You must configure at least one distribution point to  support multicast. For more information, see [Use multicast to deploy Windows over the network](../deploy-use/use-multicast-to-deploy-windows-over-the-network.md).  

 Before you deploy the operating system, you must configure a distribution point to support multicast. Use the following procedure to modify an existing distribution point to support multicast. For information about how to install a new distribution point, see [Install and configure distribution points](../../core/servers/deploy/configure/install-and-configure-distribution-points.md).

#### To enable multicast for a distribution point  

1.  In the Configuration Manager console, click **Administration**.  

2.  In the **Administration** workspace, expand **Overview**, and then select the **Distribution Points** node.  

3.  Select the distribution point that you want to use to multicast the operating system image.  

4.  On the **Home** tab, in the **Properties** group, click **Properties**.  

5.  Select the **Multicast** tab, and configure the following options:  

    -   **Enable Multicast**: You must select this option for the distribution point to support multicast.  

    -   **Multicast Connection Account**: Specify an account to connect to the site database.  

    -   **Multicast address settings**: Specify the IP addresses to send data to the destination computers. By default, the IP address is obtained from a DHCP server that is enabled to distribute multicast addresses. Depending on the network environment, you can specify a range of IP addresses between 239.0.0.0 and 239.255.255.255.  

        > [!IMPORTANT]  
        >  These IP addresses must be accessible by the destination computers that request the operating system image. This means that routers and firewalls in between the destination computer and the site server must be configured to allow multicast traffic.  

    -   **UDP Port Range**: Specify the range of UDP ports to send data to the destination computers.  

        > [!IMPORTANT]  
        >  These ports must be accessible by the destination computers that request the operating system image. This means that routers and firewalls in between the destination computer and the site server must be configured to allow multicast traffic.  

    -   **Enabled scheduled multicast**: Specify how Configuration Manager controls when to start deploying operating systems to destination computers. Click **Enabled scheduled multicast**, and then select the following options.  

         In the **Session start delay** box, specify how many minutes that Configuration Manager waits before it responds to the first deployment request.  

         In the **Minimum session size** box, specify how many requests must be received before Configuration Manager starts to deploy the operating system.  

    -   **Transfer rate**: Select the transfer rate to download data to the destination computers.  

    -   **Maximum clients**: Specify the maximum number of destination computers that can download the operating system from this distribution point.  

6.  Click **OK**.  

##  <a name="BKMK_StateMigrationPoints"></a> State migration point  
 The state migration point stores user state data that is captured on one computer and then restored on another computer. However, when you capture user settings for an operating system deployment on the  same computer, such as a deployment where you refresh the operating system on the destination computer, you can choose whether to  store the data on the same computer by using hard-links or use a state migration point. For some computer deployments, when you create the state store, Configuration Manager automatically creates an association between the state store and the destination computer. As you plan for the state migration point, consider the following factors.  

### User state size  
 The size of the user state directly affects disk storage on the state migration point and network performance during the migration. Consider the size of the user state and the number of computers to migrate. Consider also what settings to migrate from the computer. For example, if **My Documents** is already backed up to a server, then perhaps you do not have to migrate it as part of the image deployment. Avoiding unnecessary migrations can keep the overall size of the user state smaller and decrease the effect it would otherwise have on network performance and disk storage on the state migration point.  

### User State Migration Tool  
 To capture and restore the user state during the deployment of the operating systems, you must use a User State Migration Tool (USMT) package that points to the USMT source files. Configuration Manager automatically creates this package in the Configuration Manager console in **Software Library** > **Application Management** > **Packages**. Configuration Manager uses USMT 10.0, which is distributed in the Windows Assessment and Deployment Kit (Windows ADK), to capture the user state from one operating system and then restore it to another operating system.  

 For a description of different migration scenarios for USMT 10.0, see [Common Migration Scenarios](https://technet.microsoft.com/library/mt299169\(v=vs.85\).aspx).  

### Retention policy  
 When you configure the state migration point, you can specify the length of time to keep the user state data that is stored on it. The length of time to keep the data on the state migration point depends on two considerations:  

-   The effect that the stored data has on disk storage.  

-   The potential requirement to keep the data for a time in case you must migrate the data again.  

 State migration occurs in two phases: Capturing the data and restoring the data. When you capture data, the user state data is collected and saved to the state migration point. When you restore the data, the user state data is retrieved from the state migration point, written to the destination computer, and then the **Release State Store** task sequence step releases the stored data. When the data is released, the retention timer starts. If you select the option to delete migrated data immediately, the user state data is deleted as soon as it is released. If you select the option to keep the data for a certain period of time, the data is deleted when that period of time elapses after the state data is released. The longer you set the retention period, the more disk space you are likely to require.  

### Select drive to store user state migration data  
 When you configure the state migration point, you must specify the drive on the server to store the user state migration data. You select a drive from a fixed list of drives. However, some of these drives might represent non-writable drives, such as the CD drive, or a non-network share drive. In addition, some drive letters might not be mapped to any drives on the computer. You must specify a writable, shared drive when you configure the state migration point.  

### Configure a state migration point  
 You can use the following methods to configure a state migration point to store the user state data:  

-   Use the **Create Site System Server Wizard** to create a new site system server for the state migration point.  

-   Use the **Add Site System Roles Wizard** to add a state migration point to an existing server.  

 When you use these wizards, you are prompted to provide the following information for the state migration point:  

-   The folders to store the user state data.  

-   The maximum number of clients that can store data on the state migration point.  

-   The minimum free space for the state migration point to store user state data.  

-   The deletion policy for the role. You can specify that the user state data is deleted immediately after it is restored on a computer, or after a specific number of days after the user data is restored on a computer.  

-   Whether the state migration point responds only to requests to restore user state data. When you enable this option, you cannot use the state migration point to store user state data.  

 For the steps to install a site system role, see [Add site system roles](../../core/servers/deploy/configure/add-site-system-roles.md).  
