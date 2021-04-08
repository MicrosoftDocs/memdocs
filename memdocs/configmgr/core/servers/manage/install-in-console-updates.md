---
title: In-console updates
titleSuffix: Configuration Manager
description: Install updates to Configuration Manager from the Microsoft cloud
ms.date: 04/05/2021
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c14a3607-253b-41fb-8381-ae2d534a9022
author: mestew
ms.author: mstewart
manager: dougeby
---

# Install in-console updates for Configuration Manager

*Applies to: Configuration Manager (current branch)*

Configuration Manager synchronizes with the Microsoft cloud service to get updates. Then install these updates from within the Configuration Manager console.

## Get available updates

The site only downloads updates that apply to your infrastructure and version. This synchronization can be automatic or manual, depending on how you configure the service connection point for your hierarchy:

- In **online mode**, the service connection point automatically connects to the Microsoft cloud service and downloads applicable updates.  

    By default, Configuration Manager checks for new updates every 24 hours. Manually check for updates in the Configuration Manager console. Go to the **Administration** workspace, select the **Updates and Servicing** node, and choose **Check for Updates** in the ribbon.  

- In **offline mode**, the service connection point doesn't connect to the Microsoft cloud service. To download and then import available updates, [use the Service Connection Tool](use-the-service-connection-tool.md).  

> [!NOTE]  
> If necessary, import out-of-band fixes into your console. To do so, use the [update registration tool](use-the-update-registration-tool-to-import-hotfixes.md). These out-of-band fixes supplement the updates you get when you synchronize with the Microsoft cloud service.  

After updates synchronize, view them in the Configuration Manager console. Go to the **Administration** workspace and select the **Updates and Servicing** node.  

- Updates you haven't installed display as **Available**.  

- Updates you've installed display as **Installed**. Only the most recently installed update is shown. To view previously installed updates, select **History** in the ribbon.  

Before you configure the service connection point, understand and plan for its additional uses. The following uses might affect how you configure this site system role:  

- The site uses the service connection point to upload usage information about your site. This information helps the Microsoft cloud service identify the updates that are available for the current version of your infrastructure. For more information, see [Diagnostics and usage data](../../plan-design/diagnostics/diagnostics-and-usage-data.md).  

To better understand what happens when updates are downloaded, see the following flowcharts:  

- [Flowchart - Download updates](download-updates-flowchart.md)  

- [Flowchart - Update replication](update-replication-flowchart.md)  

## Assign permissions to view and manage updates and features

To view updates in the console, a user must have a role-based administration security role that includes the security class **Update packages**. This class grants access to view and manage updates in the Configuration Manager console.

### About the Update packages class

By default, the **Update packages** class (SMS_CM_Updatepackages) is part of the following built-in security roles with the listed permissions:  

- **Full Administrator** with **Modify** and **Read** permissions:  

  - A user with this security role and access to the **All** security scope can view and install updates. The user can also enable features during the installation, and enable individual features after the site updates.  

  - A user with this security role and access to the **Default** security scope can view and install updates. The user can also enable features during the installation, and view features after the site updates. But this user can't enable the features after the site updates.  

- **Read-only Analyst** with **Read** permissions:  

  - A user with this security role and access to the **Default** scope can view updates but not install them. This user can also view features after the site updates, but can't enable them.  

### Permissions required for updates and servicing

- Use an account to which you assign a security role that includes the **Update packages** class with both **Modify** and **Read** permissions.  

- Assign the account to the **Default** scope.  

### Permissions to only view updates

- Use an account to which you assign a security role that includes the **Update packages** class with only the **Read** permission.  

- Assign the account to the **Default** scope.  

### Permissions required to enable features after the site updates

- Use an account to which you assign a security role that includes the **Update packages** class with both **Modify** and **Read** permissions.  

- Assign the account to the **All** scope.  

## <a name="bkmk_beforeinstall"></a> Before you install an in-console update  

Review the following steps before you install an update from within the Configuration Manager console.  

### <a name="bkmk_step1"></a> Step 1: Review the update checklist  

Review the applicable update checklist for actions to take before you start the update:

- [Checklist for installing update 2103](checklist-for-installing-update-2103.md)

- [Checklist for installing update 2010](checklist-for-installing-update-2010.md)

