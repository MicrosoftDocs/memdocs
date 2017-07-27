---
title: "Create collections | Microsoft Docs"
description: "Create collections in System Center Configuration Manager to more easily manage groups of users and devices."
ms.custom: na
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1401a35e-4312-4d3b-8ceb-0abbb10d4f05
caps.latest.revision: 6
caps.handback.revision: 0
author: andredm7 
ms.author: andredm 
manager: angrobe

---
# How to create collections in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Collections are groupings of users or devices. Use collections for tasks such as application management, deploying compliance settings, or installing software updates. You can also use collections to manage groups of client settings or use them with role-based administration to specify the resources that an administrative user can access. Configuration Manager contains several built-in collections. For more information, see [Introduction to collections in System Center Configuration Manager](../../../../core/clients/manage/collections/introduction-to-collections.md).  

> [!NOTE]  
>  A collection can contain users or devices, but not both.  

 The following table lists the rules that you can use to configure the members of a collection in Configuration Manager.  

|Membership rule type|More information|  
|--------------------------|----------------------|  
|Direct rule|Use to choose the users or computers that you want to add to a collection. This membership does not change unless you remove a resource from Configuration Manager. Configuration Manager must have discovered the resources or you must have imported the resources before you can add them to a direct rule collection. Direct rule collections have a higher administrative overhead than query rule collections because they require manual changes.|  
|Query rule|Dynamically update the membership of a collection based on a query that Configuration Manager runs on a schedule. For example, you can create a collection of users that are a member of the Human Resources organizational unit in Active Directory Domain Services. This collection is automatically updated when new users are added to or removed from the Human Resources organizational unit.<br /><br /> For example queries that you can use to build collections, see [How to create queries in System Center Configuration Manager](../../../../core/servers/manage/create-queries.md).|  
|Include collection rule|Include the members of another collection in a Configuration Manager collection The membership of the current collection is updated on a schedule if the included collection changes.<br /><br /> You can add multiple include collection rules to a collection.<br /> |  
|Exclude collection rule|The exclude collection rule let you exclude the members of another collection from a Configuration Manager collection. The membership of the current collection is updated on a schedule if the excluded collection changes.<br /><br /> You can add multiple exclude collection rules to a collection. If a collection includes both include collection and exclude collection rules and there is a conflict, the exclude collection rule takes priority .<br />              **Example:** You create a collection that has one include collection rule and one exclude collection rule. The include collection rule is for a collection of Dell desktops. The exclude collection is for a collection of computers that have less than 4 GB RAM. The new collection will contain Dell desktops that have at least 4 GB RAM.|  

 Use the following procedures to help you create collections in Configuration Manager. You can also import collections that were created at this or another Configuration Manager site. For information about how to export and import collections, see [How to manage collections in System Center Configuration Manager](../../../../core/clients/manage/collections/manage-collections.md).  

 For information about creating collections for computers that run Linux and UNIX, see [How to manage clients for Linux and UNIX servers in System Center Configuration Manager](../../../../core/clients/manage/manage-clients-for-linux-and-unix-servers.md).  

##  <a name="BKMK_1"></a> To create a device collection  

1.  In the Configuration Manager console, choose **Assets and Compliance** > **Device Collections**.  

3.  On the **Home** tab, in the **Create** group, choose **Create Device Collection**.  

4.  On the **General** page provide a **Name** and a **Comment**. Then, in  **Limiting collection**, choose **Browse** to select a limiting collection. The collection  will only contain members from the limiting collection.  

5.  On the **Membership Rules** page of the **Create Device Collection Wizard**, in the **Add Rule** list, select the type of membership rule that you want to use for this collection. You can configure multiple rules for each collection.  

        
##### To configure a direct rule  

1.  On the **Search for Resources** page of the **Create Direct Membership Rule Wizard**, specify the following information:  

-   **Resource class**: Select the type of resource you want to search for and add to the collection. Select from **System Resource** values to search for inventory data returned from client computers or **Unknown Computer** to select from values returned by unknown computers.  

-   **Attribute name**: Select the attribute associated with the selected resource class that you want to search for. For example, if you want to select computers by their NetBIOS name, select **System Resource** in the **Resource class** list and **NetBIOS name** in the **Attribute name** list.  

