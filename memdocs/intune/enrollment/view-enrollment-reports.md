---
# required metadata

title: View enrollment reports  
titleSuffix: Microsoft Intune 
description: Monitor and troubleshoot issues with enrollment restrictions and enrollment status page assignments.  
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 08/08/2022
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: 
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: maholdaa
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier1
- M365-identity-device-management
- highpri
---

# View enrollment reports

**Applies to**
* Android  
* iOS
* macOS 
* Windows 10
* Windows 11 


[!INCLUDE [azure_portal](../includes/azure_portal.md)]  

Your can use the following reports in the Microsoft Intune admin center to monitor and troubleshoot issues with enrollment restrictions and enrollment status page assignments:  

- Enrollment failures report  
- Troubleshooting + support page  
- Device enrollment page  

This article describes each report and how to access them in the admin center.  

## Enrollment failures report  
Use the enrollment failures report to view enrollment failures for all users or for select users. This report shows each failed enrollment attempt along with the date it occurred, reason for failure, OS, OS version, username, and enrollment method.  

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Monitor** > **Enrollment failures**.
2. Select **All users** or **Select user**, depending on the scenario you're troubleshooting.
3. Select a row in the table for more details about the failure and recommended remediation steps.  

    > [!div class="mx-imgBorder"]
    > ![Example image of the enrollment failures report, showing the enrollment failure details for a selected row.](./media/enrollment-restrictions-set/enrollment-failure-report-details-2112.png)  

## Troubleshooting + support page  
Use the enrollment failures report on the Troubleshooting + support page to view enrollment failures for a select user. This report shows every failed enrollment attempt the user encountered along with the date it occurred, reason for failure, OS, OS version, username, and enrollment method. You can also view other data about the user on this page, including all assignments, devices, and app protection statuses they're associated with.    

1. In the [admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Troubleshooting + support** > **Select user**.
2. Choose a user > **Select**. 
3. Under **Enrollment failures**, select a row to view more details about the failure and recommended remediation steps.  

## Device enrollment page
The device enrollment page shows the enrollment policies (both enrollment restriction and enrollment status page policies) applied to a device when it was first enrolled in Microsoft Intune. Use this report to help pinpoint the source of the failure, such as an unexpected policy, target, or filter. Data is available for iOS/iPadOS, macOS, and Windows devices, and includes: 

  * Profile name
  * User principal name
  * Profile type (either enrollment status page or device type enrollment restriction)
  * Priority
  * Target (either user or device) 
  * Filters, with a link to the filter evaluation results (only available if the enrollment policy was assigned using an assignment filter)  

To access report data:   

1. In the [admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **All devices**.
2. Select an enrolled iOS/iPadOS, macOS, or Windows device.  
3. Under **Monitor**, select **Enrollment**.  
4. Review the report data. 

    > [!div class="mx-imgBorder"]
    > ![Example image of the Device enrollment page, showing a table of enrollment profiles.](./media/enrollment-restrictions-set/enrollment-page-report-2112.png)  

>[!NOTE]
>Report data is only available for devices enrolled after the Microsoft Intune 2112 service release. No results are available for devices enrolled prior to that release.  