- [Checklist for installing update 2006](checklist-for-installing-update-2006.md)

- [Checklist for installing update 2002](checklist-for-installing-update-2002.md)

- [Checklist for installing update 1910](checklist-for-installing-update-1910.md)  

### <a name="bkmk_step2"></a> Step 2: Run the prerequisite checker before installing an update  

Before you install an update, consider running the prerequisite check for that update. If you run the prerequisite before installing an update:  

- The site replicates update files to other sites before installing the update.  

- When you choose to install the update, the prerequisite check automatically runs again.  

> [!NOTE]  
> When you start a prerequisite check and then view the status, the **Installation** phase appears to be active. However, the site isn't actually installing the update. To run the prerequisite check, the update process extracts the package from the content library. It then puts the package into a staging folder where it can access the current prerequisite checks. When you install an update, this same process runs. This behavior is why the Installation phase shows as **In progress**. Only the *Extract Update package* step is shown in the Installation category.  

Later, when you install the update, you can configure the update to ignore prerequisite check warnings.  

#### To run the prerequisite checker before installing an update  

1. In the Configuration Manager console, go to the **Administration** workspace, and select the **Updates and Servicing** node.  

2. Select the update package for which you want to run the prerequisite check.  

3. Select **Run prerequisite check** in the ribbon.  

    When you run the prerequisite check, content for the update replicates to child sites. View the **distmgr.log** on the site server to confirm that content replicates successfully.  

4. To view the results of the prerequisite check:  

    1. In the Configuration Manager console, go to the **Monitoring** workspace.  

    2. Select the **Updates and Servicing Status** node and look for the prerequisite status.  

    3. For more information, see the **ConfigMgrPrereq.log** on the site server.  

## <a name="bkmk_install"></a> Install in-console updates  

When you're ready to install updates from within the Configuration Manager console, begin with the top-level site of your hierarchy. This site is either the central administration site or a standalone primary site.  

Install the update outside of normal business hours for each site to minimize the effect on business operations. The update installation might include actions like reinstalling site components and site system roles.  

- Child primary sites automatically start the update after the central administration site completes installation of the update. This process is by default and recommended. To control when a primary site installs updates, use [Service windows for site servers](service-windows.md).  

- After the primary parent site update is complete, manually update secondary sites from within the Configuration Manager console. Automatic update of secondary site servers isn't supported.  

- When you use a Configuration Manager console after the site is updated, you're prompted to update the console.  

- After the site server successfully completes installation of an update, it automatically updates all applicable site system roles. However, all distribution points don't reinstall and go offline to update at the same time. Instead, the site server uses the site's content distribution settings to distribute the update to a subset of distribution points at a time. The result is that only some distribution points go offline to install the update. Distribution points that haven't begun to update or that have completed the update remain online and able to provide content to clients.

### <a name="bkmk_overview"></a> Overview of in-console update installation  

#### 1. When the update installation starts

You're presented with the Updates Wizard that displays a list of the product areas that the update applies to.  

