---
title: Publish site data
titleSuffix: Configuration Manager
description: Learn how to publish Configuration Manager sites to Active Directory Domain Services.
ms.date: 02/7/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
author: sheetg09
ms.author: sheetg
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# Publish site data for Configuration Manager

*Applies to: Configuration Manager (current branch)*

After you extend the Active Directory schema for Configuration Manager, you can publish Configuration Manager sites to Active Directory Domain Services (AD DS). This lets Active Directory computers securely retrieve site information from a trusted source. Although publishing site information to AD DS is not required for basic Configuration Manager functionality, it can reduce administrative overhead to do so.  

-   **When a site is configured to publish to AD DS**, Configuration Manager clients can automatically find management points through Active Directory publishing. They use an LDAP query to a global catalog server.  

-   **When a site does not publish to AD DS**, clients must have an alternative mechanism to locate their default management point.  

For information about how clients find a management point, see [Understand how clients find site resources and services for Configuration Manager](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  

## Configure sites to publish to AD DS  
 The following are the high-level steps:  

-   You must [extend the Active Directory schema for Configuration Manager](../../../../core/plan-design/network/extend-the-active-directory-schema.md) in each forest where you will publish site data. Also ensure the **System Management** container is present.  

-   You must grant the computer account of each primary site that will publish data   **full control** to the **System Management** container, and all of its child objects.  

### To enable a Configuration Manager site to publish site information to Active Directory forest

1.  In the Configuration Manager console, click **Administration**.  

2.  In the **Administration** workspace, expand **Site Configuration**, and click **Sites**. Select the site that you want to have publish its site data. Then on the **Home** tab, in the **Properties** group, click **Properties**.  

3.  On the **Publishing** tab of the site's properties, select the forests to which this site will publish site data.  

4.  Click **OK** to save the configuration.  

### To set up Active Directory forests for publishing  

1.  In the Configuration Manager console, click **Administration**.  

2.  In the **Administration** workspace, expand **Hierarchy Configuration**, and click **Active Directory Forests**. If Active Directory Forest Discovery has previously run, you see each discovered forest in the results pane. The local forest and any trusted forests are discovered when Active Directory Forest Discovery runs. Only untrusted forests must be manually added.  

    -   To set up a previously discovered forest, select the forest in the results pane. Then on the **Home** tab, in the **Properties** group, click **Properties** to open the forest properties. Continue with step 3.  

    -   To set up a new forest that is not listed, on the **Home** tab, in the **Create** group, click **Add Forest** to open the **Add Forests** dialog box. Continue with step 3.  

3.  On the **General** tab, complete configurations for the forest that you want to discover, and specify the **Active Directory Forest Account**.  

    > [!NOTE]  
    >  Active Directory Forest Discovery requires a global account to discover and publish to untrusted forests. If you do not use the computer account of the site server, you can only select a global account.  

4.  If you plan to allow sites to publish site data to this forest, on the **Publishing** tab, complete configurations for publishing to this forest.  

    > [!NOTE]  
    >  If you enable sites to publish to a forest, you must extend the Active Directory schema of that forest for Configuration Manager. The Active Directory Forest Account must have Full Control permissions to the System container in that forest.  

5.  When you complete the configuration of this forest for use with Active Directory Forest Discovery, click **OK** to save the configuration.  
