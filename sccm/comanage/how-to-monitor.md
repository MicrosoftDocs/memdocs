---
title: Monitor co-management
titleSuffix: Configuration Manager
description: Use the co-management dashboard to review information about co-managed devices.
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: e83a7b0d-b381-4b4a-8eca-850385abbebb
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# How to monitor co-management in Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*


After you enable co-management, monitor co-management devices using the following methods:

- [Co-management dashboard](#co-management-dashboard)  

- [Deployment policies](#deployment-policies)

- [WMI device data](#wmi-device-data)



## Co-management dashboard

Starting in version 1802, view a dashboard with information about co-management. The dashboard helps you review machines that are co-managed in your environment. The graphs can help identify devices that might need attention.<!--1356648-->

In the Configuration Manager console, go to the **Monitoring** workspace, and select the **Co-management** node.

Starting in version 1810, the co-management dashboard is enhanced with more detailed information. <!--1358980-->

![Screenshot of the co-management dashboard](media/co-management-dashboard.png)


### Co-managed devices

*Applies to versions 1802 and 1806*

Shows the percentage of co-managed devices throughout your environment.

![Co-managed devices tile](media/co-management-dashboard/Percent-Co-managed-graph.PNG)


### Client OS distribution

*Applies to all versions* 

Shows the number of client devices per OS by version. It uses the following groupings:  
- Windows 7 & 8.x  
- Windows 10 lower than 1709  
- Windows 10 1709 and above  

    > [!Tip]  
    > Windows 10, version 1709 and later, is a prerequisite for co-management.  

Hover over a graph section to show the percentage of devices in that OS group.

![Client OS distribution tile](media/co-management-dashboard/Co-management-OS-distribution-graph.PNG)


### Co-management status (donut)

*Applies to versions 1802 and 1806*

Shows the breakdown of device success or failure in the following categories:
- Success, hybrid Azure AD Joined  
- Success, Azure AD Joined  
- Failure: Auto-enrollment failed  

Hover over a graph section to show the percentage of devices in that category. 

![Co-management status (donut) tile](media/co-management-dashboard/Co-management-status-graph.PNG)

Select a graph section to view the device list for that category.

![Enrollment failure device list](media/co-management-dashboard/Enrollment-Failure_Device-List.PNG)


### Co-management status (funnel)

*Applies to version 1810 and later*

A funnel chart that shows the number of devices with the following states from the enrollment process:  
- Eligible devices  
- Scheduled  
- Enrollment initiated  
- Enrolled  

![Co-management status (funnel) tile](media/co-management-dashboard/1358980-status-funnel.png)


### Co-management enrollment status

*Applies to version 1810 and later*

Shows the breakdown of device status in the following categories:
- Success, hybrid Azure AD-joined  
- Success, Azure AD-joined  
- Enrolling, hybrid Azure AD-joined  
- Failure, hybrid Azure AD-joined  
- Failure, Azure AD-joined  
- Pending user sign in  

Select a state in the tile to drill through to a list of devices in that state.  

![Co-management enrollment status tile](media/co-management-dashboard/1358980-enrollment-status.png)


### Enrollment errors

*Applies to version 1810 and later*

A table that shows the count of enrollment errors from devices.  


### Workload transition

*Applies to all versions*

Displays a bar chart with the number of devices that you've transitioned to Microsoft Intune for the available workloads. 

The list of workloads varies by version of Configuration Manager. For more information, see [Workloads able to be transitioned to Intune](/sccm/comanage/workloads).

Hover over a chart section to show the number of devices transitioned for the workload. 

![Workload transition bar graph](media/co-management-dashboard/Workload-Transition.PNG)



## Deployment policies

Two policies are created in the **Deployments** node of the **Monitoring** workspace. One policy is for the pilot group and one for production. These policies report only the number of devices where Configuration Manager has applied the policy. They don't consider how many devices are enrolled in Intune, which is a requirement before devices can be co-managed.  



## WMI device data

Query the **SMS_Client_ComanagementState** WMI class. You can create custom collections in Configuration Manager, which help determine the status of your co-management deployment. For more information on creating custom collections, see [How to create collections](/sccm/core/clients/manage/collections/create-collections). 

The following fields are available in the WMI class:  

- **MachineId**: A unique device ID for the Configuration Manager client  

- **MDMEnrolled**: Specifies whether the device is MDM-enrolled  

- **Authority**: The authority for which the device is enrolled  

- **ComgmtPolicyPresent**: Specifies whether the Configuration Manager co-management policy exists on the client. If the **MDMEnrolled** value is **0**, the device isn't co-managed regardless whether the co-management policy exists on the client.  

A device is co-managed when the **MDMEnrolled** field and **ComgmtPolicyPresent** fields both have a value of **1**.  
