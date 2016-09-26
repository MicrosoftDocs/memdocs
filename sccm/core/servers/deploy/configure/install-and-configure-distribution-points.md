---
title: "Install and configure distribution points for System Center Configuration Manager"
ms.custom: na
ms.date: 05/02/2016
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
---
# Install and configure distribution points for System Center Configuration Manager
You install System Center Configuration Manager distribution points to host the content (files and software) you deploy to devices and users. You can also create distribution point groups that simplify how you manage distribution points, and how you distribute content to distribution points.  

 When you **install a new distribution point** (by using the installation Wizard) or **manage the properties of an existing distribution point** (by editing the distribution points properties), you have the opportunity to configure most of the distribution point settings. However, there are a few settings that are only available when either installing or editing, but not both:  

-   **Settings that are only available when installing a distribution point:**  

    -   Allow Configuration Manager to install IIS on the distribution point computer  

    -   Configure drive space settings for the distribution point  

-   **Settings Steps that are only available when editing the properties of a distribution point:**  

    -   Manage distribution point group relationships  

    -   View Content deployed to the distribution point  

    -   Configure Rate limits for data transfers to distribution points  

    -   Configure Schedules for data transfers to distribution points  

##  <a name="bkmk_install"></a> Install a distribution point  
 You must designate a site system server as a distribution point before content can be made available to client computers. You can add the distribution point site role to a new site system server or add the site role to an existing site system server.  

 When you install a new distribution point, you use an installation wizard that walks you through the available settings. Before you start, consider the following:  

-   You must have the following security permissions to create and configure a distribution point:  

    -   **Read** for the **Distribution Point** object  

    -   **Copy to Distribution Point** for the **Distribution Point** object  

    -   **Modify** for the **Site** object  

    -   **Manage Certificates for Operating System Deployment** for the **Site** object  

-   IIS must be installed on the server that will host the distribution point. When you install the site system role, Configuration Manager can install and configure IIS for you.  

