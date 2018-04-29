---
title: "Hierarchy Maintenance Tool"
titleSuffix: "Configuration Manager"
description: "Understand what the Hierarchy Maintenance Tool does, and why you might use it. Includes command-line options reference."
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: cead6825-6113-4ba5-a381-ac3598dfee86
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# Hierarchy Maintenance Tool (Preinst.exe) for System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

The Hierarchy Maintenance tool (Preinst.exe) passes commands to the System Center Configuration Manager Hierarchy Manager while the Hierarchy Manager service is running. The Hierarchy Maintenance tool is automatically installed when you install a Configuration Manager site. You can find Preinst.exe in the \\&lt;*SiteServerName*>\SMS_&lt;*SiteCode*\bin\X64\00000409 shared folder on the site server.  

 You might use the Hierarchy Maintenance tool in the following scenarios:  

-   When secure key exchange is required, there are situations in which you must manually perform the initial public key exchange between sites. For more information, see [Manually Exchange Public Keys Between Sites](#BKMK_ManuallyExchangeKeys) in this topic.  

-   To remove active jobs that are for a destination site that is no longer available.  

-   To delete a site server from the Configuration Manager console when you are unable to uninstall the site by using Setup. For example, if you physically remove a Configuration Manager site without first running Setup to uninstall the site, the site information will still exist in the parent site's database, and the parent site will continue to attempt to communicate with the child site. To resolve this issue, you must run the Hierarchy Maintenance tool and manually delete the child site from the parent site's database.  

-   To stop all Configuration Manager services at a site without having to stop services individually.  

-   When you are recovering a site, you can use the CHILDKEYS option to distribute the public keys from multiple child sites to the recovering site.  

To run the Hierarchy Maintenance tool, the current user must have administrative privileges on the local computer. Also, the user must explicitly have the Site - Administer security right; it is not sufficient that the user inherits this right by being a member of a group that has that permission.  

## Hierarchy Maintenance Tool Command-Line Options  
When you use the Hierarchy Maintenance Tool, you must run it locally on the central administration site, primary site, or secondary site server.  

When you run the Hierarchy Maintenance tool, you must use the following syntax: preinst.exe /&lt;option\>. The following are the command-line options.  

 **/DELJOB &lt;*SiteCode*>** - Use this option at a site to delete all jobs or commands from the current site to the specified destination site.  

 **/DELSITE &lt;*ChildSiteCodeToRemove*>** - Use this option at a parent site to delete the data for child sites from the site database of the parent site. Typically, you use this option if a site server computer is decommissioned before you uninstall the site from it.  

> [!NOTE]  
>  The /DELSITE option does not uninstall the site on the computer specified by the ChildSiteCodeToRemove parameter. This option only removes the site information from the Configuration Manager site database.  

**/DUMP &lt;*SiteCode*>** - Use this option on the local site server to write site control images to the root folder of the drive on which the site is installed. You can write a specific site control image to the folder or write all site control files in the hierarchy.  

-   /DUMP &lt;*SiteCode*> writes the site control image only for the specified site.  

-   /DUMP writes the site control files for all sites.  

An image is a binary representation of the site control file, which is stored in the Configuration Manager site database. The dumped site control file image is a sum of the base image plus the pending delta images.  

After dumping a site control file image with the Hierarchy Maintenance tool, the file name is in the format sitectrl_&lt;*SiteCode*>.ct0.  

**/STOPSITE** - Use this option on the local site server to initiate a shutdown cycle for the Configuration Manager Site Component Manager service, which partially resets the site. When this shutdown cycle is run, some Configuration Manager services on a site server and its remote site systems are stopped. These services are flagged for reinstallation. As a result of this shutdown cycle, some passwords are automatically changed when the services are reinstalled.  

> [!NOTE]  
>  If you want to see a record of shutdown, reinstallation, and password changes for Site Component Manager, enable logging for this component before using this command-line option.  

After the shutdown cycle is started, it proceeds automatically, skipping any non-responding components or computers. However, if the Site Component Manager service cannot access a remote site system during the shutdown cycle, the components that are installed on the remote site system are reinstalled when the Site Component Manager service is restarted. When it is restarted, the Site Component Manager service repeatedly attempts reinstallation of all services that are flagged for reinstallation until it is successful.  

You can restart the Site Component Manager service using Service Manager. After it is restarted, all affected services are uninstalled, reinstalled, and restarted. After you use the /STOPSITE option to initiate the shutdown cycle, you cannot avoid the reinstallation cycles after the Site Component Manager service is restarted.  

**/KEYFORPARENT** - Use this option on a site to distribute the site's public key to a parent site.  

The /KEYFORPARENT option places the public key of the site in the file &lt;*SiteCode*>.CT4 at the root of the program files drive. After you run preinst.exe with this option, manually copy the &lt;*SiteCode*>.CT4 file to the parent site's ...\Inboxes\hman.box folder (not hman.box\pubkey).  

**/KEYFORCHILD** - Use this option on a site to distribute the site's public key to a child site.  

The /KEYFORCHILD option places the public key of the site in the file &lt;*SiteCode*>.CT5 at the root of the program files drive. After you run preinst.exe with this option, manually copy the &lt;*SiteCode*>.CT5 file to the child site's ...\Inboxes\hman.box folder (not hman.box\pubkey).  

**/CHILDKEYS** - You can use this option on the child sites of a site that you are recovering. Use this option to distribute public keys from multiple child sites to the recovering site.  

The /CHILDKEYS option places the key from the site where you run the option, and all of that sites child sites public keys into the file &lt;*SiteCode*>.CT6.  

After you run preinst.exe with this option, manually copy the &lt;*SiteCode*>.CT6 file to the recovering site's ...\Inboxes\hman.box folder (not hman.box\pubkey).  

**/PARENTKEYS** - You can use this option on the parent site of a site that you are recovering. Use this option to distribute public keys from all parent sites to the recovering site.  

The /PARENTKEYS option places the key from the site where you run the option, and the keys from each parent site above that site into the file &lt;SiteCode\>.CT7.  

After you run preinst.exe with this option, manually copy the &lt;*SiteCode*>.CT7 file to the recovering site's ...\Inboxes\hman.box folder (not hman.box\pubkey).  

##  <a name="BKMK_ManuallyExchangeKeys"></a> Manually Exchange Public Keys Between Sites  
By default, the **Require secure key exchange** option is enabled for Configuration Manager sites. When secure key exchange is required, there are two situations in which you must manually perform the initial key exchange between sites:  

-   If the Active Directory schema has not been extended for Configuration Manager  

-   Configuration Manager sites are not publishing site data to Active Directory  

You can use the Hierarchy Maintenance tool to export the public keys for each site. Once they have been exported, you must manually exchange the keys between the sites.  

> [!NOTE]  
>  After the public keys are manually exchanged, you can review the **hman.log** log file, which records site configuration changes and site information publication to Active Directory Domain Services, on the parent site server to ensure that the primary site has processed the new public key.  

#### To manually transfer the child site public key to the parent site  

1.  While logged on to the child site, open a command prompt and navigate to the location of **Preinst.exe**.  

2.  Type the following to export the child site's public key: **Preinst /keyforparent**  

3.  The /keyforparent option places the public key of the child site in the **&lt;site code\>.CT4** file located at the root of the system drive.  

4.  Move the **&lt;site code\>.CT4** file to the parent site's **&lt;install directory\>\inboxes\hman.box** folder.  

#### To manually transfer the parent site public key to the child site  

1.  While logged on to the parent site, open a command prompt and navigate to the location of **Preinst.exe**.  

2.  Type the following to export the parent site's public key: **Preinst /keyforchild**.  

3.  The /keyforchild option places the public key of the parent site in the **&lt;site code\>.CT5** file located at the root of the system drive.  

4.  Move the **&lt;site code\>.CT5** file to the **&lt;install directory\>\inboxes\hman.box** directory on the child site.  
