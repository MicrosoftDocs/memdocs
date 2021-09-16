---
title: Administrator checklist for power management
titleSuffix: Configuration Manager
description: Use the administrator checklist to help you plan for and implement power management in Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.localizationpriority: medium
---
# Administrator checklist for power management in Configuration Manager

*Applies to: Configuration Manager (current branch)*

This administrator checklist provides the recommended steps for using Configuration Manager power management in your organization.  

## Configuring power management  
 Use these steps to help you configure your hierarchy to collect power management information from client computers.  

> [!IMPORTANT]  
>  Do not apply power plans to computers in your hierarchy until you have collected and analyzed power data from client computers. If you apply new power management settings to computers without first examining the existing settings, this might lead to an increase in power consumption.  

|Task|Details|  
|----------|-------------|  
|Review the power management concepts in the Configuration Manager documentation library.|See [Introduction to power management](introduction-to-power-management.md).|  
|Review the power management prerequisites in the Configuration Manager documentation library.|See [Prerequisites for power management](prerequisites-for-power-management.md).|  
|Review the best practices information for power management.|See [Best practices for power management](best-practices-for-power-management.md).|  
|Configure your collections to manage power consumption from computers within your environment.|Use the **Collection for reporting of baseline data**, **Collection for reporting of baseline data**,   **Collection of computers incapable of power management**, **Collections of computers to which power plans will be applied**, **Collections of computers to which power plans will be applied**, and **Collections of computers that are running Windows Server** to help you manage power settings for computers in your hierarchy. You can create multiple collections and apply different power plans to each collection.|  
|Enable power management.|Before you can begin to use power management, you must enable it and configure the required client settings. For more information, see [Configuring power management](configuring-power-management.md).|  
|Collect power management information from client computers.|Power management data is reported by clients through Configuration Manager hardware inventory. Depending on the hardware inventory schedule that you have configured, it might take some time to retrieve inventory from all client computers.|  

## Monitoring and planning phase  

|Task|Details|  
|----------|-------------|  
|Run the report **Computer Activity**.|The **Computer Activity** report displays a graph showing monitor, computer, and user activity for a specified collection over a specified time period. This report links to the **Computer Activity Details** report which displays the sleep and wake capabilities of computers in the specified collection. For more information, see [How to monitor and plan for power management](monitor-and-plan-for-power-management.md).|  
|Run the report **Energy Consumption** or **Energy Consumption by Day**.|The **Energy Consumption** and **Energy Consumption by Day** reports display the total monthly power consumption in kilowatt per hour (kWh) for a specified collection over a specified time period. For more information, see [How to monitor and plan for power management](monitor-and-plan-for-power-management.md).|  
|Run the report **Environmental Impact** or  **Environmental Impact by Day**.|The **Environmental Impact** and **Environmental Impact by Day** reports display a graph showing carbon dioxide (CO2) emissions saved by a specified collection of computers for a specified period of time. For more information, see [How to monitor and plan for power management](monitor-and-plan-for-power-management.md).|  
|Run the report **Energy Cost** or **Energy Cost by Day**.|The **Energy Cost** and **Energy Cost by Day** reports display the total power consumption cost for a specified period of time. For more information, see [How to monitor and plan for power management](monitor-and-plan-for-power-management.md).|  
|Run the report **Power Capabilities**.|The **Power Capabilities** report displays the power management capabilities of computers in the specified collection. For more information, see [How to monitor and plan for power management](monitor-and-plan-for-power-management.md).|  
|Run the report **Power Settings**.|The **Power Settings** report displays an aggregated list of the current power settings used by computers in a specified collection. For more information, see [How to monitor and plan for power management](monitor-and-plan-for-power-management.md).|  
|Exclude any required collections of computers from power management.|See [Configuring power management](configuring-power-management.md).|  

> [!IMPORTANT]  
>  Ensure that you save the information from power management reports generated during the monitoring and planning phase. You can compare this data to power management information generated during the enforcement and compliance phases to help you evaluate, the power usage, power cost and environmental impact savings from applying a power plan to computers in your hierarchy.  

## Enforcement phase  

|Task|Details|  
|----------|-------------|  
|Select existing power plans or create new power plans for collections of computers in your organization.|See [How to create and apply power plans](create-and-apply-power-plans.md).|  
|Apply these power plans to computers.|See [How to create and apply power plans](create-and-apply-power-plans.md).|  

## Compliance phase  

|Task|Details|  
|----------|-------------|  
|Run the report **Computer Activity**.|The **Computer Activity** report displays a graph showing monitor, computer, and user activity for a specified collection over a specified time period. This report links to the **Power Computer Activity Details** report which displays the sleep and wake capabilities of computers in the specified collection. For more information, see [How to monitor and plan for power management](monitor-and-plan-for-power-management.md).|  
|Run the report **Energy Consumption** or **Energy Consumption by Day**.|The **Energy Consumption** and **Energy Consumption by Day** reports display the total monthly power consumption in kilowatt per hour (kWh) for a specified collection over a specified time period. For more information, see [How to monitor and plan for power management](monitor-and-plan-for-power-management.md).|  
|Run the report **Environmental Impact** or **Environmental Impact by Day**.|The **Environmental Impact** and **Environmental Impact by Day** reports display a graph showing carbon dioxide (CO2) emissions saved by a specified collection of computers for a specified period of time. For more information, see [How to monitor and plan for power management](monitor-and-plan-for-power-management.md).|  
|Run the report **Energy Cost** or **Energy Cost by Day**.|The **Energy Cost** and **Energy Cost by Day** reports display the total power consumption cost for a specified period of time. For more information, see [How to monitor and plan for power management](monitor-and-plan-for-power-management.md).|  

## Troubleshooting  

|Task|Details|  
|----------|-------------|  
|If computers in your hierarchy have not entered sleep or hibernate, run the report **Insomnia Report** to display possible causes.|The **Insomnia Report** displays a list of common causes that prevented computers from entering sleep or hibernate and the number of computers affected by each cause for a specified time period. For more information, see [How to monitor and plan for power management](monitor-and-plan-for-power-management.md).|  
|If multiple power plans are applied to one computer, then the least restrictive power plan is applied. Run the report **Computers with Multiple Power Plans** to see computers with multiple power plans applied.|See **Computers with Multiple Power Plans** in [How to monitor and plan for power management](monitor-and-plan-for-power-management.md).|  
