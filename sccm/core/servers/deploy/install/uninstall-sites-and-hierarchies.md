---
title: "Uninstall sites"
description: "Use these details as a guide to uninstall a System Center Configuration Manager site."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d466edd2-97f0-44c1-a73e-d71abbdbf4a8
caps.latest.revision: 6
caps.handback.revision: 0
author: Brendunsms.author: brendunsmanager: angrobe

---
# Uninstall sites and hierarchies in System Center Configuration Manager*Applies to: System Center Configuration Manager (Current Branch)*
Use the following details as a guide if you need to uninstall a System Center Configuration Manager site.  

To decommission a hierarchy with multiple sites, the sequence of removal is important. Start by uninstalling the sites  at the bottom of the hierarchy and then move upward:  

1.  Remove secondary sites attached to primary sites.  
2.  Remove primary sites.
3.  After all primary sites are removed, you can uninstall the central administrations site.  


##  <a name="BKMK_RemoveSecondarysite"></a> Remove a secondary site from a hierarchy  
You cannot move a secondary site or reassign a secondary site to a new parent primary site. To be removed from a hierarchy, a secondary site must be deleted from its direct parent site. Use the Delete Secondary Site Wizard from the Configuration Manager console to remove a secondary site. When you remove a secondary site, you must choose whether to delete it or uninstall it:  

-   **Uninstall the secondary site**. Use this option to remove a functional secondary site that is accessible from the network. This option uninstalls Configuration Manager from the secondary site server, and then deletes all information about the site and its resources from the Configuration Manager site hierarchy. If Configuration Manager installed SQL Server Express as part of the secondary site installation, Configuration Manager will uninstall SQL Express when it uninstalls the secondary site. If SQL Server Express was installed before you installed the secondary site, Configuration Manager will not uninstall SQL Server Express.  

-   **Delete the secondary site**. Use this option if one of the following is true:  

    -   A secondary site failed to install  
    -   The secondary site continues to be displayed in the Configuration Manager console after you uninstall it

    This option deletes all information about the site and its resources from the Configuration Manager hierarchy, but leaves Configuration Manager installed on the secondary site server.  

    > [!NOTE]  
    >  You also can use the Hierarchy Maintenance Tool and the **/DELSITE** option to delete a secondary site. For more information, see [Hierarchy Maintenance Tool (Preinst.exe) for System Center Configuration Manager](../../../../core/servers/manage/hierarchy-maintenance-tool-preinst.exe.md).  

#### To uninstall or delete a secondary site  

1.  Verify that the administrative user that runs Setup has the following security rights:  

    -   Administrative rights on the secondary site computer  
    -   Local Administrator rights on the remote site database server for the primary site, if it is remote  
    -   Infrastructure Administrator or Full Administrator security role on the parent primary site  
    -   Sysadmin rights on the site database of the secondary site  

2.  In the Configuration Manager console, select **Administration**.  
3.  In the **Administration** workspace, expand **Site Configuration**, and then select **Sites**.  
4.  Select the secondary site server that you want to remove.  
5.  On the **Home** tab, in the **Site** group, select **Delete**.  
6.  On the **General** page, select whether to uninstall or delete the secondary site, and then click **Next**.  
7.  On the **Summary** page, verify the settings, and then select **Next**.  
8.  On the **Completion** page, select **Close** to exit the wizard.  

##  <a name="BKMK_UninstallPrimary"></a> Uninstall a primary site  
You can run Configuration Manager Setup to uninstall a primary site that does not have an associated secondary site. Before you uninstall a primary site, consider the following:  

-   When Configuration Manager clients are within the boundaries configured at the site, and the primary site is part of a Configuration Manager hierarchy, consider adding the boundaries to a different primary site in the hierarchy before you uninstall the primary site.  
-   When the primary site server is no longer available, you must use the Hierarchy Maintenance Tool at the central administration site to delete the primary site from the site database. For more information, see [Hierarchy Maintenance Tool (Preinst.exe) for System Center Configuration Manager](../../../../core/servers/manage/hierarchy-maintenance-tool-preinst.exe.md).  

Use the following procedure to uninstall a primary site.  

#### To uninstall a primary site  

