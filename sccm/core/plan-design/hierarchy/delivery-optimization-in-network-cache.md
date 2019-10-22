---
title: Delivery Optimization In-Network Cache
titleSuffix: Configuration Manager
description: Use your Configuration Manager distribution point as a local cache server for Delivery Optimization
ms.date: 09/10/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: c5cb5753-5728-4f81-b830-a6fd1a3e105c
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Delivery Optimization In-Network Cache in Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

<!--3555764-->

Starting in version 1906, you can install a Delivery Optimization In-Network Cache (DOINC) server on your distribution points. By caching this content on-premises, your clients can benefit from the Delivery Optimization feature, but you can help to protect WAN links.

This cache server acts as an on-demand transparent cache for content downloaded by Delivery Optimization. Use client settings to make sure this server is offered only to the members of the local Configuration Manager boundary group.

This cache is separate from Configuration Manager's distribution point content. If you choose the same drive as the distribution point role, it stores content separately.

> [!Note]  
> Delivery Optimization In-Network Cache server is an application installed on Windows Server that's still in development.  


## How it works

When you configure clients to use the Delivery Optimization In-Network Cache server, they no longer request Microsoft cloud-managed content from the internet. Clients request this content from the DOINC server installed on the distribution point. The DOINC server caches this content using the IIS feature for Application Request Routing (ARR). Then the cache server can quickly respond to any future requests for the same content. If the DOINC server is unavailable, or the content isn't yet cached, clients download the content from the internet. Clients also use Delivery Optimization, so download portions of the content from peers in their network.

![Diagram of how DOINC works](media/3555764-delivery-optimization-in-network-cache.png)

1. Client checks for updates and gets the address for the content delivery network (CDN).

2. Configuration Manager configures Delivery Optimization (DO) settings on the client, including the cache server name.

3. Client A requests content from the DO cache server.

4. If the cache doesn't include the content, then the DO cache server gets it from the CDN.

5. If the cache server fails to respond, the client downloads the content from the CDN.

6. Clients use DO to get pieces of the content from peers.


## Prerequisites and limitations

- An *on-premises* distribution point, with the following configurations:

    - Running Windows Server 2012, Windows Server 2012 R2, Windows Server 2016, or Windows Server 2019

    - The default web site enabled on port 80

    - Don't preinstall the IIS [Application Request Routing](https://docs.microsoft.com/iis/extensions/planning-for-arr/application-request-routing-version-2-overview) (ARR) feature. DOINC installs ARR and configures its settings. Microsoft can't guarantee that DOINC's ARR configuration won't conflict with other applications on the server that also use this feature.

    - The distribution point requires internet access to the Microsoft cloud. The specific URLs can vary depending upon the specific cloud-enabled content. For more information, see [Internet access requirements](/sccm/core/plan-design/network/internet-endpoints).

- Clients running Windows 10 version 1709 or later


## Enable DOINC

1. In the Configuration Manager console, go to the **Administration** workspace, and select the **Distribution Points** node.

1. Select an on-premises distribution point, and then in the ribbon select **Properties**.

1. In the properties of the distribution point role, on the **General** tab, configure the following settings:  

    1. Enable the option to **Enable this distribution point to be used as Delivery Optimization In-Network Cache server**  

        View and accept the license terms.

    2. **Local drive to be used**: Select the disk to use for the cache. **Automatic** is the default value, which uses the disk with the most free space.<sup>[Note 1](#bkmk_note1)</sup>  

        > [!Note]  
        > You can change this drive later. Any cached content is lost, unless you copy it to the new drive.

    3. **Disk space**: Select the amount of disk space to reserve in GB or a percentage of the total disk space. By default, this value is 100 GB.

        > [!Note]  
        > The default cache size should be sufficient for most customers. You can adjust the cache size later.

    4. **Retain cache when disabling the in-network cache server**: If you remove the cache server, and you enable this option, the server keeps the cache's content on the disk.  

1. In client settings, in the **Delivery Optimization** group, configure the setting to **Enable devices managed by Configuration Manager to use Delivery Optimization In-Network Cache servers (Beta) for content download**.  

### <a name="bkmk_note1"></a> Note 1: About drive selection

If you select **Automatic**, when Configuration Manager installs the DOINC component, it honors the **no_sms_on_drive.sms** file. For example, the distribution point has the file `C:\no_sms_on_drive.sms`. Even if the C: drive has the most free space, Configuration Manager configures DOINC to use another drive for its cache.

If you select a specific drive that already has the **no_sms_on_drive.sms** file, Configuration Manager ignores the file. Configuring DOINC to use that drive is an explicit intent. For example, the distribution point has the file `F:\no_sms_on_drive.sms`. When you explicitly configure the distribution point properties to use the **F:** drive, Configuration Manager configures DOINC to use the F: drive for its cache.

To change the drive after DOINC is installed:

- Manually configure the distribution point properties to use a specific drive letter.

- If set to automatic, first create the **no_sms_on_drive.sms** file. Then make some change to the distribution point properties to trigger a configuration change.

## Verify

When clients download cloud-managed content, they use Delivery Optimization from the cache server installed on your distribution point. Cloud-managed content includes the following types:

- Microsoft Store apps
- Windows features on demand, such as languages
- If you enable [Windows Update for Business policies](/sccm/sum/deploy-use/integrate-windows-update-for-business-windows-10): Windows 10 feature and quality updates
- For [co-management workloads](/sccm/comanage/workloads):
    - Windows Update for Business: Windows 10 feature and quality updates
    - Office Click-to-Run apps: Office apps and updates
    - Client apps: Microsoft Store apps and updates
    - Endpoint Protection: Windows Defender definition updates

On Windows 10 version 1809 or later, verify this behavior with the **Get-DeliveryOptimizationStatus** Windows PowerShell cmdlet. In the cmdlet output, review the **BytesFromCacheServer** value. For more information, see [Monitor Delivery Optimization](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization-setup#monitor-delivery-optimization).

If the cache server returns any HTTP failure, the Delivery Optimization client falls back to the original cloud source.

For more detailed information, see [Troubleshoot Delivery Optimization In-Network Cache in Configuration Manager](/sccm/core/servers/deploy/configure/troubleshoot-delivery-optimization-in-network-cache).

## See also

[Optimize Windows 10 updates with Delivery Optimization](/sccm/sum/deploy-use/optimize-windows-10-update-delivery)

[Troubleshoot Delivery Optimization In-Network Cache in Configuration Manager](/sccm/core/servers/deploy/configure/troubleshoot-delivery-optimization-in-network-cache)
