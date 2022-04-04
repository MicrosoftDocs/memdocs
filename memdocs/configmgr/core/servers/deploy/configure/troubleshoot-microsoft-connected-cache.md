---
title: Troubleshoot Connected Cache
titleSuffix: Configuration Manager
description: Technical details for Microsoft Connected Cache to help you troubleshoot issues.
ms.date: 11/23/2021
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: troubleshooting
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: medium
---

# Troubleshoot Microsoft Connected Cache in Configuration Manager

This article provides technical details about Microsoft Connected Cache in Configuration Manager. Use it to help troubleshoot issues that you might have in your environment. For more information on how it works and how to use it, see [Microsoft Connected Cache in Configuration Manager](../../../plan-design/hierarchy/microsoft-connected-cache.md).

## Verify

When you correctly install the Delivery Optimization cache server, and correctly configure clients, they download from the cache server installed on your distribution point rather than the internet.

Verify this behavior [on a client](#verify-on-a-client) or [on the server](#verify-on-the-server).

### Verify on a client

1. On a client running a supported version of Windows 10 or later, download cloud-managed content. For more information on the types of content that Connected Cache supports, see [Supported content types](../../../plan-design/hierarchy/microsoft-connected-cache.md#supported-content-types).

1. Open PowerShell and run the following command: `Get-DeliveryOptimizationStatus`.

    For example:

    ```PowerShell
    PS C:\> Get-DeliveryOptimizationStatus

    FileId                      : ec523d49c4f7c3c4444f0d9b952286ce40fdcee4
    FileSize                    : 549064
    TotalBytesDownloaded        : 549064
    PercentPeerCaching          : 0
    BytesFromPeers              : 0
    BytesFromHttp               : 0
    Status                      : Caching
    Priority                    : Background
    BytesFromCacheServer        : 549064
    BytesFromLanPeers           : 0
    BytesFromGroupPeers         : 0
    BytesFromInternetPeers      : 0
    BytesToLanPeers             : 0
    BytesToGroupPeers           : 0
    BytesToInternetPeers        : 0
    DownloadDuration            : 00:00:00.0780000
    HttpConnectionCount         : 2
    LanConnectionCount          : 0
    GroupConnectionCount        : 0
    InternetConnectionCount     : 0
    DownloadMode                : 99
    SourceURL                   : http://au.download.windowsupdate.com/c/msdownload/update/software/defu/2019/09/am_delta_p
                                atch_1.301.664.0_ec523d49c4f7c3c4444f0d9b952286ce40fdcee4.exe
    NumPeers                    : 0
    PredefinedCallerApplication : WU Client Download
    ExpireOn                    : 9/6/2019 8:36:19 AM
    IsPinned                    : False
    ```

Notice that the `BytesFromCacheServer` attribute isn't zero.

If the client isn't configured correctly, or the cache server isn't installed correctly, the Delivery Optimization client falls back to the original cloud source. Then the `BytesFromCacheServer` attribute will be zero.

### Verify on the server

First, verify the registry properties are configured correctly: `HKLM\SOFTWARE\Microsoft\Delivery Optimization In-Network Cache`. For example, the drive cache location is `PrimaryDrivesInput\DOINC-E77D08D0-5FEA-4315-8C95-10D359D59294`, where `PrimaryDrivesInput` can be multiple drives, such as `C,D,E`.

Next, use the following method to simulate a client download request to the server with the mandatory headers.

1. Open a 64-bit PowerShell window as an administrator.
1. Run the following command, and replace the name or IP address of your server for `<DoincServer>`:

    ```PowerShell
    Invoke-WebRequest -URI "http://<DoincServer>/mscomtest/wuidt.gif" -Headers @{"Host"="b1.download.windowsupdate.com"}
    ```

    The output looks similar to the following example:

    ```PowerShell
    PS C:\WINDOWS\system32> Invoke-WebRequest -URI "http://SERVER01.CONTOSO.COM/mscomtest/wuidt.gif" -Headers @{"Host"="b1.download.windowsupdate.com"}


    StatusCode        : 200
    StatusDescription : OK
    Content           : {71, 73, 70, 56...}
    RawContent        : HTTP/1.1 200 OK
                        X-HW: 1567797125.dop019.se2.t,1567797125.cds058.se2.s,1567797125.dop114.at2.r,1567797125.cds079.at2
                        .p,1567797125.cds058.se2.p
                        X-CCC: cdP+dRBgUCoZO1mezA9zhg2VwQ7P1JWTh9k+GhfQmu8=_SLwv...
    Headers           : {[X-HW, 1567797125.dop019.se2.t,1567797125.cds058.se2.s,1567797125.dop114.at2.r,1567797125.cds079.a
                        t2.p,1567797125.cds058.se2.p], [X-CCC,
                        cdP+dRBgUCoZO1mezA9zhg2VwQ7P1JWTh9k+GhfQmu8=_SLwvtSBQdT3uPQ5ikBe1ABMbdYIIncem+h5dtcLI6GY=],
                        [X-CID, 100], [Accept-Ranges, bytes]...}
    RawContentLength  : 969710
    ```

    The following attributes indicate success:

    - `StatusCode : 200`
    - `StatusDescription : OK`

## Log files

- **Application Request Routing (ARR) setup log**: `%temp%\arr_setup.log`
- **Connected Cache server setup log**: `SMS_DP$\Ms.Dsp.Do.Inc.Setup\DoincSetup.log` on the distribution point and `DistMgr.log` on the site server
- **Internet Information Services (IIS) operational logs**: By default, `%SystemDrive%\inetpub\logs\LogFiles`
- **Connected Cache server operational log**: `C:\Doinc\Product\Install\Logs`

    > [!TIP]
    > Among other uses, this log can help you identify connectivity issues with the Microsoft cloud.

## Setup error codes

When Configuration Manager installs the Connected Cache component on the distribution point, the following table lists the possible error codes that might occur:

| Error code | Error description |
|------------|-------------------|
| 0x00000000 | Success |
| 0x00000BC2 | Success, reboot required |
| 0x00000643 | Generic install failure |
| 0x00D00001 | Connected Cache setup can only be run if Internet Information Services (IIS) has been installed |
| 0x00D00002 | Connected Cache setup can only be run if a 'Default Web Site' exists on the server |
| 0x00D00003 | You can't install Connected Cache if Application Request Routing (ARR) is already installed |
| 0x00D00004 | Connected Cache setup can only be run if Application Request Routing (ARR) was installed by the Install.ps1 script |
| 0x00D00005 | Connected Cache setup requires a PowerShell session running as Administrator |
| 0x00D00006 | Connected Cache setup can only be run from a 64-bit PowerShell environment |
| 0x00D00007 | Connected Cache setup can only be run on a Windows Server |
| 0x00D00008 | Failure: The number of cache drives specified must match the number of cache drive size percentages specified |
| 0x00D00009 | Failure: A valid cache node ID must be supplied |
| 0x00D0000A | Failure: A valid cache drive set must be supplied |
| 0x00D0000B | Failure: A valid cache drive size percent set must be supplied |
| 0x00D0000C | Failure: A valid cache drive size percent set or cache drive size in GB must be supplied |
| 0x00D0000D | Failure: A valid cache drive size percent set and cache drive size in GB cannot both be supplied |
| 0x00D0000E | Failure: The number of cache drives specified must match the number of cache drives size in GB specified |
| 0x00D0000F | Failure: Couldn't back up the applicationhost.config file from $AppHostConfig to $AppHostConfigDestinationName |
| 0x00D00010 | Failure: Couldn't back up the Default Web Site web.config file from $WebsiteConfigFilePath to $WebConfigDestinationName |
| 0x00D00011 | Failure: An exception occurred in SetupARRWebFarm.ps1 |
| 0x00D00012 | Failure: An exception occurred in SetupARRWebFarmRewriteRules.ps1 |
| 0x00D00013 | Failure: An exception occurred in SetupARRWebFarmProperties.ps1 |
| 0x00D00014 | Failure: An exception occurred in SetupAllowableServerVariables.ps1 |
| 0x00D00015 | Failure: An exception occurred in SetupFirewallRules.ps1 |
| 0x00D00016 | Failure: An exception occurred in SetupAppPoolProperties.ps1 |
| 0x00D00017 | Failure: An exception occurred in SetupARROutboundRules.ps1 |
| 0x00D00018 | Failure: An exception occurred in SetupARRDiskCache.ps1 |
| 0x00D00019 | Failure: An exception occurred in SetupARRProperties.ps1 |
| 0x00D0001A | Failure: An exception occurred in SetupARRHealthProbes.ps1 |
| 0x00D0001B | Failure: An exception occurred in VerifyIISSItesStarted.ps1 |
| 0x00D0001C | Failure: An exception occurred in SetDrivesToHealthy.ps1 |
| 0x00D0001D | Failure: An exception occurred in VerifyCacheNodeSetup.ps1 |
| 0x00D0001E | You can't install Connected Cache if the Default Web Site isn't on port 80 |
| 0x00D0001F | Failure: The cache drive allocation in percentage can't exceed 100 |
| 0x00D00020 | Failure: The cache drive allocation in GB can't exceed the drive's free space |
| 0x00D00021 | Failure: The cache drive allocation in percentage must be greater than 0 |
| 0x00D00022 | Failure: The cache drive allocation in GB must be greater than 0 |
| 0x00D00023 | Failure: An exception occurred in RegisterScheduledTask_CacheNodeKeepAlive |
| 0x00D00024 | Failure: An exception occurred in RegisterScheduledTask_Maintenance |
| 0x00D00025 | Failure: An exception occurred setting up the rewrite rules for HTTPS farm: $FarmName |
| 0x00D00026 | Failure: An exception occurred setting up the rewrite rules for HTTP farm: $FarmName |
| 0x00D00027 | You can't install Connected Cache because dependent software "Application Request Routing (ARR)" failed to install. See the log file located at %temp%\arr_setup.log |

## IIS configurations

The Connected Cache server installation makes several modifications to the IIS configuration on the distribution point.

### Application request routing

The Connected Cache server installs and configures IIS [Application Request Routing](https://www.iis.net/downloads/microsoft/application-request-routing). To avoid potential conflicts, the distribution point can't already have this component installed.

### Allowed server variables

After you install the Connected Cache server, the default website has the following *local* server variables:

- HTTP_HOST
- QUERY_STRING
- X-CCC
- X-CID
- X-DOINC-OUTBOUND

### Rewrite rules

The Connected Cache server adds the following rewrite rules:

#### Inbound rewrite rules

- `Doinc_ForwardToFarm_shswda01.download.manage-selfhost.microsoft.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_swdc01.manage.microsoft.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_swdc02.manage.microsoft.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_dl.delivery.mp.microsoft.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_officecdn.microsoft.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_b1.download.windowsupdate.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_download.windowsupdate.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_officecdn.microsoft.com.edgesuite.net_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_au.b1.download.windowsupdate.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_assets1.xboxlive.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_au.download.windowsupdate.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_emdl.ws.microsoft.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_tlu.dl.delivery.mp.microsoft.com_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_assets2.xboxlive.com_E77D08D0-5FEA-4315-8C95-10D359D59294`

#### Outbound rewrite rules

- `Doinc_Outbound_SetHeader_X_CID_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_Outbound_SetHeader_X_CCC_E77D08D0-5FEA-4315-8C95-10D359D59294`

### IIS custom headers

If requests with `X-Forwarded-For` headers are blocked on a proxy server, either allow the header on the proxy server or change the custom header name in IIS for each server farm.

To change the custom header name for each server farm:

1. Open IIS Manager.
1. Select **Server Farms**.
1. Select a server farm and the proxy icon.
1. Under **Custom Headers**, change the value `X-Forwarded-For` to `X-Forwarded-For-<custom-name>`.

## Manage server resources

Disk space required for each Connected Cache server might vary, based on your organization's update requirements. Disk space of 100 GB should be enough to cache the following content:

- A feature update
- Two to three months of quality and Microsoft 365 Apps updates
- Microsoft Intune apps and Windows inbox apps

The Connected Cache server shouldn't consume much system memory or processor time. After you install the Connected Cache server, if you notice significant process or memory resource consumption, analyze the IIS and ARR log files.

If the IIS and ARR log files take up too much space on the server, there are several methods you can use to manage the log files. For more information, see [Managing IIS log file storage](/iis/manage/provisioning-and-managing-iis/managing-iis-log-file-storage#overview).

## See also

[Microsoft Connected Cache in Configuration Manager](../../../plan-design/hierarchy/microsoft-connected-cache.md)
