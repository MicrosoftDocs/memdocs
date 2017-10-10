---
title: "Migration Source hierarchies"
description: "Configure a source hierarchy and source sites so you can migrate data to your System Center Configuration Manager environment."
ms.custom: na
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ccce7cb5-e18f-4337-8adf-2018edca3c00
caps.latest.revision: 5
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe

---
# Configure source hierarchies and source sites for migration to System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

To enable migration of data to your System Center Configuration Manager environment, you must configure a supported Configuration Manager source hierarchy and one or more source sites in that hierarchy that contain data that you want to migrate.  

> [!NOTE]  
>  Operations for migration are run at the top-level site in the destination hierarchy. If you configure migration when you use a Configuration Manager console that is connected to a primary child site, you must allow time for the configuration to replicate to the central administration site, start, and then replicate status back to the primary site to which you are connected.  

 Use the information and procedures in the following sections to specify the source hierarchy and add additional source sites. After you finish these procedures, you can create migration jobs and start to migrate data from the source hierarchy to the destination hierarchy.  

-   [Specify a source hierarchy for migration](#BKBM_ConfigSrcHierarchy)  

-   [Identify additional source sites of the source hierarchy](#BKBM_ConfigSrcSites)  

##  <a name="BKBM_ConfigSrcHierarchy"></a> Specify a source hierarchy for migration  
 To migrate data to your destination hierarchy, you must specify a supported source hierarchy that has the data that you want to migrate. By default, the top-level site of that hierarchy becomes a source site of the source hierarchy. If you migrate from a Configuration Manager 2007 hierarchy, you can then set up additional source sites for migration after data is gathered from the initial source site. If you migrate from a System Center 2012 Configuration Manager or System Center Configuration Manager hierarchy, you do not have to set up additional source sites to migrate data from the source hierarchy. This is because these versions of Configuration Manager use a shared database that is available at the top-level site of the source hierarchy. The shared database has all the information that you can migrate.  

 Use the following procedures to specify a source hierarchy for migration and to identify additional source sites in a Configuration Manager 2007 hierarchy.  

 Run this procedure with a Configuration Manager console that is connected to the destination hierarchy:  

### To configure a source hierarchy   

1.  In the Configuration Manager console, click **Administration**.  

2.  In the **Administration** workspace, expand **Migration**, and then click **Source Hierarchy**.  

3.  On the **Home** tab, in the **Migration** group, click **Specify Source Hierarchy**.  

4.  In the **Specify Source Hierarchy** dialog box, for **Source Hierarchy**, select **New source hierarchy**.  

5.  For **Top-level Configuration Manager site server**, enter the name or IP address of the top-level site of a supported source hierarchy.  

6.  Specify source site access accounts that have the following permissions:  

    -   Source Site Account: **Read** permission to the SMS Provider for the specified top-level site in the source hierarchy. Distribution point sharing and upgrades require **Modify** and **Delete** permissions to the site in the source hierarchy.

    -   Source Site Database Account: **Read** and **Execute** permission to the SQL Server database for the specified top-level site in the source hierarchy.  

     If you specify the use of the computer account, Configuration Manager uses the computer account of the top-level site of the destination hierarchy. For this option, ensure that this account is a member of the security group **Distributed COM Users** in the domain where the top-level site of the source hierarchy resides.  

7.  To share distribution points between the source and destination hierarchies, select the **Enable distribution point sharing for the source site server** check box. If you do not enable distribution point sharing at this time, you can do so by editing the credentials of the source site after data gathering has finished.  

8.  Click **OK** to save the configuration. This opens the **Data Gathering Status** dialog box, and data gathering starts automatically.  

9. When data gathering finishes, click **Close** to close the **Data Gathering Status** dialog box and complete the configuration.  

##  <a name="BKBM_ConfigSrcSites"></a> Identify additional source sites of the source hierarchy  
 When you configure a supported source hierarchy, the top-level site of that hierarchy is automatically configured as a source site, and data is automatically gathered from that site. The next action that you take depends on the version of Configuration Manager that is run by the source hierarchy:  

-   For a Configuration Manager 2007 source hierarchy, you can begin migration from that initial source site or set up additional source sites from the source hierarchy after the data gathering finishes for the initial source site. To migrate data that is only available from a child site, set up additional source sites for a Configuration Manager 2007 hierarchy. For example, you might configure additional source sites to gather data about content that you want to migrate when it's created at a child site in the source hierarchy and is not available at the top site of the source hierarchy.  

-   For a System Center 2012 Configuration Manager or System Center Configuration Manager source hierarchy, you do not need to configure additional source sites. This is because these versions of Configuration Manager use a shared database that is available at the top-level site of the source hierarchy. The shared database has all the information that you can migrate from all of the sites in that source hierarchy. This makes the data that you can migrate available from the top-level site of the source hierarchy.  

When you configure additional source sites for a Configuration Manager 2007 source hierarchy, you must configure the additional source sites from the top of the source hierarchy to the bottom. You must configure a parent site as a source site before you configure any of its child sites as source sites.  

Use the following procedure to configure additional source sites for Configuration Manager 2007 source hierarchies:  

### To identify additional source sites in the source hierarchy 

1.  In the Configuration Manager console, click **Administration**.  

2.  In the **Administration** workspace, expand **Migration**, and then click **Source Hierarchy**.  

3.  Choose the site that you want to configure as a source site.  

4.  On the **Home** tab, in the **Source Site** group, click **Configure**.  

5.  In the **Source Site Credentials** dialog box, for the source site access accounts, specify accounts that have the following permissions:  

    -   Source Site Account: **Read** permission to the SMS Provider for the specified top-level site in the source hierarchy. Distribution point sharing and upgrades require **Modify** and **Delete** permissions to the site in the source hierarchy.  

    -   Source Site Database Account: **Read** and **Execute** permission to the SQL Server database for the specified top-level site in the source hierarchy.  

    If you specify the use of the computer account, Configuration Manager uses the computer account of the top-level site of the destination hierarchy. For this option, ensure that this account is a member of the security group **Distributed COM Users** in the domain where the top-level site of the source hierarchy resides.  

6.  To share distribution points between the source and destination hierarchies, select the **Enable distribution point sharing for the source site server** check box. If you do not enable distribution point sharing at this time, you can do so by editing the credentials for the source site after data gathering has finished.  

7. Click **OK** to save the configuration. This opens the **Data Gathering Status** dialog box, and data gathering starts automatically.  

8.  When data gathering finishes, click **Close** to complete the configuration.  
