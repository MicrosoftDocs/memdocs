---
title: Technical Preview 1706
titleSuffix: Configuration Manager
description: Learn about features available in the Technical Preview version 1706 for Configuration Manager.
ms.date: 09/15/2017
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: whats-new
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ROBOTS: NOINDEX
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# Capabilities in Technical Preview 1706 for Configuration Manager

*Applies to: Configuration Manager (technical preview branch)*

This article introduces the features that are available in the Technical Preview for Configuration Manager, version 1706. You can install this version to update and add new capabilities to your Configuration Manager technical preview site. Before installing this version of the technical preview, review [Technical Preview for Configuration Manager](../../core/get-started/technical-preview.md) to become familiar with general requirements and limitations for using a technical preview, how to update between versions, and how to provide feedback about the features in a technical preview.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
- **Issue Name**. Details
    Workaround details.
-->
**Known Issues in this Technical Preview:**

- **Move distribution point** - The options in the console to move a distribution point between sites cannot be used with this release due to the technical preview limit of a single primary site.

- **Device compliance settings** - You might experience opposite behavior when using the two of the new device compliance settings:
  - **Block USB debugging on device**
  - **Block apps from unknown sources**

    For example, if admins set **Block USB debugging on device** to **true**, all devices that don't have USB debugging enabled are marked as non-compliant.

**The following are new features you can try out with this version.**  

<!--  Rough Section Template
##  FEATURE

### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## Improved boundary groups for software update points
<!-- 1324591 -->
This release includes improvements for how software update points work with boundary groups. The following summarizes the new fallback behavior:
- Fallback for software update points now uses a configurable time for fallback to neighbor boundary groups, with a minimum time of 120 minutes.

- Independent of the fallback configuration, a client attempts to reach the last software update point it used for 120 minutes. After failing to reach that server for 120 minutes, the client then checks its pool of available software update points, so it can find a new one.

  - All software update points in the client's current boundary group are added to the client's pool immediately.

  - Because a client tries to use its original server for 120 minutes before seeking a new one, no additional servers are contacted until after two hours have elapsed.

  - If fallback to a neighbor group is configured for the minimum of 120 minutes, software update points from that neighbor boundary group will be part of the client's pool of available servers.

- After failing to reach its original server for two hours, the client switches to a shorter cycle for contacting a new software update point.

  This means if a client fails to connect with a new server, it quickly selects the next server from its pool of available servers and attempts to contact that one.

  - This cycle continues until the client connects to a software update point it can use.
  - Until the client finds a software update point, additional servers are added to pool of available servers when the fallback time for each neighbor boundary group is met.

For more information, see [software update points](../servers/deploy/configure/boundary-groups-software-update-points.md) in the Boundary Groups topic for the Current Branch.


## Site server role high availability
<!-- 1128774 -->
High availability for the site server role is a Configuration Manager based solution to install an additional primary site server in *Passive* mode. The passive mode site server is in addition to your existing primary site server that is in *Active* mode. A passive mode site server is available for immediate use, when needed.

A primary site server in passive mode:
- Uses the same site database as your active site server.
- Receives a copy of the active site servers content library, which is then kept in synch.
- Does not write data to the site database so long as it is in passive mode.
- Does not support installation or removal of optional site system roles so long as it is in passive mode.

To make the passive mode site server your active mode site server, you manually promote it. This switches the active site server to be the passive site server. The site system roles that are available on the original active mode server remain available so long as that computer is accessible. Only the site server role is switched between active and passive mode.

To install a passive mode site server, you use the **Create Site System Server Wizard** to configure a new site server with a Type of **Primary site server** and a Mode of **Passive**. The wizard then runs Configuration Manager Setup on the specified server to install the new site server in passive mode. After installation is complete, the active mode site server keeps the passive mode site server and its content library in sync with changes or configurations that you make to the active site server.

### Prerequisites and limitations
- A single site server in passive mode is supported at each primary site.

- The site server in passive mode  can be on-premises or cloud-based in Azure.

- Both the active mode and passive mode site servers must be in the same domain.

