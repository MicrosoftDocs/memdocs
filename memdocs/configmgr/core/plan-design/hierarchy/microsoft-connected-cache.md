---
title: Microsoft Connected Cache
titleSuffix: Configuration Manager
description: Use your Configuration Manager distribution point as a local cache server for Delivery Optimization
ms.date: 04/05/2021
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c5cb5753-5728-4f81-b830-a6fd1a3e105c
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Microsoft Connected Cache in Configuration Manager

*Applies to: Configuration Manager (current branch)*

<!--3555764-->

You can install a Microsoft Connected Cache server on your distribution points. By caching this content on-premises, your clients can benefit from the Delivery Optimization feature that can help to protect WAN links.

> [!NOTE]
> This feature is now called **Microsoft Connected Cache**. It was previously known as Delivery Optimization In-Network Cache.

This cache server acts as an on-demand transparent cache for content downloaded by Delivery Optimization. Use client settings to make sure this server is offered only to the members of the local Configuration Manager boundary group.

This cache is separate from Configuration Manager's distribution point content. If you choose the same drive as the distribution point role, it stores content separately.

> [!NOTE]
> The Connected Cache server is an application installed on Windows Server. This application is still in development.

## How it works

When you configure clients to use the Connected Cache server, they no longer request Microsoft cloud-managed content from the internet. Clients request this content from the cache server installed on the distribution point. The on-premises server caches this content using the IIS feature for Application Request Routing (ARR). Then the cache server can quickly respond to any future requests for the same content. If the Connected Cache server is unavailable, or the content isn't yet cached, clients download the content from the internet. Clients also use Delivery Optimization to download portions of the content from peers in their network.

