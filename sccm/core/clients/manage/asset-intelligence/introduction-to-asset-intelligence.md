---
title: "Asset Intelligence introduction"
description: "Get an introduction to Asset Intelligence in System Center Configuration Manager."
ms.custom: na
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 0bdfdef5-390f-4099-8bde-de51d9a89175
caps.latest.revision: 7
caps.handback.revision: 0
author: andredm7 
ms.author: andredm 
manager: angrobe

---
# Introduction to Asset Intelligence in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Asset Intelligence in System Center Configuration Manager lets you inventory and manage software license usage throughout your enterprise by using the Asset Intelligence catalog. Many hardware inventory Windows Management Instrumentation (WMI) classes improve the breadth of information that is collected about hardware and software titles that are being used. Over 60 reports present this information in easy-to-use format. Many of these reports link to more specific reports, where you can query for general information and drill down to more detailed information. You can add custom information to the Asset Intelligence catalog, such as custom software categories, software families, software labels, and hardware requirements. You can also connect to System Center Online to dynamically update the Asset Intelligence catalog with the most current information available. Microsoft customers can reconcile enterprise software license usage with purchased software licenses that are being used by importing software license information into the Configuration Manager site database.  

##  <a name="BKMK_AssetIntelligenceCatalog"></a> Asset Intelligence catalog  

 The Configuration Manager Asset Intelligence catalog is a set of database tables stored in the site database that contain categorization and identification information for over 300,000 software titles and versions. These database tables are also used to manage hardware requirements for specific software titles.  

 The Asset Intelligence catalog provides software license information for software titles that are being used, both of Microsoft and of non-Microsoft software. A predefined set of hardware requirements for software titles is available in the Asset Intelligence catalog, and you can create new user-defined hardware requirement information to meet custom requirements. In addition, you can customize information in the Asset Intelligence catalog, and you can upload software title information to System Center Online for categorization.  

 Asset Intelligence catalog updates that contain newly released software are available for download periodically to perform bulk catalog updates. Or, the catalog can be dynamically updated by using the Asset Intelligence synchronization point site system role.  

###  <a name="BKMK_SoftwareCategories"></a> Software categories  
 Asset Intelligence software categories are used to widely categorize inventoried software titles and are also used as high-level groupings of more specific software families. For example, a software category could be energy companies, and a software family within that software category could be oil and gas or hydroelectric. Many software categories are predefined in the Asset Intelligence catalog, and you can create user-defined categories to additionally define inventoried software. The validation state for all predefined software categories is always **Validated**, whereas custom software category information added to the Asset Intelligence catalog is **User Defined**. For more information about how to manage software categories, see [Configuring Asset Intelligence in System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md).  

> [!NOTE]  
>  Predefined software category information that is stored in the Asset Intelligence catalog is read-only and cannot be changed or deleted. Administrative users can add, modify, or delete user-defined software categories.  

###  <a name="BKMK_SoftwareFamilies"></a> Software families  
 Asset Intelligence software families are used to define inventoried software titles within software categories. Many software families are predefined in the Asset Intelligence catalog, and you can create user-defined categories to additionally define inventoried software. The validation state for all predefined software families is always **Validated**, whereas custom software family information added to the Asset Intelligence catalog is **User-Defined**. For more information about how to manage software families, see [Configuring Asset Intelligence in System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md).  

> [!NOTE]  
>  Predefined software family information is read-only and cannot be changed. Administrative users can add, modify, or delete user-defined software families.  

###  <a name="BKMK_CustomLabels"></a> Software labels  
 Asset Intelligence custom software labels let you create filters that you can use to group software titles and to view them by using Asset Intelligence reports. You can use software labels to create user-defined groups of software titles that share a common attribute. For example, you could create a software label called Shareware, associate that software label with inventoried shareware titles, and run a report to display all software titles with the associated Shareware software label. Software labels are not predefined. The validation state for software labels is always **User Defined**. For more information about how to manage software labels, see [Configuring Asset Intelligence in System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md).  

