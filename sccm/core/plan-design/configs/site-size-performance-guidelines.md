---
title: Site sizing and performance guidelines
titleSuffix: Configuration Manager
description: Site size-related performance test results, methodology, and guidance.
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.topic: conceptual
ms.date: 04/19/2019
---

# System Center Configuration Manager site sizing and performance guidelines

*Applies to: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager leads the industry in scalability and performance. Other documentation covers [maximum supported scalability limits](size-and-scale-numbers.md) and [hardware guidelines](recommended-hardware.md) for running sites at the largest environment sizes. This article gives supplemental performance guidance for environments of all sizes. This guidance can help you more accurately estimate the hardware you need to deploy Configuration Manager.

This article focuses on the largest contributor to Configuration Manager performance bottlenecks: the disk input/output subsystem or IOPS. The article:

- Presents details and test results focused on IOPS,
- Documents how to reproduce the tests with your own environments and hardware, and
- Suggests disk IOPS requirements for various size environments. 

## Performance test methodology

You can deploy Configuration Manager in many unique ways, but it's important to understand a few variables in any sizing discussions. One variable is *feature interval*, such as an inventory cycle. Another variable is the number of users, software deployments, or other *objects* the system references or deploys. Performance testing applies these variables as part of a *load*. The load generates objects at a typical rate for enterprise customers using production deployments in different size environments.

> [!NOTE] 
> Customer telemetry data allows for testing current branch builds with the most common scenarios, configurations, and settings for most customers. The recommendations in this article are based on these averages. Your experiences may vary based on your environment size and configuration. In general, Configuration Manager requires common sense when it comes to objects and intervals. Just because you can collect every file on a system, or set the interval for a cycle to one minute, doesn't mean you should.

The following sections highlight some key settings and configurations to use when testing and modeling processing needs for large enterprises. These guidelines help set basic system performance expectations for the suggested hardware sizes.

### Feature intervals settings 
Most testing should use default intervals for the key cycles in the system. For example, hardware inventory testing occurs once per week with a larger than default *.mof* file. Some recurring feature intervals, especially hardware and software inventory cycles, can have significant effects on an environment’s performance characteristics. Environments that enable aggressive default intervals for data collection need oversized hardware in direct proportion to the increase in activity. For example, say you have 25,000 desktop clients and want to collect hardware inventory two times faster than the default interval. You should start by sizing your site's hardware as if you had 50,000 clients.

### Objects 
Tests should use the *upper average* of the objects that large enterprises tend to use with the system. Typical values are thousands of collections and applications, which are deployed to hundreds of thousands of users or systems. Tests should run simultaneously on *all* objects in the system at these limits. Many customers leverage several features, but don't generally use all features of the product at these upper limits. Testing with all product features helps ensure the best possible system-wide performance, and allows a buffer for features that some customers may use above average. 

### Loads 
Tests should also run on greater than standard *average day* loads, by performing simulations that generate peak usage demands on the system. One example is simulating Patch Tuesday rollouts, to make sure the system can return update compliance data promptly during these days of peak activity. Another example is simulating site activity during a widespread malware outbreak, to ensure timely notification and response are possible. Although deployed machines of the recommended size may be underutilized on any given day, these more extreme situations require some processing buffer.

### Configurations
Testing should run on a range of physical, Hyper-V, and Azure hardware, with a mixture of supported operating systems and SQL Server versions. Always validate the worst cases for the supported configuration. In general, Hyper-V and Azure return comparable performance results to equivalent physical hardware when configured similarly. Newer server operating systems tend to perform equally or better than older supported server operating systems. While all supported platforms meet the minimum requirements, usually the latest versions of supporting products like Windows and SQL produce even better performance. 

