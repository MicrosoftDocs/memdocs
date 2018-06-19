---
title: New version 1806
titleSuffix: Configuration Manager
description: Get details about changes and new capabilities introduced in version 1806 of Configuration Manager.
ms.date: 07/13/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 0249dbd3-1e85-4d05-a9e5-420fbe44d850
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# What's new in version 1806 of System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Update 1806 for Configuration Manager current branch is available as an in-console update. Apply this update on sites that run version 1706, 1710, or 1802. <!-- baseline only statement: When installing a new site, it's also available as a baseline version.-->

<!--
Aside from new features, this release also includes additional changes such as bug fixes. For more information, see [Summary of changes in System Center Configuration Manager current branch, version 1806](https://support.microsoft.com/help/4101375).
-->

<!--
The following additional updates to this release are also now available:
- [Update rollup for System Center Configuration Manager current branch, version 1806](https://support.microsoft.com/help/4057517)
-->


> [!TIP]  
> To install a new site, you must use a baseline version of Configuration Manager.  
>
>  Learn more about:    
>   - [Installing new sites](/sccm/core/servers/deploy/install/installing-sites)  
>   - [Installing updates at sites](/sccm/core/servers/manage/updates)  
>   - [Baseline and update versions](/sccm/core/servers/manage/updates#a-namebkmkbaselinesa-baseline-and-update-versions)  

The following sections provide details about the changes and new capabilities in version 1806 of Configuration Manager.  



<!--
## Deprecated features and operating systems
Learn about support changes before they are implemented in [removed and deprecated items](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated).

Version 1806 drops support for the following products:
-->



## Site infrastructure

At least one subsection here about high available site server.



<!-- ## Migration  -->



<!-- ## Client management -->



<!--## Co-management-->



## Compliance settings

### Configure Windows Defender SmartScreen settings for Microsoft Edge
<!--1353701-->
The [Microsoft Edge browser compliance settings policy](/sccm/compliance/deploy-use/browser-profiles) adds the following three settings for Windows Defender SmartScreen: 
- Allow SmartScreen
- Users can override SmartScreen prompt for sites
- Users can override SmartScreen prompt for files



<!--## Application Management-->



<!--## Operating system deployment-->





<!--## Software Center-->



<!--## Software updates -->




<!--## Reporting-->




<!-- ## Inventory  -->



<!-- ## Mobile device management -->



<!-- ## Protect devices-->




## Configuration Manager console

### Product lifecycle dashboard
<!--1319632-->
The new [product lifecycle dashboard](/sccm/core/clients/manage/asset-intelligence/product-lifecycle-dashboard) shows the state of the Microsoft Lifecycle Policy for Microsoft products installed on devices managed with Configuration Manager. It also provides you with information about Microsoft products in your environment, supportability state, and support end dates. Use the dashboard to understand the availability of support for each product. This information helps you plan for when to update the Microsoft products you use before their current end of support is reached.   

To access the product lifecycle dashboard, in the Configuration Manager console go to the **Assets and Compliance** workspace, expand **Asset Intelligence**, and select the **Product Lifecycle** node.




## Next Steps
When you're ready to install this version, see [Updates for Configuration Manager](/sccm/core/servers/manage/updates).
