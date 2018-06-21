---
title: Technical Preview 1806.2
titleSuffix: Configuration Manager
description: Learn about new features available in the Configuration Manager Technical Preview version 1806.2.
ms.date: 06/25/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 3af2a69d-30e7-4dce-832d-82b7a1c082f8
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Capabilities in Technical Preview 1806.2 for System Center Configuration Manager

*Applies to: System Center Configuration Manager (Technical Preview)*

This article introduces the features that are available in the Technical Preview for Configuration Manager, version 1806.2. You can install this version to update and add new capabilities to your technical preview site. 

Review the [Technical Preview](/sccm/core/get-started/technical-preview) article before installing this update. That article familiarizes you with the general requirements and limitations for using a technical preview, how to update between versions, and how to provide feedback.     


<!--  Known Issues Template
## Known Issues in this Technical Preview

### <a name="ki_ANCHOR"></a> Known issue title
<!--bugID--
Issue description and cause.

#### Workaround
Steps to workaround, if any.  
-->

## Known Issues in this Technical Preview

### <a name="ki_version"></a> Version 1806.2 shows Version 1806 in About Configuration Manager
<!--518148-->
After upgrading to technical preview version 1806.2, if you open the **About Configuration Manager** window from the upper left corner of the console, it still shows **Version 1806**. 

#### Workaround
Use the **Site version** property to determine the difference between 1806 and 1806.2:

| Site version  | Version
|---------|---------|
| 5.0.8672.1000 | 1806 |
| 5.0.8682.1000 | 1806.2 |
 


</br>

**The following are new features you can try out with this version.**  


## <a name="bkmk_msix"><a> Support for new Windows app package formats
<!--1357427-->
Configuration Manager now supports the deployment of new Windows 10 app package (.msix) and app bundle (.msixbundle) formats. The latest [Windows Insider Preview](https://insider.windows.com/) builds currently support these new formats.

For an overview of MSIX, see [A closer look at MSIX](https://blogs.msdn.microsoft.com/sgern/2018/06/18/a-closer-look-at-msix/).

For how to create a new MSIX app, see [MSIX support introduced in Insider Build 17682](https://techcommunity.microsoft.com/t5/MSIX-Blog/MSIX-support-introduced-in-Insider-Build-17682/ba-p/202376).

### Prerequisites
- A Windows 10 client running at least Windows Insider Preview build 17682
- A Windows app package in the MSIX format

### Try it out!
Try to complete the tasks. Then send [Feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback) letting us know how it worked.

1. In the Configuration Manager console, [create an application](/sccm/apps/deploy-use/create-applications). 
2. Select the application installation file **Type** as **Windows app package (*.appx, *.appxbundle, *.msix, *.msixbundle)**.
3. [Deploy the application](/sccm/apps/deploy-use/deploy-applications) to the client running the latest Windows Insider Preview build.



## Next steps
For information about installing or updating the technical preview branch, see [Technical Preview for System Center Configuration Manager](/sccm/core/get-started/technical-preview).    
