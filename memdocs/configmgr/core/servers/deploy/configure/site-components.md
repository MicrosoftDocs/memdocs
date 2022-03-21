---
title: Site components
titleSuffix: Configuration Manager
description: Learn how to configure site components to modify the behavior of site system roles and site status reporting.
ms.date: 12/15/2021
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
author: mestew
ms.author: mstewart
manager: dougeby
ms.localizationpriority: medium
---

# Site components for Configuration Manager

*Applies to: Configuration Manager (current branch)*

For each Configuration Manager site, you can configure site components to modify the behavior of site system roles and site status reporting. Site component configurations apply to a site, and to each instance of an applicable site system role at the site.

In the Configuration Manager console, go to the **Administration** workspace, expand **Site Configuration**, and select the **Sites** node. Select a site. In the **Settings** group of the ribbon, choose **Configure Site Components**. Select one of the following options:

- [Software distribution](#software-distribution)
- [Software update point](#software-update-point)
- [OS deployment](#os-deployment)
- [Management point](#management-point)
- [Status reporting](#status-reporting)
- [Email notification](#email-notification)
- [Collection membership evaluation](#bkmk_colleval)

## About site components

Most options for the various site components are self-explanatory when viewed in the Configuration Manager console. However, the following details can help explain some of the more complex configurations, or direct you to other content.

> [!NOTE]
> The available options for some components vary whether you select the central administration site, a primary site, or a secondary site. Some components are not available at all for certain types of sites.

### Software distribution

#### Content distribution settings

On the **General** tab, specify settings that modify how the site server transfers content to its distribution points. When you increase the values you use for concurrent distribution settings, content distribution can use more network bandwidth.

#### Pull distribution point

For more information, see [Use a pull-distribution point](../../../plan-design/hierarchy/use-a-pull-distribution-point.md).

#### Network access account

For more information, see [Network access account](../../../plan-design/hierarchy/accounts.md#network-access-account).

#### Automate software distribution site component with PowerShell

To programmatically view and configure the **Software distribution** site component, use the following PowerShell cmdlets:

- [Get-CMSoftwareDistributionComponent](/powershell/module/configurationmanager/get-cmsoftwaredistributioncomponent)
- [Set-CMSoftwareDistributionComponent](/powershell/module/configurationmanager/set-cmsoftwaredistributioncomponent)

### Software update point

For more information, see [Install a software update point](../../../../sum/get-started/install-a-software-update-point.md).

#### Automate software update point site component with PowerShell

To programmatically view and configure the **Software update point** site component, use the following PowerShell cmdlets:

- [Get-CMSoftwareUpdatePointComponent](/powershell/module/configurationmanager/get-cmsoftwareupdatepointcomponent)
- [Set-CMSoftwareUpdatePointComponent](/powershell/module/configurationmanager/set-cmsoftwareupdatepointcomponent)

### OS deployment

For more information, see [Specify the drive for offline OS image servicing](../../../../osd/get-started/manage-operating-system-images.md#specify-the-drive-for-offline-os-image-servicing).

### Management point

On the **General** tab, set up the site to publish information about its management points to Active Directory Domain Services.

Configuration Manager clients use management points to locate services, and to find site information such as boundary group membership and PKI certificate selection options. Clients also use management points to find other management points in the site, and distribution points from which to download software. Management points also help clients to complete site assignment, and to download client policy and upload client information.  

The most secure method for clients to find management points is to publish them in Active Directory Domain Services. This service location method requires the following to be true:

- The schema is extended for Configuration Manager.
- There's a **System Management** container, with appropriate security permissions for the site server to publish to this container.
- The Configuration Manager site is set up to publish to Active Directory Domain Services.
- Clients belong to the same Active Directory forest as the site server's forest.  

When clients on the intranet can't use Active Directory Domain Services to find management points, use [DNS publishing](../../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#dns). This article also describes the option to **Publish selected intranet management points in DNS**.

For general information about service location, see [Understand how clients find site resources and services](../../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).

#### Automate management point site component with PowerShell

To programmatically view and configure the **Management point** site component, use the following PowerShell cmdlets:

- [Get-CMManagementPointComponent](/powershell/module/configurationmanager/get-cmmanagementpointcomponent)
- [Set-CMManagementPointComponent](/powershell/module/configurationmanager/set-cmmanagementpointcomponent)

### Status reporting

These settings directly set up the level of detail that's included in status reports from sites and clients.

#### Automate status reporting site component with PowerShell

To programmatically view and configure the **Status reporting** site component, use the following PowerShell cmdlets:

- [Get-CMStatusReportingComponent](/powershell/module/configurationmanager/get-cmstatusreportingcomponent)
- [Set-CMStatusReportingComponent](/powershell/module/configurationmanager/set-cmstatusreportingcomponent)

### Email notification

Specify account and email server details to enable Configuration Manager to send email notifications for alerts.

For more information, see [Configure alerts](../../manage/configure-alerts.md#configure-email-notification-for-alerts).

#### Automate email notification site component with PowerShell

To programmatically view and configure the **Email notification** site component, use the following PowerShell cmdlets:

- [Get-CMEmailNotificationComponent](/powershell/module/configurationmanager/get-cmemailnotificationcomponent)
- [Set-CMEmailNotificationComponent](/powershell/module/configurationmanager/set-cmemailnotificationcomponent)

### <a name="bkmk_colleval"></a> Collection membership evaluation

Use this component to set how often collection membership is incrementally evaluated. Incremental evaluation updates a collection membership with only new or changed resources.

For more information, see [Best practices for collections](../../../clients/manage/collections/best-practices-for-collections.md).

#### Automate collection membership evaluation site component with PowerShell

To programmatically view and configure the **Collection membership evaluation** site component, use the following PowerShell cmdlets:

- [Get-CMCollectionMembershipEvaluationComponent](/powershell/module/configurationmanager/get-cmcollectionmembershipevaluationcomponent)
- [Set-CMCollectionMembershipEvaluationComponent](/powershell/module/configurationmanager/set-cmcollectionmembershipevaluationcomponent)

## Configuration Manager Service Manager

You can use the Service Manager to control Configuration Manager services, and to view the status of any Configuration Manager service or working thread. These services and threads are referred to collectively as Configuration Manager components.

- Components can run on any site system.

- Manage components the same way that you manage services in Windows. The following actions apply to Configuration Manager components:

  - Start
  - Stop
  - Pause
  - Resume
  - Query

A Configuration Manager service runs when there's something for it to do. For example, when a configuration file is written to a component's inbox.

### Use Service Manager

1. In the Configuration Manager console, go to the **Monitoring** workspace, expand **System Status**, and select the **Component Status** node.

1. In the **Component** group of the ribbon, select **Start**, and then choose **Configuration Manager Service Manager**.

1. When the Configuration Manager Service Manager opens, connect to the site that you want to manage.

    If you don't see the site that you want to manage, go to the **Site** menu, and select **Connect**. Then enter the name of the site server of the correct site.

1. Expand the site and navigate to **Components** or **Servers**, depending on the location of the components that you want to manage.

1. In the right pane, select one or more components. Then on the **Component** menu, select **Query** to update the status of your selection.

1. After it updates the status of the component, use one of the four action-based options on the **Component** menu. Use these actions to modify the component's operation. After you request an action, query the component again to display the new status of the component.

1. Close the Configuration Manager Service Manager when you're finished modifying the operational status of components.