###  <a name="BKMK_HardwareRequirements"></a> Hardware requirements  
 You can use the hardware requirements information to verify that computers meet the hardware requirements for software titles before they are targeted for software deployments. You can manage hardware requirements for software titles in the **Assets and Compliance** workspace in the **Hardware Requirements** node under the **Asset Intelligence** node. Many hardware requirements are predefined in the Asset Intelligence catalog, and you can create new user-defined hardware requirement information to meet custom requirements. The validation state for all predefined hardware requirements is always **Validated**, whereas user-defined hardware requirements information added to the Asset Intelligence catalog is **User Defined**. For more information about how to manage hardware requirements, see [Configuring Asset Intelligence in System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md).  

> [!NOTE]  
>  The hardware requirements displayed in the Configuration Manager console are retrieved from the Asset Intelligence catalog and are not based on inventoried software title information from System Center 2012 Configuration Manager clients. Hardware requirements information is not updated as part of the synchronization process with System Center Online. You can create user-defined hardware requirements for inventoried software that does not have associated hardware requirements.  

 By default, the following information is displayed for each listed hardware requirement:  

-   **Software Title**: Specifies the software title associated with the hardware requirement.  

-   **Minimum CPU (MHz)**: Specifies the minimum processor speed, in megahertz (MHz), required by the software title.  

-   **Minimum RAM (KB)**: Specifies the minimum RAM, in kilobytes (KB), required by the software title.  

-   **Minimum Disk Space (KB)**: Specifies the minimum free hard disk space, in KB, required by the software title.  

-   **Minimum Disk Size (KB)**: Specifies the minimum hard disk size, in KB, required by the software title.  

-   **Validation State**: Specifies the validation state for the hardware requirement.  

 Predefined hardware requirements stored in the Asset Intelligence catalog are read-only and cannot be deleted.  Administrative users can add, modify, or delete user-defined hardware requirements for software titles that are not stored in the Asset Intelligence catalog.  

##  <a name="BKMK_InventoriedSoftwareTitles"></a> Inventoried software titles  
 You can view inventoried software title information in the **Assets and Compliance** workspace in the **Inventoried Software** node under the **Asset Intelligence** node. The Hardware Inventory Client Agent collects the inventoried software information from Configuration Manager clients based on the software titles that are stored in the Asset Intelligence catalog.  

> [!WARNING]  
>  The Hardware Inventory Client Agent collects inventory based on the Asset Intelligence hardware inventory reporting classes that you enable. For more information about how to enable the reporting classes, see [Configuring Asset Intelligence in System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md).  

 By default, the following information is displayed for each inventoried software title:  

-   **Name**: Specifies the name of the inventoried software title.  

-   **Vendor**: Specifies the name of the vendor that developed the inventoried software title.  

-   **Version**: Specifies the product version of the inventoried software title.  

-   **Category**: Specifies the software category that is currently assigned to the inventoried software title.  

-   **Family**: Specifies the software family that is currently assigned to the inventoried software title.  

-   **Label** [**1**, **2**, and **3**]: Specifies the custom labels that are associated with the software title. Inventoried software titles can have up to three custom labels associated with them.  

-   **Count**: Specifies the number of Configuration Manager clients that have inventoried the software title.  

-   **State**: Specifies the validation state for the inventoried software title.  

> [!NOTE]  
>  You can change the categorization information (product name, vendor, software category, and software family) for inventoried software only at the top-level site in your hierarchy. After you modify the categorization information for predefined software, the validation state for the software changes from **Validated** to **User Defined**.  

