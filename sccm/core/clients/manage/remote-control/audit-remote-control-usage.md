---
title: "Audit remote control usage"
titleSuffix: "Configuration Manager"
description: "Audit remote control use in System Center Configuration Manager."
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5c975e69-0cc0-4afd-b7fb-b7182162a933
caps.latest.revision: 5
caps.handback.revision: 0
author: arob98
ms.author: angrobe
manager: angrobe

---
# How to audit remote control usage in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

You can use System Center Configuration Manager reports to view audit information for remote control.  

 For more information about how to configure reporting in Configuration Manager, see [Reporting in System Center Configuration Manager](../../../../core/servers/manage/reporting.md).  

 The following two reports are available with the category **Status Messages - Audit**:  

-   **Remote Control - All computers remote controlled by a specific user** - Displays a summary of remote control activity that a specific user initiated.  

-   **Remote Control - All remote control information** - Displays a summary of status messages about remote control of client computers.  

### To run the report Remote Control - All computers remote controlled by a specific user  

1.  In the Configuration Manager console, click **Monitoring**.  

2.  In the **Monitoring** workspace, expand **Reporting**, and then click **Reports**.  

3.  In the **Reports** node, click the **Category** column to sort the reports so that you can more easily find the reports in the category **Status Messages - Audit**.  

4.  Select the report **Remote Control - All computers remote controlled by a specific user**, and then, on the **Home** tab, in the **Report Group**, click **Run**.  

5.  In the **User Name** list of the **Remote Control - All computers remote controlled by a specific user**, specify the user that you want to report audit information for, and then click **View Report**.  

6.  When you have finished viewing the data in the report, close the report window.  

### To run the report Remote Control - All remote control information  

1.  In the Configuration Manager console, click **Monitoring**.  

2.  In the **Monitoring** workspace, expand **Reporting**, and then click **Reports**.  

3.  In the **Reports** node, click the **Category** column to sort the reports so that you can more easily find the reports in the category **Status Messages - Audit**.  

4.  Select the report **Remote Control - All remote control information**, and then, on the **Home** tab, in the **Report Group**, click **Run** to open the **Remote Control - All remote control information** window.  

5.  When you have finished viewing data in the report, close the report window.  
