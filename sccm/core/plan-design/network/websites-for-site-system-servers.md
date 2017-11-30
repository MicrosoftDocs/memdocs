---
title: "Websites for site systems"
titleSuffix: "Configuration Manager"
description: "Learn about default and custom websites for site system servers in System Center Configuration Manager."
ms.custom: na
ms.date: 2/8/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 681f0893-e83b-476e-9ec0-a5dc7c9deeb6
caps.latest.revision: 15
caps.handback.revision: 0
author: mstewart
ms.author: mstewart
manager: angrobe

---
# Websites for site system servers in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Several Configuration Manager site system roles require the use of Microsoft Internet Information Services (IIS) and use the default IIS website to host site system services. When you must run other web applications on the same server and settings are not compatible with Configuration Manager, consider using a custom website for Configuration Manager.  

> [!TIP]  
>  A security best practice is to dedicate a server for the Configuration Manager site systems that require IIS. When you run other applications on a Configuration Manager site system, you increase the attack surface of that computer.  




##  <a name="BKMK_What2Know"></a> What to know before choosing to use custom websites  
 By default, site system roles use the **Default Web Site** in IIS. This is set up automatically when the site system role installs. However, at primary sites, you can choose to use custom websites instead. When you use custom websites:  

-   Custom websites are enabled for the entire site instead of for individual site system servers or roles.  

-   At primary sites, each computer that will host an applicable site system role must be set up with a custom website named **SMSWEB**. Until you create this website and set up site system roles on that computer to use the custom website, clients might not be able to communicate with site system roles on that computer.  

-   Because secondary sites are automatically set up to use a custom website when their primary parent site is set up to do so, you must also create custom websites in IIS on each secondary site system server that requires IIS.  


  **Prerequisites for using custom websites:**  

 Before you enable the option to use custom websites at a site, you must:  

-   Create a custom website named **SMSWEB** in IIS on each site system server that requires IIS. Do this at the primary site and at any child secondary sites.  

-   Set up the custom website to respond to the same port that you set up for Configuration Manager client communication (client request port).  

-   For each custom or default website that uses a custom folder, place a copy of the default document type that you use in the root folder that hosts the website. For example, on a Windows Server 2008 R2 computer that has default configurations, **iisstart.htm** is one of several default document types that are available. You can find this file in the root of the default website and then place a copy of this file (or a copy of the default document type that you use) in the root folder that hosts the SMSWEB custom website. For more about default document types, see [Default Document &lt;defaultDocument\> for IIS](http://www.iis.net/configreference/system.webserver/defaultdocument).  

**About IIS requirements:**
**The following site system roles require IIS and a website to host the site system services:**  

-   Application Catalog web service point  

-   Application Catalog website point  

-   Distribution point  

-   Enrollment point  

-   Enrollment proxy point  

-   Fallback status point  

-   Management point  

-   Software update point  

-   State migration point  

Additional considerations:  

-   When a primary site has custom websites enabled, clients that are assigned to that site are directed to communicate with the custom websites instead of the default websites on applicable site system servers  

-   If you use custom websites for one primary site, consider custom websites for all primary sites in your hierarchy to ensure that clients can successfully roam within the hierarchy. (Roaming is when a client computer moves to a new network segment that is managed by a different site. Roaming can affect resources that a client can access locally instead of across a WAN link).  

-   Site system roles that use IIS but do not accept client connections, like the reporting services point, also use the SMSWEB website instead of the default website.  

-   Custom websites require you to assign port numbers that differ from those that the computer's default website uses. A default website and custom website cannot run at the same time if both websites try to use the same TCP/IP ports.  

-   The TCP/IP ports that you set up in IIS for the custom website must match the client request ports for the site.  

## Switch between default and custom websites  
Although you can check or uncheck the box for using custom websites at a primary site at any time (the box is on the General tab of the site's Properties), plan carefully before you make this change. When this configuration changes, all applicable site system roles at the primary site and child secondary sites must uninstall and then reinstall:  

The following roles **reinstall automatically**:  

-   Management point  

-   Distribution point  

-   Software update point  

-   Fallback status point  

-   State migration point  

The following roles must be **manually reinstalled**:  

-   Application Catalog web service point  

-   Application Catalog website point  

-   Enrollment point  

-   Enrollment proxy point  

Additionally:  

-   When you change from the default website to use a custom website, Configuration Manager does not remove the old virtual directories. If you want to remove the files that Configuration Manager used, you must manually delete the virtual directories that were created under the default website.  

-   If you change the site to use custom websites, clients that are already assigned to the site must then be reconfigured to use the new client request ports for the custom websites. See [How to configure client communication ports in System Center Configuration Manager](../../../core/clients/deploy/configure-client-communication-ports.md).  

## Set up custom websites  
Because the steps to create a custom website vary for different operating system versions, refer to documentation for your operating system version for exact steps, but use the following information when applicable:  

-   The website name must be: **SMSWEB**.  

-   When you set up HTTPS, you must specify a SSL certificate before you can save the configuration.  

-   After you create the custom website, remove the custom website ports that you use from other websites in IIS:  

    1.  Edit the **Bindings** of the other websites to remove ports that match those that are assigned to the **SMSWEB** website.  

    2.  Start the **SMSWEB** website.  

    3.  Restart the **SMS_SITE_COMPONENT_MANAGER** service on the site server of the site.  
