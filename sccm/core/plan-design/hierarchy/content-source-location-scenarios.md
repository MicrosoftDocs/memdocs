---
title: "Content source location"
titleSuffix: "Configuration Manager"
description: "Learn about the System Center Configuration Manager settings that enable clients to find content on a slow network."
ms.custom: na
ms.date: 1/3/2017 
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 70b5cbc0-64ba-49bd-8b34-fb4c09b2b95b
caps.latest.revision: 3
author: Brenduns
ms.author: brenduns
manager: angrobe
---
# Content source location scenarios in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Prior to version 1610, System Center Configuration Manager supported several settings that combined to define how and where clients find content when they are on a slow network. The possible combinations affect the content location clients use, and whether they can successfully use a fallback location when a preferred source for content is not available.  

> [!IMPORTANT]  
> **If your sites run version 1511, 1602, or 1606**, the information in this topic applies to your infrastructure. Also see [Boundary groups for versions 1511,1602, and 1606](/sccm/core/servers/deploy/configure/boundary-groups-for-1511-1602-and-1606) for information that's specific to boundary groups with these versions of Configuration Manager.
>
> **If your sites run version 1610 or later**, use the information in [Define site boundaries and boundary groups for System Center Configuration Manager](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#boundary-groups) to understand how your clients find distribution points that have available content.





**The following three settings define the behavior when clients request content:**

-  **Allow fallback source location for content** (enabled or not enabled): This is an option that you can enable on the **Boundary Groups** tab of a distribution point. This allows the client to use a distribution point that's configured as a fallback location when content is not available on a preferred distribution point.  

 - **Deployment behavior for network connection speed**: Each deployment is configured with one of the following behaviors to use when the connection to the distribution point is slow:  

    -   **Download content from the distribution point and run it locally**  

    -   **Do not download content**: This option is only used when a client uses a fallback location to obtain content.  

    The connection speed for a distribution point is configured on the **References** tab of a boundary group, and is specific to that boundary group.  

 -  **On-demand package distribution** (to preferred distribution points): This is enabled when you select the option **Distribute the content for this package to preferred distribution points** on the **Distribution Settings** tab of a package's or application's properties. When enabled, this option directs Configuration Manager to automatically copy the content to a preferred distribution point that does not yet have the content after a client requests that content from that distribution point.  


 **The following requirements apply to all scenarios:**


-   Content is available on a fallback distribution point  

-   Distribution points are online and accessible  


## Scenario 1  
 Applies when the following configurations exist:  

-   **Content is available on a preferred distribution point**  

-   **Allow fallback**: Not enabled  

-   **Deployment behavior for a slow network**: Any configuration  


**Details:** (The configuration for on-demand package distribution is not relevant in this scenario.)  

1.  The client sends a content request to the management point.  

2.  A content location list is returned to the client from the management point with the preferred distribution points that contain the content.  

3.  The client downloads the content from a preferred distribution point on the list.  

## Scenario 2  
 The following configurations exist:  

-   **Content is available on a preferred distribution point**  

-   **Allow fallback**: Enabled  

-   **Deployment behavior for a slow network**: Do not download content  


**Details:** (The configuration for on-demand package distribution is not relevant in this scenario.)  

1.  The client sends a content request to the management point. The client includes a flag with the request that indicates that fallback distribution points are allowed.  

2.  A content location list is returned to the client from the management point with the preferred distribution points and fallback distribution points that contain the content.  

3.  The client downloads the content from a preferred distribution point on the list.  

## Scenario 3  
 The following configurations exist:  

-   **Content is  available on a preferred distribution point**  

-   **Allow fallback**: Enabled  

-   **Deployment behavior for a slow network**: Download and install content  


**Details:** (The configuration for on-demand package distribution is not relevant in this scenario.)  

1.  The client sends a content request to the management point. The client includes a flag with the request that indicates that fallback distribution points are allowed.  

2.  A content location list is returned to the client from the management point with the preferred distribution points and fallback distribution points that contain the content.  

3.  The client downloads the content from a preferred distribution point on the list.  

## Scenario 4  
 The following configurations exist:  

-   **Content is not available on a preferred distribution point**  

-   **Distribute the content for this package to preferred distribution points** is not enabled  

-   **Allow fallback**: Not enabled  

-   **Deployment behavior for a slow network**: Any configuration  


**Details:**  

1.  The client sends a content request to the management point.  

2.  A content location list is returned to the client from the management point with the preferred distribution points that have the content. There are no preferred distribution points in the list.  

3.  The client fails with the message **Content is not available** and goes into retry mode. A new content request is started every hour.  

## Scenario 5  
 The following configurations exist:  

-   **Content is not available on a preferred distribution point**  

-   **Distribute the content for this package to preferred distribution points** is not enabled  

-   **Allow fallback**: Enabled  

-   **Deployment behavior for a slow network**: Do not download content  


**Details:**  

1.  The client sends a content request to the management point. The client includes a flag with the request that indicates that fallback distribution points are allowed.  

2.  A content location list is returned to the client from the management point with the preferred distribution points and fallback distribution points that have the content. There are no preferred distribution points that have the content, but at least one fallback distribution point has the content.  

3.  The content is not downloaded because the deployment property for when the client uses a fallback distribution point is set to **Do not download content** (which is used when clients fall back to obtain the content). The client fails with the message **Content is not available** and goes into retry mode. The client makes a new content request every hour.  

## Scenario 6  
 The following configurations exist:  

-   **Content is not available on a preferred distribution point**  

-   **Distribute the content for this package to preferred distribution points** is not enabled  

-   **Allow fallback**: Enabled  

-   **Deployment behavior for a slow network**: Download and install content  


**Details:**  

1.  The client sends a content request to the management point. The client includes a flag with the request that indicates that fallback distribution points are enabled.  

2.  A content location list is returned to the client from the management point with the preferred distribution points and fallback distribution points that have the content. There are no preferred distribution points that have the content, but at least one fallback distribution point that has the content.  

3.  The content is downloaded from a fallback distribution point on the list because the deployment property for when the client uses a fallback distribution point is set to **Download and install the content**.  

## Scenario 7  
 The following configurations exist:  

-   **Content is not available on a preferred distribution point**  

-   **Distribute the content for this package to preferred distribution points** is enabled  

-   **Allow fallback**: Not enabled  

-   **Deployment behavior for a slow network**: Any configuration  


**Details:**  

1.  The client sends a content request to the management point.  

2.  A content location list is returned to the client from the management point with the preferred distribution points that have the content. There are no preferred distribution points that have the content.  

3.  The client fails with the message **Content is not available** and goes into retry mode. A new content request is made every hour.  

4.  The management point creates a trigger for Distribution Manager to distribute the content to all preferred distribution points for the client that made the content request.  

5.  Distribution Manager distributes the content to all preferred distribution points. In most cases, the content is successfully distributed to the preferred distribution points within an hour.  

6.  A new content request is initiated by the client to the management point.  

7.  A content location list is returned to the client from the management point with the preferred distribution points that have the content. The client downloads the content from a preferred distribution point on the list.  

## Scenario 8  
 The following configurations exist:  

-   **Content is not available on a preferred distribution point**  

-   **Distribute the content for this package to preferred distribution points** is enabled  

-   **Allow fallback**: Enabled  

-   **Deployment behavior for a slow network**: Do not download content  


**Details:**  

1.  The client sends a content request to the management point. The client includes a flag with the request that indicates that fallback distribution points are allowed.  

2.  A content location list is returned to the client from the management point with the preferred distribution points and fallback distribution points that have the content. There are no preferred distribution points that have the content, but at least one fallback distribution point has the content.  

3.  The content is not downloaded because the deployment property for when the client uses a fallback distribution point is set to **Do not download**. The client fails with the message **Content is not available** and goes into retry mode. The client makes a new content request every hour.  

4.  The management point creates a trigger for Distribution Manager to distribute the content to all preferred distribution points for the client that made the content request.  

5.  Distribution Manager distributes the content to all preferred distribution points. In most cases, the content is successfully distributed to the preferred distribution points within an hour.  

6.  A new content request is initiated by the client to the management point.  

7.  A content location list is returned to the client from the management point with the preferred distribution points that have the content.  

8.  The client downloads the content from a preferred distribution point on the list.  

## Scenario 9  
 The following configurations exist:  

-   **Content is not available on a preferred distribution point**  

-   **Distribute the content for this package to preferred distribution points** is enabled  

-   **Allow fallback**: Enabled  

-   **Deployment behavior for a slow network**: Download and install content  


**Details:**  

1.  The client sends a content request to the management point. The client includes a flag with the request that indicates that fallback distribution points are allowed.  

2.  A content location list is returned to the client from the management point with the preferred distribution points and fallback distribution points that have the content. There are no preferred distribution points that have the content, but at least one fallback distribution point has the content.  

3.  The content is downloaded from a fallback distribution point on the list because the deployment property for when the client uses a fallback distribution point is set to **Download and install the content**. This deployment setting enables a client that must use a fallback content location to obtain the content from that location.  

4.  The management point creates a trigger for Distribution Manager to distribute the content to all preferred distribution points for the client that made the content request.  

5.  Distribution Manager distributes the content to all preferred distribution points, which enables additional clients to obtain the content without using a fallback distribution point.  
