---
title: "Use of diagnostics data"
titleSuffix: "Configuration Manager"
description: "Learn about how Microsoft uses the diagnostics and usage data that System Center Configuration Manager collects."
ms.custom: na
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a8021bc8-2799-41f4-83c2-e27d1242028c
caps.latest.revision: 5
author: aczechowski
ms.author: aaroncz
manager: angrobe

---
# How diagnostics and usage data is used for System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Diagnostic and usage data that System Center Configuration Manager collects provides Microsoft nearly immediate feedback about how the product is working and is used to adjust future updates. We are also able to see configuration data that helps us engineer and test the configurations that are in production. For example:  

-   The Windows server versions that are used by site servers  

-   The installed language packs  

-   The delta of the SQL schema against the product default  

This data helps the engineering team plan future tests to ensure the best experience for the most common configurations. As updates to Configuration Manager are released on a faster cadence (to better support quickly moving technologies such as Windows 10 and Microsoft Intune), this data is crucial to quickly adjust and adapt.  

Equally important is how the diagnostics and usage data is not used. Microsoft does not use this data for:  

-   Licensing audits, such as comparing customer usage against license agreements  

-   Auditing of products that are out of support  

-   Advertising based on available data such as feature usage or geolocation (time zone)  

##  <a name="bkmk_improve"></a> Examples of how diagnostics and usage data improves the product  
Microsoft uses available data to improve to the product. Following are a few examples:  

-   **Revised support for older server operating systems:**  

     The initial support offered by the current branch of System Center Configuration Manager limited the support timeline for Windows Server 2008 R2. After examining the usage data from customers who had upgraded to the Configuration Manager current branch, we identified the need to revise and extend this timeline to support customers who still use this server operating system to host site servers and site system roles.  

-   **Improved prerequisite checks:**  

     Based on the usage data, we have improved the prerequisite checks for installing an update to remove obsolete rules, account for additional cases, and, in some cases, to auto-remediate some issues.  
