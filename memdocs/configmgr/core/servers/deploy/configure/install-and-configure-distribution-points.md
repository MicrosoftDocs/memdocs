---
title: Manage distribution points
titleSuffix: Configuration Manager
description: Use distribution points to host the content that you deploy to devices and users.
ms.date: 07/15/2021
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: how-to
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: medium
---

# Install and configure distribution points in Configuration Manager

*Applies to: Configuration Manager (current branch)*

Install Configuration Manager distribution points to host the content files that you deploy to devices and users. Create distribution point groups to simplify how you manage distribution points, and how you distribute content to distribution points.

You *install a new distribution point* by using the installation wizard. For more information, see [Install a distribution point](#install-a-distribution-point). To *manage the properties of an existing distribution point*, edit the properties of the distribution point. For more information, see [Configure a distribution point](#bkmk_configs).

Configure most of the distribution point settings with either method. A few settings are available only when you're either installing or editing, but not both:

- Settings that are available only when you're installing a distribution point:

  - **Allow Configuration Manager to install IIS on the distribution point computer**

  - **Configure drive space settings for the distribution point**

- Settings that are available only when you're editing the properties of a distribution point:

  - **Manage distribution point group relationships**

  - **View Content deployed to the distribution point**

  - **Configure Rate limits for data transfers to distribution points**

  - **Configure Schedules for data transfers to distribution points**

## Install a distribution point

Before you can make content available to clients, choose a site system server as a distribution point. Assign each distribution point to at least one [boundary group](boundary-groups-distribution-points.md). Add the distribution point role to a new server, or add it to an existing server.

### Prerequisites

When you install a new distribution point, you use an installation wizard that walks you through the available settings. Before you start, consider the following prerequisites:  

- You must have the following security permissions to create and configure a distribution point:

  - **Read** for the **Distribution Point** object

  - **Copy to Distribution Point** for the **Distribution Point** object

  - **Modify** for the **Site** object

  - **Manage Certificates for Operating System Deployment** for the **Site** object

- Install Internet Information Services (IIS) on the Windows server that hosts the distribution point. Or, when you install the site system role, Configuration Manager can install and configure IIS for you.

> [!TIP]
> To prevent Configuration Manager from installing on a specific drive, create an empty file named **NO_SMS_ON_DRIVE.SMS** and copy it to the root folder of the drive before you install the distribution point.

### Procedure to install a distribution point

Use this procedure to add a new distribution point. To change the configuration of an existing distribution point, see the [Configure a distribution point](#bkmk_configs) section.

Start with the general procedure to [Install site system roles](install-site-system-roles.md). Select the **Distribution point** role on the **System Role Selection** page of the Create Site System Server wizard. This action adds the following pages to the wizard:

- [Distribution point](#bkmk_config-general)
- [Communication](#bkmk_config-comm)
- [Drive Settings](#bkmk_config-drive)
- [Pull Distribution Point](#bkmk_config-pull)
- [PXE Settings](#bkmk_config-pxe)
- [Multicast](#bkmk_config-multicast)
- [Content Validation](#bkmk_config-valid)
- [Boundary Groups](#bkmk_config-boundary)

> [!IMPORTANT]
> The following settings are available only when you're installing a distribution point:
>
> - **Allow Configuration Manager to install IIS on the distribution point computer**
>
> - **Configure drive space settings for the distribution point**

For more information on the pages of the wizard specific to the distribution point role, see the [Configure a distribution point](#bkmk_configs) section. For example, if you want to install the distribution point as a [pull-distribution point](#bkmk_config-pull), choose the option to **Enable this distribution point to pull content from other distribution points**. Then make the other configurations that pull-distribution points require.

After you finish the Create Site System Server wizard, the site adds the distribution point role to the site system server.

> [!NOTE]
> You can use PowerShell to automate the installation of a distribution point. For more information, see [Add-CMDistributionPoint](/powershell/module/configurationmanager/add-cmdistributionpoint).

To help you troubleshoot, review the following log files on the site server:

- distmgr.log
- SMSdpmon.log

For more information, see [Log file reference](../../../plan-design/hierarchy/log-files.md).

## <a name="bkmk_manage"></a> Manage distribution point groups

Distribution point groups provide a logical grouping of distribution points for content distribution. Use these groups to manage and monitor content from a central location for distribution points that span multiple sites. Keep the following point in mind:

- Add one or more distribution points from any site in the hierarchy to a distribution point group.

- Add a distribution point to more than one distribution point group.

- When you distribute content to a distribution point group, Configuration Manager distributes the content to all distribution points that are members of the group.

- If you add a distribution point to the group after an initial content distribution, Configuration Manager automatically distributes the content to the new distribution point member.

- Associate a collection with a distribution point group. When you distribute content to that collection, Configuration Manager determines which groups are associated with the collection. It then distributes the content to all distribution points that are members of those groups.

    > [!NOTE]
    > After you distribute content to a collection, if you then associate the collection with a new distribution point group, you must redistribute the content to the collection before the content is distributed to the new distribution point group.

The next sections list the procedures for the following actions to manage distribution point groups:

- [Create and configure a new distribution point group](#bkmk_dpgroup-create)
- [Modify an existing distribution point group](#bkmk_dpgroup-modify)
- [Add selected distribution points to existing distribution point groups](#bkmk_dpgroup-addexist)

### <a name="bkmk_dpgroup-create"></a> Procedure to create and configure a new distribution point group

1. In the Configuration Manager console, go to the **Administration** workspace, and select the **Distribution Point Groups** node.

2. In the ribbon, select **Create Group**.

3. In the Create New Distribution Point Group window, enter the **Name**, and optionally a **Description** for the group.

4. On the **Members** tab, select **Add**.

5. In the Add Distribution Points window, select one or more distribution points to add as members of the group. Then choose **OK**.

6. If necessary, switch to the **Collections** tab of the Create New Distribution Point Group window, and select **Add**.

7. In the Select Collections window, select the collections to associate with the distribution point group, and then choose **OK**.

8. In the Create New Distribution Point Group window, choose **OK** to create the group.

> [!NOTE]
> You can use PowerShell to automate this process. For more information, see [New-CMDistributionPointGroup](/powershell/module/configurationmanager/new-cmdistributionpointgroup).

#### Create a new group from an existing distribution point

1. In the Configuration Manager console, go to the **Administration** workspace, and select the **Distribution Points** node. Select one or more distribution points to add to a new distribution point group.

2. In the ribbon, select **Add Selected Items**, and then select **Add Selected Items to New Distribution Point Group**.

This process automatically populates the **Members** tab of the Create New Distribution Point Group window with the selected servers.

### <a name="bkmk_dpgroup-modify"></a> Procedure to modify an existing distribution point group

1. In the Configuration Manager console, go to the **Administration** workspace, and select the **Distribution Point Groups** node.

2. Select an existing distribution point group to modify. In the ribbon, select **Properties**.

3. To associate new collections with this group, switch to the **Collections** tab, and choose **Add**. Select the collections, and then choose **OK**.

4. To add new distribution points to this group, switch to the **Members** tab, and choose **Add**. Select the distribution points, and then choose **OK**.

5. Choose **OK** to save changes to the distribution point group.

> [!NOTE]
> You can use PowerShell to automate this process. For more information, see [Set-CMDistributionPointGroup](/powershell/module/configurationmanager/set-cmdistributionpointgroup).

### <a name="bkmk_dpgroup-addexist"></a> Procedure to add selected distribution points to existing distribution point groups

1. In the Configuration Manager console, go to the **Administration** workspace, and select the **Distribution Points** node. Select one or more distribution points to add to an existing group.

2. In the ribbon, select **Add Selected Items**, and then select **Add Selected Items to Existing Distribution Point Groups**.

3. In the **Available distribution point groups**, select the groups to which the selected distribution points are added as members. Then choose **OK**.

> [!NOTE]
> You can use PowerShell to automate this process. For more information, see [Add-CMDistributionPointToGroup](/powershell/module/configurationmanager/add-cmdistributionpointtogroup).

## <a name="bkmk_reassign"></a> Reassign a distribution point

<!-- 1306937 -->

Many customers have large Configuration Manager infrastructures, and are reducing primary or secondary sites to simplify their environment. They still need to keep distribution points at branch office locations to serve content to managed clients. These distribution points often contain multiple terabytes or more of content. This content is costly for time and network bandwidth to distribute to these remote servers.

This feature lets you reassign a distribution point to another primary site without redistributing the content. The distribution point's current site can be either a primary or secondary site.<!-- SCCMDocs #1677, MEMDocs #1356--> This action updates the site system assignment while persisting all of the content on the server. If you need to reassign multiple distribution points, first do this action on a single distribution point. Then continue with other servers one at a time.

> [!IMPORTANT]
> The target server can only host the distribution point role. If the site system server hosts another Configuration Manager server role, such as the state migration point, you can't reassign the distribution point. You can't reassign a cloud management gateway.

Before reassigning a distribution point, add the computer account of the destination site server to the local Administrator group on the target distribution point server.

Follow these steps to reassign a distribution point:

1. In the Configuration Manager console, connect to the central administration site.

2. Go to the **Administration** workspace, and select the **Distribution Points** node.

3. Right-click the target distribution point, and select **Reassign Distribution Point**.

4. Select the target site server and site code to which you want to reassign this distribution point.

Monitor the reassignment similarly as when you add a new role. The simplest method is to refresh the console view after several minutes. Add the site code column to the view. This value changes when Configuration Manager reassigns the server. If you try to do another action on the target server before you refresh the console view, an "object not found" error occurs. Ensure the process is complete and refresh the console view before starting any other actions on the server.

After reassigning a distribution point, refresh the server's certificate. The new site server needs to re-encrypt this certificate using its public key and store it in the site database. For more information, see the **Create a self-signed certificate or import a public key infrastructure (PKI) client certificate for the distribution point** setting on the [General](#bkmk_config-general) tab of the distribution point properties.

- For PKI certificates, you don't need to create a new certificate. Import the same .PFX and enter the password.

- For self-signed certificates, adjust the expiration date or time to update it.

- If you don't refresh the certificate, the distribution point still serves content, but the following functions fail:

  - Content validation messages (the distmgr.log shows that it can't decrypt the certificate)

  - PXE support for clients

### Tips

- Do this action from the central administration site. This practice helps with replication to the primary sites.

- Don't distribute content to the target server and then attempt to reassign it. Distribute content tasks that are in progress may fail during the reassignment process, but it retries per normal.

- If the server is also a Configuration Manager client, make sure to also reassign the client to the new primary site. This step is especially critical for pull-distribution points, which use client components to download content.

- This process removes the distribution point from the old site's default boundary group. You need to manually add it to the new site's default boundary group, if necessary. All other boundary group assignments remain the same.

> [!NOTE]
> You can use PowerShell to automate this process. For more information, see the **ReassignSiteCode** parameter of the [Set-CMDistributionPoint](/powershell/module/configurationmanager/set-cmdistributionpoint#example-3--reassign-a-distribution-point-to-a-new-site) cmdlet.

## <a name="bkmk_maint"></a> Maintenance mode

<!--3555754-->

You can set a distribution point in maintenance mode. Enable maintenance mode when you're installing software updates, or making hardware changes to the server.

While the distribution point is in maintenance mode, it has the following behaviors:

- The site doesn't distribute any content to it.

- Management points don't return the location of this distribution point to clients.

- When you update the site, a distribution point in maintenance mode still updates.

- The distribution point properties are read-only. For example, you can't change the certificate or add boundary groups.

- Any scheduled task, like content validation, still runs on the same schedule.

Be careful about enabling maintenance mode on more than one distribution point. This action may cause a performance impact to your other distribution points. Depending upon your boundary group configurations, clients may have increased download times or be unable to download content.

Maintenance mode shouldn't be a long-term state for any distribution point. For any actions with a long duration, consider first removing the distribution point role.

> [!NOTE]
> While a distribution point is in maintenance mode, don't do the following actions:<!-- SCCMDocs-pr #4699 -->
>
> - Remove role
> - Reassign distribution point

### Enable maintenance mode

To put a distribution point in maintenance mode, your user account requires the **Modify** permission on the **Site** class. For example, the **Infrastructure Administrator** and **Full Administrator** built-in roles have this permission.<!-- SCCMDocs-pr issue #3407 -->

1. In the Configuration Manager console, go to the **Administration** workspace.

2. Select the **Distribution Points** node.

3. Select the target distribution point, and choose **Enable maintenance mode** from the ribbon.

To view the current state of the distribution points, add the "Maintenance mode" column to the **Distribution Points** node in the console.

For more information on automating this process with the Configuration Manager SDK, see [SetDPMaintenanceMode method in class SMS_DistributionPointInfo](../../../../develop/reference/core/servers/configure/setdpmaintenancemode-method-in-class-sms-distributionpointinfo.md).

## <a name="bkmk_configs"></a> Configure a distribution point

Individual distribution points support different kinds of configurations. However, not all distribution point types support all configurations. For example, cloud management gateways don't support PXE- or multicast-enabled deployments. For more information about specific limitations, see the following articles:

- [Supported configurations for cloud management gateway](../../../clients/manage/cmg/supported-configurations.md)

- [Use a pull-distribution point](../../../plan-design/hierarchy/use-a-pull-distribution-point.md)

The following sections describe the distribution point configurations when you're [installing a new one](#procedure-to-install-a-distribution-point) or [editing an existing one](#bkmk_change-procedure):

- [General settings](#bkmk_config-general)
- [Communication](#bkmk_config-comm)
- [Drive Settings](#bkmk_config-drive)
- [Firewall Settings](#bkmk_firewall)
- [Pull Distribution Point](#bkmk_config-pull)
- [PXE Settings](#bkmk_config-pxe)
- [Multicast](#bkmk_config-multicast)
- [Content Validation](#bkmk_config-valid)
- [Boundary Groups](#bkmk_config-boundary)

### <a name="bkmk_change-procedure"></a> Procedure to change a distribution point

1. In the Configuration Manager console, go to the **Administration** workspace, and select the **Distribution Points** node.

2. Select the distribution point to configure. In the ribbon, choose **Properties**.

3. Use the information in the following sections when you're editing the properties of the distribution point.

4. After you make the changes that you want, select **OK** to save your settings and close the distribution point properties.

> [!NOTE]
> You can use PowerShell to automate this process. For more information, see [Set-CMDistributionPoint](/powershell/module/configurationmanager/set-cmdistributionpoint).

### <a name="bkmk_config-general"></a> General

The following settings are on the **Distribution point** page of the Create Site System Server wizard, and the **General** tab of the distribution point properties window:

- **Description**: An optional description for this distribution point role.

- **Install and configure IIS if required by Configuration Manager**: If IIS isn't already installed on the server, Configuration Manager installs and configures it. Configuration Manager requires IIS on all distribution points. If you don't choose this setting, and IIS isn't installed on the server, first install IIS before Configuration Manager can successfully install the distribution point.

    > [!NOTE]
    > This option is only on the **Distribution point** page of the Create Site System Server wizard. It's available only when you're [installing a new distribution point](#procedure-to-install-a-distribution-point).

- **Enable and configure BranchCache for this distribution point**: Choose this setting to let Configuration Manager configure Windows BranchCache on the distribution point server. For more information, see [BranchCache](../../../plan-design/hierarchy/fundamental-concepts-for-content-management.md#branchcache).

- **Adjust the download speed to use the unused network bandwidth (Windows LEDBAT)**<!--1358112-->: Enable distribution points to use network congestion control. For more information, see [Windows LEDBAT](../../../plan-design/hierarchy/fundamental-concepts-for-content-management.md#windows-ledbat). Minimum requirements for LEDBAT support:<!-- SCCMDocs issue 883 -->

  - Windows Server, version 1709 or later
  - Windows Server 2016 with the following updates:
    - Cumulative update KB4132216, released June 21, 2018, or a later cumulative update.
    - Servicing stack update KB4284833, released May 18, 2018, or a later servicing stack update.
  - Windows Server 2019

- **Enable this distribution point for prestaged content**: This setting enables you to add content to the server before you distribute software. Because the content files are already in the content library, they don't transfer over the network when you distribute the software. For more information, see [Prestaged content](../../../plan-design/hierarchy/manage-network-bandwidth.md#BKMK_PrestagingContent).

- **Enable this distribution point to be used as Microsoft Connected Cache server**: Use this option to install a Microsoft Connected Cache server on your distribution point. By caching this content on-premises, your clients can benefit from the Delivery Optimization feature, but you can help to protect WAN links. For more information, including description of the other settings, see [Microsoft Connected Cache in Configuration Manager](../../../plan-design/hierarchy/microsoft-connected-cache.md).

### <a name="bkmk_config-comm"></a> Communication

The following settings are on the **Communication** page of the Create Site System Server wizard and the distribution point properties window:

- **Configure how client devices communicate with the distribution point**: There are advantages and disadvantages to using **HTTP** or **HTTPS**. For more information, see [Security guidance for content management](../../../plan-design/hierarchy/security-and-privacy-for-content-management.md#security-guidance).

- **Allow clients to connect anonymously**: This setting specifies whether the distribution point allows anonymous connections from Configuration Manager clients to the content library.

<!-- I don't think this applies any more, but commenting instead of removing just in case.
    > [!Important]  
    > If you don't use this setting, apply the changes described in Microsoft Knowledge Base article [2619572](https://support.microsoft.com/help/2619572/) on Windows 7 clients. Otherwise repair of Windows Installer applications can fail.  
    >
    > When you deploy a Windows Installer application, the Configuration Manager client downloads the file to its local cache. The client eventually removes the files after the installation finishes. The Configuration Manager client updates the Windows Installer source list for the application. It sets the content path to the content library on associated distribution points. Later, if you try to repair the application on the device, MSIExec attempts to access the content path by using an anonymous user.  
    >
    > After you install the update on clients and modify the documented registry key, MSIExec accesses the content path by using the signed-in user account.  
 -->

- **Create a self-signed certificate or import a PKI client certificate**: Configuration Manager uses this certificate for the following purposes:

  - It authenticates the distribution point to a management point before the distribution point sends status messages.

  - When you **Enable PXE support for clients** on the **PXE Settings** page, the distribution point sends it to computers that PXE boot. These computers then use it to connect to a management point during the OS deployment process.

    When you configure all your management points in the site for HTTP, select the option to **Create self-signed certificate**. When you configure the management points for HTTPS, use the option to **Import certificate** from PKI.

    To import the certificate, browse to a valid Public Key Cryptography Standard (PKCS #12) file. This PFX or CER file has the PKI certificate with the following requirements for Configuration Manager:

  - The intended use includes client authentication

  - Enable the private key to be exported

    > [!TIP]
    > There are no specific requirements for the certificate subject or subject alternative name (SAN). If necessary, use the same certificate for multiple distribution points.

    For more information about the certificate requirements, see [PKI certificate requirements](../../../plan-design/network/pki-certificate-requirements.md).

    For an example deployment of this certificate, see [Deploying the client certificate for distribution points](../../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_clientdistributionpoint2008_cm2012).

### <a name="bkmk_config-drive"></a> Drive settings

> [!NOTE]
> These options are available only when you're installing a new distribution point.

Specify the drive settings for the distribution point. Configure up to two disk drives for the content library and two disk drives for the package share. Configuration Manager can use other drives when the first two reach the configured drive space reserve. The **Drive Settings** page configures the priority for the disk drives and the amount of free disk space that remains on each disk drive.

- **Drive space reserve (MB)**: This value determines the amount of free space on a drive before Configuration Manager chooses a different drive and continues the copy process to that drive. Content files can span multiple drives.

- **Content locations**: Specify the locations for the content library and package share on this distribution point. By default, all content locations are set to **Automatic**. Configuration Manager copies content to the primary content location until the amount of free space reaches the value specified for **Drive space reserve (MB)**. When you select **Automatic**, Configuration Manager sets the primary content locations to the disk drive with the most disk space at installation. It sets the secondary locations to the disk drive with the second-most free disk space. When the primary and secondary locations reach the drive space reserve, Configuration Manager selects another available drive with the most free disk space to continue the copy process.

> [!TIP]
> To prevent Configuration Manager from installing on a specific drive, create an empty file named **NO_SMS_ON_DRIVE.SMS** and copy it to the root folder of the drive before you install the distribution point.

For more information, see [The content library](../../../plan-design/hierarchy/the-content-library.md).

### <a name="bkmk_firewall"></a> Firewall Settings

The distribution point must have the following inbound rules configured in the Windows firewall:

- Windows Management Instrumentation (DCOM-In)
- Windows Management Instrumentation (WMI-In)

Without these rules, clients will receive error 0x801901F4 in DataTransferService.log when attempting to download content.

### <a name="bkmk_config-pull"></a> Pull distribution point

When you **Enable this distribution point to pull content from other distribution points**, it becomes a pull-distribution point. You change the behavior of how the distribution point gets the content that you distribute to it. For more information, see [Use a pull-distribution point](../../../plan-design/hierarchy/use-a-pull-distribution-point.md).

For each pull-distribution point that you configure, specify one or more source distribution points from which it gets the content:

- Choose **Add**, and then select one or more of the available distribution points to be sources.

- Use the arrow buttons to adjust the priority. When the pull-distribution point attempts to transfer content, the priority is the order in which it contacts the source distribution points. It first contacts distribution points with the lowest value.

### <a name="bkmk_config-pxe"></a> PXE

Specify whether to enable PXE on the distribution point. Use PXE to start OS deployments on clients. For more information on how to use PXE in Configuration Manager, see [Use PXE to deploy Windows over the network](../../../../osd/deploy-use/use-pxe-to-deploy-windows-over-the-network.md).

When you enable PXE, Configuration Manager installs Windows Deployment Services (WDS) on the server, if necessary. WDS is the service that supports PXE boot to install operating systems. After you finish the wizard to create the distribution point, Configuration Manager installs a provider in WDS that uses the PXE boot functions.

You can enable PXE on a distribution point without WDS.

Select the option to **Enable PXE support for clients**, and then configure the following settings:

> [!NOTE]
> Select **Yes** in the **Review Required Ports for PXE** dialog box to confirm that you want to enable PXE. Configuration Manager automatically configures the default ports on Windows firewall. If you use a different firewall, manually configure the ports.
>
> If you install WDS and DHCP on the same server, configure WDS to listen on a different port. By default, DHCP listens on the same port. For more information, see [Considerations when you have WDS and DHCP on the same server](../../../../osd/plan-design/infrastructure-requirements-for-operating-system-deployment.md#considerations-when-you-have-wds-and-dhcp-on-the-same-server).

- **Allow this distribution point to respond to incoming PXE requests**: Specify whether to enable WDS to respond to PXE service requests. Use this setting to enable and disable the service without removing the PXE functionality from the distribution point.

- **Enable unknown computer support**: Specify whether to enable support for computers that Configuration Manager doesn't manage. For more information, see [Prepare for unknown computer deployments](../../../../osd/get-started/prepare-for-unknown-computer-deployments.md).

- **Enable a PXE responder without Windows Deployment Service**: This option enables a PXE responder on the distribution point, which doesn't require WDS. This PXE responder supports IPv6 networks. If you enable this option on a distribution point that's already PXE-enabled, Configuration Manager suspends the WDS service. If you disable this option, but still **Enable PXE support for clients**, then the distribution point enables WDS again.<!--1357580-->

    > [!NOTE]
    > When you enable a PXE responder on a distribution point without Windows Deployment Service, it can be on the same server as the DHCP service. <!--3734270-->

- **Require a password when computers use PXE**: To provide more security for your PXE deployments, specify a strong password.

- **User device affinity**: Specify how you want the distribution point to associate users with the destination computer for PXE deployments. Choose one of the following options:

  - **Allow user device affinity with auto-approval**: Choose this setting to automatically associate users with the destination computer without waiting for approval.

  - **Allow user device affinity pending administrator approval**: Choose this setting to wait for approval from an administrative user before users are associated with the destination computer.

  - **Do not allow user device affinity**: Choose this setting to specify that users aren't associated with the destination computer. This setting is the default.

    For more information about user device affinity, see [Link users and devices with user device affinity](../../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).

- **Network interfaces**: Specify that the distribution point responds to PXE requests from all network interfaces or from specific network interfaces. If the distribution point responds to specific network interfaces, then provide the MAC address for each network interface.

    > [!Note]  
    > When changing the network interface, restart the WDS service to make sure it properly saves the configuration. When using the PXE responder service, restart the **ConfigMgr PXE Responder Service** (SccmPxe).<!--SCCMDocs issue 642-->

- **Specify the PXE server response delay (seconds)**: When you use multiple PXE servers, specify how long this PXE-enabled distribution point should wait before it responds to computer requests. By default, the Configuration Manager PXE-enabled distribution point responds immediately.

### <a name="bkmk_config-multicast"></a> Multicast

Specify whether to enable multicast on the distribution point. Multicast deployments conserve network bandwidth by simultaneously sending data to multiple Configuration Manager clients. Without multicast, the server sends a copy of the data to each client over a separate connection. For more information about using multicast for OS deployment, see [Use multicast to deploy Windows over the network](../../../../osd/deploy-use/use-multicast-to-deploy-windows-over-the-network.md).

When you enable multicast, Configuration Manager installs Windows Deployment Services (WDS) on the server, if necessary.

Select the option to **Enable multicast to simultaneously send data to multiple clients**, and then configure the following settings:

- **Multicast Connection Account**: Specify the account to use when you configure Configuration Manager database connections for multicast. For more information, see the [Multicast connection account](../../../plan-design/hierarchy/accounts.md#multicast-connection-account).

- **Multicast address settings**: Specify the IP addresses for sending data to the destination computers. By default, it obtains the IP address from a DHCP server that's enabled to distribute multicast addresses. Depending on the network environment, you can specify a range of IP addresses from 239.0.0.0 through 239.255.255.255.

    > [!IMPORTANT]
    > The IP addresses that you configure must be accessible by the destination computers that request the OS image. Verify that routers and firewalls allow for multicast traffic between the destination computer and the distribution point.

- **UDP port range for multicast**: Specify the range of UDP ports that are used to send data to the destination computers.

    > [!IMPORTANT]
    > The UDP ports must be accessible by the destination computers that request the OS image. Verify that routers and firewalls allow for multicast traffic between the destination computer and the site server.

- **Maximum clients**: Specify the maximum number of destination computers that can download the OS image from this distribution point.

- **Enable scheduled multicast**: Specify how Configuration Manager controls when to start deploying operating systems to destination computers. Configure the following options:

  - **Session start delay (minutes)**: Specify the number of minutes that Configuration Manager waits before it responds to the first deployment request.

  - **Minimum session size (clients)**: Specify how many requests must be received before Configuration Manager starts to deploy the operating system.

> [!IMPORTANT]
> To enable and configure multicast on the **Multicast** tab of the distribution point properties, the distribution point must use Windows Deployment Service.
>
> - If you **Enable PXE support for clients** and **Enable multicast to simultaneously send data to multiple clients**, then you can't **Enable a PXE responder without Windows Deployment Service**.
>
> - If you **Enable PXE support for clients** and **Enable a PXE responder without Windows Deployment Service**, then you can't **Enable multicast to simultaneously send data to multiple clients**.

### <a name="bkmk_config-group"></a> Group relationships

> [!NOTE]
> These options are available only when you're editing the properties of a previously installed distribution point.

Manage the distribution point groups in which this distribution point is a member.

To add this distribution point as a member to an existing a distribution point group, choose **Add**. In the Add to Distribution Point Groups window, select an existing group, and then choose **OK**.

To remove this distribution point from a distribution point group, select the group in the list, and then choose **Remove**. Removing the distribution point from a distribution point group doesn't remove any content from the distribution point.

### <a name="bkmk_config-content"></a> Content

> [!NOTE]
> These options are available only when you're editing the properties of a previously installed distribution point.

Manage the content that you distributed to the distribution point. Select from the list of deployment packages, and then select one of the following actions:

- **Validate**: Start the process to validate the integrity of the content files for the software. To view the results of the content validation process, in the **Monitoring** workspace, expand **Distribution Status**, and then choose the **Content Status** node. For more information, see [Validate content](deploy-and-manage-content.md#validate-content).

- **Redistribute**: Copies all of the content files for the selected software to the distribution point, and overwrites the existing files. You typically use this action to repair content files. For more information, see [Redistribute content](deploy-and-manage-content.md#redistribute-content).

- **Remove**: Removes the content files for the software from the distribution point. For more information, see [Remove content](deploy-and-manage-content.md#remove-content).

### <a name="bkmk_config-valid"></a> Content validation

Set a schedule to validate the integrity of content files on the distribution point. When you enable content validation on a schedule, Configuration Manager starts the process at the scheduled time. It verifies all content on the distribution point based on the local SMS_PackagesInContLib SCCMDP class. You can also configure the content validation priority. By default, the priority is set to **Lowest**. Increasing the priority might increase the processor and disk utilization on the server during the validation process, but it should complete faster.

To view the results of the content validation process, in the **Monitoring** workspace, expand **Distribution Status**, and then choose the **Content Status** node. It shows the content for each software type, for example, application, software update package, and boot image.

> [!WARNING]
> Although you specify the content validation schedule by using the local time for the computer, the Configuration Manager console shows the schedule in UTC.

For more information, see [Validate content](deploy-and-manage-content.md#validate-content).

### <a name="bkmk_config-boundary"></a> Boundary groups

Manage the boundary groups to which you assign this distribution point. Add the distribution point to at least one boundary group. During content deployment, clients must be in a boundary group associated with a distribution point to use that distribution point as a source location for content.

Configure boundary group *relationships* that define when and to which boundary groups a client can fall back to find content. For more information, see [Boundary groups](boundary-groups.md).

Choose **Add** and select an existing boundary group from the list.

To create a new boundary group for this distribution point, choose **Create**. For more information on how to create and configure a boundary group, see [Procedures for boundary groups](boundary-group-procedures.md).

When you're editing the properties of a previously installed distribution point, manage the option to **Enable for on-demand distribution**. This option allows Configuration Manager to automatically distribute content to this server when a client requests it. For more information, see [On-demand content distribution](../../../plan-design/hierarchy/fundamental-concepts-for-content-management.md#on-demand-content-distribution).

### <a name="bkmk_config-sched"></a> Schedule

> [!NOTE]
> These options are available only when you're editing the properties of a previously installed distribution point.
>
> This tab is available only when you edit the properties for a distribution point that's remote from the site server.

Configure a schedule that restricts when Configuration Manager can transfer data to the distribution point. Restrict data by priority or close the connection for selected time periods.

To restrict data, select the time period in the grid, and then choose one of the following settings for **Availability**:

- **Open for all priorities**: Configuration Manager sends data to the distribution point with no restrictions. This setting is the default for all time periods.

- **Allow medium and high priority**: Configuration Manager sends only medium-priority and high-priority data to the distribution point.

- **Allow high priority only**: Configuration Manager sends only high-priority data to the distribution point.

- **Closed**: Configuration Manager doesn't send any data to the distribution point.

Configure the **Distribution priority** of software on the **Distribution Settings** tab of the software's properties.

> [!IMPORTANT]
> The schedule is based on the time zone from the sending site, not the distribution point.

### <a name="bkmk_config-rate"></a> Rate limits

> [!NOTE]
> These options are available only when you're editing the properties of a previously installed distribution point.
>
> This tab is available only when you edit the properties for a distribution point that's remote from the site server.

Configure rate limits to control the network bandwidth that Configuration Manager uses to transfer content to the distribution point. Choose from the following options:

- **Unlimited when sending to this destination**: Configuration Manager sends content to the distribution point with no rate limit restrictions. This setting is the default.

- **Pulse mode**: This option specifies the size of the data blocks that the site server sends to the distribution point. You can also specify a time delay between sending each data block. Use this option when you must send data across a very low-bandwidth network connection to the distribution point. For example, you have constraints to send 1 KB of data every five seconds, whatever the speed of the link or its usage at a given time.

- **Limited to specified maximum transfer rates by hour**: Specify this setting to have a site send data to a distribution point by using only the percentage of time that you configure. When you use this option, Configuration Manager doesn't identify the network's available bandwidth. Instead it divides the time that it can send data. The server sends data for a short period of time, which is followed by periods of time when data isn't sent. For example, if you set **Limit available bandwidth** to **50%**, Configuration Manager transmits data for a time period followed by an equal period of time when no data is sent. The actual size amount of data, or size of the data block, isn't managed. It only manages the amount of time during which it sends data.
