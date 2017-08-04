---
title: "Client installation properties | Microsoft Docs"
description: "Learn about client installation properties in System Center Configuration Manager."
ms.custom: na
ms.date: 01/04/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c890fd27-7a8c-4f51-bbe2-f9908af1f42b
caps.latest.revision: 15
author: robstackmsft
ms.author: robstack
manager: angrobe
---
# About client installation properties in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Use the System Center Configuration Manager CCMSetup.exe command to manually install the Configuration Manager client.  

##  <a name="aboutCCMSetup"></a> About CCMSetup.exe  
 The CCMSetup.exe command downloads needed files to install the client from a management point or a source location. These files might include:  

-   The Windows Installer package Client.msi that installs the client software.  

-   Microsoft Background Intelligent Transfer Service (BITS) installation files.  

-   Windows Installer installation files.  

-   Updates and fixes for the Configuration Manager client.  

> [!NOTE]  
>  In Configuration Manager, you cannot run the Client.msi file directly.  

 CCMSetup.exe provides [command-line properties](#ccmsetup-exe-command-line-properties) to customize the installation. You can also specify properties to modify the behavior of Client.msi at the CCMSetup.exe command line.  

> [!IMPORTANT]  
>  Specify CCMSetup properties before you specify properties for Client.msi.  

 CCMSetup.exe and its supporting files are located on the Configuration Manager site server in the **Client** folder of the Configuration Manager installation folder. This folder is shared to the network as **&lt;Site Server Name\>\SMS_&lt;Site Code\>\Client**.  

 At the command prompt, the CCMSetup.exe command uses the following format:  

 `CCMSetup.exe [&lt;Ccmsetup properties\>] [&lt;client.msi setup properties>]`  

 Example:  

 'CCMSetup.exe /mp:SMSMP01 /logon SMSSITECODE=S01 FSP=SMSFSP01`  

 This example does the following:  

-   Specifies the management point named SMSMP01 to request a list of distribution points to download the client installation files.  

-   Specifies that installation should stop if a version of the client already exists on the computer.  

-   Instructs client.msi to assign the client to the site code S01.  

-   Instructs client.msi to use the fallback status point named SMSFP01.  

> [!NOTE]  
>  If a property contains spaces, surround it with quotation marks.  


> [!IMPORTANT]  
>  If you have extended the Active Directory schema for Configuration Manager, many client installation properties are published in Active Directory Domain Services and read automatically by the Configuration Manager client. For a list of the client installation properties published in Active Directory Domain Services, see [About client installation properties published to Active Directory Domain Services in System Center Configuration Manager](about-client-installation-properties-published-to-active-directory-domain-services.md)  

##  CCMSetup.exe Command-Line Properties  

### /?  

Opens the **CCMSetup** dialog box showing command-line properties for ccmsetup.exe.  

Example: **ccmsetup.exe /?**  

### /source:&lt;Path\>  

 Specifies the  file download location. Use a local or UNC path. Files are downloaded using the server message block (SMB) protocol.  To use  **/source**, the Windows user account for client installation must have Read permissions to the location.

> [!NOTE]  
>  You can use the **/source** property multiple times in a command line to specify alternative download locations.  

 Example: **ccmsetup.exe /source:"\\\computer\folder"**  

### /mp:&lt;Computer\>

 Specifies a source management point for computers to connect to so that they can find the nearest distribution point for the installation files. If there are no distribution points or computers cannot download the files from the distribution points after 4 hours, clients download the files from the specified management point.  

> [!IMPORTANT]  
>  This property is used to specify an initial management point for computers to find a download source, and can be any management point in any site. It does not *assign* the client to a management point.   

 Computers download the files over an HTTP or HTTPS connection, depending on the site system role configuration for client connections. The download uses BITS throttling, if configured. If all distribution points and management points are configured for HTTPS client connections only,  verify that the client computer has a valid client certificate.  

You can use the **/mp** command-line property to specify multiple management points so that if the computer fails to connect to the first one, the next is tried, and so on. When you specify multiple management points, separate the values by semicolons.

If the client connects to a management point using HTTPS, typically, you must specify the FQDN, not the computer name. The value must match the management point’s PKI certificate Subject or Subject Alternative Name. Although Configuration Manager supports using a computer name in the certificate for connections on the intranet, as a security best practice, an FQDN is recommended.

Example for when you use the computer name: `ccmsetup.exe /mp:SMSMP01`  

Example for when you use the FQDN: `ccmsetup.exe /mp:smsmp01.contoso.com`  

### /retry:&lt;Minutes\>

The retry interval if CCMSetup.exe fails to download installation files.  CCMSetup continues to retry until it reaches the limit specified in the **downloadtimeout** property.  

Example: `ccmsetup.exe /retry:20`  

### /noservice

Prevents CCMSetup from running as a service, which is the default. When CCMSetup runs as a service, it runs in the context of the Local System account of the computer, which might not have sufficient rights to access required network resources for the installation. With **/noservice**, CCMSetup.exe runs in the context of the user account that you use to start the installation. Also, if you are use a script to run CCMSetup.exe with the **/service** property, CCMSetup.exe exits after the service starts and might not report installation details correctly.   

Example: `ccmsetup.exe /noservice`  

### /service

Specifies that CCMSetup should run as a service that uses the local system account.  

Example: `ccmsetup.exe /service`  

### /uninstall

Specifies that the client software should be uninstalled. For more information, see [How to manage clients in System Center Configuration Manager](../manage/manage-clients.md).  

Example: `ccmsetup.exe /uninstall`  

### /logon

Specifies that the client installation should stop if any version of the  client is already installed.  

Example: `ccmsetup.exe /logon`  

### /forcereboot

 Specifies that CCMSetup should force the client computer to restart if necessary to complete the installation. If this is not specified, CCMSetup exits when a restart is necessary, and then continues after the next manual restart.  

 Example: `CCMSetup.exe /forcereboot`  

### /BITSPriority:&lt;Priority\>

 Specifies the download priority when client installation files are downloaded over an HTTP connection. Possible values are as follows:  

-   FOREGROUND  

-   HIGH  

-   NORMAL  

-   LOW  

 The default value is NORMAL.  

 Example: `ccmsetup.exe /BITSPriority:HIGH`  

### /downloadtimeout:&lt;Minutes\>

The length of time in minutes that CCMSetup attempts to download the  installation files before stopping. The default value is **1440** minutes (1 day).  

Example: `ccmsetup.exe /downloadtimeout:100`  

### /UsePKICert

 When specified, the client uses a PKI certificate that includes client authentication, if available. If a valid certificate cannot be found, the client uses an HTTP connection and a self-signed certificate, which is also the behavior when you don't use this property.

> [!NOTE]  
>  In some scenarios you do not have to specify this property when you are installing a client, and still use a client certificate. These scenarios include installing a client by using client push, and software update point–based client installation. However, you must specify this property whenever you manually install a client and use the **/mp** property to specify a management point that is configured to accept only HTTPS client connections. You also must specify this property when you install a client for Internet-only communication, by using the CCMALWAYSINF=1 property (together with the properties for the Internet-based management point and the site code). For more information about Internet-based client management, see [Considerations for client communications from the Internet or an untrusted forest](../../plan-design/hierarchy/communications-between-endpoints.md#BKMK_clientspan) in  [Communications between endpoints in System Center Configuration Manager](../../plan-design/hierarchy/communications-between-endpoints.md).  

 Example: `CCMSetup.exe /UsePKICert`  

### /NoCRLCheck

 Specifies that a client should not check the certificate revocation list (CRL) when it communicates over HTTPS with a PKI certificate.  

 When not specified, the client checks the CRL before establishing an HTTPS connection.  

 For more information about client CRL checking, see [Planning for PKI certificate revocation](../../plan-design/security/plan-for-security.md#BKMK_PlanningForCRLs) in[Plan for security in System Center Configuration Manager](../../plan-design/security/plan-for-security.md).  

 Example: `CCMSetup.exe /UsePKICert /NoCRLCheck`  

### /config:&lt;configuration file\>

Specifies the name of a text file containing client installation properties.

- If you don't specify the **/noservice** CCMSetup property, this file must be located in the CCMSetup folder, which is %Windir%\\Ccmsetup for 32-bit and 64-bit operating systems.
- If you specify the **/noservice** property, this file must be located in the same folder from which you run CCMSetup.exe.  

Example: `CCMSetup.exe /config:&lt;Configuration File Name.txt\>`  

Use the mobileclienttemplate.tcf file in the &lt;Configuration Manager directory\>\\bin\\&lt;platform\> folder on the site server computer to provide the correct file format. This file also contains comments about the sections and how they are used. Specify the client installation properties in the [Client Install] section, after the following text: **Install=INSTALL=ALL**.  

Example [Client Install] section entry: `Install=INSTALL=ALL SMSSITECODE=ABC SMSCACHESIZE=100`  

### /skipprereq:&lt;filename\>

 Specifies that CCMSetup.exe must not install the specified prerequisite program when the Configuration Manager client is installed. This property supports entering multiple values. Use the semicolon character (;) to separate each value.  


 Examples: `CCMSetup.exe /skipprereq:silverlight.exe` or `CCMSetup.exe /skipprereq:dotnetfx40_client_x86_x64.exe;Silverlight.exe`  

### /forceinstall

 Specify that any existing client will be uninstalled and a new client will be installed.  

### /ExcludeFeatures:&lt;feature\>

Specifies that CCMSetup.exe will not install the specified feature when the client is installed.  

Example: `CCMSetup.exe /ExcludeFeatures:ClientUI` will not install  Software Center on the client.  

> [!NOTE]  
>  For this release, **ClientUI** is the only value supported with the **/ExcludeFeatures** property.  

##  <a name="ccmsetupReturnCodes"></a> CCMSetup.exe return codes  
 The CCMSetup.exe command provides the following return codes completed. To troubleshoot, review the ccmsetup.log file on the client computer for context and additional detail about return codes.  

|Return code|Meaning|  
|-----------------|-------------|  
|0|Success|  
|6|Error|  
|7|Reboot required|  
|8|Setup already running|  
|9|Prerequisite evaluation failure|  
|10|Setup manifest hash validation failure|  

##  <a name="clientMsiProps"></a> Client.msi Properties  
 The following properties can modify the installation behavior of client.msi. If you use the client push installation method, you can also specify the properties in the **Client** tab of the **Client Push Installation Properties** dialog box.  

### CCMADMINS  

Specifies one or more Windows user accounts or groups to be given access to client settings and policies. This is useful where the Configuration Manager admin does not have local administrative credentials on the client computer. Specify a list of accounts that are separated by semi-colons.  

Example: `CCMSetup.exe CCMADMINS="Domain\Account1;Domain\Group1"`  

### CCMALLOWSILENTREBOOT

Specifies that the computer is allowed to restart following the client installation if required.  

> [!IMPORTANT]  
>  The computer will restart without warning even if a user is logged on.  

Example: **CCMSetup.exe  CCMALLOWSILENTREBOOT**  

### CCMALWAYSINF

 Set to 1 to specify that the client will always be Internet-based and will never connect to the intranet. The client's connection type displays **Always Internet**.  

 This property should be used in conjunction with CCMHOSTNAME, which specifies the FQDN of the Internet-based management point. It should also be used in conjunction with the CCMSetup property /UsePKICert and with the site code.  

 For more information about Internet-based client management, see [Considerations for client communications from the Internet or an untrusted forest](../../plan-design/hierarchy/communications-between-endpoints.md#BKMK_clientspan) in  [Communications between endpoints in System Center Configuration Manager](../../plan-design/hierarchy/communications-between-endpoints.md).  

 Example: `CCMSetup.exe /UsePKICert  CCMALWAYSINF=1 CCMHOSTNAME=SERVER3.CONTOSO.COM SMSSITECODE=ABC`  

### CCMCERTISSUERS

 Specifies the certificate issuers list, which is a list of trusted root certification (CA) certificates that the Configuration Manager site trusts.  

 For more information about the certificate issuers list and how clients use it during the certificate selection process, see [Planning for PKI client certificate selection](../../plan-design/security/plan-for-security.md#BKMK_PlanningForClientCertificateSelection) in [Plan for security in System Center Configuration Manager](../../plan-design/security/plan-for-security.md).  

 This is a case-sensitive match for subject attributes that are in the root CA certificate. Attributes can be separated by a comma (,) or semi-colon (;). Multiple root CA certificates can be specified by using a separator bar. Example:  

 `CCMCERTISSUERS=”CN=Contoso Root CA; OU=Servers; O=Contoso, Ltd; C=US &#124; CN=Litware Corporate Root CA; O=Litware, Inc.”`  

> [!TIP]  
>  Reference the mobileclient.tcf file in the &lt;Configuration Manager directory\>\bin\\&lt;platform\> folder on the site server computer to copy the **CertificateIssuers=&lt;string\>** that is configured for the site.  

### CCMCERTSEL

 Specifies the certificate selection criteria if the client has more than one certificate for HTTPS communication (a valid certificate that includes client authentication capability).  

 You can search for an exact match (use **Subject:**) or a partial match (use **SubjectStr:)** in the Subject Name or Subject Alternative Name. Examples:  

 `CCMCERTSEL="Subject:computer1.contoso.com"` searches for a certificate with an exact match to the computer name "computer1.contoso.com" in the Subject Name or the Subject Alternative Name.  

 `CCMCERTSEL="SubjectStr:contoso.com"` searches for a certificate that contains "contoso.com" in the Subject Name or the Subject Alternative Name.  

 You can also use Object Identifier (OID) or distinguished name attributes in the Subject Name or Subject Alternative Name attributes, for example:  

 `CCMCERTSEL="SubjectAttr:2.5.4.11 = Computers"` searches for the organizational unit attribute expressed as an object identifier, and named Computers.  

 `CCMCERTSEL="SubjectAttr:OU = Computers"` searches for the organizational unit attribute expressed as a distinguished name, and named Computers.  

> [!IMPORTANT]  
>  If you use the Subject Name box, the **Subject:** is case-sensitive, and the  **SubjectStr:** is case-insensitive.  
>   
>  If you use the Subject Alternative Name box, the **Subject:**and the **SubjectStr:** are case-insensitive.  

 The complete list of attributes that you can use for certificate selection is listed in [Supported Attribute Values for the PKI Certificate Selection Criteria](#BKMK_attributevalues).  

 If more than one certificate matches the search, and the property CCMFIRSTCERT has been set to 1, the certificate with the longest validity period is selected.  

### CCMCERTSTORE

 Specifies an alternate certificate store name if the client certificate for HTTPS is not located in the default certificate store of **Personal** in the Computer store.  

 Example: `CCMSetup.exe /UsePKICert CCMCERTSTORE="ConfigMgr"`  

### CCMDEBUGLOGGING

  Enables debug logging. Values can be set to 0 (off, default) or 1 (on). This causes the client to log low-level information for troubleshooting. As a best practice, avoid using this property in production sites because excessive logging can occur, which might make it difficult to find relevant information in the log files. CCMENABLELOGGING must also be set to TRUE to enable debug logging.  

  Example: `CCMSetup.exe CCMDEBUGLOGGING=1`  

### CCMENABLELOGGING

  By default, set to TRUE to enable logging. The log files are stored in the **Logs** folder in the Configuration Manager client installation folder. By default, this folder is %Windir%\CCM\Logs.  

  Example: `CCMSetup.exe CCMENABLELOGGING=TRUE`  

### CCMEVALINTERVAL  

 The frequency at which client health evaluation tool (ccmeval.exe) runs. Can be **1** to **1440** minutes. By default, runs once a day.  

### CCMEVALHOUR

 The hour when the client health evaluation tool (ccmeval.exe) runs,  between **0** (midnight) and **23** (11pm). Runs at midnight by default.  

### CCMFIRSTCERT

 If set to 1, this property specifies that the client should select the PKI certificate with the longest validity period. This setting might be required if you are using Network Access Protection with IPsec enforcement.  

 Example: `CCMSetup.exe /UsePKICert CCMFIRSTCERT=1`  

### CCMHOSTNAME

 Specifies the FQDN of the Internet-based management point, if the client is managed over the Internet.  

 Do not specify this option with the installation property of SMSSITECODE=AUTO. Internet-based clients must be directly assigned to their Internet-based site.  

 Example: `CCMSetup.exe  /UsePKICert/ CCMHOSTNAME="SMSMP01.corp.contoso.com"`  

### CCMHTTPPORT

 Specifies the port that the client should use when communicating over HTTP to site system servers. Set to Port 80 by default.  

 Example: `CCMSetup.exe CCMHTTPPORT=80`  

### CCMHTTPSPORT

Specifies the port that the client should use when communicating over HTTPS to site system servers. Set to Port 443 by default.  

Example: `CCMSetup.exe /UsePKICert CCMHTTPSPORT=443`  

### CCMINSTALLDIR

 Identifies the folder where the Configuration Manager client files are installed, *%Windir%*\CCM by default. Regardless of where these files are installed, the Ccmcore.dll file is always installed in the *%Windir%\System32* folder. Also, on 64-bit operating systems, a copy of the Ccmcore.dll file is always installed in the *%Windir%*\SysWOW64 folder to support 32-bit applications that use the 32-bit version of the Configuration Manager client APIs from the Configuration Manager software developer kit (SDK).  

 Example: `CCMSetup.exe CCMINSTALLDIR="C:\ConfigMgr"`  

### CCMLOGLEVEL

Specifies the level of detail to write to Configuration Manager log files. Specify an integer from 0 to 3, where 0 is the most verbose logging and 3 logs only errors. The default is 1.  

Example: `CCMSetup.exe CCMLOGLEVEL=3`  

### CCMLOGMAXHISTORY

When a Configuration Manager log file reaches 250000 bytes in size (or the value specified by the property CCMLOGMAXSIZE), it is renamed as a backup, and a new log file is created.  

This property specifies how many previous versions of the log file to retain. The default value is 1. If the value is set to 0, no old log files are kept.  

Example: `CCMSetup.exe CCMLOGMAXHISTORY=0`  

### CCMLOGMAXSIZE

The maximum log file size in bytes. When a log grows to the size that is specified, it is renamed as a history file, and a new file is created. This property must be set to at least 10000 bytes. The default value is 250000 bytes.  

Example: `CCMSetup.exe CCMLOGMAXSIZE=300000`  

### DISABLESITEOPT

 If set to TRUE, disables the ability of end users with administrative credentials on the client computer to change the Configuration Manager assigned site in **Configuration Manager** in the client Control Panel.  

 Example: **CCMSetup.exe DISABLESITEOPT=TRUE**  

### DISABLECACHEOPT

If set to TRUE, disables the ability of end users with administrative credentials on the client computer to change the  client cache folder settings for the Configuration Manager client by using Configuration Manager in Control Panel of the client computer.  

Example: `CCMSetup.exe DISABLECACHEOPT=TRUE`  

### DNSSUFFIX

 Specifies a DNS domain for clients to locate management points that are published in DNS. When a management point is located, it informs the client about other management points in the hierarchy. This means that the management point that is located by using DNS publishing does not have to be from the client’s site, but can be any management point in the hierarchy.  

> [!NOTE]  
>  You do not have to specify this property if the client is in the same domain as a published management point. In that case, the client’s domain is automatically used to search DNS for management points.  

 For more information about DNS publishing as a service location method for Configuration Manager clients, see [Service Location and how clients determine their assigned management point](../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#BKMK_Plan_Service_Location) in [Understand how clients find site resources and services for System Center Configuration Manager](../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md) .  

> [!NOTE]  
>  By default, DNS publishing is not enabled in Configuration Manager.  

 Example: `CCMSetup.exe SMSSITECODE=ABC DNSSUFFIX=contoso.com`  

### FSP

Specifies the fallback status point that receives and processes state messages sent by Configuration Manager client computers.  

For more information about the fallback status point, see [Determine if you need a fallback status point](/sccm/core/clients/deploy/plan#determine-if-you-need-a-fallback-status-point).  

Example: `CCMSetup.exe FSP=SMSFP01`  

### IGNOREAPPVVERSIONCHECK

 Specifies that the presence of the minimum required version of Microsoft Application Virtualization (App-V) is not checked before the client is installed.  

> [!IMPORTANT]  
>  If you install the Configuration Manager client without installing App-V, you cannot deploy virtual applications.  

 Example: `CCMSetup.exe IGNOREAPPVVERSIONCHECK=TRUE`  

### NOTIFYONLY

Specifies that client status will report, but not remediate problems that are found with the client.  

Example: `CCMSetup.exe NOTIFYONLY=TRUE`  

For more information, see [How to configure client status in System Center Configuration Manager](configure-client-status.md).  

### RESETKEYINFORMATION

 If a Configuration Manager client has the wrong Configuration Manager trusted root key and cannot contact a trusted management point to receive the new trusted root key, you must manually remove the old trusted root key by using this property. This situation may occur when you move a client from one site hierarchy to another. This property applies to clients that use HTTP and HTTPS client communication.  

 Example: `CCMSetup.exe RESETKEYINFORMATION=TRUE`  

### SITEREASSIGN

Enables automatic site reassignment for client upgrades when used with [SMSSITECODE](#smssitecode)=AUTO.

Example: `CCMSetup.exe SMSSITECODE=AUTO SITEREASSIGN=TRUE`

### SMSCACHEDIR

Specifies the location of the client cache folder on the client computer, which stores temporary files. By default, the location is *%Windir \ccmcache*.  

Example: `CCMSetup.exe SMSCACHEDIR="C:\Temp"`  

This property can be used in conjunction with the SMSCACHEFLAGS property to control the client cache folder location.  

Example: `CCMSetup.exe SMSCACHEDIR=Cache SMSCACHEFLAGS=MAXDRIVE` installs the client cache folder on the largest available client disk drive.  

### SMSCACHEFLAGS

Specifies further installation details for the client cache folder. You can use SMSCACHEFLAGS properties individually or in combination, separated by semicolons. If this property is not specified, the client cache folder is installed according to the SMSCACHEDIR property, the folder is not compressed, and the SMSCACHESIZE value is used as the size in MB of the folder.  

This setting is ignored when you upgrade an existing client.  

Properties:  

-   PERCENTDISKSPACE: Specifies the folder size as a percentage of the total disk space. If you specify this property, you must also specify the property SMSCACHESIZE as the percentage value to use.  

-   PERCENTFREEDISKSPACE: Specifies the folder size as a percentage of the free disk space. If you specify this property, you must also specify the property SMSCACHESIZE as the percentage value to use. For example, if the disk has 10 MB free and SMSCACHESIZE is specified as 50, the folder size is set to 5 MB. You cannot use this property with the PERCENTDISKSPACE property.  

-   MAXDRIVE: Specifies that the folder should be installed on the largest available disk. This value will be ignored if a path has been specified with the SMSCACHEDIR property.  

-   MAXDRIVESPACE: Specifies that the folder should be installed on the disk drive that has the most free space. This value will be ignored if a path has been specified with the SMSCACHEDIR property.  

-   NTFSONLY: Specifies that the folder can be installed only on NTFS disk drives. This value will be ignored if a path has been specified with the SMSCACHEDIR property.  

-   COMPRESS: Specifies that the folder should be stoed in a compressed form.  

-   FAILIFNOSPACE: Specifies that the client software should be removed if there is insufficient space to install the folder.  

Example: `CCMSetup.exe SMSCACHEFLAGS=NTFSONLY;COMPRESS`  


### SMSCACHESIZE

> [!IMPORTANT]
> Beginning with Configuration Manager version 1606, new client settings are available for specifying the client cache folder size. The addition of those client settings effectively replaces using SMSCACHESIZE as a client.msi property to specify the size of the client cache. For more information, see the [client settings for cache size](about-client-settings.md#client-cache-settings).  

For 1602 and earlier, SMSCACHESIZE specifies the size of the client cache folder in megabyte (MB) or as a percentage when used with the PERCENTDISKSPACE or PERCENTFREEDISKSPACE property. If this property is not set, the folder defaults to a maximum size of 5120 MB. The lowest value that you can specify is 1 MB.  

> [!NOTE]  
>  If a new package that must be downloaded would cause the folder to exceed the maximum size, and if the folder cannot be purged to make sufficient space available, the package download fails, and the program or application will not run.  

This setting is ignored when you upgrade an existing client and when the client downloads software updates.  

Example: `CCMSetup.exe SMSCACHESIZE=100`  

> [!NOTE]  
>  If you reinstall a client, you cannot use the SMSCACHESIZE or SMSCACHEFLAGS installation properties to set the cache size to be smaller than it was previously. If you try to do this, your value is ignored and the cache size is automatically set to the size it was previously.  

### SMSCONFIGSOURCE

Specifies the location and order that the Configuration Manager Installer checks for configuration settings. The property is a string containing one or more characters, each defining a specific configuration source. Use the character values R, P, M, and U, alone or in combination:  

-   R: Check for configuration settings in the registry.  

   For more information, see [information about storing client installation properties in the registry.](https://technet.microsoft.com/library/gg712298.aspx#BKMK_Provision).  

-   P: Check for configuration settings in the installation properties provided at the command prompt.  

-   M: Check for existing settings when upgrading an older client with the Configuration Manager client software.  

-   U: Upgrade the installed client to a newer version (and use  the assigned site code).  

 By default, the client installation uses `PU` to check first the installation properties and then the existing settings.  

 Example: `CCMSetup.exe SMSCONFIGSOURCE=RP`  

### SMSDIRECTORYLOOKUP

 Specifies whether the client can use Windows Internet Name Service (WINS) to find a management point that accepts HTTP connections. Clients use this method when they cannot find a management point in Active Directory Domain Services or in DNS.  

 This property doesn't affect whether the client uses WINS for name resolution.  

 You can configure two different modes for this property:  

-   NOWINS: This is the most secure setting for this property and prevents clients from finding a management point in WINS .  When you use this setting, clients must have an alternative method to locate a management point on the intranet, such as Active Directory Domain Services or by using DNS publishing.  

-   WINSSECURE (default): In this mode, a client that uses HTTP communication can use WINS to find a management point. However, the client must have a copy of the trusted root key before it can successfully connect to the management point. For more information, see [Planning for the Trusted Root Key](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK) in [Plan for security in System Center Configuration Manager](../../plan-design/security/plan-for-security.md).  


 Example: `CCMSetup.exe SMSDIRECTORYLOOKUP=NOWINS`  

### SMSMP

Specifies an initial management point for the Configuration Manager client to use.  

> [!IMPORTANT]  
>  If the management point only accepts client connections over HTTPS, you must prefix the management point name with https://.  

Example: `CCMSetup.exe SMSMP=smsmp01.contoso.com`

Example: `CCMSetup.exe SMSMP=https://smsmp01.contoso.com`  

### SMSPUBLICROOTKEY

 Specifies the Configuration Manager trusted root key when it cannot be retrieved from Active Directory Domain Services. This property applies to clients that use HTTP and HTTPS client communication. For more information, see [Planning for the Trusted Root Key](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK) in [Plan for security in System Center Configuration Manager](../../plan-design/security/plan-for-security.md).  

 Example: `CCMSetup.exe SMSPUBLICROOTKEY=&lt;key\>`  

### SMSROOTKEYPATH

 Used to reinstall the Configuration Manager trusted root key. Specifies the full path and file name to a file containing the trusted root key. This property applies to clients that use HTTP and HTTPS client communication. For more information, see [Planning for the Trusted Root Key](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK) in [Plan for security in System Center Configuration Manager](../../plan-design/security/plan-for-security.md).  

 Example: 'CCMSetup.exe SMSROOTKEYPATH=&lt;Full path and filename\>`  

### SMSSIGNCERT

 Specifies the full path and .cer file name of the exported self-signed certificate on the site server.  

 This certificate is stored in the **SMS** certificate store and has the Subject name **Site Server** and the friendly name **Site Server Signing Certificate**.  

 Example: **CCMSetup.exe /UsePKICert SMSSIGNCERT=&lt;Full path and file name\>**  

### SMSSITECODE

 Specifies the Configuration Manager site to assign the Configuration Manager client to. This can either be a three-character site code or the word AUTO. If AUTO is specified, or if this property is not specified, the client attempts to determine its Configuration Manager site assignment from Active Directory Domain Services or from a specified management point. To enable AUTO for client upgrades, you must also set [SITEREASSIGN](#sitereassign) to TRUE.    

> [!NOTE]  
>  Do not use AUTO if you also specify the Internet-based management point (CCMHOSTNAME). In that case, you must directly assign the client to its site.  

 Example: `CCMSetup.exe SMSSITECODE=XZY`  

##  <a name="BKMK_attributevalues"></a> Supported Attribute Values for the PKI Certificate Selection Criteria  
 Configuration Manager supports the following attribute values for the PKI certificate selection criteria:  

|OID attribute|Distinguished Name attribute|Attribute definition|  
|-------------------|----------------------------------|--------------------------|  
|0.9.2342.19200300.100.1.25|DC|Domain component|  
|1.2.840.113549.1.9.1|E or E-mail|Email address|  
|2.5.4.3|CN|Common name|  
|2.5.4.4|SN|Subject name|  
|2.5.4.5|SERIALNUMBER|Serial number|  
|2.5.4.6|C|Country code|  
|2.5.4.7|L|Locality|  
|2.5.4.8|S or ST|State or province name|  
|2.5.4.9|STREET|Street address|  
|2.5.4.10|O|Organization name|  
|2.5.4.11|OU|Organizational unit|  
|2.5.4.12|T or Title|Title|  
|2.5.4.42|G or GN or GivenName|Given name|  
|2.5.4.43|I or Initials|Initials|  
|2.5.29.17|(no value)|Subject Alternative Name|  
