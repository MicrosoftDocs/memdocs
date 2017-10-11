---
title: "Manage distribution points"
titleSuffix: "Configuration Manager"
description: "Host the content (files and software) that you deploy to devices and users by using distribution points. Here's how to install and configure them."
ms.custom: na
ms.date: 09/18/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: aebafaf9-b3d5-4a0f-9ee5-685758c037a1
caps.latest.revision: 5
author: Brenduns
ms.author: brenduns
manager: angrobe
---
# Install and configure distribution points for System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

You install System Center Configuration Manager distribution points to host the content (files and software) that you deploy to devices and users. You can also create distribution point groups that simplify how you manage distribution points, and how you distribute content to distribution points.  

 When you *install a new distribution point* (by using the installation wizard) or *manage the properties of an existing distribution point* (by editing the distribution point's properties), you can configure most of the distribution point settings. A few settings are available only when you're either installing or editing, but not both:  

-   Settings that are available only when you're installing a distribution point:  

    -   **Allow Configuration Manager to install IIS on the distribution point computer**

    -   **Configure drive space settings for the distribution point**  

-   Settings that are available only when you're editing the properties of a distribution point:  

    -   **Manage distribution point group relationships**  

    -   **View Content deployed to the distribution point**  

    -   **Configure Rate limits for data transfers to distribution points**  

    -   **Configure Schedules for data transfers to distribution points**  

##  <a name="bkmk_install"></a> Install a distribution point  
You must designate a site system server as a distribution point before content can be made available to client computers. You must also assign a distribution point to at least one [boundary group](/sccm/core/servers/deploy/configure/boundary-groups#distribution-points) before on-premises client computers can use that distribution point as a content source location. You can add the distribution point site role to a new site system server or add the site role to an existing site system server.


 When you install a new distribution point, you use an installation wizard that walks you through the available settings. Before you start, consider the following:  

-   You must have the following security permissions to create and configure a distribution point:  

    -   **Read** for the **Distribution Point** object  

    -   **Copy to Distribution Point** for the **Distribution Point** object  

    -   **Modify** for the **Site** object  

    -   **Manage Certificates for Operating System Deployment** for the **Site** object  

-   Internet Information Services (IIS) must be installed on the server that will host the distribution point. When you install the site system role, Configuration Manager can install and configure IIS for you.  

Use the following basic procedures to install or change a distribution point. For details about available configuration options, see the [Configure a distribution point](#bkmk_configs) section of this topic.  

#### To install a distribution point  

1.  In the Configuration Manager console, choose **Administration** >  **Site Configuration** > **Servers and Site System Roles**.  

2.  Add the distribution point site system role to a new or existing site system server:  

    -   **New site system server**: On the **Home** tab, in the **Create** group, choose **Create Site System Server**. The Create Site System Server Wizard opens.  

    -   **Existing site system server**: Choose the server in which you want to install the distribution point site system role. When you choose a server, a list of the site system roles that are already installed on the server appears in the results pane.  

         On the **Home** tab, in the **Server** group, choose **Add Site System Role**. The Add Site System Roles Wizard opens.  

3.  On the **General** page, specify the general settings for the site system server. When you add the distribution point to an existing site system server, verify the values that were previously configured.  

4.  On the **System Role Selection** page, choose **Distribution point** from the list of available roles, and then choose **Next**.  

5.  For the subsequent pages of the wizard, see the information in the [Configure a distribution point](#bkmk_configs) section.  

     For example, if you want to install the distribution point as a pull-distribution point, you choose **Enable this distribution point to pull content from other distribution points** and then make the additional configurations that pull-distribution points require.  

6.  After you finish the wizard, the distribution point site role is added to the site system server.  

#### To change a distribution point  

1.  In the Configuration Manager console, choose **Administration** >  **Distribution Points**, and then select the distribution point that you want to configure.  

2.  On the **Home** tab, in the **Properties** group, choose **Properties**.  

3.  Use the information in the [Configure a distribution point](#bkmk_configs) section when you're editing the properties of the distribution point.  

4.  After you make the changes that you want, save your settings and close the distribution point properties.  

##  <a name="bkmk_manage"></a> Manage distribution point groups  
 Distribution point groups provide a logical grouping of distribution points for content distribution. You can use these groups to  manage and monitor content from a central location for distribution points that span multiple sites. Keep the following in mind:

-   You can add one or more distribution points from any site in the  hierarchy to a distribution point group.  

-   You can add a distribution point to more than one distribution point group.  

-   When you distribute content to a distribution point group, Configuration Manager distributes the content to all distribution points that are members of the distribution point group.  

-   If you add a distribution point to the distribution point group after an initial content distribution, Configuration Manager automatically distributes the content to the new distribution point member.  

-   You can associate a collection with a distribution point group. When you distribute content to that collection, Configuration Manager determines which distribution point groups are associated with the collection. The content is then distributed to all distribution points that are members of those distribution point groups.  

    > [!NOTE]  
    >  After you distribute content to a collection, if you then associate the collection with a new distribution point group, you must redistribute the content to the collection before the content is distributed to the new distribution point group.  

#### To create and configure a new distribution point group  

1.  In the Configuration Manager console, choose **Administration** > **Distribution Point Groups**.  

2.  On the **Home** tab, in the **Create** group, choose **Create Group**.  

3.  Enter the name and description for the distribution point group.  

4.  On the **Collections** tab, choose **Add**, select the collections that you want to associate with the distribution point group, and then choose **OK**.  

5.  On the **Members** tab, choose **Add**, select the distribution points that you want to add as members of the distribution point group, and then choose **OK**.  

6.  Choose **OK** to create the distribution point group.  

#### To add distribution points and associate collections with an existing distribution point group  

1.  In the Configuration Manager console, choose **Administration** > **Distribution Point Groups**.  

2.  On the **Home** tab, in the **Properties** group, choose **Properties**.  

3.  On the **Collections** tab, choose **Add** to select the collections that you want to associate with the distribution point group, and then choose **OK**.  

4.  On the **Members** tab, choose **Add** to select the distribution points that you want to add as members of the distribution point group, and then choose **OK**.  

5.  Choose **OK** to save changes to the distribution point group.  

#### To add selected distribution points to a new distribution point group  

1.  In the Configuration Manager console, choose **Administration** > **Distribution Points**, and then select the distribution points that you want to add to the new distribution point group.  

2.  On the **Home** tab, in the **Distribution Point** group, expand **Add Selected Items**, and then choose **Add Selected Items to New Distribution Point Group**.  

3.  Enter the name and description for the distribution point group.  

4.  On the **Collections** tab, choose **Add** to select the collections that you want to associate with the distribution point group, and then choose **OK**.  

5.  On the **Members** tab, verify that you want Configuration Manager to add the listed distribution points as members of the distribution point group. Choose **Add** to add the distribution points, and then choose **OK**.  

6.  Choose **OK** to create the distribution point group.  

#### To add selected distribution points to existing distribution point groups  

1.  In the Configuration Manager console, choose **Administration** > **Distribution Points**, and then select the distribution points that you want to add to the new distribution point group.  

2.  On the **Home** tab, in the **Distribution Point** group, expand **Add Selected Items**, and then choose **Add Selected Items to Existing Distribution Point Groups**.  

3.  In the **Available distribution point groups**, select the distribution point groups to which the selected distribution points are added as members, and then choose **OK**.  

##  <a name="bkmk_configs"></a> Configure a distribution point  
 Individual distribution points support a variety of different configurations. However, not all distribution point types support all configurations. For example, cloud-based distribution points do not support content deployments that are enabled for PXE or multicast. You can find information about specific limitations in the following topics:  

-   [Use a cloud-based distribution point with System Center Configuration Manager](../../../../core/plan-design/hierarchy/use-a-cloud-based-distribution-point.md)  

-   [Use a pull-distribution point with System Center Configuration Manager](/sccm/core/plan-design/hierarchy/use-a-pull-distribution-point)  

The following sections describe the configurations that you can select when you're installing a new distribution point or editing the properties of an existing distribution point.  

### General  
 Configure the general distribution point settings:  

-   **Install and configure IIS if required by Configuration Manager**: Choose this setting to let Configuration Manager install and configure IIS on the server if it is not already installed. IIS must be installed on all distribution points. If IIS is not installed on the server and you do not choose this setting, you must install IIS before the distribution point can be installed successfully.  

    > [!NOTE]  
    >  This option is available only when you're installing a new distribution point.  

- **Enable and configure BranchCache for this distribution point**: Choose this setting to let Configuration Manager configure Windows BranchCache on the distribution point server. For more information about using Windows BranchCache with System Center Configuration Manager, see [BranchCache](/sccm/core/plan-design/configs/support-for-windows-features-and-networks#a-namebkmkbranchcachea-branchcache) in *Support for Windows features and networks in System Center Configuration Manager*.

-   **Configure how client devices communicate with the distribution point**: There are advantages and disadvantages to using HTTP and HTTPS. For more information, see "Security best practices for content management" in [Fundamental concepts for content management in System Center Configuration Manager](../../../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md).  

-   **Allow clients to connect anonymously**: This setting specifies whether the distribution point will allow anonymous connections from Configuration Manager clients to the content library.  

    > [!IMPORTANT]  
    >  Repair of a Windows Installer application can fail on a client when you do not use this setting.  
    >   
    >  When you deploy a Windows Installer application on a Configuration Manager client, Configuration Manager downloads the file to the local cache on the client. The files are eventually removed after the installation finishes.
    >  
    >  The Configuration Manager client updates the Windows Installer source list for the installed Windows Installer applications with the content path for the content library on associated distribution points. Later, if you start the repair action from Add or Remove Programs on a Configuration Manager client, MSIExec attempts to access the content path by using an anonymous user.  
    >   
    >  However, you can install the update described in Microsoft Knowledge Base article [2619572](http://go.microsoft.com/fwlink/?LinkId=279699) and then modify a registry key to change this behavior.  
    >   
    >  After the update is installed on the clients, MSIExec will access the content path by using the logged-on user account when you do not choose the **Allow clients to connect anonymously** setting.  

-   **Create a self-signed certificate or import a public key infrastructure (PKI) client certificate for the distribution point**: The certificate has the following purposes:  

    -   It authenticates the distribution point to a management point before the distribution point sends status messages.  

    -   When you check the **Enable PXE support for clients** box on the **PXE Settings** page, the certificate is sent to computers that perform a PXE boot so that they can connect to a management point during the deployment of the operating system.  

    When all your management points in the site are configured for HTTP, create a self-signed certificate. When your management points are configured for HTTPS, import a PKI client certificate.  

    To import the certificate, browse to a Public Key Cryptography Standard (PKCS #12) file that has a PKI certificate with the following requirements for Configuration Manager:  

    -   Intended use must include client authentication.  

    -   The private key must be enabled to be exported.  

    > [!TIP]  
    >  There are no specific requirements for the certificate subject or subject alternative name (SAN), and you can use the same certificate for multiple distribution points.  

     For more information about the certificate requirements, see [PKI certificate requirements for System Center Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md).  

     For an example deployment of this certificate, see the "Deploying the Client Certificate for Distribution Points" section in [Step-by-step example deployment of the PKI certificates for System Center Configuration Manager: Windows Server 2008 Certification Authority](/sccm/core/plan-design/network/example-deployment-of-pki-certificates).  

-   **Enable this distribution point for prestaged content**: Choose this setting to enable the distribution point for prestaged content. When this setting is selected, you can configure distribution behavior when you distribute content. You can choose to always do one of the following:

 - Prestage the content on the distribution point.
 - Prestage the initial content for the package, but use the normal content distribution process when there are updates to the content.
 - Use the normal content distribution process for the content in the package.  

### Drive settings  

> [!NOTE]  
>  These options are available only when you're installing a new distribution point.  

Specify the drive settings for the distribution point. You can configure up to two disk drives for the content library and two disk drives for the package share. Configuration Manager can use additional drives when the first two reach the configured drive space reserve. The **Drive Settings** page configures the priority for the disk drives and the amount of free disk space that remains on each disk drive.  

-   **Drive space reserve (MB)**: The value that you configure for this setting determines the amount of free space on a drive before Configuration Manager chooses a different drive and continues the copy process to that drive. Content files can span multiple drives.  

-   **Content Locations**: Specify the content locations for the content library and package share. Configuration Manager copies content to the primary content location until the amount of free space reaches the value specified for **Drive space reserve (MB)**. By default, the content locations are set to **Automatic**. The primary content location is set to the disk drive that has the most disk space at installation, and the secondary location is assigned to the disk drive that has the second-most free disk space. When the primary and secondary drives reach the drive space reserve, Configuration Manager selects another available drive with the most free disk space and continues the copy process.  

> [!NOTE]  
>  To prevent Configuration Manager from installing on a specific drive, create an empty file named **no_sms_on_drive.sms** and copy it to the root folder of the drive before you install the distribution point.  

### Pull-distribution point  
When you choose **Enable this distribution point to pull content from other distribution points**, you change the behavior of how that computer gets the content that you distribute to the distribution point. It becomes a pull-distribution point.  

For each pull-distribution point that you configure, you must specify one or more source distribution points from which the pull-distribution point gets the content:  

-   Choose **Add**, and then select one or more of the available distribution points to be source distribution points.  

-   Choose **Remove** to remove the selected distribution point as a source distribution point.  

-   Use the arrow buttons to adjust the order in which the pull-distribution point contacts the source distribution points when the pull-distribution point attempts to transfer content. Distribution points with the lowest value are contacted first.  

### PXE  
Specify whether to enable PXE on the distribution point. When you enable PXE, Configuration Manager installs Windows Deployment Services on the server, if required. Windows Deployment Services is the service that performs the PXE boot to install operating systems. After you finish the wizard to create the distribution point, Configuration Manager installs a provider in Windows Deployment Services that uses the PXE boot functions.  

When you choose **Enable PXE support for clients**, configure the following settings:  

-   **Allow this distribution point to respond to incoming PXE requests**: Specify whether to enable Windows Deployment Services so that it responds to PXE service requests. Use this box to enable and disable the service without removing the PXE functionality from the distribution point.  

-   **Enable unknown computer support**: Specify whether to enable support for computers that Configuration Manager does not manage.  

-   **Require a password when computers use PXE**: To provide additional security for your PXE deployments, specify a strong password.  

-   **User device affinity**: Specify how you want the distribution point to associate users with the destination computer for PXE deployments. Choose one of the following options:  

    -   **Allow user device affinity with auto-approval**: Choose this setting to automatically associate users with the destination computer without waiting for approval.  

    -   **Allow user device affinity pending administrator approval**: Choose this setting to wait for approval from an administrative user before users are associated with the destination computer.  

    -   **Do not allow user device affinity**: Choose this setting to specify that users are not associated with the destination computer.  

     For more information about user device affinity, see [Link users and devices with user device affinity in System Center Configuration Manager](../../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).  

-   **Network interfaces**: Specify that the distribution point responds to PXE requests from all network interfaces or from specific network interfaces. If the distribution point responds to specific network interfaces, you must provide the MAC address for each network interface.  

-   **Specify the PXE server response delay (seconds)**: Specify, in seconds, how long the delay is for the distribution point before it responds to computer requests when multiple PXE-enabled distribution points are used. By default, the Configuration Manager PXE service point responds first to network PXE requests.  

> [!NOTE]  
>  You can use the PXE protocol to start operating system deployments to Configuration Manager client computers. Configuration Manager uses the PXE-enabled distribution point site role to initiate the operating system deployment process. The PXE-enabled distribution point must be configured to:
>
> 1. Respond to PXE boot requests that Configuration Manager clients make on the network.
> 2. Interact with the Configuration Manager infrastructure to determine the appropriate deployment actions to take.  

### Multicast  
Specify whether to enable multicast on the distribution point. When you enable multicast, Configuration Manager installs Windows Deployment Services on the server, if required.  

When you check the **Enable multicast to simultaneously send data to multiple clients** box, configure the following settings:  

-   **Multicast Connection Account**: Specify the account to use when you configure Configuration Manager database connections for multicast.  

-   **Multicast address settings**: Specify the IP addresses for sending data to the destination computers. By default, the IP address is obtained from a DHCP server that is enabled to distribute multicast addresses. Depending on the network environment, you can specify a range of IP addresses from 239.0.0.0 through 239.255.255.255.  

    > [!IMPORTANT]  
    >  The IP addresses that you configure must be accessible by the destination computers that request the operating system image. Verify that routers and firewalls allow for multicast traffic between the destination computer and the site server.  

-   **UDP port range for multicast**: Specify the range of User Datagram Protocol (UDP) ports that are used to send data to the destination computers.  

    > [!IMPORTANT]  
    >  The UDP ports must be accessible by the destination computers that request the operating system image. Verify that routers and firewalls allow for multicast traffic between the destination computer and the site server.  

-   **Client transfer rate**: Select the transfer rate that is used to download data to the destination computers.  

-   **Maximum clients**: Specify the maximum number of destination computers that can download the operating system from this distribution point.  

-   **Enable scheduled multicast**: Specify how Configuration Manager controls when to start deploying operating systems to destination computers. Configure the following options:  

    -   **Session start delay (minutes)**: Specify the number of minutes that Configuration Manager waits before it responds to the first deployment request.  

    -   **Minimum session size (clients)**: Specify how many requests must be received before Configuration Manager starts to deploy the operating system.  

> [!NOTE]  
>  Multicast deployments conserve network bandwidth by simultaneously sending data to multiple Configuration Manager clients instead of sending a copy of the data to each client over a separate connection. For more information about using multicast for operating system deployment, see [Use multicast to deploy Windows over the network with System Center Configuration Manager](../../../../osd/deploy-use/use-multicast-to-deploy-windows-over-the-network.md).  

### Group relationships  

> [!NOTE]  
>  These options are available only when you're editing the properties of a previously installed distribution point.  

Manage the distribution point groups in which this distribution point is a member.  

To add this distribution point as a member to an existing a distribution point group, choose **Add**. Select an existing distribution point group in the list in the **Add to Distribution Point Groups** dialog box, and then choose **OK**.  

To remove this distribution point from a distribution point group, select the distribution point group in the list, and then choose **Remove**.  

### Content  

> [!NOTE]  
>  These options are available only when you're editing the properties of a previously installed distribution point.  

Manage the content that has been distributed to the distribution point. The **Deployment packages** section provides a list of the packages distributed to this distribution point. You can select a package from the list and perform the following actions:  

-   **Validate**: Starts the process to validate the integrity of the content files in the package. To view the results of the content validation process, in the **Monitoring** workspace, expand **Distribution Status**, and then choose the **Content Status** node.  

-   **Redistribute**: Copies all of the content files in the package to the distribution point, and overwrites the existing files. You typically use this action to repair content files in the package.  

-   **Remove**: Removes the content files from the distribution point for the package.  

### Content validation  
Specify whether to set a schedule to validate the integrity of content files on the distribution point. When you enable content validation on a schedule, Configuration Manager starts the process at the scheduled time, and all content on the distribution point is verified. You can also configure the content validation priority. By default, the priority is set to **Lowest**.  

To view the results of the content validation process, in the **Monitoring** workspace, expand **Distribution Status**, and then choose the **Content Status** node. The content for each package type (for example, application, software update package, and boot image) is shown.  

> [!WARNING]  
>  Although you specify the content validation schedule by using the local time for the computer, the Configuration Manager console shows the schedule in UTC.  

### Boundary group  
Manage the boundary groups for which this distribution point is assigned. Plan to add the distribution point to at least one boundary group. During content deployment, clients must be in a boundary group associated with a distribution point to use that distribution point as a source location for content.

Additionally:

- Before version 1610, you can check the **Allow clients to use this site system as a fallback source location for content** box to let clients outside these boundary groups fall back and use the distribution point as a source location for content when no other distribution points are available. For more information about boundary groups, see [Boundary groups for versions 1511, 1602, and 1606](/sccm/core/servers/deploy/configure/boundary-groups-for-1511-1602-and-1606). For preferred distribution points, see [Fundamental concepts for content management in System Center Configuration Manager](../../../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md).

- With version 1610 or later, you configure boundary group *relationships* that define when and to which boundary groups a client can fall back to find content. For more information, see [Boundary groups](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#boundary-groups).


### Schedule  

> [!NOTE]  
>  These options are available only when you're editing the properties of a previously installed distribution point.  

> [!TIP]  
>  This tab is available only when you edit the properties for a distribution point that is remote from the site server computer.  

 Specify whether to configure a schedule that restricts when Configuration Manager can transfer data to the distribution point.  

> [!IMPORTANT]  
>  The schedule is based on the time zone from the sending site, not the distribution point.  

To restrict data, select the time period and then choose one of the following settings for **Availability**:  

-   **Open for all priorities**: Specifies that Configuration Manager sends data to the distribution point with no restrictions.  

-   **Allow medium and high priority**: Specifies that Configuration Manager sends only medium-priority and high-priority data to the distribution point.  

-   **Allow high priority only**: Specifies that Configuration Manager sends only high-priority data to the distribution point.  

-   **Closed**: Specifies that Configuration Manager does not send any data to the distribution point.  

You can restrict data by priority or close the connection for selected time periods.  

### Rate limits  

> [!NOTE]  
>  These options are available only when you're editing the properties of a previously installed distribution point.  

> [!TIP]  
>  This tab is available only when you edit the properties for a distribution point that is remote from the site server computer.  

Specify whether to configure rate limits to control the network bandwidth that is in use when Configuration Manager is transferring content to the distribution point. You can choose from the following options:  

-   **Unlimited when sending to this destination**: This option specifies that Configuration Manager sends content to the distribution point with no rate limit restrictions.  

-   **Pulse mode**: This option specifies the size of the data blocks that are sent to the distribution point. You can also specify a time delay between sending each data block. Use this option when you must send data across a very low-bandwidth network connection to the distribution point. For example, you might have constraints to send 1 KB of data every five seconds, regardless of the speed of the link or its usage at a given time.  

-   **Limited to specified maximum transfer rates by hour**: Specify this setting to have a site send data to a distribution point by using only the percentage of time that you configure. When you use this option, Configuration Manager does not identify the network's available bandwidth, but instead divides the time that it can send data. Then data is sent for a short block of time, which is followed by blocks of time when data is not sent. For example, if the maximum rate is set to **50%**, Configuration Manager transmits data for a period of time followed by an equal period of time when no data is sent. The actual size amount of data, or size of the data block, is not managed. Instead, only the amount of time during which data is sent is managed.  