-   **Exclude resources marked as obsolete** - If a client computer is marked as obsolete, do not include this value in the search results.  

-   **Exclude resources that do not have the Configuration Manager client installed** - these won't be displayed in the search results.  

-   **Value:** Enter a value for which you want to search the selected attribute name. You can use the percent character **%** as a wildcard. For example, to search for computers that have a NetBIOS name beginning with "M", enter **M%** in this field.  

2.  On the **Select Resources** page, select the resources that you want to add to the collection in the **Resources** list, and then choose **Next**.  


##### To configure a query rule  

1.  In the **Query Rule Properties** dialog box, specify the following information:  

-   **Name**: Specify a unique name.  

-   **Import Query Statement** - Opens the **Browse Query** dialog box where you can select a [Configuration Manager query](../../../../core/servers/manage/create-queries.md) to use as the query rule for the collection.   

-   **Resource class:** Select the type of resource you want to search for and add to the collection. Select a value from **System Resource** values to search for inventory data returned from client computers or **Unknown Computer** to select from values returned by unknown computers.  

-   **Edit Query Statement** - Opens the **Query Statement Properties** dialog box where you can author a query to use as the rule for the collection. For more information about queries, see [Queries technical reference for System Center Configuration Manager](../../../../core/servers/manage/queries-technical-reference.md).  

    
##### To configure an include collection rule  

In the **Select Collections** dialog box, select the collections you want to include in the new collection, then choose **OK**.  

##### To configure an exclude collection rule  

In the **Select Collections** dialog box, select the collections you want to exclude from the new collection, then choose **OK**.  

-   **Use incremental updates for this collection** - Select this option to periodically scan for and update only new or changed resources from the previous collection evaluation, independently of a full collection evaluation. Incremental updates occur at 10 minute intervals.  

> [!IMPORTANT]  
>  Collections configured by using query rules that use the following classes do not support incremental updates:  
>   
> -   SMS_G_System_CollectedFile  
> -   SMS_G_System_LastSoftwareScan  
> -   SMS_G_System_AppClientState  
> -   SMS_G_System_DCMDeploymentState  
> -   SMS_G_System_DCMDeploymentErrorAssetDetails  
> -   SMS_G_System_DCMDeploymentCompliantAssetDetails  
> -   SMS_G_System_DCMDeploymentNonCompliantAssetDetails  
> -   SMS_G_User_DCMDeploymentCompliantAssetDetails (for collections of users only)  
> -   SMS_G_User_DCMDeploymentNonCompliantAssetDetails (for collections of users only)  
> -   SMS_G_System_SoftwareUsageData  
> -   SMS_G_System_CI_ComplianceState  
> -   SMS_G_System_EndpointProtectionStatus  
> -   SMS_GH_System_*  
> -   SMS_GEH_System_*  

-   **Schedule a full update on this collection** - Schedule a regular full evaluation of the collection membership.  

6.  Complete the wizard to create the new collection. The new collection is displayed in the **Device Collections** node of the **Assets and Compliance** workspace.  

> [!NOTE]  
>  You must refresh or reload the Configuration Manager console to see the collection members. However, the members will not appear in the collection until after the first scheduled update, or if you manually select **Update Membership** for the collection. It may take a few minutes for a collection update to complete.  

##  <a name="BKMK_2"></a> To create a user collection  

1.  In the Configuration Manager console, choose **Assets and Compliance** > **User Collections**.  

3.  On the **Home** tab, in the **Create** group, choose **Create User Collection**.  

4.  On the **General** page of the wizardprovide a **Name** and a **Comment**. Then, in  **Limiting collection**, choose **Browse** to select a limiting collection. The collection will only contain members from the limiting collection.  

5.  On the **Membership Rules** page, specify the following:  

    -   In the **Add Rule** list, select the type of membership rule you want to use for this collection. You can configure multiple rules for each collection.  

##### To configure a direct rule  

1.  On the **Search for Resources** page of the **Create Direct Membership Rule Wizard**, specify:  

