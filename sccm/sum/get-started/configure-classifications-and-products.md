---

title: Configure classifications and products to synchronize | Microsoft Docs
description: "Follow these steps to configure classifications and products to synchronize in the Configuration Manager console."
keywords:
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 10/06/2016
ms.topic: article
ms.prod: configuration-manager
ms.service:
ms.technology:
 - configmgr-sum
ms.assetid: 5ddde4e6-d553-4182-b752-6bc8b4a26745


---
#  Configure classifications and products to synchronize  

*Applies to: System Center Configuration Manager (Current Branch)*


> [!NOTE]  
>  Use the procedure from this section only on the top-level site.  

 Software updates metadata is retrieved during the synchronization process in Configuration Manager based on the settings that you specify in the Software Update Point component properties. After you synchronize software updates for the first time, or when new products and classifications are released, you must go to the properties to select the new items. Use the following procedure to configure classifications and products to synchronize.  

#### To configure classifications and products to synchronize  

1.  In the **Configuration Manager** console, navigate to **Administration** > **Site Configuration** > **Sites**.

2. Select the central administration site or the stand-alone primary site.  

3.  On the **Home** tab, in the **Settings** group, click **Configure Site Components**, and then click **Software Update Point**.

4.  On the **Classifications** tab, specify the software update classifications for which you want to synchronize software updates.  

    > [!NOTE]  
    >  Every software update is defined with an update classification that helps to organize the different types of updates. During the synchronization process, the software updates metadata for the specified classifications are synchronized. Configuration Manager provides the ability to synchronize software updates with the following update classifications:  
    >   
    > - **Critical Updates**: Specifies a broadly released update for a specific problem that addresses a critical, non-security-related bug.  
    > - **Definition Updates**: Specifies an update to virus or other definition files.  
    > - **Feature Packs**: Specifies new product features that are distributed outside of a product release and that are typically included in the next full product release.  
    > - **Security Updates**: Specifies a broadly released update for a product-specific, security-related issue.  
    > - **Service Packs**: Specifies a cumulative set of hotfixes that are applied to an application. These hotfixes can include: security updates, critical updates, software updates, and so on.  
    > - **Tools**: Specifies a utility or feature that helps to complete one or more tasks.  
    > - **Update Rollups**: Specifies a cumulative set of hotfixes that are packaged together for easy deployment. These hotfixes can include security updates, critical updates, updates, and so on. An update rollup generally addresses a specific area, such as security or a product component.  
    > - **Updates**: Specifies an update to an application or file that is currently installed.  
    > - **Upgrade**: Specifies an  upgrade for Windows 10 features and functionality. Your software update points and sites must run a minimum of WSUS 4.0 with the [hotfix 3095113](https://support.microsoft.com/kb/3095113) to get the **Upgrade** classification.    
    >       
    > Beginning in Configuration Manager version 1706, you can also select the **Include Microsoft Surface drivers and firmware updates** checkbox to synchronize Microsoft Surface drivers. All software update points must run Windows Server 2016 to successfully synchronize Surface drivers.    
    > [!IMPORTANT]    
    > This is a pre-release feature available in Configuration Manager version 1706. Pre-release features are included in the product for early testing in a production environment, but should not be considered production ready. You must turn on this feature for it to be available. For more information, see [Use pre-release features from updates](https://docs.microsoft.com/sccm/core/servers/manage/install-in-console-updates#bkmk_prerelease).

5.  On the **Products** tab, specify the products for which you want to synchronize software updates, and then click **Close**.  

    > [!NOTE]  
    >  The metadata for each software update defines the products for which the update is applicable. A product is a specific edition of an operating system or application, such as Windows Server 2012. A product family is the base operating system or application from which the individual products are derived. An example of a product family is Windows, of which Windows Server 2012 is a member. You can specify a product family or individual products within a product family. The more products that you select, the longer it will take to synchronize software updates.  
    >   
    >  When software updates are applicable to multiple products, and at least one of the products was selected for synchronization, all of the products will appear in the Configuration Manager console even if some products were not selected. For example, if Windows Server 2012 is the only operating system that you selected, and if a software update applies to Windows 8 and Windows Server 2012, both products will be displayed in the Configuration Manager console.  

    > [!IMPORTANT]  
    >  Configuration Manager stores a list of products and product families from which you can choose when you first install the software update point. Products and product families that are released after Configuration Manager is released might not be available to select until you complete software updates synchronization, which updates the list of available products and product families from which you can choose.  

## Next steps
Start software updates synchronization to retrieve software updates based on the new criteria. For details, see [Synchronize software updates](synchronize-software-updates.md).
