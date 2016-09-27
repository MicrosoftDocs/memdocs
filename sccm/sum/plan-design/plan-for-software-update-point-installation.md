---
# required metadata

title: Plan for software update point installation | Configuration Manager
description:
keywords:
author: dougeby
manager: angrobe
ms.date: 9/14/2016
ms.topic: article
ms.prod:
ms.service:
ms.technology:
ms.assetid: d6284c33-59b4-4f85-bed8-a956af91f707

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
#ms.reviewer:
#ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

#  <a name="BKMK_SUPInstallation"></a> Plan for Software Update Point installation  
 Before you create a software update point site system role in Configuration Manager, there are several requirements that you must consider depending on your Configuration Manager infrastructure. When you configure the software update point to communicate by using SSL, this section is especially important to review because you must take additional steps for the software update points in your hierarchy will work properly. This section provides information about the steps that you must take to successfully plan and prepare for the software update point installation.  

##  <a name="BKMK_SUPSystemRequirements"></a> Requirements for the software update point  
 The software update point site system role must be installed on a site system that meets the minimum requirements for WSUS and the supported configurations for Configuration Manager site systems.  

-   For more information about the minimum requirements for the WSUS server role in Windows Server 2012, see [Step 1: Prepare for Your WSUS Deployment](http://go.microsoft.com/fwlink/p/?LinkId=271144) in the Windows Server 2012 documentation library.  

-   For more information about the supported configurations for Configuration Manager site systems, see [Supported configurations for System Center Configuration Manager](../../core/plan-design/configs/supported-configurations.md).  

##  <a name="BKMK_PlanningForWSUS"></a> Plan for WSUS installation  
 Software updates requires that a supported version of WSUS is installed on all site system servers that you configure for the software update point site system role. Additionally, when you do not install the software update point on the site server, you must install the WSUS Administration Console on the site server computer, if it is not already installed. This allows the site server to communicate with WSUS that runs on the software update point.  

 When you use WSUS on Windows Server 2012, you must configure additional permissions to allow **WSUS Configuration Manager** in Configuration Manager to connect to the WSUS in order to perform periodic health checks. Choose one of the following options to configure the permissions:  

-   Add the **SYSTEM** account to the **WSUS Administrators** group  

-   Add the **NT AUTHORITY\SYSTEM** account as a user for the WSUS database (SUSDB) and configure a minimum of the webService database role membership  

 For more information about how to install WSUS on Windows Server 2012, see [Install the WSUS Server Role](http://go.microsoft.com/fwlink/p/?LinkId=272355) in the Windows Server 2012 documentation library.  

 When you install more than one software update point at a primary site, use the same WSUS database for each software update point in the same Active Directory forest. If you share the same database, it significantly mitigates, but does not completely eliminate the client and the network performance impact that you might experience when clients switch to a new software update point. A delta scan still occurs when a client switches to a new software update point that shares a database with the old software update point, but the scan is much smaller than it would be if the WSUS server had its own database.  

###  <a name="BKMK_CustomWebSite"></a> Configure WSUS to use a custom web site  
 When you install WSUS, you have the option to use the existing IIS Default website, or to create a custom WSUS website. Create a custom website for WSUS so that IIS hosts the WSUS services in a dedicated virtual website, instead of sharing the same web site that is used by the other Configuration Manager site systems or other applications. This is especially true when you install the software update point site system role on the site server. When you run WSUS in Windows Server 2012, WSUS is configured by default to use port 8530 for HTTP and port 8531 for HTTPS. You must specify these port settings when you create the software update point at a site.  

###  <a name="BKMK_WSUSInfrastructure"></a> Use an existing WSUS infrastructure  
 You can use a WSUS server that was active in your environment before you installed Configuration Manager. When the software update point is configured, you must specify the synchronization settings. Configuration Manager connects to the WSUS that runs on the software update point and configures the WSUS server with the same settings. When the WSUS server was previously synchronized with products or classifications that you did not configure as part of the software update point synchronization settings, the software updates metadata for the products and classifications are synchronized for all of the software updates metadata in the WSUS database regardless of the synchronization settings for the software update point. This might result in unexpected software updates metadata in the site database. You will experience the same behavior when you add products or classifications directly in the WSUS Administration console, and then immediately initiate synchronization. Every hour, by default, Configuration Manager connects to the WSUS that runs on the software update point and resets any settings that were modified outside of Configuration Manager.  

 The software updates that do not meet the products and classifications that you specify in synchronization settings are set to expired, and then they are removed from the site database.  

###  <a name="BKMK_WSUSAsReplica"></a> Configure WSUS as a replica server  
 When you create a software update point site system role on a primary site server, you cannot use a WSUS server that is configured as a replica. When the WSUS server is configured as a replica, Configuration Manager fails to configure the WSUS server, and the WSUS synchronization fails as well. When a software update point is created on a secondary site, Configuration Manager configures WSUS to be a replica server of the WSUS that runs on the software update point at the parent primary site. The first software update point that you install at a primary site is the default software update point. Additional software update points at the site are configured as replicas of the default software update point.  

###  <a name="BKMK_WSUSandSSL"></a> Decide whether to configure WSUS to use SSL  
 You can use the SSL protocol to help secure the WSUS that runs on the software update point. WSUS uses SSL to authenticate client computers and downstream WSUS servers to the WSUS server. WSUS also uses SSL to encrypt software update metadata. When you choose to secure WSUS with SSL, you must prepare the WSUS server before you install the software update point.  

 When you install and configure the software update point, you must select the **Enable SSL communications for the WSUS Server** setting. Otherwise, Configuration Manager will configure WSUS not to use SSL. When you enable SSL for WSUS that runs on a software update point, WSUS that runs on the software update point at any child sites must also be configured to use SSL.  

##  <a name="BKMK_ConfigureFirewalls"></a> Configure firewalls  
 Software updates on a Configuration Manager central administration site communicate with the WSUS that runs on the software update point, which in turn communicates with the synchronization source to synchronize software updates metadata. Software update points on a child site communicate with the software update point at the parent site. When there is more than one software update point at a primary site, the additional software update points must communicate with the first software update point that is installed at the site, which is the default software update point.  

 The firewall might need to be configured to accept the HTTP or HTTPS ports that are used by WSUS in following scenarios: when you have a corporate firewall between the Configuration Manager software update point and the Internet; when you have a software update point and its upstream synchronization source; or when you have the additional software update points. The connection to Microsoft Update is always configured to use port 80 for HTTP and port 443 for HTTPS. You can use a custom port for the connection from WSUS that runs on the software update point at a child site to WSUS that runs on the software update point at the parent site. When your security policy does not allow the  connection, you must use the export and import synchronization method. For more information, see the [Synchronization source](#BKMK_SyncSource) section in this topic. For more information about the ports that are used by WSUS, see [How to determine the port settings used by WSUS in System Center Configuration Manager](../../sum/plan-design/determine-wsus-port-settings.md).  

### Restrict Access to Specific Domains  
 If your organization does not allow the ports and protocols to be open to all addresses on the firewall between the active software update point and the Internet, you can restrict access to the following domains, so that WSUS and Automatic Updates can communicate with Microsoft Update:  

-   http://windowsupdate.microsoft.com  

-   http://*.windowsupdate.microsoft.com  

-   https://*.windowsupdate.microsoft.com  

-   http://*.update.microsoft.com  

-   https://*.update.microsoft.com  

-   http://*.windowsupdate.com  

-   http://download.windowsupdate.com  

-   http://download.microsoft.com  

-   http://*.download.windowsupdate.com  

-   http://test.stats.update.microsoft.com  

-   http://ntservicepack.microsoft.com  

 You might need to add the following addresses to the firewall that is located between the two site systems in the following cases: if child sites have a software update point or if there is a remote active Internet-based software update point at a site:  

 **Software update point on the child site**  

-   http://<*FQDN for software update point on child site*>  

-   https://<*FQDN for software update point on child site*>  

-   http://<*FQDN for software update point on parent site*>  

-   https://<*FQDN for software update point on parent site*>  

