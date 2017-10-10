---
title: "Site components for Configuration Manager"
description: "Learn how to configure site components to modify the behavior of site system roles and site status reporting."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 5fccbbeb-0faa-4943-83c2-e67db62d392d
caps.latest.revision: 9
author: Brenduns
ms.author: brenduns
manager: angrobe

---
# Site components for System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

At each System Center Configuration Manager site, you can set up site components to modify the behavior of site system roles and site status reporting. Site component configurations apply to a site, and to each instance of an applicable site system role at the site.  

## About site components  
 Most options for the various site components are self-explanatory when viewed in the Configuration Manager console. However, the following details can help explain some of the more complex configurations, or direct you to additional content that does explain them.  

### Software distribution  

-   **Content distribution settings:**  You can specify settings that modify how the site server transfers content to its distribution points. When you increase the values you use for concurrent distribution settings, content distribution can use more network bandwidth.  

-   **Network Access Account:**  For information about setting up and using the Network Access Account, see [Network Access Account](../../../../core/plan-design/hierarchy/manage-accounts-to-access-content.md#bkmk_NAA).  

### Software update point  

-   For information about configuration options for the software update point component, see [Install a software update point](../../../../sum/get-started/install-a-software-update-point.md).  

### Management point  

-   **Management points:** You can set up the site to publish information about its management points to Active Directory Domain Services.  

     Configuration Manager clients use management points to locate services, and to find site information such as boundary group membership and PKI certificate selection options. Clients also use management points to find other management points in the site, as well as distribution points from which to download software. Management points also help clients to complete site assignment, and to download client policy and upload client information.  

     Because the most secure method for clients to find management points is to publish them in Active Directory Domain Services, you will typically always select all functioning management points to publish to Active Directory Domain Services. However, this service location method requires the following to be true:

     - The schema is extended for Configuration Manager.
     - There is a **System Management** container, with appropriate security permissions for the site server to publish to this container.
     - The Configuration Manager site is set up to publish to Active Directory Domain Services.
     - Clients belong to the same Active Directory forest as the site server's forest.  

     When clients on the intranet cannot use Active Directory Domain Services to find management points, use [DNS](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#bkmk_dns) publishing instead.  

 For general information about service location, see [Understand how clients find site resources and services for System Center Configuration Manager](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  

-   **Publish selected intranet management points in DNS:** Specify this option when clients on the intranet cannot find management points from Active Directory Domain Services. Instead, they can use a DNS service location resource record (SRV RR) to find a management point in their assigned site.  

    For Configuration Manager to publish intranet management points to DNS, all the following conditions must be met:  

    -   Your DNS servers have a version of BIND that is 8.1.2 or later.  

    -   Your DNS servers are set up for automatic updates, and support service location resource records.  

    -   The specified fully qualified domain names (FQDNs) for the management points in Configuration Manager have host entries (A or AAA records) in DNS.  

    > [!WARNING]  
    >  For clients to find management points that are published in DNS, you must assign the clients to a specific site (rather than use automatic-site assignment). Set up these clients to use the site code with the domain suffix of their management point. For more information, see [Locating Management Points](/sccm/core/clients/deploy/assign-clients-to-a-site#locating-management-points) in [How to assign clients to a site in System Center Configuration Manager](/sccm/core/clients/deploy/assign-clients-to-a-site).  

     If Configuration Manager clients cannot use Active Directory Domain Services or DNS to find management points on the intranet, they use [WINS](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#bkmk_wins). The first management point that is installed for the site is automatically published to WINS when it is set up to accept HTTP client connections on the intranet.  

### Status reporting  

-   These settings directly set up the level of detail that is included in status reports from sites and clients.  

### Email notification  

-   Specify account and email server details to enable Configuration Manager to send email notifications for alerts.  

### Collection membership evaluation  

-   Use this task to set how often collection membership is incrementally evaluated. Incremental evaluation updates a collection membership with only new or changed resources.  

### Edit the site components at a site  

Use the following steps to edit site components:

1.  In the Configuration Manager console, click **Administration** > **Site Configuration** > **Sites**, and then select the site that has site components you want to configure.  

2.  On the **Home** tab, in the **Settings** group, click **Configure Site Components**. Then select the site component you want to configure.  

##  <a name="BKMK_ServiceMgr"></a> Use the Configuration Manager Service Manager to manage site components  
You can use the Configuration Manager Service Manager to control Configuration Manager services, and to view the status of any Configuration Manager service or working thread (referred to collectively as Configuration Manager components). Understand the following about Configuration Manager components:  

-   Components can run on any site system.  

-   Components are managed the same way that you manage services in Windows. You can start, stop, pause, resume, or query Configuration Manager components.  

A Configuration Manager service runs when there is something for it to do (typically, when a configuration file is written to a component's inbox). If you have to identify the component involved in an operation, you can use the Configuration Manager Service Manager to manipulate various services and threads. You can then view the resulting change in the behavior of Configuration Manager. For example, you can stop Configuration Manager services one at a time, until a particular response is eliminated. Doing so enables you to determine which service causes the behavior.  

> [!TIP]  
>  The following procedure can be used to manipulate Configuration Manager component operation.  

### Use the Configuration Manager Service Manager  

1.  In the Configuration Manager console, click **Monitoring** >  **System Status**, and then click **Component Status**.  

2.  On the **Home** tab, in the **Component** group, click **Start**. Then select **Configuration Manager Service Manager**.  

3.  When the Configuration Manager Service Manager opens, connect to the site that you want to manage.  

     If you do not see the site that you want to manage, click **Site**, click **Connect**, and then enter the name of the site server of the correct site.  

4.  Expand the site and navigate to **Components** or **Servers**, depending on where the components that you want to manage are located.  

5.  In the right pane, select one or more components. Then on the **Component** menu, click **Query** to update the status of your selection.  

6.  After the status of the component is updated, use one of the four action-based options on the **Component** menu to modify the component's operation. After you request an action, you must query the component to display the new status of the component.  

7.  Close the Configuration Manager Service Manager when you are finished modifying the operational status of components.  
