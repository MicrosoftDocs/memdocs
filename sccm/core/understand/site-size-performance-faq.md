---
title: Site sizing and performance FAQ
titleSuffix: Configuration Manager
description: Answers to common System Center Configuration Manager questions about site sizing and performance.
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.topic: conceptual
ms.date: 04/19/2019
---

# System Center Configuration Manager site sizing and performance FAQ

*Applies to: System Center Configuration Manager (Current Branch)*

This document addresses frequently asked questions about Configuration Manager site sizing guidance and common performance issues.

## Machine and disk configuration FAQs and examples

### How should I format the disks on my site server and SQL Server?

You should separate Configuration Manager inboxes and SQL files on at least two different volumes. The optimized cluster allocation sizes are different, depending on the characteristics of the I/O they perform. 

For the volume hosting your sites server inboxes, use NTFS, with 4K or 8K allocation units. ReFS writes 64k even for small files. Configuration Manager has many small files, so ReFS can produce unnecessary disk overhead.

For disks containing SQL database files, use either NTFS or ReFS formatting, with 64K allocation units.

### How and where should I lay out my SQL database files?

Modern arrays of solid state drives (SSD) and Azure Premium Storage can provide very high IOPS on a single volume, with very few disks. You typically add more drives to an array for additional storage, not additional throughput. But if you require more IOPS than you can generate on a single volume, usually because you are using physical spindle-based disks, you should allocate 60% of the total recommended IOPS and disk space for the *.MDF* file, 20% for the *.LDF* file, and 20% for the log and data temp files. The *.LDF* and temp files can all reside on a single volume with 40% (20% + 20%) of your allocated IOPS.

By default, SQL will create one temp data file, but you should create more, to avoid SQL locks and waiting for access to a single file. Community opinions vary on the best number of temp data files to create, from four to eight. Testing reveals very little difference between four to eight, so you can create four *equally sized* temp data files. Your tempdb data files should be up to 20-25% the size of your full database.

### Are there any other recommendations for disk setup?

When configurable, set RAID controller memory to 70% allocation for write operations and 30% for read operations. In general, use a RAID 10 array configuration for the site database. RAID 1 is also acceptable for small-scale sites with low I/O requirements, or if you use fast SSDs. With larger disk arrays, configure spare disks to automatically replace failing disks.

**Example: Physical machine with physical disks** 

