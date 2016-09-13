---
title: "Define site boundaries and boundary groups for System Center Configuration Manager"
ms.custom: na
ms.date: 2016-07-22
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 54aa20d5-791e-4416-9db4-5aaea472c0b7
caps.latest.revision: 10
author: Brenduns
translation.priority.ht:
  - cs-cz
  - de-de
  - en-gb
  - es-es
  - fr-fr
  - hu-hu
  - it-it
  - ja-jp
  - ko-kr
  - nl-nl
  - pl-pl
  - pt-br
  - pt-pt
  - ru-ru
  - sv-se
  - tr-tr
  - zh-cn
  - zh-tw
---
# Define site boundaries and boundary groups for System Center Configuration Manager
Boundaries for System Center Configuration Manager define network locations on your intranet that can contain devices that you want to manage. Boundary groups are logical groups of  boundaries that you configure. Both boundary groups and boundaries are available throughout a  hierarchy and you do not configure them for individual sites.  

 A  hierarchy can include any number of boundary groups, and each boundary group can contain any combination of the following boundary types:  

-   IP subnet,  

-   Active Directory site name  

-   IPv6 Prefix  

-   IP address range  

Clients on the intranet evaluate their current network location and then use that information to identify boundary groups to which they belong.  

 Clients use boundary groups to:  

-   **Find an assigned site:** Boundary groups enable clients to find a primary site for client assignment (automatic site assignment).  

-   **Find certain site system roles they can use:**  When you associate a boundary group with certain site system roles, the boundary group provides clients that list of site systems for use during content location and as  preferred management points.  

Clients that are on the Internet or configured as Internet-only clients do not use boundary information. These clients cannot use automatic site assignment and can always download content from any distribution point from their assigned site when the distribution point is configured to allow client connections from the Internet.  


##  <a name="BKMK_Boundaries"></a> Boundaries  
 You can manually create individual boundaries. Additionally, you can configure [Active Directory Forest Discovery](../../../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutForest) to auto-discover and create boundaries for each IP Subnet and Active Directory Site it discovers.  

-   Each boundary represents a network location in and is available for use by  every site in your hierarchy.  

-   Configuration Manager does not support the direct entry of a supernet as a boundary. Instead, use the IP address range boundary type.  

-   When Active Directory Forest Discovery identifies a supernet that is assigned to an Active Directory site, Configuration Manager converts the supernet into an IP address range boundary.  

-   The boundary a client is on is equivalent to the Active Directory site, or network IP address that the client identifies. (It is not uncommon for a client to use an IP address that the Configuration Manager administrator is not aware of. If the clients network location is in doubt, confirm what the client reports as its location using the **IPCONFIG** command on the client.)  

When you create a boundary, it automatically receives a name that is based upon the type and scope of the boundary. You cannot modify this name. Instead, when you configure the boundary specify a description to help identify the boundary in the Configuration Manager console.  

 After you create a boundary, you can modify its properties to do the following:  

-   Add the boundary to one or more boundary groups.  

-   Change the type or scope of the boundary.  

-   View the boundaries **Site Systems** tab to see which site system servers (distribution points, state migration points, and management  points) are associated with the boundary.  

#### To create a boundary  

1.  In the Configuration Manager console, click **Administration** > **Hierarchy Configuration** > **Boundaries**  

2.  On the **Home** tab, in the **Create** group, click **Create Boundary.**  

3.  On the **General** tab of the Create Boundary dialog box you can specific a **Description** to identify the boundary by a friendly name or reference.  

4.  Select a **Type** for this boundary:  

    -   If you select **IP Subnet**, you must specify a **Subnet ID** for this boundary.  

        > [!TIP]  
        >  You can specify the **Network** and **Subnet mask** to have the **Subnet ID** automatically specified. When you save the boundary, only the Subnet ID value is saved.  

    -   If you select **Active Directory site**, you must specify or **Browse** to an Active Directory site in the local forest of the site server.  

        > [!IMPORTANT]  
        >  When you specify an Active Directory site for a boundary, the boundary includes each IP Subnet that is a member of that Active Directory site. If the configuration of the Active Directory site changes in Active Directory, the network locations included in this boundary also change.  

    -   If you select **IPv6 prefix**, you must specify a **Prefix** in the IPv6 prefix format.  

    -   If you select **IP address range**, you must specify a **Starting IP address** and **Ending IP address** that includes part of an IP Subnet or includes multiple IP Subnets.  

5.  Click **OK** to save the new boundary.  

#### To configure a boundary  

1.  In the Configuration Manager console, click **Administration** > **Hierarchy Configuration** > **Boundaries**  

2.  Select the boundary you want to modify.  

3.  On the **Home** tab, in the **Properties** group, click **Properties**.  

4.  In the **Properties** dialog box for the boundary, select the **General** tab to edit the **Description** or **Type** for the boundary. You can also change the scope of a boundary by editing the network locations for the boundary. For example, for an Active Directory site boundary you can specify a new Active Directory site name.  

