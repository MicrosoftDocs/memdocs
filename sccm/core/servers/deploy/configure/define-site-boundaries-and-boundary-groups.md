---
title: "Define site boundaries | System Center Configuration Manager"
description: "Understand how to define network locations on your intranet that can contain devices you want to manage."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 54aa20d5-791e-4416-9db4-5aaea472c0b7
caps.latest.revision: 10
author: Brendunsms.author: brendunsmanager: angrobe

---
# Define site boundaries and boundary groups for System Center Configuration Manager*Applies to: System Center Configuration Manager (Current Branch)*
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

### To create a boundary  

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

### To configure a boundary  

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
> [!IMPORTANT]  
>  **The information in this Boundary groups section and its child sections applies to version 1610 or later.** This content has been revised to be specific to the design changes introduced for boundary groups with this update version.
>
> **If you use versions 1511, 1602, or 1606**, see [Boundary groups for System Center Configuration Manager versions 1511, 1602, and 1606](/sccm/core/servers/deploy/configure/boundary-groups-for-1511-1602-and-1606) for information on how to use and configure boundary groups with those product versions.

Version 1610 introduces important changes to boundary groups and how they work with distribution points. These changes help simplify the design of your content infrastructure while giving you more control over how and when clients fallback to search additional distribution points as content source locations. This includes both on-premises and cloud-based distribution points.

**About boundary groups:**  
 You create boundary groups to logically group related network locations (boundaries) to make it easier to manage your infrastructure. You must assign boundaries to boundary groups before you can use the boundary group. Clients use the boundary group configuration for:  

