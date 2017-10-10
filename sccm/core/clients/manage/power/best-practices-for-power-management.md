---
title: "Best practices for power management"
titleSuffix: "Configuration Manager"
description: "Get best practices for power management in System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9f7142e1-c972-4384-853b-2da1568cb3e3
caps.latest.revision: 5
caps.handback.revision: 0
author: arob98ms.author: angrobemanager: angrobe

---
# Best practices for power management in System Center Configuration Manager*Applies to: System Center Configuration Manager (Current Branch)*
Use the following best practices for power management in System Center Configuration Manager.  

## Perform the monitoring phase at a representative time  
 The monitoring phase of power management provides you with information about the power consumption, activity, power management capabilities, and environmental impact of computers in your organization. Ensure that you choose a representative time to perform the monitoring phase. For example, performing the monitoring phase over a public holiday does not provide a realistic report on computer power usage.  

## Create a control collection of computers with no power plans applied  
 Create two collections of computers to help you monitor the effects of applying power plans to computers. The first collection should contain the majority of the computers to which you want to apply power settings and the other collection (the control collection) should contain the remaining computers. Apply the required power management plan to the collection containing the majority of computers. You can then run reports to compare the power cost, power usage and environmental impact of the computers to which you have applied power settings with the control collection that you have not applied power settings to.  

## Run the Power Settings report before you apply a power management plan  
 Before you apply a power management plan to a collection of computers, run the **Power Settings** report to help you understand the power management settings that are already configured on computers in the collection. If you apply new power management settings to computers without first examining the existing settings, this might lead to an increase in power consumption.  

## Exclude servers from power management  
 Power management for computers that run Windows Server is not supported (although power usage data is collected). Ensure that you add servers to a collection and exclude it from power management.  

## Exclude computers that you do not want to manage  
 If you have computers that you do not want to manage with power management, add these to a collection and ensure that the collection is excluded from power management.  

 Examples of computers you might want to exclude from power management include:  

-   Computers that must remain turned on.  

-   Computers that users need to connect to by using Remote Desktop Connection.  

-   Computers that cannot use power management.  

-   Computers that have the distribution point site system role.  

-   Public computers such as kiosk computers, information displays or monitoring consoles where the computer and the monitor must always be turned on.  

 For more information, see [Configuring power management in System Center Configuration Manager](../../../../core/clients/manage/power/configuring-power-management.md).  

## First, apply power plans to a test collection of computers  
 Always test the effect of applying a power management plan on a test collection of computers before you apply the power plan to a larger collection of computers.  

 Power settings applied to computers running Windows XP or Windows Server 2003 are not reverted to their original values even if you exclude the computer from power management. On later versions of Windows, excluding a computer from power management causes all power settings to be reverted to their original values. You cannot revert individual power settings to their original values.  

## Apply power plan settings individually  
 Monitor the effect of applying each power setting before you apply the next one to ensure each setting has the required effect. For more information about power plan settings, see [Available power management plan settings](../../../../core/clients/manage/power/create-and-apply-power-plans.md#BKMK_Plans) in the topic [How to create and apply power plans in System Center Configuration Manager](../../../../core/clients/manage/power/create-and-apply-power-plans.md).  

## Regularly monitor computers to see if they have multiple power plans applied  
 Power management includes a report that displays computers that have more than one power plan applied.  

 If a computer is a member of multiple collections, each applying different power plans, then the following actions will be taken:  

-   Power plan: If multiple values for power settings are applied to a computer, the least restrictive value is used.  

-   Wakeup time: If multiple wakeup times are applied to a desktop computer, the time closest to midnight will be used.  

     For more information, see [Computers with Multiple Power Plans](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md#BKMK_Multiple) in the topic [How to monitor and plan for power management in System Center Configuration Manager](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md). For more information about how power management resolves conflicts, see [How to create and apply power plans in System Center Configuration Manager](../../../../core/clients/manage/power/create-and-apply-power-plans.md).  

## Save or export power management information during the monitoring and planning phase of power management  
 Power management information used by daily reports is retained in the Configuration Manager site database for 31 days.  

 Power management information used by monthly reports is retained in the Configuration Manager site database for 13 months.  

 When you run reports during the monitoring and planning and compliance phases of power management, save or export the results from any reports for which you want to retain the data for later comparison in case they are later removed by Configuration Manager.  
