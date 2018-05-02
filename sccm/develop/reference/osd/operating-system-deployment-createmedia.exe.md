---
title: "OS Deployment CreateMedia.exe"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 41417409-6c56-4099-bafc-3700c6761de3
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# Operating System Deployment CreateMedia.exe
Use `CreateMedia.exe` binary to create media from the command-line or through a script that was implemented by System Center Configuration Manager Operating System Deployment.  

## Requirements  

1.  Install the administrator console on the computer used to create media from the command-line or a script.  

2.  Run `CreateMedia.exe` with required parameters from the folder: `%SMS_ADMIN_UI_PATH%`  

3.  All content referenced by the selected type of media needs to be on one of the distribution points identified on the command-line.  Examples are: boot image package, operating system image package, software packages, drivers or applications referenced by the task sequence, or a pre-execution package used during media execution.  

## Additional information necessary to create media  

1.  A valid PKI certificate (if specified on the command-line). When a PKI certificate is not specified, a self-signed certificate will be used with default expiration date in one year from current day-time unless the dates are specified as additional parameters.  

2.  Task Sequence package IDs, boot image, operating system image, pre-execution package required to create stand-alone media.  

3.  You should know package ID of the Task Sequence you will be using in stand-alone media creation, of the boot image, the operating system image, or the pre-execution package.  

4.  Names of task sequence variables used to specify the Management Point on command-line.  

    -   For dynamic media:  

         ``"SMSTSLocationMPs= http://server1.contoso.net*http://server2.contoso.net"``

         Note: * is a separator symbol.  

    -   For static based media:  

         ``"SMSTSMP= http://server.contoso.net"``

         Note: It is important to correctly specify whether the prefix is http:// or https://  

5.  Running the `CreateMedia.exe` program returns to the command prompt immediately. View the `CreateTsMedia.log` file to monitor progress.  

6.  Command-line switches are not case sensitive.  

## Parameters for boot media  

|**Parameter**|**Value**|**Comment**|  
|-------------------|---------------|-----------------|  
|**/K:    (or /k: )**|Boot|Label used to specify the boot media type|  
|**/P:    (or /p: )**|\<FQDN of Configuration Manager Provider>|example: “server.contoso.net��?|  
|**/S:    (or /s: )**|\< Configuration Manager site code>|example:  “MCM��?|  
|**/C:**|Credentials|optional, example: "Username=Administrator,Domain=MyDomain,Password=password"|  
|**/D:  (or /d: )**|\<FQDN of one or more distribution points >|list of distribution point FQDN names separated by a comma,<br /><br /> example: “server1.contoso.net, server2.contoso.net��?|  
|**/L: (or /l: )**|\<Media Text Label>|optional, example: “Configuration Manager��?|  
|**/E: (or /e: )**|\<Pre-exec Package ID>|optional, example: “MCM00009��?|  
|**/G: (or /g: )**|\<Pre-exec command-line>|optional, example: “notepad license.txt��?|  
|**/Y: (or /y: )**|\<Password>|optional, example: “Password1��?|  
|**/R: (or /r: )**|\<Certificate file path>|Optional, example: “c:\cert\certificate.file��?|  
|**/W**: (or /w: )|\<Certificate file password>|example: “Password2��?|  
|**/U: (or /u: )**|\<Unknown machine support>|true or false|  
|**/J: (or /j:)**|\<Internet client>|true or false|  
|**/Z: (or /z: )**|\<User interaction>|true or false|  
|**/1:**|\<[SS certificate start time] HIGH;LOW >|Long integer; long integer|  
|**/2:**|\<[SS certificate expire time] HIGH;LOW >|Long integer; long integer|  
|**/5:**|\<UDA setting>|Integer as a string, example: 0|  
|**/X: (or /x: )**|\<TS variable>|task sequence variable, in the form name=value<br /><br /> i.e. SMSTSMP= server.contoso.net|  
|**/B: (or /b: )**|\<Boot Image ID>|i.e. “MCM00002��?|  
|**/T: (or /t: )**|\<Media Type>|One of:  “CD��?, “UDF��?, “UDF+FORMAT��?|  
|**/F: (or /f: )**|\<Destination of media file>|Path for media ISO file|  

## Parameters for capture media  

|**Parameter**|**Value**|**Comment**|  
|-------------------|---------------|-----------------|  
|**/K:    (or /k: )**|capture|Label used to specify the capture media type|  
|**/P:    (or /p: )**|\<FQDN of Configuration Manager Provider>|example: “server.contoso.net��?|  
|**/S:    (or /s: )**|\< Configuration Manager site code>|example:  “MCM��?|  
|**/C:**|Credentials|optional, example: "Username=Administrator,Domain=MyDomain,Password=password"|  
|**/D:  (or /d: )**|\<FQDN of one or more distribution points>|list of distribution point FQDN names separated by a comma,<br /><br /> example: “server1.contoso.net, server2.contoso.net��?|  
|**/L: (or /l: )**|\<Media Text Label>|optional, example: “Configuration Manager��?|  
|**/B: (or /b: )**|\<Boot Image ID>|i.e. “MCM00002��?|  
|**/T: (or /t: )**|\<Media Type>|One of:  “CD��?, “UDF��?, “UDF+FORMAT��?|  
|**/F: (or /f: )**|\<Destination of media file>|Path for boot ISO file|  

