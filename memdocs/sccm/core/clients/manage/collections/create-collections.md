---
title: Create collections
titleSuffix: Configuration Manager
description: Create collections in Configuration Manager to more easily manage groups of users and devices.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 1401a35e-4312-4d3b-8ceb-0abbb10d4f05
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# How to create collections in Configuration Manager

*Applies to: Configuration Manager (current branch)*

Collections are groupings of users or devices. Use collections for tasks like managing applications, deploying compliance settings, or installing software updates. You can also use collections to manage groups of client settings or use them with role-based administration to specify the resources that an administrative user can access. Configuration Manager contains several built-in collections. For more information, see [Introduction to collections](/sccm/core/clients/manage/collections/introduction-to-collections).  

> [!NOTE]  
> A collection can contain users or devices, but not both.  


The information in this article can help you create collections in Configuration Manager. You can also import collections that were created at the current  Configuration Manager site or at another one. For more information about how to export and import collections, see [How to manage collections](/sccm/core/clients/manage/collections/manage-collections).  


## Collection rules

There are different types of rules that you can use to configure the members of a collection in Configuration Manager.  


### Direct rule

Use direct rules to choose the users or computers that you want to add to a collection. The membership doesn't change unless you remove a resource from Configuration Manager. Before you can add the resources to a direct rule collection, Configuration Manager must have discovered them or you must have imported them. Direct rule collections have more administrative overhead than query rule collections because they require manual changes.


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

Exclude collection rules let you exclude the members of one collection from another Configuration Manager collection. If the excluded collection changes, Configuration Manager updates the membership of the current collection on a schedule.

You can add multiple exclude collection rules to a collection. If a collection includes both include collection and exclude collection rules and there's a conflict, the exclude collection rule takes priority.

#### Example
You create a collection that has one include collection rule and one exclude collection rule. The include collection rule is for a collection of Dell desktops. The exclude collection is for a collection of computers that have less than 4 GB of RAM. The new collection contains Dell desktops that have at least 4 GB of RAM.



## <a name="bkmk_create"></a> Create a collection  

1. In the Configuration Manager console, go to the **Assets and Compliance** workspace.  

    - To create a *device collection*, select the **Device Collections** node. Then, on the **Home** tab of the ribbon, in the **Create** group, select **Create Device Collection**.  

    - To create a *user collection*, select the **User Collections** node. Then, on the **Home** tab of the ribbon, in the **Create** group, select **Create User Collection**.  

2. On the **General** page of the wizard, provide a **Name** and a **Comment**. In the **Limiting collection** section, select **Browse**, and then select a limiting collection. The collection you're creating will contain only members from the limiting collection.  

