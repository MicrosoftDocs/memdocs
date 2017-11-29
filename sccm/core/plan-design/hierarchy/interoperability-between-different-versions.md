---
title: "Interoperability between versions"
titleSuffix: "Configuration Manager"
description: "Learn how to avoid conflicts between multiple System Center Configuration Manager hierarchies on the same network."
ms.custom: na
ms.date: 1/30/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9b0a7859-747f-4495-a2f4-13fd5991f897
caps.latest.revision: 8
author: aaroncz
ms.author: aaroncz
manager: angrobe

---
# Interoperability between different versions of System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

You can install and operate multiple, independent hierarchies of System Center Configuration Manager on the same network. However, because different hierarchies of Configuration Manager do not interoperate outside of the migration process, each hierarchy requires configurations to prevent conflicts between them. Additionally, you can create certain configurations to help resources that you manage interact with the site systems from the correct hierarchy.  

 The following sections provide information about using different versions of Configuration Manager on the same network:  

-   [Interoperability between System Center Configuration Manager and earlier product versions](#BKMK_SupConfigInterop)  

-   [Interoperability for the Configuration Manager Console](#BKMK_ConsoleInterop)  

-   [Configuration Manager limitations in a mixed-version hierarchy](#bkmk_mixed)  

##  <a name="BKMK_SupConfigInterop"></a> Interoperability between System Center Configuration Manager and earlier product versions  
 Sites of different versions cannot coexist in the same hierarchy, except during the process of upgrade from System Center 2012 Configuration Manager to System Center Configuration Manager, or from one System Center Configuration Manager version to a newer version (using in-console updates).   

 Because you can deploy a System Center Configuration Manager site and hierarchy side-by-side with an existing System Center 2012 Configuration Manager site or hierarchy, we recommend that you plan to prevent clients from either version from trying to join a site from the other version.

For example, if two or more Configuration Manager hierarchies have overlapping boundaries (See [overlapping boundaries](/sccm/core/servers/deploy/configure/boundary-groups#overlapping-boundaries)) that include the same network locations, it's a best practice to assign each new client to a specific site instead of using automatic site assignment. For information about automatic site assignment in System Center 2012 Configuration Manager, see [How to assign clients to a site in System Center Configuration Manager](../../../core/clients/deploy/assign-clients-to-a-site.md).  

 Additionally, you can't install a client from System Center 2012 Configuration Manager on a computer that hosts a site system role from System Center Configuration Manager, nor can you install a System Center Configuration Manager client on a computer that hosts a site system role from System Center 2012 Configuration Manager.  

 Similarly, the following clients and the following Virtual Private Network (VPN) connection are not supported:  

-   Any System Center 2012 Configuration Manager or earlier computer client version  

-   Any System Center 2012 Configuration Manager or earlier device management client  

-   Windows CE Platform Builder device management client (any version)  

-   System Center Mobile Device Manager VPN connection  

###  <a name="BKMK_SupConfigSiteAssignment"></a> Client site assignment considerations  
 System Center Configuration Manager clients can be assigned to only a single primary site. When automatic site assignment is used to assign clients to a site during client installation, and more than one boundary group includes the same boundary, and the boundary groups have different assigned sites, the actual site assignment of a client cannot be predicted.  

 If boundaries overlap across multiple Configuration Manager sites and hierarchies, clients might not be assigned to the site you expect,  or might not get assigned to a site at all.  

 System Center Configuration Manager clients check the version of the Configuration Manager site before they complete site assignment, and cannot be assigned to a previous version when and if site boundaries overlap. However, System Center 2012 Configuration Manager clients might incorrectly be assigned to a System Center Configuration Manager site.  

 To prevent clients from unintentionally being assigned to the wrong site when two hierarchies have overlapping boundaries, we recommend that you configure Configuration Manager client installation parameters to assign clients to a specific site.  

##  <a name="bkmk_mixed"></a> Configuration Manager limitations  in a mixed-version hierarchy  
 When you're in the process of upgrading a System Center Configuration Manager site, there are times when different sites will have different versions. For example, you might upgrade a central administration site to a new version but due to site maintenance windows, one or more primary sites might not upgrade until a later time and date.  

 When different sites in a single hierarchy run different versions, some functionality is not available. This can affect how you manage Configuration Manager objects in the Configuration Manager console, and which functionality is available to clients. Typically, functionality from the newer version of Configuration Manager is not accessible at sites or to clients that run a lower service pack version.  

### Limitations when upgrading  Configuration Manager  

|Object|Details|  
|------------|-------------|  
|Network access account|**When upgrading from System Center 2012 Configuration Manager to System Center Configuration Manager:** When you view the network access account details from a Configuration Manager console that's connected to a  central administration site that has updated to System Center Configuration Manager, the console does not display details for accounts that are configured at a primary site that runs System Center 2012 Configuration Manager. After the primary site upgrades to the same version as the central administration site, the account details are visible in the console.<br /><br /> **When upgrading between System Center Configuration Manager versions:** When you view the network access account details from a Configuration Manager console that's connected to a  central administration site that has updated to a new version of System Center Configuration Manager, the console does not display details for accounts that are configured at a primary site that runs a previous version. After the primary site upgrades to the same version as the central administration site, the account details are visible in the console.|  
|Boot images for operating system deployment|**When upgrading from System Center 2012 Configuration Manager to System Center Configuration Manager:**  When the top-level site of a hierarchy upgrades to System Center Configuration Manager, the default boot images are automatically updated to boot images based on Windows Assessment and Deployment Kit 10 (Windows ADK). Use these boot images only for deployments to clients at System Center Configuration Manager sites. For more information, see [Planning for operating system deployment interoperability in System Center Configuration Manager](../../../osd/plan-design/planning-for-operating-system-deployment-interoperability.md).<br /><br /> **When upgrading between System Center Configuration Manager versions:** As long as new versions of cm6long do not update the version of Windows ADK that's in use, there is no effect on boot images.|  
|New task sequence steps|When you create a task sequence with a step introduced in one version of Configuration Manager that is not available in an earlier version, you might encounter the following issues:<br /><br /> --   An error occurs when you try to edit the task sequence from a site that's running a previous version of Configuration Manager.<br /><br /> -- The task sequence doesn't run on a computer that runs a previous version of the Configuration Manager client.|  
|Client to down-level management point communications|A Configuration Manager client that communicates with a management point from a site that runs a lower version than the client can only use functionality that the down-level version of Configuration Manager supports. For example, if you deploy content from a System Center Configuration Manager site that was recently upgraded to a client that communicates with a management point that has not yet upgraded to that version, that client cannot use new functionality from the latest version.|  

##  <a name="BKMK_ConsoleInterop"></a> Interoperability for the Configuration Manager console  
 The following table contains information about the use of the Configuration Manager console in an environment that has a mix of Configuration Manager versions.  

|Interoperability environment|More information|  
|----------------------------------|----------------------|  
|An environment with both System Center 2012 Configuration Manager and System Center Configuration Manager|To manage a Configuration Manager site, both the console and the site the console connects to must run the same version of Configuration Manager. For example, you cannot use a System Center 2012 Configuration Manager console to manage a System Center Configuration Manager site, or vice versa.<br /><br /> It is not supported to install both the System Center 2012 Configuration Manager console and the System Center Configuration Manager console on the same computer.|  
|An environment with multiple versions of System Center Configuration Manager|System Center Configuration Manager does not support installing more than a single Configuration Manager console on a computer. To use multiple consoles that are specific to different versions of System Center Configuration Manager, you must install the different consoles on separate computers.<br /><br /> During the process of updating sites in a hierarchy to a new version, you can connect a console to a site that runs a newer version and view information about other sites in that hierarchy. However, this configuration is not recommended as it is possible that differences between the console version and Configuration Manager site version can result in data issues, and some features that are available in the latest product version will not be available in the console. <br /></br /> It is not supported to manage a site when using a console with a version that does not match the site version. Doing so might cause loss of data and can put your site at risk. For example, it is not supported to use a console from version 1610 to manage a site that runs version 1606. |
