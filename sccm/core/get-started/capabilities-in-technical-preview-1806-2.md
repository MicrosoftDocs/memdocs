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

### <a name="ki_contentlib"></a> Site fails to upgrade with remote content library
<!--514642-->
The site fails to upgrade with the following errors in **cmupdate.log**:  
```  
Failed to find any valid drives  
GetContentLibraryParameters failed; 0x80070057  
ERROR: Failed to process configuration manager update.  
```  

This issue occurs in this release when the content library is in a remote location.

#### Workaround
Move the content library to a drive local to the site server. For more information, see [Configure a remote content library for the site server](/sccm/core/get-started/capabilities-in-technical-preview-1804#configure-a-remote-content-library-for-the-site-server). 



</br>

**The following are new features you can try out with this version.**  


## Feature Name
Feature description



## Next steps
For information about installing or updating the technical preview branch, see [Technical Preview for System Center Configuration Manager](/sccm/core/get-started/technical-preview).    