![Diagram of how Connected Cache works](media/3555764-microsoft-connected-cache.png)

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

  - Don't preinstall the IIS [Application Request Routing](/iis/extensions/planning-for-arr/application-request-routing-version-2-overview) (ARR) feature. Connected Cache installs ARR and configures its settings. Microsoft can't guarantee that the Connected Cache's ARR configuration won't conflict with other applications on the server that also use this feature.

  - The distribution point requires internet access to the Microsoft cloud. The specific URLs can vary depending upon the specific cloud-enabled content. Make sure to also allow the endpoints for delivery optimization. For more information, see [Internet access requirements](../network/internet-endpoints.md).

  - Starting in version 2002, the Connected Cache application can use an unauthenticated proxy server for internet access. For more information, see [Configure the proxy for a site system server](../network/proxy-server-support.md#configure-the-proxy-for-a-site-system-server).<!-- 5856396 -->

  - Don't use a distribution point that has other site roles, for example, a management point. Enable Connected Cache on a site system server that only has the distribution point role.<!-- 9580345 -->

- Clients running Windows 10 version 1709 or later

## Enable Connected Cache

1. In the Configuration Manager console, go to the **Administration** workspace, and select the **Distribution Points** node.

1. Select an *on-premises* distribution point, and then in the ribbon select **Properties**.

1. In the properties of the distribution point role, on the **General** tab, configure the following settings:  

    1. Enable the option to **Enable this distribution point to be used as Microsoft Connected Cache server**  

        View and accept the license terms.

    2. **Local drive to be used**: Select the disk to use for the cache. **Automatic** is the default value, which uses the disk with the most free space.<sup>[Note 1](#bkmk_note1)</sup>  

        > [!Note]  
        > You can change this drive later. Any cached content is lost, unless you copy it to the new drive.

    3. **Disk space**: Select the amount of disk space to reserve in GB or a percentage of the total disk space. By default, this value is 100 GB.

        > [!Note]  
        > The default cache size should be sufficient for most customers. You can adjust the cache size later.
        >
        > If the cache size on disk exceeds the allocated space, ARR clears space by removing content based on its built-in heuristics.<!-- SCCMDocs#2045 -->

    4. **Retain cache when disabling the Connected Cache server**: If you remove the cache server, and you enable this option, the server keeps the cache's content on the disk.  

1. In client settings, in the **Delivery Optimization** group, configure the setting to **Enable devices managed by Configuration Manager to use Microsoft Connected Cache servers for content download**.  

### <a name="bkmk_note1"></a> Note 1: About drive selection

If you select **Automatic**, when Configuration Manager installs the Connected Cache component, it honors the **NO_SMS_ON_DRIVE.SMS** file. For example, the distribution point has the file `C:\NO_SMS_ON_DRIVE.SMS`. Even if the C: drive has the most free space, Configuration Manager configures Connected Cache to use another drive for its cache.

If you select a specific drive that already has the **NO_SMS_ON_DRIVE.SMS** file, Configuration Manager ignores the file. Configuring Connected Cache to use that drive is an explicit intent. For example, the distribution point has the file `F:\NO_SMS_ON_DRIVE.SMS`. When you explicitly configure the distribution point properties to use the **F:** drive, Configuration Manager configures Connected Cache to use the F: drive for its cache.

To change the drive after you install Connected Cache:

- Manually configure the distribution point properties to use a specific drive letter.

- If set to automatic, first create the **NO_SMS_ON_DRIVE.SMS** file. Then make some change to the distribution point properties to trigger a configuration change.

### Automation

<!-- SCCMDocs#1911 -->

You can use the Configuration Manager SDK to automate the configuration of Microsoft Connected Cache settings on a distribution point. As is the case for all site roles, use the [SMS_SCI_SysResUse WMI class](../../../develop/reference/core/servers/configure/sms_sci_sysresuse-server-wmi-class.md). For more information, see [Programming the site roles](../../../develop/osd/about-operating-system-deployment-site-role-configuration.md#programming-the-site-roles).

When you update the **SMS_SCI_SysResUse** instance for the distribution point, set the following properties:

- **AgreeDOINCLicense**: Set to `1` to accept the license terms.
- **Flags**: Enable `|= 4`, disable `&= ~4`
- **DiskSpaceDOINC**: Set to `Percentage` or `GB`
- **RetainDOINCCache**: Set to `0` or `1`
- **LocalDriveDOINC**: Set to `Automatic`, or a specific drive letter, such as `C:` or `D:`

## Verify

When clients download cloud-managed content, they use Delivery Optimization from the cache server installed on your distribution point. Cloud-managed content includes the following types:

- Microsoft Store apps
- Windows features on demand, such as languages
- If you enable [Windows Update for Business policies](../../../sum/deploy-use/integrate-windows-update-for-business-windows-10.md): Windows 10 feature and quality updates
- For [co-management workloads](../../../comanage/workloads.md):
  - Windows Update for Business: Windows 10 feature and quality updates
  - Office Click-to-Run apps: Microsoft 365 Apps and updates
  - Client apps: Microsoft Store apps and updates
  - Endpoint Protection: Windows Defender definition updates

On Windows 10 version 1809 or later, verify this behavior with the **Get-DeliveryOptimizationStatus** Windows PowerShell cmdlet. In the cmdlet output, review the **BytesFromCacheServer** value. For more information, see [Monitor Delivery Optimization](/windows/deployment/update/waas-delivery-optimization-setup#monitor-delivery-optimization).

If the cache server returns any HTTP failure, the Delivery Optimization client falls back to the original cloud source.

For more detailed information, see [Troubleshoot Microsoft Connected Cache in Configuration Manager](../../servers/deploy/configure/troubleshoot-microsoft-connected-cache.md).

## <a name="bkmk_intune"></a> Support for Intune Win32 apps

<!--5032900-->

When you enable Connected Cache on your Configuration Manager distribution points, they can serve Microsoft Intune Win32 apps to co-managed clients.

> [!TIP]
> All other content that Intune-managed devices download from Microsoft with Delivery Optimization can also be cached on Microsoft Connected Cache. This content includes software updates for Windows, Microsoft 365 apps, and Microsoft Edge.

### Prerequisites

#### Client

- Update the client to the latest version.

- The client device needs to have at least 4 GB of memory.

    > [!TIP]
    > Use the following group policy setting: Computer Configuration > Administrative Templates > Windows Components > Delivery Optimization > **Minimum RAM capacity (inclusive) required to enable use of Peer Caching (in GB)**.

#### Site

- Enable Connected Cache on a distribution point. For more information, see [Microsoft Connected Cache](microsoft-connected-cache.md).

- The client and the Connected Cache-enabled distribution point need to be in the same boundary group. If a client isn't in a boundary group with a Connected Cache-enabled distribution point, it won't download content from a Connected Cache-enabled distribution point in a neighbor or site default boundary group.

  - Enable **Allow peer downloads in this boundary group** option for the Boundary Group which contains the client and the distribution point. For more information, see [Boundary Group options](../../servers/deploy/configure/boundary-groups.md#bkmk_bgoptions).

- Enable the following client settings in the [**Delivery Optimization**](../../clients/deploy/about-client-settings.md#delivery-optimization) group:

  - **Use Configuration Manager Boundary Groups for Delivery Optimization Group ID**
  - **Enable devices managed by Configuration Manger to use Microsoft Connected Cache servers for content download**

- Enable co-management, and switch the **Client apps** workload to **Pilot Intune** or **Intune**. For more information, see the following articles:

  - [Workloads - Client apps](../../../comanage/workloads.md#client-apps)
  - [How to enable co-management](../../../comanage/how-to-enable.md)
  - [Switch workloads to Intune](../../../comanage/how-to-switch-workloads.md)

    If in pilot, add the client to the pilot collection for Client Apps.

#### Intune

- This feature only supports the Intune Win32 app type.

  - Create and assign (deploy) a new app in Intune for this purpose. (Apps created before Intune version 1811 don't work.) For more information, see [Intune Win32 app management](/intune/apps/apps-win32-app-management).

## Support for cloud-managed devices

<!-- 8827227 -->

When you install a Microsoft Connected Cache on a Configuration Manager distribution point, cloud-managed devices can use the on-premises cache. For example, a device that's managed by Intune, but connects to the on-premises network. As long as the device can communicate with the server, the cache is available to deliver content to these devices.

To configure the device to use the Microsoft Connected Cache, configure the **DOCacheHost** policy. Set it to the FQDN or IP address of the Configuration Manager distribution point. For more information on this policy, see [Policy CSP - DeliveryOptimization](/windows/client-management/mdm/policy-csp-deliveryoptimization#deliveryoptimization-docachehost). To use Intune to configure this policy, use the **Cache server host names** setting. For more information, see [Delivery Optimization settings for Windows 10 devices in Intune](../../../../intune/configuration/delivery-optimization-settings.md#local-server-caching).

When you enable this policy for cloud-managed devices, either type of device can request the server to cache content, and either can download the content. If multiple devices request the same content, no matter their management authority, they download supported and available content from the Microsoft Connected Cache.

## See also

[Optimize Windows 10 updates with Delivery Optimization](../../../sum/deploy-use/optimize-windows-10-update-delivery.md)

[Troubleshoot Microsoft Connected Cache in Configuration Manager](../../servers/deploy/configure/troubleshoot-microsoft-connected-cache.md)
