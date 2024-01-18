---
title: Uninstall sites
titleSuffix: Configuration Manager
description: A guide for removing roles, and uninstalling sites and hierarchies
ms.date: 02/16/2022
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: conceptual
author: sheetg09
ms.author: sheetg
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Uninstall roles, sites, and hierarchies in Configuration Manager

*Applies to: Configuration Manager (current branch)*

Use this article as a guide to uninstall a Configuration Manager site system role, site, or hierarchy. You can also remove the central administration site (CAS) from a hierarchy, but keep the primary site.

## <a name="bkmk_role"></a> Site system role

You might want to remove a role from a site system server for the following reasons:

- Broader infrastructure change, such as network or physical locations
- Decommission the underlying server
- Consolidate roles to reduce costs and complexity
- Reconfigure or redesigning the site roles
- Discontinue use of the feature that role supports

When you decide you need to remove a role, first consider your answers to the following questions:

- Do you still need the role in the site? If so, does another site system already have the role?

- Are other site systems with this role properly sized to support your business requirements for performance and availability?

- Are all clients already reconfigured to use another role? Will you rely upon default client behaviors to fall back or discover another server?

### Procedure to remove a site system role

Use the following procedure to remove a role:

1. In the **Configuration Manager** console, go to the **Administration** workspace. Expand **Site Configuration**, and then select the **Servers and Site System Roles** node.

1. Select the site system server with the role to remove. In the **Site System Roles** details pane, select the target role.

1. In the ribbon, on the **Site Role** tab, in the **Site Role** group, select **Remove Role**. Confirm that you want to remove the role.

### Additional information for specific roles

Some roles may have additional steps and considerations.

#### Software update point

After you remove the software update point, Configuration Manager updates the client policy to remove the software update point from the list. When you remove the last software update point at the site, the software update point list contains no software update points. With no roles available, software updates management is essentially disabled at the site.

When you have more than one software update point at a primary site, and you remove the software update point that's the synchronization source, choose another software update point at the site to be the new synchronization source.

## <a name="bkmk_secondary"></a> Secondary site  

Other than when you're [decommissioning a hierarchy](#bkmk_hierarchy), the main reason to remove a secondary site is because of a broader infrastructure change, such as network or physical locations. Also review the reasons to [choose a secondary site](../../../plan-design/hierarchy/design-a-hierarchy-of-sites.md#BKMK_ChooseSecondary).

When you decide you need to remove a secondary site, first consider your answers to the following questions:

- Did you remove all site system roles from the site server?

- Are any boundaries or boundary groups associated with the secondary site? Reconfigure boundaries before removing the site.

- Are any clients still at the location?

