---
title: Use Asset Intelligence
titleSuffix: Configuration Manager
description: Do common Asset Intelligence tasks in Configuration Manager.
ms.date: 08/30/2017
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: conceptual
author: sheetg09
ms.author: sheetg
manager: apoorvseth
ms.localizationpriority: medium
ms.reviewer: mstewart,aaroncz 
ms.collection: tier3
---
# How to use Asset Intelligence in Configuration Manager

*Applies to: Configuration Manager (current branch)*

This topic contains information to help you manage typical Asset Intelligence tasks in your Configuration Manager hierarchy:  

##  <a name="BKMK_ViewInformation"></a> View Asset Intelligence information  
 You can view Asset Intelligence information on the **Asset Intelligence** home page and in Asset Intelligence reports.  

###  <a name="BKMK_AssetIntelligenceHomePage"></a> Asset Intelligence home page  
 The **Asset Intelligence** home page displays a summary dashboard for Asset Intelligence catalog information. On the home page, you can view information about catalog synchronization and inventoried software status. The **Asset Intelligence** home page is divided into the following sections:  

- **Catalog Synchronization**: Provides information about whether Asset Intelligence is enabled, the current status of the Asset Intelligence synchronization point, the synchronization schedule, whether the customer license statement is imported, when status was last updated and the time for the next scheduled update, and the number of changes that occurred after the Asset Intelligence synchronization point site system was installed.  

  > [!NOTE]  
  >  The Asset Intelligence catalog synchronization section of the **Asset Intelligence** home page is only displayed if an Asset Intelligence synchronization point site system role has been installed.  

- **Inventoried Software Status**: Provides the count and percentage of inventoried software, software categories, and software families that are identified by Microsoft, identified by an administrative user, pending online identification, or unidentified and not pending. The information displayed in table format shows the count for each, while the information displayed in the chart shows the percentage for each.  

  Use the following procedure to view Asset Intelligence information on the **Asset Intelligence** home page.  

##### To view Asset Intelligence information on the Asset Intelligence home page  

1.  In the Configuration Manager console, click **Assets and Compliance**.  

2.  In the **Asset and Compliance** workspace, click **Asset Intelligence**. The Asset Intelligence reports are displayed.  

###  <a name="BKMK_AssetIntelligenceReports"></a> Asset Intelligence reports  
 There are over 60 Asset Intelligence reports that display the information collected by Asset Intelligence. Many of these reports link to more specific reports in which you can query for general information and drill down to more detailed information. The Asset Intelligence reports are located in the Configuration Manager console, in the **Monitoring** workspace, under the **Reporting** node. The reports provide information about hardware, license management, and software. For more information about reports in Configuration Manager, see [Introduction to reporting](../../../servers/manage/introduction-to-reporting.md).  

> [!NOTE]  
>  The accuracy of installed software title quantities and license information displayed in Asset Intelligence reports might vary from the actual number of software titles installed or licenses in use in the environment because of the complex dependencies and limitations involved in inventorying software license information for software titles installed in enterprise environments. Asset Intelligence reports should not be used as the sole source for determining purchased software license compliance.  

 Use the following procedure to view Asset Intelligence information by using the Asset Intelligence reports.  

##### To view collected Asset Intelligence information by using Asset Intelligence reports  

1.  In the Configuration Manager console, click **Monitoring**.  

2.  In the **Monitoring** workspace, expand **Reporting**, expand **Reports**, and click **Asset Intelligence**. The Asset Intelligence reports are displayed.  

    > [!WARNING]  
    >  If no report folders exist under the **Reports** node, verify that you have configured reporting. For more information, see [Configuring reporting](../../../../core/servers/manage/configuring-reporting.md).  

3.  Select the Asset Intelligence report that you want to run, and then on the **Home** tab, in the **Report Group** group, click **Run**.  

