---
# required metadata

title: Plan for software updates synchronization | Configuration Manager
description:
keywords:
author: dougeby
manager: angrobe
ms.date: 9/14/2016
ms.topic: article
ms.prod:
ms.service:
ms.technology:
ms.assetid: 8938c566-64a8-437a-861a-02be080133f8

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
#ms.reviewer:
#ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

#  <a name="BKMK_SyncSettings"></a> Plan for software updates synchronization  
Software updates synchronization in Configuration Manager is the process of retrieving the software updates metadata that meets the criteria that you configure. The top-level site in your hierarchy, the central administration site or stand-alone primary site, synchronizes software updates from Microsoft Update. You also have the option to configure the software update point on the top-level site to synchronize with an existing WSUS server, not in the Configuration Manager hierarchy. The child primary sites synchronize software updates metadata from the software update point on the central administration site. Before you install and configure a software update point, use this topic to plan for software updates synchronization and settings associated with synchronization.

The following sections provide information about synchronization settings that you will configure as part of the software update point installation.



## <a name="BKMK_SyncSource"></a> Synchronization source
To successfully complete the synchronization, the software update point must have access to its upstream synchronization source. When the software update point is disconnected from the upstream synchronization source, you must use the WSUSUtil tool to export software updates metadata from a software updates source and import the metadata to the disconnected software update point. The following table lists the software update point types and the upstream synchronization source for which the software update point requires access.  

  |Software update point|Upstream synchronization source|  
  |---------------------------|-------------------------------------|  
  |Central administration site|Microsoft Update (Internet)<sup>1</sup><br /><br /> Existing WSUS server|  
  |Stand-alone primary site|Microsoft Update (Internet)<sup>1</sup><br /><br /> Existing WSUS server|  
  |Child primary site|Central administration site|  
  |Secondary site|Parent primary site|  

   <sup>1</sup>When the software update point is disconnected from the upstream update source, you can manually perform software updates synchronization. For more information, see [Synchronize software updates from a disconnected software update point](../get-started/syncrhonize-software-updates-disconnected.md#BKMK_SyncDisconnected).




### <a name="BKMK_SyncSource"></a> Synchronization source settings
 The synchronization source settings for the software update point specify the location for where the software update point retrieves software updates metadata, and whether the WSUS reporting events are created during the synchronization process.  

-   **Synchronization source:** The software update point at the top-level site configures the synchronization source for Microsoft Update by default. You have the option to synchronize the top-level site with an existing WSUS server. The software update point on a child primary site configures the synchronization source as the software update point at the central administration site by default.  

    > [!NOTE]  
    >  The first software update point that you install at a primary site, which is the default software update point, synchronizes with the central administration site. Additional software update points at the primary site synchronize with the default software update point at the primary site.  

     When a software update point is disconnected from Microsoft Update or from the upstream update server, you can configure the synchronization source not to synchronize with a configured synchronization source, but instead to use the export and import function of the WSUSUtil tool to synchronize software updates. For more information, see [Synchronize software updates from a disconnected software update point](../../sum/deploy-use/configure-software-updates.md#BKMK_SyncDisconnected).  

-   **WSUS reporting events:** The Windows Update Agent on client computers can create event messages that are used for WSUS reporting. These events are not used by software update in Configuration Manager, and therefore, the **Do not create WSUS reporting events** option is selected by default. When these events are not created, the only time that the client computer should connect to the WSUS server is during software update evaluation and compliance scans. If these events are needed for reporting outside of software updates in Configuration Manager, you will need to modify this setting to create WSUS reporting events.  

##  <a name="BKMK_SyncSchedule"></a> Synchronization schedule  
 You can configure the synchronization schedule only at the software update point on the top-level site in the Configuration Manager hierarchy. When you configure the synchronization schedule, the software update point synchronizes with the synchronization source at the date and time that you specified. The custom schedule allows you to synchronize software updates on a date and time when the demands from the WSUS server, site server, and network are low, such as 2:00 AM once a week. Alternatively, you can initiate synchronization on the top-level site by using the **Synchronization Software Updates** action from the **All Software Updates** or **Software Update Groups** node in the Configuration Manager console.  

> [!TIP]  
>  Schedule the software updates synchronization to run by using a time frame that is appropriate for your environment. One common scenario is to set the software updates synchronization schedule to run shortly after the Microsoft regular security update release on the second Tuesday of each month, which is typically referred to as Patch Tuesday. Another common scenario is to set the software updates synchronization schedule to run daily when you use software updates to deliver the Endpoint Protection definition and engine updates.  

 After the software update point successfully completes synchronization, a synchronization request is sent to child sites. If you have additional software update points at a primary site, a synchronization request is sent to each software update point. The process is repeated on every site in the hierarchy.  

##  <a name="BKMK_UpdateClassifications"></a> Update classifications  
 Every software update is defined with an update classification that helps to organize the different types of updates. During the synchronization process, the software updates metadata for the specified classifications will be synchronized. Configuration Manager allows you to synchronize software updates with the following update classifications:  

-   **Critical Updates:** Specifies a broadly released update for a specific problem that addresses a critical, non-security-related bug.  

-   **Definition Updates:** Specifies an update to virus or other definition files.  

-   **Feature Packs:** Specifies new product features that are distributed outside of a product release and feature that are typically included in the next full product release.  

-   **Security Updates:** Specifies a broadly released update for a product-specific, security-related issue.  

-   **Service Packs:** Specifies a cumulative set of hotfixes that are applied to an application. These hotfixes can include security updates, critical updates, software updates, and so on.  

-   **Tools:** Specifies a utility or feature that helps to complete one or more tasks.  

-   **Update Rollups:** Specifies a cumulative set of hotfixes that are packaged together for easy deployment. These hotfixes can include security updates, critical updates, updates, and so on. An update rollup generally addresses a specific area, such as security or a product component.  

-   **Updates:** Specifies an update to an application or file that is currently installed.  

 The update classification settings are configured only on the top-level site. The update classification settings are not configured on the software update point on child sites, because the software updates metadata is replicated from the top-level site to child primary sites. When you select the update classifications, be aware that the more classifications that you select, the longer it takes to synchronize the software updates metadata.  

> [!WARNING]  
>  As a best practice, clear all classifications before you synchronize software updates for the first time. After the initial synchronization, select the classifications from Software Update Point Component properties, and then re-initiate synchronization.  

##  <a name="BKMK_UpdateProducts"></a> Products  
 The metadata for each software update defines  one or more products for which the update is applicable. A product is a specific edition of an operating system or application. An example of a product is Microsoft Windows Server 2008. A product family is the base operating system or application from which the individual products are derived. An example of a product family is Microsoft Windows, of which Microsoft Windows Server 2008 is a member. You can specify a product family or individual products within a product family.  

 When software updates are applicable to multiple products, and at least one of the products is selected for synchronization, all of the products will appear in the Configuration Manager console even if some products were not selected. For example, if Windows Server 2012 is the only operating system that you subscribed to, and if a software update applies to Windows Server 2012 and Windows Server 2012 Datacenter Edition, both products will be in the site database.  

 The product settings are configured only on the top-level site. The product settings are not configured on the software update point for child sites because the software updates metadata is replicated from the top-level site to child primary sites. When you select products, be aware that the more products that you select, the longer it will take to synchronize the software updates metadata.  

> [!IMPORTANT]  
>  Configuration Manager stores a list of products and product families that you can choose from when you first install the software update point. Products and product families that are released after Configuration Manager is released might not be available to select until you complete software updates synchronization, which updates the list of available products and product families from which you can choose. As a best practice, clear all products before you synchronize software updates for the first time. After the initial synchronization, select the products from Software Update Point Component properties, and then reinitiate synchronization.  

##  <a name="BKMK_SupersedenceRules"></a> Supersedence rules  
 Typically, a software update that supersedes another software update does one or more of the following actions:  

-   Enhances, improves, or updates the fix that was provided by one or more previously released updates.  

-   Improves the efficiency of the superseded update file package, which is installed on client computers if the update is approved for installation. For example, the superseded update might contain files that are no longer relevant to the fix or to the operating systems that are supported by the new update, so those files are not included in the superseding  file package of the update.  

-   Updates newer versions of a product. In other words, it updates versions that are no longer applicable to older versions or configurations of a product. Updates can also supersede other updates if modifications were made to expand language support. For example, a later revision of a product update for Microsoft Office might remove the support for an older operating system, but it might add additional support for new languages in the initial update release.  

 In the properties for the software update point, you can specify that the superseded software updates are immediately expired, which prevents them from being included in new deployments and flags the existing deployments to indicate that they contain one or more expired software updates. Or, you can specify a period of time before the superseded software updates are expired, which allows you to continue to deploy them. Consider the following scenarios in which you might need to deploy a superseded software update:  

-   If a superseding software update supports only newer versions of an operating system, and some of your client computers run earlier versions of the operating system.  

-   If a superseding software update has more restricted applicability than the software update it supersedes. This would make it inappropriate for some client computers.  

-   If a superseding software update was not approved for deployment in your production environment.  

##  <a name="BKMK_UpdateLanguages"></a> Languages  
 The language settings for the software update point allow you to configure the languages for which the summary details (software updates metadata) are synchronized for software updates, and the software update file languages that will be downloaded for software updates.  

### Software update file  
 The languages that you configure for the **Software update file** setting in the properties for the software update point provide the default set of languages that are available when you download software updates at a site. You can modify the languages that are selected by default each time that the software updates are downloaded or deployed. During the download process, the software update files for the configured languages are downloaded to the deployment package source location, if the software update files are available in the selected language. Then they are  copied to the content library on the site server, and then they are copied to the distribution points that are configured for the package.  

 The software update file language settings should be configured with the languages that are most often used in your environment. For example, if client computers that are assigned to the site use mostly English and Japanese languages for the operating system or applications, and there are very few other languages that are used at the site, then select English and Japanese in the **Software Update File** column when you download or deploy the software update and clear the other languages. This allows you to use the default settings on the **Language Selection** page of the deployment and to download wizards. This also prevents unneeded update files from being downloaded. This setting is configured at each software update point in the Configuration Manager hierarchy.  

### Summary details  
 During the synchronization process, the summary details information (software updates metadata) is updated for software updates in the languages that you specify. The metadata provides the information about the software update, such as name, description, products that the update supports, update classification, article ID, download URL, applicability rules, and so on.  

 The summary details settings are configured only on the top-level site. The summary details are not configured on the software update point on child sites because the software updates metadata is replicated from the central administration site down to these sites by using file-based replication. When you select the summary details languages, select only the languages that you need in your environment. The more languages that you select, the longer it takes to synchronize the software updates metadata. Configuration Manager displays the software updates metadata in the locale of the operating system in which the Configuration Manager console runs. If the localized properties for the software updates are not available in the locale of the operating system, the software updates information displays in English.  

> [!IMPORTANT]  
>  It is important that you select all of the summary details languages that you will need in your Configuration Manager hierarchy. When the software update point on top-level site synchronizes with the synchronization source, the selected summary details languages determine the software updates metadata that is retrieved. If you modify the summary details languages after synchronization ran at least one time, the software updates metadata is retrieved for the modified summary details languages only for new or updated software updates. The software updates that have already been synchronized are not updated with new metadata for the modified languages unless there is a change to the software update on the synchronization source.  

