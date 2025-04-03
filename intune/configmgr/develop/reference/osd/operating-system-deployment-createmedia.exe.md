---
title: OS deployment CreateMedia.exe
titleSuffix: Configuration Manager
description: Create OS deployment media from the command-line or through a script.
ms.date: 02/16/2022
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# OS deployment CreateMedia.exe

Use `CreateMedia.exe` binary to create media from the command-line or through a script.  

## Requirements  

- Install the Configuration Manager console on the computer used to create media from the command-line or a script.  

- Run `CreateMedia.exe` with required parameters from the folder: `%SMS_ADMIN_UI_PATH%`  

- All content referenced by the selected type of media needs to be on one of the distribution points identified on the command-line:
    - Boot image package
    - OS image package
    - Software packages
    - Drivers
    - Applications referenced by the task sequence
    - A pre-execution package used during media execution

## Additional information

- If you specify it on the command line, you need a valid PKI certificate. When you don't specify a PKI certificate, the site uses a self-signed certificate with a default expiration date. The default is one year from the current date and time, unless you specify the dates as additional parameters.  

- You need the following objects and associated package IDs:
    - Task sequence
    - Boot image
    - OS image
    - Pre-execution package

- Task sequence variables used to specify the management point on the command line.  

    - For dynamic media:  

        `"SMSTSLocationMPs= http://server1.contoso.net*http://server2.contoso.net"`

        > [!Note]
        > `*` is a separator symbol.  

    - For static based media:  

        `"SMSTSMP= http://server.contoso.net"`

        > [!Important]
        > Correctly specify whether the prefix is `http://` or `https://`  

- When you run the `CreateMedia.exe` program, it immediately returns to the command prompt. View the `CreateTsMedia.log` file to monitor progress.  

- Command-line parameters aren't case sensitive.  

## Parameters for boot media  

|**Parameter**|**Value**|**Comment**|  
|-------------------|---------------|-----------------|  
|`/K:`|`mylabel`|Label used to specify the boot media type|  
|`/P:`|`server.contoso.net`|FQDN of SMS Provider|  
|`/S:`|`MCM`|Configuration Manager site code|  
|`/C:`|`"Username=Administrator,Domain=MyDomain,Password=password"`|Optional credentials|  
|`/D:`|`server1.contoso.net; server2.contoso.net`|One or more distribution point FQDN names, separated by a semicolon|  
|`/L:`|`Configuration Manager`|Media text label|  
|`/E:`|`MCM00009`|Optional pre-execution package ID|  
|`/G:`|`cmd.exe`|Optional pre-execution command-line|  
|`/Y:`|`4BootIt^`|Optional media password|  
|`/R:`|`c:\cert\certificate.file`|Optional certificate file path|  
|`/W:`|`qY249^i5we5X`|Certificate file password|  
|`/U:`|`true` or `false`|Unknown machine support|  
|`/J:`|`true` or `false`|Internet client|  
|`/Z:`|`true` or `false`|User interaction|  
|`/1:`|Long integer; long integer|SS certificate start time (HIGH;LOW)|  
|`/2:`|Long integer; long integer|SS certificate expire time (HIGH;LOW)|  
|`/5:`|`0`|UDA setting, integer as a string|  
|`/X:`|`SMSTSMP=server.contoso.net`|Task sequence variable, in the form name=value|  
|`/B:`|`MCM00002`|Boot image ID|  
|`/T:`|`CD`, `UDF`, or `UDF+FORMAT`|Media type|  
|`/F:`|`c:\file.iso`|Path for capture media file|  

## Parameters for capture media  

|Parameter|Example value|Comment|  
|-------------------|---------------|-----------------|  
|`/K:`|`mylabel`|Label used to specify the capture media type|  
|`/P:`|`server.contoso.net`|FQDN of SMS Provider|  
|`/S:`|`MCM`|Configuration Manager site code|  
|`/C:`|`"Username=Administrator,Domain=MyDomain,Password=password"`|Optional credentials|  
|`/D:`|`server1.contoso.net; server2.contoso.net`|One or more distribution point FQDN names, separated by a semicolon|  
|`/L:`|`Configuration Manager`|Media text label|  
|`/B:`|`MCM00002`|Boot image ID|  
|`/T:`|`CD`, `UDF`, or `UDF+FORMAT`|Media type|  
|`/F:`|`c:\file.iso`|Path for capture media file|  

## Parameters for stand-alone media  

|Parameter|Example value|Comment|  
|-------------------|---------------|-----------------|  
|`/K:`|`mylabel`|Label used to specify the standalone media type|  
|`/P:`|`server.contoso.net`|FQDN of SMS Provider|  
|`/S:`|`MCM`|Configuration Manager site code|  
|`/C:`|`"Username=Administrator,Domain=MyDomain,Password=password"`|Optional credentials|  
|`/D:`|`server1.contoso.net; server2.contoso.net`|One or more distribution point FQDN names, separated by a semicolon|  
|`/L:`|`Configuration Manager`|Media text label|  
|`/E:`|`MCM00009`|Optional pre-execution package ID|  
|`/G:`|`cmd.exe`|Optional pre-execution command-line|  
|`/Y:`|`4BootIt^`|Optional media password|  
|`/A:`|`MCM00007`|Task sequence ID|  
|`/T:`|`CD`, `UDF`, or `UDF+FORMAT`|Media type|  
|`/Z:`|`true` or `false`|User interaction|  
|`/X:`|`SMSTSMP=server.contoso.net`|Task sequence variable, in the form name=value|  
|`/M:`|`4GB`|Size of selected media, units|  
|`/F:`|`c:\file.iso`|Path for standalone media file|  

## Parameters for pre-staged media  

|Parameter|Example value|Comment|  
|-------------------|---------------|-----------------|  
|`/K:`|`mylabel`|Label used to specify the prestaged media type|  
|`/P:`|`server.contoso.net`|FQDN of SMS Provider|  
|`/S:`|`MCM`|Configuration Manager site code|  
|`/C:`|`"Username=Administrator,Domain=MyDomain,Password=password"`|Optional credentials|  
|`/D:`|`server1.contoso.net; server2.contoso.net`|One or more distribution point FQDN names, separated by a semicolon|  
|`/L:`|`Configuration Manager`|Media text label|  
|`/3:`|`1.10.1.10`|Optional version text|  
|`/4:`|`OEM scenario image`|Optional description text|  
|`/E:`|`MCM00009`|Optional pre-execution package ID|  
|`/G:`|`cmd.exe`|Optional pre-execution command-line|  
|`/Y:`|`4BootIt^`|Optional media password|  
|`/R:`|`c:\cert\certificate.file`|Optional certificate file path|  
|`/W:`|`qY249^i5we5X`|Certificate file password|  
|`/U:`|`true` or `false`|Unknown machine support|  
|`/J:`|`true` or `false`|Internet client|  
|`/Z:`|`true` or `false`|User interaction|  
|`/1:`|Long integer; long integer|SS certificate start time (HIGH;LOW)|  
|`/2:`|Long integer; long integer|SS certificate expire time (HIGH;LOW)|  
|`/5:`|`0`|UDA setting, integer as a string|  
|`/X:`|`SMSTSMP=server.contoso.net`|Task sequence variable, in the form name=value|  
|`/B:`|`MCM00002`|Boot image ID|  
|`/O:`|`MCM00006`|OS image ID|  
|`/I:`|`1`|OS image index number|  
|`/T:`|`HD`|Media type|  
|`/F:`|`c:\file.iso`|Path for prestaged media file|  
