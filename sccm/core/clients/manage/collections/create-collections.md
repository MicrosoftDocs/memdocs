---
title: Create collections
titleSuffix: Configuration Manager
description: Create collections in Configuration Manager to more easily manage groups of users and devices.
ms.date: 03/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 1401a35e-4312-4d3b-8ceb-0abbb10d4f05
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
---

# How to create collections in Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Collections are groupings of users or devices. Use collections for tasks such as application management, deploying compliance settings, or installing software updates. You can also use collections to manage groups of client settings or use them with role-based administration to specify the resources that an administrative user can access. Configuration Manager contains several built-in collections. For more information, see [Introduction to collections](/sccm/core/clients/manage/collections/introduction-to-collections).  

> [!NOTE]  
> A collection can contain users or devices, but not both.  


Use this article to help you create collections in Configuration Manager. You can also import collections that were created at this or another Configuration Manager site. For more information about how to export and import collections, see [How to manage collections](/sccm/core/clients/manage/collections/manage-collections).  



## Collection rules

There are different rules that you can use to configure the members of a collection in Configuration Manager.  


### Direct rule

Use to choose the users or computers that you want to add to a collection. This membership doesn't change unless you remove a resource from Configuration Manager. Before you can add the resources to a direct rule collection, Configuration Manager must have discovered them or you must have imported them. Direct rule collections have a higher administrative overhead than query rule collections because they require manual changes.


### Query rule

Dynamically update the membership of a collection based on a query that Configuration Manager runs on a schedule. For example, you can create a collection of users that are a member of the Human Resources organizational unit in Active Directory Domain Services. This collection is automatically updated when new users are added to or removed from the Human Resources organizational unit.

For example queries that you can use to build collections, see [How to create queries](/sccm/core/servers/manage/create-queries).


### Device category rule

You can make management of your devices easier by associating device categories with the device collections. 

For more information, see [Automatically categorize devices into collections](/sccm/core/clients/manage/collections/automatically-categorize-devices-into-collections).<!-- SCCMDocs issue 552 -->


### Include collection rule

Include the members of another collection in a Configuration Manager collection. If the included collection changes, Configuration Manager updates the membership of the current collection on a schedule.

You can add multiple include collection rules to a collection.


### Exclude collection rule

The exclude collection rule let you exclude the members of another collection from a Configuration Manager collection. If the excluded collection changes, Configuration Manager updates the membership of the current collection on a schedule.

You can add multiple exclude collection rules to a collection. If a collection includes both include collection and exclude collection rules and there's a conflict, the exclude collection rule takes priority.

#### Example
You create a collection that has one include collection rule and one exclude collection rule. The include collection rule is for a collection of Dell desktops. The exclude collection is for a collection of computers that have less than 4-GB RAM. The new collection contains Dell desktops that have at least 4-GB RAM.



## <a name="bkmk_create"></a> Create a collection  

1. In the Configuration Manager console, go to the **Assets and Compliance** workspace.  

    - To create a *device collection*, select the **Device Collections** node. Then on the **Home** tab of the ribbon, in the **Create** group, choose **Create Device Collection**.  

    - To create a *user collection*, select the **User Collections** node. Then on the **Home** tab of the ribbon, in the **Create** group, choose **Create User Collection**.  

2. On the **General** page of the wizard, provide a **Name** and a **Comment**. In the **Limiting collection** section, choose **Browse**, and select a limiting collection. The collection you're creating will only contain members from the limiting collection.  

