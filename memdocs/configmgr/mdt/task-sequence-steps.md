---
title: Toolkit reference - Microsoft Deployment Toolkit (MDT) Task Sequence Steps
titleSuffix: Microsoft Deployment Toolkit
description: Reference details for Microsoft Deployment Toolkit (MDT) Task Sequence Steps
ms.date: 09/09/2016
ms.subservice: mdt
ms.service: configuration-manager
ms.topic: conceptual
author: BalaDelli
ms.author: baladell
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: frankroj,mstewart,aaroncz
---

# Task Sequence Steps

*Task sequences* are created by the Task Sequence Editor and consist of a combined series of steps that are designed to complete an action. Task sequences can operate across a computer restart and can be configured to automate tasks on a computer without requiring user intervention. In addition, you can add task sequence steps to a task sequence group, which helps keep similar task sequence steps together for better organization and error control.

Each task sequence step performs a specific task, such as validating that the target computer is capable of receiving the deployment image, storing user data in a safe location, deploying an image to a target computer, and restoring saved user data. These task sequence steps accomplish their tasks by using utilities and scripts provided with MDT or by the deployment team. Use this reference to help determine the correct task sequence groups and task sequence steps to configure the deployment process and the valid properties and options to use.

The following information is provided for each task sequence group and step:

- **Name**. The name of the task sequence group or step

- **Description**. A description of the purpose of the task sequence group or step and any pertinent information regarding its customization

- **Properties**. Indicates the valid configuration properties that you can specify for the task sequence group or step that define how the task is performed

- **Options**. Indicates the valid configuration options that you can specify for the task sequence group or step that define if and when the task is performed and what is considered a successful exit code from the task

  For more information about the Task Sequence Editor, see [Operating System Deployment: Task Sequence Editor](../osd/understand/introduction-to-operating-system-deployment.md).

## Common Properties and Options for Task Sequence Step Types

Each task sequence group and step has configurable settings on the **Properties** and **Options** tabs that are common to all task sequence groups and steps. These common settings are briefly described in the following sections.

### Common Properties

Table 1 shows the settings that are available on the **Properties** tab of each task sequence step. For more information about the **Properties** tab for a particular task sequence step, see the topic that corresponds to the step later in this reference.

> [!NOTE]
>
> The task sequence step types listed here are those that are available in the Deployment Workbench. Additional task sequence step types might be available when configuring task sequences using Microsoft System Center 2012 R2 Configuration Manager.

#### Table 1. Settings Available on the Properties Tab

|**Name**|**Description**|**Group**|**Step**|
|-|-|-|-|
|**Type**|A read-only value that indicates the task sequence group or step type. The type will be set to one of these values:<br><br> - Apply Network Settings<br><br> - Authorize DHCP<br><br> - Capture Network Settings<br><br> - Configure ADDS<br><br> - Configure DHCP<br><br> - Configure DNS<br><br> - Enable BitLocker<br><br> - Format and Partition Disk<br><br> - Gather<br><br> - Group<br><br> - Inject Drivers<br><br> - Install Application<br><br> - Install Operating System<br><br> - Install Roles and Features<br><br> - Install Updates Offline<br><br> - Recover From Domain Join Failure<br><br> - Restart computer<br><br> - Run Command Line<br><br> - Validate|-|-|
|**Name**|A user-defined name that should allow easy identification and differentiation from other task sequence steps.|-|-|
|**Description**|A user-defined description that should make the task sequence step requirements and tasks easily understandable.|-|-|

### Common Options