5.  Select the **Site Systems** tab to view the site systems that are associated with this boundary. You cannot change this configuration from the properties of a boundary.  

    > [!TIP]  
    >  For a site system server to be listed as a site system for a boundary, the site system server must be associated as a site system server for at least one boundary group that includes this boundary. This is configured on the **References** tab of a boundary group.  

6.  Select the **Boundary Groups** tab to modify the boundary group membership for this boundary:  

    -   To add this boundary to one or more boundary groups, click **Add**, select the check box for one or more boundary groups, and then click **OK**.  

    -   To remove this boundary from a boundary group, select the boundary group and click **Remove**.  

7.  Click **OK** to close the boundary properties and save the configuration.  

##  <a name="BKMK_BoundaryGroups"></a> Boundary groups  
 You create boundary groups to logically group related network locations (boundaries) to make it easier to manage your infrastructure. You must assign boundaries to boundary groups before you can use the boundary group. Clients use the boundary group configuration for:  

-   Automatic site assignment  

-   Content location  

-   Preferred management points  (If you will use preferred management points, you must enable this option for the hierarchy and not from within the boundary group configuration. See the following procedure *To enable use of preferred management points*)  

When you configure boundary groups, you add one or more boundaries to the boundary group, and then configure additional settings for use by clients that are  located on those boundaries.  

#### To create a boundary group  

1.  In the Configuration Manager console, click **Administration** > **Hierarchy Configuration** >  **Boundary Groups**.  

2.  On the **Home** tab, in the **Create** group, click **Create Boundary Group**.  

3.  In the **Create Boundary Group** dialog box, select the **General** tab and specify a **Name** for this boundary group.  

4.  Click **OK** to save the new boundary group.  

#### To configure a boundary group  

1.  In the Configuration Manager console, click **Administration** > **Hierarchy Configuration** >  **Boundary Groups**.  

2.  Select the boundary group you want to modify.  

3.  On the **Home** tab, in the **Properties** group, click **Properties**.  

4.  In the **Properties** dialog box for the boundary group, select the **General** tab to modify the boundaries that are members of this boundary group:  

    -   To add boundaries, click **Add**, select the check box for one or more boundaries, and click **OK**.  

    -   To remove boundaries, select the boundary and click **Remove**.  

5.  Select the **References** tab to modify the site assignment and associated site system server configuration:  

    -   To enable this boundary group for use by clients for site assignment, select the check box for **Use this boundary group for site assignment**, and then select a site from the **Assigned site** dropdown box.  

    -   To configure which available site system servers are associated with this boundary group:  

    1.  Click **Add**, and then select the check box for one or more servers. The servers are added as associated site system servers for this boundary group. Only servers that have supported site system role installed on them are available.  

        > [!NOTE]  
        >  You can select any combination of available site systems from any site in the hierarchy. Selected site systems are listed on the **Site Systems** tab in the properties of each boundary that is a member of this boundary group.  

    2.  To remove a server from this boundary group, select the server and then click **Remove**.  

        > [!NOTE]  
        >  To stop use of this boundary group for associating site systems you must remove all servers listed as associated site system servers.  

    3.  To change the network connection speed for a site system server for this boundary group, select the server and then click **Change Connection**.  

         By default, the connection speed for each site system is **Fast**, but can be changed to **Slow**. The network connection speed and the configuration of a deployment determine whether a client can download content from the server.  

6.  Click **OK** to close the boundary group properties and save the configuration.  

#### To associate a content deployment server or management point with a boundary group  

1.  In the Configuration Manager console, click **Administration** > **Hierarchy Configuration** >  **Boundary Groups**.  

2.  Select the boundary group you want to modify.  

3.  On the **Home** tab, in the **Properties** group, click **Properties**.  

4.  In the **Properties** dialog box for the boundary group, select the **References** tab.  

5.  Under **Select site system servers**, click **Add**, select the check box for the site system servers you want to associate with this boundary group, and then click **OK**.  

6.  Click **OK** to close the dialog box and save the boundary group configuration.  

#### To enable use of preferred management points  

1.  In the Configuration Manager console, click **Administration** > **Site Configuration** > **Sites**, and then on the **Home** tab select  **Hierarchy Settings**.  

2.  On the **General** tab of the Hierarchy Settings, select **Clients prefer to use management points specified in boundary groups**.  

3.  Click **OK** to close the dialog box and save the configuration.  

#### To configure a fallback site for automatic site assignment  

1.  In the Configuration Manager console, click **Administration** > **Site Configuration** >  **Sites**.  

2.  On the **Home** tab, in the **Sites** group, click **Hierarchy Settings**.  

3.  On the **General** tab, select the checkbox for **Use a fallback site**, and then select a site from the **Fallback site** drop-down list.  

4.  Click **OK** to save the configuration.  

 The following sections provide additional details about boundary group configurations.  

###  <a name="BKMK_BoundarySiteAssignment"></a> About site assignment  
 You can configure each boundary group with an assigned site for clients.  

-   A newly installed client that uses automatic site assignment will join the assigned site of a boundary group that contains the client’s current network location.  

-   After assigning to a site, a client does not change its site assignment when it changes its network location. For example, if the client roams to a new network location that is represented by a boundary in a boundary group with a different site assignment, the client’s assigned site will remain unchanged.  