-   **Resource class**: Select the type of resource you want to search for and add to the collection. Select from **User Resource** values to search for user information collected by Configuration Manager or **User Group Resource** to search for user group information collected by Configuration Manager.  

-   **Attribute name**: Select the attribute associated with the resource class that you want to search for. For example, if you want to select users by their Organizational Unit (OU) name, select **User Resource** in the **Resource class** list and **User OU Name** in the **Attribute name** list.  

-   **Value:** Enter a value that you want to search for. You can use the percent character **%** as a wildcard. For example, to search for users in the Contoso OU, enter **Contoso** in this field.  

2.  On the **Select Resources** page, select the resources that you want to add to the collection in the **Resources** list.  

##### To configure a query rule  

1.  In the **Query Rule Properties** dialog, provide:  

-   **Name**: A unique name.  

-   **Import Query Statement** - Opens the **Browse Query** dialog box where you can select a [Configuration Manager query](../../../../core/servers/manage/queries-technical-reference.md) to use as the query rule for the collection.  

-   **Resource class**: Select the type of resource you want to search for and add to the collection. Select from **User Resource** values to search for user information collected by Configuration Manager or **User Group Resource** to search for user group information collected by Configuration Manager.  

-   **Edit Query Statement** - Opens the **Query Statement Properties** dialog box where you can [author a query](../../../../core/servers/manage/queries-technical-reference.md) to use as the rule for the collection.  

##### To configure an include collection rule  

In the **Select Collections** dialog box, select the collections you want to include in the new collection, then choose **OK**.  

##### To configure an exclude collection rule  

In the **Select Collections** dialog box, select the collections you want to exclude from the new collection, then choose **OK**.  


-   **Use incremental updates for this collection** - Select this option to periodically scan for and update only new or changed resources from the previous collection evaluation, independently of a full collection evaluation. Incremental updates occur at 10 minute intervals.  

> [!IMPORTANT]  
>  Collections configured by using query rules that use the following classes do not support incremental updates:  
>   
> -   SMS_G_System_CollectedFile  
> -   SMS_G_System_LastSoftwareScan  
> -   SMS_G_System_AppClientState  
> -   SMS_G_System_DCMDeploymentState  
> -   SMS_G_System_DCMDeploymentErrorAssetDetails  
> -   SMS_G_System_DCMDeploymentCompliantAssetDetails  
> -   SMS_G_System_DCMDeploymentNonCompliantAssetDetails  
> -   SMS_G_User_DCMDeploymentCompliantAssetDetails (for collections of users only)  
> -   SMS_G_User_DCMDeploymentNonCompliantAssetDetails (for collections of users only)  
> -   SMS_G_System_SoftwareUsageData  
> -   SMS_G_System_CI_ComplianceState  
> -   SMS_G_System_EndpointProtectionStatus  
> -   SMS_GH_System_*  
> -   SMS_GEH_System_*  

-   **Schedule a full update on this collection** -  Schedule a regular full evaluation of the collection membership.  

6.  Complete the wizard. The new collection is displayed in the **User Collections** node of the **Assets and Compliance** workspace.  

> [!NOTE]  
>  You must refresh or reload the Configuration Manager console to see the collection members. However, the members will not appear in the collection until after the first scheduled update, or you manually select **Update Membership** for the collection. It may take a few minutes for a collection update to complete.  

##  <a name="BKMK_3"></a> To import a collection  

1.  In the Configuration Manager console, choose **Assets and Compliance** > **User Collections** or **Device Collections**.  

3.  On the **Home** tab, in the **Create** group, choose **Import Collections**.  

4.  On the **General** page of the **Import Collections Wizard**, choose **Next**.  

5.  On the **MOF File Name** page, choose **Browse** and then browse to the MOF file that contains the collection information you want to import.  

    > [!NOTE]  
    >  The file you want to import must have been exported from a site running the same version of Configuration Manager as this one. For more information about exporting collections, see [How to manage collections in System Center Configuration Manager](../../../../core/clients/manage/collections/manage-collections.md).  

6.  Complete the wizard to import the collection. The new collection is displayed in the **User Collections** or **Device Collections** node of the **Assets and Compliance** workspace. Refresh or reload the Configuration Manager console to see the collection members for the newly imported collection.  
