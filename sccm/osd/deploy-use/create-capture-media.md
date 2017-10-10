---
title: "Create capture media - Configuration Manager"
description: "Use the Create Task Sequence Media Wizard to create capture media in Configuration Manager to capture an operating system image from a reference computer."
ms.custom: na
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 10eb8958-3848-49d7-95c0-16119b624580
caps.latest.revision: 11
caps.handback.revision: 0
author: Dougebyms.author: dougebymanager: angrobe

---
# Create capture media with System Center Configuration Manager*Applies to: System Center Configuration Manager (Current Branch)*
Capture media in Configuration Manager allows you to capture an operating system image from a reference computer. Use capture media for the following scenario:  

-   [Create a task sequence to capture an operating systems](create-a-task-sequence-to-capture-an-operating-system.md)  

##  <a name="BKMK_CreateCaptureMedia"></a> How to Create Capture Media  
 Use capture media to capture an operating system image from a reference computer. Capture media contains the boot image that starts the reference computer and the task sequence that captures the operating system image.

You create capture media by using the Create Task Sequence Media Wizard. Before you run the wizard, be sure that all the following conditions are met:  

|Task|Description|  
|----------|-----------------|  
|Boot image|Consider the following about the boot image that you will use in the task sequence to capture the operating system:<br /><br /> -   The architecture of the boot image must be appropriate for the architecture of the destination computer. For example, an x64 destination computer can boot and run an x86  or x64 boot image. However, an x86 destination computer can boot and run only an x86 boot image.<br />-   Ensure that the boot image contains the network and mass storage drivers that are required to provision the destination computer.|  
|Distribute all content associated with the task sequence|You must distribute to at least one distribution point all content that is required by the task sequence. This includes the boot image, operating system image, and other associated files. The wizard gathers the information from the distribution point when it creates the stand-alone media. You must have **Read** access rights to the content library on that distribution point.  For more information, see [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).|  
|Prepare the removable USB drive|For a removable USB drive:<br /><br /> If you are going to use a removable USB drive, the USB  drive must be connected to the computer where the wizard is run and the USB drive must be detectable by Windows as a removal device. The wizard writes directly to the USB drive when it creates the media.|  
|Create an output folder|For a CD/DVD set:<br /><br /> Before you run the Create Task Sequence Media Wizard to create media for a CD or DVD set, you must create a folder for the output files created by the wizard. Media that is created for a CD or DVD set is written as .iso files directly to the folder.|  

 Use the following procedure to create capture media.  

#### To create capture media  

1.  In the Configuration Manager console, click **Software Library**.  

2.  In the **Software Library** workspace, expand **Operating Systems**, and then click **Task Sequences**.  

3.  On the **Home** tab, in the **Create** group, click **Create Task Sequence Media** to start the Create Task Sequence Media Wizard.  

4.  On the **Select Media Type** page, select **Capture media**, and then click **Next**.  

5.  On the **Media Type** page, specify whether the media is a flash drive or a CD/DVD set, and then click configure the following:  

    -   If you select **USB flash drive**, specify the drive where you want to store the content.  

    -   If you select **CD/DVD set**, specify the capacity of the media and the name and path of the output files. The wizard writes the output files to this location. For example: **\\\servername\folder\outputfile.iso**  

         If the capacity of the media is too small to store the entire content, multiple files are created and you must store the content on multiple CDs or DVDs. When multiple media is required, Configuration Manager adds a sequence number to the name of each output file that it creates. In addition, if you deploy an application along with the operating system and the application cannot fit on a single media, Configuration Manager stores the application across multiple media. When the stand-alone media is run, Configuration Manager prompts the user for the next media where the application is stored.  

        > [!IMPORTANT]  
        >  If you select an existing .iso image, the Task Sequence Media Wizard deletes that image from the drive or share as soon as you proceed to the next page of the wizard. The existing image is deleted, even if you then cancel the wizard.  

     Click **Next**.  

6.  On the **Boot image** page, specify the following information, and then click **Next**.  

    > [!IMPORTANT]  
    >  The architecture of the boot image that you specify must be appropriate for the architecture of the reference computer. For example, an x64 reference computer can boot and run an x86 or x64 boot image. However, an x86 reference computer can boot and run only an x86 boot image.  

    -   In the **Boot image** box, specify the boot image to start the reference computer.  

    -   In the **Distribution point** box, specify the distribution point where the boot image resides. The wizard retrieves the boot image from the distribution point and writes it to the media.  

        > [!NOTE]  
        >  You must have Read access rights to the content library on the distribution point.  

7.  Complete the wizard.  