-   When Active Directory System Discovery discovers a new resource, network information for the discovered resource is evaluated against the boundaries in boundary groups. This process associates the new resource with an assigned site for use by the client push installation method.  

-   When a boundary is a member of multiple boundary groups that have different assigned sites, clients will randomly select one of the sites.  

-   Changes to a boundary groups assigned site only apply to new  site assignment actions. Clients that  previously  assigned to a site, do not re-evaluate their site assignment based on changes to the configuration of a boundary group (or to their own network location).  

For more information about client site assignment, see [Using Automatic Site Assignment for Computers](../../../../core/clients/deploy/assign-clients-to-a-site.md#BKMK_AutomaticAssignment) in [How to assign clients to a site in System Center Configuration Manager](../../../../core/clients/deploy/assign-clients-to-a-site.md).  

###  <a name="BKMK_BoundaryContentLocation"></a> About content location  
 You can configure each boundary group with one or more distribution points and state migration points, and you can associate the same distribution points and state migration points with multiple boundary groups.  

-   **During software distribution**, clients request a location for deployment content. Configuration Manager sends the client a list of distribution points that are associated with each boundary group that includes the current network location of the client.  

-   **During operating system deployment, clients** request a location to send or receive their state migration information. Configuration Manager sends the client a list of state migration points that are associated with each boundary group that includes the current network location of the client.  

This behavior enables the client to select the nearest server from which to transfer the content or state migration information.  

###  <a name="BKMK_PreferredMP"></a> About preferred management points  
 Preferred management points enable a client to identify a management point that is associated with its current network location (boundary).  

-   A client attempts to use a preferred management point from its assigned site before using a   management point from its  assigned site that is not configured as preferred.  

-   To use this option you must enable it for the hierarchy, and configure boundary groups at individual primary sites to include the management points that should be associated with that boundary group’s associated boundaries  

-   When preferred management points are configured and a client organizes its list of management points, the client places the preferred management points at the top of its list of assigned management points (which includes all management points from the client’s assigned site)  

> [!NOTE]  
>  When a client roams (which means to change its network locations such as  when a laptop travels to a remote office location) it might use a management point (or proxy management point) from the local site at its new location before attempting to use a management point from its assigned site (which includes the preferred management points).  See [Understand how clients find site resources and services for System Center Configuration Manager](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md) for more information.  

###  <a name="BKMK_BoundaryOverlap"></a> About overlapping boundaries  
 Configuration Manager supports overlapping boundary configurations for content location:  

-   **When a client requests content**, and the client network location belongs to multiple boundary groups, Configuration Manager sends the client a list of all distribution points that have the content.  

-   **When a client requests a server to send or receive its state migration information**, and the client network location belongs to multiple boundary groups, Configuration Manager sends the client a list of all state migration points that are associated with a boundary group that includes the current network location of the client.  

This behavior enables the client to select the nearest server from which to transfer the content or state migration information.  

###  <a name="BKMK_BoudnaryNetworkSpeed"></a> About network connection speed  
 You can set the  network connection speed for each site system server in a boundary group. This setting applies to clients that connect to a site system based on this boundary groups configuration. The same site system server can have a different connection speed set for it in different boundary groups.  

 By default, the network connection speed is configured as **Fast**, but it can also be configured as **Slow**. The network connection speed and the deployment configuration determine whether a client can download content from a distribution point when the client is in an associated boundary group.  

 For more information about how the network connection speed configuration affects how clients get content, see [Content source location scenarios](../../../../core/plan-design/hierarchy/content-source-location-scenarios.md).  

##  <a name="BKMK_BoundaryBestPractices"></a> Best practices for boundaries  

-   **Consider using the IP address range boundary type only when other boundary types cannot be used:**  

     When designing your boundary strategy, we recommend you use boundaries that are based on Active Directory sites before using other boundary types. Where boundaries based on Active Directory sites are not an option, then use IP subnet or IPv6 boundaries. If none of these options are available to you, then leverage IP address range boundaries. This is because the site evaluates boundary members periodically, and the query required to assess members of an IP address range requires a substantially larger use of SQL Server resources than queries that assess members of other boundary types.  

-   **Avoid overlapping boundaries for automatic site assignment:**  

     Although each boundary group supports both site assignment configurations and those for content location, it is a best practice to create a separate set of  boundary groups to use only for site assignment. Meaning: ensure that each boundary in a boundary group is not a member of another boundary group with a different site assignment. This is because:  

    -   A single  boundary can be included in multiple boundary groups  

    -   Each boundary group can be associated with a different primary site for site assignment  

    -   A client on a boundary that is a member of two different boundary groups with different site assignments will randomly select a site to join, which might not be the site you intend the client to join.  This configuration is called overlapping boundaries.  

     Overlapping boundaries is not a problem for content location, and instead is often a desired  configuration that provides clients additional resources or content locations they can use.  

## See Also  
 [Configure sites and hierarchies for System Center Configuration Manager](../../../../core/servers/deploy/configure/configure-sites-and-hierarchies.md)
