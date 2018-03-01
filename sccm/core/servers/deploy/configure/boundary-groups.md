---
title: "Define boundary groups"
titleSuffix: "Configuration Manager"
description: "Understand boundary groups that link clients to site systems in System Center Configuration Manager."
ms.custom: na
ms.date: 03/09/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 5db2926f-f03e-49c7-b44b-e89b1a5a6779
caps.latest.revision: 10
author: mestew
ms.author: mstewart
manager: dougeby

---
# Configure boundary groups for System Center Configuration Manager


*Applies to: System Center Configuration Manager (Current Branch)*

Use boundary groups in Configuration Manager to logically organize related network locations ([boundaries](/sccm/core/servers/deploy/configure/boundaries)) to make it easier to manage your infrastructure. Assign boundaries to boundary groups before using the boundary group.

By default, Configuration Manager creates a default site boundary group at each site.

To configure boundary groups, associate boundaries (network locations) and site system roles, like distribution points, to the boundary group. This configuration helps associate clients to site system servers like distribution points that are located near the clients on the network.

To increase the availability of site systems servers, like distribution points, to a wider range of network locations, assign the same boundary and the same server to multiple boundary groups.

Clients use a boundary group for:  

-   Automatic site assignment  
-   To find a site system server that can provide a service, including:
    - Distribution points for content location
    -	Software update points (beginning with version 1702)
    - State migration points
    - Preferred management points (If you use preferred management points, you must enable this option for the hierarchy and not from within the boundary group configuration. See [To enable use of preferred management points](#to-enable-use-of-preferred-management-points) in this topic.)

##  Boundary groups and relationships
For each boundary group in your hierarchy, you can assign:

-  One or more boundaries. A client's **current** boundary group is a network location that is defined as a boundary assigned to a specific boundary group. A client can have more than one current boundary group.
- One or more site system roles. Clients can always use site system roles associated with their current boundary group. Depending on additional configurations, they might be able to use site system roles in additional boundary groups.  

For each boundary group you create, you can configure a one-way link to another boundary group. The link is called a **relationship**. The boundary groups you link to are called **neighbor** boundary groups. A boundary group can have multiple relationships, each with a specific neighbor boundary group.

When a client fails to find an available site system server in its current boundary group, the configuration of each relationship determines when it begins to search a neighbor boundary group. This search of additional groups is called **fallback**.

## Fallback
To prevent problems when clients can't find an available site system in their current boundary group, define the relationship between boundary groups for fallback behavior. Fallback lets a client expand its search to additional boundary groups to find an available site system.

Relationships are configured on a boundary group properties **Relationships** tab. When you configure a relationship, you define a link to a neighbor boundary group. For each type of supported site system role, configure independent settings for fallback to the neighbor boundary group. For example, when you configure a relationship to a specific boundary group, set fallback for distribution points to occur after 20 minutes instead of the default of 120. For a more extensive example, see [Example of using boundary groups](#example-of-using-boundary-groups).

If a client fails to find an available site system role in its current boundary group, the client uses the fallback time in minutes. This fallback time determines when the client begins to search for an available site system associated with the neighbor boundary group.  

When a client can't find an available site system, and begins to search locations from neighbor boundary groups, it increases the pool of available site systems. The configuration of boundary groups and their relationships defines the client's use of this pool of available site systems.

- A boundary group can have more than one relationship. With multiple relationships, you can configure fallback for each type of site system to different neighbors to occur after different periods of time.    
- Clients only fallback to a boundary group that is a direct neighbor of their current boundary group.
- When a client is a member of multiple boundary groups, the current boundary group is defined as a union of all the client's boundary groups. The client falls back to neighbors of any of those original boundary groups.

### The default site boundary group
In addition to the boundary groups you create, each site has a default site boundary group that is created by Configuration Manager. This group is named ***Default-Site-Boundary-Group&lt;sitecode>***. For example, the group for site ABC would be named *Default-Site-Boundary-Group&lt;ABC>.*

For each boundary group you create, Configuration Manager automatically creates an implied link to each default site boundary group in the hierarchy.
-	The implied link is a default fallback option from a current boundary group to the sites default boundary group that has a default fallback time of 120 minutes.
-	For clients not in a boundary associated with any boundary group: to identify valid site system roles, use the default site boundary group from their assigned site.

To manage fallback to the default site boundary group:
- Open the properties of the site default boundary group, and change the values on the **Default Behavior** tab. Changes you make here apply to *all* implied links to this boundary group. These settings can be overridden when you configure the explicit link to this default site boundary group from another boundary group.
- Open the properties of a custom boundary group. Change the values for the explicit link to a default site boundary group. When you set a new time in minutes for fallback or block fallback, that change affects only the link you are configuring. Configuration of the explicit link overrides the settings on the **Default Behavior** tab of a default site boundary group.


## Site assignment  
 You can configure each boundary group with an assigned site for clients.  

-   A newly installed client that uses automatic site assignment joins the assigned site of a boundary group that contains the client's current network location.  
-   After assigning to a site, a client does not change its site assignment when it changes its network location. For example, if the client roams to a new network location represented by a boundary in a boundary group with a different site assignment, the client's assigned site remains unchanged.  
-   When Active Directory System Discovery discovers a new resource, network information for the discovered resource is evaluated against the boundaries in boundary groups. This process associates the new resource with an assigned site for use by the client push installation method.  
-   When a boundary is a member of multiple boundary groups that have different assigned sites, clients randomly select one of the sites.  
-   Changes to a boundary groups assigned site only apply to new  site assignment actions. Clients that previously  assigned to a site do not reevaluate their site assignment based on changes to the configuration of a boundary group (or to their own network location).  

For more information about client site assignment, see [Using Automatic Site Assignment for Computers](../../../../core/clients/deploy/assign-clients-to-a-site.md#BKMK_AutomaticAssignment) in [How to assign clients to a site in System Center Configuration Manager](../../../../core/clients/deploy/assign-clients-to-a-site.md).  

## Distribution points

When a client requests the location of a distribution point, Configuration Manager sends the client a list of site systems. These site systems are of the appropriate type associated with each boundary group that includes the clients current network location:

-   **During software distribution**, clients request a location for deployment content that is available from a distribution point, or other valid content source (like a client configured for Peer Cache).

-   **During operating system deployment**, clients request a location to send or receive their state migration information.  

During content deployment, if a client requests content that is not available from a source in its current boundary group, the client continues to request that content. The client tries different content sources in its current boundary group until it reaches the fallback period for a neighbor boundary group or the default site boundary group. If the client has not yet found content, it then expands its search for content sources to include the neighbor boundary groups.

If the content is distributed on-demand, and not available on a distribution point when requested by a client, the process to transfer the content to that distribution point begins. It is possible the client finds that server as a content source before falling back to use a neighbor boundary group.

## Software update points
Clients use boundary groups to find a new software update point. To control which servers a client can find, add individual software update points to different boundary groups.

If you update from a version prior to 1702, each site adds all existing software update points to the default site boundary group. This site update behavior maintains the prior client behavior to select a software update point from the pool of available servers. This behavior is maintained until you choose to add individual software update points to different boundary groups for controlled selection and fallback behavior.

If you install a new site, software update points are not added to the default site boundary group. Assign software update points to a boundary group so that clients can find and use them.

### Fallback for software update points
Fallback for software update points is configured like other site system roles, but has the following caveats:
- **New clients use boundary groups to select software update points.** New clients that you install select a software update point from those servers associated with the boundary groups you configure. This behavior replaces the previous behavior where clients select a software update point randomly from a list of the servers that share the client's forest.

- **Clients continue to use a last-known good software update point until they fallback to find a new one.** Clients that already have a software update point continue to use it until it can't be reached. This behavior includes continued use of a software update point that is not associated with the client's current boundary group.

  The continued use of an existing software update point even when that server is not in the client's current boundary group is intentional. When the software update point changes, the client synchronizes data with the new server, which causes significant network usage. If all clients switch to a new server at the same time, the delay in transition helps to avoid saturating your network.

- **A client always attempts to reach its last known-good software update point for 120 minutes before starting fallback.** After 120 minutes, if the client has not established contact, it then begins fallback. When fallback starts, the client receives a list of all software update points from its current boundary group. Additional software update points from neighbor and site default boundary groups are available based on fallback configurations.

### Fallback configurations for software update points
#### Beginning with version 1706   
You can configure **Fallback times (in minutes)** for software update points to be less than 120 minutes. However, the client still attempts to reach its original software update point for 120 minutes. Then it expands its search to additional servers. Boundary group fallback times start when the client first fails to reach its original server. When the client expands its search, the site provides any boundary groups configured for less than 120 minutes.

To block fallback for a software update point to a neighbor boundary group, configure the setting to **Never fallback**.

After failing to reach its original server for two hours, the client then uses a shorter cycle to establish a connection to a new software update point. This behavior enables the client to rapidly search through the expanding list of potential software update points.

 -  **Example of fallback:**  
    A client's current boundary group has fallback for software update points that is configured as *10* minutes for boundary group *A*, and *130* minutes for boundary group *B*. When the client fails to reach its last known-good software update point:
    -   The client attempts to reach only its original server for the next 120 minutes. After 10 minutes, the software update points from boundary group A are added to the pool of available servers. However, the client cannot attempt to contact them or any other server until the initial 120-minute period to reconnect with the original server has elapsed.
    -   After trying to locate that original software update point for 120 minutes, the client can then expand its search. At that time, the client adds servers to the available pool of software update points that are in it's current and any neighbor boundary groups configured for 120 minutes or less. This pool includes the servers in boundary group A which were previously added to the pool of available servers.
    -   	After 10 more minutes (130-minutes total time after the client first failed to reach its last known-good software update point), the client expands the search to include software update points from boundary group B.  

#### Prior to version 1706
Prior to version 1706, fallback configurations for software update points do not support a configurable time in minutes. Instead, fallback behavior is limited to:

  - **Fallback times (in minutes):** This option is grayed out for software update points and cannot be configured. It is set to 120 minutes.
  - 	**Never fallback:** You can block fallback for a software update point to a neighbor boundary group when you use this configuration.

When a client that already has a software update point fails to reach it, the client then falls back to find another. When using fallback, the client receives a list of all software update points from its current boundary group. If it fails to find an available server for 120 minutes, it then falls back to its neighbor boundary groups and the default site boundary group. Fallback to both boundary groups happens at the same time. The software update point's fallback time to neighbor groups is set to 120 minutes. You can't change this fallback time. 120 minutes is also the default period used for fallback to the default site boundary group. When a client falls back to both a neighbor and default site boundary group, the client attempts to contact software update points from the neighbor boundary group before trying to use one from the default site boundary group.

### Manually switch to a new software update point
In addition to using fallback, you can use *Client Notification* to manually force a device to switch to a new software update point.

When you switch to a new server, the devices use fallback to find that new server. Review your boundary group configurations. Ensure that your software update points are in the correct boundary groups before you start this change.

For more information, see [Manually switch clients to a new software update point](/sccm/sum/plan-design/plan-for-software-updates#manually-switch-clients-to-a-new-software-update-point).



## Management points
<!-- 1324594 -->
Starting in version 1802, configure fallback relationships for management points between boundary groups. This behavior provides greater control for the management points that clients use. On the **Relationships** tab of the boundary group properties, there is a column for management point. When you add a new fallback boundary group, the fallback time for the management point is currently always zero (0). This behavior is the same for the **Default Behavior** on the site default boundary group.

Previously, a common problem occurs when you have a protected management point in a secure network. Clients on the main corporate network receive policy that includes this protected management point, even though they cannot communicate with it across a firewall. To address this problem, use the **Never fallback** option to ensure that clients only fallback to management points with which they can communicate.

When upgrading the site to version 1802, Configuration Manager adds all non-internet-facing management points into the site default boundary group. This upgrade behavior ensures that older client versions continue to communicate with management points. In order to take full advantage of this feature, move your management points to the desired boundary groups.

Management point boundary group fallback does not change the behavior during client installation (ccmsetup.exe). If the command line does not specify the initial management point using the /MP parameter, the new client receives the full list of available management points. For its initial bootstrap process, the client uses the first management point it can access. Once the client registers with the site, it receives the management point list properly sorted with this new behavior. 

For clients to use this capability, enable the following setting: **Clients prefer to use management points specified in boundary groups** in **Hierarchy Settings**. 

> [!Note]
> Operating system deployment processes are not aware of boundary groups.

### Troubleshooting
New entries appear in the **LocationServices.log**. The **Locality** attribute identifies one of the following states:
- 0: Unknown
- 1: The specified management point is only in the site default boundary group for fallback
- 2: The specified management point is in a remote or neighbor boundary group. When the management point is in both a neighbor and the site default boundary groups, the locality is 2.
- 3: The specified management point is in the local or current boundary group. When the management point is in the current boundary group as well as either a neighbor or the site default boundary group, the locality is 3. If you do not enable the preferred management points setting in Hierarchy Settings, the locality is always 3 no matter which boundary group the management point is in.

Clients use local management points first (locality 3), remote second (locality 2), then fallback (locality 1). 

When a client receives five errors in 10 minutes and fails to communicate with a management point in its current boundary group, it tries to contact a management point in a neighbor or the site default boundary group. If the management point in the current boundary group later comes back online, the client will return to the local management point on the next refresh cycle. The refresh cycle is 24 hours, or when the Configuration Manager agent service restarts.




## Preferred management points

 Preferred management points enable a client to identify a management point that is associated with its current network location (boundary).  

-   A client attempts to use a preferred management point from its assigned site before using one not configured as preferred from its assigned site.  
-   To use this option, enable it for the hierarchy. Then configure boundary groups at individual primary sites. Include the management points that should be associated with that boundary group's associated boundaries.  
-   When you configure preferred management points, and a client organizes its list of management points, the client places the preferred management points at the top of its list. This list includes all management points from the client's assigned site.  

> [!NOTE]  
>  Client roaming means it changes its network locations. For example, when a laptop travels to a remote office location. When a client roams, it might use a management point or proxy management point from the local site at its new location before attempting to use a server from its assigned site. This list of servers from its assigned site includes the preferred management points. For more information, see [Understand how clients find site resources and services](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  

## Overlapping boundaries  
 Configuration Manager supports overlapping boundary configurations for content location. When the client network location belongs to multiple boundary groups:

-   When a client requests content, Configuration Manager sends the client a list of all distribution points that have the content.  
-   When a client requests a server to send or receive its state migration information, Configuration Manager sends the client a list of all state migration points associated with a boundary group that includes the current network location of the client.  

This behavior enables the client to select the nearest server from which to transfer the content or state migration information.  



## Example of using boundary groups
The following example uses a client searching for content from a distribution point. This example can be applied to other site system roles that use boundary groups. Keep in mind that software update points do not support configuration of fallback to a neighbor group, and always use a period of 120 minutes.

You create three boundary groups that do not share boundaries or site system servers:
-	Group BG_A with distribution points DP_A1 and DP_A2 associated to the group
-	Group BG_B with distribution points DP_B1 and DP_B2 associated to the group
-	Group BG_C with distribution points DP_C1 and DP_C2 associated to the group

Add the network locations of your clients as boundaries to only the BG_A boundary group. Then configure relationships from that boundary group to the other two boundary groups:
-	Configure distribution points for the first *neighbor* group (BG_B) to be used after 10 minutes. This group contains distribution points DP_B1 and DP_B2. Both are well connected to the first groups boundary locations.
-	Configure the second *neighbor* group (BG_C) to be used after 20 minutes. This group contains distribution points DP_C1 and DP_C2. Both are across a WAN from the other two boundary groups.
-	Also add to the sites default site boundary group another distribution point that is on the site server. This server is your least preferred content source location, but it is centrally located to all your boundary groups.

	Example of boundary groups and fallback times:

	 ![BG_Fallack](media/BG_Fallback.png)


With this configuration:
-	The client begins searching for content from distribution points in its *current* boundary group (BG_A). It searches each distribution point for two minutes, and then switches to the next distribution point in the boundary group. The clients pool of valid content source locations includes DP_A1 and DP_A2.
-	If the client fails to find content from its *current* boundary group after searching for 10 minutes, it then adds the distribution points from the BG_B boundary group to its search. It then continues to search for content from a distribution point in its combined pool of servers. This pool now includes servers from both the BG_A and BG_B boundary groups. The client continues to contact each distribution point for two minutes, and then switches to the next server in its pool. The clients pool of valid content source locations includes DP_A1, DP_A2, DP_B1, and DP_B2.
-	After an additional 10 minutes (20 minutes total), if the client still has not found a distribution point with content, it expands its pool to include available servers from the second *neighbor* group, boundary group BG_C. The client now has six distribution points to search (DP_A1, DP_A2, DP_B2, DP_B2, DP_C1, and DP_C2). It continues changing to a new distribution point every two minutes until it finds content.
-	If the client has not found content after a total of 120 minutes, it falls back to include the *default site boundary group* as part of its continued search. Now the pool includes all distribution points from the three configured boundary groups, and the final distribution point located on the site server. The client then continues its search for content, changing distribution points every two minutes until content is found.

By configuring the different neighbor groups to be available at different times, you control when specific distribution points are added as a content source location. The client uses fallback to the default site boundary group as a safety net for content that is not available from any other location.






### Update existing boundary groups to the new model
When you update to version prior to 1610, the following configurations are automatically made. This behavior ensures your current fallback behavior remains available until you configure new boundary groups and relationships.

-	Each primary site creates a default site boundary group named ***Default-Site-Boundary-Group&lt;sitecode>***.
  -	The primary site adds to the *Default-Site-Boundary-Group&lt;sitecode>* boundary group any state migration points and distribution points configured to **Allow fallback source location for content**.
  -	The site adds software update points to the *Default-Site-Boundary-Group&lt;sitecode>* boundary group.
-	The site makes a copy of each existing boundary group that includes a site server configured with a slow connection. The name of the new group is ***&lt;original boundary group name>-&lt;original boundary group ID>***:  
	-	Site systems that have a fast connection are left in the original boundary group.
	-	A copy of site systems (distribution points, management points) that have a slow connection are added to the copy of the boundary group. The original site systems configured as slow remain in their original boundary groups for backward compatibility, but are not used from those boundary groups.
	- This boundary group copy does not have boundaries associated with it. However, A fallback link is created between the original group and the new boundary group copy that has the fallback time set to zero.  


- **Specific to secondary sites:**
  - If a secondary site has at least one state migration point or distribution point enabled to **Allow fallback source location for content**, Configuration Manager creates a boundary group named ***Secondary-Site-Neighbor--Tmp&lt;Sitecode>***. 
  - All distribution points enabled to **Allow fallback source location for content** and state migration points are added to this secondary site boundary group.
  - A fallback link is created between the original boundary group and the newly created neighbor boundary group. The fallback time is set to zero.


 The following table identifies the new fallback behavior you can expect from the combination the original deployment settings and distribution point configurations:

Original deployment configuration for “Do not run program” in slow network  |Original distribution point configuration for “Allow client to use a fallback source location for content”  |New fallback behavior  
---------|---------|---------
Selected     |  Selected    |  **No fallback** - Only use the distribution points in current boundary group       
Selected     |  Not selected|  **No fallback** - Only use the distribution points in current boundary group       
Not selected |  Not selected|  **Fallback to neighbor** - Use the distribution points in current boundary group, and then add the distribution points from the neighbor boundary group. Unless an explicit link to the default site boundary group is configured, clients do not fallback to that group.    
Not selected | Selected		|   **Normal fallback** - Use distribution points in current boundary group, then servers from the neighbor and site default boundary groups

 All other deployment configurations result in **Normal fallback**.  




## Changes from prior versions for UI and behavior for content locations
The following are the key changes to boundary groups and how clients find content. These changes are introduced with version 1610. Many of these changes and concepts work together.


-	Configurations for Fast or Slow are removed: You no longer configure individual distribution points to be fast or slow. Instead, each site system associated with a boundary group is treated the same. Because of this change, the **References** tab of the boundary group properties no longer supports the configuration of Fast or Slow.
- New default boundary group at each site: Each primary site has a new default boundary group named ***Default-Site-Boundary-Group&lt;sitecode>***. When a client is not on a network location assigned to a boundary group, it uses the site systems associated with the default group from its assigned site. Plan to use this boundary group as a replacement to the concept of fallback content location.  	
 -	**Allow fallback source locations for content** is removed: You no longer explicitly configure a distribution point to be used for fallback. The options to configure this setting are removed from the console.

	Additionally, the result of setting **Allow clients to use a fallback source location for content** on a deployment type for applications has changed. This setting on a deployment type now enables a client to use the default site boundary group as a content source location.

 -	Boundary groups relationships: Each boundary group can be linked to one or more additional boundary groups. These links form relationships that are configured on the new boundary group properties tab named **Relationships**:
 	-	Each boundary group that a client is directly associated with is called a **current** boundary group.  
	- 	Any boundary group a client can use due to an association between that client's *current* boundary group and another group is called a **neighbor** boundary group.
	-  On the **Relationships** tab, add boundary groups to use as a *neighbor* boundary group. Also configure a time in minutes for fallback. When a client fails to find content from a distribution point in the *current* group, this time is when the client begins to search content locations from *neighbor* boundary groups.

		When you add or change a boundary group configuration, you have the option to block fallback to that specific boundary group from the current group you are configuring.

	To use the new configuration, define explicit associations (links) from one boundary group to another. Configure all distribution points in that associated group with the same time in minutes. When a client fails to find a content source from its *current* boundary group, the time you configure determines when it begins to search for content sources from its neighbor boundary group.

	In addition to boundary groups you explicitly configure, each boundary group has an implied link to the default site boundary group. This link becomes active after 120 minutes. Then the default site boundary group becomes a neighbor boundary group. This behavior allows the clients to use as content source locations the distribution points associated with that boundary group.

	This behavior replaces what was previously referred to as fallback for content. Override this default behavior of 120 minutes by explicitly associating the default site boundary group to a *current* group. Set a specific time in minutes, or block fallback entirely to prevent its use.


- 	Clients attempt to get content from each distribution point for up to two minutes: When a client searches for a content source location, it attempts to access each distribution point for two minutes before then trying another distribution point. This behavior is a change from previous versions where clients attempted to connect to a distribution point for up to two hours.

	- Clients randomly select the first distribution point from the pool of available servers in the client's *current* boundary group (or groups).

	- After two minutes, if the client has not found the content, it switches to a new distribution point and attempts to get content from that server. This process repeats every two minutes until the client finds the content or reaches the last server in its pool.

	- If a client cannot find a valid content source location from its *current* pool before it reaches the period for fallback to a *neighbor* boundary group, the client then adds the distribution points from that *neighbor* group to the end of its current list. It then searches the expanded group of source locations that includes the distribution points from both boundary groups.

		> [!TIP]  
		> When you create an explicit link from the current boundary group to the default site boundary group, and define a fallback time that is less than the fallback time for a link to a neighbor boundary group, clients begin searching source locations from the default site boundary group before including the neighbor group.

	- When the client fails to get content from the last server in the pool, it begins the process again.


## Procedures for boundary groups

### To create a boundary group  
1.  In the Configuration Manager console, click **Administration** > **Hierarchy Configuration** >  **Boundary Groups**.  

2.  On the **Home** tab, in the **Create** group, click **Create Boundary Group**.  

3.  In the **Create Boundary Group** dialog box, select the **General** tab, and specify a **Name** for this boundary group.  

4.  Click **OK** to save the new boundary group.  


### To configure a boundary group  
 1.  In the Configuration Manager console, click **Administration** > **Hierarchy Configuration** >  **Boundary Groups**.  

 2.  Select the boundary group you want to modify.  

 3.  On the **Home** tab, in the **Properties** group, click **Properties**.  

 4.  In the **Properties** dialog box for the boundary group, select the **General** tab to modify the boundaries that are members of this boundary group:  

     -   To add boundaries, click **Add**, select the check box for one or more boundaries, and click **OK**.  

     -   To remove boundaries, select the boundary and click **Remove**.  

 5.  Select the **References** tab to modify the site assignment and associated site system server configuration:  

     -   To enable this boundary group for use by clients for site assignment, select **Use this boundary group for site assignment**. Then select a site from the **Assigned site** dropdown list.  

     -   To configure which available site system servers are associated with this boundary group:  

     1.  Click **Add**, and then select the check box for one or more servers. The servers are added as associated site system servers for this boundary group. Only servers that have supported site system role installed on them are available.  

         > [!NOTE]  
         >  You can select any combination of available site systems from any site in the hierarchy. Selected site systems are listed on the **Site Systems** tab in the properties of each boundary that is a member of this boundary group.  

     2.  To remove a server from this boundary group, select the server and then click **Remove**.  

         > [!NOTE]  
         >  To stop use of this boundary group for associating site systems, remove all servers listed as associated site system servers.  

 6.  To configure fallback behavior, select the **Relationships** tab:  

     - Click **Add**, and then select the boundary group you want to configure.

     - Set a fallback time for distribution points. After this period of time, clients in the boundary group you are configuring relationships for, will be able to begin searching for content from the distribution points of the boundary group you are adding.

     - To prevent fallback to a specific boundary group, including the *default site boundary group* that is configured by default, select the boundary group, and then check the box for **Never fallback**.   

 7.  Click **OK** to close the boundary group properties and save the configuration.  

#### To associate a site system server with a boundary group  
 1.  In the Configuration Manager console, click **Administration** > **Hierarchy Configuration** >  **Boundary Groups**.  

 2.  Select the boundary group you want to modify.  

 3.  On the **Home** tab, in the **Properties** group, click **Properties**.  

 4.  In the **Properties** dialog box for the boundary group, select the **References** tab.  

 5.  Under **Select site system servers**, click **Add**. Select the site system servers to associate with this boundary group, and then click **OK**.  

 6.  Click **OK** to close the dialog box and save the boundary group configuration.  


#### To configure a fallback site for automatic site assignment  

  1.  In the Configuration Manager console, click **Administration** > **Site Configuration** >  **Sites**.  

  2.  On the **Home** tab, in the **Sites** group, click **Hierarchy Settings**.  

  3.  On the **General** tab, select the checkbox for **Use a fallback site**, and then select a site from the **Fallback site** drop-down list.  

  4.  Click **OK** to save the configuration.  

#### To enable use of preferred management points  

 1.  In the Configuration Manager console, click **Administration** > **Site Configuration** > **Sites**, and then on the **Home** tab select  **Hierarchy Settings**.  

 2.  On the **General** tab of the Hierarchy Settings, select **Clients prefer to use management points specified in boundary groups**.  

 3.  Click **OK** to close the dialog box and save the configuration.  