The largest variation comes from the SQL Server versions in use. For more information about SQL Server versions, see [What version of SQL should I run?](../../understand/site-size-performance-faq.md#what-version-of-sql-should-i-run). 

## Key performance determinants

You can test and measure Configuration Manager performance with a variety of settings, in different ways, and at different site sizes. The following settings and objects can dramatically affect performance. Be sure to consider them when testing and modeling performance in your environment.

> [!CAUTION]
> While few aspects of Configuration Manager have official maximums or user interface limits that prevent excessive usage, going beyond the guidelines can have significant adverse effects on a site's performance. Exceeding recommended levels or ignoring sizing guidance typically requires larger hardware, and may render your environment unmaintainable until you reduce the frequency or count of various objects.

### Hardware inventory
To test baseline performance, set hardware inventory collection to once per week, with the default *.mof* file size plus approximately 20% additional properties. Don't enable all properties, and collect only properties you actually need. Pay special attention when collecting properties, such as available virtual memory, that will *always* change with *every* inventory cycle. Collecting these properties can cause excessive churn on every inventory cycle from every client.

### Software inventory
To test baseline performance, set software inventory collection to once per week, with *product only* details. Collecting many files can place a significant strain on the inventory subsystem. Avoid specifying filters that could end up collecting thousands of files across many clients, such as *\*.exe* or *\*.dll*.

### Collections
Baseline performance testing can include several thousand collections with a variety of scope, size, complexity, and update settings. Site performance isn't a direct function of the sheer number of collections on a site. Performance is also a cross-product of collections' query complexity, full and incremental updates and change frequency, dependencies among collections, and numbers of clients in the collections.

Where possible, minimize collections that have expensive or complicated dynamic rule queries. For collections that require these types of rules, set appropriate update intervals and update times to minimize the impact of collection re-evaluation on the system. For example, update at midnight instead of 8:00 AM.

Enabling incremental updates on collections ensures quick and timely updates to collection membership. But even though incremental updates are efficient, they still put load on the system. Balance the change frequency you anticipate with the need for near real-time updates on membership. For example, say you expect heavy churn in collection members, but you don't require near real-time membership updates. It's more efficient and produces less load on the system to update the collection with a scheduled full update at some interval, than to enable incremental updates. 

When you enable incremental updates, reduce any scheduled full updates on the same collections. They're only a backup method of evaluation, since incremental updates should keep your collection membership updated in near real time. [Best practices for collections](../../clients/manage/collections/best-practices-for-collections.md#do-not-use-incremental-updates-for-a-large-number-of-collections) recommends a maximum number of total collections for incremental updates, but as the article points out, your experience can vary based on many factors.

Collections with only direct membership rules and with a limiting collection that isn't performing incremental updates don't need scheduled full updates. Disable update schedules for these types of collections to prevent unnecessary load on the system. If the limiting collection uses incremental updates, collections with only direct membership rules may not reflect membership updates for up to 24 hours, or until a scheduled refresh takes place.

While not a best practice, some organizations create hundreds or even thousands of collections as part of various business processes. If you use automation to create collections, it's important to enable any needed incremental updates correctly. Minimize and spread out any full update schedules to avoid hot spots of collection evaluation during a single time period. Establish a regular grooming process to delete unused collections, especially if you automatically create collections that you no longer need after some time.

Remember that Configuration Manager creates policies for all objects in your collections when you target tasks like deployments to them. Membership changes, either through scheduled refresh or incremental updates, can create a lot of other work for the whole system. The latest current branch builds have special policy optimizations for the All Systems and All Users collections. When targeting your entire enterprise, use the built-in collections instead of a clone of these built-in collections.

To investigate collection performance even deeper, you can use the Collection Evaluation Viewer (CEViewer) in the [Configuration Manager Toolkit](https://www.microsoft.com/download/details.aspx?id=50012).

### Discovery methods
For baseline performance testing, run server-based discovery methods once a week, enabling delta discovery as appropriate to keep the data fresh during the week. The tests should discover an object quantity proportional to the simulated enterprise size. The performance baseline test for heartbeat discovery should also run once a week.

Discovery data is global data. A common performance-related problem is to misconfigure server-based discovery methods in a hierarchy, causing duplicate discovery of the same resources from multiple primary sites. Carefully configure discovery methods to optimize communication with the target service, such as Active Directory domain controllers, while avoiding duplication of the same discovery scope on multiple primary sites.

## General sizing guidelines 

Based on the preceding [performance test methodology](#performance-test-methodology), the following table gives general *minimum* hardware requirement guidelines for specific numbers of managed clients. These values should allow most customers with the specified number of clients to process objects fast enough to administer the specified site. Computing power continues to decrease in price every year, and some of the requirements below are small in terms of modern server hardware configurations. Hardware that exceeds the following guidelines will proportionally increase performance for sites that require additional processing power, or have special product usage patterns. 

| Desktop clients  | Site type/role  | Cores<sup>1</sup>   | Memory (GB)   | SQL memory allocation  | IOPS:  Inboxes<sup>2</sup>  | IOPS: SQL<sup>2</sup>   | Storage space required (GB)<sup>3</sup>   |
|------|-------------------------------------------------------------|-----|-----|-----|------|------|------|
| 25k  | Primary or CAS with database site role on the same server   | 6   | 24  | 65% | 600  | 1700 | 350  |
| 25k  | Primary or CAS                                              | 4   | 8   |     | 600  |      | 100  |
|      | Remote SQL                                                  | 4   | 16  | 70% |      | 1700 | 250  |
|      |                                                             |     |     |     |      |      |      |
| 50k  | Primary or CAS with database site role on the same server   | 8   | 32  | 70% | 1200 | 2800 | 600  |
| 50k  | Primary or CAS                                              | 4   | 8   |     | 1200 |      | 200  |
|      | Remote SQL                                                  | 8   | 24  | 70% |      | 2800 | 400  |
|      |                                                             |     |     |     |      |      |      |
| 100k | Primary or CAS with database site role on the same server   | 12  | 64  | 70% | 1200 | 5000 | 1100 |
| 100k | Primary or CAS                                              | 6   | 12  |     | 1200 |      | 300  |
|      | Remote SQL                                                  | 12  | 48  | 80% |      | 5000 | 800  |
|      |                                                             |     |     |     |      |      |      |
| 150k | Primary or CAS with database site role on the same server   | 16  | 96  | 70% | 1800 | 7400 | 1600 |
| 150k | Primary or CAS                                   | 8   | 16   |     | 1800  |         | 400   |
|      | Remote SQL                                       | 16  | 72   | 90% |       | 7400    | 1200  |
|      |                                                             |     |     |     |      |      |      |
| 700k | CAS with database site role on the same server   | 20+ | 128+ | 80% | 1800+ | 9000+   | 5000+ |
| 700k | CAS                                              | 8+  | 16+  |     | 1800+ |         | 500+  |
|      | Remote SQL                                       | 16+ | 96+  | 90% |       | 9000+   | 4500+ |
|      |                                                             |     |     |     |      |      |      |
| 5k   | Secondary Site                                   | 4   | 8    |     | 500   | -       | 200   |
| 15k  | Secondary Site                                   | 8   | 16   |     | 500   | -       | 300   |

**Notes**

1. **Cores**: Configuration Manager performs many simultaneous processes, so needs a certain minimum number of CPU cores for various site sizes. While cores get faster each year, it's important to ensure that a certain minimum number of cores work in parallel. In general, any server-level CPU produced after 2015 meets the basic performance needs for the cores specified in the table. Configuration Manager takes advantage of additional cores beyond the recommendations, but generally, once you have the minimum suggested cores, you should prioritize CPU resource investment to increase the speed of existing cores, not add more, slower cores. For example, Configuration Manager will perform better on key processing tasks with 16 fast cores than with 24 slower cores, assuming enough other system resources like disk IOPS are available.
   
   The relationship between cores and memory is also important. In general, having less than 3-4 GB of RAM per core reduces the total processing capability on your SQL servers. You need more RAM per core when SQL is colocated with the site server components.
   
   > [!NOTE]
   > All testing sets machine power plans to allow maximum CPU power consumption and performance.
   
2. **IOPS: Inboxes and IOPS: SQL** refer to the IOPS needs for the Configuration Manager and SQL logical drives. The **IOPS: Inboxes** column shows the IOPS requirements for the logical drive where the Configuration Manager inbox directories reside. The **IOPS: SQL** column shows the total IOPS needs for the logical drive(s) that various SQL files use. These columns are different because the two drives should have different formatting. For more information and examples on suggested SQL disk configurations and file best practices, including details on splitting files across multiple volumes, see the [Site sizing and performance FAQ](../../understand/site-size-performance-faq.md).
   
   Both of these IOPS columns use data from the industry-standard tool, *Diskspd*. See [How to measure disk performance](#how-to-measure-disk-performance) for instructions on duplicating these measurements. In general, once you meet basic CPU and memory requirements, the storage subsystem has the largest impact on site performance, and improvements here will give the most payback on investment.
   
3.  **Storage space required:** These real-world values may differ from other documented recommendations. We provide these numbers only as a general guideline; individual requirements could vary widely. Carefully plan for disk space needs before site installation. Assume that some amount of this storage remains as free disk space most of the time. You may use this buffer space in a recovery scenario, or for upgrade scenarios that need free disk space for setup package expansion. Your site may require additional storage for large amounts of data collection, longer periods of data retention, and large amounts of software distribution content. You can also store these items on separate, lower-throughput volumes.

## How to measure disk performance 

You can use the industry-standard tool *Diskspd* to provide standardized suggestions for the IOPS that various-sized Configuration Manager environments require. While not exhaustive, the following test steps and command lines provide a simple and reproducible way to estimate your servers' disk subsystem throughput. You can compare your results to the minimum recommended IOPS in the [general sizing guidelines](#general-sizing-guidelines) table. 

See [Example disk configurations](#example-disk-configurations) for test results from a variety of hardware configurations in lab environments. You can use the data for a rough starting point when designing the storage subsystem for a new environment from scratch.

### To test disk IOPS  
1. Download the *Diskspd* utility here: [https://gallery.technet.microsoft.com/DiskSpd-A-Robust-Storage-6ef84e62](https://gallery.technet.microsoft.com/DiskSpd-A-Robust-Storage-6ef84e62).
   
1. Make sure you have at least 100 GB of free disk space. Disable any apps that might interfere or cause extra load on the disk, such as active antivirus scanning of the directory, SQL, or SMSExec.
   
1. Run *Diskspd* from an elevated command prompt. 
   
   Perform two runs of the tool in sequence for the volume that you want to test. The first test performs 64k-size, random write operations for one minute. This test ensures controller cache loading and disk space allocation, in case the volume is dynamically expanding. Discard the results of the first test. The second test should *immediately* follow the first test, and perform the same load for five minutes.
   
   For example, use the following specific command lines to test the G:\\ volume.
   
   `DiskSpd.exe -r -w100 -t8 -o8 -b64K -c100G -d60 -h -L G:\\test\testfile.dat` 
   
   `del G:\\test\testfile.dat`
   
   `DiskSpd.exe -r -w100 -t8 -o8 -b64K -c100G -d300 -h -L G:\\test\testfile.dat`
   
1. Review the output from the second test to find the total IOPS in the **I/O per s** column. In the following example, the total IOPS are **3929.18**.
   
   ```
   Total IO
   | thread |  bytes      |  I/Os   |  MB/s  | I/O per s | AvgLat | LatStdDev |
   |--------|-------------|---------|--------|-----------|--------|-----------| 
   |   1    |  9651814400 |  147275 |  30.68 |    490.92 | 16.294 | 10.210    | 
   |   2    |  9676652544 |  147654 |  30.76 |    492.18 | 16.252 |  9.998    |
   |   3    |  9638248448 |  147068 |  30.64 |    490.23 | 16.317 | 10.295    |
   |   4    |  9686089728 |  147798 |  30.79 |    492.66 | 16.236 | 10.072    | 
   |   5    |  9590931456 |  146346 |  30.49 |    487.82 | 16.398 | 10.384    | 
   |   6    |  9677242368 |  147663 |  30.76 |    492.21 | 16.251 | 10.067    |
   |   7    |  9637330944 |  147054 |  30.64 |    490.18 | 16.319 | 10.249    | 
   |   8    |  9692577792 |  147897 |  30.81 |    492.99 | 16.225 | 10.125    | 
   | Total: | 77250887680 | 1178755 | 245.57 |   3929.18 | 16.286 | 10.176    |
   ```

## Example disk configurations

The following tables show results from running the test steps in [How to measure disk performance](#how-to-measure-disk-performance) with various test lab configurations. Use this data for a *rough* starting point when designing the storage subsystem for a new environment from scratch. 

### Physical machines and Hyper-V 
Hardware is always improving. Expect newer generations of hardware and different hardware combinations, like SSDs and SANs, to exceed the performance stated below. These results are a basic starting point to consider when designing a server or discussing with your hardware vendor.

The following table shows the test results across various disk subsystems, including spindle and SSD-based hard drives, in various test lab configurations. All configurations format the disks with 64k clusters and attach them to an enterprise class disk controller. In addition to the RAID array disk count, they each have at least one spare disk.

| Disk type   | Disk count, not including +1 spare disk | RAID     | IOPS measured  |
|------------------|----------------------------------------------------|---------------|---------------|
| 15k SAS          | 2                                                  |           1   | 620           |
| 15k SAS          | 4                                                  |           10  | 1206          |
| 15k SAS          | 6                                                  |           10  | 1751          |
| 15k SAS          | 8                                                  |           10  | 2322          |
| 15k SAS          | 10                                                 |           10  | 2882          |
| 15k SAS          | 12                                                 |           10  | 3476          |
| 15k SAS          | 16                                                 |           10  | 4236          |
| 15k SAS          | 20                                                 |           10  | 5148          |
| 15k SAS          | 30                                                 |           10  | 7398          |
| 15k SAS          | 40                                                 |           10  | 9913          |
| SSD SATA         | 2                                                  |           1   | 3300          |
| SSD SATA         | 4                                                  |           10  | 5542          |
| SSD SATA         | 6                                                  |           10  | 7201          |
| SSD SAS          | 2                                                  |           1   | 7539          |
| SSD SAS          | 4                                                  |           10  | 14346         |
| SSD SAS          | 6                                                  |           10  | 15607         |

These are the devices the example used. This information isn't a recommendation for any specific hardware model or manufacturer. 

| Disk type    | Model      | RAID controller | Cache memory and configuration |
|-------------------|-----------------|----------------------|-------------------------------------|
| 15k RPM SAS HD    | HP EH0300JDYTH  | Smart Array P822     | 2GB, 20% Read / 80% Write           |
| SSD SATA          | ATA MK0200GCTYV | Smart Array P420i    | 1GB, 20% Read / 80% Write           |
| SSD SAS           | HP MO0800 JEFPB | Smart Array P420i    | 1GB, 20% Read / 80% Write           |

### Azure machine and disk performance 
Azure disk performance depends on several factors, such as the size of the Azure VM, and the number and type of disks it uses. Azure is also constantly adding new machine types and disk speeds that are different from the following chart. For more information about Configuration Manager running on Azure, and additional information on understanding disk I/O on Azure, see [Configuration Manager on Azure frequently asked questions](../../understand/configuration-manager-on-azure.md).

All disks are formatted NTFS 64k cluster size, and rows with more than one disk are configured as striped volumes via the Windows Disk Management utility.

| Azure VM| Azure disk| Disk count | Available space | IOPS measured   | Limiting factor   |
|--------------------------------------------|-------------------------|---------------------|---------------------------|-------|-----------------|
| **DS2/DS11**                              | P20                     | 1                   | 512 MB                    | 965   | Azure VM size   |
| **DS2/DS11**                              | P20                     | 2                   | 1024 MB                   | 996   | Azure VM size   |
| **DS2/DS11**                              | P30                     | 1                   | 1024 MB                   | 996   | Azure VM size   |
| **DS2/DS11**                              | P30                     | 2                   | 2048 MB                   | 996   | Azure VM size   |
| **DS3/DS12/F4S**                          | P20                     | 1                   | 512 MB                    | 1994  | Azure VM size   |
| **DS3/DS12/F4S**                          | P20                     | 2                   | 1024 MB                   | 1992  | Azure VM size   |
| **DS3/DS12/F4S**                          | P30                     | 1                   | 1024 MB                   | 1993  | Azure VM size   |
| **DS3/DS12/F4S**                          | P30                     | 2                   | 2048 MB                   | 1992  | Azure VM size   |
| **DS4/DS13/F8S**                          | P20                     | 1                   | 512 MB                    | 2334  | P20 disk        |
| **DS4/DS13/F8S**                          | P20                     | 2                   | 1024 MB                   | 3984  | Azure VM size   |
| **DS4/DS13/F8S**                          | P20                     | 3                   | 1536 MB                   | 3984  | Azure VM size   |
| **DS4/DS13/F8S**                          | P30                     | 1                   | 1024 MB                   | 3112  | P30 disk        |
| **DS4/DS13/F8S**                          | P30                     | 2                   | 2048 MB                   | 3984  | Azure VM size   |
| **DS4/DS13/F8S**                          | P30                     | 3                   | 3072 MB                   | 3996  | Azure VM size   |
| **DS5/DS14/F16S**                         | P20                     | 1                   | 512 MB                    | 2335  | P20 disk        |
| **DS5/DS14/F16S**                         | P20                     | 2                   | 1024 MB                   | 4639  | P20 disk        |
| **DS5/DS14/F16S**                         | P20                     | 3                   | 1536 MB                   | 6913  | P20 disk        |
| **DS5/DS14/F16S**                         | P20                     | 4                   | 2048 MB                   | 7966  | Azure VM size   |
| **DS5/DS14/F16S**                         | P30                     | 1                   | 1024 MB                   | 3112  | P30 disk        |
| **DS5/DS14/F16S**                         | P30                     | 2                   | 2048 MB                   | 6182  | P30 disk        |
| **DS5/DS14/F16S**                         | P30                     | 3                   | 3072 MB                   | 7963  | Azure VM size   |
| **DS5/DS14/F16S**                         | P30                     | 4                   | 4096 MB                   | 7968  | Azure VM size   |
| **DS15**                                  | P30                     | 1                   | 1024 MB                   | 3113  | P30 disk        |
| **DS15**                                  | P30                     | 2                   | 2048 MB                   | 6184  | P30 disk        |
| **DS15**                                  | P30                     | 3                   | 3072 MB                   | 9225  | P30 disk        |
| **DS15**                                  | P30                     | 4                   | 4096 MB                   | 10200 | Azure VM size   |

## See also

[Site sizing and performance FAQ](../../understand/site-size-performance-faq.md)
[Configuration Manager on Azure frequently asked questions](../../understand/configuration-manager-on-azure.md)
[Size and scale numbers](size-and-scale-numbers.md)
[Recommended hardware](recommended-hardware.md

