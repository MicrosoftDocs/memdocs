---
title: Icons used for software updates
titleSuffix: Configuration Manager
description: The Configuration Manager console contains icons that indicate a state for the synchronized update or software update group.
manager: dougeby
ms.date: 06/21/2021
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
author: mestew
ms.author: mstewart
ms.localizationpriority: medium
---
# Icons used for software updates in Configuration Manager

*Applies to: Configuration Manager (current branch)*

Synchronized software updates are displayed in the Configuration Manager console, and the first column for each software update contains an icon that indicates a specific state. Software update groups are also represented with an icon that provides information about the state of the software updates contained in the group. This section provides information about the software update icons and what each icon represents.  

## Icons for Software Updates  
 Synchronized software updates are represented by one of the following icons.  

### Normal Icon  
 ![Normal icon](../media/Normal.jpg) The icon with the green arrow represents a normal software update.  

 **Description:**  

 Normal software updates have been synchronized and are available for software deployment.  

 **Operational Concerns:**  

 There are no operational concerns.  

### Expired Icon  
 ![Expired icon](../media/Expired.jpg) The icon with the black X represents an expired software update. You can also identify expired software updates by viewing the **Expired** column for the software update when it displays in the Configuration Manager console.  

 **Description:**  

 Expired software updates were previously deployable to client computers, but once a software update is expired, new deployments can no longer be created for the software updates. Expired software updates are removed from active deployments and will no longer be made available to clients.  

 **Operational Concerns:**  

 There are no operational concerns.

### Superseded Icon  
 ![Superseded icon](../media/Superseded.jpg) The icon with the yellow star represents a superseded software update. You can also identify superseded software updates by viewing the **Superseded** column for the software update when it displays in the Configuration Manager console.  

 **Description:**  

 Superseded software updates have been replaced with newer versions of the software update. Typically, a software update that supersedes another software update does one or more of the following things:  

- Enhances, improves, or adds to the fix provided by one or more previously released software updates.  

- Improves the efficiency of its software update file package, which clients install if the software update is approved for installation. For example, the superseded software update might contain files that are no longer relevant to the fix or to the operating systems now supported by the new software update, so those files aren't included in the superseding software update's file package.  

- Updates newer versions of a product, or in other words, is no longer applicable to older versions or configurations of a product. Software updates can also supersede other software updates if modifications have been made to expand language support. For example, a later revision of a product update for Microsoft 365 Apps might remove support for an older operating system, but add additional support for new languages in the initial software update release.  

  On the Supersedence Rules tab in the Software Update Point Component properties, you can specify how to manage superseded software updates. For more information, see [Supersedence rules](../plan-design/plan-for-software-updates.md#BKMK_SupersedenceRules).  

  **Operational Concerns:**  
   Configuration Manager can [automatically expire superseded updates](../get-started/install-a-software-update-point.md#supersedence-rules) based on a schedule you choose. The default setting is to wait 3 months before expiring a superseded update. The 3 month default is to give you time to verify the update is no longer needed by any of your client computers. It's recommended that you don't assume that superseded updates should be immediately expired in favor of the new, superseding update. You can display a list of the software updates that supersede the software update on the **Supersedence Information** tab in the software update properties.  

### Invalid Icon  
 ![Invalid icon](../media/Invalid.jpg) The icon with the red X represents an invalid software update.  

 **Description:**  

 Invalid software updates are in an active deployment, but for some reason the content (software update files) isn't available. The following are scenarios in which this state can occur:  

- You successfully deploy the software update, but the software update file is removed from the deployment package and is no longer available.  

- You create a software update deployment at a site and the deployment object is successfully replicated to a child site, but the deployment package hasn't successfully replicated to the child site.  

  **Operational Concerns:**  

  When the content is missing for a software update, clients are unable to install the software update until the content becomes available on a distribution point. You can redistribute the content to distribution points by using the **Redistribute** action. When content is missing for a software update in a deployment created at a parent site, the software update must be replicated or redistributed to the child site. For more information about content redistribution, see [Manage the content you've distributed](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_manage).  

### Metadata-Only Icon
 ![Metadata-only icon](../media/MetadataOnly.png) The icon with the blue arrow represents a metadata-only software update.

 **Description:**  

 Metadata-only software updates are available in the Configuration Manager console for reporting. You can't deploy or download metadata-only software updates because a software update file isn't associated with the software updates metadata.  

 **Operational Concerns:**  

 Metadata-only software updates are available for reporting purposes and aren't intended for software update deployment.  

## Icons for Software Update Groups  
 Software update groups are represented by one of the following icons.  

### Normal Icon  
 ![Software Update Groups - Normal icon](../media/Normal.jpg) The icon with the green arrow represents a software update group that contains only normal software updates.  

 **Operational Concerns:**  

 There are no operational concerns.  

### Expired Icon  
 ![Software Update Groups - Expired icon](../media/Expired.jpg) The icon with the black X represents a software update group that contains one or more expired software updates.  

 **Operational Concerns:**  

 Remove or replace expired software updates in the software update group when possible.  

### Superseded Icon  
 ![Software Update Groups - Superseded icon](../media/Superseded.jpg) The icon with the yellow star represents a software update group that contains one or more superseded software updates.  

 **Operational Concerns:**  

 Replace the superseded software update in the software update group with the superseding software update when possible.  

### Invalid Icon  
 ![Software Update Groups - Invalid icon](../media/Invalid.jpg) The icon with the red X represents a software update group that contains one or more invalid software updates.  

 **Operational Concerns:**  

 When the content is missing for a software update, clients are unable to install the software update until the content becomes available on a distribution point. You can redistribute the content to distribution points by using the **Redistribute** action. When content is missing for a software update in a deployment created at a parent site, the software update needs to be replicated or redistributed to the child site. For more information about content redistribution, see [Manage the content you've distributed](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_manage).  


## Next steps 

[Plan for software updates](../plan-design/plan-for-software-updates.md)