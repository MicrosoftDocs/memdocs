---
title: "Boundary groups for 1511, 1602, and 1606 | System Center Configuration Manager"
description: "Use boundary groups with Configuration Manager versions 1511, 1602, and 1606."
ms.custom: na
ms.date: 2/8/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: dec1e0d7-5864-43a8-9f56-413923b3914e
caps.latest.revision: 10
author: Brenduns
ms.author: brenduns
manager: angrobe

---
# Boundary groups for System Center Configuration Manager version 1511, 1602, and 1606

*Applies to: System Center Configuration Manager (Current Branch)*
<!-- This topic drops from TOC with the release of version 1706 -->

The information in this topic is specific to using boundary groups with versions 1511, 1602, and 1606 of System Center Configuration Manager.
If you use version 1610 or later, see [Configure boundary groups](/sccm/core/servers/deploy/configure/boundary-groups) for information about how to use the redesigned boundary groups.  


##  <a name="BKMK_BoundaryGroups"></a> Boundary groups  
 You create boundary groups to logically group related network locations (boundaries) to make it easier to manage your infrastructure. You must assign boundaries to boundary groups before you can use the boundary group. Clients use the boundary group configuration for:  

-   Automatic site assignment  

-   Content location  

-   Preferred management points

    If you will use preferred management points, you must enable this option for the hierarchy and not from within the boundary group configuration. See the *To enable use of preferred management points* procedure later in this topic.  

When you set up boundary groups, you add one or more boundaries to the boundary group. You then configure additional settings for use by clients that are located on those boundaries.  

#### To create a boundary group  

1.  In the Configuration Manager console, choose **Administration** > **Hierarchy Configuration** >  **Boundary Groups**.  

2.  On the **Home** tab, in the **Create** group, choose **Create Boundary Group**.  

3.  In the **Create Boundary Group** dialog box, choose the **General** tab, and then enter a **Name** for this boundary group.  

4.  Choose **OK** to save the new boundary group.  

#### To set up a boundary group  

1.  In the Configuration Manager console, choose **Administration** > **Hierarchy Configuration** >  **Boundary Groups**.  

2.  Choose the boundary group that you want to change.  

3.  On the **Home** tab, in the **Properties** group, choose **Properties**.  

4.  In the **Properties** dialog box for the boundary group, choose the **General** tab to change the boundaries that are members of this boundary group:  

    -   To add boundaries, choose **Add**, check the check box for one or more boundaries, and then choose **OK**.  

    -   To remove boundaries, select the boundary, and then choose **Remove**.  

5.  Choose the **References** tab to change the site assignment and associated site system server configuration:  

    -   To enable this boundary group for use by clients for site assignment, check the check box for **Use this boundary group for site assignment**, and then choose a site from the **Assigned site** dropdown box.  

    -   To set up the available site system servers that are associated with this boundary group:  

    1.  Choose **Add**, and then check the check box for one or more servers. The servers are added as associated site system servers for this boundary group. Only servers that have supported site system role installed on them are available.  

        > [!NOTE]  
        >  You can select any combination of available site systems from any site in the hierarchy. Selected site systems are listed on the **Site Systems** tab in the properties of each boundary that is a member of this boundary group.  

    2.  To remove a server from this boundary group, choose the server, and then choose **Remove**.  

        > [!NOTE]  
        >  To stop use of this boundary group for associating site systems, you must remove all servers that are listed as associated site system servers.  

    3.  To change the network connection speed for a site system server for this boundary group, choose the server, and then choose **Change Connection**.  

         By default, the connection speed for each site system is **Fast**, but you can change the speed to **Slow**. The network connection speed and the configuration of a deployment determine whether a client can download content from the server.  

6.  Choose **OK** to close the boundary group properties and save the configuration.  

#### To associate a content deployment server or management point with a boundary group  

1.  In the Configuration Manager console, choose **Administration** > **Hierarchy Configuration** >  **Boundary Groups**.  

2.  Choose the boundary group that you want to change.  

3.  On the **Home** tab, in the **Properties** group, choose **Properties**.  

4.  In the **Properties** dialog box for the boundary group, choose the **References** tab.  

5.  Under **Select site system servers**, choose **Add**, check the check box for the site system servers that you want to associate with this boundary group, and then choose **OK**.  

6.  Choose **OK** to close the dialog box and save the boundary group configuration.  

#### To enable use of preferred management points  

1.  In the Configuration Manager console, choose **Administration** > **Site Configuration** > **Sites**, and then, on the **Home** tab, choose **Hierarchy Settings**.  

