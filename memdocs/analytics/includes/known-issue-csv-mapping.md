---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: include
ms.date: 03/31/2022
ms.localizationpriority: medium
---
<!--Don't apply H2 in this include file since they are context driven by article. Used in startup-performance.md, work-from-anywhere.md, app-reliability.md, and scores.md files -->

When reporting data is exported to a `.csv` file, the exported data doesn't use the friendly names you're used to seeing in the online reports. Use the chart below to map the data in the exported file into the meaning of the value. 

**Application reliability report** </br>

- The `TotalAppUsageDuration` and `MeanTimeToFailure` columns in the `.csv` file are integer values with a unit of **minutes**
- A `MeanTimeToFailure` value of 2147483647 means `No crash events`

**Per device score report** </br>

- A value of `-1` or `-2` in the `EndpointAnalyticsScore`, `StartupPerformanceScore`, and `AppReliabilityScore` columns means the associated score is unavailable
- Health status: </br>
   |HealthStatus `.csv` value| Report value|
   |---|---|
   |0|Unknown|
   |1|Insufficient data|
   |2|Needs attention|
   |3|Meeting goals|

**Startup performance report** </br> 

The `CoreBootTime`, `GPBootTime`, `CoreLogonTime`, `GPLogonTime`, `DesktopUsableTime`, `Median`, and `TimePerProcess` columns are integer values with a unit of **seconds**.

**Work from anywhere report** </br>
- Column name in `.csv` file: UpgradeEligibility </br>
Report column name: Windows 11 readiness status </br>

   |`.csv` value| Report value|
   |---|---|
   |0|Upgraded|
   |1|Unknown|
   |2|Not capable|
   |3|Capable|

- Column name in `.csv` file: GraphDeviceIsManaged </br> Report column name: Azure AD registered
