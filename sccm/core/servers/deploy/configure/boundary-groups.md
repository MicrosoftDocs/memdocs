---
title: Configure boundary groups
titleSuffix: Configuration Manager
description: Help clients find site systems by using boundary groups to logically organize related network locations called boundaries
ms.date: 11/16/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 5db2926f-f03e-49c7-b44b-e89b1a5a6779
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Configure boundary groups for Configuration Manager


*Applies to: System Center Configuration Manager (Current Branch)*

Use boundary groups in Configuration Manager to logically organize related network locations ([boundaries](/sccm/core/servers/deploy/configure/boundaries)) to make it easier to manage your infrastructure. Assign boundaries to boundary groups before using the boundary group.

By default, Configuration Manager creates a default site boundary group at each site.

To configure boundary groups, associate boundaries (network locations) and site system roles, like distribution points, to the boundary group. This configuration helps associate clients to site system servers like distribution points that are located near the clients on the network.

To increase the availability of servers to a wider range of network locations, assign the same boundary and the same server to more than one boundary group.

Clients use a boundary group for:  

-   Automatic site assignment  
-   To find a site system server that can provide a service, including:  
    - Distribution points for content location  
    - Software update points  
    - State migration points  
    - Preferred management points  

        > [!Note]  
        > If you use preferred management points, enable this option for the hierarchy, not from within the boundary group configuration. For more information, see [Enable use of preferred management points](#to-enable-use-of-preferred-management-points).  



##  Boundary groups and relationships

For each boundary group in your hierarchy, you can assign:

- One or more boundaries. A client's **current** boundary group is a network location that's defined as a boundary assigned to a specific boundary group. A client can have more than one current boundary group.  

- One or more site system roles. Clients can always use roles associated with their current boundary group. Depending on additional configurations, they can use roles in additional boundary groups.  

For each boundary group you create, you can configure a one-way link to another boundary group. The link is called a **relationship**. The boundary groups you link to are called **neighbor** boundary groups. A boundary group can have more than one relationship, each with a specific neighbor boundary group.

When a client fails to find an available site system in its current boundary group, the configuration of each relationship determines when it begins to search a neighbor boundary group. This search of additional groups is called **fallback**.

For more information, see the following procedures:  
- [Create a boundary group](/sccm/core/servers/deploy/configure/boundary-group-procedures#bkmk_create)  
- [Configure a boundary group](/sccm/core/servers/deploy/configure/boundary-group-procedures#bkmk_config)  



## Fallback

To prevent problems when clients can't find an available site system in their current boundary group, define the relationship between boundary groups for fallback behavior. Fallback lets a client expand its search to additional boundary groups to find an available site system.

Relationships are configured on a boundary group properties **Relationships** tab. When you configure a relationship, you define a link to a neighbor boundary group. For each type of supported site system role, configure independent settings for fallback to the neighbor boundary group. For more information, see [Configure fallback behavior](/sccm/core/servers/deploy/configure/boundary-group-procedures#bkmk_bg-fallback).

For example, when you configure a relationship to a specific boundary group, set fallback for distribution points to occur after 20 minutes. The default is 120 minutes For a more extensive example, see [Example of using boundary groups](#example-of-using-boundary-groups).

If a client fails to find an available site system role in its current boundary group, the client uses the fallback time in minutes. This fallback time determines when the client begins to search for an available site system associated with the neighbor boundary group.  

When a client can't find an available site system, it begins to search locations from neighbor boundary groups. This behavior increases the pool of available site systems. The configuration of boundary groups and their relationships defines the client's use of this pool of available site systems.

- A boundary group can have more than one relationship. With this configuration, you can configure fallback for each type of site system to different neighbors to occur after different periods of time.    

- Clients only fallback to a boundary group that's a direct neighbor of their current boundary group.  

- When a client is a member of more than one boundary group, it defines its current boundary group as a union of all its boundary groups. The client falls back to neighbors of any of those original boundary groups.  


### The default site boundary group

You can create your own boundary groups, and each site has a default site boundary group that Configuration Manager creates. This group is named **Default-Site-Boundary-Group&lt;sitecode>**. For example, the group for site ABC would be named **Default-Site-Boundary-Group&lt;ABC>**.

For each boundary group you create, Configuration Manager automatically creates an implied link to each default site boundary group in the hierarchy.  

- The implied link is a default fallback option from a current boundary group to the site's default boundary group. The default fallback time is 120 minutes.  

- For clients not in a boundary associated with any boundary group: to identify valid site system roles, use the default site boundary group from their assigned site.  


To manage fallback to the default site boundary group:  

- Open the properties of the site default boundary group, and change the values on the **Default Behavior** tab. Changes you make here apply to *all* implied links to this boundary group. When you configure an explicit link to this default site boundary group from another boundary group, you override these default settings.  

- Open the properties of a custom boundary group. Change the values for the explicit link to a default site boundary group. When you set a new time in minutes for fallback or block fallback, that change affects only the link you're configuring. Configuration of the explicit link overrides the settings on the **Default Behavior** tab of a default site boundary group.  



## Site assignment  

 You can configure each boundary group with an assigned site for clients.  

-   A newly installed client that uses automatic site assignment joins the assigned site of a boundary group that contains the client's current network location.  

-   After assigning to a site, a client doesn't change its site assignment when it changes its network location. For example, a client roams to a new network location. This location is a boundary in a boundary group with a different site assignment. The client's assigned site doesn't change.  

-   When Active Directory System Discovery discovers a new resource, the site evaluates network information for the resource against the boundaries in boundary groups. This process associates the new resource with an assigned site for use by the client push installation method.  

-   When a boundary is a member of more than one boundary groups that have different assigned sites, clients randomly select one of the sites.  

-   Changes to a boundary groups assigned site only apply to new site assignment actions. Clients that previously assigned to a site don't reevaluate their site assignment based on changes to the configuration of a boundary group (or to their own network location).  

For more information about client site assignment, see [Using automatic site assignment for computers](/sccm/core/clients/deploy/assign-clients-to-a-site#BKMK_AutomaticAssignment).  

For more information on how to configure site assignment, see the following procedures:
- [Configure site assignment and select site system servers](/sccm/core/servers/deploy/configure/boundary-group-procedures#bkmk_references)
- [Configure a fallback site for automatic site assignment](/sccm/core/servers/deploy/configure/boundary-group-procedures#bkmk_site-fallback)



## Distribution points

When a client requests the location of a distribution point, Configuration Manager sends the client a list of site systems. These site systems are of the appropriate type associated with each boundary group that includes the client's current network location:

-   **During software distribution**, clients request a location for deployment content on a valid content source. This location may be a distribution point, or a peer cache source.  

-   **During OS deployment**, clients request a location to send or receive their state migration information.  

    - Starting in version 1810, clients acquire content based on boundary group behaviors. For more information, see [Task sequence support for boundary groups](#bkmk_bgr-osd).  

During content deployment, if a client requests content that isn't available from a source in its current boundary group, the client continues to request that content. The client tries different content sources in its current boundary group until it reaches the fallback period for a neighbor or the default site boundary group. If the client still hasn't found content, it then expands its search for content sources to include the neighbor boundary groups.

If you configure the content to distribute on-demand, and it isn't available on a distribution point when a client requests it, the site begins to transfer the content to that distribution point. It's possible the client finds that server as a content source before falling back to use a neighbor boundary group.


### <a name="bkmk_ccmsetup"></a> Client installation
<!--1358840-->

When installing the Configuration Manager client, the ccmsetup process contacts the management point to locate the necessary content. During this process in versions 1806 and earlier, the management point only returns distribution points in the client's current boundary group. If no content is available, the setup process falls back to download content from the management point. There's no option to fall back to distribution points in other boundary groups that might have the necessary content. 

Starting in version 1810, the management point returns distribution points based on boundary group configuration. If you define relationships on the boundary group, the management point returns distribution points in the following order:
1. Current boundary group  
2. Neighbor boundary groups  
3. The site default boundary group  

> [!Note]  
> The client setup process doesn't use the fallback time. To locate content as quickly as possible, it immediately falls back to the next boundary group.  


### <a name="bkmk_bgr-osd"></a> Task sequence support for boundary groups
<!--1359025-->

Starting in version 1810, when a device runs a task sequence and needs to acquire content, it now uses boundary group behaviors similar to the Configuration Manager client.   

Configure this behavior using the following settings on the **Distribution Points** page of the task sequence deployment: 

- **When no local distribution point is available, use a remote distribution point**: For this deployment, the task sequence can fall back to distribution points in a neighbor boundary group.  

- **Allow clients to use distribution points from the default site boundary group**: For this deployment, the task sequence can fall back to distribution points in the default site boundary group.  

To use this new behavior, make sure to update clients to the latest version.

#### Location priority  

The task sequence tries to acquire content in the following order:  

1. Peer cache sources  

2. Distribution points in the *current* boundary group  

3. Distribution points in a *neighbor* boundary group  

    > [!Important]  
    > Due to the real-time nature of task sequence processing, it doesn't wait for the failover time on a neighbor boundary group. It uses the failover times for prioritizing the neighbor boundary groups. For example, if the task sequence fails to acquire content from a distribution point in its current boundary group, it immediately tries a distribution point in a neighbor boundary group with the shortest failover time. If that process fails, it then fails over to a distribution point in a neighbor boundary group with a larger failover time.  

4. Distribution points in the *site default* boundary group  

The task sequence log file **smsts.log** shows the priority of the location sources that it uses based on the deployment properties.


### <a name="bkmk_bgoptions"></a> Boundary group options for peer downloads

<!--1356193-->
Starting in version 1806, boundary groups include the following additional settings to give you more control over content distribution in your environment:  

- [Allow peer downloads in this boundary group](#bkmk_bgoptions1)  

- [During peer downloads, only use peers within the same subnet](#bkmk_bgoptions2)  

<!--1358749-->
Version 1810 adds the following options:  

- [Prefer distribution points over peers with the same subnet](#bkmk_bgoptions3)  

- [Prefer cloud distribution points over distribution points](#bkmk_bgoptions4)  

For more information on how to configure these settings, see [Configure a boundary group](/sccm/core/servers/deploy/configure/boundary-group-procedures#bkmk_config).


#### <a name="bkmk_bgoptions1"></a> Allow peer downloads in this boundary group
This setting is enabled by default. The management point provides clients a list of content locations that includes peer sources. This setting also affects applying Group IDs for [Delivery Optimization](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management#delivery-optimization).  

There are two common scenarios in which you should consider disabling this option:  

- If you have a boundary group that includes boundaries from geographically dispersed locations such as a VPN. Two clients may be in the same boundary group because they're connected through VPN, but in vastly different locations that are inappropriate for peer sharing of content.  

- If you use a single, large boundary group for site assignment that doesn't reference any distribution points.  

#### <a name="bkmk_bgoptions2"></a> During peer downloads, only use peers within the same subnet
This setting is dependent upon the preceding option. If you enable this option, the management point only includes in the content location list peer sources that are in the same subnet as the client.

Common scenarios for enabling this option:

- Your boundary group design for content distribution includes one large boundary group that overlaps other smaller boundary groups. With this new setting, the list of content sources that the management point provides to clients only includes peer sources from the same subnet.

- You have a single large boundary group for all remote office locations. Enable this option and clients only share content within the subnet at the remote office location, instead of risking sharing content between locations.

#### <a name="bkmk_bgoptions3"></a> Prefer distribution points over peers with the same subnet
By default, the management point prioritizes peer cache sources at the top of the list of content locations. This setting reverses that priority for clients that are in the same subnet as the peer cache source.  

#### <a name="bkmk_bgoptions4"></a> Prefer cloud distribution points over distribution points
If you have a branch office with a faster internet link, you can now prioritize cloud content.  



## Software update points

Clients use boundary groups to find a new software update point. To control which servers a client can find, add individual software update points to different boundary groups.

If you update from a version prior to 1702, each site adds all existing software update points to the default site boundary group. This site update behavior maintains the prior client behavior to select a software update point from the pool of available servers. This behavior is maintained until you choose to add individual software update points to different boundary groups for controlled selection and fallback behavior.

If you install a new site, software update points aren't added to the default site boundary group. Assign software update points to a boundary group so that clients can find and use them.


### Fallback for software update points

Fallback for software update points is configured like other site system roles, but has the following caveats:  

#### New clients use boundary groups to select software update points
When you install new clients, they select a software update point from those servers associated with the boundary groups you configure. This behavior replaces the previous behavior where clients select a software update point randomly from a list of the servers that share the client's forest.

#### Clients continue to use a last known-good software update point until they fallback to find a new one
Clients that already have a software update point continue to use it until it can't be reached. This behavior includes continued use of a software update point that isn't associated with the client's current boundary group.

This behavior is intentional. The client continues to use an existing software update point, even when it isn't in the client's current boundary group. When the software update point changes, the client synchronizes data with the new server, which causes significant network usage. If all clients switch to a new server at the same time, the delay in transition helps to avoid saturating your network.

#### A client always tries to reach its last known-good software update point for 120 minutes before starting fallback
After 120 minutes, if the client hasn't established contact, it then begins fallback. When fallback starts, the client receives a list of all software update points in its current boundary group. Additional software update points in neighbor and site default boundary groups are available based on fallback configurations.


### Fallback configurations for software update points

You can configure **Fallback times (in minutes)** for software update points to be less than 120 minutes. However, the client still tries to reach its original software update point for 120 minutes. Then it expands its search to additional servers. Boundary group fallback times start when the client first fails to reach its original server. When the client expands its search, the site provides any boundary groups configured for less than 120 minutes.

To block fallback for a software update point to a neighbor boundary group, configure the setting to **Never fallback**.

After failing to reach its original server for two hours, the client then uses a shorter cycle to establish a connection to a new software update point. This behavior enables the client to rapidly search through the expanding list of potential software update points.

#### Example
You configure software update points in boundary group *A* to fallback after **10** minutes. You configure the same setting for boundary group *B* to **130** minutes. A client in boundary group *Z* fails to reach its last known-good software update point.

- For the next 120 minutes, the client tries to reach only its original server in boundary group Z. After 10 minutes, Configuration Manager adds the software update points from boundary group A to the pool of available servers. However, the client doesn't try to contact them or any other server until the initial 120-minute period elapses.  

- After trying to contact the original software update point for 120 minutes, the client expands its search. It adds servers to the available pool of software update points that are in it's current and any neighbor boundary groups configured for 120 minutes or less. This pool includes the servers in boundary group A, which were previously added to the pool of available servers.  

- After 10 more minutes, the client expands the search to include software update points from boundary group B. This period is 130 minutes of total time after the client first failed to reach its last known-good software update point.  


### Manually switch to a new software update point

Along with fallback, use client notification to manually force a device to switch to a new software update point.

When you switch to a new server, the devices use fallback to find that new server. Review your boundary group configurations. Before you start this change, make sure that your software update points are in the correct boundary groups.

For more information, see [Manually switch clients to a new software update point](/sccm/sum/plan-design/plan-for-software-updates#manually-switch-clients-to-a-new-software-update-point).



## Management points
<!-- 1324594 -->
Starting in version 1802, configure fallback relationships for management points between boundary groups. This behavior provides greater control for the management points that clients use. On the **Relationships** tab of the boundary group properties, there's a column for management point. When you add a new fallback boundary group, the fallback time for the management point is currently always zero (0). This behavior is the same for the **Default Behavior** on the site default boundary group.

Previously, a common problem occurs when you have a protected management point in a secure network. Clients on the main corporate network receive policy that includes this protected management point, even though they can't communicate with it across a firewall. To address this problem, use the **Never fallback** option to make sure that clients only fallback to management points with which they can communicate.

When upgrading the site to version 1802, Configuration Manager adds all intranet management points into the site default boundary group. (This group of servers doesn't include management points that are only internet-facing.) This upgrade behavior makes sure that older client versions continue to communicate with management points. To take full advantage of this feature, move your management points to the desired boundary groups.

> [!Note]  
> If you enable distribution points in the site default boundary group to fallback, and a management point is colocated on a distribution point, the site also adds that management point to the site default boundary group.<!--VSO 2841292-->  

If a client is in a boundary group that with no assigned management point, the site gives the client the entire list of management points. This behavior makes sure that a client always receives a list of management points.

Management point boundary group fallback doesn't change the behavior during client installation (ccmsetup.exe). If the command line doesn't specify the initial management point using the /MP parameter, the new client receives the full list of available management points. For its initial bootstrap process, the client uses the first management point it can access. Once the client registers with the site, it receives the management point list properly sorted with this new behavior. 

For more information on the client's behavior to acquire content during installation, see [Client installation](#bkmk_ccmsetup).

During client upgrade, if you don't specify the /MP command-line parameter, the client queries sources such as Active Directory and WMI for any available management point. Client upgrade doesn't honor the boundary group configuration. <!--VSO 2841292-->  

For clients to use this capability, enable the following setting: **Clients prefer to use management points specified in boundary groups** in **Hierarchy Settings**. 

> [!Note]  
> OS deployment processes aren't aware of boundary groups for management points.  


### Troubleshooting

New entries appear in the **LocationServices.log**. The **Locality** attribute identifies one of the following states:

- **0**: Unknown  

- **1**: The specified management point is only in the site default boundary group for fallback  

- **2**: The specified management point is in a remote or neighbor boundary group. When the management point is in both a neighbor and the site default boundary groups, the locality is 2.  

- **3**: The specified management point is in the local or current boundary group. When the management point is in the current boundary group and either a neighbor or the site default boundary group, the locality is 3. If you don't enable the preferred management points setting in Hierarchy Settings, the locality is always 3 no matter which boundary group the management point is in.  

Clients use local management points first (locality 3), remote second (locality 2), then fallback (locality 1). 

When a client receives five errors in 10 minutes and fails to communicate with a management point in its current boundary group, it tries to contact a management point in a neighbor or the site default boundary group. If the management point in the current boundary group later comes back online, the client returns to the local management point on the next refresh cycle. The refresh cycle is 24 hours, or when the Configuration Manager agent service restarts.



## <a name="bkmk_preferred"></a> Preferred management points

 > [!Note]
 > The behavior of this hierarchy setting, **Clients prefer to use management points specified in boundary groups**, changes starting in version 1802. When you enable this setting, Configuration Manager uses the boundary group functionality for the assigned management point. For more information, see [management points](#management-points). 

 Preferred management points enable a client to identify a management point that's associated with its current network location (boundary).  

- A client tries to use a preferred management point from its assigned site before using one not configured as preferred from its assigned site.  

- To use this option, enable **Clients prefer to use management points specified in boundary groups** in **Hierarchy Settings**. Then configure boundary groups at individual primary sites. Include the management points that should be associated with that boundary group's associated boundaries. For more information, see [Enable use of preferred management points](/sccm/core/servers/deploy/configure/boundary-group-procedures#bkmk_proc-prefer).  

- When you configure preferred management points, and a client organizes its list of management points, the client places the preferred management points at the top of its list. This list includes all management points from the client's assigned site.  

> [!NOTE]  
>  Client roaming means it changes its network locations. For example, when a laptop travels to a remote office location. When a client roams, it might use a management point from the local site before attempting to use a server from its assigned site. This list of servers from its assigned site includes the preferred management points. For more information, see [Understand how clients find site resources and services](/sccm/core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services).  



## Overlapping boundaries  

 Configuration Manager supports overlapping boundary configurations for content location. When the client's network location belongs to more than one boundary group:

-   When a client requests content, Configuration Manager sends the client a list of all distribution points that have the content.  

-   When a client requests a server to send or receive its state migration information, Configuration Manager sends the client a list of all state migration points associated with a boundary group that includes the current network location of the client.  

This behavior enables the client to select the nearest server from which to transfer the content or state migration information.  



## Example of using boundary groups

The following example uses a client searching for content from a distribution point. This example can be applied to other site system roles that use boundary groups. 

Create three boundary groups that don't share boundaries or site system servers:  

- Group BG_A with distribution points DP_A1 and DP_A2   

- Group BG_B with distribution points DP_B1 and DP_B2  

- Group BG_C with distribution points DP_C1 and DP_C2  

Add the network locations of your clients as boundaries to only the BG_A boundary group. Then configure relationships from that boundary group to the other two boundary groups:  

- Configure distribution points for the first *neighbor* group (BG_B) to be used after 10 minutes. This group contains distribution points DP_B1 and DP_B2. Both are well connected to the first group's boundary locations.  

- Configure the second *neighbor* group (BG_C) to be used after 20 minutes. This group contains distribution points DP_C1 and DP_C2. Both are across a WAN from the other two boundary groups.  

- Also add to the default site boundary group another distribution point that's on the site server. This server is your least preferred content source location, but it's centrally located to all your boundary groups.

	Example of boundary groups and fallback times:

	 ![Example of boundary groups and fallback times](media/BG_Fallback.png)


With this configuration:  

- The client begins searching for content from distribution points in its *current* boundary group (BG_A). It searches each distribution point for two minutes, and then switches to the next distribution point in the boundary group. The client's pool of valid content source locations includes DP_A1 and DP_A2.  

- If the client fails to find content from its *current* boundary group after searching for 10 minutes, it then adds the distribution points from the BG_B boundary group to its search. It then continues to search for content from a distribution point in its combined pool of servers. This pool now includes servers from both the BG_A and BG_B boundary groups. The client continues to contact each distribution point for two minutes, and then switches to the next server in its pool. The client's pool of valid content source locations includes DP_A1, DP_A2, DP_B1, and DP_B2.  

- After an additional 10 minutes (20 minutes total), if the client still hasn't found a distribution point with content, it expands its pool to include available servers from the second *neighbor* group, boundary group BG_C. The client now has six distribution points to search: DP_A1, DP_A2, DP_B2, DP_B2, DP_C1, and DP_C2. It continues changing to a new distribution point every two minutes until it finds content.  

- If the client hasn't found content after a total of 120 minutes, it falls back to include the *default site boundary group* as part of its continued search. Now the pool includes all distribution points from the three configured boundary groups, and the final distribution point located on the site server. The client then continues its search for content, changing distribution points every two minutes until content is found.  

By configuring the different neighbor groups to be available at different times, you control when specific distribution points are added as a content source location. The client uses fallback to the default site boundary group as a safety net for content that isn't available from any other location.



## Changes from prior versions

The following are the key changes to boundary groups and how clients find content in Configuration Manager current branch. Many of these changes and concepts work together.


### Configurations for Fast or Slow are removed

You no longer configure individual distribution points to be fast or slow. Instead, each site system associated with a boundary group is treated the same. Because of this change, the **References** tab of the boundary group properties no longer supports the configuration of Fast or Slow.  


### New default boundary group at each site

Each primary site has a new default boundary group named **Default-Site-Boundary-Group&lt;sitecode>**. When a client isn't on a network location assigned to a boundary group, it uses the site systems associated with the default group from its assigned site. Plan to use this boundary group as a replacement to the concept of fallback content location.  	

#### **Allow fallback source locations for content** is removed
You no longer explicitly configure a distribution point to be used for fallback. The options to configure this setting are removed from the console.

Additionally, the result of setting **Allow clients to use a fallback source location for content** on a deployment type for applications has changed. This setting on a deployment type now enables a client to use the default site boundary group as a content source location.

#### Boundary groups relationships
You can link each boundary group to one or more additional boundary groups. These links form relationships that you configure on the new boundary group properties tab named **Relationships**:  

- Each boundary group that a client is directly associated with is called a **current** boundary group.  

- Any boundary group a client can use because of an association between that client's *current* boundary group and another group is called a **neighbor** boundary group.  

- On the **Relationships** tab, add boundary groups to use as a *neighbor* boundary group. Also configure a time in minutes for fallback. When a client fails to find content from a distribution point in the *current* group, this time is when the client begins to search content locations from *neighbor* boundary groups.  

    When you add or change a boundary group configuration, you can block fallback to that specific boundary group from the current group you're configuring.  

To use the new configuration, define explicit associations (links) from one boundary group to another. Configure all distribution points in that associated group with the same time in minutes. When a client fails to find a content source from its *current* boundary group, the time you configure determines when it begins to search for content sources from its neighbor boundary group.

In addition to boundary groups you explicitly configure, each boundary group has an implied link to the default site boundary group. This link becomes active after 120 minutes. Then the default site boundary group becomes a neighbor boundary group. This behavior allows the clients to use as content source locations the distribution points associated with that boundary group.

This behavior replaces what was previously referred to as fallback for content. Override this default behavior of 120 minutes by explicitly associating the default site boundary group to a *current* group. Set a specific time in minutes, or block fallback entirely to prevent its use.


### Clients try to get content from each distribution point for up to two minutes

When a client searches for a content source location, it tries to access each distribution point for two minutes before then trying another distribution point. This behavior is a change from previous versions where clients tried to connect to a distribution point for up to two hours.

- Clients randomly select the first distribution point from the pool of available servers in the client's *current* boundary group (or groups).  

- After two minutes, if the client hasn't found the content, it switches to a new distribution point and tries to get content from that server. This process repeats every two minutes until the client finds the content or reaches the last server in its pool.  

- If a client can't find a valid content source location from its *current* pool before it reaches the period for fallback to a *neighbor* boundary group, the client then adds the distribution points from that *neighbor* group to the end of its current list. It then searches the expanded group of source locations that includes the distribution points from both boundary groups.  

    > [!TIP]  
    > When you create an explicit link from the current boundary group to the default site boundary group, and define a fallback time that is less than the fallback time for a link to a neighbor boundary group, clients begin searching source locations from the default site boundary group before including the neighbor group.  

- When the client fails to get content from the last server in the pool, it begins the process again.  



## See also

- [Procedures for boundary groups](/sccm/core/servers/deploy/configure/boundary-group-procedures)  

- [About boundaries](/sccm/core/servers/deploy/configure/boundaries)  

- [Fundamental concepts for content management](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management)  
