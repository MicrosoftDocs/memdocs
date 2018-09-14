---
title: "Co-management Dashboard"
titleSuffix: Configuraton Manager
description: "Review information about co-management using the dashboard."
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: e83a7b0d-b381-4b4a-8eca-850385abbebb
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Co-management dashboard in System Center Configuration Manager
*Applies to: System Center Configuration Manager (Current Branch)*

Beginning in version 1802, you can view a dashboard with information about co-management. The dashboard helps you review machines that are co-managed in your environment. The graphs can help identify devices that might need attention.<!--1356648-->

## Open the co-management dashboard
To open the co-management dashboard, use the following steps: 

1. Open the Configuration Manager console. 
2. Click on the **Monitoring** node. 
3. To load the dashboard, click on **Co-management**.

## Reviewing information in the co-management dashboard

The co-management dashboard shows four graphs for your environment. 

- **Co-managed devices** -Gives you the percentage of co-managed devices throughout your environment.

    ![Co-managed devices graph](media\co-management-dashboard\Percent-Co-managed-graph.PNG)

- **Client OS distribution** -Shows the number of client devices per OS by version. The following groupings are used: </br>
    - Windows 7 & 8.x
    - Windows 10 lower than 1709
    - Windows 10 1709 and above

         > [!NOTE] 
         > Windows 10, version 1709 and later, is a prerequisite for co-management.

     Hovering over a graph section will give you the percentage of devices in the OS grouping selected.

     ![Graph of Client OS distribution](media\co-management-dashboard\Co-management-OS-distribution-graph.PNG)

- **Co-management status**- The breakdown of device success or failure in the following categories:
    - Success, hybrid Azure AD Joined
    - Success, Azure AD Joined
    - Failure: Auto-enrollment failed
    
     Hovering over a graph section gives you the percentage of devices in the category. 

     ![Status graph for co-management](media\co-management-dashboard\Co-management-status-graph.PNG)

     Clicking on a graph section takes you to a device list for the category.
 
     ![Enrollment failure device list](media\co-management-dashboard\Enrollment-Failure_Device-List.PNG)


- **Workload transition**- Displays a bar chart with the number of devices that you transitioned to Microsoft Intune for the four available workloads:
    - Compliance Policies
    - Resource Access
    - Windows Update for Business
    - Endpoint Protection

     Hovering over a chart section will give you the number of devices transitioned for the workload. 
     ![Workload transition bar graph](media\co-management-dashboard\Workload-Transition.PNG)


## Next steps

For more information about co-management, see:
 - [Co-management for Windows 10 devices](/sccm/core/clients/manage/co-management-overview)
 - [Prepare Windows 10 devices for co-management](/sccm/core/clients/manage/co-management-prepare)

    
