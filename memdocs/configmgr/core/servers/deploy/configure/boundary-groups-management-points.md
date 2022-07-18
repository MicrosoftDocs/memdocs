---
title: Boundary groups and management points
titleSuffix: Configuration Manager
description: Understand how clients and management points behave with boundary groups.
ms.date: 02/16/2022
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
author: mestew
ms.author: mstewart
manager: dougeby
ms.localizationpriority: medium
---

# Boundary groups and management points

*Applies to: Configuration Manager (current branch)*

<!-- 1324594 -->
Configure fallback relationships for management points between boundary groups. This behavior provides greater control for the management points that clients use. On the **Relationships** tab of the boundary group properties, there's a column for management point. When you add a new fallback boundary group, the fallback time for the management point is currently always zero (0). This behavior is the same for the **Default Behavior** on the site default boundary group.

Previously, a common problem occurred when you had a protected management point in a secure network. Clients on the main network received policy that included this protected management point, even though they couldn't communicate with it across a firewall. To address this problem now, use the **Never fallback** option to make sure that clients only fall back to management points with which they can communicate.

> [!NOTE]
> If you enable distribution points in the site default boundary group to fallback, and a management point is collocated on a distribution point, the site also adds that management point to the site default boundary group.<!--VSO 2841292-->

If a client is in a boundary group with no assigned management point, the site gives the client the entire list of management points. This behavior makes sure that a client always receives a list of management points.

> [!TIP]
> If you enable the option to **Prefer cloud-based sources over on-premises sources** then clients will prefer a cloud management gateway (CMG) for both policy and content.

Management point boundary group fallback doesn't change the behavior during client installation (ccmsetup.exe). If the command line doesn't specify the initial management point using the `/MP` parameter, the new client receives the full list of available management points. For its initial bootstrap process, the client uses the first management point it can access. Once the client registers with the site, it receives the management point list properly sorted with this new behavior.

For more information on the client's behavior to acquire content during installation, see [Client installation](boundary-groups-distribution-points.md#client-installation).

During client upgrade, if you don't specify the `/MP` command-line parameter, the client queries sources such as Active Directory and WMI for any available management point. Client upgrade doesn't honor the boundary group configuration. <!--VSO 2841292-->

For clients to use this capability, enable the following setting: **Clients prefer to use management points specified in boundary groups** in **Hierarchy Settings**.

> [!NOTE]
> OS deployment processes aren't aware of boundary groups for management points.

## Troubleshoot

New entries appear in the **LocationServices.log**. The **Locality** attribute identifies one of the following states:

- **0**: Unknown

- **1**: The specified management point is only in the site default boundary group for fallback.

- **2**: The specified management point is in a remote or neighbor boundary group. When the management point is in both a neighbor and the site default boundary groups, the locality is 2.

- **3**: The specified management point is in the local or current boundary group. When the management point is in the current boundary group and either a neighbor or the site default boundary group, the locality is 3. If you don't enable the preferred management points setting in Hierarchy Settings, the locality is always 3 no matter which boundary group the management point is in.

Clients use local management points first (locality 3), remote second (locality 2), then fallback (locality 1).

When a client receives five errors in 10 minutes and fails to communicate with a management point in its current boundary group, it tries to contact a management point in a neighbor or the site default boundary group. If the management point in the current boundary group later comes back online, the client returns to the local management point on the next refresh cycle. The refresh cycle is 24 hours, or when the Configuration Manager agent service restarts.

## Preferred management points

> [!NOTE]
> When you enable **Clients prefer to use management points specified in boundary groups**, Configuration Manager uses the boundary group functionality for the assigned management point.

Preferred management points enable a client to identify a management point that's associated with its current network location (boundary).

- A client tries to use a preferred management point from its assigned site before using one not configured as preferred from its assigned site.

- To use this option, enable **Clients prefer to use management points specified in boundary groups** in **Hierarchy Settings**. Then configure boundary groups at individual primary sites. Include the management points that should be associated with that boundary group's associated boundaries. For more information, see [Enable use of preferred management points](boundary-group-procedures.md#enable-use-of-preferred-management-points).

- When you configure preferred management points, and a client organizes its list of management points, the client places the preferred management points at the top of its list. This list includes all management points from the client's assigned site.

> [!NOTE]
> Client roaming means it changes its network locations. For example, when a laptop travels to a remote office location. When a client roams, it might use a management point from the local site before attempting to use a server from its assigned site. This list of servers from its assigned site includes the preferred management points. For more information, see [Understand how clients find site resources and services](../../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).

## Next steps

- [Example of using boundary groups](boundary-groups-example.md)

- [Procedures for boundary groups](boundary-group-procedures.md)
