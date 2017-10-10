---
title: "Reporting best practices"
titleSuffix: "Configuration Manager"
description: "Read some helpful tips about using the reporting capability of System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 64f9d931-33f1-456f-a4e4-0ec077465bd0
caps.latest.revision: 4
caps.handback.revision: 0
author: Dougebyms.author: dougebymanager: angrobe

---
# Best practices for reporting in System Center Configuration Manager*Applies to: System Center Configuration Manager (Current Branch)*
Use the following best practices for reporting in System Center Configuration Manager:  

## For best performance, install the reporting services point on a remote site system server  
 Although you can install the reporting services point on the site server or a remote site system, performance is increased when you install the reporting services point on a remote site system server.  

## Optimize SQL Server Reporting Services queries  
 Typically, any reporting delays are because of the time it takes to run queries and retrieve the results. If you are using Microsoft SQL Server, tools such as Query Analyzer and Profiler can help you optimize queries.  

## Schedule report subscription processing to run outside standard office hours  
 Whenever possible, schedule report subscription processing to run outside normal office standard hours to minimize the CPU processing on the Configuration Manager site database server. This practice also improves availability for unpredicted report requests.  

## Next steps
[Configure reporting](configuring-reporting.md)
