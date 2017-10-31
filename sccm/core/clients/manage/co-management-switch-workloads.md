---
# required metadata

title: Switch Configuration Manager workloads to Intune
description: Learn how to switch workloads currently managed by Configuration Manager to Microsoft Intune. 
keywords:
author: dougeby
manager: angrobe
ms.date: 10/31/2017
ms.topic: article
ms.prod: configuration-manager
ms.service:
ms.technology:
ms.assetid: 60e2022f-a4f9-40dd-af01-9ecb37b43878

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
#ms.reviewer: [ALIAS]
#ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Switch Configuration Manager workloads to Intune
In [Prepare Windows 10 devices for co-management](co-management-prepare.md), you prepared Windows 10 devices for co-management. These devices are now joined to AD and Azure AD, and they are enrolled in Intune and have the Configuration Manager client. You likely still have Windows 10 devices that are joined to AD and have the Configuration Manager client, but not joined to Azure AD or enrolled in Intune. The following procedure provides the steps to enable co-management, prepare the rest of your Windows 10 devices (Configuration Manager clients without Intune enrollment) for co-management, and allows you to start switching specific Configuration Manager workloads to Intune.

1. In the Configuration Manager console, go to **Administration** > **Overview** > **Cloud Services** > **Co-management**.    
2. On the Home tab, in the Manage group, choose **Configure co-management** to open the Co-management Onboarding Wizard.    
3. On the Subscription page, click **Sign In** and sign in to your Intune tenant, and then click **Next**.   
4. On the Staging page, configure the following settings and then click **Next**:
    - **Pilot group**: The pilot group contains one or more collections that you select. Use this group as part of your phased rollout of co-management. You can start with a small test collection, and then add more collections to the pilot group as you roll out co-management to more users and devices. You can change the collections in the pilot group at any time from the co-management properties.
    - **Production**: When you select this setting, all supported Windows 10 devices are enabled for co-management. Configure the **Exclusion group** with one or more collections. Devices that are members of any of the collections in this group are excluded from using co-management. 
5. On the Enablement page, choose either **Pilot** or **All** (depending on the settings you configured on the Staging page) to enable Automatic enrollment in Intune, and then click **Next**. When you choose **Pilot**, only the Configuration manager clients that are members of the Pilot group are automatically enrolled in Intune. This allows you to enable co-management on a subset of clients to initially test co-management, and rollout co-management using a phased approach. 
6. On the Workloads page, choose whether to switch Configuration Manager workloads to be managed by Intune, and then click **Next**. Use the sliders to select whether to switch the workload to the Pilot group or for all Windows 10 clients (depending on the settings you configured on the Staging page). 
7. To enable co-management, complete the wizard.  

<!--### Modify your co-management settings
After you enable co-management using the wizard, you can modify your target group and change the workloads that are managed by Configuration Manager and Intune.  
- In the Configuration Manager console, go to **Administration** > **Overview** > **Cloud Services** > **Co-management**.  
Select the co-management object, and then on the Home tab, click **Properties**. -->   

<!--### Monitor co-management
After you have enabled co-management, you can monitor which devices are managed by Configuration Manager and which are managed by Intune. You can also see which Configuration Manager workloads are managed by which product.-->