1.  Verify that the administrative user that runs Setup has the following security rights:  

    -   Local Administrator rights on the central administration site server  
    -   Local Administrator rights on the remote site database server for the central administration site, if it is remote
    -   Sysadmin rights on the site database of the central administration site  
    -   Local Administrator rights on the primary site computer  
    -   Local Administrator rights on the remote site database server for the primary site, if it is remote  
    -   A user name associated with the Infrastructure Administrator or Full Administrator security role on the central administration site  

2.  Start Configuration Manager Setup on the primary site server by using one of the following methods:  

    -   On **Start**, select **Configuration Manager Setup**.  
    -   Open Setup.exe from &lt;*ConfigMgrInstallationMedia*>\SMSSETUP\BIN\X64.  
    -   Open Setup.exe from &lt;*ConfigMgrInstallationPath*>\BIN\X64.  

3.  On the **Before You Begin** page, select **Next**.  
4.  On the **Getting Started** page, select **Uninstall a Configuration Manager site**, and then select **Next**.  
5.  On the **Uninstall the Configuration Manager Site**, specify whether to remove the site database from the primary site server, and whether to remove the Configuration Manager console. By default, Setup removes both items.  

    > [!IMPORTANT]  
    >  When a secondary site is attached to the primary site, you must remove the secondary site before you can uninstall the primary site.  

6.  Select **Yes** to confirm the uninstallation of the Configuration Manager primary site.  

##  <a name="BKMK_UninstallPrimaryDistViews"></a> Uninstall a primary site that is configured with distributed views  
 Before you uninstall a child primary site that has distributed views turned on for its replication link to the central administration site, you must turn off distributed views in your hierarchy. Use the following information to turn off distributed views before you uninstall a primary site.  

#### To uninstall a primary site that is configured with distributed views  

1.  Before you uninstall any primary site, you must turn off distributed views on each link in the hierarchy between the central administration site and a primary site.  
2.  After you turn off distributed views on each link, confirm that the data from the primary site finishes reinitializing at the central administration site. To monitor the initialization of data, in the Configuration Manager console, in the **Monitoring** workspace, view the link on the **Database Replication** node.  
3.  After the data successfully reinitializes with the central administration site, you can uninstall the primary site. To uninstall a primary site, see [Uninstall a primary site](#BKMK_UninstallPrimary).  
4.  When the primary site is completely uninstalled, you can reconfigure distributed views on links to primary sites.  

    > [!IMPORTANT]  
    >  If you uninstall the primary site before you turn off distributed views at each site, or before the data from the primary site successfully reinitializes at the central administration site, replication of data between primary sites and the central administration site might fail. In this scenario, you must turn off distributed views for each link in your site hierarchy, and then, after the data successfully reinitializes with the central administration site, you can reconfigure distributed views.  

##  <a name="BKMK_UninstallCAS"></a> Uninstall the central administration site  
 You can run Configuration Manager Setup to uninstall a central administration site that does not have child primary sites. Use the following procedure to uninstall the central administration site.  

#### To uninstall a central administration site  

1.  Verify that the administrative user who runs Setup has the following security rights:  

    -   Local Administrator rights on the central administration site server  
    -   Local Administrator rights on the site database server for the central administration site, if the site database server is not installed on the site server 

2.  Start Configuration Manager Setup on the central administration site server by using one of the following methods:  

    -   On **Start**, click **Configuration Manager Setup**.  
    -   Open Setup.exe from &lt;*ConfigMgrInstallationMedia*>\SMSSETUP\BIN\X64.  
    -   Open Setup.exe from &lt;*ConfigMgrInstallationPath*>\BIN\X64.  

3.  On the **Before You Begin** page, select **Next**.  
4.  On the **Getting Started** page, select **Uninstall a Configuration Manager site**, and then select **Next**.  
5.  On the **Uninstall the Configuration Manager Site**, specify whether to remove the site database from the central administration site server, and whether to remove the Configuration Manager console. By default, Setup removes both items.  

    > [!IMPORTANT]  
    >  When there is a primary site attached to the central administration site, you must uninstall the primary site before you can uninstall the central administration site.  

6.  Select **Yes** to confirm the uninstallation of the Configuration Manager central administration site.  