-   Automatic site assignment  
-   Content location  
-   Preferred management points  (If you will use preferred management points, you must enable this option for the hierarchy and not from within the boundary group configuration. See the following procedure [To enable use of preferred management points](#to-enable-use-of-preferred-management-points) in this topic.)  

When you configure boundary groups, you add one or more boundaries to the boundary group, and then configure additional settings for use by clients that are  located on those boundaries.  

You can find [procedures for managing boundary groups](#procedures-for-boundarygroups) later in this topic.


###  <a name="BKMK_BoundarySiteAssignment"></a> About site assignment  
 You can configure each boundary group with an assigned site for clients.  

-   A newly installed client that uses automatic site assignment will join the assigned site of a boundary group that contains the client's current network location.  
-   After assigning to a site, a client does not change its site assignment when it changes its network location. For example, if the client roams to a new network location that is represented by a boundary in a boundary group with a different site assignment, the client's assigned site will remain unchanged.  
-   When Active Directory System Discovery discovers a new resource, network information for the discovered resource is evaluated against the boundaries in boundary groups. This process associates the new resource with an assigned site for use by the client push installation method.  
-   When a boundary is a member of multiple boundary groups that have different assigned sites, clients will randomly select one of the sites.  
-   Changes to a boundary groups assigned site only apply to new  site assignment actions. Clients that  previously  assigned to a site, do not re-evaluate their site assignment based on changes to the configuration of a boundary group (or to their own network location).  

For more information about client site assignment, see [Using Automatic Site Assignment for Computers](../../../../core/clients/deploy/assign-clients-to-a-site.md#BKMK_AutomaticAssignment) in [How to assign clients to a site in System Center Configuration Manager](../../../../core/clients/deploy/assign-clients-to-a-site.md).  

###  <a name="BKMK_BoundaryContentLocation"></a> About content location  
When you configure boundary groups, you associate boundaries (network locations) and site system roles, like distribution points, to the boundary group. This helps link clients to site system servers like distribution points that are located near the clients on the network.

You can assign the same boundary to multiple boundary groups, and site system servers, like distribution points, can be associated to multiple boundary groups. This makes them available to a wider range of network locations.

-   **During software distribution**, clients request a location for deployment content. Configuration Manager sends the client a list of distribution points that are associated with each boundary group that includes the current network location of the client.  
-   **During operating system deployment**, clients request a location to send or receive their state migration information. Configuration Manager sends the client a list of state migration points that are associated with each boundary group that includes the current network location of the client.  

You define relationships between boundary groups to configure fallback behavior for content source locations. First introduced with version 1610, you configure realtionships on the new **Relationships** tab of the boundary group properties. Relationships replaces the need to configure site systems to be slow or fast, or to configure a boundary group to allow fallback source location for content.

When configuring a boundary group, which is called the **current** boundary group, you add other boundary groups to create a one-way link from the current boundary group to each boundary group you add. Boundary groups you add are called **neighbor** boundary groups. Then, for each link to a neighbor that you create, you can configure distribution points with a fallback time in minutes. This time is used to determine after how long clients in the current boundary group can begin using distribution points in the neighbor boundary group if clients are unable to find a valid content source location from their current boundary group.

When a client can’t find content and begins to search locations from neighbor boundary groups, it increases the pool of available distribution points for that client in a controlled manner.

-	A boundary group can have more than one Relationship. This lets you configure fallback to different neighbors to occur after different periods of time.
- 	Clients will only fallback to a boundary group that is a direct neighbor of their current boundary group.
-	When a client is a member of multiple boundary groups, the current boundary group is defined as a union of all that client’s boundary groups. That client can then fallback to a neighbor of any of those original boundary groups.

In addition to the links you define, there is an implied link that is created automatically between the boundary groups you create and the default boundary group that is automatically created for each site. This automatic link:
- 	Is used by clients that are not on a boundary associated with any boundary group in your hierarchy. Clients automatically use the default boundary group from their assigned site to identify valid content source locations.
- 	Is a default fallback option from the current boundary group to the sites default boundary group that is used after 120 minutes.

**Example of using the new model:**
You create three boundary groups that do not share boundaries or site system servers:
-	Group BG_A with distribution points DP_A1 and DP_A2 associated to the group
-	Group BG_B with distribution points DP_B1 and DP_B2 associated to the group
-	Group BG_C with distribution points DP_C1 and DP_C2 associated to the group

You add the network locations of your clients as boundaries to only the BG_A boundary group, and you then configure relationships from that boundary group to the other two boundary groups:
-	You configure distribution points for the first *neighbor* group (BG_B) to be used after 10 minutes. This group contains distribution points DP_B1 and DP_B2. Both are well connected to the first groups boundary locations.
-	You configure the second *neighbor* group (BG_C) to be used after 20 minutes. This group contains distribution points DP_C1 and DP_C2. Both are across a WAN from the other two boundary groups.
-	You also add an additional distribution point that is located on the site server to the sites default site boundary group. This is your least preferred content source location, but it is centrally located to all your boundary groups.

	Example of boundary groups and fallback times:

	 ![BG_Fallack](media/BG_Fallback.png)


With this configuration:
-	The client begins searching for content from distribution points in its *current* boundary group (BG_A), searching each distribution point for two minutes before switching to the next distribution point in the boundary group. The clients pool of valid content source locations includes DP_A1 and DP_A2.
-	If the client fails to find content from its *current* boundary group after searching for 10 minutes, it then adds the distribution points from the BG_B boundary group to its search. It then continues to search for content from a distribution point in its combined pool of distribution points that now includes those from both the BG_A and BG_B boundary groups. The client continues to contact each distribution point for two minutes before switching to the next distribution point from its pool. The clients pool of valid content source locations includes DP_A1, DP_A2, DP_B1, and DP_B2.
-	After an additional 10 minutes (20 minutes total) if the client still has not found a distribution point with content, it expands its pool of available distribution points to include those from the second *neighbor* group, boundary group BG_C. The client now has 6 distribution points to search (DP_A1, DP_A2, DP_B2, DP_B2, DP_C1, and DP_C2) and continues changing to a new distribution point every two minutes until content is found.
-	If the client has not found content after a total of 120 minutes, it falls back to include the *default site boundary group* as part of its continued search. Now the pool of distribution points includes all the distribution points from the three configured boundary groups and the final distribution point located on the site server computer.  The client then continues its search for content, changing distribution points every two minutes until content is found.

By configuring the different neighbor groups to be available at different times you control when specific distribution points are added as a content source location, and when, or if, the client uses fallback to the default site boundary group as a safety net for content that is not available from any other location.




### Update existing boundary groups to the new model
When you update to version 1610, the following configurations are automatically made. These are intended to ensure your current fallback behavior remains available, until you configure new boundary groups and relationships.
-	A default site boundary group is created for each primary site, the name is ***Default-Site-Boundary-Group\<sitecode>.***
-	Unprotected distribution points and state migration points at primary sites are added to the *Default-Site-Boundary-Group\<sitecode>* boundary group of that site.
-	A copy is made of each existing boundary group that includes a site server configured with a slow connection. The name of the new group is ***\<original boundary group name>-Slow-Tmp***:  
	-	Site systems that have a fast connection are left in the original boundary group.
	-	A copy of site systems (distribution points, management points, and state migration points) that have a slow connection are added to the copy of the boundary group. The original site systems configured as slow remain in their original boundary groups for backward compatibility, but are not used from those boundary groups.
	- 	This boundary group copy does not have boundaries associated with it. However, A fallback link is created between the original group and the new boundary group copy that has the fallback time set to zero.  


- **Specific to secondary sites:**
  - A boundary group is created if a secondary site has at least one unprotected distribution point or state migration point. The name of the boundary group is ***Secondary-Site-Neighbor--Tmp\<Sitecode>.***
  - All unprotected distribution points and state migration points are added to this newly created secondary site boundary group.
  - A fallback link is created between the original boundary group and the newly created neighbor boundary group and the fallback time is set to zero.


 The following table identifies the new fallback behavior you can expect from the combination the original deployment settings and distribution point configurations:

Original deployment configuration for “Do not run program” in slow network  |Original distribution point configuration for “Allow client to use a fallback source location for content”  |New fallback behavior  
---------|---------|---------
Selected     |  Selected    |  **No fallback** - Only use the distribution points in current boundary group       
Selected     |  Not selected|  **No fallback** - Only use the distribution points in current boundary group       
Not selected |  Not selected|  **Fallback to neighbor** - Use the distribution points in current boundary group, and then add the distribution points from the neighbor boundary group. Unless an explicit link to the default site boundary group is configured, clients will not fallback to that group.    
Not selected | Selected		|   **Normal fallback** - Use distribution points in current boundary group, then those from the neighbor and site default boundary groups

 All other deployment configurations result in **Normal fallback**.  



### Changes from prior versions for UI and behavior for content locations
The following are the key changes to boundary groups and how clients find content that are introduced with version 1610. Many of these changes and concepts work together.


-	**Configurations for Fast or Slow are removed:** You no longer configure individual distribution points to be fast or slow.  Instead, each site system associated with a boundary group is treated the same. Because of this change, the **References** tab of the boundary group properties no longer supports the configuration of Fast or Slow.
- 	**New default boundary group at each site:**  Each primary site has a new default boundary group named ***Default-Site-Boundary-Group\<sitecode>***.  When a client is not on a network location that is assigned to a boundary group, that client will use the site systems associated with the default group from its assigned site. Plan to use this boundary group as a replacement to the concept of fallback content location.  	
 -	**‘Allow fallback source locations for content’** is removed: You no longer explicitly configure a distribution point to be used for fallback, and the options to set this are removed from the UI.

	Additionally, the result of setting **Allow clients to use a fallback source location for content** on a deployment type for applications has changed. This setting on a deployment type now enables a client to use the default site boundary group as a content source location.

 -	**Boundary groups relationships:** Each boundary group can be linked to one or more additional boundary groups. These links form relationships that are configured on the new boundary group properties tab named **Relationships**:
 	-	Each boundary group that a client is directly associated with is called a **current** boundary group.  
	- 	Any boundary group a client can use due to an association between that client’s *current* boundary group and another group is called a **neighbor** boundary group.
	-  It is on the **Relationships** tab that you add boundary groups that can be used as a *neighbor* boundary group. You can also configure a time in minutes that determines when a client that fails to find content from a distribution point in the *current* group will begin to search content locations from those *neighbor* boundary groups.

		When you add or change a boundary group configuration, you will have the option to block fallback to that specific boundary group from the current group you are configuring.

	To use the new configuration, you define explicit associations (links) from one boundary group to another, and configure all distribution points in that associated group with the same time in minutes. The time you configure determines when a client that fails to find a content source from its *current* boundary group can begin to search for content sources from that neighbor boundary group.

	In addition to boundary groups you explicitly configure, each boundary group has an implied link to the default site boundary group. This link becomes active after 120 minutes at which time the default site boundary group becomes a neighbor boundary group which allows the clients to use the distribution points associated with that boundary group as content source locations.

	This behavior replaces what was previously referred to as fallback for content.  You can override this default behavior of 120 minutes by explicitly associating the default site boundary group to a *current* group, and setting a specific time in minutes, or blocking fallback entirely to prevent its use.


- 	**Clients attempt to get content from each distribution point for up to 2 minutes:** When a client searches for a content source location, it attempts to access each distribution point for 2 minutes before then trying another distribution point. This is a change from previous versions where clients attempted to connect to a distribution point for up to 2 hours.

	- The first distribution point that a client attempts to use is randomly selected from the pool of available distribution points in the client’s *current* boundary group (or groups).

	- After two minutes, if the client has not found the content, it switches to a new distribution point and attempts to get content from that server. This process repeats every two minutes until the client finds the content or reaches the last server in its pool.

	- If a client cannot find a valid content source location from its *current* pool before the period for fallback to a *neighbor* boundary group is reached, the client then adds the distribution points from that *neighbor* group to the end of its current list, and will then search the expanded group of source locations that includes the distribution points from both boundary groups.

		> [!TIP]  
		> When you create an explicit link from the current boundary group to the default site boundary group and define a fallback time that is less than the fallback time for a link to a neighbor boundary group, clients will begin searching source locations from the default site boundary group before including the neighbor group.

	- When the client fails to get content from the last server in the pool, it begins the process again.





###  <a name="BKMK_PreferredMP"></a> About preferred management points  
 Preferred management points enable a client to identify a management point that is associated with its current network location (boundary).  

-   A client attempts to use a preferred management point from its assigned site before using a management point from its assigned site that is not configured as preferred.  
-   To use this option you must enable it for the hierarchy, and configure boundary groups at individual primary sites to include the management points that should be associated with that boundary group's associated boundaries  
-   When preferred management points are configured and a client organizes its list of management points, the client places the preferred management points at the top of its list of assigned management points (which includes all management points from the client's assigned site)  

> [!NOTE]  
>  When a client roams (which means to change its network locations such as  when a laptop travels to a remote office location) it might use a management point (or proxy management point) from the local site at its new location before attempting to use a management point from its assigned site (which includes the preferred management points).  See [Understand how clients find site resources and services for System Center Configuration Manager](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md) for more information.  

###   <a name="BKMK_BoundaryOverlap"></a> About overlapping boundaries  
 Configuration Manager supports overlapping boundary configurations for content location:  

-   **When a client requests content**, and the client network location belongs to multiple boundary groups, Configuration Manager sends the client a list of all distribution points that have the content.  
-   **When a client requests a server to send or receive its state migration information**, and the client network location belongs to multiple boundary groups, Configuration Manager sends the client a list of all state migration points that are associated with a boundary group that includes the current network location of the client.  

This behavior enables the client to select the nearest server from which to transfer the content or state migration information.  






## Procedures for boundary groups
The following procedures apply to version 1610 or later. If you use version 1511, 1602, or 1606, see the procedures in [Boundary groups for System Center Configuration Manager versions 1511, 1602, and 1606](/sccm/core/servers/deploy/configure/boundary-groups-for-1511-1602-and-1606).


### To create a boundary group  
1.  In the Configuration Manager console, click **Administration** > **Hierarchy Configuration** >  **Boundary Groups**.  

2.  On the **Home** tab, in the **Create** group, click **Create Boundary Group**.  

3.  In the **Create Boundary Group** dialog box, select the **General** tab and specify a **Name** for this boundary group.  

4.  Click **OK** to save the new boundary group.  


### To configure a boundary group  
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

##  <a name="BKMK_BoundaryBestPractices"></a> Best practices for boundaries  

-   **Consider using the IP address range boundary type only when other boundary types cannot be used:**  
     When designing your boundary strategy, we recommend you use boundaries that are based on Active Directory sites before using other boundary types. Where boundaries based on Active Directory sites are not an option, then use IP subnet or IPv6 boundaries. If none of these options are available to you, then leverage IP address range boundaries. This is because the site evaluates boundary members periodically, and the query required to assess members of an IP address range requires a substantially larger use of SQL Server resources than queries that assess members of other boundary types.  

-   **Avoid overlapping boundaries for automatic site assignment:**  
     Although each boundary group supports both site assignment configurations and those for content location, it is a best practice to create a separate set of  boundary groups to use only for site assignment. Meaning: ensure that each boundary in a boundary group is not a member of another boundary group with a different site assignment. This is because:  

    -   A single  boundary can be included in multiple boundary groups  

    -   Each boundary group can be associated with a different primary site for site assignment  

    -   A client on a boundary that is a member of two different boundary groups with different site assignments will randomly select a site to join, which might not be the site you intend the client to join.  This configuration is called overlapping boundaries.  

     Overlapping boundaries is not a problem for content location, and instead is often a desired  configuration that provides clients additional resources or content locations they can use.  