- Have you configured other content management options like [peer caching](../../../plan-design/hierarchy/fundamental-concepts-for-content-management.md#peer-caching-technologies)?

### Options to delete secondary sites

You can't move or reassign a secondary site to another primary site. When you remove a secondary site from its direct parent site, choose whether to uninstall or delete it.

#### Uninstall the secondary site

Use this option to remove a functional secondary site that's accessible from the network. This option uninstalls Configuration Manager from the secondary site server. It then deletes all information about the site and its resources from the Configuration Manager site.

If Configuration Manager installed SQL Server Express for the secondary site, Configuration Manager uninstalls SQL Server Express as well. If you installed SQL Server Express before you installed the secondary site, Configuration Manager doesn't uninstall SQL Server Express.

#### Delete the secondary site

Use this option in the following situations:

- It failed to install

- After you uninstall it, the Configuration Manager console still shows the secondary site

    This option deletes all information about the site and its resources from the Configuration Manager hierarchy, but doesn't make any changes on the site server.

    > [!TIP]
    >  You also can use the Hierarchy Maintenance Tool with the `/DELSITE` option to delete a secondary site. For more information, see [Hierarchy Maintenance Tool (Preinst.exe)](../../manage/hierarchy-maintenance-tool-preinst.exe.md).

### Prerequisites to delete a secondary site

The administrative user that runs Configuration Manager setup needs the following security rights:

- Local **Administrator** rights on the secondary site server

- If the primary site database server is remote from the primary site server, local **Administrator** rights on the remote site database server for the primary site.

- **Infrastructure Administrator** or **Full Administrator** security role on the parent primary site

- **Sysadmin** rights on the secondary site database

### Procedure to delete a secondary site

Use the following procedure to uninstall or delete a secondary site:

1. In the Configuration Manager console, go to the **Administration** workspace, expand **Site Configuration**, and then select the **Sites** node.

1. Select the secondary site server that you want to remove. In the ribbon, on the **Home** tab, in the **Site** group, select **Delete**.

1. On the **General** page, select whether to uninstall or delete the secondary site.

1.  Complete the wizard.

## <a name="bkmk_primary"></a> Primary site  

You might want to uninstall a primary site from your hierarchy for the following reasons:

- Consolidate sites to reduce costs and complexity
- Reconfigure or redesign the sites of the hierarchy

Before you uninstall a child primary site that uses [distributed views](../../../plan-design/hierarchy/database-replication.md#distributed-views) for its replication link to the CAS, first turn off distributed views in your hierarchy. For more information, see [Uninstall a primary site that is configured with distributed views](#bkmk_distviews).

### <a name="bkmk_pri-plan"></a> Plan to uninstall a primary site

Before you uninstall a primary site, review the following tasks:

- Review boundaries, boundary groups, and fallback relationships. If you assign clients to a new site, but don't change the boundaries, they may be considered roaming. For more information, see [Define site boundaries and boundary groups](../configure/define-site-boundaries-and-boundary-groups.md).

- Make sure all active clients are reassigned to another primary site in the hierarchy. Otherwise clients will be unmanaged after you uninstall the site. For more information, see [How to assign clients to a site](../../../clients/deploy/assign-clients-to-a-site.md).

  - Review the list of site roles to make sure the new site provides the same level of service.

  - Make sure that you've properly sized the other site systems with this role in the other site. They will need to support your business requirements for performance and availability with the additional clients.

  - If this site has lots of clients, reassign them in stages. Monitor database replication as clients refresh full inventory and other site-specific data. If you manage software updates, clients will assign to a new software update point. This behavior causes a full scan for update compliance.

  - Client reassignment may impact reports and queries that rely on inventory data, and state-based compliance. Consider temporarily adjusting any client cycles during the transition.

  - Review all client assignment methods to make sure that none refers to this primary site.

- Check if any actively used objects in the hierarchy have static references to the site code. For example, collection queries, task sequences, or administrative scripts.

- If the hierarchy uses a [fallback site](../configure/boundary-group-procedures.md#configure-a-fallback-site-for-automatic-site-assignment) for automatic site assignment, make sure it doesn't reference this primary site.

- Reconfigure any [client installation methods](../../../clients/deploy/plan/client-installation-methods.md) that may reference a static site code.

- If this primary site has any site-specific cloud-attached services, make sure to remove them. If you still need the cloud resources, move them to another primary site in the hierarchy. Remove them from the primary site that you're going to uninstall, and add them to another primary site.

- If this primary site has any [discovery methods](../configure/run-discovery.md) for the hierarchy, move them to another site.

- Retire any site-based [OS deployment media](../../../../osd/deploy-use/create-task-sequence-media.md).

- Uninstall all site system roles from the site and the site server. For more information, see [Uninstall site system roles](#bkmk_role). While this preparation step isn't required, it helps identify any additional dependencies before uninstalling the site.

- Uninstall any secondary sites under this primary site. For more information, see the [Secondary site](#bkmk_secondary) section.

### <a name="bkmk_pri-prereq"></a> Prerequisites to uninstall a primary site

The administrative user that runs Configuration Manager setup needs the following security rights:

- Local **Administrator** rights on the CAS server

- If the CAS database server is remote from the site server, local **Administrator** rights on the remote site database server for the CAS.

- **Sysadmin** rights on the CAS site database

- Local **Administrator** rights on the primary site server

- If the primary site database server is remote from the primary site server, local **Administrator** rights on the remote site database server for the primary site.

- **Infrastructure Administrator** or **Full Administrator** security role on the CAS

### <a name="bkmk_pri-process"></a> Procedure to uninstall a primary site

You run Configuration Manager setup to uninstall a primary site that doesn't have an associated secondary site. Use the following procedure to uninstall a primary site:

> [!TIP]
> If the primary site server is no longer available, use the Hierarchy Maintenance Tool at the CAS to delete the primary site from the site database. For more information, see [Hierarchy Maintenance Tool (Preinst.exe)](../../manage/hierarchy-maintenance-tool-preinst.exe.md).

1. Start Configuration Manager setup on the primary site server by using one of the following methods:

    - On the **Start** menu, select **Configuration Manager Setup**.

    - In the directory for the Configuration Manager *installation media*, open `\SMSSETUP\BIN\X64\setup.exe`. Make sure this version is the same as the site version.

    - In the directory where Configuration Manager is *installed*, open `\BIN\X64\setup.exe`.

1. Review the information on the **Before You Begin** page.

1. On the **Getting Started** page, select **Uninstall a Configuration Manager site**.

    > [!IMPORTANT]  
    >  When a secondary site is attached to the primary site, you must remove the secondary site before you can uninstall the primary site.  

1. On the **Uninstall the Configuration Manager Site** page, both of the following options are enabled by default:

    - Remove the site database from the primary site server
    - Remove the Configuration Manager console

1. Select **Yes** to confirm the uninstallation of the Configuration Manager primary site.

### <a name="bkmk_distviews"></a> Uninstall a primary site that uses distributed views

1. Before you uninstall a child primary site, turn off distributed views on each link in the hierarchy between the CAS and a primary site.

1. After you turn off distributed views on each link, confirm that the data from the primary site finishes reinitializing at the CAS. To monitor the initialization of data, see [Monitor replication](../../manage/monitor-replication.md).

1. After the data successfully reinitializes with the CAS, you can [uninstall the primary site](#bkmk_pri-process).

1. When the primary site is uninstalled, you can reconfigure distributed views on links from the CAS to other primary sites.

    > [!IMPORTANT]
    > If you uninstall the primary site before you turn off distributed views at each site, or before the data from the primary site successfully reinitializes at the CAS, data replication might fail.

## <a name="bkmk_hierarchy"></a> Decommission a hierarchy

Some organizations have multiple hierarchies because of mergers, acquisitions, test environments, or other business requirements. If you consolidate management to a single hierarchy, this action can help reduce costs and complexity. Another reason to decommission the hierarchy is that you're migrating to a cloud-only management service such as Microsoft Intune, and are ready to remove your on-premises infrastructure.

To decommission a hierarchy with multiple sites, the sequence of removal is important. Start by uninstalling the sites at the bottom of the hierarchy and then move upward:

1. Remove secondary sites attached to primary sites.
2. Uninstall primary sites.
3. After you uninstall all primary sites, you can uninstall the CAS.

For more information, see the following sections:

- [Remove a secondary site](#bkmk_secondary)
- [Uninstall a primary site](#bkmk_primary)
- [Uninstall the CAS](#bkmk_uninstall-cas)

### <a name="bkmk_uninstall-cas"></a> Uninstall the CAS

The final step to decommission a hierarchy is to uninstall the CAS. Run Configuration Manager setup to uninstall the CAS that doesn't have child primary sites.

#### Prerequisites to uninstall the CAS

The administrative user who runs Configuration Manager setup needs the following security rights:

- Local **Administrator** rights on the CAS server

- If the CAS database server is remote from the site server, local **Administrator** rights on the remote site database server for the CAS.

#### Procedure to uninstall the CAS

1. Start Configuration Manager setup on the CAS server by using one of the following methods:

    - On the **Start** menu, select **Configuration Manager Setup**.

    - In the directory for the Configuration Manager *installation media*, open `\SMSSETUP\BIN\X64\setup.exe`. Make sure this version is the same as the site version.

    - In the directory where Configuration Manager is *installed*, open `\BIN\X64\setup.exe`.

1. Review the information on the **Before You Begin** page.

1. On the **Getting Started** page, select **Uninstall a Configuration Manager site**.

    > [!IMPORTANT]  
    >  Remove all child primary sites before you can uninstall the CAS.  

1. On the **Uninstall the Configuration Manager Site** page, both of the following options are enabled by default:

    - Remove the site database from the CAS server
    - Remove the Configuration Manager console

1. Select **Yes** to confirm the uninstallation of the Configuration Manager central administration site (CAS).

## <a name="bkmk_remove-cas"></a> Remove the CAS

<!-- 3607277 -->

If the hierarchy consists of the CAS and a single child primary site, you can remove the CAS. This action simplifies your Configuration Manager infrastructure to a single, standalone primary site. It removes the complexities of site-to-site replication, and focuses your management tasks to the single site.

For more information, see [Remove the CAS](remove-central-administration-site.md).