2.  On the **General** tab of **Hierarchy Settings**, choose **Clients prefer to use management points specified in boundary groups**.  

3.  Choose **OK** to close the dialog box and save the configuration.  

#### To set up a fallback site for automatic site assignment  

1.  In the Configuration Manager console, choose **Administration** > **Site Configuration** >  **Sites**.  

2.  On the **Home** tab, in the **Sites** group, choose **Hierarchy Settings**.  

3.  On the **General** tab, check the check box for **Use a fallback site**, and then choose a site from the **Fallback site** drop-down list.  

4.  Choose **OK** to save the configuration.  

 The following sections provide additional details about boundary group configurations.  

###  <a name="BKMK_BoundarySiteAssignment"></a> About site assignment  
 You can set up each boundary group with an assigned site for clients.  

-   A newly installed client that uses automatic site assignment will join the assigned site of a boundary group that has the client's current network location.  

-   A client that's assigned to a site does not change its site assignment when the client changes its network location. For example, if the client roams to a new network location that is represented by a boundary in a boundary group that has a different site assignment, the client's assigned site will remain unchanged.  

-   When Active Directory System Discovery discovers a new resource, network information for the discovered resource is evaluated against the boundaries in boundary groups. This process associates the new resource with an assigned site for use by the client push installation method.  

-   When a boundary is a member of multiple boundary groups that have different assigned sites, clients randomly select one of the sites.  

-   Changes to a boundary group's assigned site apply only to new site assignment actions. Clients that were previously assigned to a site do not evaluate their site assignment again based on changes to the configuration of a boundary group (or to their own network location).  

For more about client site assignment, see [Using Automatic Site Assignment for Computers](../../../../core/clients/deploy/assign-clients-to-a-site.md#BKMK_AutomaticAssignment) in [How to assign clients to a site in System Center Configuration Manager](../../../../core/clients/deploy/assign-clients-to-a-site.md).  

###  <a name="BKMK_BoundaryContentLocation"></a> About content location  
 You can set up each boundary group with one or more distribution points and state migration points, and you can associate the same distribution points and state migration points with multiple boundary groups.  

-   **During software distribution**, clients request a location for deployment content. Configuration Manager sends the client a list of distribution points that are associated with each boundary group that includes the current network location of the client.  

-   **During operating system deployment**, clients request a location to send or receive their state migration information. Configuration Manager sends the client a list of state migration points that are associated with each boundary group that includes the current network location of the client.  

This behavior lets the client select the nearest server from which to transfer the content or state migration information.  

###  <a name="BKMK_PreferredMP"></a> About preferred management points  
 Preferred management points let a client identify a management point that is associated with its current network location (boundary).  

-   A client tries to use a preferred management point from its assigned site before it uses a management point from its assigned site that is not set up as preferred.  

-   To use this option, you must enable it for the hierarchy and set up boundary groups at individual primary sites to include the management points that should be associated with that boundary group's associated boundaries  

-   When preferred management points are set up and a client organizes its list of management points, the client places the preferred management points at the top of its list of assigned management points, which includes all management points from the client's assigned site.  

> [!NOTE]  
>  When a client roams, like when a laptop travels to a remote office location and changes its network location, it might use a management point (or proxy management point) from the local site at its new location before it tries to use a management point from its assigned site (which includes the preferred management points).  See [Understand how clients find site resources and services for System Center Configuration Manager](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md) for more information.  

###  <a name="BKMK_BoundaryOverlap"></a> About overlapping boundaries  
 Configuration Manager supports overlapping boundary configurations for content location:  

-   **When a client requests content**, and the client network location belongs to multiple boundary groups, Configuration Manager sends the client a list of all distribution points that have the content.  

-   **When a client requests a server to send or receive its state migration information**, and the client network location belongs to multiple boundary groups, Configuration Manager sends the client a list of all state migration points that are associated with a boundary group that includes the current network location of the client.  

This behavior lets the client select the nearest server from which to transfer the content or state migration information.  

###  <a name="BKMK_BoudnaryNetworkSpeed"></a> About network connection speed  
 You can set the network connection speed for each site system server in a boundary group. This setting applies to clients that connect to a site system based on this boundary group's configuration. The same site system server can have a different connection speed set for it in different boundary groups.  

 By default, the network connection speed is set to **Fast**, but you can change it to **Slow**. The network connection speed and the deployment configuration check whether a client can download content from a distribution point when the client is in an associated boundary group.  

 For more about how the network connection speed configuration affects how clients get content, see [Content source location scenarios](../../../../core/plan-design/hierarchy/content-source-location-scenarios.md).  
