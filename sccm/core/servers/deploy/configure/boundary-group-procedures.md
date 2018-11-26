---
title: Procedures for boundary groups
titleSuffix: Configuration Manager
description: Configure boundary groups to logically organize related network locations called boundaries.
ms.date: 11/26/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: a1fe22d0-4695-4de0-8bf0-e3475b03cf0e
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# How to configure boundary groups for Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

This article includes procedures on how to configure boundary groups. Before you begin, make sure you understand boundary group concepts. For more information, see [Boundary groups](/sccm/core/servers/deploy/configure/boundary-groups).



## <a name="bkmk_create"></a> Create a boundary group  

1.  In the Configuration Manager console, go to the **Administration** workspace, expand **Hierarchy Configuration**, and select the **Boundary Groups** node.  

2.  On the **Home** tab, in the **Create** group, select **Create Boundary Group**.  

3.  In the **Create Boundary Group** dialog box, on the **General** tab, specify a **Name** for this boundary group. Optionally include a **Description**.  

4.  Select **OK** to save the new boundary group, or continue to the next section to configure the boundary group.  


## <a name="bkmk_config"></a> Configure a boundary group  

1.  In the Configuration Manager console, go to the **Administration** workspace, expand **Hierarchy Configuration**, and select the **Boundary Groups** node.  

2.  Select the boundary group you want to modify, and select **Properties** in the ribbon. This action opens the boundary group Properties window.  

Configure the following settings:  
- [Add or remove boundaries](#bkmk_add)  
- [Configure site assignment and select site system servers](#bkmk_references)  
- [Configure fallback behavior](#bkmk_bg-fallback)  
- [Configure boundary group options](#bkmk_options)  


### <a name="bkmk_add"></a> Add or remove boundaries

In the boundary group Properties window, use the **General** tab to modify the boundaries that are members of this boundary group:  

- To add boundaries, select **Add**. In the Add Boundaries window, select the check box for one or more boundaries, and select **OK**.  

- To remove boundaries, select the boundary in the list, and select **Remove**.  


### <a name="bkmk_references"></a> Configure site assignment and select site system servers

To modify the site assignment and associated site system server configuration, switch to the **References** tab in the boundary group Properties window.  

- To enable this boundary group for use by clients for site assignment, select **Use this boundary group for site assignment**. Then select a site from the **Assigned site** dropdown list. For more information, see [Site assignment](/sccm/core/servers/deploy/configure/boundary-groups#site-assignment).  

- To associate available site system servers with this boundary group, select **Add**. The Add Site Systems window only lists servers that have supported site system roles. Select the check box for one or more servers, and select **OK**. It adds them as associated site system servers for this boundary group.  

    > [!NOTE]  
    >  You can select any combination of available site systems from any site in the hierarchy. Selected site systems are listed on the **Site Systems** tab in the properties of each boundary that's a member of this boundary group.  

- To remove a server from this boundary group, select the server and then select **Remove**.  

    > [!NOTE]  
    >  To stop use of this boundary group for associating site systems, remove all servers listed as associated site system servers.  


### <a name="bkmk_bg-fallback"></a> Configure fallback behavior

To configure fallback behavior, switch to the **Relationships** tab in the boundary group Properties window.  

- To create a relationship with another boundary group:  

    - Select **Add**. In the Fallback Boundary Groups window, select the boundary group to configure.  

    - Set a fallback time for the following site system roles:  
        - Distribution point  
        - Software update point  
        - Management point  

        > [!Note]  
        > For example, you open the Properties window for the Branch Office boundary group. In the Fallback Boundary Groups window, you select the Main Office boundary group. You set the distribution point fallback time to `20`. When you save this configuration, clients in the Branch Office boundary group will start searching for content from the distribution points in the Main Office boundary group after 20 minutes.  

    - To prevent fallback to a specific boundary group, select the boundary group, and then select **Never fallback** for the type of site system role. This action can include the *default site boundary group*.  

- To modify the configuration of an existing relationship, select the boundary group in the list, and select **Change**. This action opens the Fallback Boundary Groups window for just this boundary group.  
 
- To remove a relationship, select the boundary group in the list, and select **Remove**.  

For more information, see [Fallback](/sccm/core/servers/deploy/configure/boundary-groups#fallback). 


### <a name="bkmk_options"></a> Configure boundary group options
<!--1356193-->
Starting in version 1806, to configure additional options for clients in this boundary group, switch to the **Options** tab. For more information, see [Boundary group options for peer downloads](/sccm/core/servers/deploy/configure/boundary-groups#bkmk_bgoptions).

- **Allow peer downloads in this boundary group**: This option is enabled by default. The management point provides clients a list of content locations that includes peer sources.  

    - **During peer downloads, only use peers within the same subnet**: This setting is dependent upon the one above. If you enable this option, the management point only includes in the content location list peer sources that are in the same subnet as the client.  


## <a name="bkmk_site-fallback"></a> Configure a fallback site for automatic site assignment  

If clients aren't in a boundary group with an assigned site, assign them to this site when they're installed.

1.  In the Configuration Manager console, go to the **Administration** workspace, expand **Site Configuration**, and select the **Sites** node.  

2.  On the **Home** tab of the ribbon, in the **Sites** group, select **Hierarchy Settings**.  

3.  On the **General** tab, select the checkbox to **Use a fallback site**. Then select a site from the **Fallback site** drop-down list.  

4.  Select **OK** to save the configuration.  

For more information, see [Site assignment](/sccm/core/servers/deploy/configure/boundary-groups#site-assignment).


## <a name="bkmk_proc-prefer"></a> Enable use of preferred management points  

For more information, see [Preferred management points](/sccm/core/servers/deploy/configure/boundary-groups#bkmk_preferred).

1.  In the Configuration Manager console, go to the **Administration** workspace, expand **Site Configuration**, and select the **Sites** node.  

2. On the **Home** tab of the ribbon, in the **Sites** group, select **Hierarchy Settings**.  

3. On the **General** tab, select **Clients prefer to use management points specified in boundary groups**.  

4. Select **OK** to save the configuration.  