- On the **General** page of the wizard, configure **Prerequisite warnings** as necessary:  

  - Prerequisite errors always stop the update installation. Fix errors before you can successfully retry the update installation. For more information, see [Retry installation of a failed update](#bkmk_retry).  

  - Prerequisite warnings can also stop the update installation. Fix warnings before you retry the update installation. For more information, see [Retry installation of a failed update](#bkmk_retry).  

  - **Ignore any prerequisite check warnings and install this update regardless of missing requirements**: Set a condition for the update installation to ignore prerequisite warnings. This option allows the update installation to continue. If you don't select this option, the update installation stops when the process encounters a warning. Unless you've previously run the prerequisite check and fixed prerequisite warnings for a site, don't use this option.  

    In both the **Administration** and **Monitoring** workspaces, the Updates and Servicing node includes a button on the ribbon named **Ignore prerequisite warnings**. This button becomes available when an update package fails to complete installation due to prerequisite check warnings. For example, you install an update without using the option to ignore prerequisite warnings (from within the Updates Wizard). The update installation stops with a state of prerequisite warning but no errors. Later, you select **Ignore prerequisite warnings** in the ribbon. This action triggers an automatic continuation of that update installation, which ignores prerequisite warnings. When you use this option, the update installation automatically continues after a few minutes.  

- When an update applies to the Configuration Manager client, choose to test the client update with a limited set of clients. For more information, see [How to test client upgrades in a pre-production collection](../../clients/manage/upgrade/test-client-upgrades.md).  

#### 2. During the update installation

As part of the update installation, Configuration Manager does the following actions:  

- Reinstalls any affected components, like site system roles or the Configuration Manager console.  

- Manages updates to clients based on the selections that you made for client piloting, and for [automatic client upgrades](../../clients/manage/upgrade/upgrade-clients-for-windows-computers.md#bkmk_autoupdate).  

- Site system servers generally don't need to restart as part of the update. If a role uses .NET, and the package updates that prerequisite component, then the site system may restart.  

> [!TIP]  
> When you install Configuration Manager updates, the site also updates the CD.Latest folder. For more information, see [The CD.Latest folder](the-cd.latest-folder.md).  

#### 3. Monitor the progress of updates as they install

Use the following steps to monitor progress:  

- In the Configuration Manager console, go to the **Administration** workspace, and select the **Updates and Servicing** node. This node shows the installation status for all update packages.  

- In the Configuration Manager console, go to the **Monitoring** workspace, and select the **Updates and Servicing Status** node. This node shows the installation status of only the current update package that the site is installing.  

    The update installation is divided into several phases for easier monitoring. For each of the following phases, additional details in the installation status include which log file to view for more information:  

  - **Download**: This phase applies only to the top-level site with the service connection point.

  - **Replication**

  - **Prerequisites Check**

  - **Installation**

  - **Post Installation**: For more information, see [post installation tasks](#post-installation-tasks).  

- View the **CMUpdate.log** file in `<ConfigMgr_Installation_Directory>\Logs` on the site server.  

>[!NOTE]
> During the **Installation** phase, you can see the state of the **Upgrade ConfigMgr database** task.
>
> - If the database upgrade is blocked, then you'll be given the warning **In progress, needs attention**.
>   - The cmupdate.log will log the program name and sessionid from SQL Server that is blocking the database upgrade.
> - When the database upgrade is no longer blocked, the status will be reset to **In progress** or **Complete**.
>   - When the database upgrade is blocked, a check is done every 5 minutes to see if it's still blocked.

#### 4. When the update installation completes

After the first site update completes installation:  

- Child primary sites install the update automatically. No further action is required.  

- Manually update secondary sites from within the Configuration Manager console. For more information, see [start the update installation at a secondary site](#bkmk_secondary).  

- Until all sites in your hierarchy update to the new version, your hierarchy operates in a mixed version mode. For more information, see [Interoperability between different versions](../../plan-design/hierarchy/interoperability-between-different-versions.md).  

#### 5. Update Configuration Manager consoles

After a central administration site or primary site updates, each Configuration Manager console that connects to the site must also update. You're prompted to update a console:  

- When you open the console  

- When you go to a new node in an open console  

Update the console right away after the site updates.  

After the console update completes, verify the console and site versions are correct. Go to **About Configuration Manager** at the top-left corner of the console.  

> [!Note]  
> The console version is slightly different from the site version. The minor version of the console corresponds to the Configuration Manager release version. For example, in Configuration Manager version 1802 the initial site version is 5.0.8634.1000, and the initial console version is 5.**1802**.1082.1700. The build (1082) and revision (1700) numbers may change with future hotfixes.

### <a name="bkmk_toptier"></a> To start the update installation at the top-level site  

At the top-level site of your hierarchy, in the Configuration Manager console, go to the **Administration** workspace, and select the **Updates and Servicing** node. Select an update with the state of **Available**, and then choose **Install Update Pack** in the ribbon.  

### <a name="bkmk_secondary"></a> To start the update installation at a secondary site  

After a secondary site's parent primary site updates, update the secondary site from within the Configuration Manager console. To do so, you use the **Upgrade Secondary Site Wizard**.  

1. In the Configuration Manager console, go to the **Administration** workspace, expand **Site Configuration**, and select the **Sites** node. Select the secondary site you want to update, and then choose **Upgrade** in the ribbon.  

2. Select **Yes** to start the update of the secondary site.  

To monitor the update installation on a secondary site, select the secondary site, and choose **Show Install Status** in the ribbon. Also add the **Version** column to the Sites node so that you can view the version of each secondary site.  

In some instances, the status in the console doesn't refresh or suggests the update has failed. After a secondary site successfully updates, use the **Retry installation** option. This option doesn't reinstall the update for a secondary site that successfully installed the update, but forces the console to update the status.

### Post-installation tasks

When a site installs an update, there are several tasks that can't start until after the update completes installation on the site server. This list includes the post-installation tasks that are critical for site and hierarchy operations. Because they're critical, they're actively monitored. Additional tasks that aren't directly monitored include the reinstallation of site system roles. To view the status of the critical post-installation tasks, select the **Post Installation** task while monitoring the update installation for a site.

Not all tasks complete immediately. Some tasks don't start until each site completes installation of the update. New functionality you might expect can be delayed until these tasks complete. Turning on new features doesn't start until all sites complete update installation, so new features might not be visible for some time.

The post installation tasks include:

- **Installing SMS_EXECUTIVE service**

  - Critical service that runs on the site server.
  - Reinstallation of this service should complete quickly.

- **Installing SMS_DATABASE_NOTIFICATION_MONITOR component**

  - Critical site component thread of SMS_EXECUTIVE service.
  - Reinstallation of this service should complete quickly.

- **Installing SMS_HIERARCHY_MANAGER component**

  - Critical site component that runs on the site server.
  - Responsible for reinstalling roles on site system servers. Status for individual site system role reinstallation doesn't display.
  - Reinstallation of this service should complete quickly.

    > [!Note]
    > Some Configuration Manager site roles share the client framework. For example, the management point and pull distribution point. When these roles update, the client version on these servers updates at the same time. For more information, see [How to upgrade clients](../../clients/manage/upgrade/upgrade-clients-for-windows-computers.md).

- **Installing SMS_REPLICATION_CONFIGURATION_MONITOR component**

  - Critical site component that runs on the site server.
  - Reinstallation of this service should complete quickly.

- **Installing SMS_POLICY_PROVIDER component**

  - Critical site component that runs only on primary sites.
  - Reinstallation of this service should complete quickly.

- **Monitoring replication initialization**

  - This task only displays at the central administration site and child primary sites.
  - Dependent on the SMS_REPLICATION_CONFIGURATION_MONITOR.
  - Should complete quickly.

- **Updating Configuration Manager Client Preproduction Package**

  - This task displays even when client preproduction (also called client piloting) isn't enabled for use.
  - Doesn't start until all sites in the hierarchy finish installing the update.

- **Updating Client folder on Site Server**

  - This task doesn't display if you use the client in preproduction.  
  - Should complete quickly.

- **Updating Configuration Manager Client Package**

  - This task doesn't display if you use the client in preproduction.  
  - Finishes only after all sites install the update.  

- **Turning on Features**

  - This task displays only at the top-tier site of the hierarchy.
  - Doesn't start until all sites in the hierarchy finish installing the update.
  - Individual features aren't displayed.

## <a name="bkmk_retry"></a> Retry installation of a failed update  

When an update fails to install, review the in-console feedback to identify resolutions for warnings and errors. For more details, view the **ConfigMgrPrereq.log** on the site server. Before you retry the installation of an update, you must fix errors, and should fix warnings.  

> [!TIP]  
> If an update has problems downloading or replicating, use the [update reset tool](update-reset-tool.md).  

When you're ready to retry the installation of an update, select the failed update, and then choose an applicable option. The update installation retry behavior depends on the node where you start the retry, and the retry option that you use.  

### Retry installation for the hierarchy

Retry the installation of an update for the entire hierarchy when that update is in one of the following states:  

- Prerequisite checks passed with one or more warnings, and the option to ignore prerequisite check warnings wasn't set in the Update Wizard. (The update's value for **Ignore Prereq Warning** in the **Updates and Servicing** node is **No**.)

- Prerequisite failed

- Installation failed  

- Replication of the content to the site failed

Go to the **Administration** workspace and select the **Updates and Servicing** node. Select the update, and then choose one of the following options:  

- **Retry**: When you **Retry** from **Updates and Servicing**, the update install starts again and automatically ignores prerequisite warnings. If content replication previously failed, content for the update replicates again.  

- **Ignore prerequisite warnings**: If the update install stops because of a warning, you can then choose **Ignore prerequisite warnings**. This action allows the installation of the update to continue after a few minutes, and uses the option to ignore prerequisite warnings.

### Retry installation for the site

Retry the installation of an update at a specific site when that update is in one of the following states:  

- Prerequisite checks passed with one or more warnings, and the option to ignore prerequisite check warnings wasn't set in the Update Wizard. (The updates value for **Ignore Prereq Warning** in the Updates and Servicing node is **No**.)  

- Prerequisite failed

- Installation failed

Go to the **Monitoring** workspace, and select the **Site Servicing Status** node. Select the update, and then choose one of the following options:  

- **Retry**: When you **Retry** from **Site Servicing Status**, you restart the installation of the update at only that site. Unlike running **Retry** from the **Updates and Servicing** node, this retry doesn't ignore prerequisite warnings.  

- **Ignore prerequisite warnings**: If the update install stops because of a warning, you can then select **Ignore prerequisite warnings**. This action allows the installation of the update to continue after a few minutes, and uses the option to ignore prerequisite warnings.

## <a name="bkmk_report"></a> Report setup and upgrade failures to Microsoft
<!--5622909-->
Starting in Configuration Manager version 2010, if the setup or update process fails to complete successfully, you can report the error directly to Microsoft. If a failure occurs, the **Report update error to Microsoft** button is enabled. When you use the button, an interactive wizard opens allowing you to provide more information to us. When running [setup from the media](../../servers/deploy/install/use-the-setup-wizard-to-install-sites.md) rather than the console, you'll also be given the **Report update error to Microsoft** option if setup fails.

> [!IMPORTANT]
> Contact [Microsoft support](https://aka.ms/cmcbsupport) to open a new support request for business impacting issues. Reporting setup and upgrade failures from the console is for providing product feedback on setup errors you may have encountered. Reporting an error doesn't generate a support request.

To report upgrade failures to Microsoft:

1. In the Configuration Manager console, go to **Administration** > **Overview** > **Updates and Servicing**.
1. Select an update then select **Report update error to Microsoft** in the ribbon.
   :::image type="content" source="./media/5622909-report-error.png" alt-text="Report update error to Microsoft button in the ribbon" lightbox="./media/5622909-report-error.png":::
1. Before you submit the feedback, you'll be given options to:
   - Attach additional files
   - Provide your email address if you're willing to be contacted about the error.
1. When you submit feedback, you'll be given a transaction ID for the feedback. A status message is also generated with this information.
   - Message ID 53900 is a successful submission.
   - Message ID 53901 is a failed submission.

## <a name="bkmk_after"></a> After a site installs an update  

After the site updates, review the post-update checklist for the applicable version:  

- [Post-update checklist for version 2103](checklist-for-installing-update-2103.md#post-update-checklist)

- [Post-update checklist for version 2010](checklist-for-installing-update-2010.md#post-update-checklist)

- [Post-update checklist for version 2006](checklist-for-installing-update-2006.md#post-update-checklist)

- [Post-update checklist for version 2002](checklist-for-installing-update-2002.md#post-update-checklist)

- [Post-update checklist for version 1910](checklist-for-installing-update-1910.md#post-update-checklist)  

## <a name="bkmk_options"></a> Enable optional features from updates  

When an update includes one or more optional features, you have the opportunity to enable those features in your hierarchy. Enable features when the update installs, or return to the console later to enable the optional features.

To view available features and their status, in the console go to the **Administration** workspace, expand **Updates and Servicing**, and select the **Features** node.

When a feature isn't optional, it's installed automatically. It doesn't appear in the **Features** node.  

> [!IMPORTANT]
> In a multi-site hierarchy, enable optional or pre-release features only from the central administration site. This behavior ensures there are no conflicts across the hierarchy. <!--507197-->  

When you enable a new feature or pre-release feature, the Configuration Manager hierarchy manager (HMAN) must process the change before that feature becomes available. Processing of the change is often immediate. Depending on the HMAN processing cycle, it can take up to 30 minutes to complete. After the change is processed, restart the console before you can use the feature.

Starting in version 2002,<!--5834830--> when new cloud-based features are available in the Microsoft Endpoint Manager admin center, or other attached cloud services for your on-premises Configuration Manager installation, you can now opt in to these new features in the Configuration Manager console.

### List of optional features

The following features are optional in the latest version of Configuration Manager:<!--505213-->  

<!--Note to include in target articles

> [!NOTE]
> Configuration Manager doesn't enable this optional feature by default. You must enable this feature before using it. For more information, see [Enable optional features from updates](install-in-console-updates.md#bkmk_options).  

-->

- [Orchestration groups](../../../sum/deploy-use/orchestration-groups.md)<!--3098816, 290B66D8-C735-4895-B59A-DD732D84A697-->
- [Task sequence deployment type](../../../apps/get-started/creating-windows-applications.md#bkmk_tsdt) <!-- 3555953, CB0CDFFB-9C6F-4B18-8954-A43A387302A2-->
- [Remove the central administration site](../deploy/install/remove-central-administration-site.md) <!-- 3607277 -->
- [BitLocker management](../../../protect/plan-design/bitlocker-management.md) <!-- 3601034,6DD56E46-C3EC-4E38-A16F-E98644BB6434 -->
- [Application groups](../../../apps/deploy-use/create-app-groups.md) <!--3555907,EE16A1D8-EF1B-4094-845F-AC107E7C621D-->
- [Task sequence debugger](../../../osd/deploy-use/debug-task-sequence.md) <!--3612274,C3F37661-69E4-4D53-A39C-5D02F97E0E71-->
- [Approve application requests for users per device](../../../apps/deploy-use/deploy-applications.md#bkmk_deploy-settings) <!--1357015,4BA987C9-08FC-48E2-BFFE-C9DCF35B496A-->  
- [PFX create](../../../protect/deploy-use/introduction-to-certificate-profiles.md) <!--1321368,CED76B79-929C-4C45-981F-B9BCA6D38A17-->
- [Azure Log Analytics connector](/azure/azure-monitor/platform/collect-sccm) <!--1258052,73A7EC4D-EF22-4EA4-82A9-419C2A8CFC4D-->
- [Windows Defender Exploit Guard policy](../../../protect/deploy-use/create-deploy-exploit-guard-policy.md) <!--1355468,8491D4C8-8484-46B8-BCD6-17DC2CADBAEB-->
- [VPN for Windows 10](../../../protect/deploy-use/vpn-profiles.md) <!--1283610,EDBEBA3D-3A4D-4465-84D9-D71EB811E7F6-->
- [Windows Hello for Business](../../../protect/deploy-use/windows-hello-for-business-settings.md) (previously known as *Passport for Work*) <!--1245704,8BCA2642-3719-4862-A355-9D39C979E1B4-->

> [!TIP]
> For more information on features that require consent to enable, see [pre-release features](pre-release-features.md).  
>
> For more information on features that are only available in the technical preview branch, see [Technical Preview](../../get-started/technical-preview.md).

## <a name="bkmk_prerelease"></a> Use pre-release features from updates

The current branch includes pre-release features for early testing in a production environment. For more information, see [pre-release features](pre-release-features.md).

## <a name="bkmk_faq"></a> Frequently asked questions

### Why don't I see certain updates in my console?

If you can't find a specific update in your console after a successful sync with the Microsoft cloud service, this behavior might be because of one of the following reasons:  

- The update requires a configuration that your infrastructure doesn't use, or your current product version doesn't fulfill a prerequisite for receiving the update.  

    If you think you have the required configurations and prerequisites for a missing update, confirm the service connection point is in online mode. Then, use the **Check for Updates** option in the **Updates and Servicing** node to force a check. If your service connection point is in offline mode, use the service connection tool to manually sync with the cloud service.  

- Your account lacks the correct role-based administration permissions to view updates in the Configuration Manager console. For more information, see [Permissions to manage updates](#assign-permissions-to-view-and-manage-updates-and-features).

### Why did the current branch name change with version 2103?

To better align with other releases within Microsoft Endpoint Manager, starting in the year 2021 the current branch version names will be 2103, 2107, and 2111. They will still release every four months, and release at the same time of the year.
