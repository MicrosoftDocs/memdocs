---
title: Management insights
titleSuffix: Configuration Manager
description: Learn about the management insights functionality available in the Configuration Manager console.
ms.date: 08/11/2021
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
author: mestew
ms.author: mstewart
manager: dougeby
ms.localizationpriority: medium
---

# Management insights in Configuration Manager

*Applies to: Configuration Manager (current branch)*

Management insights in Configuration Manager provide information about the current state of your environment. The information is based on analysis of data from the site database. Insights help you to better understand your environment and take action based on the insight. <!--1353967-->

## Review management insights

To view the insights, your account needs the **Read** permission on the **Site** object.

1. In the Configuration Manager console, go to the **Administration** workspace, expand **Management Insights**, and select **All Insights**.

    > [!NOTE]
    > When you select the **Management Insights** node, it shows the [Management insights dashboard](#bkmk_insights).

1. Open the management insights group name you want to review.

1. In the ribbon, select **Show Insights**.

The following four tabs are available for review:

- **All Rules**: Gives the complete list of insights for the chosen group.

- **Complete**:  Lists insights where no action is needed.

- **In Progress**: Shows insights where some, but not all, prerequisites are complete.

- **Action Needed**: This tab lists insights that need you to take action. Select **More Details** to show specific items where action is needed.

The **Prerequisites** pane lists any required items needed to run the selected insight.

For example, the following screenshot shows an example of the **All Rules** tab for the **Cloud Services** group:

:::image type="content" source="media/management-insights-all-cloud-rules.png" alt-text="Management insights: All rules and prerequisites for Cloud Services group.":::

To see the details, select an insight, and then select **More Details**.

## Operations

The site reevaluates the applicability of the management insights on a weekly schedule. To manually reevaluate an insight, right-click the insight, and select **Re-evaluate**.

The log file for management insights is **SMS_DataEngine.log** on the site server.

<!--1357930-->
Some insights let you take action. Select an insight, select **More Details**, and then if available select **Take action**. Depending upon the insight, this action has one of the following behaviors:

- Automatically navigate in the console to the node where you can take further action. For example, if the management insight recommends changing a client setting, taking action navigates to the **Client Settings** node. Then take further action by modifying the default or a custom client settings object.

- Navigate to a filtered view based on a query. For example, taking action on the empty collections insight shows just these collections in the list of collections. Then take further action, such as deleting a collection or modifying its membership rules.

## <a name="bkmk_insights"></a> Management insights dashboard

<!--1357979-->

Select the **Management Insights** node to display a graphical dashboard. This dashboard displays an overview of the insight states, which makes it easier for you to show your progress.

Use the following filters at the top of the dashboard to refine the view:

- Show Completed
- Optional
- Recommended
- Critical

The dashboard includes the following tiles:  

- **Management insights index**: Tracks overall progress on management insights. The index is a weighted average. Critical insights are worth the most. This index gives the least weight to optional insights.

- **Management insights groups**: Shows percent of insights in each group, honoring the filters. Select a group to drill down to the specific insights in this group.

- **Management insights priority**: Shows percent of insights by priority, honoring the filters.

- **Top 10 applicable insight rules**: A table of insights including priority and state. Use the **Filter** field at the top of the table to match strings in any of the available columns. The dashboard sorts the table in the following order:

  - Status: Action Needed, Completed, Unknown  
  - Priority: Critical, Recommended, Optional  
  - Last Changed: older dates on top  

:::image type="content" source="media/1357979-management-insights-dashboard.png" alt-text="Screenshot of management insights dashboard." lightbox="media/1357979-management-insights-dashboard.png":::

## Groups and insights

Insights are organized into the following management insight groups:

- [Applications](#applications)
- [Cloud services](#cloud-services)
- [Collections](#collections)
- [Configuration Manager Assessment](#configuration-manager-assessment)
- [Optimize for remote workers](#optimize-for-remote-workers)
- [Proactive maintenance](#proactive-maintenance)
- [Security](#security)
- [Simplified management](#simplified-management)
- [Software Center](#software-center)
- [Software updates](#software-updates)
- [Windows 10](#windows-10)

> [!NOTE]
> Your site may not show all of the following groups and insights. Some insights don't appear when you've already configured the site for the recommendation.

### Applications

Insights for your application management.

- **Applications without deployments or references**: Lists the applications in your environment that don't have active deployments or references. References include dependencies, task sequences, and virtual environments. This insight helps you find and delete unused applications to simplify the list of applications displayed in the console. For more information, see [Deploy applications](../../../apps/deploy-use/deploy-applications.md).<!-- B585E3FF-585F-4CE9-AE2C-648A7CA2F143 -->

### Cloud services

Helps you integrate with many cloud services, which enable modern management of your devices.

- **Assess co-management readiness**: Helps you understand what steps are needed to enable co-management. This insight has prerequisites. For more information, see [Co-management overview](../../../comanage/overview.md).<!-- D99F094A-A965-402F-AFE5-EE00CCAF0A12 -->

- **Devices not uploaded to Azure AD**: This insight lists devices that the site hasn't uploaded to Azure Active Directory (Azure AD) because you haven't configured it for HTTPS.<!--6268489--> Configure [Enhanced HTTP](../../plan-design/hierarchy/enhanced-http.md), or enable at least one management point for HTTPS. If you already configured the site for HTTPS communication, this insight doesn't appear.<!-- 609F03D4-D9B4-4D0D-A67F-9E365F6C0DD0 -->

- **Enable cloud management gateway**: The cloud management gateway (CMG) provides a simple way to manage Configuration Manager clients over the internet. By deploying the CMG as a cloud service in Microsoft Azure, you can continue to manage and serve content to clients that roam onto the internet. With CMG, you don't need any additional on-premises infrastructure exposed to the internet. For more information, see [Overview of CMG](../../clients/manage/cmg/overview.md).<!-- 451B9B3A-D86A-4EF1-ACC3-FE6A207886BA -->

- **Enable devices to be hybrid Azure Active Directory joined**: Azure AD-joined devices allow users to sign in with their domain credentials, and make sure devices meet the organization's security and compliance standards. For more information, see [Azure AD hybrid identity design considerations](/azure/active-directory/hybrid/plan-hybrid-identity-design-considerations-overview).<!-- 6DC6B149-8B48-45E9-B189-F1E12A62D994 -->

- **Sites that don't have proper HTTPS configuration**: This insight lists sites in your hierarchy that aren't properly configured for HTTPS. This configuration prevents the site from [synchronizing collection membership results to Azure AD groups](../../clients/manage/collections/create-collections.md#bkmk_aadcollsync). It may cause Azure AD sync to not upload all devices. Management of these clients may not function properly.<!--6268489--> Configure [Enhanced HTTP](../../plan-design/hierarchy/enhanced-http.md), or enable at least one management point for HTTPS. If you already configured the site for HTTPS communication, this insight doesn't appear.<!-- 73884047-3395-430E-B971-F853806D4349 -->

- **Update clients to the latest Windows 10 version**: Windows 10, version 1709 or above improves and modernizes the computing experience of your users. For more information, see [Stay current with Windows as a service](../../understand/configuration-manager-and-windows-as-service.md#windows-as-a-service).<!-- FD2C7B93-E5C6-4DCB-89AF-9EFCFCD01524 -->

### Collections

Insights that help simplify management by cleaning up and reconfiguring collections.

- **Empty Collections**: Lists collections in your environment that have no members. For more information, see [How to manage collections](../../clients/manage/collections/manage-collections.md).<!-- 4266054A-695D-4BCA-8000-27BD32F7C006 -->

<!--3555752-->
- **Collections with no query rules and no direct members**: To simplify the list of collections in your hierarchy, delete these collections.<!-- 3C234964-B3F3-49EE-AA13-048CD2021924 -->

- **Collections with the same re-evaluation start time**: These collections have the same re-evaluation time as other collections. Modify the re-evaluation time so they don't conflict.<!-- A85B79A6-BA81-404F-8DA4-DD7C87582CCD -->

- **Collections with query time over 5 minutes**: Review the query rules for this collection. Consider modifying or deleting the collection.<!-- 6AF42536-BDF4-4535-87C1-535AE1B813DA -->

- The following insights include configurations that potentially cause unnecessary load on the site. Review these collections, then either delete them, or disable collection rule evaluation:

  - **Collections with no query rules and incremental updates enabled**<!-- 6A4845AB-6D2C-4F2A-B7AB-EC77C81FD571 -->

  - **Collections with no query rules and enabled for any schedule**<!-- 219B9C45-BD02-4E7E-A29D-B66094366200 -->

  - **Collections with no query rules and schedule full evaluation selected**<!-- 8A401207-5A7C-4200-A1DB-990A197458FA -->

> [!NOTE]
> For more information on managing collections and collection evaluation, see the following articles:<!-- MEMDocs#967 -->
>
> - [Best practices for collections](../../clients/manage/collections/best-practices-for-collections.md)
> - [Collection evaluation](../../clients/manage/collections/collection-evaluation.md)
> - [How to view collection evaluation](../../clients/manage/collections/collection-evaluation-view.md)

### Configuration Manager Assessment

<!--3607758-->

This group is courtesy of Microsoft Premier Field Engineering. These insights are a sample of the many more checks that Microsoft Premier provides in the [Services Hub](/services-hub/health/getting_started_with_on_demand_assessments).

- **Active Directory Security Group Discovery is configured to run too frequently**: You typically don't need to configure Active Directory Security Group Discovery to occur more frequently than every three hours. A more frequent configuration can have a negative performance impact on Active Directory, the network, and Configuration Manager. Enable incremental synchronization instead of using a full sync schedule. For more information, see [Active Directory group discovery](../deploy/configure/about-discovery-methods.md#bkmk_aboutGroup).<!-- 4E739B65-AEC9-4B1D-8B36-AC6AC4A72022 -->

- **Active Directory System Discovery is configured to run too frequently**: You typically don't need to configure Active Directory System Discovery to occur more frequently than every three hours. A more frequent configuration can have a negative performance impact on Active Directory, the network, and Configuration Manager. Enable incremental synchronization instead of using a full sync schedule. For more information, see [Active Directory system discovery](../deploy/configure/about-discovery-methods.md#bkmk_aboutSystem).<!-- 353CAFBC-AC90-4FD3-B3CF-51D6D9FB376C -->

- **Active Directory User Discovery is configured to run too frequently**: You typically don't need to configure Active Directory User Discovery to occur more frequently than every three hours. A more frequent configuration can have a negative performance impact on Active Directory, the network, and Configuration Manager. Enable incremental synchronization instead of using a full sync schedule. For more information, see [Active Directory user discovery](../deploy/configure/about-discovery-methods.md#bkmk_aboutUser).<!-- 2E742924-7319-4013-B1E1-97DE7EB16B74 -->

- **Collections limited to All Systems or All Users**: Review any collections that use the **All Systems** or **All Users** collections as the limiting collection. Configuration Manager updates the membership of these default collections with data from the Active Directory discovery methods. This data may not be valid information for Configuration Manager clients.<!-- 2382F0C9-A36D-4079-AB37-E3D8EE47E8D4 -->

- **Heartbeat Discovery is disabled**: Heartbeat discovery requires that you install the Configuration Manager client on devices. It's the only discovery method that clients start. All other methods occur on site servers. Heartbeat discovery is essential to keep client activity status current. It makes sure that the site doesn't accidentally age out the resource records from the site database. For more information, see [Heartbeat discovery](../deploy/configure/about-discovery-methods.md#bkmk_aboutHeartbeat).<!-- A3089798-DF4E-490A-AF78-4AF474B214CF -->

- **Long running collection queries enabled for incremental updates**: Collections with a last incremental refresh time higher than 30 seconds use site server and database resources, which could potentially impact overall Configuration Manager performance. For more information, see [Best practices for collections](../../clients/manage/collections/best-practices-for-collections.md).<!-- 21F14C0E-008B-47F3-B1E2-19CF79DC97B4 -->

- **Reduce the number of applications and packages on distribution points**: Microsoft officially supports a combined total of up to 10,000 packages and applications on a distribution point. Exceeding this total can lead to operational problems. For more information, see [Size and scale numbers - distribution point](../../plan-design/configs/size-and-scale-numbers.md#distribution-point).<!-- FFE6906E-932E-4927-8EE0-BA25C37943CB -->

- **Secondary site installation issues**: The installation status of some secondary sites is **Pending** or **Failed**. These states mean that you started the install but it didn't complete successfully. Until the secondary site install finishes, clients may not communicate properly with the primary site. Check the **Monitoring** workspace, and retry the installation. For more information, see [Retry installation of a failed update](post-in-console-updates.md#retry-installation-of-a-failed-update).<!-- ED3F5BDD-2F02-44A4-87F4-BB2C1032D4DE -->

- **Update all sites to the same version**: Use the same version of Configuration Manager in a hierarchy. This configuration makes sure all sites provide the same functionality. Sites of different versions in the same hierarchy introduce interoperability scenarios. Later versions of Configuration Manager include new features and resolve known issues. For more information, see [Interoperability between different versions](../../plan-design/hierarchy/interoperability-between-different-versions.md).<!-- 88C630A5-6D6B-4DDB-95D7-78E12107970D -->

For more information on these insights, see [Remediation steps for Configuration Manager management insights](/services-hub/health/remediation-steps-configmgr).

> [!TIP]
> If you're already a customer of Microsoft Unified or Microsoft Premier, sign in to the [Services Hub](https://serviceshub.microsoft.com/assessments/) for additional on-demand assessments.
>
> For more information about Microsoft Services, see [Support Solutions](https://www.microsoft.com/enterprise/services/support).

### Operating system deployment

<!--6982275-->

Starting in version 2006, the following management insights help you manage the policy size of task sequences. When the size of the task sequence policy exceeds 32 MB, the client fails to process the large policy. The client then fails to run the task sequence deployment.

- **Large task sequences may contribute to exceeding maximum policy size**: If you deploy these task sequences, clients may not be able to process the large policy objects. Reduce the size of the task sequence policy to prevent potential policy processing issues.<!-- D9A15248-832E-4780-8151-ACD1B9E53FE1 -->

- **Total policy size for task sequences exceeds policy limit**: Clients can't process the policy for these task sequences because it's too large. Reduce the size of the task sequence policy to allow the deployment to run on clients.<!-- 6568F6A3-D1D8-4E63-940B-FE44F8349802 -->

For more information, see [Reduce the size of task sequence policy](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md#reduce-the-size-of-task-sequence-policy).

In version 2006, the following insight moved to this group from the **Proactive Maintenance** group:

- **Unused boot images**: Boot images not referenced for PXE boot or task sequence use. For more information, see [Manage boot images](../../../osd/get-started/manage-boot-images.md).<!-- 4C1FBA51-AD56-4CA8-8326-066F65D24F0E -->

### Optimize for remote workers

<!--6982226-->

Starting in version 2006, the following insights help you create better experiences for remote workers and reduce load on your infrastructure:

- **Configure VPN connected clients to prefer cloud based content sources**: To reduce traffic on the VPN, enable the boundary group option to **Prefer cloud based sources over on-premises sources**. This option allows clients to download content from the internet instead of distribution points across the VPN. For more information, see [Boundary group options](../deploy/configure/boundary-group-options.md).<!-- 1BFD7A7A-077C-4E8A-9EAA-4559E41D400A -->

- **Define VPN boundary groups**: Create a VPN boundary and associate it to a boundary group. Associate VPN-specific site systems to the group, and configure the settings for your environment. This insight checks for at least one boundary group with at least one VPN boundary in it. From the properties of this insight, select **Review Actions** to go to the **Boundary Groups** node. For more information, see [VPN boundary type](../deploy/configure/boundaries.md#vpn).<!-- E44BF0CC-0ADA-4B00-A4DF-4005256DF73E -->

- **Disable peer to peer content sharing for VPN connected clients**: To prevent unnecessary peer-to-peer traffic that likely doesn't benefit the remote clients, disable the boundary group option to **Allow peer downloads in this boundary group**. For more information, see [Boundary group options](../deploy/configure/boundary-group-options.md).<!-- 60404B23-96A9-4EE2-B8D6-1F226C2F2F5A -->

### Proactive maintenance

<!--1352184-->
The insights in this group highlight potential configuration issues to avoid through upkeep of Configuration Manager objects.

- **Boundary groups with no assigned site systems**: Without assigned site systems, boundary groups can only be used for site assignment. For more information, see [Configure boundary groups](../deploy/configure/boundary-groups.md).<!-- 01E5A4BC-0E31-494E-A553-2B32C410FA5B -->

- **Boundary groups with no members**: Boundary groups aren't applicable for site assignment or content lookup if they don't have any members. For more information, see [Configure boundary groups](../deploy/configure/boundary-groups.md).<!-- 4f0d37b1-f979-4ba3-b15b-7fe3c915f239 -->

- **Distribution points not serving content to clients**: Distribution points that haven't served content to clients in the past 30 days. This data is based on reports from clients of their download history. For more information, see [Install and configure distribution points](../deploy/configure/install-and-configure-distribution-points.md).<!-- 9A115092-F8D4-4AB7-B846-C09143B9B9B0 -->

- **Enable WSUS Cleanup**: Verifies that you've enabled the option to run WSUS cleanup on the properties of the software update point component. This option helps to improve WSUS performance. For more information, see [Software update maintenance](../../../sum/deploy-use/software-updates-maintenance.md).<!-- D43080F1-FE98-4F24-94ED-FEB1C2DDEF50 -->

- **Unused configuration items**: Configuration items that aren't part of a configuration baseline and are older than 30 days. For more information, see [Create configuration baselines](../../../compliance/deploy-use/create-configuration-baselines.md).<!-- 0597907B-17D4-4EA5-92E4-CCE692E1468D -->

- **Update Microsoft .NET Framework on site systems**: <!--10402814-->Starting in version 2107, Configuration Manager requires Microsoft .NET Framework version 4.6.2 for site servers, specific site systems, clients, and the console. Before you run setup to install or update the site, first update .NET and restart the system. If possible in your environment, install the latest version of .NET version 4.8. For more information, [Site and site system prerequisites](../../plan-design/configs/site-and-site-system-prerequisites.md#net-version-requirements).

- **Upgrade peer cache sources to the latest version of the Configuration Manager client**:<!--1358008--> Identify clients that serve as a peer cache source but haven't upgraded from a pre-1806 client version. Pre-1806 clients can't be used as a peer cache source for clients that run version 1806 or later. Select **Take action** to open a device view that displays the list of clients.<!-- B51C6733-F9FF-46BC-8F5E-624F2CBED719 -->

> [!TIP]
> In version 2006, the insight for **Unused boot images** moved to the new [OS deployment](#operating-system-deployment) group.

### Security

Insights for improving the security of your infrastructure and devices.

- **NTLM fallback is enabled**:<!--4572953--> This insight detects if you enabled the less secure NTLM authentication fallback method for the site. When using the client push method of installing the Configuration Manager client, the site can require Kerberos mutual authentication. This enhancement helps to secure the communication between the server and the client. For more information, see [How to install clients with client push](../../clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush).<!-- C16C6826-8209-47A9-BA71-14A8C83E4C35 -->

- **Unsupported antimalware client versions**: More than 10% of clients are running versions of System Center Endpoint Protection that aren't supported. For more information, see [Endpoint Protection](../../../protect/deploy-use/endpoint-protection.md).<!-- ACD63321-CF15-4CDD-B1A3-69005887C633 -->

- **Update clients running Windows 7 and Windows Server 2008**: <!--7520646--> The rule shows clients running Windows 7, Windows Server 2008 (non-Azure), and Windows Server 2008 R2 (non-Azure) that are no longer receiving security updates. For more information about updates for these operating systems, see [Extended Security Updates (ESU)](https://support.microsoft.com/help/4497181/lifecycle-faq-extended-security-updates).<!--A22E3D36-5A90-43A5-B6C6-D7D0B7DCF073-->

### Simplified management

Insights that help you simplify the day-to-day management of your environment.

- **Connect the site to the Microsoft cloud for Configuration Manager updates**: This insight makes sure your Configuration Manager service connection point has connected to the Microsoft cloud within the past seven days. This connection is to download content for regular updates. Review DMPDownloader.log and hman.log. For more information, see [Internet access requirements](../../plan-design/network/internet-endpoints.md#updates-and-servicing).<!-- AC662C91-54DF-4B43-B09A-B19D2766144B -->

- **Non-CB Client Versions**: Lists all clients whose versions aren't a current branch (CB) build. For more information, see [Upgrade clients](../../clients/manage/upgrade/upgrade-clients.md).<!-- 450090EA-DF71-428C-AB49-6DEBB85A004C -->

- **Update clients to a supported Windows 10 version**:<!--3897268, 9742262, 9910532--> This insight reports on clients that are running a version of Windows 10 that's no longer supported.<!-- 560669D6-1756-4814-9505-C54BDB4930D0 -->

### Software Center

Insights for managing Software Center.

- **Direct users to Software Center instead of Application Catalog**: Check if users have installed or requested applications from the application catalog in the last 14 days. The primary functionality of application catalog is now included in Software Center. Support for the application catalog roles ended with version 1910. For more information, see [Deprecated features](../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md#deprecated-features).<!-- DB9E65CF-C59C-4B76-B6A0-ADB95D809246 -->

- **Use the new version of Software Center**: The previous version of Software Center is no longer supported. Set up clients to use the new Software Center by enabling the client setting **Use new Software Center** in the **Computer Agent** group. For more information, see [About client settings](../../clients/deploy/about-client-settings.md#use-new-software-center).<!-- A9BCA10D-834F-4F39-89F5-CDCCE8F80C56 -->

### Software updates

- **Client settings aren't configured to allow clients to download delta content**: Some software updates synchronized in your environment include delta content. Enable the client setting, **Allow clients to download delta content when available**. If you don't enable this setting, when you deploy these updates, client will unnecessarily download more content than they require. For more information, see [Client settings - Software updates](../../clients/deploy/about-client-settings.md#software-updates).<!-- 3E2E9E10-1CDC-47E3-BFC9-3A46AB7FE1BD -->

- **Enable the software updates product category 'Windows 10, version 1903 and later'**: There's a new software updates product category for Windows 10, version 1903 and later. If you synchronize Windows 10 updates, and have Windows 10, version 1903 or later clients, select the **Windows 10, version 1903 and later** product category in the software update point component properties. For more information, see[Configure classifications and products to synchronize](../../../sum/get-started/configure-classifications-and-products.md).<!-- 16B1152D-6511-4DC7-824E-539B2597F9B0 -->

- **Configure software update points to use TLS/SSL**:<!--7470529--> Detects if your software update points are [configured to use TLS/SSL](../../../sum/get-started/software-update-point-ssl.md). Configuring Windows Server Update Services (WSUS) servers and their corresponding software update points (SUPs) to use TLS/SSL may reduce the ability of a potential attacker to remotely compromise a client and elevate privileges. This rule was added in Configuration Manager version 2107.<!--F7AC423D-7BAD-4B62-9CC6-26C351960CDF-->

### Windows 10

Insights related to the deployment and servicing of Windows 10. The Windows 10 management insight group is only available when more than half of clients are running Windows 7, Windows 8, or Windows 8.1.

- **Configure Windows diagnostic data and commercial ID key**: To use data from Desktop Analytics, configure devices with a Commercial ID key and enable collection of diagnostic data. Set Windows 10 devices to **Enhanced (Limited)** level or higher. For more information, see [Enable data sharing for Desktop Analytics](../../../desktop-analytics/enable-data-sharing.md).<!-- B224393F-B255-4C80-A1D1-1014BE1DC7D4 -->