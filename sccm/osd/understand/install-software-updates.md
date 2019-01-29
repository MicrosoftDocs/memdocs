---
title: Install Software Updates
titleSuffix: Configuration Manager
description: Recommendations for using the task sequence step Install Software Updates in Configuration Manager.
ms.date: 01/28/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 72d1ccd5-3763-4f88-9273-e1a73e8f4286
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Install Software Updates

*Applies to: System Center Configuration Manager (Current Branch)*

The **Install Software Updates** step is commonly used in Configuration Manager task sequences. When installing or updating the OS, it triggers the software updates component. This step can cause challenges for some customers, such as long timeout delays or missed updates. Use the information in this article to help mitigate common issues with this step, and better troubleshoot when things go wrong.

For more information on the step, see [Install Software Updates](/sccm/osd/understand/task-sequence-steps#BKMK_InstallSoftwareUpdates)



## Recommendations

To help this process be successful, use the following recommendations:

#### Use offline servicing
Use Configuration Manager to regularly install applicable software updates to your image files. This practice then reduces the number of updates that you need to install during the task sequence. 

For more information, see [Apply software updates to an image](/sccm/osd/get-started/manage-operating-system-images#BKMK_OSImagesApplyUpdates).


#### Single index
Many image files include multiple indexes, such as for different editions of Windows. Reduce the image file to a single index that you require. This practice reduces the amount of time to apply software updates to the image. It also enables the next recommendation to [Reduce the image size](#bkmk_resetbase). 


#### <a name="bkmk_resetbase"></a> Reduce image size
When you apply software updates to the image, optimize the output by removing any superseded updates. Use DISM to mount the image, and then use the following commands: 

```
dism /Image:C:\Mountdir /Cleanup-Image /StartComponentCleanup /ResetBase 
dism /unmount-image /MountDir:C:\Mountdir /Commit  
```



## Image engineering decisions

When you design your imaging process, there are several options that can impact the installation of software updates:

- [Recapture the image every month](#bkmk_goldimage)  
- [Use offline servicing](#bkmk_offline)  
- [Use default image only](#bkmk_installwim)


### <a name="bkmk_goldimage"></a> Recapture the image every month

You have an automated process to capture a custom OS image on a regular schedule. This capture task sequence installs the latest software updates. The deployment task sequence installs any additional updates since capture.

For more information on this process, see [Create a task sequence to capture an OS](/sccm/osd/deploy-use/create-a-task-sequence-to-capture-an-operating-system).


#### Advantages
- Few updates to apply at deployment time, which saves time during deployment
- Fewer updates to worry about causing restarts
- Customized image for the organization
- Fewer variables at deployment time

#### Disadvantages 
- Time to create and capture image, even though it's mostly automated
- Increased time to distribute the image to distribution points, which can be seen as outage for active deployments
- Time to test through pre-production environments may be longer than OS patch cycle, which can make the updated image irrelevant 


### <a name="bkmk_offline"></a> Use offline servicing

Schedule Configuration Manager to apply software updates to your images. 

For more information, see [Apply software updates to an image](/sccm/osd/get-started/manage-operating-system-images#BKMK_OSImagesApplyUpdates).


#### Advantages
- Few updates to apply at deployment time, which saves time during deployment
- Fewer updates to worry about causing restarts
- You can schedule the servicing process at the site

#### Disadvantages 
- Manual selection of updates
- Increased time to distribute the image to distribution points
- Only supports CBS-based updates. It can't apply Office updates


### <a name="bkmk_installwim"></a> Use default image only

Use the default Windows install.wim image file in your deployment task sequences.

#### Advantages
- A known good source, which reduces the risk of image corruption as a possible issue
- Eliminates modifications to image as a possible issue

#### Disadvantages 
- Potential for high volume of updates during the deployment
- Increased deployment time for every device
- May not have needed customizations, requires additional task sequence steps to customize



## Flow chart

{insert flowchart diagram and text description}


