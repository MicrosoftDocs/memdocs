---
title: Prepare Windows PE peer cache to reduce WAN traffic
titleSuffix: Configuration Manager
description: The Windows PE Peer Cache works in the Windows PE to get content from a local peer and minimize WAN traffic when there's no local distribution point.
ms.date: 06/18/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: medium
---
# Prepare Windows PE peer cache to reduce WAN traffic in Configuration Manager

*Applies to: Configuration Manager (current branch)*

When you deploy a new operating system in Configuration Manager, computers that run the task sequence can use Windows PE Peer Cache to obtain content from a local peer (a peer cache source) instead of downloading content from a distribution point. This helps minimize wide area network (WAN) traffic in branch office scenarios where there is no local distribution point.  

 Windows PE Peer Cache is similar to [Windows BranchCache](../../core/plan-design/configs/support-for-windows-features-and-networks.md#bkmk_branchcache), but functions in the Windows Preinstallation Environment (Windows PE). The following terms are used to describe the clients that use Windows PE Peer Cache:  

-   A **peer cache client** is a computer that is configured to use Windows PE Peer Cache.  

-   A **peer cache source** is a client that is configured for peer cache and that makes content available to other peer cache clients that request that content.  

Use the following sections to manage Peer Cache.

##  <a name="BKMK_PeerCacheObjects"></a> Objects stored on a Peer Cache source  
 A task sequence configured to use Windows PE Peer Cache can get the following content objects while running in Windows PE:  

- Operating system image  

- Driver package  

- Packages and Programs (When the client continues to run the task sequence in the full operating system, the client gets this content from a peer cache source if the task sequence was originally configured for peer cache when running in Windows PE.)  

- Additional boot images  

  The following content objects never transfer using peer cache. Instead, they transfer from a distribution point or by  Windows BranchCache if you have configured Windows BranchCache in your environment:  

- Applications  

- Software updates  

##  <a name="BKMK_PeerCacheWork"></a> How does  Windows PE Peer Cache work?  
 Consider a scenario with a branch office that does not have a distribution point but does have several clients enabled to use Windows PE Peer Cache. You deploy the task sequence configured to use peer cache to several clients that are configured to be part of the peer cache source. The first client to run the task sequence broadcasts a request for a peer with the content. It doesn't find one so it gets the content from a distribution point across the WAN. The client installs the new image and then stores the content in its Configuration Manager client cache so it can function as a peer cache source to other clients. When the next client runs the task sequence, it broadcasts a request on the subnet for a peer cache source, and that first client responds and makes its cached content  available.  

##  <a name="BKMK_PeerCacheDetermine"></a> Determine what  clients will be part of the Windows PE Peer Cache source  
 To help  you determine what computers to select as a Windows PE Peer Cache source, there are several things that you should consider:  

-   The Windows PE Peer Cache source should be a desktop computer that is always powered on and available to peer cache clients.  

-   The Windows PE Peer Cache has a client cache size sufficient to store the images.  

##  <a name="BKMK_PeerCacheRequirements"></a> Requirements for a client to use a  Windows PE Peer Cache source  
 For clients to use a Windows PE Peer Cache source, they must meet the following requirements:  

-   The Configuration Manager client must be able to communicate across the following ports on your network:  

    -   Port for the initial network broadcast to find a peer cache source. By default, this is UDP port 8004.  

    -   Port for content downloading from a peer cache source (HTTP and HTTPS). By default, this is TCP port 8003.  
    
        For more information, see [Ports used for connections](../../core/plan-design/hierarchy/ports.md#BKMK_PortsClient-ClientWakeUp).  

        > [!TIP]  
        >  Clients will use HTTPS to download content when it is available. However, the same port number is used for either HTTP or HTTPS.  

-   [Configure the client cache](../../core/clients/manage/configure-client-cache.md) on clients to ensure they have enough space to hold and store the images you deploy. Windows PE Peer Cache does not affect the configuration or behavior of the client cache.  

-   The deployment options for the  task sequence deployment must be configured as Download content locally when needed by task sequence.  

##  <a name="BKMK_PeerCacheConfigure"></a> Configure Windows PE Peer Cache  
 You can use the following methods to provision a client with peer cache content so it can serve as a peer cache source:  

- A peer cache client that cannot find a peer cache source with the content will download it from a distribution point.  If  the client receives client settings that enable peer cache and the task sequence is configured to preserve the cached content, the client becomes a peer cache source.  

- A peer cache client can get content from another peer cache client (a peer cache source).  Because the client is configured for peer cache, when it runs a task sequence that is configured to preserve the cached content, the client becomes a peer cache source.  

- A  client runs a task sequence that includes the optional step, [Download Package Content](../understand/task-sequence-steps.md#BKMK_DownloadPackageContent), which is used to prestage the relevant content that is included in the Windows PE Peer Cache task sequence. When you use this method:  

  -   The client does not need to install the image that is being deployed.  

  -   In addition to the **Download Package Content** option, the task sequence must also use the **Configuration Manager client cache** option. You use this option to store the content in the clients cache so the client can act as a peer cache source for other peer cache clients.  

  The following procedures will help you configure Windows PE Peer Cache on clients and configure task sequences that support peer cache.  

### To configure the Windows PE Peer Cache source computers  

1. In the Configuration Manager console, navigate to **Administration** > **Client Settings**, and then   create a new **Custom Client Device Settings** or edit an existing settings object. You can also configure this for the **Default Client Settings** object.  

   > [!TIP]  
   >  Use a custom settings object to manage which clients receive this configuration. For example, you might want to avoid configuring this on the laptops of users who are frequently on the move. A highly mobile system can be a poor source to provide content to other peer cache clients.  
   >   
   >  Also remember that when you configure this setting as part of the **Default Client Settings**, the configuration applies to all clients in your environment.  

2. Under **Client Cache Settings**, set **Enable Configuration Manager client in full OS to share content** to **Yes**.  

   -   By default, only HTTP is enabled. If you want to enable clients to download content over HTTPS, set **Enable HTTPS for client peer communication** to **Yes**.  

   -   By default, the port for broadcasts is set to 8004 and the port for content downloads is set to 8003. You can change both.  

3. Save and deploy the Client Settings to the clients that you select to be a peer cache source.  

   After a device is configured with this settings object, the device  is configured to act as a peer cache source. These settings should be deployed to potential peer cache clients to configure the required ports and protocols.  

###  <a name="BKMK_PeerCacheConfigureTS"></a> Configure a task sequence for Windows PE Peer Cache  
 When you configure the task sequence, use the following task sequence variables as Collection Variables on the collection to which the task sequence is deployed:  

- **SMSTSPeerDownload**  

   Value:  TRUE  

   This enables the client to use Windows PE Peer Cache.  

- **SMSTSPeerRequestPort**  

   Value: <Port number\>  

   When you do not use the default port configured in the Client Settings (8004), you must configure this variable with a custom value of the network port to use for the initial broadcast.  

- **SMSTSPreserveContent**  

   Value: TRUE  

   This flags the content in the task sequence to be retained in the Configuration Manager client cache after the deployment. This is different than using SMSTSPersisContent which only preserves the content for the duration of the task sequence and uses the task sequence cache, not the Configuration Manager client cache.  

  For more information, see [Task sequence variables](../understand/task-sequence-variables.md).  

###  <a name="BKMK_PeerCacheValidate"></a> Validate the success of using Windows PE peer cache  
 After you use Windows PE peer cache to deploy and install a task sequence, you can confirm that peer cache was successfully used in the process by viewing the **smsts.log** on the client that ran the task sequence.  

 In the log, locate an entry similar to the following where <*SourceServerName*> identifies the computer from which the client obtained the content. This computer should be a peer cache source, and not a distribution point server. Other details will vary based on your local environment and configurations.  

-   *<![LOG[Downloaded file from http:// <SourceServerName\>:8003/SCCM_BranchCache$/SS10000C/sccm?/install.wim to C:\\_SMSTaskSequence\Packages\SS10000C\install.wim ]LOG]!><time="14:24:33.329+420" date="06-26-2015" component="ApplyOperatingSystem" context="" type="1" thread="1256" file="downloadcontent.cpp:1626">*  