##  <a name="BKMK_SynchronizeTheCatalog"></a> Synchronize the Asset Intelligence catalog  
 You can synchronize the local Asset Intelligence catalog with System Center Online to retrieve the latest software title categorization. When you manually request catalog synchronization with System Center Online, it could take 15 minutes or longer to complete the synchronization process with System Center Online. Configuration Manager updates the **Last Successful Update** setting on the **Asset Intelligence** home page with the current time for when synchronization successfully finishes.  

> [!NOTE]  
>  An Asset Intelligence synchronization point site system role must first be installed before by using the procedures. For information about installing an Asset Intelligence synchronization point, see [Configuring Asset Intelligence](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md).  

 Use the following procedure to create a synchronization schedule for the Asset Intelligence catalog.  

#### To create a synchronization schedule for the Asset Intelligence catalog  

1. In the Configuration Manager console, click **Assets and Compliance**.  

2. In the **Assets and Compliance** workspace, click **Asset Intelligence**.  

3. On the **Home** tab, in the **Create** group, click **Synchronize**, and then click **Schedule Synchronization**.  

4. In the **Asset Intelligence Synchronization Point Schedule** dialog box, select **Enable synchronization on a schedule**, and then configure a simple or custom schedule.  

5. Click **OK** to save the changes.  

   > [!NOTE]  
   >  For information about the synchronization schedule, including the next scheduled synchronization, see the **Asset Intelligence** node in the **Assets and Compliance** workspace on the top-level site of the hierarchy.  

   Use the following procedure to manually synchronize the Asset Intelligence catalog.  

> [!WARNING]  
>  System Center Online accepts only one manual synchronization request in a 12-hour period.  

###  <a name="BKMK_ManuallySynchronizeCatalog"></a> To manually synchronize the Asset Intelligence catalog  

1.  In the Configuration Manager console, click **Assets and Compliance**.  

2.  In the **Assets and Compliance** workspace, click **Asset Intelligence**.  

3.  On the **Home** tab, in the **Create** group, click **Synchronize**, click **Synchronize Asset Intelligence Catalog**, and then click **OK**.  

##  <a name="BKMK_CustomizeCatalog"></a> Customize the Asset Intelligence catalog  
 Asset Intelligence catalog categorization information received from System Center Online is stored in the site database with read-only permissions and cannot be modified or deleted. However, you can create, modify, and delete custom software categories, software families, software labels, and hardware requirements catalog information. Then you can use custom categorization data instead of the information supplied by System Center Online for existing or user-defined software title information. When you change or add categorization information, the catalog information is considered user-defined. User-defined categorization information is stored in different database tables than validated catalog information.  

###  <a name="BKMK_SoftwareCategories"></a> Software categories  
 Asset Intelligence software categories are used to broadly categorize inventoried software titles and are also used as high-level groupings of more specific software families. For example, a software category could be energy companies, and a software family within that software category could be oil and gas or hydroelectric. Many software categories are predefined in the Asset Intelligence catalog, and additional user-defined categories can be created to further define inventoried software. The validation state for all predefined software categories is always **Validated**, while custom software category information added to the Asset Intelligence catalog is **User Defined**.  

 Use the following procedure to create a user-defined software category.  

##### To create a user-defined software category  

1.  In the Configuration Manager console, click **Assets and Compliance**.  

2.  In the **Assets and Compliance** workspace, click **Asset Intelligence**, and then click **Catalog**.  

3.  On the **Home** tab, in the **Create** group, click **Create Software Category**.  

4.  On the **General** page, enter a name for the new software category and, optionally, a description.  

    > [!NOTE]  
    >  The validation state for all new custom software categories is always set to **User Defined**.  

     Click **Next**.  

5.  On the **Summary** page, review the settings, and then click **Next**.  

6.  On the **Completion** page, click **Close** to exit the wizard.  