##  <a name="AssetIntelligenceSycnronizationPoint"></a> Asset Intelligence Synchronization Point  
 The Asset Intelligence synchronization point is a Configuration Manager site system role used to connect to System Center Online (by using TCP port 443) to manage dynamic Asset Intelligence catalog information updates. This site role can be installed only on top-level site of the hierarchy. You must configure all Asset Intelligence catalog customization by using a Configuration Manager console connected to the top-level site. Although all updates must be configured at the top-level site, Asset Intelligence catalog information is replicated to other sites in the hierarchy. The Asset Intelligence synchronization point site role lets you request on-demand catalog synchronization with System Center Online or schedule automatic catalog synchronization. In addition to downloading new Asset Intelligence catalog information, the Asset Intelligence synchronization point can upload custom software title information to System Center Online for categorization. Microsoft treats all software titles uploaded to System Center Online for categorization as public information. Therefore, you should make sure that your custom software titles do not contain confidential or proprietary information.  

> [!NOTE]  
>  After an uncategorized software title is submitted, and there are at least 4 categorization requests from customers for the same software title, System Center Online researchers identify, categorize, and then make the software title categorization information available to all customers who are using the online service. Software titles that represent the most requests for categorization receive the highest priority to categorize. Custom software and line-of-business applications are unlikely to receive a category, and as a best practice, you should not send these software titles to Microsoft for categorization.  

> [!NOTE]  
>  An Asset Intelligence synchronization point site system role is required to connect to System Center Online. For information about how to install an Asset Intelligence synchronization point, see [Configuring Asset Intelligence in System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md).  

##  <a name="BKMK_AssetIntelligenceHomePage"></a> Asset Intelligence home page  
 The **Asset Intelligence** node in the **Asset and Compliance** workspace is the home page for Asset Intelligence in Configuration Manager. The **Asset Intelligence** home page displays a summary dashboard view for Asset Intelligence catalog information.  

> [!NOTE]  
>  The **Asset Intelligence** home page does not automatically update while it is being viewed.  

 The **Asset Intelligence** home page contains the following sections:  

-   **Catalog Synchronization**: Provides information about whether Asset Intelligence is enabled and the current status of the Asset Intelligence synchronization point. The section also provides the synchronization schedule, whether the customer license statement is imported, when status was last updated and the time for the next scheduled update, and number of changes that occurred after the Asset Intelligence synchronization point site system was installed.  

    > [!NOTE]  
    >  The Asset Intelligence catalog synchronization section of the **Asset Intelligence** home page is only displayed if an Asset Intelligence synchronization point site system role was installed.  

-   **Inventoried Software Status**: Provides the count and percentage of inventoried software, software categories, and software families that are identified by Microsoft, identified by an administrator, pending online identification, or unidentified and not pending. The information displayed in table format shows the count for each, and the information displayed in the chart shows the percentage for each.  

##  <a name="BKMK_AssetIntelligenceReports"></a> Asset Intelligence reports  
 The Asset Intelligence reports are located in the Configuration Manager console, in the **Monitoring** workspace, in the Asset Intelligence folder under the **Reporting** node. The reports provide information about hardware, license management, and software. For more information about reports in Configuration Manager, see [Reporting in System Center Configuration Manager](../../../../core/servers/manage/reporting.md).  

> [!NOTE]  
>  The accuracy of the quantity of installed software titles and license information displayed in Asset Intelligence reports might vary from the actual number of software titles installed or licenses that are used in the environment. This variation is because of the complex dependencies and limitations involved in inventorying software license information for software titles that are installed in enterprise environments. Do not use Asset Intelligence reports as the sole source for determining purchased software license compliance.  

###  <a name="BKMK_HardwareReports"></a> Asset Intelligence hardware reports  
 Asset Intelligence hardware reports provide information about hardware assets in the organization. By using hardware inventory information, such as speed, memory, peripheral devices, and more, Asset Intelligence hardware reports can present information about USB devices, about hardware that must be upgraded, and even about computers that are not ready for a specific software upgrade.  

> [!NOTE]  
>  Some user data in Asset Intelligence hardware reports is collected from the System Security Event Log. For better report accuracy, we recommend that you clear this log when you reassign a computer to a new user.  

