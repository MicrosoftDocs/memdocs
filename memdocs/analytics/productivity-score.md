---
title: Endpoint analytics page in Microsoft Productivity Score
titleSuffix: Microsoft Endpoint Manager
description: Get details about endpoint analytics in Microsoft Productivity Score
ms.date: 03/03/2021
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: a98ec089-a85f-4b5b-bce5-ec0ffd84f318
author: mestew
ms.author: mstewart
manager: dougeby
---

# Endpoint analytics in Microsoft Productivity Score
<!--IN8529842-->
 Understanding how your devices contribute to your end user’s experience is critical to any digital transformation effort. Endpoint analytics information was added to the Microsoft productivity score to further your understanding. The **Endpoint analytics** page in [Microsoft Productivity Score](/microsoft-365/admin/productivity/productivity-score) shares organizational level insights with the other roles outside of Microsoft Endpoint Manager. The visibility and insights this provides in areas like device boot times and application reliability can help your users by highlighting potential issues within your organization. For instance, Endpoint analytics can expose a long sign-in process or issues with applications unexpectedly stopping.  

## Endpoint analytics page in the Productivity Score report

Endpoint analytics contains great insights, but most people couldn't see them since it requires access to the Microsoft Endpoint Manager admin center. If you happened to be an Intune Admin or a Global Administrator, you could display the analytics. However, other users of Microsoft Productivity Score may have been unaware this information existed. Displaying these insights to Microsoft Productivity Score users allows them to use the data to help drive transformation efforts across your organization.

:::image type="content" source="media/8529842-endpoint-analytics-microsoft-365-admin-center.png" alt-text="Endpoint analytics in the Microsoft 365 admin center" lightbox="media/8529842-endpoint-analytics-microsoft-365-admin-center.png":::

The **Endpoint analytics** page looks similar to the other pages in Productivity Score, making it easy to dive right in. The following information is displayed on the **Endpoint analytics** page:

- The current Endpoint analytics score
- Endpoint analytics score over the past 180 days
- Startup performance scores

## About the Endpoint analytics scores

The **Endpoint analytics score** is a 50/50 weighted average of the [**Recommended software**](recommended-software.md) and [**Startup performance scores**](startup-performance.md).

[!INCLUDE [Endpoint analytics startup score](includes/startup-score.md)]

## Startup performance metrics

Selecting the **Learn more** link under the startup performance information give you additional details and a link to **View more in Microsoft Endpoint Manager**. The **Startup performance metrics** are averages of the following items: 

- **Average device startup time in seconds**
   - **Total boot time**: The combination of the **Group Policy phase** and the **Time to sign-in prompt**
   - **Group Policy phase**: The time spent querying and processing Group Policy
   - **Time to sign-in prompt**: Boot time minus the time spent processing Group Policy

- **Average sign-in time in seconds**
   - **Total sign-in time**: Total time for the **Group Policy phase**, **Time to desktop**, and **Time to responsive desktop**
   - **Group Policy phase**: The time spent querying and processing Group Policy
   - **Time to desktop**: The time it takes to reach the desktop but where background processes are still running, and users experience slower performance
   - **Time to responsive desktop**: Time where background processes are complete and CPU utilization is less than 50%

:::image type="content" source="media/8529842-startup-performance-metrics.png" alt-text="Endpoint analytics startup performance metrics" lightbox="media/8529842-startup-performance-metrics.png":::

## Known issues

### Unsupported roles

Currently, the following roles aren't supported:
- Exchange Administrator
- SharePoint Administrator
- Lync Administrator
## Next steps

For more information, see:
- [Recommended software](recommended-software.md) 
- [Startup performance scores](startup-performance.md)