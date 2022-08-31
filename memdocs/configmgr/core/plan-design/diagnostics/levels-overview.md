---
title: Levels of diagnostic usage data
titleSuffix: Configuration Manager
description: Learn about the levels of diagnostics and usage data that Configuration Manager collects
ms.date: 08/12/2022
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
author: paasin
ms.author: paasin
manager: apoorvseth
ms.localizationpriority: medium
---

# Levels of diagnostic usage data

*Applies to: Configuration Manager (current branch)*

Configuration Manager collects three levels of diagnostics and usage data: **Basic**, **Enhanced**, and **Full**. By default, this feature is set at the Enhanced level.

> [!IMPORTANT]
> Configuration Manager doesn't collect site codes, sites names, IP addresses, user names, computer names, physical addresses, or email addresses on the Basic or Enhanced levels. Any collection of this information on the Full level isn't purposeful. It's potentially included in advanced diagnostic information like log files or memory snapshots. Microsoft doesn't use this information to identify you, contact you, or develop advertising.

## Levels

### Basic

The Basic level includes data about your hierarchy. It's required to help improve your installation or upgrade experience. This data also helps determine the Configuration Manager updates that are applicable for your hierarchy.

### Enhanced

The Enhanced level is the default after setup finishes. This level includes data that's collected in the Basic level and feature-specific data. It shows frequency and duration of use of different features. It also includes Configuration Manager client settings data: component name, state, and certain settings like polling intervals. Information about software updates is basic on feature usage, it doesn't include data about update compliance at this level.

Microsoft recommends this level because it provides the minimum data to make product and service improvements.

Some examples of data that this level doesn't collect include:

- Names of sites, users, computer, or other objects

- Details of security-related objects

- Vulnerabilities like counts of systems that require software updates

### Full

The Full level includes all data in the Basic and Enhanced levels. It also includes additional information about Endpoint Protection, update compliance percentages, and software update information. This level can also include advanced diagnostic information like system files and memory snapshots. This advanced data might include personal information exists in memory or log files at the time of capture.

## How to change the level

To change the data collection level, you need **Modify** permissions on the **Site** object class.

1. In the Configuration Manager console, go to the **Administration** workspace, expand **Site Configuration**, and select the **Sites** node.

1. Select **Hierarchy Settings** in the ribbon.

1. Switch to the **Diagnostic and Usage Data** tab, then choose the data level.

## Version-specific details

The following articles detail the specific data that Configuration Manager collects at each level with each supported version:

- [Diagnostic and usage data for 2207](levels-of-diagnostic-usage-data-collection-2207.md)
- [Diagnostic and usage data for 2203](levels-of-diagnostic-usage-data-collection-2203.md)
- [Diagnostic and usage data for 2111](levels-of-diagnostic-usage-data-collection-2111.md)
- [Diagnostic and usage data for 2107](levels-of-diagnostic-usage-data-collection-2107.md)
- [Diagnostic and usage data for 2103](levels-of-diagnostic-usage-data-collection-2103.md)



## Next steps

Next, learn about the diagnostics and usage data that Configuration Manager collects for its tools:

> [!div class="nextstepaction"]
> [Diagnostic usage data for tools](tools.md)