###  <a name="BKMK_LicenseManagementReports"></a> Asset Intelligence license management reports  
 Asset Intelligence license management reports provide data about licenses that are being used. The License Ledger report lists installed Microsoft applications in a format congruent with a Microsoft License Statement (MLS). This provides a convenient method of matching purchased licenses with used licenses. Other License Management reports provide information about computers acting as servers that run the Key Management Service (KMS) for operating system activation statistics.  

> [!IMPORTANT]  
>  Several of the Asset Intelligence License Management reports present information about the function of KMS, a method of administering volume licensing. If a KMS server has not been implemented, some reports might not return any data. For more information about KMS, search for KMS on [Microsoft TechNet](http://go.microsoft.com/fwlink/?linkid=3225).  

###  <a name="BKMK_SoftwareReports"></a> Asset Intelligence software reports  
 Asset Intelligence software reports provide information about software families, categories, and specific software titles that are installed on computers in the organization. The software reports present information about browser helper objects, software that starts automatically, and more. These reports can be used to identify adware, spyware, and other malware, and identify software redundancy to help streamline software purchasing and support.  

###  <a name="BKMK_SoftwareIdTagReports"></a> Asset Intelligence software identification tag reports  
 Asset Intelligence software identification tag reports provide information about software that contains a software identification tag that is compliant with ISO/IEC 19770-2. The software identification tags provide authoritative information that is used to identify installed software. When you enable the SMS_SoftwareTag hardware inventory reporting class, Configuration Manager collects information about the software with software identification tags. The following reports provide information about the software:  

-   **Software 14A - Search for software identification tag enabled software**: This report provides the count of installed software with a software identification tag enabled.  

-   **Software 14B - Computers with specific software identification tag enabled software installed**: This report lists all computers that have installed software with a specific software identification tag enabled.  

-   **Software 14C - Installed software identification tag enabled software on a specific computer**: This report lists all installed software with a specific software identification tag enabled on a specific computer.  

###  <a name="BKMK_ReportingLImitations"></a> Asset Intelligence reporting limitations  
 Asset Intelligence reports can provide large amounts of information about installed software titles and purchased software licenses that are being used. However, you should not use this information as the only source for determining purchased software license compliance.  

####  <a name="BKMK_ExampleDependencies"></a> Example dependencies  
 The accuracy of the quantity displayed in the Asset Intelligence reports for installed software titles and license information can vary from the actual amounts currently used. This variation is caused by the complex dependencies involved in inventorying software license information for software titles in use in enterprise environments. The following examples show the dependencies involved in inventorying installed software in the enterprise by using Asset Intelligence that might affect the accuracy of Asset Intelligence reports:  

 **Client hardware inventory dependencies**  
 Asset Intelligence installed software reports are based on data that is collected from Configuration Manager clients by extending hardware inventory to enable Asset Intelligence reporting. Because of this dependency on hardware inventory reporting, Asset Intelligence reports reflect data only from Configuration Manager clients that successfully complete hardware inventory processes with the required Asset Intelligence WMI reporting classes enabled. In addition, because Configuration Manager clients perform hardware inventory processes on a schedule defined by the administrative user, a delay might occur in data reporting that affects the accuracy of Asset Intelligence reports. For example, an inventoried licensed software title might be uninstalled after the client finishes a successful hardware inventory cycle. However, the software title is displayed as installed in Asset Intelligence reports until the client's next scheduled hardware inventory reporting cycle.  

 **Software packaging dependencies**  
 Because Asset Intelligence reports are based on installed software title data that is collected by using standard Configuration Manager client hardware inventory processes, some software title data might not be collected correctly. For example, software installations that do not comply with standard installation processes or software installations that were changed before installation could cause inaccurate Asset Intelligence reporting.  

####  <a name="BKMK_LegalLimitations"></a> Legal limitations  
 The information displayed in Asset Intelligence reports are subject to many limitations and the information displayed in them does not represent legal, accounting, or other professional advice. The information that is provided by Asset Intelligence reports is for information only and should not be used as the only source of information for determining software license usage compliance.  

 The following are example limitations involved in inventorying installed software and license usage in the enterprise by using Asset Intelligence that might affect the accuracy of Asset Intelligence reports:  

 **Microsoft license usage quantity limitations**  
 -   The quantity of purchased Microsoft software licenses is based on information that administrators supply and should be closely reviewed to ensure that the correct number of software licenses is provided.  

-   The reported quantity of Microsoft software licenses contains information only about Microsoft software licenses acquired through volume licensing programs and does not reflect information for software licenses acquired through retail, OEM, or other software license sales channels.  

-   Software licenses acquired in the last 45 days might not be included in the quantity of Microsoft software licenses reported because of software reseller reporting requirements and schedules.  

-   Software license transfers from company mergers or acquisitions might not be reflected in Microsoft software license quantities.  

-   Nonstandard terms and conditions in a Microsoft Volume Licensing (MVLS) agreement might affect the number of software licenses reported and, therefore, might require additional review by a Microsoft representative.  

 **Installed software title quantity limitations**  
 Configuration Manager Clients must successfully complete hardware inventory reporting cycles for the Asset Intelligence reports to accurately report the quantity of installed software titles. Additionally, there might be a delay between the installation or uninstallation of a licensed software title after a successful hardware inventory reporting cycle that is not reflected in Asset Intelligence reports run before the client reports its next scheduled hardware inventory.  

 **License reconciliation limitations**  
 The reconciliation of the quantity of installed software titles to the quantity of purchased software licenses is calculated by using a comparison of the license quantity specified by the administrator and the quantity of installed software titles collected from Configuration Manager client hardware inventories based on the schedule set by the administrator. This comparison does not represent a final Microsoft conclusion of the license positions. The actual license position depends on the specific software title license and usage rights granted by the license terms.  

##  <a name="BKMK_ValidationStates"></a> Asset Intelligence validation states  
 Asset Intelligence validation states represent the source and current validation status of Asset Intelligence catalog information. The following table shows possible Asset Intelligence validation states and administrator actions that can cause them.  

|**State**|**Definition**|**Administrator action**|**Comment**|  
|---------------|--------------------|------------------------------|-----------------|  
|**Validated**|Catalog item was defined by System Center Online researchers.|None.|Best state.|  
|**User Defined**|Catalog item has not been defined by System Center Online researchers.|Customized the local catalog information.|This state is displayed in Asset Intelligence reports.|  
|**Pending**|Catalog item was not defined by System Center Online researchers, but the item was submitted to System Center Online for categorization.|Requested categorization from System Center Online.|Catalog item remains in this state until System Center Online researchers categorize the item, and the Asset Intelligence catalog is synchronized.|  
|**Updateable**|A user-defined catalog item has been categorized differently by System Center Online during subsequent catalog synchronization.|Customized the local Asset Intelligence catalog to categorize an item as user-defined.|You can use the Resolve Conflict action to decide whether to use the new categorization information or the previous user-defined value. For more information about how to resolve conflicts, see [Operations for Asset Intelligence in System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md).|  
|**Uncategorized**|Catalog item has not been defined by System Center Online researchers, the item has not been submitted to System Center Online for categorization, and the administrator has not assigned a user-defined categorization value.|None.|Request categorization or customize local catalog information.<br /><br /> For more information about requesting categorization, see [Operations for Asset Intelligence in System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md).<br /><br /> For more information about how to change the category for the software title, see [Operations for Asset Intelligence in System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md).|  

> [!NOTE]  
>  Catalog items submitted to System Center Online for categorization have a validation state of **Pending** on a central administration site, but continue to be displayed with a validation state of **Uncategorized** on child primary sites.  

> [!NOTE]  
>  After a categorization conflict is resolved, the item is not validated as conflicting again unless later categorization updates introduce new information about the item.  

 For examples of when a validation state might transition from one state to another, see [Example validation state transitions for Asset Intelligence in System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/example-validation-state-transitions-for-asset-intelligence.md).  