## Parameters for stand-alone media  

|**Parameter**|**Value**|**Comment**|  
|-------------------|---------------|-----------------|  
|**/K:    (or /k: )**|full|Label used to specify the full media type|  
|**/P:    (or /p: )**|\<FQDN of Configuration Manager Provider>|example: “server.contoso.net��?|  
|**/S:    (or /s: )**|\< Configuration Manager site code>|example:  “MCM��?|  
|**/C:**|Credentials|optional, example: "Username=Administrator,Domain=MyDomain,Password=password"|  
|**/D:  (or /d: )**|\<FQDN of one or more distribution points>|list of distribution point FQDN names separated by a comma,<br /><br /> example: “server1.contoso.net, server2.contoso.net��?|  
|**/L: (or /l: )**|\<Media Text Label>|optional, example: “Configuration Manager��?|  
|**/E: (or /e: )**|\<Pre-exec Package ID>|optional, example: “MCM00009��?|  
|**/G: (or /g: )**|\<Pre-exec command-line>|optional, example: “cmd.exe��?|  
|**/Y: (or /y: )**|\<Password>|optional, example: “Password1��?|  
|**/A: (or /a: )**|\<ID of task sequence>|i.e. “MCM00007��?|  
|**/T: (or /t: )**|\<Media Type>|One of:  “CD��?, “UDF��?, “UDF+FORMAT��?|  
|**/Z: (or /z: )**|\<User interaction>|true or false|  
|**/X: (or /x: )**|\<TS variable>|task sequence variable, in the form name=value<br /><br /> i.e. var1=test|  
|**/T: (or /t: )**|\<Media Type>|One of:  “CD��?, “UDF��?, “UDF+FORMAT��?|  
|**/M: (or /m: )**|\<Media size>|Size of selected media, units|  
|**/F: (or /f: )**|\<Destination of media file>|Path for media ISO file|  

## Parameters for pre-staged media  

|**Parameter**|**Value**|**Comment**|  
|-------------------|---------------|-----------------|  
|**/K:    (or /k: )**|prestaged|Label used to specify the prestaged media type|  
|**/P:    (or /p: )**|\< FQDN of Configuration Manager Provider >|example: “server.contoso.net��?|  
|**/S:    (or /s: )**|\<Configuration Manager site code>|example:  “MCM��?|  
|**/C:**||optional, example: L"Username=Administrator,Domain=MyDomain,Password=password"|  
|**/D:  (or /d: )**|\<One or more distribution point FQDN names>|list of distribution point FQDN names separated by a semicolon,<br /><br /> example: “server1.contoso.net; server2.contoso.net��?|  
|**/L: (or /l: )**|\<CREATED BY text>|optional example: “Bob��?|  
|**/3:**|\<Version text>|optional i.e. 1.10.1.10|  
|**/4:**|\<Description text>|optional i.e. “OEM scenario image��?|  
|**/L: (or /l: )**|\<Media Text Label>|optional, example: “Configuration Manager��?|  
|**/E: (or /e: )**|\<Pre-exec Package ID>|optional, example: “MCM00009��?|  
|**/G: (or /g: )**|\<Pre-exec command-line>|optional, example: “cmd.exe��?|  
|**/Y: (or /y: )**|\<Password>|optional, example: “Password1��?|  
|**/R: (or /r: )**|\<Certificate file path>|Optional, example: “c:\cert\certificate.file��?|  
|**/W**: (or /w: )|\<Certificate file password>|example: “Password2��?|  
|**/U: (or /u: )**|\<Unknown machine support>|true or false|  
|**/J:**|\<Internet client>|true or false|  
|**/Z: (or /z: )**|\<User interaction>|true or false|  
|**/1:**|\<[SS certificate start time] HIGH;LOW >|Long integer; long integer|  
|**/2:**|\<[SS certificate expire time] HIGH;LOW >|Long integer; long integer|  
|**/5:**|\<UDA setting>|Integer as a string, example: 0|  
|**/X: (or /x: )**|\<TS variable>|task sequence variable, in the form name=value<br /><br /> i.e. SMSTSMP=server.contoso.net|  
|**/B: (or /b: )**|\<Boot Image ID>|i.e. “MCM00002��?|  
|**/O: (or /o: )**|\<Operating system image ID>|i.e. “MCM00006��?|  
|**/I: (or /i: )**|\<Operating system image index number>|i.e. “1��?|  
|**/T: (or /t: )**|\<Media Type>|“HD��?|  
|**/F: (or /f: )**|\<destination of media file>|Path for prestaged media file|  

## See Also  
 [Configuration Manager Operating System Deployment](../../../develop/reference/osd/operating-system-deployment-classes.md)
