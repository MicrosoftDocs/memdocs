---
title: About boundary groups
titleSuffix: Configuration Manager
description: Help clients find site systems by using boundary groups to logically organize related network locations.
ms.date: 08/02/2021
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
author: sheetg09
ms.author: sheetg
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# About boundary groups in Configuration Manager

*Applies to: Configuration Manager (current branch)*

Use boundary groups in Configuration Manager to logically organize related network locations called [boundaries](boundaries.md). Use boundaries and boundary groups to make it easier to manage your infrastructure. Assign boundaries to boundary groups before using the boundary group.

By default, Configuration Manager creates a default site boundary group at each site.

To configure boundary groups, associate boundaries and site system roles to the boundary group. This configuration helps associate clients to site system servers that are located near the clients on the network.

To increase the availability of servers to a wider range of network locations, assign the same boundary and the same server to more than one boundary group.

Clients use a boundary group for:

- Automatic site assignment

- To find a site system server that can provide a service, including:

  - [Distribution points](boundary-groups-distribution-points.md) for content location.

  - [Software update points](boundary-groups-software-update-points.md)

  - State migration points

    > [!NOTE]
    > The state migration point doesn't use fallback relationships. For more information, see [Fallback](#fallback).

  - [Management points](boundary-groups-management-points.md)

  - [Preferred management points](boundary-groups-management-points.md#preferred-management-points)

    > [!NOTE]
    > If you use preferred management points, enable this option for the hierarchy, not from within the boundary group configuration. For more information, see [Enable use of preferred management points](boundary-group-procedures.md#enable-use-of-preferred-management-points).

  - Cloud management gateway (CMG) for policy and content

## Boundary groups and relationships

For each boundary group in your hierarchy, you can assign:

- One or more boundaries. A client's _current_ boundary group is a network location that's defined as a boundary assigned to a specific boundary group. A client can have more than one current boundary group.

- One or more site system roles. Clients can always use roles associated with their current boundary group. Depending on other configurations, they can use roles in other boundary groups.

For each boundary group you create, you can configure a one-way link to another boundary group. The link is called a _relationship_. The boundary groups you link to are called _neighbor_ boundary groups. A boundary group can have more than one relationship, each with a specific neighbor boundary group.

When a client fails to find an available site system in its current boundary group, the configuration of each relationship determines when it begins to search a neighbor boundary group. This search of other groups is called _fallback_.

For more information, see the following articles:

- [Example of using boundary groups](boundary-groups-example.md)
- [Create a boundary group](boundary-group-procedures.md#create-a-boundary-group)
- [Configure a boundary group](boundary-group-procedures.md#configure-a-boundary-group)
- [Show boundary groups for devices](boundary-group-procedures.md#show-boundary-groups-for-devices)

## Fallback

To prevent problems when clients can't find an available site system in their current boundary group, define the relationship between boundary groups for fallback behavior. Fallback lets a client expand its search to other boundary groups to find an available site system.

Relationships are configured on a boundary group properties **Relationships** tab. When you configure a relationship, you define a link to a neighbor boundary group. For each type of supported site system role, configure independent settings for fallback to the neighbor boundary group. For more information, see [Configure fallback behavior](boundary-group-procedures.md#configure-fallback-behavior).

For example, when you configure a relationship to a specific boundary group, set fallback for distribution points to occur after 20 minutes. The default is 120 minutes For a more detailed example, see [Example of using boundary groups](boundary-groups-example.md).

If a client fails to find an available site system role in its current boundary group, the client uses the fallback time in minutes. This fallback time determines when the client begins to search for an available site system associated with the neighbor boundary group.

When a client can't find an available site system, it begins to search locations from neighbor boundary groups. This behavior increases the pool of available site systems. The configuration of boundary groups and their relationships defines the client's use of this pool of available site systems.

- A boundary group can have more than one relationship. With this configuration, you can configure fallback for each type of site system to different neighbors to occur after different periods of time.

- Clients only fall back to a boundary group that's a direct neighbor of their current boundary group.

- When a client is a member of more than one boundary group, it defines its current boundary group as a union of all its boundary groups. The client falls back to neighbors of any of those original boundary groups.

> [!NOTE]
> The state migration point role doesn't use fallback relationships. If you add both the state migration point and distribution point roles to the same site system server, don't configure fallback on its boundary group. If you need to use boundary group fallback for the distribution point, add the state migration point role on a different site system server.<!-- 2838807 -->

## The default site boundary group

You can create your own boundary groups, and each site has a default site boundary group that Configuration Manager creates. This group is named **Default-Site-Boundary-Group&lt;sitecode>**. For example, the group for site ABC would be named **Default-Site-Boundary-Group&lt;ABC>**.

For each boundary group you create, Configuration Manager automatically creates an implied link to each default site boundary group in the hierarchy.

- The implied link is a default fallback option from a current boundary group to the site's default boundary group. The default fallback time is 120 minutes.

- For clients not in a boundary associated with any boundary group: to identify valid site system roles, use the default site boundary group from their assigned site.

To manage fallback to the default site boundary group:

- Open the properties of the site default boundary group, and change the values on the **Default Behavior** tab. Changes you make here apply to *all* implied links to this boundary group. When you configure an explicit link to this default site boundary group from another boundary group, you override these default settings.

- Open the properties of a custom boundary group. Change the values for the explicit link to a default site boundary group. When you set a new time in minutes for fallback or block fallback, that change affects only the link you're configuring. Configuration of the explicit link overrides the settings on the **Default Behavior** tab of a default site boundary group.



## Site assignment

You can configure each boundary group with an assigned site for clients.

- A newly installed client that uses automatic site assignment joins the assigned site of a boundary group that contains the client's current network location.

- After assigning to a site, a client doesn't change its site assignment when it changes its network location. For example, a client roams to a new network location. This location is a boundary in a boundary group with a different site assignment. The client's assigned site doesn't change.

- When Active Directory System Discovery discovers a new resource, the site evaluates network information for the resource against the boundaries in boundary groups. This process associates the new resource with an assigned site for use by the client push installation method.

- When a boundary is a member of more than one boundary groups that have different assigned sites, clients randomly select one of the sites.

- Changes to a boundary groups assigned site only apply to new site assignment actions. Clients that previously assigned to a site don't reevaluate their site assignment based on changes to the configuration of a boundary group (or to their own network location).

For more information about client site assignment, see [Using automatic site assignment for computers](../../../clients/deploy/assign-clients-to-a-site.md#automatic-site-assignment).

For more information on how to configure site assignment, see the following procedures:

- [Configure site assignment and select site system servers](boundary-group-procedures.md#configure-site-assignment-and-select-site-system-servers)
- [Configure a fallback site for automatic site assignment](boundary-group-procedures.md#configure-a-fallback-site-for-automatic-site-assignment)


## Default site boundary group behavior supports cloud source selection
<!--10674394-->

*(Added in version 2207)*

You can add options via PowerShell to include and prefer cloud management gateway (CMG) management points for the default site boundary group. When a site is set up, there's a default site boundary group created for each site and all the clients are by default mapped to it until they're assigned to some custom boundary group. 

Currently on the admin console, you can add references to default site boundary group, but the added references don't have any effect when the client requests for management point list. Starting with technical preview version 2206, you can use PowerShell cmdlets to include and prefer cloud-based sources for clients in the default site boundary group. This action is currently only for the management point role.  

> [!NOTE]
> You can't currently configure this behavior from the Configuration Manager console. For more information on configuring this behavior with PowerShell, see the cmdlet details in the following section. 

### Set-CMDefaultBoundaryGroup 

Use this cmdlet to modify the properties of a default site boundary group. You can set the options to include and prefer the cloud-based sources for the clients in default site boundary group. 

#### Syntax

```powershell
Set-CMDefaultBoundaryGroup [-IncludeCloudBasedSources <Boolean>] [-PreferCloudBasedSources <Boolean>] 
```

#### Examples

```powershell
Set-CMDefaultBoundaryGroup -IncludeCloudBasedSources $true -PreferCloudBasedSources $true 

Set-CMDefaultBoundaryGroup -IncludeCloudBasedSources $true 

Set-CMDefaultBoundaryGroup -IncludeCloudBasedSources $true -PreferCloudBasedSources $false 
```

#### Parameters

- **IncludeCloudBasedSources**: Used to specify whether admin wants to include the cloud-based sources in the management point list for the clients in default site boundary group. 

- **PreferCloudBasedSources**: Used to specify whether admin wants to prefer the cloud-based sources in the management point list for the clients in default site boundary group. On selecting this option, cloud-based servers will be given preference by the clients. 

> [!NOTE]
> You can only set this option to true if the parameter IncludeCloudBasedSources is set to true or was already set to true by admin. 

## Next steps

- [Boundary group options](boundary-group-options.md)

- [Procedures for boundary groups](boundary-group-procedures.md)

<!-- catch-all for previous anchors -->
<a name="overlapping-boundaries"></a>
<a name="bkmk_show-boundary"></a>
<a name="distribution-points"></a>
<a name="bkmk_bgoptions"></a>
<a name="bkmk_preferred"></a>
<a name="bkmk_sup"></a>

> [!NOTE]
> Some sections that were previously in this article have moved:
>
> - [Show boundary groups for devices](boundary-group-procedures.md#show-boundary-groups-for-devices)
> - [Distribution points](boundary-groups-distribution-points.md)
> - [Boundary group options](boundary-group-options.md)
> - [Software update points](boundary-groups-software-update-points.md)
> - [Management points](boundary-groups-management-points.md)
> - [Preferred management points](boundary-groups-management-points.md#preferred-management-points)
> - [Overlapping boundaries](define-site-boundaries-and-boundary-groups.md#overlapping-boundaries)
> - [Example of using boundary groups](boundary-groups-example.md)