Use the following basic procedures to install or modify  a distribution point, and reference the [Distribution point configurations](#bkmk_configs) section of this topic  for details about available configuration options.  

#### To install a distribution point  

1.  In the Configuration Manager console, click **Administration** >  **Site Configuration** > **Servers and Site System Roles**.  

2.  Add the distribution point site system role to a new or existing site system server:  

    -   **New site system server**: On the **Home** tab, in the **Create** group, click **Create Site System Server**. The Create Site System Server Wizard opens.  

    -   **Existing site system server**: Click the server in which you want to install the distribution point site system role. When you click a server, a list of the site system roles that are already installed on the server are displayed in the results pane.  

         On the **Home** tab, in the **Server** group, click **Add Site System Role**. The Add Site System Roles Wizard opens.  

3.  On the **General** page, specify the general settings for the site system server. When you add the distribution point to an existing site system server, verify the values that were previously configured.  

4.  On the **System Role Selection** page, select **Distribution point** from the list of available roles, and then click **Next**.  

5.  For the subsequent pages of the wizard, reference the information in the [Distribution point configurations](#bkmk_configs) section to complete each page of the wizard when prompted.  

     For example, if you want to install the distribution point as a pull-distribution point, you would  select **Enable this distribution point to pull content from other distribution points** and then configure the addition configurations that pull-distribution points require.  

6.  After you complete the wizard, the distribution point site role is added to the site system server.  

#### To modify a distribution point  

1.  In the Configuration Manager console, click **Administration** >  **Distribution Points**, and then select the distribution point that you want to configure.  

2.  On the **Home** tab, in the **Properties** group, click **Properties**.  

3.  Use the information in the [Distribution point configurations](#bkmk_configs) section when editing the properties of the distribution point.  

4.  After making the changes you desire, save your settings and close the distribution point properties.  

##  <a name="bkmk_manage"></a> Manage distribution point groups  
 Distribution point groups provide a logical grouping of distribution points for content distribution. You can use these groups to  manage and monitor content from a central location for distribution points that span multiple sites  

-   You can add one or more distribution points from any site in the  hierarchy to a distribution point group  

-   You can add a distribution point to more than one distribution point group  

-   When you distribute content to a distribution point group, Configuration Manager distributes the content to all distribution points that are members of the distribution point group  

-   If you add a distribution point to the distribution point group after an initial content distribution, Configuration Manager automatically distributes the content to the new distribution point member  

-   You can  associate a collection to a distribution point group. Then, when you distribute content to that collection, Configuration Manager determines the distribution point groups associated with the collection, and then the content is distributed to all distribution points that are members of those distribution point groups  

    > [!NOTE]  
    >  After you distribute content to a collection, if you then associate the collection to a new distribution point group, you must redistribute the content to the collection before the content is distributed to the new distribution point group.  

#### To create and configure a new distribution point group  

1.  In the Configuration Manager console, click **Administration** > **Distribution Point Groups**.  

2.  On the **Home** tab, in the **Create** group, click **Create Group**.  

3.  Enter the name and description for the distribution point group.  

4.  On the **Collections** tab, click **Add**, select the collections that you want to associate with the distribution point group, and then click **OK**.  

5.  On the **Members** tab, click **Add**, select the distribution points that you want to add as members of the distribution point group, and then click **OK**.  

6.  Click **OK** to create the distribution point group.  

#### To add distribution points and associate collections to an existing distribution point group  

1.  In the Configuration Manager console, click **Administration** > **Distribution Point Groups**.  

2.  On the **Home** tab, in the **Properties** group, click **Properties**.  

3.  On the **Collections** tab, click **Add** to select the collections that you want to associate with the distribution point group, and then click **OK**.  

4.  On the **Members** tab, click **Add** to select the distribution points that you want to add as members of the distribution point group, and then click **OK**.  

5.  Click **OK** to save changes to the distribution point group.  

#### To add selected distribution points to a new distribution point group  

1.  In the Configuration Manager console, click **Administration** > **Distribution Points**, and then select the distribution points that you want to add to the new distribution point group.  

2.  On the **Home** tab, in the **Distribution Point** group, expand **Add Selected Items**, and then click **Add Selected Items to New Distribution Point Group**.  

3.  Enter the name and description for the distribution point group.  

4.  On the **Collections** tab, click **Add** to select the collections that you want to associate with the distribution point group, and then click **OK**.  

5.  On the **Members** tab, verify that you want Configuration Manager to add the listed distribution points as members of the distribution point group. Click **Add** to modify the distribution points that you want to add as members of the distribution point group, and then click **OK**.  

6.  Click **OK** to create the distribution point group.  

#### To add selected distribution points to existing distribution point groups  

1.  In the Configuration Manager console, click **Administration** > **Distribution Points**, and then select the distribution points that you want to add to the new distribution point group.  

2.  On the **Home** tab, in the **Distribution Point** group, expand **Add Selected Items**, and then click **Add Selected Items to Existing Distribution Point Groups**.  

3.  In the **Available distribution point groups**, select the distribution point groups to which the selected distribution points are added as members, and then click **OK**.  

##  <a name="bkmk_configs"></a> Distribution point configurations  
 Individual distribution points support a variety of different configurations. However, not all distribution point types support all configurations. For example, cloud-based distribution points do not support content deployments that are enabled for PXE or multicast. You can find information about specific limitation in the following topics:  

-   [Use a cloud-based distribution point with System Center Configuration Manager](../../../../core/plan-design/hierarchy/use-a-cloud-based-distribution-point.md)  

-   [Use a pull-distribution point with System Center Configuration Manager](../Topic/Use%20a%20pull-distribution%20point%20with%20System%20Center%20Configuration%20Manager.md)  

The following sections describe the  configurations you can select when installing a new distribution point  or editing the properties of an existing distribution point:  

### General  
 Configure the general distribution point settings:  

-   **Install and configure IIS if required by Configuration Manager:** Select this setting to let Configuration Manager install and configure Internet Information Services (IIS) on the server if it is not already installed. IIS must be installed on all distribution points. If IIS is not installed on the server and you do not select this setting, you must install IIS before the distribution point can be installed successfully.  

    > [!NOTE]  
    >  This option is only available when installing a new distribution point  

-   **Configure how client devices communicate with the distribution point:** There are advantages and disadvantages for using HTTP and HTTPS. For more information, see [Security best practices for content management](../../../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#BKMK_Security_ContentManagement) in [Fundamental concepts for content management in System Center Configuration Manager](../../../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md).  

-   **Allow clients to connect anonymously:** This setting specifies whether the distribution point will allow anonymous connections from Configuration Manager clients to the content library.  

    > [!IMPORTANT]  
    >  Repair of a Windows Installer application can fail on a client when you do not use this setting.  
    >   
    >  -   When you deploy a Windows Installer application on a Configuration Manager client, Configuration Manager downloads the file to the local cache on the client and the files are eventually removed after the installation completes.  
    > -   The Configuration Manager client updates the Windows Installer source list for the installed Windows Installer applications with the content path for the content library on associated distribution points.  
    > -   Later, if you start the repair action from Add or Remove Programs on a Configuration Manager client, MSIExec attempts to access the content path by using an anonymous user.  
    >   
    >  However, you can install the update described in Microsoft Knowledge Base article [2619572](http://go.microsoft.com/fwlink/?LinkId=279699) and  then modify a registry key to change this behavior.  
    >   
    >  -   After the update is installed on the clients, MSIExec will access the content path by using the logged on user account when you do not select the **Allow clients to connect anonymously** setting  

-   **Create a self-signed certificate or import a public key infrastructure (PKI) client certificate for the distribution point:** The certificate has the following purposes:  

    -   It authenticates the distribution point to a management point before the distribution point sends status messages.  

    -   When you select **Enable PXE support for clients** check box on the **PXE Settings** page, the certificate is sent to computers that perform a PXE boot so that they can connect to a management point during the deployment of the operating system.  

    When all your management points in the site are configured for HTTP, create a self-signed certificate. When your management points are configured for HTTPS, import a PKI client certificate.  

    To import the certificate, browse to a Public Key Cryptography Standard (PKCS #12) file that contains a PKI certificate with the following requirements for Configuration Manager:  

    -   Intended use must include client authentication.  

    -   The private key must be enabled to be exported.  

    > [!TIP]  
    >  There are no specific requirements for the certificate subject or subject alternative name (SAN), and you can use the same certificate for multiple distribution points.  

     For more information about the certificate requirements, see [PKI certificate requirements for System Center Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md).  

     For an example deployment of this certificate, see the [Deploying the Client Certificate for Distribution Points](../Topic/Step-by-step%20example%20deployment%20of%20the%20PKI%20certificates%20for%20System%20Center%20Configuration%20Manager:%20Windows%20Server%202008%20Certification%20Authority.md#BKMK_clientdistributionpoint2008_cm2012) section in the [Step-by-step example deployment of the PKI certificates for System Center Configuration Manager: Windows Server 2008 Certification Authority](../Topic/Step-by-step%20example%20deployment%20of%20the%20PKI%20certificates%20for%20System%20Center%20Configuration%20Manager:%20Windows%20Server%202008%20Certification%20Authority.md) topic.  

-   **Enable this distribution point for prestaged content:** Select this setting to enable the distribution point for prestaged content. When this setting is selected, you can configure distribution behavior when you distribute content. You can choose whether you always want to prestage the content on the distribution point, prestage the initial content for the package, but use the normal content distribution process when there are updates to the content, or always use the normal content distribution process for the content in the package.  

### Drive Settings  

> [!NOTE]  
>  These options are only available when installing a new distribution point  

Specify the drive settings for the distribution point. You can configure up to two disk drives for the content library and two disk drives for the package share, although Configuration Manager can use additional drives when the first two reach the configured drive space reserve. The **Drive Settings** page configures the priority for the disk drives and the amount of free disk space that remains on each disk drive.  

-   **Drive space reserve (MB):** The value that you configure for this setting determines the amount of free space on a drive before Configuration Manager chooses a different drive and continues the copy process to that drive. Content files can span multiple drives.  

-   **Content Locations:** Specify the content locations for the content library and package share. Configuration Manager copies content to the primary content location until the amount of free space reaches the value specified for **Drive space reserve (MB)**. By default, the content locations are set to **Automatic**. The primary content location is set to the disk drive that has the most disk space at installation, and the secondary location is assigned to the disk drive that has the second most free disk space. When the primary and secondary drives reach the drive space reserve, Configuration Manager selects another available drive with the most free disk space and continues the copy process.  

> [!NOTE]  
>  To prevent Configuration Manager from installing on a specific drive, create an empty file named **no_sms_on_drive.sms** and copy it to the root folder of the drive before you install the distribution point.  

### Pull Distribution Point  
When you select **Enable this distribution point to pull content from other distribution points** you change the behavior of how that computer obtains the content that you distribute to the distribution point. It becomes a pull-distribution point.  

For each pull-distribution point you configure, you must specify one or more source distribution points from which the pull-distribution point obtains the content.  

-   Click **Add**, and then select one or more of the available distribution points to be source distribution points.  

-   Click **Remove** to remove the selected distribution point as a source distribution point.  

-   Use the arrow buttons to adjust the order in which the source distribution points are contacted by the pull-distribution point when the pull-distribution point attempts to transfer content. Distribution points with the lowest value are contacted first.  

### PXE  
Specify whether to enable PXE on the distribution point. When you enable PXE, Configuration Manager installs Windows Deployment Services on the server, if required. Windows Deployment Service is the service that performs the PXE boot to install operating systems. After you complete the wizard to create the distribution point, Configuration Manager installs a provider in Windows Deployment Services that uses the PXE boot functions.  

When you select **Enable PXE support for clients**, configure the following settings:  

-   **Allow this distribution point to respond to incoming PXE requests**: Specifies whether to enable Windows Deployment Services so that it responds to PXE service requests. Use this check box to enable and disable the service without removing the PXE functionality from the distribution point.  

-   **Enable unknown computer support**: Specify whether to enable support for computers that are not managed by Configuration Manager.  

-   **Require a password when computers use PXE**: To provide additional security for your PXE deployments, specify a strong password.  

-   **User device affinity**: Specify how you want the distribution point to associate users with the destination computer for PXE deployments. Select one of the following options:  

    -   **Allow user device affinity with auto-approval**: Select this setting to automatically associate users with the destination computer without waiting for approval.  

    -   **Allow user device affinity pending administrator approval**: Select this setting to wait for approval from an administrative user before users are associated with the destination computer.  

    -   **Do not allow user device affinity**: Select this setting to specify that users are not associated with the destination computer.  

     For more information about user device affinity, see [Link users and devices with user device affinity in System Center Configuration Manager](../../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).  

-   **Network interfaces**: Specify that the distribution point responds to PXE requests from all network interfaces or from specific network interfaces. If the distribution point responds to specific network interface, you must provide the MAC address for each network interface.  

-   **Specify the PXE server response delay (seconds)**: Specifies, in seconds, how long the delay is for the distribution point before it responds to computer requests when multiple PXE-enabled distribution points are used. By default, the Configuration Manager PXE service point responds first to network PXE requests.  

> [!NOTE]  
>  You can use the PXE protocol to start operating system deployments to Configuration Manager client computers. Configuration Manager uses the PXE-enabled distribution point site role to initiate the operating system deployment process. The PXE-enabled distribution point must be configured to respond to PXE boot requests that Configuration Manager clients make on the network and then interact with Configuration Manager infrastructure to determine the appropriate deployment actions to take.  

### Multicast  
Specify whether to enable multicast on the distribution point. When you enable multicast, Configuration Manager installs Windows Deployment Services on the server, if required.  

When you select the **Enable multicast to simultaneously send data to multiple clients** check box, configure the following settings:  

-   **Multicast Connection Account**: Specify the account to use when you configure Configuration Manager database connections for multicast.  

-   **Multicast address settings**: Specify the IP addresses used to send data to the destination computers. By default, the IP address is obtained from a DHCP server that is enabled to distribute multicast addresses. Depending on the network environment, you can specify a range of IP addresses between 239.0.0.0 and 239.255.255.255.  

    > [!IMPORTANT]  
    >  The IP addresses that you configure must be accessible by the destination computers that request the operating system image. Verify that routers and firewalls allow for multicast traffic between the destination computer and the site server.  

-   **UDP port range for multicast**: Specify the range of user datagram protocol (UDP) ports that are used to send data to the destination computers.  

    > [!IMPORTANT]  
    >  The UDP ports must be accessible by the destination computers that request the operating system image. Verify that routers and firewalls allow for multicast traffic between the destination computer and the site server.  

-   **Client transfer rate**: Select the transfer rate that is used to download data to the destination computers.  

-   **Maximum clients**: Specify the maximum number of destination computers that can download the operating system from this distribution point.  

-   **Enable scheduled multicast**: Specify how Configuration Manager controls when to start deploying operating systems to destination computers. When selected, configure the following options:  

    -   **Session start delay (minutes)**: Specify the number of minutes that Configuration Manager waits before it responds to the first deployment request.  

    -   **Minimum session size (clients)**: Specify how many requests must be received before Configuration Manager starts to deploy the operating system.  

> [!NOTE]  
>  Multicast deployments conserve network bandwidth by simultaneously sending data to multiple Configuration Manager clients instead of sending a copy of the data to each client over a separate connection. For more information about using multicast for operating system deployment, see [Use multicast to deploy Windows over the network with System Center Configuration Manager](../../../../osd/deploy-use/use-multicast-to-deploy-windows-over-the-network.md).  

### Group Relationships  

> [!NOTE]  
>  These options are only available when editing the properties of a previously installed distribution point  

Manage the distribution point groups in which this distribution point is a member.  

To add this distribution point as a member to an existing a distribution point group, click **Add**. Select an existing distribution point group in the list in the **Add to Distribution Point Groups** dialog box, and then click **OK**.  

To remove this distribution point from a distribution point group, select the distribution point group in the list, and then click **Remove**.  

### Content  

> [!NOTE]  
>  These options are only available when editing the properties of a previously installed distribution point  

Manage the content that has been distributed to the distribution point. The Deployment packages section provides a list of the packages distributed to this distribution point. You can select a package from the list and perform the following actions:  

-   **Validate**: Starts the process to validate the integrity of the content files in the package. To view the results of the content validation process, in the **Monitoring** workspace, expand **Distribution Status**, and then click the **Content Status** node.  

-   **Redistribute**: Copies all of the content files in the package to the distribution point, and overwrites the existing files. You typically use this operation to repair content files in the package.  

-   **Remove**: Removes the content files from the distribution point for the package.  

### Content Validation  
Specify whether to set a schedule to validate the integrity of content files on the distribution point. When you enable content validation on a schedule, Configuration Manager starts the process at the scheduled time, and all content on the distribution point is verified. You can also configure the content validation priority. By default, the priority is set to **Lowest**.  

To view the results of the content validation process, in the **Monitoring** workspace, expand **Distribution Status**, and then click the **Content Status** node. The content for each package type (for example, Application, Software Update Package, and Boot Image) is displayed.  

> [!WARNING]  
>  While you specify the content validation schedule by using the local time for the computer, the schedule displays in the Configuration Manager console by using UTC.  

### Boundary Group  
Manage the boundary groups for which this distribution point is assigned. You can associate boundary groups to a distribution point. During content deployment, clients must be in a boundary group associated with the distribution point to use it as a source location for content. You can select the **Allow clients to use this site system as a fallback source location for content** check box to let clients outside these boundary groups fall back and use the distribution point as a source location for content when no other distribution points are available.  

For more information about preferred distribution points, see [Fundamental concepts for content management in System Center Configuration Manager](../../../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md).  

### Schedule  

> [!NOTE]  
>  These options are only available when editing the properties of a previously installed distribution point  

> [!TIP]  
>  This tab is only available when you edit the properties for a distribution point that is remote from the site server computer.  

 Specify whether to configure a schedule that restricts when Configuration Manager can transfer data to the distribution point.  

> [!IMPORTANT]  
>  The schedule is based on the time zone from the sending site, not the distribution point.  

To restrict data, select the time period and then select one of the following settings for **Availability**:  

-   **Open for all priorities**: Specifies that Configuration Manager sends data to the distribution point with no restrictions.  

-   **Allow medium and high priority**: Specifies that Configuration Manager sends only medium and high priority data to the distribution point.  

-   **Allow high priority only**: Specifies that Configuration Manager sends only high priority data to the distribution point.  

-   **Closed**: Specifies that Configuration Manager does not send any data to the distribution point.  

You can restrict data by priority or close the connection for selected time periods.  

### Rate Limits  

> [!NOTE]  
>  These options are only available when editing the properties of a previously installed distribution point  

> [!TIP]  
>  This tab is only available when you edit the properties for a distribution point that is remote from the site server computer.  

Specify whether to configure rate limits to control the network bandwidth that is in use when transferring content to the distribution point. You can choose from the following options:  

-   **Unlimited when sending to this destination**: Specifies that Configuration Manager sends content to the distribution point with no rate limit restrictions.  

-   **Pulse mode**: Specifies the size of the data blocks that are sent to the distribution point. You can also specify a time delay between sending each data block. Use this option when you must send data across a very low bandwidth network connection to the distribution point. For example, you might have constraints to send 1 KB of data every five seconds, regardless of the speed of the link or its usage at a given time.  

-   **Limited to specified maximum transfer rates by hour**: Specify this setting to have a site send data to a distribution point by using only the percentage of time that you configure. When you use this option, Configuration Manager does not identify the networks available bandwidth, but instead divides the time it can send data into slices of time. Then data is sent for a short block of time, which is followed by blocks of time when data is not sent. For example, if the maximum rate is set to **50%**, Configuration Manager transmits data for a period of time followed by an equal period of time when no data is sent. The actual size amount of data, or size of the data block, is not managed. Instead, only the amount of time during which data is sent is managed.  

