---
title: Diagnostic and usage data FAQ
titleSuffix: Configuration Manager
description: Frequently asked questions about diagnostic and usage data for Configuration Manager
ms.date: 01/23/2020
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 3fe32aa2-d594-4ad0-a291-b8f5395ac50b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
---

# Frequently asked questions about diagnostics and usage data

*Applies to: Configuration Manager (current branch)*

This article provides answers to frequently asked questions about diagnostic and usage data in Configuration Manager.

## <a name="bkmk_off"></a> Can I turn off diagnostic and usage data?

To help manage when the site sends data, use the service connection point in offline mode. Then use the service connection tool to manually send data. For more information, see the following articles:

- [About the service connection point](/configmgr/core/servers/deploy/configure/about-the-service-connection-point)
- [Use the service connection tool](/configmgr/core/servers/manage/use-the-service-connection-tool)

To support new versions of Windows 10 and cloud services like Microsoft Intune, you need to update the current branch of Configuration Manager on a regular basis. Microsoft requires at least the basic level of diagnostic and usage data. This data is used to keep the product up to date, improve the update experience, and improve the quality and security of the product.

No data is sent to the service when the service connection point is in offline mode. When you switch to online mode or use the service connection tool, it sends data to the service to check for updates.

You can also choose the level of data that Configuration Manager collects. For more information, see [Levels of diagnostic usage data](/configmgr/core/plan-design/diagnostics/levels-overview).

## <a name="bkmk_retention"></a> What is the data retention period?

Microsoft stores Configuration Manager diagnostic and usage data for one year.

## <a name="bkmk_update"></a> Is diagnostics and usage data sent when setup runs?

No. Diagnostics and usage data is only sent after the site is installed and operational.

## <a name="bkmk_frequency"></a> How frequently is the data sent?

The SQL stored procedures run every seven days from the date you installed the site.

- In online mode, the service connection point uploads the data after the queries run.

- In offline mode, you use the service connection tool to upload the data. (The data isn't initially available for offline use until seven days after you install the site.)  

## <a name="bkmk_network"></a> Can the data be used to form a network map?

No. This data doesn't include any network details, such as IP addresses or detailed geographic information. For more information, see [Levels of diagnostic usage data](/configmgr/core/plan-design/diagnostics/levels-overview#bkmk_versions), and find more detail for the version you're using.

The data does include time zone information from each site. This information can provide insight into the broad geolocation and global dispersion of sites in a hierarchy.

## <a name="bkmk_tables"></a> Can you see data in custom SQL tables?

No. Configuration Manager collects diagnostics and usage data via SQL stored procedures. These stored procedures run against default product tables in the database. All of these SQL tables are prefixed with **TEL_**. As part of the SQL schema detection query, all table names are hashed for comparison against the known defaults. This behavior determines that custom tables exist in the database. The presence of custom tables informs Microsoft that you extended the database schema from the default. It doesn't include any of the data stored within those tables.

## <a name="bkmk_databases"></a> Can you see other databases?

No. The stored procedures to collect data are limited to the Configuration Manager site database. Microsoft can't see the names of other databases, or any data in other databases.

## <a name="bkmk_cloud"></a> Is any data sent to other integrated cloud services?

Yes, when you integrate those services with Configuration Manager. As part of the interaction with any cloud service, Configuration Manager sends some data to that service. This data is specific to that cloud service, and separate from Configuration Manager diagnostics and usage data. For more information on the specific data used in the interaction with another cloud service, see the documentation for that service.

For example, the following cloud services are a part of Microsoft Endpoint Manager:

- [Desktop Analytics data privacy](/configmgr/desktop-analytics/privacy)
- [Privacy and personal data in Intune](https://docs.microsoft.com/intune/protect/privacy-personal-data)
- [Windows Autopilot requirements](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-autopilot-requirements)

## <a name="bkmk_personal"></a> Does Configuration Manager collect any personal data?

No. Configuration doesn't collect or transmit any personal data, customer data, or customer-authored data. It's an on-premises product that you directly deploy, manage, and operate. The diagnostics and usage data that Microsoft collects improves the installation experience, quality, and security of future releases.

For more information about Configuration Manager data, see [Levels of diagnostic usage data](/configmgr/core/plan-design/diagnostics/levels-overview).
