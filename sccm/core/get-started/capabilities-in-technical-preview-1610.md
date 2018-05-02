---
title: "Capabilities in Technical Preview 1610"
titleSuffix: "Configuration Manager"
description: "Learn about features available in the Technical Preview for System Center Configuration Manager, version 1610."
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 8b31fd3e-875a-4a31-9498-5b050aadce32
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# Capabilities in Technical Preview 1610 for System Center Configuration Manager

*Applies to: System Center Configuration Manager (Technical Preview)*



This article introduces the features that are available in the Technical Preview for System Center Configuration Manager, version 1610. You can install this version to update and add new capabilities to your Configuration Manager technical preview site.      Before installing this version of the technical preview, review the introductory topic, [Technical Preview for System Center Configuration Manager](../../core/get-started/technical-preview.md), to become familiar with general requirements and limitations for using a technical preview, how to update between versions, and how to provide feedback about the features in a technical preview.    


**The following are new features you can try out with this version.**  
## Filter by content size in automatic deployment rules
You can now filter on the content size for software updates in automatic deployment rules. For example, you can set the **Content Size (KB)** filter to **< 2048** to only download software updates that are smaller than 2MB. Using this filter prevents large software updates from automatically downloading to better support simplified Windows down-level servicing when network bandwidth is limited. For details, see [Configuration Manager and Simplified Windows Servicing on Down Level Operating Systems](https://blogs.technet.microsoft.com/enterprisemobility/2016/10/07/configuration-manager-and-simplified-windows-servicing-on-down-level-operating-systems/).

#### To configure the Content Size field
To configure the **Content Size (KB)** field, go to the **Software Updates** page in the Create Automatic Deployment Rule Wizard when you create an ADR or go to the **Software Updates** tab in the properties for an existing ADR.

![Content size field](media/contentsizefield.png)

## Improved functionality for required software dialogs
When a user receives required software, from the **Snooze and remind me:** setting, they can select from the following drop-down list of values:
- Later: specifies that notifications are scheduled based on the notification settings configured in Client Agent settings.
- Fixed time: specifies that the notification will be scheduled to display again after the selected time. For example, if a user selects 30 minutes, the notification will display again in 30 minutes.

![Computer Agent page in Client Agent settings](media/computeragentsettings.png)

The maximum snooze time is always based on the notification values configured in the Client Agent settings at every time along the deployment timeline. For example, if the **Deployment deadline greater than 24 hours, remind users every (hours)** setting on the Computer Agent page is configured for 10 hours, and it is more than 24 hours before the deadline when the dialog is launched, the user would be presented with a set of snooze options up to but never greater than 10 hours. As the deadline approaches, the dialog will show fewer options, consistent with the relevant Client Agent settings for each component of the deployment timeline.

Additionally, for a high-risk deployment, such as a task sequence that deploys an operating system, the end-user notification experience is now more intrusive. Instead of a transient taskbar notification, each time the user is notified that critical software maintenance is required, a dialog box such as the following displays on the user's computer:

![Required Software dialog](media/requiredsoftwaredialog.png)


For more information:
- [Settings to manage high-risk deployments](../../protect/understand/settings-to-manage-high-risk-deployments.md)
- [How to configure client settings](../clients/deploy/configure-client-settings.md)

## Deny previously approved application requests

As an administrator you can now deny a previously approved application request. Once denied, to install this application later users must resubmit a request. Denial does not uninstall the application; rather it forces reapproval for any new request for that application from that user. Previously, application request denial was only available for application requests that had not been approved.

#### Try it out
To deny an application approved request:

1.	In the Configuration Manager console, [create and deploy an application](https://docs.microsoft.com/sccm/apps/deploy-use/create-applications) that requires approval.
2.	On a client computer, open Software Center and submit a request for the application.
3.	In the Configuration Manager console, approve the application request.
4.	Deny the approved application request: In the Configuration Manager console, navigate **Software Library** > **Overview** > **Application Management** > **Approval Requests** and select the application request you want to deny.  In the ribbon, click **Deny**.

## Exclude clients from automatic upgrade
Technical Preview 1610 introduces a new setting you can use to exclude a collection of clients from automatically installing updated client versions.  This applies to automatic upgrade as well as other methods such as software update-based upgrade, logon scripts, and group policy. This can be used for a collection of computers that need greater care when upgrading the client. A client that is in an excluded collection ignores requests to install updated client software.

### Configure exclusion from automatic upgrade
To configure automatic upgrade exclusions:
1.	In the Configuration Manager console open **Hierarchy Settings** under **Administration > Site Configuration > Sites**, and then select the **Client Upgrade** tab.
2.	Select the checkbox for **Exclude specified clients from upgrade**, and then for **Exclusion collection**, select the collection you want to exclude. You can only select a single collection for exclusion.
3.	Click **OK** to close and save the configuration. Then, after clients update policy, clients in the excluded collection will no longer automatically install updates to the client software.

  ![Settings for automatic upgrade exclusion](media/automatic_upgrade_exclusion.png)

> [!NOTE]
> Although the user interface states that clients will not be upgraded via any method, there are two methods you can use to override these settings. Client push installation and a manual client installation can be used to override this configuration. For more details, see the following section.

### How to upgrade a client that is in an excluded collection
So long as a collection is configured to be excluded, members of that collection can only have their client software upgraded by one of two methods, which override the exclusion:
 - **Client Push Installation** – You can use client push installation to upgrade a client that is in an excluded collection. This is allowed as it is considered to be the intent of the administrator and enables you to upgrade clients without removing the entire collection from exclusion.       
 - **Manual client installation** – You can manually upgrade clients that are in an excluded collection when you use the following command line switch with ccmsetup:  ***/ignoreskipupgrade***

  If you attempt to manually upgrade a client that is a member of the excluded collection and do not use this switch, the client will not install the new client software. For more information see [How to install Configuration Manager Clients Manually](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#a-namebkmkmanuala-how-to-install-configuration-manager-clients-manually).

For more information on client installation methods, see [How to deploy clients to Windows computers in System Center Configuration Manager](/sccm/core/clients/deploy/deploy-clients-to-windows-computers).

## Windows Defender configuration settings

You can now configure Windows Defender client settings on Intune-enrolled Windows 10 computers using configuration items in the Configuration Manager console.

Specifically, you can configure the following Windows Defender settings:
- Allow real-time monitoring
- Allow behavior monitoring
- Enable Network Inspection System
- Scan all downloads
- Allow script scanning
- Monitor file and program activity
  - Files monitored
- Days to track resolved malware
- Allow client UI access
- Schedule a system scan
  - Day scheduled
  - Time scheduled
- Schedule a daily quick scan
  - Time scheduled
- Limit CPU usage % during a scan
 Scan archive files
- Scan email messages
- Scan removable drives
- Scan mapped drives
- Scan files opened from net shares
- Signature update interval
- Allow cloud protection
- Prompt users for samples
- Potentially Unwanted Application detection
- Excluded files/folders
- Excluded file extensions
- Excluded processes

> [!NOTE]
> These settings can only be configured on client computers running Windows 10 November Update (1511) and above.

### Try it out!

1.	In the Configuration Manager console, go **Assets and Compliance** > **Overview** > **Compliance Settings** > **Configuration Items**, and create a new **Configuration Item**.
2.	Enter a name, then select **Windows 8.1 and Windows 10** under **Settings for devices managed without the Configuration Manager client** and click **Next**.
3.	Ensure **All Windows 10 (64-bit)** and **All Windows 10 (32-bit)** are selected on the **Supported Platforms** page, then click **Next**.
4.	Select the **Windows Defender** setting group, then click **Next**.
5.	Configure the desired settings on this page, then click **Next**.
6.	Complete the wizard.
7.	Add this configuration item to a configuration baseline, and deploy this baseline to computers running Windows 10 November Update (1511) or above.

> [!NOTE]
> Remember to check the **Remediate noncompliant settings** checkbox when deploying the configuration baseline.

## Request policy sync from administrator console

You can now request a policy sync for a mobile device from the Configuration Manager console, instead of needing to request a sync from the device itself. Sync request state information is available as a new column in device views, called **Remote Sync State**. State also appears in the **Discovery data** section of the **Properties** dialog for each mobile device.

### Try it out!

1.	In the Configuration Manager console, go **Assets and Compliance** > **Overview** > Devices.
2.	In the **Remote Device Actions** menu, select **Send Sync Request**.

Sync can take five to ten minutes. Any changes in policy are synced to the device. You can track the state of the sync request in the **Remote Sync State** column in the **Devices** view, or in the device's **Properties** dialog.

## Additional security role support

In addition to Full Administrator, the following built-in security roles now have full access to items in the **All Corporate-owned Devices** node, including **Predeclared Devices**, **iOS Enrollment Profiles**, and **Windows Enrollment Profiles**:
•	**Asset Manager**
•	**Company Resource Access Manager**

Read-only access to these areas of the Configuration Manager console is still granted to the **Read-only Analyst** role.

## Conditional access for Windows 10 VPN profiles

You can now require Windows 10 devices enrolled in Azure Active Directory to be compliant in order to have VPN access through Windows 10 VPN profiles created in the Configuration Manager console. This is possible through the new **Enable conditional access for this VPN connection** checkbox on the **Authentication Method** page in the VPN profile wizard and VPN profile properties for Windows 10 VPN profiles. You can also specify a separate certificate for single sign-on authentication if you enable conditional access for the profile.

## See Also
[Technical Preview for System Center Configuration Manager](../../core/get-started/technical-preview.md)