###  <a name="BKMK_SoftwareFamilies"></a> Software families  
 Asset Intelligence software families are used to further define inventoried software titles within software categories. For example, a software category could be energy companies, and a software family within that software category could be oil and gas or hydroelectric. Many software families are predefined in the Asset Intelligence catalog, and additional user-defined families can be created to define inventoried software. The validation state for all predefined software families is always **Validated**, while custom software family information added to the Asset Intelligence catalog is **User Defined**.  

 Use the following procedure to create a user-defined software family.  

##### To create a user-defined software family  

1.  In the Configuration Manager console, click **Assets and Compliance**.  

2.  In the **Assets and Compliance** workspace, click **Asset Intelligence**, and then click **Catalog**.  

3.  On the **Home** tab, in the **Create** group, click **Create Software Family**.  

4.  On the **General** page, enter a name for the new software family and, optionally, a description.  

    > [!NOTE]  
    >  The validation state for all new custom software families is always set to **User Defined**.  

5.  On the **Summary** page, review the settings, and then click **Next**.  

6.  On the **Completion** page, click **Close** to exit the wizard.  

###  <a name="BKMK_SoftwareLabels"></a> Software labels  
 Asset Intelligence custom software labels let you create filters that you can use to group software titles and view them by using Asset Intelligence reports. For example, you can create a software label called shareware, associate it with a number of applications, and then run a report that shows you all titles with the software label of shareware. The validation state is **User Defined** for all custom software labels that you add to the Asset Intelligence catalog.  

 Use the following procedure to create a user-defined custom label.  

##### To create a user-defined software label  

1.  In the Configuration Manager console, click **Assets and Compliance**.  

2.  In the **Assets and Compliance** workspace, click **Asset Intelligence**, and then click **Catalog**.  

3.  On the **Home** tab, in the **Create** group, click **Create Software Label**.  

4.  On the **General** page, enter a name for the new software family and, optionally, a description.  

    > [!NOTE]  
    >  The validation state for all new custom software labels is always set to **User Defined**.  

5.  On the **Summary** page, review the settings, and then click **Next**.  

6.  On the **Completion** page, click **Close** to exit the wizard.  

###  <a name="BKMK_HardwareRequirements"></a> Hardware requirements  
 Hardware requirements information can help you verify that computers meet the hardware requirements for software titles before they are targeted for software deployments. Many hardware requirements are predefined in the Asset Intelligence catalog, and you can create new user-defined hardware requirement information to meet custom requirements. The validation state for all predefined hardware requirements is always **Validated**, while user-defined hardware requirements information added to the Asset Intelligence catalog is **User Defined**.  

> [!IMPORTANT]  
>  The hardware requirements displayed in the Configuration Manager console are retrieved from the Asset Intelligence catalog on the local computer and are not based on inventoried software title information from System Center 2012 Configuration Manager clients. Hardware requirements information is not updated as part of the synchronization process with System Center Online. You can create user-defined hardware requirements for inventoried software that does not have associated hardware requirements.  

 Use the following procedure to create a user-defined hardware requirement.  

##### To create a user-defined hardware requirements  

1. In the Configuration Manager console, click **Assets and Compliance**.  

2. In the **Assets and Compliance** workspace, click **Asset Intelligence**, and then click **Hardware Requirements**.  

3. On the **Home** tab, in the **Create** group, click **Create Hardware Requirements**.  

4. On the **General** page, enter the following information:  

   1. **Software title**: Specifies the software title for which the hardware requirements are associated. The software title cannot already exist in the Asset Intelligence catalog.  

   2. **Validation state**: Lists the validation state as **User Defined** for the hardware requirements. You cannot modify this setting.  

   3. **Minimum CPU (MHz)**: Specifies the minimum processor speed, in megahertz (MHz), required by the software title.  

   4. **Minimum RAM (KB)**: Specifies the minimum RAM, in kilobytes (KB), required by the software title.  

   5. **Minimum Disk Space (KB)**: Specifies the minimum free disk space, in KB, required by the software title.  

   6. **Minimum Disk Size (KB)**: Specifies the minimum hard disk size, in KB, required by the software title.  

      Click **Next**.  