According to [sizing guidelines](../plan-design/config/site-size-performance-guidelines.md#general-sizing-guidelines), for a colocated site server and SQL server supporting **100,000** clients, you need 1200 IOPS for your site server inboxes and 5000 IOPS for SQL server files.

Your resulting disk configuration might look like this:

| Drives<sup>1</sup> | RAID | Format | Volume contents | Minimum IOPS needed| Approx. IOPS supplied<sup>2</sup>  |
|----------------|-----------|-------------|----------------------|---------------------|------------------|
| 2x10k          | 1         | -           | Windows              |                     | -                |
| 6x15k          | 10        | NTFS 8k     | ConfigMgr inboxes    |     1700            | 1751             |
| 12x15k         | 10        | 64k ReFS    | SQL .MDF             | 60%*5000 = 3000     | 3476             |
| 8x15k          | 10        | 64k ReFS    | SQL .LDF, temp files | 40%*5000 = 2000     | 2322             |

1. Does not include recommended spare disks. 
2. This value is from [Example disk configurations](../plan-design/config/site-size-performance-guidelines.md#example-disk-configurations). 

### I use Hyper-V on Windows Server. How should I configure the disks for my Configuration Manager VMs for best performance?

Hyper-V delivers similar performance to a physical server, if hardware resources (CPU cores and pass-through storage) are 100% dedicated to the virtual machine (VM). Using fixed-size *.VHD* or *.VHDX* disk files causes a minimal 1-5% I/O performance impact. Using dynamically expanding *.VHD* or *.VHDX* disk files causes up to 25% I/O performance impact for the Configuration Manager workload. If you need dynamically expanding disks, compensate by adding an additional 25% IOPS performance to the array.

When running your Configuration Manager site server or SQL inside a VM, isolate the Hyper-V host OS drives from the VM OS and data drives.

For more information about optimizing VMs, see (/windows-server/administration/performancetuning/role/hyper-v-server/).

**Example: Hyper-V VM-based site server** 

According to [sizing guidelines](../plan-design/config/site-size-performance-guidelines.md#general-sizing-guidelines), for a colocated site server and SQL server supporting **150,000** clients, you need 1800 IOPS for your site server inboxes and 7400 IOPS for SQL Server files.

Your resulting disk configuration might look like this:

| Drives<sup>1</sup> | RAID | Format<sup>2</sup> | Volume contents | Minimum IOPS needed| Approx. IOPS supplied<sup>3</sup>  |
|----------------|-----------|----------------|---------------------------|----------------------|------------------|
| 2x10k          | 1         | -              | Hyper-V host OS           | -                    | -                |
| 2x10k          | 1         | -              | (VM) site server OS       | -                    | -                |
| 2xSSD SAS      | 1         | NTFS 8k        | (VM) ConfigMgr inboxes    | 1800                 | 7539             |
| 4xSSD SAS      | 10        | 64k ReFS       | (VM) Host SQL (all files) | 7400                 | 14346            |

1. Does not include recommended spare disks. 
2. Fixed-size, pass-through *.VHDX* for the VM drive dedicated to the underlying volume. 
3. This value is from [Example disk configurations](../plan-design/config/site-size-performance-guidelines.md#example-disk-configurations). 

### Are there any suggestions for Configuration Manager environments in Microsoft Azure?

Start by reading the [Configuration Manager on Azure frequently asked questions](configuration-manager-on-azure.md).

Azure infrastructure as a service (IaaS) VMs that leverage Premium Storage-based disks can have very high IOPS. On these VMs, configure additional disks for anticipated disk space needs, rather than for additional IOPS.

Azure storage is inherently redundant and doesn't require multiple disks for availability. You can stripe disks in Disk Manager or Storage Spaces to provide additional space and performance.

For more information and recommendations on how to maximize Premium Storage performance and run SQL servers in Azure IaaS VMs, see:

- [https://docs.microsoft.com/en-us/azure/storage/storage-premium-storageperformance\#optimizing-application-performance](/azure/storage/storage-premium-storage-performance#optimizing-application-performance)
 
- [https://docs.microsoft.com/en-us/azure/virtual-machines/windows/sql/virtual-machineswindows-sql-performance\#disks-guidance](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-performance#disks-guidance)

**Example: Azure-based site server** 

According to [sizing guidelines](../plan-design/config/site-size-performance-guidelines.md#general-sizing-guidelines), for a colocated site server and SQL server supporting **50,000** clients, you need 8 cores, 32 GB, and 1200 IOPS for your site server inboxes, and 2800 IOPS for SQL Server files.

Your resulting Azure machine might be a DS13v2 (8 cores, 56GB) with the following disk configuration:

| Drives | RAID | Format | Contains | Minimum IOPS needed| Approx. IOPS supplied<sup>1</sup>  |
|------------------|---------------|--------------------|----------------------|------------------|
| &lt;standard&gt; | -             | Site server OS     | -                    | -                |
| 1xP20 (512GB)    | NTFS 8k       | ConfigMgr inboxes  | 1200                 | 2334             |
| 1xP30 (1024GB)   | 64k ReFS      | SQL (all files<sup>2</sup>) | 2800                 | 3112             |

1. This value is from [Example disk configurations](../plan-design/config/site-size-performance-guidelines.md#example-disk-configurations).
2. [Azure guidance](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-performance#disks-guidance) allows for placing the TempDB on the local, SSD-based *D:* drive, given it will not exceed available space and will allow for additional disk I/O distribution.

## Example: Azure-based site server (for instant performance increase) 

Azure disk throughput is limited by the size of the VM. The configuration in the preceding Azure example may limit future expansion or additional performance. Adding additional disks during initial deployment of your Azure VM lets you upsize your Azure VM in the future for increased processing power, with minimal upfront investment. Planning ahead is a much simpler way to increase site performance as requirements change, instead of later needing to do a more complicated migration.

Change the disks in the preceding Azure example to see how the IOPS change.

**DS13v2** 

| Drives<sup>1</sup> | RAID | Format | Contains | Minimum IOPS needed| Approx. IOPS supplied<sup>2</sup>  |
|------------------|---------------|--------------------|----------------------|------------------|
| &lt;standard&gt; | -             | Site server OS     | -                    | -                |
| 2xP20 (1024GB)   | NTFS 8k       | ConfigMgr inboxes  | 1200                 | 3984             |
| 2xP30 (2048GB)   | 64k ReFS      | SQL (all files<sup>3</sup>) | 2800                 | 3984             |

1. Disks are striped using Storage Spaces.
2. This value is from [Example disk configurations](../plan-design/config/site-size-performance-guidelines.md#example-disk-configurations). VM size limits performance.
3. [Azure guidance](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-performance#disks-guidance) allows for placing the TempDB on the local, SSD-based *D:* drive, given it will not exceed available space and will allow for additional disk I/O distribution.

If you need more performance in future, you can upsize your VM to a DS14v2, which will double CPU and memory. The additional disk bandwidth allowed by that VM size will also instantly boost the available disk IOPS on your previously configured disks.

**DS14v2**

| Drives<sup>1</sup> | RAID | Format | Contains | Minimum IOPS needed| Approx. IOPS supplied<sup>2</sup>  |
|------------------|---------------|--------------------|----------------------|------------------|
| &lt;standard&gt; | -             | Site server OS     | -                    | -                |
| 2xP20 (1024GB)   | NTFS 8k       | ConfigMgr inboxes  | 1200                 | 4639             |
| 2xP30 (2048GB)   | 64k ReFS      | SQL (all files<sup>3</sup>) | 2800                 | 6182             |

1. Disks are striped using Storage Spaces.
2. This value is from [Example disk configurations](../plan-design/config/site-size-performance-guidelines.md#example-disk-configurations). VM size limits performance.
3. [Azure guidance](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-performance#disks-guidance) allows for placing the TempDB on the local, SSD-based *D:* drive, given it will not exceed available space and will allow for additional disk I/O distribution.

## Other common SQL Server-related performance questions 

### Is it better to run with SQL colocated with the site server, or run it on a remote server?

Both can perform adequately, assuming the single server is appropriately sized, or network connectivity is sufficient between the two servers.

Remote SQL requires the upfront and operational cost of an additional server, but is typical among the majority of large-scale customers. Benefits of this configuration include:

- Increased site availability options, such as SQL Always On)
  
- Ability to run heavy reporting with less overheard to site processing
  
- Simpler disaster recovery in some situations
  
- Easier security management
  
- Role separation for SQL management, such as with a separate DBA team
  
Colocated SQL requires a single server, and is typical for most small-scale customers. Benefits of this configuration include:

- Lower costs for machines, licenses, and maintenance
  
- Fewer points of failure in the site
  
- Better control for planning downtime
  
### How much RAM should I allocate for SQL?

By default, SQL will use all available memory on your server, potentially starving the OS and other processes on the machine. To avoid potential performance issues, it's important to explicitly allocate memory to SQL, On site servers colocated with your SQL server, make sure the OS has enough RAM for file caching and other operations, and there is enough RAM remaining for SMSExec and other Configuration Manager processes. When running SQL on a remote server, you can allocate the *majority* of the memory to SQL, but not all. Review the [sizing guidelines](../plan-design/config/site-size-performance-guidelines.md#general-sizing-guidelines) for initial guidance. 

SQL Server memory allocation should be rounded to whole GB. Also, as RAM increases to very large amounts, you can let SQL have a higher percentage. For example, when 256 GB or more of RAM is available, you can configure SQL for up to 95%, as that still preserves plenty of memory for the OS. Monitoring the page file is a good way to ensure enough memory has been allocated for the OS and any Configuration Manager processes.

### Cores are cheap these days. Should I just add a bunch of them to my SQL server?

You may run into memory contention issues when more than 16 physical cores are available and there is not enough RAM on your SQL server. The Configuration Manager workload performs better when at least 3-4 GB of RAM per core is available for SQL. When adding cores to your SQL servers, be sure to increase RAM in proportional amounts.

### Will SQL Always On impact my performance?

In general, SQL Always On has negligible effect on performance of the system when sufficient networking is available between the SQL replica servers. You can have rapid database log *.LDF* file growth in a busy SQL Always On environment. However, log file space is automatically released after a successful database backup. Add a SQL job for the Configuration Manager database to perform a backup, for example every 24 hours, and an *.LDF* backup every six hours. For more information about SQL Always On and Configuration Manager, including more about SQL backup strategies, see [SQL Server Always On for a highly-available site database](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database).

### Should I enable SQL compression on my database?

SQL compression is not generally recommended for the Configuration Manager database. While there are no functional issues with enabling compression on a Configuration Manager database, test results don’t show much size savings compared to the potential sizable performance impact to the system.

### Should I enable SQL encryption on my database?

Any secrets stored in the Configuration Manager database are already stored in securely, but adding SQL encryption can add yet another layer of security. While there are no functional issues with enabling encryption on your database, you may notice up to a 25% performance degradation, depending on the tables you choose to encrypt and the version of SQL you're using. Therefore, encrypt with caution, especially in large-scale environments. Also remember to update your backup and recovery plans to ensure you can successfully recover the encrypted data.

### What version of SQL should I run?

For supported versions of SQL, see [Support for SQL Server versions](../plan-design/configs/support-for-sql-server-versions.md). From a performance standpoint, all supported versions of SQL meet required performance criteria. However, SQL 2012 and SQL 2016 or newer tend to outperform SQL 2014 in some aspects of the Configuration Manager workload. Also, running SQL 2014 at SQL 2012 compatibility level (110) improves performance in general. At installation time, Configuration Manager databases running on SQL 2012 and SQL 2014 are set to compatibility level 110. SQL 2016 or newer is set to that SQL version's default compatibility level, such as 130 for SQL 2016. Upgrade SQL in place does not update compatibility levels until you install the next major Configuration Manager current branch version. If you are experiencing unusual timeouts or slowness on certain SQL queries on SQL 2016 or later, such as in certain areas of the Admin Console when using RBAC, changing the SQL compatibility level on the Configuration Manager database to 110 may help. Running at SQL compatibility level 110 on SQL 2014 and newer versions of SQL is fully supported. For more information on using compatibility level 110 with Configuration Manager, see [SQL query times out or console slow on certain Configuration Manager database queries](https://support.microsoft.com/help/3196320/sql-query-times-out-or-console-slow-on-certain-configuration-manager-d).

As of January 2018, you should *avoid* the following SQL versions, due to various known performance-related or other potential issues:

- SQL 2012 SP3 CU1 to CU5
- SQL 2014 SP1 CU6 to SP2 CU2
- SQL 2016 RTM to CU3, SP1 CU3 to CU5

### Should I implement any additional SQL indexing tasks?

Yes, update indexes as often as once a week and statistics as often as once a day to improve SQL performance. Third-party scripts and additional information available from the Configuration Manager and SQL communities can help optimize these tasks.

In large sites, some SQL tables, such as CI\_CurrentComplianceStatusDetails, HinvChangeLog, might be very big, depending on your usage patterns. You may need to reduce or alter your maintenance approach for them one by one.

### When should I use full SQL Server instead of SQL Express on my secondary sites?

SQL Express does not have any significant performance implications on secondary sites, and it is completely adequate for most customers. It is also very easy to deploy and manage, and is the recommended configuration for nearly all customers at any size.

There is one situation where a full SQL Server installation might be needed. It is possible to exceed the 10 GB size limit of SQL Express if you have a very large number of distribution points and packages or sources in your environment. If you anticipate having the number of packages times the number of distribution points greater than 4,000,000, such as 2,000 DPs with 2,000 pieces of content across the entire hierarchy, you should consider using full SQL Server at your secondary sites, to avoid running into potential database size constraints.

### Should I change MaxDOP settings on my database?

Leaving your setting at 0 (use all available processors) is optimal for overall processing performance in most circumstances.

Many Configuration Manager administrators follow the guidance at [Recommendations and guidelines for the "max degree of parallelism" configuration option in SQL Server](https://support.microsoft.com/help/2806535/recommendations-and-guidelines-for-the-max-degree-of-parallelism-confi). On most modern large hardware, this guidance leads to a suggested maximum setting of 8. However, if you run many smaller queries compared to your number of processors, it may help to set it to a higher number. Limiting yourself to 8 is not necessarily the best setting on larger sites when more cores are available. 

On SQL servers with greater than 8 cores, start with a setting of 0, and only make changes if you experience performance issues or excessive locking. If you need to change MaxDOP because you are encountering performance issues at 0, start with a new value at least greater than or equal to the minimum number of cores recommended for that site’s SQL server sizing. Going lower than this value nearly always has negative performance implications. For example, a remote SQL server for a 100,000 client site needs at least 12 cores. If your SQL server has 16 cores, start your MaxDOP setting testing with a value of 12.

## Other common performance-related questions

### Which folders on the site server (or other roles) should I exclude for antivirus software?

Take care when disabling antivirus protection on any system. In high volume and secure environments, we recommend disabling *active monitoring* for optimum performance.

For more information about recommended antivirus exclusions, see [Recommended antivirus exclusions for Configuration Manager 2012 and Current Branch Site Servers, Site Systems, and Clients](https://support.microsoft.com/help/327453/recommended-antivirus-exclusions-for-configuration-manager-2012-and-cu).

### What can I do to make WSUS perform better when it's used with Configuration Manager?

Changing a few key IIS settings, such as WsusPool Queue Length and WsusPool Private Memory limit, can improve WSUS performance, even on smaller installations. For more information, see [Recommended hardware](../plan-design/configs/recommended-hardware.md).

You should also make sure you have the latest updates installed for the operating system running WSUS:

- Windows Server 2012: Any non "Security only" cumulative update released October 2017 or later. ([KB4041690](https://support.microsoft.com/help/4041690/windows-server-2012-update-kb4041690))
- Windows Server 2012 R2: Any non "Security only" cumulative update released August 2017 or later. ([KB4039871](https://support.microsoft.com/help/4039871/windows-8-1-windows-server-2012-r2-update-kb4039871))
- Window Server 2016: any non "Security only" cumulative update released August 2017 or later. ([KB4039396](https://support.microsoft.com/help/4039396/windows-10-update-kb4039396))

### What type of maintenance should I run on my WSUS servers?

See [The complete guide to Microsoft WSUS and Configuration Manager SUP maintenance](https://support.microsoft.com/help/4490644/complete-guide-to-microsoft-wsus-and-configuration-manager-sup-maint).

### I want to set up basic performance monitoring for my site. What should I watch?

Traditional server performance monitoring works very effectively for general Configuration Manager. You can also leverage the various System Center Operations Manager management packs for Configuration Manager, SQL Server, and Windows Server to monitor basic health of your servers. You can also directly monitor the Windows Performance Monitor (PerfMon) counters Configuration Manager provides. Monitor the backlogs in the various inboxes for early warning signs of potential performance issues or backlogs in a site.

## See also

[Site sizing and performance guidelines](../plan-design/config/site-size-performance-guidelines.md)
[Configuration Manager on Azure frequently asked questions](configuration-manager-on-azure.md).
