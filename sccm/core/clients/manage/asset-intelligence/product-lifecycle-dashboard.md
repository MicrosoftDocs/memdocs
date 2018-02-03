---
title: "Product Lifecycle dashboard"
titleSuffix: "Configuration Manager"
description: "Get information about the Product Lifecycle dashboard in System Center Configuration Manager."
ms.custom: na
ms.date: 2/09/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 8b5b144a-0e5f-4fcc-87b2-33b9bcdb5655
caps.latest.revision: 1
caps.handback.revision: 0
author: mestew
ms.author: mstewart
manager: angrobe

---
# Manage Microsoft Lifecycle Policy using System Center Configuration Manager

*Applies to: System Center Configuration Manager (Technical Preview)*

Beginning with Technical Preview version 1802, you can use the Configuration Manager Product Lifecycle dashboard. The dashboard shows the state of the Microsoft Product Lifecycle policy for Microsoft products installed on devices managed with Configuration Manager. The dashboard provides you with information about Microsoft products in your environment, supportability state, and support end dates. 
 You can use the dashboard to understand the availability of support for each product. Helping you plan for when to update the Microsoft products you use before their current end of support is reached.  

For more information about the Microsoft Product Lifecycle Policy, see [Microsoft Lifecycle Policy](https://support.microsoft.com/en-us/lifecycle).

## Prerequisites 

 To see data in the Product Lifecycle dashboard, the following are required: 
- Internet Explorer 9 or later must be installed on the computer running the Configuration Manager console. 
- The Asset Intelligence synchronization point must be configured and synchronized. For more information, see [Configure Asset Intelligence in System Center Configuration Manager](/sccm/core/clients/manage/asset-intelligence/configuring-asset-intelligence).

The data in the dashboard depends on having the Asset Intelligence synchronization point installed. The dashboard uses the Asset Intelligence catalog as metadata for product titles. The metadata is compared against inventory data in your hierarchy. 

## Use the Microsoft Product Lifecycle dashboard

Based on inventory data you collected from managed devices, the dashboard displays information about all current products. However, the information displayed for operating systems and SQL Server is limited to the following versions:

- Windows Server 2008 and later
- Windows XP and later
- SQL Server 2008 and later

To access the Lifecycle dashboard in the Configuration Manager console, go to **Assets and Compliance** > **Asset Intelligence** > **Product Lifecycle**.

[!NOTE]
The data in the dashboard is based on the site the Configuration Manager console connects to. If the console connects to your top-tier site, you see data for the entire hierarchy. When connected to a child primary site, only data from that site displays.

### Product Lifecycle dashboard

![Product Lifecycle dashboard](/sccm/core/clients/manage/asset-intelligence/media/product-lifecycle-dashboard.png)

The dashboard has the following tiles: 
- **Top five products past end-of-life:** This tile is a consolidated data view of products past their end-of-life found in your environment. The graph shows installed software that is expired when compared against the support lifecycle for operating systems and SQL server products.  
- **Top five products nearing end-of-life:** This tile is a consolidated data view of products that are nearing end-of-life in next six months found in your environment. The graph shows installed software that is within six months of end-of-life when compared against the support lifecycle for operating systems and SQL server products.
- **Lifecycle data for installed products:** This tile gives you a general idea of when a product transitions from supported to the expired state. The chart provides a breakdown of the number of clients where the product is installed, the support availability state, along with a link to learn more about the next steps to take. The following information is included in the chart:     
    - Support time remaining
    - Number in environment 
    - Mainstream support end date
    - Extended support end date
    - Next steps 

>[!IMPORTANT]
>The information shown in this dashboard is provided for your convenience and only for use internally within your company. You should not solely rely on this information to confirm compliance. Be sure to verify the accuracy of the information provided to you, along with availability of support information by visiting https://support.microsoft.com/en-us/lifecycle.

## Reporting
The following new reports are added under the category **Product Lifecycle**:
- **General Product Lifecycle overview:** View a list of Product Lifecycles. The list can be filtered by product name and days to expiration definable by the user. 
- **Computers with a specific software product:** View a list of computers on which a specified product is detected.
- **List of expired products found in the organization:** View details for products in your environment that have expired lifecycle dates. 
- **List of machines with expired products in the organization:** View computers that have expired products on them. You can filter this report by product name.

### Next steps
For information about installing or updating the technical preview branch, see [Technical Preview for System Center Configuration Manager](/sccm/core/get-started/technical-preview).  