5. On the **Summary** page, review the settings, and then click **Next**.  

6. On the **Completion** page, click **Close** to exit the wizard.  

###  <a name="BKMK_ModifyCategorization"></a> Modify categorization information for inventoried software  
 Predefined software in the Asset Intelligence catalog is configured with specific categorization information, such as product name, vendor, software category, and software family. When the predefined categorization information does not meet your requirements, you can modify the information in the properties for the software title. When you modify categorization information for predefined software, the validation state for the software changes from **Validated** to **User Defined**.  

> [!IMPORTANT]  
>  The categorization information can only be modified at the top-level site.  

 Use the following procedure to modify categorization information for inventoried software.  

##### To modify the categorizations for software titles  

1. In the Configuration Manager console, click **Assets and Compliance**.  

2. In the **Assets and Compliance** workspace, click **Asset Intelligence**, and then click **Inventoried Software**.  

3. Select a software title or select multiple software titles for which you want to modify categorizations.  

4. On the **Home** tab, in the **Properties** group, click **Properties**.  

5. On the **General** tab, you can modify the following categorization information:  

   -   **Product Name**: Specifies the name of the inventoried software title.  

   -   **Vendor**: Specifies the name of the vendor that developed the inventoried software title.  

   -   **Category**: Specifies the software category that is currently assigned to the inventoried software title.  

   -   **Family**: Specifies the software family that is currently assigned to the inventoried software title.  

6. Click **OK** to save the changes.  

   Use the following procedure to revert software to the original categorization information.  

### Revert categorization information to original settings for software  
 Configuration Manager stores categorization information obtained from System Center Online in the database. The information cannot be deleted. After the information has been modified, you can revert the categorization information back to the System Center Online categorization. Inventoried software that is not in the Asset Intelligence catalog can also be reverted back to the original settings.  

 Use the following procedure to revert categorization information to the original settings.  

##### To revert categorization information to original settings  

1.  In the Configuration Manager console, click **Assets and Compliance**.  

2.  In the **Assets and Compliance** workspace, click **Asset Intelligence**, and then click **Inventoried Software**.  

3.  Select a software title or select multiple software titles that you want to revert to the original settings. Only software that has a **User Defined** state can be reverted.  

    > [!TIP]  
    >  Click the **State** column to sort by the validation state. Sorting lets you see all software by validation state and quickly select multiple items to revert to the original settings.  

4.  On the **Home** tab, in the **Product** group, click **Revert**.  

5.  Click **Yes** to revert the software to the original categorization information.  

6.  When you revert categorization information for software that is in the Asset Intelligence catalog, the validation state changes from **User Defined** to **Validated**. When you revert software that is not in the catalog, the validation state changes from **User Defined** to **Uncategorized**.  

##  <a name="BKMK_RequestCatalogUpdate"></a> Request a catalog update for uncategorized software titles  
 Uncategorized software title information can be submitted to System Center Online for research and categorization. After an uncategorized software title is submitted, and there are at least 4 categorization requests from customers for the same software title, researchers identify, categorize, and then make the software title categorization information available to all customers that are using the System Center Online service. Microsoft gives the highest priority to software titles that have the most requests for categorization. Custom software and line-of-business applications are unlikely to receive a category, and as a best practice, you should not send these software titles to Microsoft for categorization.  

 When software title information is submitted to System Center Online for categorization, the following conditions apply:  

-   Only basic software title information is transmitted to System Center Online, and software title information to be categorized can be reviewed before submission.  

-   Software license information is never transmitted.  

-   Any software title that is uploaded becomes publicly available as part of the System Center Online catalog and can be downloaded by other customers.  

