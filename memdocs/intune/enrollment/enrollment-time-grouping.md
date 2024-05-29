---
# required metadata

title: Set up enrollment time grouping    
titleSuffix: Microsoft Intune 
description: Overview and setup of the enrollment time grouping feature in Microsoft Intune. 
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 05/31/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: 
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier1
- M365-identity-device-management
- highpri
- highseo
---

# Enrollment time grouping in Microsoft Intune        

**Applies to**  

* Windows 10
* Windows 11  

Set up enrollment time grouping to speed up app and policy provisioning during device enrollment. With enrollment time grouping, you can preconfigure groups so that devices are added to a Microsoft Entra security group during enrollment, rather than after. The earlier grouping means that Intune can deliver the appropriate apps and policies to users and devices sooner, both reducing post-enrollment latency and improving time to productivity. Additionally, you can recategorize devices in static Microsoft Entra groups without the need to re-enroll them.   

If you don't configure enrollment time grouping, Microsoft Intune groups devices into Microsoft Entra security groups after enrollment. Then it delivers apps and policies. Intune can only determine the apps and policies a device needs after the device is grouped, so devices grouped this way often aren't ready for immediate use. It can take up to 8 hours post enrollment for devices to receive all apps and policies. 

This article provides an overview of enrollment time grouping, how to configure it, and feature limitations.  

## Role based access control (RBAC)  

To add Microsoft Entra groups to an enrollment profile, you must have the *enrollment time device membership assignment* permission. This permission is available for custom roles, under the **Enrollment programs** category in the Microsoft Intune admin center. For more information about creating custom roles, see [Role based access control](../fundamentals/role-based-access-control.md#custom-roles).  

To add Intune FPA as a security group owner, which is a required step for enrollment time grouping, you must meet one of the following prerequisites:  

 - Must be a Microsoft Entra Group Administrator, or another role with the *microsoft.directory/groups/owners/update* permission.  
 - Must be an existing owner of the Microsoft Entra security group. 

## Prerequisites   

Enrollment time grouping is supported on devices provisioned via Windows Autopilot device preparation policies. You must be able to access Microsoft Entra ID and the Microsoft Intune admin center.   

## Step 1: Create Microsoft Entra security group   

Create a Microsoft Entra security group for use in enrollment profiles. You don't need to add devices or users to this group right now.  

1. Sign in to the Microsoft Intune admin center. 
1. Go to **Groups** and select **New Group**.  
1. For group type, select **Security**.  
1. For membership type, select **Assigned**.  
1. Select owners. 
1. Search for **Intune**. Then add **Intune Provisioning Client**. If the option isn't available, run the following PowerShell command:  

    ```powershell  

    install-module azuread Connect-AzureAD` 
    New-AzureADServicePrincipal -AppId f1346770-5b25-470b-88bd-d5744ab7952c 

    ```
1. Select **Create** to complete group setup.  

After you configure enrollment time grouping in the enrollment profile, you can come back to this security group as neeed to add and remove devices. Any Intune administrator with the appropriate security group permissions can edit the security group. 
 
## Step 2: Configure enrollment time grouping in enrollment profile 

The enrollment time grouping feature only applies to new device enrollments. It doesn't affect or apply to devices that are already enrolled. 

You can add one static Microsoft Entra security group per enrollment profile. As an Intune admin, you can only add Microsoft Entra groups that are authorized in the scope group for your Intune role. Make sure scope groups and group tags are assigned to the appropriate roles so that admins can see the security group during profile creation. 

1. In the Microsoft Intune admin center, go to **Devices** >**Enrollment**.  
1. Select **Windows Autopilot device preparation policies** and create a new profile.  
1. When you get to the **Device group** step, select the Microsoft Entra security group you want to use for grouping. 
1. Select **Next** to complete the remaining steps in the profile.  
1. Then save the profile.   

After you save the profile, you can return to it at any time to edit group settings. If you remove a device from the group, Microsoft Intune reevaluates policy configurations and forces the device to check in to obtain new configurations.   

## Step 3: Enroll devices  

When devices assigned the enrollment profile enroll, they become members of the Microsoft Entra security group and start receiving apps and policies. After the admin or end user completes the initial device setup, they land on the home screen of the device. At this point, all targeted apps and policies should already be on the device or in the process of being installed.  

## Known issues and limitations  

Reporting for enrollment time grouping isn't currently available.  

## Troubleshooting 

If unexpected behavior occurs, contact Microsoft Support with the following information: 

- Device serial number.   
- Company Portal app logs, if applicable, with log ID.  
- Approximate time stamp of the event and time zone where it happened. 
- Screenshots from the Microsoft Intune admin center or device.    
- Detailed explanation of the behavior on the device.   