- Both the active mode and passive mode site servers must use the same site database, which must be remote from the computers of each site server.

    - The SQL Server that hosts the database can use a default instance, named instance, SQL Server Always On failover cluster instance, or an availability group.

    - The site server in passive mode is configured to use the same site database as the active mode site server. However, the passive mode site server does not use that database until after it is promoted to active mode.

- The computer that will run the passive mode site server:

    - Must meet the [prerequisites for installing a primary site](/sccm/core/servers/deploy/install/prerequisites-for-installing-sites#primary-sites-and-the-central-administration-site).

    - Installs using source files that match the version of the active mode site server.

    - Cannot have a site system role from any site prior to installing the passive mode site.

- The active and passive mode site server computers can run different operating systems or service pack versions, so long as they both remain supported by your version of Configuration Manager.

- Promotion of the passive mode site server to active mode server is manual. There is no automatic failover.

- Site system roles can be installed only on the site server that is in active mode.

    - A site server in active mode supports all site system roles. You cannot install site system roles on server when it is in passive mode.

    - Site system roles that use a database (like the reporting point) must have that database on a server that is remote from both the active mode and passive mode site servers.

    - The SMS_Provider does not install on the site server in passive mode. Because you must connect to an SMS_Provider for the site to manually promote the passive mode site server to active mode, we recommend [installing at least one additional instance of the provider](../plan-design/hierarchy/plan-for-the-sms-provider.md) on an additional computer.

**Known Issue**:   
With this release, **Status** for the following conditions appear in the console as numerical values instead of readable text:
- 131071 – Site server installation failed
- 720895 – Site server role uninstallation failed
- 851967 – Failover failed

### Add a site server in passive mode
1. In the console go to **Administration** > **Site Configuration** > **Sites** and start the [Add Site System Roles Wizard](../servers/deploy/configure/install-site-system-roles.md). You can also use the **Create Site System Server Wizard**.

2. On the **General** page, specify the server that will host the passive mode site server. The server you specify cannot host any site system roles before installing a site server in passive mode.

3. On the **System Role Selection** page, select only **Primary site server in passive mode**.

4. To complete the wizard, you must provide the following information that is used to run Setup and install the site server role on the specified server:
    - Choose to copy installation files from the active site server to the new passive mode site server, or specify a path to a location that contains the contents of the active site server's **CD.Latest** folder.

    - Specify the same site database server and database name as used by the active mode site server.

5. Configuration Manager then installs the site server in passive mode on the specified server.

For detailed installation status, go to **Administration** > **Site Configuration** > **Sites**.
- The status for the site server in passive mode displays as **Installing**.

- Select the server and then click **Show Status** to open **Site Server Installation Status** for more detailed information.



### Promote the passive mode site server to active mode
When you want to change the passive mode site server to active mode, you do so from the **Nodes** pane in **Administration** > **Site Configuration** > **Sites**. So long as you can access an instance of the SMS_Provider, you can access the site to make this change.
1. In the **Nodes** pane of the Configuration Manager console, select the site server in passive mode, and then from the Ribbon, choose **Promote to active**.

2. The simple **Status** for the server you are promoting displays in the **Nodes** pane as **Promoting**.

3. After the promotion is complete, the **Status** column shows **OK** for both the new *Active* mode site server, and for the new *Passive* mode site server.

4. In **Administration** > **Site Configuration** > **Sites**, the name of the primary site server now displays the name of the new *Active* mode site server.
For detailed status, go to **Monitoring** > **Site Server Status**.
    - The **Mode** column identifies which server is *Active* or *Passive*.

    - While promoting a server from passive mode to active mode, select the site server that you are promoting to active, and then choose **Show Status** from the ribbon. This opens the **Site Server Promotion Status** window that displays additional details about the process.

When a site server in active mode switches over to passive mode, only the site system role is made passive. All other site system roles that are installed on that computer remain active and accessible to clients.


### Daily monitoring
When you have a primary site in passive mode, monitor it daily to ensure it remains in sync with the active mode site server, and ready to use. To do so, go to **Monitoring** > **Site Server Status**. Here you can view both the active mode and passive mode site servers.

The **Summary** tab:
- The **Mode** column identifies which server is Active or Passive.
- The **Status** column lists **OK** when the passive mode server is in sync with the active mode server.
- To view additional details about the state of content synchronization, click **Show status** from the Content Sync State. This opens the Content Library tab where you can try to fix content sync issues.

The **Content Library** tab:
- View the **State** for content that synchronizes from the active site server to the passive mode site server.
- You can select content with a State of **Failed**, and then choose **Sync selected items** from the Ribbon. This action tries to resynchronize that content from the content's source to the passive mode site server. During recovery, the State displays as **In progress**, and when it is in sync, it displays as **Success**.

### Try it out!
Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
- I can install a primary site in passive mode.
- I can use the console to promote the passive mode site server to make it the active mode site server, and confirm the change of status for both site servers.


## Include trust for specific files and folders in a Device Guard policy
<!-- 1324676 -->
In this release, we've added further capabilities to [Device Guard](../../protect/deploy-use/use-device-guard-with-configuration-manager.md) policy management

You can now optionally add trust for specific files for folders in a Device Guard policy. This lets you:

1. Overcome issues with managed installer behaviors
2. Trust line-of-business apps that cannot be deployed with Configuration Manager
3. Trust apps that are included in an operating system deployment image.

### Try it out!

1. While you are creating a Device Guard policy, on the Inclusions tab of the Create Device Guard policy wizard, click **Add**.
2. In the **Add Trusted File or Folder** dialog box, specify information about the file or folder that you want to trust. You can either specify a local file or folder path or connect to a remote device to which you have permission to connect and specify a file or folder path on that device.
3. Complete the wizard.


## Hide task sequence progress
<!-- 1354291 -->
In this release, you can control when task sequence progress is displayed to end users by using a new variable. In your task sequence, use the **Set Task Sequence Variable** step to set the value for the **TSDisableProgressUI** variable to hide or display task sequence progress. You can use the Set Task Sequence Variable step multiple times in a task sequence to change the value for the variable. This lets you hide or display task sequence progress in different sections of the task sequence.

#### To hide task sequence progress
In task sequence editor, use the [Set Task Sequence Variable](../../osd/understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable) step to set the value of the **TSDisableProgressUI** variable to **True** to hide task sequence progress.

#### To display task sequence progress
In task sequence editor, use the [Set Task Sequence Variable](../../osd/understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable) step to set the value of the **TSDisableProgressUI** variable to **False** to display task sequence progress.

## Specify a different content location for install content and uninstall content
<!-- 1097546 -->
In Configuration Manager today, you specify the installation location that contains the setup files for an app. When you specify an install location, this is also used as the uninstall location for the application content.
Based on your feedback, when you want to uninstall a deployed application, and the app content is not on the client computer, then the client will download all of the app setup files again before the application is uninstalled.
To solve this problem, you can now specify both an installation content location and an optional uninstall content location. Additionally, you can choose not to specify an uninstall content location.

### Try it Out!

1. In the deployment type properties of an application, click the **Content** tab.
2. Configure the **Install content location** as normal.
3. For **Uninstall content settings**, choose one of the following:
   - **Same as install content** - The same content location will be used regardless of whether you are installing, or uninstalling the application.
   - **No uninstall content** - Choose this if you don't want to supply an uninstall content location for the application.
   - **Different from install content** - Choose this if you want to specify an uninstall content location that's different from the install content location.
5. If you selected **Different from install content**, browse to, or enter the location of the application content that will be used to uninstall the application.
6. Click **OK** to close the deployment type properties dialog box.


## Accessibility improvements  
<!--1253000 -->
This preview introduces several improvements to the [accessibility features](../understand/accessibility-features.md) in the Configuration Manager console. These include:     

**New keyboard shortcuts to move around the console:**
- Ctrl + M - Sets focus on the main (central) pane.
- Ctrl + T - Sets focus to the top node in the navigation pane. If the focus was already in that pane, the focus is set to the last node you visited.
- Ctrl + I -  Sets focus to the breadcrumb bar, below the ribbon.
- Ctrl + L - Sets focus to the **Search** field, when available.
- Ctrl + D - Sets focus to the details pane, when available.
- Alt – Changes focus in and out of the ribbon.

**General improvements:**
- Improved navigation in the navigation pane when you type the letters of a node name.
- Keyboard navigation through the main view and the ribbon are now circular.
- Keyboard navigation in the details pane is now circular. To return to the previous object or pane, use Ctrl + D, then Shift + TAB.
- After refreshing a Workspace view, the focus is set to the main pane of that workspace.
- Fixed an issue to enable screen readers to announce the names of list items.
- Added accessible names for multiple controls on the page that enables screen readers to announce important information.


## Changes to the Azure Services Wizard to support Upgrade Readiness
<!-- 1353331 -->
Beginning with this release, use the Azure Services Wizard to configure a connection from Configuration Manager to Upgrade Readiness. The use of the wizard simplifies configuration of the connector by using a common wizard for related Azure services.   

Although the method to configure the connection has changed, prerequisites for the connection and how you use Upgrade Readiness remain unchanged.   

### Prerequisites for Upgrade Readiness
The prerequisites for a connection to Upgrade Readiness are unchanged from those detailed for the Current Branch of Configuration Manager. They are repeated here for convenience:  

**Prerequisites**
- In order to add the connection, your Configuration Manager environment must first configure a [service connection point](../servers/deploy/configure/about-the-service-connection-point.md) in an [online mode](../servers/deploy/configure/about-the-service-connection-point.md#bkmk_modes). When you add the connection to your environment, it will also install the Microsoft Monitoring Agent on the machine running this site system role.
- Register Configuration Manager as a "Web Application and/or Web API" management tool, and get the [client ID from this registration](/azure/active-directory/develop/quickstart-register-app).
- Create a client key for the registered management tool in Microsoft Entra ID.
- In the Azure portal, provide the registered web app with permission to access OMS.

> [!IMPORTANT]       
> When configuring permission to access OMS, be sure to choose the **Contributor** role, and assign it permissions to the resource group of the registered app.

After the prerequisites are configured, you are ready to use the Wizard to create the connection.

### Use the Azure Services Wizard to configure Upgrade Readiness
1. In the console, go to **Administration** > **Overview** > **Cloud Services** > **Azure Services**, and then choose **Configure Azure Services** from the **Home** tab of the ribbon, to start the **Azure Services Wizard**.

2. On the **Azure Services** page, select the **Upgrade Readiness Connector**, and then click **Next**.

3. On the **App** page, specify your **Azure environment** (the technical preview supports only the Public Cloud). Then, click **Import** to open the **Import Apps** window.

4. In the **Import Apps** window, specify details for a web app that already exists in your Microsoft Entra ID.
    - Provide a friendly name for the Microsoft Entra tenant Name. Then, specify the Tenant ID, Application Name, Client ID, secret key for the Azure web app, and the App ID URI.
    - Click **Verify**, and if successful, click **OK** to continue.

5.  On the **Configuration** page, specify the subscription, resource group, and Windows Analytics Workspace you want to use with this connection to Upgrade Readiness.  

6. Click **Next** to go to the **Summary** page, and then complete the wizard to create the connection.


## New client settings for cloud services
<!-- 1319883 -->

In this release, we've added two new client settings to Configuration Manager. You'll find these in the **Cloud Services** section.  These settings give you the following capabilities:

- Control which Configuration Manager clients can access a configured cloud management gateway.
- Automatically register Windows 10 domain-joined Configuration Manger clients with Microsoft Entra ID.

These new settings help you accomplish the capabilities described in the [Configuration Manager 1705 Technical Preview](capabilities-in-technical-preview-1705.md#new-capabilities-for-azure-ad-and-cloud-management).

### Before you start

You must have installed and configured Microsoft Entra Connect between your on-premises Active Directory and your Microsoft Entra tenant.

If you remove the connection, devices are not un-registered, but no new devices will register.

### Try it out!

1. Configure the following client settings (found in the Cloud Services) section using the information in [How to configure client settings](../clients/deploy/configure-client-settings.md).
   - **Automatically register new Windows 10 domain joined devices with Microsoft Entra ID** – Set to **Yes** (default), or **No**.
   - **Enable clients to use a cloud management gateway** – Set to **Yes** (default), or **No**.
2. Deploy the client settings to the required collection of devices.

To confirm that the device is joined to Microsoft Entra ID, run the command **dsregcmd.exe /status** in a command prompt window. The **AzureAdjoined** field in the results will show **YES** if the device is Microsoft Entra joined.

## Create and run PowerShell scripts from the Configuration Manager console
<!-- 1236459 -->

In Configuration Manager, you can deploy scripts to client devices using packages and programs. In this technical preview, we've added new functionality that lets you take the following actions:

- Import PowerShell Scripts to Configuration Manager
- Edit the scripts from the Configuration Manager console (for unsigned scripts only)
- Mark scripts as Approved or Denied, to improve security
- Run scripts on collections of Windows client PCs, and on-premises managed Windows PCs. You don't deploy scripts, instead, they are run in near real time on client devices.
- Examine the results returned by the script in the Configuration Manager console.


### Prerequisites

To use scripts, you must be a member of the appropriate Configuration Manager security role.

- **To import, and author scripts** - Your account must have **Create** permissions for **SMS Scripts** in the **Full Administrator** security role.
- **To approve, or deny scripts** - Your account must have **Approve** permissions for **SMS Scripts** in the **Full Administrator** security role.
- **To run scripts** - Your account must have **Run Script** permissions for **Collections** in the **Compliance Settings Manager** security role.

For more information about Configuration Manager security roles, see [Fundamentals of role-based administration](../understand/fundamentals-of-role-based-administration.md).

By default, users cannot approve a script they have authored. Since scripts are powerful, versatile, and can be deployed to many devices, we've introduced a new concept of providing the ability to separate the roles between the person that authors the script and the person that approves the script. This gives additional level of security against running a script without oversight. You can turn off this secondary approval, for ease of testing, particularly during the Technical Preview release.

To allow users to approve their own scripts:

1. In the Configuration Manager console, click **Administration**.
2. In the **Administration** workspace, expand **Site Configuration**, and then click **Sites**.
3. In the list of sites, choose your site and then, on the **Home** tab, in the **Sites** group, click **Hierarchy Settings**.
4. On the **General** tab of the **Hierarchy Settings Properties** dialog box, clear the checkbox **Do not allow script authors to approve their own scripts**.


### Try it out!

#### Import and edit a script

1. In the Configuration Manager console, click **Software Library**.
2. In the **Software Library** workspace, click **Scripts**.
3. On the **Home** tab, in the **Create** group, click **Create Script**.
4. On the **Script** page of the **Create Script** wizard, configure the following:
   - **Script Name** - Enter a name for the script. Although you can create multiple scripts with the same name, this will make it harder for you to find the script you need in the Configuration Manager console.
   - **Script language** - Currently, only **PowerShell** scripts are supported.
   - **Import** - Import a PowerShell script into the console. The script is displayed in the **Script** field.
   - **Clear** - Removes the current script from the **Script** field.
   - **Script** - Displays the currently imported script. You can edit the script in this field as necessary.
5. Complete the wizard. The new script is displayed in the **Script** list with a status of **Waiting for approval**. Before you can run this script on client devices, you must approve it.


#### Approve or deny a script



Before you can run a script, it must be approved. To approve a script:

1. In the Configuration Manager console, click **Software Library**.
2. In the **Software Library** workspace, click **Scripts**.
3. In the **Script** list, choose the script you want to approve or deny and then, on the **Home** tab, in the **Script** group, click **Approve/Deny**.
4. In the **Approve or deny script** dialog box, **Approve**, or **Deny** the script, and optionally enter a comment about your decision. If you deny a script, it cannot be run on client devices.
5. Complete the wizard. In the **Script** list, you'll see the **Approval State** column change depending on the action you took.

#### Run a script

Once a script has been approved, it can be run against a collection you choose.

1. In the Configuration Manager console, click **Assets and Compliance**.
2. In the **Assets and Compliance** workspace, click **Device Collections**.
3. In the **Device Collections** list, click the collection of devices on which you want to run the script.
3. On the **Home** tab, in the **All Systems** group, click **Run Script**.
4. On the **Script** page of the **Run Script** wizard, choose a script from the list. Only approved scripts are shown. Click **Next**, and then complete the wizard.

#### Monitor a script

After you have run a script to client devices, use this procedure to monitor the success of the operation.

1. In the Configuration Manager console, click **Monitoring**.
2. In the **Monitoring** workspace, click **Script Results**.
3. In the **Script Results** list, you view the results for each script you ran on client devices. A script exit code of **0**, generally indicates that the script ran successfully.

## PXE network boot support for IPv6
<!-- 1269793 -->
You can now enable PXE network boot support for IPv6 to start a task sequence operating system deployment. When you use this setting, PXE-enabled distribution points will support both IPv4 and IPv6. This option does not require WDS and will stop WDS if it is present.

#### To enable PXE boot support for IPv6
Use the following procedure to enable the option for IPv6 support for PXE.

1. In the Configuration Manager console, go to **Administration** > **Overview** > **Distribution Points**, and click **Properties** for PXE-enabled distribution points.
2. On the **PXE** tab, select **Support IPv6** to enable IPv6 support for PXE.

## Manage Microsoft Surface driver updates
<!-- 1098490 -->
You can now use Configuration Manager to manage Microsoft Surface driver updates.

### Prerequisites
All software update points must run Windows Server 2016.

### Try it out!
Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
1. Enable Synchronization for Microsoft Surface drivers. Use the procedure in [Configure classification and products](../../sum/get-started/configure-classifications-and-products.md) and select **Include Microsoft Surface drivers and firmware updates** on the **Classifications** tab to enable Surface drivers.
2. [Synchronize the Microsoft Surface drivers](../../sum/get-started/synchronize-software-updates.md).
3. [Deploy synchronized Microsoft Surface drivers](../../sum/deploy-use/deploy-software-updates.md)

## Configure Windows Update for Business deferral policies
<!-- 1290890 -->
You can now configure deferral policies for Windows 10 Feature Updates or Quality Updates for Windows 10 devices managed directly by Windows Update for Business. You can manage the deferral policies in the new **Windows Update for Business Policies** node under **Software Library** > **Windows 10 Servicing**.

### Prerequisites
Windows 10 devices managed by Windows Update for Business must have Internet connectivity.

#### To create a Windows Update for Business deferral policy
1. In **Software Library** > **Windows 10 Servicing** > **Windows Update for Business Policies**
2. On the **Home** tab, in the **Create** group, select **Create Windows Update for Business Policy** to open the Create Windows Update for Business Policy Wizard.
3. On the **General** page, provide a name and description for the policy.
4. On the **Deferral Policies** page, configure whether to defer or pause Feature Updates.    
    Feature Updates are generally new features for Windows. After you configure the **Branch readiness level** setting, you can then define if, and for how long, you would like to defer receiving Feature Updates following their availability from Microsoft.
    - **Branch readiness level**: Set the branch for which the device will receive Windows updates (Current Branch or Current Branch for Business).
    - **Deferral period (days)**:  Specify the number of days for which Feature Updates will be deferred. You can defer receiving these Feature Updates for a period of 180 days from their release.
    - **Pause Features Updates starting**: Select whether to pause devices from receiving Feature Updates for a period of up to 60 days from the time you pause the updates. After the maximum days have passed, pause functionality will automatically expire and the device will scan Windows Updates for applicable updates. Following this scan, you can pause the updates again. You can unpause Feature Updates by clearing the checkbox.   
5. Choose whether to defer or pause Quality Updates.     
    Quality Updates are generally fixes and improvements to existing Windows functionality and are typically published the first Tuesday of every month, though can be released at any time by Microsoft. You can define if, and for how long, you would like to defer receiving Quality Updates following their availability.
    - **Deferral period (days)**: Specify the number of days for which Feature Updates will be deferred. You can defer receiving these Feature Updates for a period of 180 days from their release.
    - **Pause Quality Updates starting**: Select whether to pause devices from receiving Quality Updates for a period of up to 35 days from the time you pause the updates. After the maximum days have passed, pause functionality will automatically expire and the device will scan Windows Updates for applicable updates. Following this scan, you can pause the updates again. You can unpause Quality Updates by clearing the checkbox.
6. Select **Install updates from other Microsoft Products** to enable the group policy setting that make deferral settings applicable to Microsoft Update, as well as Windows Updates.
7. Select **Include drivers with Windows Update** to automatically update drivers from Windows Updates. If you clear this setting, driver updates are not downloaded from Windows Updates.
8. Complete the wizard to create the new deferral policy.

#### To deploy a Windows Update for Business deferral policy
1. In **Software Library** > **Windows 10 Servicing** > **Windows Update for Business Policies**
2. On the **Home** tab, in the **Deployment** group, select **Deploy Windows Update for Business Policy**.
3. Configure the following settings:
    - **Configuration policy to deploy**: Select the Windows Update for Business policy that you would like to deploy.
    - **Collection**: Click **Browse** to select the collection where you want to deploy the policy.
    - **Remediate noncompliant rules when supported**: Select to automatically remediate any rules that are noncompliant for Windows Management Instrumentation (WMI), the registry, scripts, and all settings for mobile devices that are enrolled by Configuration Manager.
    - **Allow remediation outside the maintenance window**: If a maintenance window has been configured for the collection to which you are deploying the policy, enable this option to let compliance settings remediate the value outside of the maintenance window. For more information about maintenance windows, see [How to use maintenance windows](../clients/manage/collections/use-maintenance-windows.md).
    - **Generate an alert**: Configures an alert that is generated if the configuration baseline compliance is less than a specified percentage by a specified date and time. You can also specify whether you want an alert to be sent to System Center Operations Manager.
    - **Random delay (hours)**: Specifies a delay window to avoid excessive processing on the Network Device Enrollment Service. The default value is 64 hours.
    - **Schedule**: Specify the compliance evaluation schedule by which the deployed profile is evaluated on client computers. The schedule can be either a simple or a custom schedule. The profile is evaluated by client computers when the user logs on.
4.  Complete the wizard to deploy the profile.



## Support for Entrust certification authorities
<!-- 1350740 -->
Configuration Manager now supports Entrust certification authorities; this enables PFX certificate delivery to devices enrolled into Microsoft Intune.

You can configure Entrust as the certification authority when adding a Certificate Registration Point role in Configuration Manager. When adding a new certificate profile that issues PFX certificates, you can select either a Microsoft or Entrust certification authority.

**Known issue**: In the 1706 technical preview, PFX certificates are not issued for Microsoft certification authorities. This does not affect imported PFX certificates or SCEP profiles.


## Cisco (IPsec) support for iOS VPN profiles
<!-- 1321367 -->

You can create a iOS VPN profile with Cisco (IPsec) as the connection type. For more information, see [Create VPN profiles](../../protect/deploy-use/create-vpn-profiles.md#create-a-vpn-profile).


## New Windows configuration item settings
<!-- 1354715 -->

In this release, we've added the following new settings you can use in Windows configuration items:

### Password

- **Device Encryption**

### Device

- **Region settings modification (desktop only)**
- **Power and sleep settings modification**
- **Language settings modification**
- **System time modification**
- **Device name modification**

### Store

- **Auto-update apps from store**
- **Use private store only**
- **Store originated app launch**

### Microsoft Edge

- **Block access to about:flags**
- **SmartScreen prompt override**
- **SmartScreen prompt override for files**
- **WebRTC localhost IP address**
- **Default search engine**
- **OpenSearch XML URL**
- **Homepages (desktop only)**

For more information about compliance settings, see [Ensure device compliance](../../compliance/understand/ensure-device-compliance.md).


## New device compliance policy rules

* **Required password type**. Specify whether the user must create an alphanumeric password or a numeric password. For alphanumeric passwords, you also specify the minimum number of character sets that the password must have. The four character sets are: Lowercase, uppercase letters, symbols and numbers.

  **Supported on:**
  * Windows Phone 8+
  * Windows 8.1+
  * iOS 6+
<br></br>
* **Block USB debugging on device**. You do not have to configure this settings as USB debugging is already disabled on Android for Work devices.

  **Supported on:**
  * Android 4.0+
  * Samsung KNOX Standard 4.0+
<br></br>
* **Block apps from unknown sources**. Require that devices prevent installation of apps from unknown sources. You do not have to configure this setting as Android for Work devices always restrict installation from unknown sources.

  **Supported on:**
  * Android 4.0+
  * Samsung KNOX Standard 4.0+
<br></br>
* **Require threat scan on apps**. This setting specifies that the Verify apps feature is enabled on the device.

  **Supported on:**
  * Android 4.2 through 4.4
  * Samsung KNOX Standard 4.0+


## New mobile application management policy settings
Beginning with this release, you can use three new mobile application management (MAM) policy settings:

- **Block screen capture (Android devices only):** Specifies that the screen capture capabilities of the device are blocked when using this app.

- **Disable contact sync:** Prevents the app from saving data to the native Contacts app on the device.

- **Disable printing:** Prevents the app from printing work or school data.

## Android and iOS enrollment restrictions
<!-- 1290826 -->
Starting with this release, admins can now specify that users cannot enroll personal Android or iOS devices in their hybrid environment. This allows you to limit enrolled devices to predeclared, company-owned devices or iOS devices enrolled with Device Enrollment Program only.

### Try it out
1. In the Configuration Manager console in the **Administration** workspace, go to **Cloud Services** > **Microsoft Intune Subscription**.
2. On the **Home** tab in the **Subscription** group, choose **Configure Platforms** and then select **Android** or **iOS**.
3. Select **Block personally owned devices**.

## Android for Work application management policy for copy-paste
We have updated the setting descriptions for Android for Work configuration items for the **Allow data sharing between  work and personal profile**.

|Before 1706 Technical Preview | New option name | Behavior|
|-|-|-|
|Prevent any sharing across boundaries| Default sharing restrictions| Work-to-personal: Default (expected to be blocked on all versions) <br>Personal-to-work: Default (allowed on 6.x+, blocked on 5.x)|
|No restrictions| Apps in personal profile can handle sharing requests from work profile| Work-to-personal: Allowed  <br>Personal-to-work: Allowed|
|Apps in work profile can handle sharing requests from personal profile |Apps in work profile can handle sharing requests from personal profile |Work-to-personal: Default<br>Personal-to-work: Allowed<br>(Only useful on 5.x where personal-to-work is blocked)|

None of these options directly prevent copy-paste behavior. We added a custom setting to the service and Company Portal app in 1704 that can be configured to prevent copy-paste. This can be set through custom URI.

- OMA-URI:  ./Vendor/MSFT/WorkProfile/DisallowCrossProfileCopyPaste
- Value type: Boolean

Setting DisallowCrossProfileCopyPaste to true prevents copy-paste behavior between Android for Work personal and work profiles.

### Try it out
1. In the Configuration Manager console, select **Assets and Compliance** > **Overview** > **Compliance settings** > **Configuration items**.
2. Choose **Create** to create a new configuration item, and specify **Name** and **Android for Work**.
3. In the device setting groups to configure, select **Work Profile**, and choose **Next**.
4. Select the value for **Allow data sharing between work and personal profiles**, and then complete the wizard.

## Device Health Attestation assessment for compliance policies for Conditional Access
<!-- 1097546 -->
Starting with this release you can use Device Health Attestation status as a compliance policy rule for Conditional Access to company resources.

### Try it out
Select a Device Health Attestation rule as part of a compliance policy assessment.