-   The source of the software title is not stored in the System Center Online catalog. However, application titles containing confidential or proprietary information should not be submitted for categorization by System Center Online.  

> [!NOTE]  
>  For more information about Asset Intelligence privacy information, see [Security and privacy for Asset Intelligence](../../../../core/clients/manage/asset-intelligence/security-and-privacy-for-asset-intelligence.md).  

 Use the following procedure to request Asset Intelligence catalog software title categorization from System Center Online.  

#### To request a catalog update for uncategorized software titles  

1.  In the Configuration Manager console, click **Assets and Compliance**.  

2.  In the **Assets and Compliance** workspace, click **Asset Intelligence**, and then click **Inventoried Software**.  

3.  Select a product name or select multiple product names, to be submitted to System Center Online for categorization. Only uncategorized inventoried software titles can be submitted to System Center Online for categorization. If an inventoried software title has been categorized by an administrator resulting in a user-defined state, you must right-click the inventoried software title, and then click **Revert** to revert the software title to the **Uncategorized** state before it can be submitted to System Center Online for categorization.  

    > [!NOTE]  
    >  Configuration Manager can process up to 2000 software titles for categorization at a time. If you select more than 2000 software titles, only the first 2000 software titles will be processed. You must select the remaining software titles for categorization in batches of less than 2000.  

    > [!TIP]  
    >  Click the **State** column to sort by the validation state. This lets you see all uncategorized product names and quickly select multiple items to submit for categorization.  

4.  On **Home** tab, in the **Product** group, click **Request Catalog Update**.  

5.  Review the System Center Online categorization submission privacy message. Click **Details** to view the information that will be sent to System Center Online.  

6.  Select **I have read and understood this message**, and then click **OK** to allow the selected software titles to be submitted for categorization.  

7.  Verify that the state of the inventoried software product names submitted to System Center Online for categorization has changed from **Uncategorized** to **Pending**.  

    > [!NOTE]  
    >  Software that is submitted to System Center Online for categorization has a validation state of **Pending** on a central administration site is still displayed with a validation state of **Uncategorized** on child primary sites.  

##  <a name="BKMK_ResolveSoftwareDetails"></a> Resolve software details conflicts  
 After newly updated software categorization details have been received from System Center Online that conflict with existing software details information, you can choose how to resolve the conflict. Software that has a current conflict has a validation state of **Updatable**. After a software details conflict has been resolved, the software categorization information is retained in the Asset Intelligence catalog according to the setting that you specify. A software details conflict does not occur for the same software categorization value again unless the System Center Online value changes after the conflict has been resolved.  

 Use the following procedure to resolve a software details conflict.  

#### To resolve a software details conflict  

1. In the Configuration Manager console, click **Assets and Compliance**.  

2. In the **Assets and Compliance** workspace, click **Asset Intelligence**, and then click **Inventoried Software**.  

3. Review the **State** column for software titles in the **Updatable** state.  

4. Select the software title for which you have to resolve a conflict, and then on the **Home** tab, in the **Product** group, and click **Resolve Conflict**.  

5. Review the following information:  

   -   **Local value**: Specifies the existing software categorization information in the Asset Intelligence catalog that conflicts with newer System Center Online software categorization details.  

   -   **Downloaded value**: Specifies the new System Center Online software categorization information for conflicting Asset Intelligence catalog software categorization information.  

6. Select one of the following settings to resolve the software details conflict:  

   - **Do not change the locally edited catalog information value**: Resolves the software details conflict by retaining the existing Asset Intelligence catalog software categorization information. When you select this setting, the software title state changes from **Updatable** to **User Defined**.  

   - **Overwrite the locally edited catalog information value with the downloaded System Center Online value**: Resolves the software details conflict by overwriting the existing Asset Intelligence catalog software categorization information with new information obtained from System Center Online. When you select this setting, the software title state changes from **Updatable** to **Validated**.  

     Click **OK** to save the conflict resolution.  
