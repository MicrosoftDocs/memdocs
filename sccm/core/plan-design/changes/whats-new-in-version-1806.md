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

### CMPivot
<!--1358456-->
Configuration Manager has always provided a large centralized store of device data, which customers use for reporting purposes. However, that data is only as good as the last time it was collected from clients. CMPivot is a new in-console utility that provides access to real-time state of devices in your environment. It immediately runs a query on all currently connected devices in the target collection and returns the results. You can then filter and group this data in the tool. By providing real-time data from online clients, you can more quickly answer business questions, troubleshoot issues, and respond to security incidents. For more information, see [CMPivot](/sccm/core/servers/manage/cmpivot).  


### Site server high availability
<!--1128774,1358224-->
High availability for the site server role is a Configuration Manager-based solution to install an additional site server in passive mode. The site server in passive mode is in addition to your existing site server that is in active mode. A site server in passive mode is available for immediate use, when needed. For more information, see the following articles: 
- [Site server high availability](/sccm/core/servers/deploy/configure/site-server-high-availability) 
- [Flowchart - Set up a site server in passive mode](/sccm/core/servers/deploy/configure/passive-site-server-flowchart)
- [Flowchart - Promote site server (planned)](/sccm/core/servers/deploy/configure/promote-site-server-flowchart)
- [Flowchart - Promote site server (unplanned)](/sccm/core/servers/deploy/configure/promote-site-server-unplanned-flowchart)



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


### SCAP extensions
<!--1357552-->
Convert Security Content Automation Protocol (SCAP) content to compliance settings baselines and generate SCAP reports using a console extension. This feature also includes a new dashboard to visualize the client compliance as well as XCCDF rule compliance. For more information, see [About the SCAP extensions](/sccm/compliance/plan-design/scap/about-scap).



<!--## Application Management-->



<!--## Operating system deployment-->





<!--## Software Center-->



## Software updates

### Deploy software updates without content
<!--1357933-->
You can now deploy software updates to devices without first downloading and distributing software update content to distribution points. This feature is beneficial when dealing with extremely large update content, or when you always want clients to get content from the Microsoft Update cloud service. Clients in this scenario can also download content from peers that already have the necessary content. The Configuration Manager client continues to manage the content download, thus can utilize the Configuration Manager peer cache feature, or other technologies such as Delivery Optimization. This feature supports any update type supported by Configuration Manager software updates management, including Windows and Office updates. For more information, see the **No deployment package** option when you [Manually deploy software updates](/sccm/sum/deploy-use/manually-deploy-software-updates) or [Automatically deploy software updates](/sccm/sum/deploy-use/automatically-deploy-software-updates).


### Filter automatic deployment rules by software update architecture
 <!--1322266-->
You can now filter automatic deployment rules (ADR) to exclude architectures like Itanium and ARM64. On the **Software Updates** page of the Create Automatic Deployment Rule Wizard, the **Architecture** property filter is now available. For more information, see [Automatically deploy software updates](/sccm/sum/deploy-use/automatically-deploy-software-updates).




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