Table 2 shows the settings that are available on the Options tab of a task sequence step. For more information about the Options tab, see [Task Sequence Options Tab](../osd/understand/task-sequence-steps.md#common-settings).

#### Table 2. Settings Available on the Options Tab

|**Name**|**Description**|**Group**|**Step**|
|-|-|-|-|
|**Disable this step**|Select this option to disable this task sequence step.|-|-|
|**Success codes**|Exit codes of the utility associated with this task sequence step that indicate that the step has finished successfully.||-|
|**Continue on error** |Select this option to allow the Task Sequencer to process additional task sequence steps if a failure occurs.|-|-|
|**Conditional statements**|One or more conditions that limit the running of this task sequence group or step. These conditional are based on the following:<br><br> - File properties<br><br> - Folder properties<br><br> Operating system version:<br><br> - Is a certain architecture<br><br> - Is a certain version<br><br> - Query Windows Management Instrumentation (WMI)<br><br> Registry setting:<br><br> - Exists<br><br> - Does not exist<br><br> - Equals<br><br> - Does not equal<br><br> - Greater than<br><br> - Greater than or equals<br><br> - Less than<br><br> - Less than or equals<br><br> - Installed software<br><br> Task sequence variable:<br><br> - Exists<br><br> - Equals<br><br> - Does not equal<br><br> - Greater than<br><br> - Greater than or equals<br><br> - Less than<br><br> - Less than or equals<br><br> These conditions can be grouped using **IF** statements that test all conditions, any condition, or no condition that evaluates as True.|-|-|

> [!NOTE]
>
> Additional conditional statements might be available when using Configuration Manager to configure task sequence steps.

## Specific Properties and Settings for Task Sequence Step Types

Some properties and parameters of each task sequence step type are unique to that type. Each type with unique properties and settings is shown in the following sections with its unique task sequence step properties and settings.

### Apply Network Settings

This task sequence step configures the network adapter on the target computer. For more information about what script accomplishes this task and which properties are used, see [ZTINICConfig.wsf](scripts.md#ztinicconfigwsf).

 The unique properties and settings for the **Apply Network Settings** task sequence step type are:

#### Properties

|**Name**|**Value**|
|-|-|
|**Type**|Apply Network Settings|

#### Settings

|**Name**|**Value**|
|-|-|
|**Name**|The name to be assigned to the network connection.|
|**Obtain an IP address automatically**|When selected, Dynamic Host Configuration Protocol (DHCP) is used to obtain the required Internet Protocol (IP) configuration settings for the network connection. This is the default selection.|
|**Use the following IP address**|When selected, you can provide one or more IP address and subnet mask combinations in addition to gateways that will be assigned to the network connection.|
|**Obtain a Domain Name System (DNS) server automatically**|When selected, DHCP is used to obtain the required IP configuration settings for the network connection. This is the default selection.|
|**Use the following DNS servers**|When selected, you can provide one or more DNS server IP addresses that will be assigned to the network connection.|
|**DNS Suffix**|The DNS suffix that will be applied to all network connections that use TCP/IP.|
|**Register this connection's address in DNS**|Specifies that the computer will attempt dynamic registration of the IP addresses (through DNS) of this connection with the full computer name of this computer.|
|**Use this connection's DNS suffix in DNS registration**|Specifies whether DNS dynamic update is used to register the IP addresses and the connection-specific domain name of this connection.|
|**WINS server addresses**|You can provide one or more Windows Internet Naming Service (WINS) server IP addresses that will be assigned to the network connection.|
|**Enable LMHOSTS lookup**|Specifies whether a local area network (LAN) Manager Hosts (LMHOSTS) file for network basic input/output system (NetBIOS) name resolution is used.|
|**Default**|Specifies whether this network connection obtains the setting to enable or disable NetBIOS over TCP/IP (NetBT) from a DHCP server. This is the default selection.|
|**Enable NetBIOS over TCP/IP**|Specifies that this network connection uses NetBT and WINS.|
|**Disable NetBIOS over TCP/IP**|Specifies that this network connection does not use NetBT and WINS.|

### Authorize DHCP

This task sequence step authorizes the target computer as a DHCP server. For more information about which script accomplishes this task and which properties you use, see [ZTIAuthorizeDHCP.wsf](scripts.md#ztiauthorizedhcpwsf).

 The unique properties and settings for the **Authorize DHCP** task sequence step type are:

#### Properties

|**Name**|**Description**|
|-|-|
|**Type**|Set this read-only type to **Authorize DHCP Server**.|

#### Settings

|**Name**|**Description**|
|-|-|
|**Name**|**Description**|
|**Account**|A user account that is a member of the Enterprise Admins group, to be used when authorizing DHCP for the target computer.|

### Capture Network Settings

This task sequence step gathers the network adapter settings from the target computer. For more information about which script accomplishes this task and which properties you use, see [ZTINICConfig.wsf](scripts.md#ztinicconfigwsf).

 The unique properties and settings for the **Capture Network Settings** task sequence step type are:

#### Properties

|**Name**|**Description**|
|-|-|
|**Name**|**Description**|
|**Type**|Set this read-only type to **Capture Network Settings**.|

#### Settings

|**Name**|**Description**|
|-|-|
|None|None|

### Configure ADDS

This task sequence step configures the target computer as an Active Directory&reg; Domain Services (AD DS) domain controller. For more information about the settings listed in the following tables and which this task sequence step can configure, see the Microsoft Help and Support article, [How to use unattended mode to install and remove Active Directory Domain Services on Windows Server 2008-based domain controllers](/troubleshoot/windows-server/identity/syntax-build-answer-files-unattended-installation-ad-ds).

 The unique properties and settings for the **Configure ADDS** task sequence step type are:

#### Properties

|**Name**|**Description**|
|-|-|
|**Type**|Set this read-only type to **Configure ADDS**.|

#### Settings

|**Name**|**Description**|
|-|-|
|Create|Specifies the configuration set that will be used to configure the target computer. The configuration sets are:<br><br> - **New domain controller replica**. Creates an additional domain controller in an existing AD DS domain<br><br> - **New read-only domain controller (RODC) replica**. Creates an RODC<br><br> - **New domain in existing forest**. Creates a domain in an existing AD DS forest<br><br> - **New domain tree in existing forest**. Creates a new tree in an existing AD DS forest<br><br> - **New forest**. Creates a new AD DS forest|
|**Domain DNS name**|The DNS name of the new or existing domain.|
|**Domain NetBIOS name**|The NetBIOS name of the new child domain, child domain tree, or forest that pre-AD DS clients use to access the domain. This name must be unique on the network.|
|**DNS name**|The DNS name of the child domain or domain tree.|
|**Replication source domain controller**|The name of the domain controller from which to source AD DS on new replica or backup domain controller upgrade installations. If no value is supplied, the closest domain controller from the domain being replicated will be selected by default.|
|**Account**|The account to be used to perform the configuration.|
|**Recovery (safe mode) password**|The password for the offline Administrator account that is used in AD DS Repair mode.|
|**Install DNS if not already present**|When selected, DNS will be installed if it has not already been installed.|
|**Make this domain controller a global catalog (GC) server**|Specifies whether the replica will also be a GC server. When selected, the target computer will be configured as a GC server if the replication source domain controller is a GC server.|
|**Wait for critical replication only**|When selected, this setting specifies that only critical replication is sourced during the replication phase of Dcpromo. Noncritical replication resumes when the computer restarts as a domain controller.|
|**Forest functional level**|Specifies the functional level for a new forest. Available options are:<br><br> - Windows Server 2003<br><br> - Windows Server 2008<br><br> - Windows Server 2008 R2|
|**Domain functional level**|Specifies the functional level for a new domain. Available options are:<br><br> - Windows Server 2003<br><br> - Windows Server 2008<br><br> - Windows Server 2008 R2|
|**Database**|Fully qualified, non-Universal Naming Convention (UNC) directory on a hard disk of the local computer that will host the AD DS database (NTDS.dit). If the directory exists, it must be empty. If it does not exist, it will be created. Free disk space on the logical drive selected must be 200 megabytes (MB) and possibly larger when rounding errors are encountered and to accommodate all objects in the domain. For best performance, the directory should be located on a dedicated hard disk.|
|**Log files**|Fully qualified, non-UNC directory on a hard disk on the local computer to host the AD DS log files. If the directory exists, it must be empty. If it does not exist, it will be created.|
|**SYSVOL**|Fully qualified, non-UNC directory on a hard disk of the local computer that will host the AD DS System Volume (SYSVOL) files. If the directory exists, it must be empty. If it does not exist, it will be created. The directory must be located on a partition that is formatted with the NTFS version 5.0 file system. For best performance, the directory should be located on a different physical hard disk than the operating system.|
|**Site name**|The value of an existing AD DS site on which to locate the new domain controller. If not specified, an appropriate site will be selected. This option only applies to the new tree in a new forest scenario. For all other scenarios, a site will be selected using the current site and subnet configuration of the forest.|

### Configure DHCP

This task sequence step configures the DHCP server service on the target computer. For more information about which script accomplishes this task and which properties you use, see [ZTIConfigureDHCP.wsf](scripts.md#zticonfiguredhcpwsf).

 The unique properties and settings for the **Configure DHCP** task sequence step type are:

#### Properties

|**Name**|**Description**|
|-|-|
|**Type**|Set this read-only type to **Configure DHCP Server**.|

#### Settings

|**Name**|**Description**|
|-|-|
|**Name**|Configure DHCP|
|Scope Details|These options apply to any client computers that obtain a lease within that particular scope. Configured scope option values always apply to all computers obtaining a lease in a given scope unless they are overridden by options assigned to class or client reservation.<br><br> Within the **Scope Details** setting, the following sub-settings are configurable:<br><br> - **Scope Name**. A user-definable name<br><br> - **Start IP address**. The starting IP address for the scope<br><br> - **End IP address**. The ending IP address for the scope<br><br> - **Subnet mask**. The subnet mask of the client subnet<br><br> - **Lease duration for DHCP clients**. The duration that the DHCP lease is valid for the client<br><br> - **Description**. A description of the scope<br><br> - **Exclude IP address range, Start IP address**. The starting IP address for the range of IP addresses that are to be excluded from the scope<br><br> -                                 **Exclude IP address range, End IP address**. The ending IP address for the range of IP addresses that are to be excluded from the scope<br><br> - **003 Router**. A list of IP addresses for routers on the client subnet<br><br> - **006 DNS Servers**. A list of IP addresses for DNS name servers available to the client<br><br> - **015 DNS Domain Name**. The domain name that the DHCP client should use when resolving unqualified domain names with DNS<br><br> -                                 **044 WINS/NBNS Servers**. Lists the IP addresses for NetBIOS name servers (NBNSes) on the network<br><br> - **046 WINS/NBT Node Type**. Configures the client node type for NetBT clients<br><br> - **060 PXE Client**. The address used for Pre-Boot Execution Environment (PXE) client bootstrap code|
|Server Options|These options apply globally for all scopes and classes defined at each DHCP server and for any clients that a DHCP server services. Configured server option values always apply unless they are overridden by options assigned to other scope, class, or client reservation.<br><br> Within the **Server Options** setting, the following sub-settings are configurable:<br><br> - **003 Router**. A list of IP addresses for routers on the client subnet<br><br> - **006 DNS Servers**. A list of IP addresses for DNS name servers available to the client<br><br> - **015 DNS Domain Name**. The domain name that the DHCP client should use when resolving unqualified domain names with the DNS<br><br> - **044 WINS/NBNS Servers**. Lists the IP addresses for NBNSes on the network<br><br> -                                 **046 WINS/NBT Node Type**. Configures the client node type for NetBT clients<br><br> - **060 PXE Client**. The address used for PXE client bootstrap code|

### Configure DNS

This task sequence step configures DNS on the target computer. For more information about which script accomplishes this task and which properties you use, see [ZTIConfigureDNS.wsf](scripts.md#zticonfigurednswsf).

 The unique properties and settings for the **Configure DNS** task sequence step type are:

#### Properties

|**Name**|**Description**|
|-|-|
|**Type**|Set this read-only type to **Configure DNS Server**.|

#### Settings

|**Name**|**Description**|
|-|-|
|**Name**|Configure DNS|
|Zones|Within the **Scope Details** setting, the following sub-settings are configurable:<br><br> -                                 **DNS zone name**. A user-definable name<br><br> - Type. The type of DNS zone to be created<br><br> - **Replication**. Specifies the replication scheme used to share information among DNS servers<br><br> - **Zone file name**. The zone's DNS database file<br><br> -                                 **Dynamic updates**. Enables DNS client computers to register and dynamically update their resource records with a DNS server whenever changes occur<br><br> -                                 **Scavenge stale resource records**. Removes stale resource records|
|Server Properties|Within the Server Properties setting, the following sub-settings are configurable:<br><br> -                                 **Disable recursion**. Specifies that the DNS server will not perform recursion on any query<br><br> - **BIND secondaries**. Specifies whether to use fast transfer format to transfer a zone to DNS servers running legacy Berkeley Internet Name Domain (BIND) implementations<br><br> - **Fail on load if bad data**. Specifies the DNS server should parse files strictly<br><br> -                                 **Enable round robin**. Specifies the DNS server should use the round robin mechanism to rotate and reorder a list of resource records if multiple resource records exist of the same type exist for a query answer<br><br> - **Enable netmask ordering**. Specifies whether the DNS server should reorder resource records within the same resource record set in its response to a query based on the IP address of the source of the query<br><br> - **Secure cache against pollution**. Specifies whether the DNS server will attempt to clean up responses to avoid cache pollution<br><br> - **Name checking**. Configures the name-checking method to be used|

> [!NOTE]
>
> The **Configure DNS** task sequence step uses the Dnscmd tool, which is included in Windows Support Tools, to configure DNS. Be sure that Windows Support Tools is installed before running the **Configure DNS** task sequence step.

> [!NOTE]
>
> For more information about these server properties, see [Dnscmd](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/cc772069(v=ws.11)).

### Enable BitLocker

This task sequence step configures BitLocker&reg; Drive Encryption on the target computer. For more information about this step type, see [Enable BitLocker](../osd/understand/task-sequence-steps.md#enable-bitlocker).

 The unique properties and settings for the **Enable BitLocker** task sequence step type are:

#### Properties

|**Name**|**Description**|
|-|-|
|**Type**|Set this read-only type to **Enable BitLocker**.|

#### Settings

|**Name**|**Description**|
|-|-|
|**Current operating system drive**|When selected, the operating system drive will be configured. This is the default selection.|
|**Specific drive**|When selected, the specified drive will be configured.|
|**TPM only**|When selected, the Trusted Platform Module (TPM) is required. This is the default selection.|
|**Startup key on USB only**|When selected, a startup key is required on the specified USB drive.|
|**TPM and startup key on USB**|When selected, the TPM is required in addition to a startup key on the specified USB drive.|
|**In Active Directory**|When selected, the recovery key is stored in AD DS. This is the default selection.|
|**Do not create a recovery key**|When selected, the recovery key is not created. Using this option is not recommended.|
|**Wait for BitLocker to complete**|When selected, this step will not finish until after BitLocker has finished processing all drives.|

### Execute Runbook

This task sequence step runs Microsoft System Center 2012 Orchestrator runbooks on the target computer. An Orchestrator *runbook* is the sequence of activities that orchestrate actions on computers and networks. You can initiate Orchestrator runbooks in MDT using this task sequence step type.

> [!NOTE]
>
> This task sequence step is not included any MDT task sequence templates. You must add this task sequence step to any task sequences you create.

 The unique properties and settings for the **Execute Runbook** task sequence step type are:

#### Properties

|**Name**|**Description**|
|-|-|
|**Type**|Set this read-only type to **Execute Runbook**.|
|**Name**|The name of the task sequence step, which should reflect the name of the runbook being run.|
|**Description**|Informative text that provides additional information about the task sequence step|

#### Settings

|                       **Name**                       |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               **Description**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
|------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|               **Orchestrator Server**                | Type the URL for the Orchestrator web service, which includes the server name. The Orchestrator web service can use either Hypertext Transfer Protocol (HTTP) or HTTP over Secure Sockets Layer (HTTPS). The Orchestrator web service defaults to port 81.<br><br> The Orchestrator web service supports multiple runbook servers. By default, a runbook can run on any runbook server. A runbook can be configured to specify which runbook servers should be used to run the runbook.<br><br> Note:<br><br> The Orchestrator web service supports the ability to run a runbook on a specific runbook server. This feature is not supported in MDT.<br><br> Specify the URL in any of the following formats:<br><br> - ***servername***. When using this format, the URL defaults to:<br><br> `https://<servername>:81/Orchestrator2012/Orchestrator.svc`<br><br> - ***servername:port***. When using this format, the URL defaults to:<br><br> `https://<servername:port>/Orchestrator2012/Orchestrator.svc.`<br><br> - **https://*servername:port**<em>. When using this format, the URL defaults to:<br><br> `https://<servername:port>/Orchestrator2012/Orchestrator.svc.`<br><br> - **https://</em>servername:port**<em>. When using this format, the URL defaults to:<br><br> `https://<servername:port>/Orchestrator2012/Orchestrator.svc.`<br><br> - *</em>https://*servername:port*/Orchestrator2012/Orchestrator.svc**. When using this format, MDT assumes that you are providing the fully qualified URL, because the value ends with .svc.<br><br> -                                 **https://<em>servername:port</em>/Orchestrator2012/Orchestrator.svc**. When using this format, MDT assumes that you are providing the fully qualified URL, because the value ends with .svc. |
|                     **Runbook**                      |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              Select **Browse**, and then select the name of the Orchestrator runbook that this task sequence should run.<br><br> Note:<br><br> To successfully browse for Orchestrator runbooks, install the ADO.NET Data Services Update for .NET Framework 3.5 SP1 for Windows 7 and Windows Server 2008 R2.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
|     **Automatically provide runbook parameters**     |                                                                                                                                                                                                                                                                                                                                                                         Select this option to automatically provide the Orchestrator runbook input parameter values( which assumes that the runbook parameter values are task sequence variables). For example, if a runbook has an input parameter named **OSDComputerName**, then the **OSDComputerName** task sequence variable value is passed to the runbook.<br><br> Note:<br><br> This option works only for input parameters that are valid task sequence variable names and do not contain spaces or other special characters. Although spaces and other special characters are supported as Orchestrator parameter names, they are not valid task sequence variable names. If you need to pass values to parameters with spaces or other special characters, use the **Specify explicit runbook parameters** option.<br><br> The other option is **Specify explicit runbook parameters**.<br><br> Note:<br><br> The values provided for the runbook input parameters to the Orchestrator web service are formatted as XML. Passing values that contain data that is or resembles XML-formatted data may cause errors.                                                                                                                                                                                                                                                                                                                                                                          |
|       **Specify explicit  runbook parameters**       |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                Select this option to explicitly provide the Orchestrator runbook input parameters.<br><br> You must configure the following settings for each input parameter that the Orchestrator runbook requires:<br><br> -                                 **Name**. This is the name of the input runbook parameter.<br><br> Note:<br><br> If you change the parameters for an existing Orchestrator runbook, you need to browse (reselect) for the runbook again, because MDT only retrieves the parameter list when initially adding the Orchestrator runbook.<br><br> - **Value**. This can be a constant or a variable, such as a task sequence variable or an environment variable. For example, you can specify a value of **%OSDComputerName%**, which will pass the value of the **OSDComputerName** task sequence variable to the runbook input parameter.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| **Wait for the runbook to finish before continuing** |                                                                                                                                                                                                                                                                                                                                                                                                                                                       This check box controls whether the task sequence step will wait for the runbook to finish before proceeding to the next task sequence step.<br><br> If this check box is:<br><br> - **Selected**, then the task sequence step will wait for the runbook to finish before proceeding on to the next task sequence step.<br><br> When this check box is selected, the task sequence step will poll the Orchestrator web service for the runbook to finish. The amount of time between polls starts at 1 second, then increases to 2, 4, 8, 16, 32, and 64 seconds between each poll. Once the amount of time reaches 64 seconds, the task sequence step continues to poll every 64 seconds.<br><br> - **Cleared**, then the task sequence step will not wait for the runbook to finish before proceeding to the next task sequence step.<br><br> Note:<br><br> This check box must be selected if the runbook returns output parameters.                                                                                                                                                                                                                                                                                                                                                                                                                                                        |

### Format and Partition Disk

This task sequence step partitions and formats disks on the target computer. For more information about this step type, see [Format and Partition Disk](../osd/understand/task-sequence-steps.md#BKMK_FormatandPartitionDisk).

 The unique properties and settings for the **Format and Partition Disk** task sequence step type are:

#### Properties

|**Name**|**Description**|
|-|-|
|**Type**|Set this read-only type to **Format and Partition Disk**.|

#### Settings

|**Name**|**Description**|
|-|-|
|**Disk number**|The physical number of the disk to be configured.|
|**Disk type**|The type of drive to be created. Values are:<br><br> -                                 **Standard (MBR)** (Master Boot Record)<br><br> - **GPT** (GUID [globally unique identifier] Partition Table).<br><br> The default selection is **Standard (MBR)**.|
|**Volume**|Within the **Volume** setting, the following sub-settings are configurable:<br><br> - Partition **Name**. A user-definable name.<br><br> - **Partition Type.** Values vary by disk type:<br><br> - MBR: **Primary** only<br><br> - GPT: **Primary**, **EFI**, or **MSR**<br><br> - **Use a percentage of remaining space.**<br><br> -                                 **Use specific drive size.** Values are in increments of 1 MB or 1 gigabyte (GB).<br><br> -                                 **Make this a boot partition.**<br><br> -                                 **File System.** Values are **NTFS** or **FAT32**.<br><br> - **Quick Format.** When selected, a quick format is performed.<br><br> - **Variable.** The drive letter that was assigned to this newly configured partition.|

> [!NOTE]
>
> When using the CustomSettings.ini file to specify the hard disk and partition configurations, only the first hard disk and first two partitions will be configured. Edit ZTIGather.xml to configure additional hard disks or partitions.

### Gather

This task sequence step gathers data and processing rules for the target computer. The unique properties and settings for the **Gather** task sequence step type are:

#### Properties

|**Name**|**Description**|
|-|-|
|**Type**|Set this read\-only type to **Gather**.|

#### Settings

|**Name**|**Description**|
|-|-|
|**Gather only local data**|When selected, this step processes only the properties contained in the ZTIGather.xml file.|
|**Gather local data and process rules**|When selected, this step processes the properties contained in the ZTIGather.xml file and the properties contained in the file that the Rules file specifies. This is the default selection.|
|**Rules file**|The name of the Rules file to process. If left blank, the task sequence step attempts to locate and process the CustomSettings.ini file.|

> [!NOTE]
>
> This task sequence step is natively available in System Center 2012 R2 Configuration Manager as **Set Dynamic Variables**in the General group.

### Inject Drivers

This task sequence step injects drivers that have been configured for deployment to the target computer. The unique properties and settings for the **Inject Drivers** task sequence step type are:

#### Properties

|**Name**|**Description**|
|-|-|
|**Type**|Set this read\-only type to **Inject Drivers**.|

#### Settings

|**Name**|**Description**|
|-|-|
|**Install only matching drivers**|Injects only the drivers that the target computer requires and that match what is available in Out\-of\-Box Drivers|
|**Install all drivers**|Installs all drivers|
|**Selection profile**|Installs all drivers in the selected profile|

### Install Application

This task sequence step installs applications on the target computer. For more information about this step type, see [Install Software](../osd/understand/task-sequence-steps.md#BKMK_InstallSoftwareUpdates).

 The unique properties and settings for the **Install Application** task sequence step type are:

#### Properties

|**Name**|**Description**|
|-|-|
|**Type**|Set this read\-only type to **Install Application**.|

#### Settings

|**Name**|**Description**|
|-|-|
|**Install multiple applications**|Install mandatory applications that the **MandatoryApplications** property has specified and optional applications that the **Applications** property has specified. These properties are configured by rules or are specified during the Deployment Wizard interview process. This is the default selection.|
|**Install a single application**|The specific application to install. You select the application from a drop\-down list that consists of applications that have been configured in the Applications node of the Deployment Workbench.|
|**Success codes**|A space\-delimited list of application installation exit codes that should be used when determining the successful installation of applications.|

### Install Operating System

This task sequence step installs an operating system on the target computer. MDT can deploy Windows 8.1, Windows 8, Windows 7, Windows Server 2012 R2, Windows Server 2012, and Windows Server 2008 R2 using:

- **setup.exe**. This method is the traditional method used, initiated by running setup.exe from the installation media. MDT uses setup.exe by default.

- **imagex.exe**. This method installs the operating system image using imagex.exe with the **\/apply** option. MDT uses this method when the setup.exe method cannot be used \(i.e., it falls back to using imagex.exe\).

  You can control which of these methods is used by using the **ForceApplyFallback** property, which also affects which operating system task sequences are listed in the Deployment Wizard for a specific processor architecture boot image. For more information, see the [ForceApplyFallback](properties.md#forceapplyfallback) property.

  The unique properties and settings for the **Install Operating System** task sequence step type are:

#### Properties

|**Name**|**Description**|
|-|-|
|**Type**|Set this read\-only type to **Install Operating System**.|

#### Settings

|**Name**|**Description**|
|-|-|
|**Operating system to install**|The name of the operating system to be installed on the target computer. You select the operating system from a drop\-down list compiled from operating systems that have been configured in the Operating Systems node of the Deployment Workbench.|
|**Disk**|The disk on which to install the operating system.|
|**Partition**|The partition on which to install the operating system.|

### Install Roles and Features

This task sequence step installs the selected roles and features on the target computer. For more information about which script accomplishes this task and the properties used, see [ZTIOSRole.wsf](scripts.md#ztiosrolewsf).

 The unique properties and settings for the **Install Roles and Features** task sequence step type are:

#### Properties

|**Name**|**Description**|
|-|-|
|**Type**|Set this read\-only type to **Install Roles and Features**.|
|**Description**|Informative text that describes the purpose of the task sequence step.|

#### Settings

|**Name**|**Description**|
|-|-|
|**Select the operating system for which the roles are to be installed**|Select the operating system to be deployed to the target computer.|
|**Select the roles and features that should be installed**|Select one or more roles and features for installation on the target computer.|

### Install Language Packs Offline

This task sequence step installs updates to the image on the target computer after the operating system has been deployed but before the target computer has been restarted. These updates include language packs. For more information about which script accomplishes this task and which properties you use, see [ZTIPatches.wsf](scripts.md#ztipatcheswsf).

 The unique properties and settings for the **Install Language Packs Offline** task sequence step type are:

#### Properties

|**Name**|**Description**|
|-|-|
|**Type**|Set this read\-only type to **Install Updates Offline**.|

#### Settings

|**Name**|**Description**|
|-|-|
|**Package Name**|The name of the language pack package that should be applied to the target computer|

> [!NOTE]
>
> This task sequence step is valid only when using MDT with Configuration Manager.

### Install Language Packs Online

This task sequence step installs language packs to the image on the target computer after the operating system has been deployed and after the target computer has been restarted. For more information about which script accomplishes this task and which properties you use, see [ZTILangPacksOnline.wsf](scripts.md#ztilangpacksonlinewsf).

 The unique properties and settings for the **Install Language Packs Online** task sequence step type are:

#### Properties

|**Name**|**Description**|
|-|-|
|**Type**|Set this read\-only type to **Install Language Packs Online**.|

#### Settings

|**Name**|**Description**|
|-|-|
|**Package Name**|The name of the language pack package that should be applied to the target computer|

> [!NOTE]
>
> This task sequence step is valid only when using MDT with Configuration Manager.

### Install Updates Offline

This task sequence step installs updates to the image on the target computer after the operating system has been deployed but before the target computer has been restarted. These updates include language packs. For more information about which script accomplishes this task and which properties you use, see [ZTIPatches.wsf](scripts.md#ztipatcheswsf).

 The unique properties and settings for the **Install Updates Offline** task sequence step type are:

#### Properties

|**Name**|**Description**|
|-|-|
|**Type**|Set this read\-only type to **Install Updates Offline**.|

#### Settings

|**Name**|**Description**|
|-|-|
|**Selection Profile**|The name of the selection profile that should be applied to the target computer<br><br> Note:<br><br> When using MDT with Configuration Manager, specify the name of the update package that should be applied.|

### Recover from Domain Join Failure

This task sequence step verifies that the target computer has joined a domain. The unique properties and settings for the **Recover from Domain Join Failure** task sequence step type are:

#### Properties

|**Name**|**Description**|
|-|-|
|**Type**|Set this read\-only type to Recover from **Domain Join Failure**.|

#### Settings

|**Name**|**Description**|
|-|-|
|**Auto recover**|The task sequence step attempts to join the target computer to a domain.|
|**Manual recover**|If the target computer fails to join a domain, the task sequence step causes the Task Sequencer to pause, allowing you to attempt to join the target computer to a domain.|
|**No recover**|If the target computer is not able to join a domain, the task sequence fails, stopping the task sequence.|

### Restart computer

This task sequence step restarts the target computer. The unique properties and settings for the **Restart computer** task sequence step type are:

#### Properties

|**Name**|**Description**|
|-|-|
|**Type**|Set this read\-only type to **Restart computer**.|

#### Settings

|**Name**|**Description**|
|-|-|
|**None**|None|

### Run Command Line

This task sequence step runs the specified commands on the target computer. For more information about this step type, see [Run Command Line](../osd/understand/task-sequence-steps.md#BKMK_RunCommandLine).

 The unique properties and settings for the **Run Command Line** task sequence step type are:

#### Properties

|**Name**|**Description**|
|-|-|
|**Type**|Set this read\-only type to **Run Command Line**.|

#### Settings

|**Name**|**Description**|
|-|-|
|**Command Line**|The commands to be run when this task sequence step is processed|
|**Start in**|The starting folder for the application \(The path must be a valid path on the target computer.\)|
|**Run this step as the following account**|Allows specification of user credentials that will be used to run the specified command|
|**Account**|The user credentials that will be used to run the specified command|
|**Load the user's profile**|When selected, loads the user profile for the specified account|

### Run PowerShell Script

This task sequence step runs the specified Windows PowerShell&trade; script on the target computer. For more information about what script accomplishes this task and which properties are used, see [ZTIPowerShell.wsf](scripts.md#ztipowershellwsf).

 The unique properties and settings for the **Run PowerShell Script** task sequence step type are:

#### Properties

|**Name**|**Description**|
|-|-|
|**Type**|Set this read\-only type to **Run PowerShell Script**.|

#### Settings

|**Name**|**Description**|
|-|-|
|**PowerShell script**|The Windows PowerShell script to be run when this task sequence step is processed|
|Parameters|The parameters to be passed to the Windows PowerShell script. These parameters should be specified the same as if you were adding them to the Windows PowerShell script from a command line.<br><br> The parameters provided should be only those parameters the script consumes, not for the Windows PowerShell command line.<br><br> The following example would be a valid value for this setting:<br><br> `-MyParameter1 MyValue1 -MyParameter2 MyValue2`<br><br> The following example would be an invalid value for this setting \(bold items are incorrect\):<br><br> `-nologo -executionpolicy unrestricted -File MyScript.ps1 -MyParameter1 MyValue1 -MyParameter2 MyValue2`<br><br> The previous example is invalid, because the value includes Windows PowerShell command\-line parameters \(**\-nologo** and **-executionpolicy unrestricted**\).|

> [!NOTE]
>
> This task sequence step is natively available in System Center 2012 R2 Configuration Manager as **Run PowerShell Script** in the General group.

### Set Task Sequence Variable

This task sequence step sets the specified task sequence variable to the specified value. For more information about this step type, see [Set Task Sequence Variable](../osd/understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable).

 The unique properties and settings for the **Set Task Sequence Variable** task sequence step type are:

#### Properties

|**Name**|**Description**|
|-|-|
|**Type**|Set this read\-only type to **Set Task Sequence Variable**.|

#### Settings

|**Name**|**Description**|
|-|-|
|**Task Sequence Variable**|The name of the variable to modify|
|**Value**|The value to assign to the specified variable|

### Uninstall Roles and Features

This task sequence step uninstalls the selected roles and features from the target computer. For more information about which script accomplishes this task and the properties used, see [ZTIOSRole.wsf](scripts.md#ztiosrolewsf).

 The unique properties and settings for the **Uninstall Roles and Features** task sequence step type are:

#### Properties

|**Name**|**Description**|
|-|-|
|**Type**|Set this read\-only type to **Uninstall Roles and Features**.|
|**Description**|Informative text that describes the purpose of the task sequence step.|

#### Settings

|**Name**|**Description**|
|-|-|
|**Select the operating system for which the roles are to be installed**|Select the operating system to be deployed to the target computer.|
|**Select the roles and features that should be installed**|Select one or more roles and features for unstallation from the target computer.|

### Validate

This task sequence step verifies that the target computer meets the specified deployment prerequisite conditions. The unique properties and settings for the **Validate** task sequence step type are:

#### Properties

|**Name**|**Description**|
|-|-|
|**Type**|Set this read\-only type to **Validate**.|

#### Settings

|**Name**|**Description**|
|-|-|
|**Ensure minimum memory**|When selected, this step verifies that the amount of memory, in megabytes, installed on the target computer meets or exceeds the amount specified. This is a default selection.|
|**Ensure minimum processor speed**|When selected, this step verifies that the speed of the processor, in megahertz \(MHz\), installed in the target computer meets or exceeds the amount specified. This is a default selection.|
|**Ensure specified image size will fit**|When selected, this step verifies that the amount of free disk space, in megabytes, on the target computer meets or exceeds the amount specified.|
|**Ensure current operating system to be refreshed**|When selected, this step verifies that the operating system installed on the target computer meets the requirement specified. This is a default selection.|

> [!NOTE]
>
> This task sequence step is natively available in System Center 2012 R2 Configuration Manager as **Check Readiness** in the General group.

## Out\-of\-Box Task Sequence Steps

The following task sequence steps are referenced by one or more of the available task sequence templates included with MDT. Each of the following examples lists the preconfigured properties, parameters, and options and can be used as a basis for building custom task sequences.

 Only the task sequence step properties, parameters, and options, and their corresponding values are listed in the examples.

> [!NOTE]
>
> For more information about each task sequence step, see the corresponding topics in [Common Properties and Options for Task Sequence Step Types](#common-properties-and-options-for-task-sequence-step-types) and [Specific Properties and Settings for Task Sequence Step Types](#specific-properties-and-settings-for-task-sequence-step-types).

### Apply Network Settings

This task sequence step configures the network adapter on the target computer. Following is a brief listing of the settings that show how this step was originally configured in one of the MDT task sequence templates. For more information about which script accomplishes this task and which properties are used, see [ZTINICConfig.wsf](scripts.md#ztinicconfigwsf).

 The default configuration of the **Apply Network Settings** task sequence step is:

#### Properties

|**Name**|**Value**|
|-|-|
|**Type**|Apply Network Settings|
|**Name**|Apply Network Settings|
|**Description**|Not specified|

#### Settings

|**Name**|**Value**|
|-|-|
||No parameters are preconfigured for this step. This causes this step, by default, to configure the network adapter to use DHCP.|

#### Options

|**Name**|**Value**|
|-|-|
|**Disable this step**|Not selected|
|**Success codes**|0 3010|
|**Continue on error**|Not selected|
|**Conditional qualifier**|Not specified|

> [!NOTE]
>
> When using the CustomSettings.ini file to specify the network adapter configurations, only the first network adapter will be configured. Edit ZTIGather.xml to configure additional network adapters.

### Apply Patches

This task sequence step installs updates to the image on the target computer after the operating system has been deployed but before the target computer has been restarted. Following is a brief listing of the settings that show how this step was originally configured in one of the MDT task sequence templates. For more information about which script accomplishes this task and which properties you use, see [ZTIPatches.wsf](scripts.md#ztipatcheswsf).

 The default configuration of the **Install Updates Offline** task sequence step is:

#### Properties

|**Name**|**Value**|
|-|-|
|**Type**|Install Updates Offline|
|**Name**|Apply Patches|
|**Description**|Not specified|

#### Settings

|**Name**|**Value**|
|-|-|
|**Selection profile**|The name of the profile used when selecting the patches to install on the target computer|

#### Options

|**Name**|**Value**|
|-|-|
|**Disable this step**|Not selected|
|**Success codes**|0 3010|
|**Continue on error**|Not selected|
|**Conditional qualifier**|Not specified|

### Apply Windows PE

This task sequence step prepares the target computer to start in Windows Preinstallation Environment \(Windows PE\). Following is a brief listing of the settings that show how this step was originally configured in one of the MDT task sequence templates. For more information about which script accomplishes this task and which properties you use, see [LTIApply.wsf](scripts.md#ltiapplywsf).

 The default configuration of the **Apply Windows PE** task sequence step is:

#### Properties

|**Name**|**Value**|
|-|-|
|**Type**|Run Command Line|
|**Name**|Apply Windows PE|
|**Description**|Not specified|

#### Settings

|**Name**|**Value**|
|-|-|
|**Command line**|`cscript.exe "%SCRIPTROOT%\LTIApply.wsf" /PE`|
|**Start in**|Not specified|
|**Run this step as the following account**|Not specified|

#### Options

|**Name**|**Value**|
|-|-|
|**Disable this step**|Not selected|
|**Success codes**|0 3010|
|**Continue on error**|Not selected|
|**Conditional qualifier**|Not specified|

### Backup

This task sequence step backs up the target computer before starting the operating system deployment. Following is a brief listing of the settings that show how this step was originally configured in one of the MDT task sequence templates. For more information about which script accomplishes this task and which properties you use, see [ZTIBackup.wsf](scripts.md#ztibackupwsf).

 The default configuration of the **Backup** task sequence step is:

#### Properties

|**Name**|**Value**|
|-|-|
|**Type**|Run Command Line|
|**Name**|Backup|
|**Description**|Not specified|

#### Settings

|**Name**|**Value**|
|-|-|
|**Command line**|`cscript.exe "%SCRIPTROOT%\ZTIBackup.wsf"`|
|**Start in**|Not specified|
|**Run this step as the following account**|Not specified|

#### Options

|**Name**|**Value**|
|-|-|
|**Disable this step**|Not selected|
|**Success codes**|0 3010|
|**Continue on error**|Not selected|
|**Conditional qualifier**|Not specified|

### Capture Groups

This task sequence step captures group membership of local groups that exist on the target computer. Following is a brief listing of the settings that show how this step was originally configured in one of the MDT task sequence templates. For more information about which script accomplishes this task and which properties you use, see [ZTIGroups.wsf](scripts.md#ztigroupswsf).

 The default configuration of the **Capture Groups** task sequence step is:

#### Properties

|**Name**|**Value**|
|-|-|
|**Type**|Run Command Line|
|**Name**|Capture Groups|
|**Description**|Not specified|

#### Settings

|**Name**|**Value**|
|-|-|
|**Command line**|`cscript.exe "%SCRIPTROOT%\ZTIGroups.wsf" /capture`|
|**Start in**|Not specified.|
|**Run this step as the following account**|Not specified|

#### Options

|**Name**|**Value**|
|-|-|
|**Disable this step**|Not selected|
|**Success codes**|0 3010|
|**Continue on error**|Not selected|
|**Conditional qualifier**|Not specified|

### Capture User State

This task sequence step captures the user state for user profiles that exist on the target computer. Following is a brief listing of the settings that show how this step was originally configured in one of the MDT task sequence templates. For more information about what script accomplishes this task and what properties are used, see [ZTIUserState.wsf]((scripts.md#ztiuserstatewsf). For more information about this step type, see [Capture User State](../osd/deploy-use/create-a-task-sequence-to-capture-and-restore-user-state.md#capture-the-user-state).

 The default configuration of the **Capture User State** task sequence step is:

#### Properties

|**Name**|**Value**|
|-|-|
|**Type**|Run Command Line|
|**Name**|Capture User State|
|**Description**|Not specified|

#### Settings

|**Name**|**Value**|
|-|-|
|**Command line**|`cscript.exe "%SCRIPTROOT%\ZTIUserState.wsf" /capture`|
|**Start in**|Not specified|
|**Run this step as the following account**|Not specified|

#### Options

|**Name**|**Value**|
|-|-|
|**Disable this step**|Not selected|
|**Success codes**|0 3010|
|**Continue on error**|Not selected|
|**Conditional qualifier**|Not specified|

### Check BIOS

This task sequence step checks the basic input\/output system \(BIOS\) of the target computer to ensure that it is compatible with the operating system you are deploying. Following is a brief listing of the settings that show how this step was originally configured in one of the MDT task sequence templates. For more information about which script accomplishes this task and which properties are used, see [ZTIBIOSCheck.wsf]((scripts.md#ztibioscheckwsf).

 The default configuration of the **Check BIOS** task sequence step is:

#### Properties

|**Name**|**Value**|
|-|-|
|**Type**|Run Command Line|
|**Name**|Check BIOS|
|**Description**|Not specified|

#### Settings

|**Name**|**Value**|
|-|-|
|**Command line**|`cscript.exe "%SCRIPTROOT%\ZTIBIOSCheck.wsf"`|
|**Start in**|Not specified|
|**Run this step as the following account**|Not specified|

#### Options

|**Name**|**Value**|
|-|-|
|**Disable this step**|Not selected|
|**Success codes**|0 3010|
|**Continue on error**|Not selected|
|**Conditional qualifier**|Not specified|

### Configure

This task sequence step configures the Unattend.xml file with the required property values that are applicable to the operating system you are deploying to the target computer. Following is a brief listing of the settings that show how this step was originally configured in one of the MDT task sequence templates. For more information about which script accomplishes this task and which properties you use, see [ZTIConfigure.wsf]((scripts.md#zticonfigurewsf).

 The default configuration of the **Configure** task sequence step is:

#### Properties

|**Name**|**Value**|
|-|-|
|**Type**|Run Command Line|
|**Name**|Configure|
|**Description**|Not specified|

#### Settings

|**Name**|**Value**|
|-|-|
|**Command line**|`cscript.exe "%SCRIPTROOT%\ZTIConfigure.wsf"`|
|**Start in**|Not specified|
|**Run this step as the following account**|Not specified|

#### Options

|**Name**|**Value**|
|-|-|
|**Disable this step**|Not selected|
|**Success codes**|0 3010|
|**Continue on error**|Not selected|
|**Conditional qualifier**|Not specified|

### Copy Scripts

This task sequence step copies the deployment scripts used during the deployment processes to a local hard disk on the target computer. Following is a brief listing of the settings that show how this step was originally configured in one of the MDT task sequence templates. For more information about which script accomplishes this task and which properties you use, see [LTICopyScripts.wsf](scripts.md#lticopyscriptswsf).

 The default configuration of the **Copy Scripts** task sequence step is:

#### Properties

|**Name**|**Value**|
|-|-|
|**Type**|Run Command Line|
|**Name**|Copy Scripts|
|**Description**|Not specified|

#### Settings

|**Name**|**Value**|
|-|-|
|**Command line**|`cscript.exe "%SCRIPTROOT%\LTICopyScripts.wsf"`|
|**Start in**|Not specified|
|**Run this step as the following account**|Not specified|

#### Options

|**Name**|**Value**|
|-|-|
|**Disable this step**|Not selected|
|**Success codes**|0 3010|
|**Continue on error**|Not selected|
|**Conditional qualifier**|Not specified|

### Copy Sysprep Files

This task sequence step copies the Sysprep files to the target computer. Following is a brief listing of the settings that show how this step was originally configured in one of the MDT task sequence templates. For more information about which script accomplishes this task and which properties you use, see [LTISysprep.wsf](scripts.md#ltisysprepwsf).

 The default configuration of the **Copy Sysprep Files** task sequence step is:

#### Properties

|**Name**|**Value**|
|-|-|
|**Type**|Run Command Line|
|**Name**|Copy Sysprep Files|
|**Description**|Not specified|

#### Settings

|**Name**|**Value**|
|-|-|
|**Command line**|`cscript.exe "%SCRIPTROOT%\LTISysprep.wsf"`|
|**Start in**|Not specified|
|**Run this step as the following account**|Not specified|

#### Options

|**Name**|**Value**|
|-|-|
|**Disable this step**|Not selected|
|**Success codes**|0 3010|
|**Continue on error**|Not selected|
|**Conditional qualifier**|Not specified|

### Create BitLocker Partition

This task sequence step sets the **BDEInstall** property to True, indicating that BitLocker should be installed on the target computer. The unique properties and settings for the **Create BitLocker Partition** task sequence step type are:

#### Properties

|**Name**|**Value**|
|-|-|
|**Type**|Set Task Sequence Variable|
|**Name**|Create BitLocker Partition|
|**Description**|None|

#### Settings

|**Name**|**Value**|
|-|-|
|**Task Sequence Variable**|BDE Install|
|**Value**|True|

#### Options

|**Name**|**Value**|
|-|-|
|**Disable this step**|Not selected|
|**Success codes**|0 3010|
|**Continue on error**|Not selected|
|**Conditional qualifier**|Not specified|

### Create WIM

This task sequence step creates a backup of the target computer. The unique properties and settings for the **Create WIM** task sequence step type are:

#### Properties

|**Name**|**Value**|
|-|-|
|**Type**|Run Command Line|
|**Name**|Create WIM|
|**Description**|None|

#### Settings

|**Name**|**Value**|
|-|-|
|**Command line**|`cscript.exe "%SCRIPTROOT%\ZTIBackup.wsf"`|
|**Start in**|Not specified|
|**Run this step as the following account**|Not specified|

#### Options

|**Name**|**Value**|
|-|-|
|**Disable this step**|Not selected|
|**Success codes**|0 3010|
|**Continue on error**|Not selected|
|**Conditional qualifier**|Not specified|

### Disable BDE Protectors

If BitLocker is installed on the target computer, this task sequence step disables the BitLocker protectors.

 The unique properties and settings for the **Disable BDE Protectors** task sequence step type are:

#### Properties

|**Name**|**Value**|
|-|-|
|**Type**|Run Command Line|
|**Name**|Disable BDE Protectors|
|**Description**|None|

#### Settings

|**Name**|**Value**|
|-|-|
|**Command line**|`cscript.exe "%SCRIPTROOT%\ZTIDisableBDEProtectors.wsf"`|
|**Start in**|Not specified|
|**Run this step as the following account**|Not specified|

#### Options

|**Name**|**Value**|
|-|-|
|**Disable this step**|Not selected|
|**Success codes**|0 3010|
|**Continue on error**|Not selected|
|**Conditional qualifier**|Not specified|

### Enable BitLocker

This task sequence step enables BitLocker on the target computer. Following is a brief listing of the settings that show how this step was originally configured in one of the MDT task sequence templates. For more information about which script accomplishes this task and what properties are used, see [ZTIBde.wsf](scripts.md#ztibdewsf).

 The default configuration of the **Enable BitLocker** task sequence step is:

#### Properties

|**Name**|**Value**|
|-|-|
|**Type**|Enable BitLocker|
|**Name**|Enable BitLocker|
|**Description**|None|

#### Settings

|**Name**|**Value**|
|-|-|
|**Current operating system drive**|Selected|
|**TPM only**|Selected|
|**Startup key on USB only**|Not selected|
|**TPM and startup key on USB**|Not selected|
|**Specific drive**|Not selected|
|**In Active Directory**|Selected|
|**Do not create a recovery key**|Not selected|
|**Wait for BitLocker to complete**|Not selected|

#### Options

|**Name**|**Value**|
|-|-|
|**Disable this step**|Not selected|
|**Success codes**|0 3010|
|**Continue on error**|Not selected|
|**Conditional qualifier**|**BdeInstallSuppress** does not equal YES|

### Enable OEM Disk Configuration

This task sequence step sets the **DeploymentType**property to **NEWCOMPUTER**, which allows the target computer's disk to be partitioned and formatted.

 The unique properties and settings for the **Enable OEM Disk Configuration** task sequence step type are:

#### Properties

|**Name**|**Value**|
|-|-|
|**Type**|Set Task Sequence Variable |
|**Name**|Enable OEM Disk Configuration|
|**Description**|None|

#### Settings

|**Name**|**Value**|
|-|-|
|**Task Sequence Variable**|DeploymentType|
|**Value**|NEWCOMPUTER|

#### Options

|**Name**|**Value**|
|-|-|
|**Disable this step**|Not selected|
|**Success codes**|0 3010|
|**Continue on error**|Not selected|
|**Conditional qualifier**|Not specified|

### End Phase

This task sequence step ends the current deployment phase and restarts the target computer. Following is a brief listing of the settings that show how this step was originally configured in one of the MDT task sequence templates.

 The default configuration of the **End Phase** task sequence step is:

#### Properties

|**Name**|**Value**|
|-|-|
|**Type**|Restart computer|
|**Name**|End Phase|
|**Description**|Not specified|

#### Settings

|**Name**|**Value**|
|-|-|
|None|None|

#### Options

|**Name**|**Value**|
|-|-|
|**Disable this step**|Not selected|
|**Success codes**|0 3010|
|**Continue on error**|Not selected|
|**Conditional qualifier**|Not specified|

### Execute Sysprep

This task sequence step starts Sysprep on the target computer. Following is a brief listing of the settings that show how this step was originally configured in one of the MDT task sequence templates. For more information about what script accomplishes this task and what properties are used, see [LTISysprep.wsf](scripts.md#ltisysprepwsf).

 The default configuration of the **Execute Sysprep** task sequence step is:

#### Properties

|**Name**|**Value**|
|-|-|
|**Type**|Run Command Line|
|**Name**|Execute Sysprep|
|**Description**|None|

#### Settings

|**Name**|**Value**|
|-|-|
|**Command line**|`cscript.exe "%SCRIPTROOT%\LTISysprep.wsf"`|
|**Start in**|Not specified|
|**Run this step as the following account**|Not specified|

#### Options

|**Name**|**Value**|
|-|-|
|**Disable this step**|Not selected|
|**Success codes**|0 3010|
|**Continue on error**|Not selected|
|**Conditional qualifier**|Not specified|

### Force Diskpart Action

If the C:\\oem.wsf file exists, this task sequence step deletes the C:\\oem.wsf file, which will allow the **Format and Partition Disk** task sequence step to run. Following is a brief listing of the settings that show how this step was originally configured in one of the MDT task sequence templates.

 The default configuration of the **Force Diskpart Action** task sequence step is:

#### Properties

|**Name**|**Value**|
|-|-|
|**Type**|Run Command Line|
|**Name**|Force Diskpart Action|
|**Description**|Not specified|

#### Settings

|**Name**|**Value**|
|-|-|
|**Command line**|`cmd.exe /c if exist c:\oem.wsf del /q c:\oem.wsf`|
|**Start in**|Not specified|
|**Run this step as the following account**|Not specified|

#### Options

|**Name**|**Value**|
|-|-|
|**Disable this step**|Not selected|
|**Success codes**|0.1|
|**Continue on error**|Selected|
|**Conditional qualifier**|None|

### Format and Partition Disk

This task sequence step configures and formats disk partitions on the target computer. Following is a brief listing of the settings that show how this step was originally configured in one of the MDT task sequence templates.

 For more information about what script accomplishes this task and what properties are used, see [ZTIDiskpart.wsf](scripts.md#ztidiskpartwsf).

 The default configuration of the **Format and Partition Disk** task sequence step is:

#### Properties

|**Name**|**Value**|
|-|-|
|**Type**|Format and Partition Disk|
|**Name**|Format and Partition Disk|
|**Description**|Not specified|

#### Settings

|**Name**|**Value**|
|-|-|
|**Disk number**|0|
|**Disk type**|Standard \(MBR\)|
|**Volume**|Within the Volume setting, the following sub\-settings are configured:<br><br> \-                                 **Partition Name**. OSDisk<br><br> \- **Partition Type**. Primary<br><br> \-                                 **Use a percentage of remaining space**. Selected<br><br> \-                                 **Size\(%\)**. 100<br><br> \- **Use specific drive size**. Not selected<br><br> \-                                 **Make this a boot partition**. Selected<br><br> \- **File System**. NTFS<br><br> \- **Quick Format**. Selected<br><br> \- **Variable**. Not specified|

#### Options

|**Name**|**Value**|
|-|-|
|**Disable this step**|Not selected|
|**Success codes**|0 3010|
|**Continue on error**|Not selected|
|**Conditional qualifier**|Not specified|

> [!NOTE]
>
> When using the CustomSettings.ini file to specify the hard disk and partition configurations, only the first hard disk and first two partitions will be configured. Edit ZTIGather.xml to configure additional hard disks or partitions.

### Gather local only

This task sequence step gathers deployment configurations settings from local sources that apply to the target computer. Following is a brief listing of the settings that show how this step was originally configured in one of the MDT task sequence templates.

 For more information about what script accomplishes this task and what properties are used, see [ZTIGather.wsf](scripts.md#ztigatherwsf).

 The default configuration of the **Gather local only** task sequence step is:

#### Properties

|**Name**|**Value**|
|-|-|
|**Type**|Gather|
|**Name**|Gather local only|
|**Description**|Not specified|

#### Settings

|**Name**|**Value**|
|-|-|
|**Gather only local data**|Selected|
|**Gather local data and process rules**|Not selected|
|**Rules file**|Not specified|

#### Options

|**Name**|**Value**|
|-|-|
|**Disable this step**|Not selected|
|**Success codes**|0 3010|
|**Continue on error**|Not selected|
|**Conditional qualifier**|None|

### Generate Application Migration File

This task sequence step generates the ZTIAppXmlGen.xml file, which contains a list of file associations that are installed on the target computer. Following is a brief listing of the settings that show how this step was originally configured in one of the MDT task sequence templates.

 For more information about what script accomplishes this task and what properties are used, see [ZTIAppXmlGen.wsf](scripts.md#ztiappxmlgenwsf).

 The default configuration of the **Generate Application Migration** File task sequence step is:

#### Properties

|**Name**|**Value**|
|-|-|
|**Type**|Run Command Line|
|**Name**|Generate Application Migration File|
|**Description**|Not specified|

#### Settings

|**Name**|**Value**|
|-|-|
|**Command Line**|`cscript.exe "%SCRIPTROOT%\ZTIAppXmlGen.wsf" /capture`|
|**Start in**|Not specified|
|**Run this step as the following account**|Not specified|

#### Options

|**Name**|**Value**|
|-|-|
|**Disable this step**|Not selected|
|**Success codes**|0 3010|
|**Continue on error**|Not selected|
|**Conditional qualifier**|None|

### Inject Drivers

This task sequence step injects drivers that have been configured for deployment to the target computer. Following is a brief listing of the settings that show how this step was originally configured in one of the MDT task sequence templates.

 For more information about what script accomplishes this task and what properties are used, see [ZTIDrivers.wsf](scripts.md#ztidriverswsf).

 The default configuration of the **Inject Drivers** task sequence step is:

#### Properties

|**Name**|**Value**|
|-|-|
|**Type**|Inject Drivers|
|**Name**|Inject Drivers|
|**Description**|Not specified|

#### Settings

|**Name**|**Value**|
|-|-|
|**Install only matching drivers**|Injects only the drivers which are required by the target computer and match with what is available in Out\-of\-Box Drivers|
|**Install all drivers**|Injects all drivers|
|**Selection profile**|Injects drivers which are associated with the selected profile|

#### Options

|**Name**|**Value**|
|-|-|
|**Disable this step**|Not selected|
|**Success codes**|0 3010|
|**Continue on error**|Not selected|
|**Conditional qualifier**|Not specified|

### Install Applications

This task sequence step installs applications on the target computer. Following is a brief listing of the settings that show how this step was originally configured in one of the MDT task sequence templates.

 For more information about what script accomplishes this task and what properties are used, see [ZTIApplications.wsf](scripts.md#ztiapplicationswsf).

 The default configuration of the **Install Applications** task sequence step is:

#### Properties

|**Name**|**Value**|
|-|-|
|**Type**|Install Applications|
|**Name**|Install Applications|
|**Description**|Not specified|

#### Settings

|**Name**|**Value**|
|-|-|
|**Install multiple applications**|Selected|
|**Install a single application**|Not selected|

#### Options

|**Name**|**Value**|
|-|-|
|**Disable this step**|Not selected|
|**Success codes**|0 3010|
|**Continue on error**|Not selected|
|**Conditional qualifier**|Not specified|

### Install Operating System

This task sequence step installs an operating system on the target computer. Following is a brief listing of the settings that show how this step was originally configured in one of the MDT task sequence templates.

 The default configuration of the **Install Operating System** task sequence step is:

#### Properties

|**Name**|**Value**|
|-|-|
|**Type**|Install Operating System|
|**Name**|Install Operating System|
|**Description**|Not specified|

#### Settings

|**Name**|**Value**|
|-|-|
|**Operating system to install**|This value corresponds to the operating system that was selected when the task sequence was created.|
|**Disk**|The disk where the operating system is to be installed.|
|**Partition**|The partition where the operating system is to be installed.|

#### Options

|**Name**|**Value**|
|-|-|
|**Disable this step**|Not selected|
|**Success codes**|0 3010|
|**Continue on error**|Not selected|
|**Conditional qualifier**|Not specified|

### Next Phase

This task sequence step updates the **Phase** property to the next phase in the deployment process. Following is a brief listing of the settings that show how this step was originally configured in one of the MDT task sequence templates.

 For more information about what script accomplishes this task and what properties are used, see [ZTINextPhase.wsf](scripts.md#ztinextphasewsf).

 The default configuration of the **Next Phase** task sequence step is:

#### Properties

|**Name**|**Value**|
|-|-|
|**Type**|Run Command Line|
|**Name**|Next Phase|
|**Description**|Not specified|

#### Settings

|**Name**|**Value**|
|-|-|
|**Command line**|`cscript.exe "%SCRIPTROOT%\ZTINextPhase.wsf"`|
|**Start in**|Not specified|
|**Run this step as the following account**|Not specified|

#### Options

|**Name**|**Value**|
|-|-|
|**Disable this step**|Not selected|
|**Success codes**|0 3010|
|**Continue on error**|Not selected|
|**Conditional qualifier**|Not specified|

### Post\-Apply Cleanup

This task sequence step cleans up unnecessary files after the installation of an image on the target computer. Following is a brief listing of the settings that show how this step was originally configured in one of the MDT task sequence templates.

 For more information about what script accomplishes this task and what properties are used, see [LTIApply.wsf](scripts.md#ltiapplywsf).

 The default configuration of the **Post\-Apply Cleanup** task sequence step is:

#### Properties

|**Name**|**Value**|
|-|-|
|**Type**|Run Command Line|
|**Name**|Post\-Apply Cleanup|
|**Description**|Not specified|

#### Settings

|**Name**|**Value**|
|-|-|
|**Command line**|`cscript.exe "%SCRIPTROOT%\LTIApply.wsf" /post`|
|**Start in**|Not specified|
|**Run this step as the following account**|Not specified|

#### Options

|**Name**|**Value**|
|-|-|
|**Disable this step**|Not selected|
|**Success codes**|0 3010|
|**Continue on error**|Not selected|
|**Conditional qualifier**|Not specified|

### Recover from Domain

This task sequence step will verify the target computer has joined a domain. For more information about which script accomplishes this task and which properties are used, see [ZTIDomainJoin.wsf](scripts.md#ztidomainjoinwsf).

 The unique properties and settings for the Recover from Domain task sequence step type are:

#### Properties

|**Name**|**Description**|
|-|-|
|**Type**|This read\-only type is set to Recover from Domain Join Failure.|

#### Settings

|**Name**|**Description**|
|-|-|
|**Auto recover**|The task sequence step will attempt to join the target computer to a domain.|
|**Manual recover**|If the target computer fails to join a domain, the task sequence step will cause the task sequencer to pause, allowing the user attempts to join the target computer to a domain.|
|**No recover**|If the target computer is not able to join a domain, the task sequence fails, stopping the task sequence.|

### Restart computer

This task sequence step restarts the target computer. Following is a brief listing of the settings that show how this step was originally configured in one of the MDT task sequence templates.

 The default configuration of the **Restart computer** task sequence step is:

#### Properties

|**Name**|**Value**|
|-|-|
|**Type**|Restart computer|
|**Name**|Restart computer|
|**Description**|Not specified|

#### Settings

|**Name**|**Value**|
|-|-|
|None|None|

#### Options

|**Name**|**Value**|
|-|-|
|**Disable this step**|Not selected|
|**Success codes**|0 3010|
|**Continue on error**|Not selected|
|**Conditional qualifier**|Not specified|

### Restore Groups

This task sequence step restores the previously captured group membership of local groups on the target computer. Following is a brief listing of the settings that show how this step was originally configured in one of the MDT task sequence templates.

 For more information about what script accomplishes this task and what properties are used, see [ZTIGroups.wsf](scripts.md#ztigroupswsf).

 The default configuration of the **Restore Groups** task sequence step is:

#### Properties

|**Name**|**Value**|
|-|-|
|**Type**|Run Command Line|
|**Name**|Restore Groups|
|**Description**|Not specified|

#### Settings

|**Name**|**Value**|
|-|-|
|**Command line**|`cscript.exe "%SCRIPTROOT%\ZTIGroups.wsf" /restore`|
|**Start in**|Not specified|
|**Run this step as the following account**|Not specified|

#### Options

|**Name**|**Value**|
|-|-|
|**Disable this step**|Not selected|
|**Success codes**|0 3010|
|**Continue on error**|Not selected|
|**Conditional qualifier**|If all conditions are true:<br><br> \- **DoCapture** does not equal YES<br><br> \-                                 **DoCapture** does not equal PREPARE|

### Restore User State

This task sequence step restores previously captured user state to the target computer. Following is a brief listing of the settings that show how this step was originally configured in one of the MDT task sequence templates.

 For more information about what script accomplishes this task and what properties are used, see [ZTIUserState.wsf]((scripts.md#ztiuserstatewsf).

 For more information about this step type, see [Restore User State](../osd/deploy-use/create-a-task-sequence-to-capture-and-restore-user-state.md#restore-the-user-state).

 The default configuration of the **Restore User State** task sequence step is:

#### Properties

|**Name**|**Value**|
|-|-|
|**Type**|Run Command Line|
|**Name**|Restore User State|
|**Description**|Not specified|

#### Settings

|**Name**|**Value**|
|-|-|
|**Command Line**|`cscript.exe "%SCRIPTROOT%\ZTIUserState.wsf" /restore`|
|**Start in**|Not specified|
|**Run this step as the following account**|Not specified|

#### Options

|**Name**|**Value**|
|-|-|
|**Disable this step**|Not selected|
|**Success codes**|0 3010|
|**Continue on error**|Not selected|
|**Conditional qualifier**|If all conditions are true:<br><br> \- If **DoCapture** does not equal YES<br><br> \- If **DoCapture** does not equal PREPARE|

### Set Image Build

This task sequence step sets the **ImageBuild** property to the value contained in **OSCurrentVersion**. Following is a brief listing of the settings that show how this step was originally configured in one of the MDT task sequence templates.

 The default configuration of the **Set Image Build** task sequence step is:

#### Properties

|**Name**|**Value**|
|-|-|
|**Type**|Set Task Sequence Variable|
|**Name**|Set Image Build|
|**Description**|Not specified|

#### Settings

|**Name**|**Value**|
|-|-|
|**Task Sequence Variable**|**ImageBuild**|
|**Value**|**%OSCurrentVersion%**|

#### Options

|**Name**|**Value**|
|-|-|
|**Disable this step**|Not selected|
|**Success codes**|**0 3010**|
|**Continue on error**|Not selected|
|**Conditional qualifier**|Not specified|

### Set Image Flags

This task sequence step sets the **ImageFlags** property to the value contained in **OSSKU**. Following is a brief listing of the settings that show how this step was originally configured in one of the MDT task sequence templates.

 The default configuration of the **Set Image Flags** task sequence step is:

#### Properties

|**Name**|**Value**|
|-|-|
|**Type**|Set Task Sequence Variable|
|**Name**|Set Image Flags|
|**Description**|Not specified|

#### Settings

|**Name**|**Value**|
|-|-|
|**Task Sequence Variable**|ImageFlags|
|**Value**|%OSSKU%|

#### Options

|**Name**|**Value**|
|-|-|
|**Disable this step**|Not selected|
|**Success codes**|0 3010|
|**Continue on error**|Not selected|
|**Conditional qualifier**|Not specified|

### Tattoo

This task sequence step tattoos the target computer with identification and version information. Following is a brief listing of the settings that show how this step was originally configured in one of the MDT task sequence templates.

 For more information about what script accomplishes this task and what properties are used, see [ZTITatoo.wsf](scripts.md#ztitatoowsf).

 The default configuration of the **Tattoo** task sequence step is:

#### Properties

|**Name**|**Value**|
|-|-|
|**Type**|Run Command Line|
|**Name**|Tattoo|
|**Description**|Not specified|

#### Settings

|**Name**|**Value**|
|-|-|
|**Command line**|`cscript.exe "%SCRIPTROOT%\ZTITatoo.wsf"`|
|**Start in**|Not specified|
|**Run this step as the following account**|Not specified|

#### Options

|**Name**|**Value**|
|-|-|
|**Disable this step**|Not selected|
|**Success codes**|0 3010|
|**Continue on error**|Not selected|
|Conditional qualifier|Not specified|

### Validate

This task sequence step validates that the target computer meets the specified deployment prerequisite conditions. Following is a brief listing of the settings that show how this step was originally configured in one of the MDT task sequence templates.

 For more information about what script accomplishes this task and what properties are used, see [ZTIValidate.wsf](scripts.md#ztivalidatewsf).

 The default configuration of the **Validate** task sequence step is:

#### Properties

|**Name**|**Value**|
|-|-|
|**Type**|Validate|
|**Name**|Validate|
|**Description**|Not specified|

#### Settings

|**Name**|**Value**|
|-|-|
|**Ensure minimum memory \(MB\)**|Selected. The value selector is set to **768**.|
|**Ensure minimum processor speed \(MHz\)**|Selected. The value selector is set to **800**.|
|**Ensure specified image size will fit \(MB\)**|Not selected.|
|**Ensure current operating system to be refreshed**|Selected. The value selector is set to **Server** or **Client**, depending on the template used to create the task sequence.|

#### Options

|**Name**|**Value**|
|-|-|
|**Disable this step**|Not selected|
|**Success codes**|0 3010|
|**Continue on error**|Not selected|
|**Conditional qualifier**|Not specified|

### Windows Update \(Pre\-Application Installation)

This task sequence step installs updates to the target computer prior to the installation of applications. Following is a brief listing of the settings that show how this step was originally configured in one of the MDT task sequence templates.

 For more information about what script accomplishes this task and what properties are used, see [ZTIWindowsUpdate.wsf](scripts.md#ztiwindowsupdatewsf).

 The default configuration of the **Windows Update \(Pre\-Application Installation\)** task sequence step is:

#### Properties

|**Name**|**Value**|
|-|-|
|**Type**|Run Command Line|
|**Name**|Windows Update \(Pre\-Application Installation\)|
|**Description**|Not specified|

#### Settings

|**Name**|**Value**|
|-|-|
|**Command line**|`cscript.exe "%SCRIPTROOT%\ZTIWindowsUpdate.wsf"`|
|**Start in**|Not specified|
|**Run this step as the following account**|Not specified|

#### Options

|**Name**|**Value**|
|-|-|
|**Disable this step**|Not selected|
|**Success codes**|0 3010|
|**Continue on error**|Not selected|
|**Conditional qualifier**|Not specified|

### Windows Update (Post-Application Installation)

This task sequence step is the same as the **Windows Update (Pre-Application Installation)** task sequence step.

### Wipe Disk

This task sequence step wipes all information from the disk using the **Format** command.

 For more information about what script accomplishes this task and what properties are used, see [ZTIWipeDisk.wsf](scripts.md#ztiwipediskwsf).

 The default configuration of the **Wipe Disk** task sequence step is:

#### Properties

|**Name**|**Value**|
|-|-|
|**Type**|Run Command Line|
|**Name**|Wipe Disk|
|**Description**|This will only run if **WipeDisk**=TRUE in CustomSettings.ini|

#### Settings

|**Name**|**Value**|
|-|-|
|**Command line**|`cscript.exe "%SCRIPTROOT%\ZTIWipeDisk.wsf"`|
|**Start in**|Not specified|
|**Run this step as the following account**|Not specified|

#### Options

|**Name**|**Value**|
|-|-|
|**Disable this step**|Not selected|
|**Success codes**|0 3010|
|**Continue on error**|Not selected|
|**Conditional qualifier**|Not specified|

## Related articles

- [Properties](properties.md).
- [Scripts](scripts.md).
- [Support Files](support-files.md).
- [Utilities](utilities.md).
- [MDT Windows PowerShell Cmdlets](mdt-windows-powershell-cmdlets.md).
- [Tables and Views in the MDT DB](tables-views-mdt-db.md).
- [Windows 7 Feature Dependency Reference](windows-7-feature-dependency.md).
- [UDI Reference](udi-reference.md).