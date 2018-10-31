---
title: Site components
titleSuffix: Configuration Manager
description: Learn how to configure site components to modify the behavior of site system roles and site status reporting.
ms.date: 10/26/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 5fccbbeb-0faa-4943-83c2-e67db62d392d
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Site components for Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

For each Configuration Manager site, you can configure site components to modify the behavior of site system roles and site status reporting. Site component configurations apply to a site, and to each instance of an applicable site system role at the site.  

In the Configuration Manager console, go to the **Administration** workspace, expand **Site Configuration**, and select the **Sites** node. Select a site. In the **Settings** group of the ribbon, choose **Configure Site Components**. Select one of the following options:

- [Software distribution](#software-distribution)  
- [Software update point](#software-update-point)  
- [Management point](#management-point)  
- [Status reporting](#status-reporting)  
- [Email notification](#email-notification)
- [Collection membership evaluation](#bkmk_colleval)


## About site components  

 Most options for the various site components are self-explanatory when viewed in the Configuration Manager console. However, the following details can help explain some of the more complex configurations, or direct you to additional content.  

> [!Note]  
> The available options for some components vary whether you select the central administration site, a primary site, or a secondary site. Some components are not available at all for certain types of sites.  



### Software distribution  

#### Content distribution settings
On the **General** tab, specify settings that modify how the site server transfers content to its distribution points. When you increase the values you use for concurrent distribution settings, content distribution can use more network bandwidth.  

#### Pull distribution point
For more information, see [Use a pull-distribution point](/sccm/core/plan-design/hierarchy/use-a-pull-distribution-point).

#### Network access account
For more information, see [Network access account](/sccm/core/plan-design/hierarchy/accounts#network-access-account).  


### Software update point  

For more information, see [Install a software update point](/sccm/sum/get-started/install-a-software-update-point).  


### Management point  

On the **General** tab, set up the site to publish information about its management points to Active Directory Domain Services.  

Configuration Manager clients use management points to locate services, and to find site information such as boundary group membership and PKI certificate selection options. Clients also use management points to find other management points in the site, as well as distribution points from which to download software. Management points also help clients to complete site assignment, and to download client policy and upload client information.  

The most secure method for clients to find management points is to publish them in Active Directory Domain Services. This service location method requires the following to be true:

- The schema is extended for Configuration Manager.
- There's a **System Management** container, with appropriate security permissions for the site server to publish to this container.
- The Configuration Manager site is set up to publish to Active Directory Domain Services.
- Clients belong to the same Active Directory forest as the site server's forest.  

When clients on the intranet can't use Active Directory Domain Services to find management points, use [DNS publishing](/sccm/core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services#bkmk_dns).  

For general information about service location, see [Understand how clients find site resources and services](/sccm/core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services).  


#### Publish selected intranet management points in DNS
Specify this option when clients on the intranet can't find management points from Active Directory Domain Services. Instead, they can use a DNS service location resource record (SRV RR) to find a management point in their assigned site.  

For Configuration Manager to publish intranet management points to DNS, all the following conditions must be met:  

-   Your DNS servers have a version of BIND that is 8.1.2 or later.  

-   Your DNS servers are set up for automatic updates, and support service location resource records.  

-   The specified fully qualified domain names (FQDNs) for the management points in Configuration Manager have host entries (A or AAA records) in DNS.  

> [!WARNING]  
>  For clients to find management points that are published in DNS, you must assign the clients to a specific site (rather than use automatic-site assignment). Set up these clients to use the site code with the domain suffix of their management point. For more information, see [Locating management points](/sccm/core/clients/deploy/assign-clients-to-a-site#locating-management-points).  

If Configuration Manager clients can't use Active Directory Domain Services or DNS to find management points on the intranet, they use [WINS](/sccm/core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services#bkmk_wins). The first management point that is installed for the site is automatically published to WINS when it's set up to accept HTTP client connections on the intranet.  


### Status reporting  

These settings directly set up the level of detail that's included in status reports from sites and clients.  


### Email notification  

Specify account and email server details to enable Configuration Manager to send email notifications for alerts.  

For more information, see [Use alerts and the status system](/sccm/core/servers/manage/use-alerts-and-the-status-system).


### <a name="bkmk_colleval"></a> Collection membership evaluation  

Use this component to set how often collection membership is incrementally evaluated. Incremental evaluation updates a collection membership with only new or changed resources.  

For more information, see [Best practices for collections](/sccm/core/clients/manage/collections/best-practices-for-collections).



##  <a name="BKMK_ServiceMgr"></a> Use the Configuration Manager Service Manager to manage site components  

You can use the Configuration Manager Service Manager to control Configuration Manager services, and to view the status of any Configuration Manager service or working thread. These services and threads are referred to collectively as Configuration Manager components. Understand the following statements about Configuration Manager components:  

-   Components can run on any site system.  

-   Components are managed the same way that you manage services in Windows. You can start, stop, pause, resume, or query Configuration Manager components.  

A Configuration Manager service runs when there's something for it to do. This action is typically when a configuration file is written to a component's inbox. 


### Use the Configuration Manager Service Manager  

1.  In the Configuration Manager console, go to the **Monitoring** workspace, expand **System Status**, and select the **Component Status** node.  

2.  In the **Component** group of the ribbon, select **Start**, and then choose **Configuration Manager Service Manager**.  

3.  When the Configuration Manager Service Manager opens, connect to the site that you want to manage.  

     If you don't see the site that you want to manage, go to the **Site** menu, and select **Connect**. Then enter the name of the site server of the correct site.  

4.  Expand the site and navigate to **Components** or **Servers**, depending on where the components that you want to manage are located.  

5.  In the right pane, select one or more components. Then on the **Component** menu, select **Query** to update the status of your selection.  

6.  After the status of the component is updated, use one of the four action-based options on the **Component** menu to modify the component's operation. After you request an action, you must query the component to display the new status of the component.  

7.  Close the Configuration Manager Service Manager when you're finished modifying the operational status of components.  