4. On the **Membership Rules** page, in the **Add Rule** list, select the type of membership rule that you want to use for the collection. You can configure multiple rules for each collection. The configuration for each rule varies. For more information on configuring each rule, see the following sections of this article:  
    - [Direct rule](#bkmk-direct)
    - [Query rule](#bkmk-query)
    - [Device category rule](#bkmk-category)
    - [Include collection rule](#bkmk-include)
    - [Exclude collection rule](#bkmk-exclude)

5. Also on the **Membership Rules** page, review the following settings.

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

        Starting in version 1810, these changes in collection evaluation behavior can improve site performance:<!--3607726-->  

        - Previously, when you configured a schedule on a query-based collection, the site would continue to evaluate the query whether or not you enabled the collection setting to **Schedule a full update on this collection**. To fully disable the schedule, you had to change the schedule to **None**.

            Now the site clears the schedule when you disable this setting. To specify a schedule for collection evaluation, enable the option to **Schedule a full update on this collection**.  

            When you update your site, for any existing collection on which you specified a schedule, the site enables the option to **Schedule a full update on this collection**. While this configuration might not be your intent, it was the actual behavior of the schedule before you updated the site. To stop the site evaluating a collection on a schedule, disable this option.  

        - You can't disable the evaluation of built-in collections like **All Systems**, but now you can configure the schedule. This behavior allows you to customize this action at a time that meets your requirements. 

            > [!TIP]  
            > On built-in collections, only change the **Time** of the custom schedule. Don't change the **Recurrence pattern**. Future iterations might enforce a specific recurrence pattern.  

6. Complete the wizard to create the new collection. The new collection is displayed in the **Device Collections** node of the **Assets and Compliance** workspace.  

> [!NOTE]  
> You must refresh or reload the Configuration Manager console to see the collection members. They don't appear in the collection until after the first scheduled update. You can also manually select **Update Membership** for the collection. It might take a few minutes for a collection update to complete.  

        
### <a name="bkmk-direct"></a> Configure a direct rule  

1. On the **Search for Resources** page of the **Create Direct Membership Rule Wizard**, specify the following information.  

    - **Resource class**: Select the type of resource you want to search for and add to the collection. For example:
        - **System Resource**: Search for inventory data returned from client computers.
        - **Unknown Computer**: Select from values returned by unknown computers.
        - **User Resource**: Search for user information collected by Configuration Manager.
        - **User Group Resource**: Search for user group information collected by Configuration Manager.

    - **Attribute name**: Select the attribute associated with the selected resource class that you want to search for. For example:  

        - If you want to select computers by their NetBIOS name, select **System Resource** in the **Resource class** list and **NetBIOS name** in the **Attribute name** list.  

        - If you want to select users by their organizational unit (OU) name, select **User Resource** in the **Resource class** list and **User OU Name** in the **Attribute name** list.  

    - **Exclude resources marked as obsolete**: If a client computer is marked as obsolete, don't include this value in the search results.  

    - **Exclude resources that do not have the Configuration Manager client installed**: These resources won't be displayed in the search results.  

    - **Value**: Enter a value to search the selected attribute name. Use the percent character (%) as a wildcard. For example:  
        - To search for computers that have a NetBIOS name beginning with "M", enter **M%** in this field.  
        - To search for users in the Contoso OU, enter **Contoso** in this field.

2. On the **Select Resources** page, select the resources that you want to add to the collection in the **Resources** list, and then select **Next**.  


### <a name="bkmk-query"></a> Configure a query rule  

In the **Query Rule Properties** dialog box, specify the following information.  

- **Name**: Specify a unique name for the query.  

- **Import Query Statement**: Opens the **Browse Query** dialog box. Select a [Configuration Manager query](/sccm/core/servers/manage/create-queries) to use as the query rule for the collection.   

- **Resource class**: Select the type of resource you want to search for and add to the collection. Select a value from **System Resource** to search for inventory data returned from client computers or from **Unknown Computer** to select from values returned by unknown computers.  

- **Edit Query Statement**: Opens the **Query Statement Properties** dialog box, where you can write a query to use as the rule for the collection. For more information about queries, see [Introduction to queries](/sccm/core/servers/manage/introduction-to-queries).  

        
        > [!TIP]  
        > On the General tab, selecting the checkbox to **Omit duplicate rows (select distinct)** may result in less rows returned and potentially quicker results. 

### <a name="bkmk-category"></a> Device category rule

The following actions are available in the **Select Device Categories** window.

- **Create**: Specify a name to create a new category.
- **Rename**: Rename the selected category.
- **Delete**: Select one or more categories, and use this action to remove them from the list.

For more information, see [Automatically categorize devices into collections](/sccm/core/clients/manage/collections/automatically-categorize-devices-into-collections).<!-- SCCMDocs issue 552 -->


### <a name="bkmk-include"></a> Configure an include collection rule  

In the **Select Collections** dialog box, select the collections you want to include in the new collection, and then select **OK**.  


### <a name="bkmk-exclude"></a> Configure an exclude collection rule  

In the **Select Collections** dialog box, select the collections you want to exclude from the new collection, and then select **OK**.  



## <a name="bkmk_import"></a> Import a collection  

When you export a collection from a site, Configuration Manager saves it as a Managed Object Format (MOF) file. Use this procedure to import that file into your site database. To complete this procedure, you need **Create** permissions on the collections class.

> [!IMPORTANT]  
> - Make sure the file contains only collection data, is from a trusted source, and hasn't been tampered with.  
> 
> - Make sure the file was exported from a site running the same version of Configuration Manager that you're using.  

For more information about exporting collections, see [How to manage collections](/sccm/core/clients/manage/collections/manage-collections).


1. In the Configuration Manager console, go to the **Assets and Compliance** workspace. Select either the **User Collections** or the **Device Collections** node.  

2. On the **Home** tab of the ribbon, in the **Create** group, select **Import Collections**.  

3. On the **General** page of the **Import Collections Wizard**, select **Next**.  

4. On the **MOF File Name** page, select **Browse**. Browse to the MOF file that contains the collection information you want to import.  

5. Complete the wizard to import the collection. The new collection is displayed in the **User Collections** or **Device Collections** node of the **Assets and Compliance** workspace. Refresh or reload the Configuration Manager console to see the collection members for the newly imported collection.  

## <a name="bkmk_aadcollsync"></a> Synchronize collection membership results to Azure Active Directory groups

<!--3607475-->
> [!Tip]  
> This feature was first introduced in version 1906 as a [pre-release feature](/sccm/core/servers/manage/pre-release-features). Beginning with version 2002, it's no longer a pre-release feature.  

You can enable the synchronization of collection memberships to an Azure Active Directory (Azure AD) group. This synchronization allows you to use your existing on premises grouping rules in the cloud by creating Azure AD group memberships based on collection membership results. You can synchronize device collections. Only devices with an Azure Active Directory record are reflected in the Azure AD Group. Both Hybrid Azure AD Joined and Azure Active Director joined devices are supported.

The Azure AD synchronization happens every five minutes. It's a one-way process, from Configuration Manager to Azure AD. Changes made in Azure AD aren't reflected in Configuration Manager collections, but aren't overwritten by Configuration Manager. For example, if the Configuration Manager collection has two devices, and the Azure AD group has three different devices, after synchronization the Azure AD group has five devices.


### Prerequisites

- [Cloud Management](/sccm/core/servers/deploy/configure/azure-services-wizard)
- [Azure Active Directory user discovery](/sccm/core/servers/deploy/configure/about-discovery-methods#azureaddisc)

### Create a group and set the owner in Azure AD

1. Go to [https://portal.azure.com](https://portal.azure.com).
1. Navigate to **Azure Active Directory** > **Groups** > **All groups**.
1. Click **New group** and type in a **Group name** and optionally **Group description**.
1. Make sure that **Membership type** is **Assigned**.
1. Select **Owners**, then add the identity that will create the synchronization relationship in Configuration Manager.
1. Click **Create** to finish creating the Azure AD group.

### Enable collection synchronization for the Azure service

1. In the Configuration Manager console, go to **Administration** > **Overview** > **Cloud Services** > **Azure Services**.
1. Right-click on the Azure AD tenant where you created the group and select **Properties**.
1. In the **Collection Synchronization** tab, check the box for the **Enable Azure Directory Group Sync**.
1. Click **OK** to save the setting.

### Enable the collection to synchronize

1. In the Configuration Manager console, go to **Assets and Compliance** > **Overview** > **Device Collections**.
1. Right-click on the collection to sync, then click **Properties**. 
1. In the **AAD Group Sync** tab, click **Add**.
1. From the drop-down menu, select the **Tenant** where you created your Azure AD group.
1. Type in your search criteria in the **Name starts with** field, then click **Search**.
  - If you are prompted to sign in, use the identity you specified as the owner for the Azure AD group.
1. Select the target group, then click **OK** to add the group and **OK** again to exit the collection's properties.
1. You'll need to wait about 5 to 7 minutes before you can verify the group memberships in the Azure portal.
   - To initiate a full synchronization, right-click the collection then select **Synchronize Membership**.


### Verify the Azure AD group membership

1. Go to [https://portal.azure.com](https://portal.azure.com).
1. Navigate to **Azure Active Directory** > **Groups** > **All groups**.
1. Find the group you created and select **Members**. 
1. Confirm that the members reflect those in the Configuration Manager collection.
   - Only devices with Azure AD identity will show in the group.


![Synchronize collections to Azure AD](media/3607475-sync-collection-to-azuread.png)

## <a name="bkmk_powershell"></a> Using PowerShell

You can use PowerShell to create and import collections. For more information, see:

* [New-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmcollection)
* [Set-CMCollection](https://docs.microsoft.com/powershell/module/ConfigurationManager/Set-CMCollection)
* [Import-CMCollection](https://docs.microsoft.com/powershell/module/ConfigurationManager/Import-CMCollection)

## Next steps

[Manage collections](/sccm/core/clients/manage/collections/manage-collections)
