---
title: Troubleshoot Connected Cache
description: Technical details for Microsoft Connected Cache to help you troubleshoot issues.
ms.date: 11/23/2021
ms.subservice: core-infra
ms.topic: troubleshooting
ms.collection: tier3
---

# Troubleshoot Microsoft Connected Cache with Configuration Manager

This article provides technical details about Microsoft Connected Cache with Configuration Manager. Use it to help troubleshoot issues that you might have in your environment. For more information on how it works and how to use it, see [Microsoft Connected Cache with Configuration Manager](../../../plan-design/hierarchy/microsoft-connected-cache.md).

## Verify

When you correctly install the Delivery Optimization cache server, and correctly configure clients, they download from the cache server installed on your distribution point rather than the internet.

Verify this behavior [on a client](#verify-on-a-client) or [on the server](#verify-on-the-server).

### Verify on a client

Use the following workflow to verify the Microsoft Connected Cache configuration:

1. Open a 64-bit PowerShell window as an administrator.
1. Ensure the host is targeted by policy. If policy isn't set by Configuration Manager or Intune, set `DOCacheHost` to the distribution point FQDN or IP:

    ```powershell
    $parentKeyPath = "HKLM:\SOFTWARE\Policies\Microsoft\Windows\DeliveryOptimization"
    if (!(Test-Path $parentKeyPath)) {
        New-Item -Path $parentKeyPath -ItemType RegistryKey -Force -ErrorAction Stop | Out-Null
    }
    Set-ItemProperty -Path $parentKeyPath -Name "DOCacheHost" -Value "[DP IP Address or FQDN]" -ErrorAction Stop
    ```

1. Verify HTTP delivery by running the following command, and replace the name or IP address of your server for `<DoincServer>`:

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

1. Verify MSIX download via HTTPS channel by requesting Microsoft Teams content from Connected Cache:

    ```powershell
    Add-AppxPackage "https://installer.teams.static.microsoft/production-windows-x64/25177.2002.3761.5185/MSTeams-x64.msix"
    ```

    Expected result: Download completes without error.

1. Verify that bytes were served by cache:

    ```powershell
    Get-DeliveryOptimizationStatus | Select-Object DownloadMode, TotalBytesDownloaded, BytesFromCacheServer
    ```

    Expected result: `BytesFromCacheServer` is greater than `0`.

1. (Optional) In environments using DOINC/CDN byte reporting, interpret results as follows:

    - `CDN` bytes equals `DOINC` bytes: 100% of bytes came from cache.
    - `DOINC` bytes is `0`: 100% of bytes came from CDN.
    - `CDN` bytes greater than `DOINC` bytes: Partial bytes came from cache.

> [!NOTE]
> You may observe an issue where Intune content isn't cached until the third request from the cache server. This can occur when the Intune CDN returns a `VARY` header that instructs content not to be cached.

### Verify on the server

On the distribution point server, check the registry values at `HKLM\SOFTWARE\Microsoft\Delivery Optimization In-Network Cache`. Verify that `PrimaryDrivesInput` value reflects the actual cache location, like  `PrimaryDrivesInput\DOINC-E77D08D0-5FEA-4315-8C95-10D359D59294`. Note that `PrimaryDrivesInput` can reference multiple drives (for example, `C,D,E`).

Also, check the **DoincSetup.log** to confirm successful installation:

1. On the distribution point server, navigate to `\SMS_DP$\Ms.Dsp.Do.Inc.Setup\DoincSetup.log` located at one of the logical drives.
1. Open the file and scroll to the end.
1. Verify that it contains entries similar to the following:

```output
Requesting content from the Delivery Optimization In-Network Cache (DOINC) instance... (Attempt #1)
     Started download of test content from http://localhost/mscomtest/cedtest/r20.gif
     Completed download of test content from http://localhost/mscomtest/cedtest/r20.gif
     Download response
          StatusCode:        OK
          ContentLength:     43
     Successful download of test content from http://localhost/mscomtest/cedtest/r20.gif
     Verifying downloaded content is present in primary disk cache: E:\DOINC-E77D08D0-5FEA-4315-8C95-10D359D59294\download.windowsupdate.com\mscomtest\cedtest\r20.gif.full (
Found
)
Completed VerifyCacheNodeSetup.ps1
Delivery Optimization In-Network Cache (DOINC) Install succeeded
```

## Log files

- **Application Request Routing (ARR) setup log**: `%temp%\arr_setup.log`
- **Connected Cache server setup log**: `\SMS_DP$\Ms.Dsp.Do.Inc.Setup\DoincSetup.log` on the distribution point and `DistMgr.log` on the site server
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
| 0x00D0000C | Failure: A valid cache drive size percent set or cache drive size in GB must be supplied |
| 0x00D0000D | Failure: A valid cache drive size percent set and cache drive size in GB cannot both be supplied |
| 0x00D0000E | Failure: The number of cache drives specified must match the number of cache drive sizes in GB specified |
| 0x00D0000F | Failure: Could not back up the applicationhost.config file from $AppHostConfig to $AppHostConfigDestinationName |
| 0x00D00010 | Failure: Could not back up the Default Web Site web.config file from $WebsiteConfigFilePath to $WebConfigDestinationName |
| 0x00D00011 | Failure: An exception occurred in Setup.ps1, method SetupFarmAndRewriteRules |
| 0x00D00012 | Failure: An exception occurred in Setup.ps1, method SetupFarmAndRewriteRules (v15 or v20) |
| 0x00D00014 | Failure: An exception occurred in SetupAllowableServerVariables.ps1 |
| 0x00D00015 | Failure: An exception occurred in SetupFirewallRules.ps1 |
| 0x00D00017 | Failure: An exception occurred in SetupARROutboundRules.ps1 |
| 0x00D00018 | Failure: An exception occurred in SetupARRDiskCache.ps1 |
| 0x00D00019 | Failure: An exception occurred in SetupARRProperties.ps1 |
| 0x00D0001A | Failure: An exception occurred in SetupARRHealthProbes.ps1 |
| 0x00D0001B | Failure: An exception occurred in VerifyIISSitesStarted.ps1 |
| 0x00D0001D | Failure: An exception occurred in VerifyCacheNodeSetup.ps1 |
| 0x00D0001E | You can't install Connected Cache if the Default Web Site isn't on port 80 |
| 0x00D0001F | Failure: The cache drive allocation in percentage can't exceed 100, or another Install.ps1 instance is already running |
| 0x00D00020 | Failure: The cache drive allocation in GB can't exceed the drive's free space |
| 0x00D00021 | Failure: The cache drive allocation in percentage must be greater than 0 |
| 0x00D00022 | Failure: The cache drive allocation in GB must be greater than 0 |
| 0x00D00023 | Failure: Connected Cache dependency installation failed |
| 0x00D00024 | Failure: An exception occurred in RegisterScheduledTask_Maintenance |
| 0x00D00025 | Failure: An exception occurred setting up the rewrite rules for HTTPS farm: $FarmName |
| 0x00D00026 | Failure: An exception occurred setting up the rewrite rules for HTTP farm: $FarmName |
| 0x00D00027 | You can't install Connected Cache because dependent software "Application Request Routing (ARR)" failed to install. See the log file located at %temp%\arr_setup.log |
| 0x00D00029 | Connected Cache can't be installed because IIS is still running (iisreset /stop failed to stop IIS) |

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

Connected Cache creates inbound rules using this naming pattern:

- `Doinc_ForwardToFarm_<origin>_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_v15_<origin>_E77D08D0-5FEA-4315-8C95-10D359D59294`
- `Doinc_ForwardToFarm_v20_<origin>_E77D08D0-5FEA-4315-8C95-10D359D59294`

Depending on origin and transport mapping, additional protocol-specific variants can exist with suffixes such as `_HTTP`, `_HTTPS`, or `_HTTP_HTTPS`.

In [KB33247081: Connected Cache update for Microsoft Configuration Manager versions 2409, 2503, 2509 and 2603](../../../../hotfix/2509/33247081.md), inbound rewrite rules are created for these origins:

- `assets.xbox.com`
- `assets1.xboxlive.com`
- `assets2.xboxlive.com`
- `au.b1.download.windowsupdate.com`
- `au.download.windowsupdate.com`
- `b.c2r.ts.cdn.office.net`
- `b1.download.windowsupdate.com`
- `betaswda01-mscdn.download.manage-beta.microsoft.com`
- `betaswda01.download.manage-beta.microsoft.com`
- `betaswdb01-mscdn.download.manage-beta.microsoft.com`
- `betaswdb01.download.manage-beta.microsoft.com`
- `bg.tscdn.m365.static.microsoft`
- `ctldl.windowsupdate.com`
- `d1.xboxlive.com`
- `d2.xboxlive.com`
- `dl.delivery.mp.microsoft.com`
- `dlassets.xboxlive.com`
- `dlassets2.xboxlive.com`
- `download.windowsupdate.com`
- `emdl.ws.microsoft.com`
- `f.c2r.ts.cdn.office.net`
- `fg.tscdn.m365.static.microsoft`
- `installer.teams.static.microsoft`
- `officecdn.microsoft.com`
- `officecdn.microsoft.com.edgesuite.net`
- `onedfswd-mscdn.download.manage-dogfood.microsoft.com`
- `onedfswd.blob.core.windows.net`
- `onedfswd.download.manage-dogfood.microsoft.com`
- `sb.dl.delivery.mp.microsoft.com`
- `sb.teams.static.microsoft`
- `sb.tlu.dl.delivery.mp.microsoft.com`
- `sf.dl.delivery.mp.microsoft.com`
- `sf.teams.static.microsoft`
- `sf.tlu.dl.delivery.mp.microsoft.com`
- `shswda01-mscdn.download.manage-selfhost.microsoft.com`
- `shswda01.download.manage-selfhost.microsoft.com`
- `statics.teams.cdn.office.net`
- `swda01-mscdn.manage.microsoft.com`
- `swda01.manage.microsoft.com`
- `swda02-mscdn.manage.microsoft.com`
- `swda02.manage.microsoft.com`
- `swdb01-mscdn.manage.microsoft.com`
- `swdb01.manage.microsoft.com`
- `swdb02-mscdn.manage.microsoft.com`
- `swdb02.manage.microsoft.com`
- `swdc01-mscdn.manage.microsoft.com`
- `swdc01.manage.microsoft.com`
- `swdc02-mscdn.manage.microsoft.com`
- `swdc02.manage.microsoft.com`
- `swdd01-mscdn.manage.microsoft.com`
- `swdd01.manage.microsoft.com`
- `swdd02-mscdn.manage.microsoft.com`
- `swdd02.manage.microsoft.com`
- `swdin01-mscdn.manage.microsoft.com`
- `swdin01.manage.microsoft.com`
- `swdin02-mscdn.manage.microsoft.com`
- `swdin02.manage.microsoft.com`
- `swdsw01-mscdn.manage.microsoft.com`
- `swdsw01.manage.microsoft.com`
- `swdsw02-mscdn.manage.microsoft.com`
- `swdsw02.manage.microsoft.com`
- `tlu.dl.delivery.mp.microsoft.com`
- `xvcb1.xboxlive.com`
- `xvcb2.xboxlive.com`
- `xvcf1.xboxlive.com`
- `xvcf2.xboxlive.com`

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

[Microsoft Connected Cache with Configuration Manager](../../../plan-design/hierarchy/microsoft-connected-cache.md)
