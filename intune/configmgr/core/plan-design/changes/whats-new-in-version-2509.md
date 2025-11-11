---
title: What's new in version 2509
titleSuffix: Configuration Manager
description: Get details about changes and new capabilities introduced in version 2509 of Configuration Manager current branch.
ms.date: 11/11/2025
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: whats-new
author: bhuney
ms.author: brianhun
manager: dougeby
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart
---

# What's new in version 2509 of Configuration Manager current branch

*Applies to: Configuration Manager (current branch)*

Update 2509 for Configuration Manager current branch is available as an in-console update. Apply this update on sites that run version 2309 or later.

Always review the latest checklist for installing this update. For more information, see [Checklist for installing update 2509](../../servers/manage/checklist-for-installing-update-2509.md). After you update a site, also review the [Post-update checklist](../../servers/manage/checklist-for-installing-update-2509.md#post-update-checklist).

To take full advantage of new Configuration Manager changes, after you update the site, also update clients to the latest version. New functionality appears in the Configuration Manager console when you update the site and console, but the complete scenario isn't functional until the client version is also the latest.

## General enhancements

As part of Microsoft's Secure Future Initiative (SFI) the 2509 version of Configuration Manager focuses on security and quality updates. For more information, see the [Microsoft Trust Center](https://www.microsoft.com/trust-center/security/secure-future-initiative).
For a list of significant customer-reported issues resolved in this release, see the [Summary of changes in Configuration Manager version 2509](../../../hotfix/2509/31909343.md) knowledge base article.


## Known Issues

 - Upgrade SQL 2012 or 2014 Express, Standard, Enterprise edition to SQL 2016 or latest version. **VC++ Redistributable Version** needs to be upgraded to latest version on **Secondary sites**. [Download Latest Microsoft Visual C++ Redistributable Version](https://aka.ms/vs/17/release/vc_redist.x64.exe).

### Microsoft ODBC redistributable
 - The Microsoft ODBC redistributable component is updated to version **18.4.1.1** on all Site servers and Management Points.
 - ConfigMgrPreReq throws an error stalling the upgrade if it detects a version lower than 18.4.4.1.
    
    > INFO: Microsoft ODBC Driver 18 for SQL Server is installed but it is older than the required version.  
    > SQL client prerequisite missing for Configuration Manager setup.;    Error;    Install the Microsoft ODBC driver 18 for SQL setup from https://go.microsoft.com/fwlink/?linkid=2299909. More information https://go.microsoft.com/fwlink/?linkid=2226618


<!-- ## Deprecated features

Learn about support changes before they're implemented in [removed and deprecated items](deprecated/removed-and-deprecated.md).

 - MDT Integration with CM and Standalone is no longer supported with Configuration Manager deprecation first announced in December 2024 and planned end of support the first release after Oct 10, 2025. Customers should remove MDT Task sequence steps, followed by removing MDT integration, to avoid TS corruption and modification failures.

For more information, see [Removed and deprecated features for Configuration Manager.](deprecated/removed-and-deprecated-cmfeatures.md). -->

## Next steps
At this time, version 2509 is released for the early update ring. To install this update, you need to opt in. For more information, see [Early update ring](../../servers/manage/checklist-for-installing-update-2509.md#early-update-ring).

<!-- As of December 11, 2025, version 2509 is globally available for all customers to install. -->

When you're ready to install this version, see [Installing updates for Configuration Manager](../../servers/manage/updates.md) and [Checklist for installing update 2509](../../servers/manage/checklist-for-installing-update-2509.md).


> [!TIP]
> To install a new site, use a baseline version of Configuration Manager.
>
> Learn more about:
>
> - [Installing new sites](../../servers/deploy/install/installing-sites.md)
> - [Baseline and update versions](../../servers/manage/updates.md#bkmk_Baselines)

For known significant issues, see the [Release notes](../../servers/deploy/install/release-notes.md).

After you update a site, also review the [Post-update checklist](../../servers/manage/checklist-for-installing-update-2509.md#post-update-checklist).