4. On the **Membership Rules** page, in the **Add Rule** list, select the type of membership rule that you want to use for this collection. You can configure multiple rules for each collection. The configuration for each rule varies. For more information on configuring each rule, see the following sections:  
    - [Direct rule](#bkmk-direct)
    - [Query rule](#bkmk-query)
    - [Device category rule](#bkmk-category)
    - [Include collection rule](#bkmk-include)
    - [Exclude collection rule](#bkmk-exclude)

5. Also on the **Membership Rules** page, review the following settings:

    - **Use incremental updates for this collection**: Select this option to periodically scan for and update only new or changed resources from the previous collection evaluation. This process is independent of a full collection evaluation. By default, incremental updates occur at 5-minute intervals.  

        > [!IMPORTANT]  
        >  Collections with query rules that use the following classes don't support incremental updates:  
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

    - **Schedule a full update on this collection**: Schedule a regular full evaluation of the collection membership.  

        Starting in version 1810, the following changes in collection evaluation behavior can improve site performance:<!--3607726-->  

        - Previously, when you configured a schedule on a query-based collection, the site would continue to evaluate the query whether or not you enabled the collection setting to **Schedule a full update on this collection**. To fully disable the schedule, you had to change the schedule to **None**. 

            Now the site clears the schedule when you disable this setting. To specify a schedule for collection evaluation, enable the option to **Schedule a full update on this collection**.  

            When you update your site, for any existing collection on which you specified a schedule, the site enables the option to **Schedule a full update on this collection**. While this configuration may not be your intent, it was the actual behavior. To stop the site evaluating a collection on a schedule, disable this option.  

        - You can't disable the evaluation of built-in collections like **All Systems**, but now you can configure the schedule. This behavior allows you to customize this action at a time that meets your requirements. 

            > [!Tip]  
            > Only change the **Time** of the custom schedule on built-in collections. Don't change the **Recurrence pattern**. Future iterations may enforce a specific recurrence pattern.  

6. Complete the wizard to create the new collection. The new collection is displayed in the **Device Collections** node of the **Assets and Compliance** workspace.  

> [!NOTE]  
> You must refresh or reload the Configuration Manager console to see the collection members. They don't appear in the collection until after the first scheduled update. You can also manually select **Update Membership** for the collection. It may take a few minutes for a collection update to complete.  

        
### <a name="bkmk-direct"></a> Configure a direct rule  

1. On the **Search for Resources** page of the **Create Direct Membership Rule Wizard**, specify the following information:  

    - **Resource class**: Select the type of resource you want to search for and add to the collection. For example, 
        - **System Resource**: Search for inventory data returned from client computers
        - **Unknown Computer**: Select from values returned by unknown computers
        - **User Resource**: Search for user information collected by Configuration Manager
        - **User Group Resource**: Search for user group information collected by Configuration Manager

    - **Attribute name**: Select the attribute associated with the selected resource class that you want to search for. For example,  

        - If you want to select computers by their NetBIOS name, select **System Resource** in the **Resource class** list and **NetBIOS name** in the **Attribute name** list.  

        - If you want to select users by their Organizational Unit (OU) name, select **User Resource** in the **Resource class** list and **User OU Name** in the **Attribute name** list.  

    - **Exclude resources marked as obsolete**: If a client computer is marked as obsolete, don't include this value in the search results.  

    - **Exclude resources that do not have the Configuration Manager client installed**: These resources won't be displayed in the search results.  

    - **Value**: Enter a value to search the selected attribute name. Use the percent character `%` as a wildcard. For example,  
        - To search for computers that have a NetBIOS name beginning with "M", enter `M%` in this field.  
        - To search for users in the Contoso OU, enter `Contoso` in this field.

2. On the **Select Resources** page, select the resources that you want to add to the collection in the **Resources** list, and then choose **Next**.  


### <a name="bkmk-query"></a> Configure a query rule  

In the **Query Rule Properties** dialog box, specify the following information:  

- **Name**: Specify a unique name for the query.  

- **Import Query Statement**: Opens the **Browse Query** dialog box. Select a [Configuration Manager query](/sccm/core/servers/manage/create-queries) to use as the query rule for the collection.   

- **Resource class**: Select the type of resource you want to search for and add to the collection. Select a value from **System Resource** values to search for inventory data returned from client computers or **Unknown Computer** to select from values returned by unknown computers.  

- **Edit Query Statement**: Opens the **Query Statement Properties** dialog box where you can author a query to use as the rule for the collection. For more information about queries, see [Introduction to queries](/sccm/core/servers/manage/introduction-to-queries).  


### <a name="bkmk-category"></a> Device category rule

The following actions are available in the **Select Device Categories** window:

- **Create**: Specify a name to create a new category
- **Rename**: Rename the selected category
- **Delete**: Select one or more categories, and use this action to remove them from the list

For more information, see [Automatically categorize devices into collections](/sccm/core/clients/manage/collections/automatically-categorize-devices-into-collections).<!-- SCCMDocs issue 552 -->


### <a name="bkmk-include"></a> Configure an include collection rule  

In the **Select Collections** dialog box, select the collections you want to include in the new collection, then choose **OK**.  


### <a name="bkmk-exclude"></a> Configure an exclude collection rule  

In the **Select Collections** dialog box, select the collections you want to exclude from the new collection, then choose **OK**.  



## <a name="bkmk_import"></a> Import a collection  

When you export a collection from a site, Configuration Manager saves it as a managed object format (MOF) file. Use this procedure to import that file into your site database. You need **Create** permissions on the collections class. 

> [!Important]  
> - Make sure the file only contains collection data, is from a trusted source, and hasn't been tampered with.  
> 
> - Make sure the file was exported from a site running the same version of Configuration Manager.  

For more information about exporting collections, see [How to manage collections](/sccm/core/clients/manage/collections/manage-collections).


1. In the Configuration Manager console, go to the **Assets and Compliance** workspace. Select either the **User Collections** or **Device Collections** node.  

2. On the **Home** tab of the ribbon, in the **Create** group, choose **Import Collections**.  

3. On the **General** page of the **Import Collections Wizard**, choose **Next**.  

4. On the **MOF File Name** page, choose **Browse**. Browse to the MOF file that contains the collection information you want to import.  

5. Complete the wizard to import the collection. The new collection is displayed in the **User Collections** or **Device Collections** node of the **Assets and Compliance** workspace. Refresh or reload the Configuration Manager console to see the collection members for the newly imported collection.  

## <a name="bkmk_powershell"></a> Using PowerShell

PowerShell can be used to create and import collections.  For more information, see:

* [New-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmcollection)
* [Set-CMCollection](https://docs.microsoft.com/powershell/module/ConfigurationManager/Set-CMCollection)
* [Import-CMCollection](https://docs.microsoft.com/powershell/module/ConfigurationManager/Import-CMCollection)
