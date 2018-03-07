---
# required metadata

title: Switch Configuration Manager workloads to Intune
titleSuffix: "System Center Configuration Manager"
description: Learn how to switch workloads currently managed by Configuration Manager to Microsoft Intune. 
ms.prod: configuration-manager
ms.suite: na
ms.technology:
  - configmgr-client
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 03/09/2018
ms.topic: article
ms.service:
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
In [Prepare Windows 10 devices for co-management](co-management-prepare.md), you prepared Windows 10 devices for co-management. These devices are joined to AD, Azure AD, they are enrolled in Intune, and have the Configuration Manager client. You likely still have Windows 10 devices that are joined to AD and have the Configuration Manager client, but not joined to Azure AD or enrolled in Intune. The following procedure provides the steps to enable co-management, prepare the rest of your Windows 10 devices (Configuration Manager clients without Intune enrollment) for co-management, and allows you to start switching specific Configuration Manager workloads to Intune.

1. In the Configuration Manager console, go to **Administration** > **Overview** > **Cloud Services** > **Co-management**.    
2. On the Home tab, in the Manage group, choose **Configure co-management** to open the Co-management Configuration Wizard.    
3. On the Subscription page, click **Sign In** and sign in to your Intune tenant, and then click **Next**.   
4. On the Enablement page, choose either **Pilot** or **All**  to enable Automatic enrollment in Intune, and then click **Next**. When you choose **Pilot**, only the Configuration manager clients that are members of the Pilot group are automatically enrolled in Intune. This option allows you to enable co-management on a subset of clients to initially test co-management, and rollout co-management using a phased approach. The command line can be used to deploy the Configuration Manager client as an app in Intune for devices already enrolled in Intune. For details, see [Windows 10 devices enrolled in Intune](co-management-prepare.md#windows-10-devices-enrolled-in-intune).
5. On the Workloads page, choose whether to switch Configuration Manager workloads to be managed by Pilot Intune or Intune, and then click **Next**. The **Pilot Intune** setting switches the associated workload only for the devices in the Pilot group. The **Intune** setting switches the associated workload for all co-managed Windows 10 devices. 
        
   > [!Important]    
   > Before you switch any workloads, make sure the corresponding workload in Intune has been properly configured and deployed. Doing so ensures that workloads are always managed by one of the management tools for your devices.   
1. On the Staging page, configure the following settings and then click **Next**:
    - **Pilot**: The pilot group contains one or more collections that you select. Use this group as part of your phased rollout of co-management. You can start with a small test collection, and then add more collections to the pilot group as you roll out co-management to more users and devices. You can change the collections in the pilot group at any time from the co-management properties.
    - **Production**: Configure the **Exclusion group** with one or more collections. Devices that are members of any of the collections in this group are excluded from using co-management. 
2. To enable co-management, complete the wizard.  

## Modify your co-management settings
After you enable co-management using the wizard, you can modify the settings in the co-management properties.  
- In the Configuration Manager console, go to **Administration** > **Overview** > **Cloud Services** > **Co-management**.  
Select the co-management object, and then on the Home tab, click **Properties**. 

## Workloads able to be transitioned to Intune
Certain workloads are available to be switched over to Intune. The following list  will be updated as workloads become available to transition:
1. Device compliance policies
2. Resource access policies
3. Windows Update policies
4. Endpoint Protection (starting in Configuration Manager version 1802)
      - Windows Defender Antivirus
      - Windows Defender Application Guard
      - Windows Defender Firewall
      - Windows Defender SmartScreen
      - Windows Encryption
      - Windows Defender Exploit Guard
      - Windows Defender Application Control
      - Windows Defender Security Center
      - Windows Defender Advanced Threat Protection



## Monitor co-management
After you enable co-management, you can monitor co-management devices using the following methods:
- **SQL view and WMI class**: You can query the **v&#95;ClientCoManagementState** SQL view in the Configuration Manager site database or the **SMS&#95;Client&#95;ComanagementState** WMI class. With the information in the WMI class, you can create custom collections in Configuration Manager to help determine the status of your co-management deployment. For details, see [How to create collections](/sccm/core/clients/manage/collections/create-collections). The following fields are available in the SQL view and WMI class: 
    - **MachineId**: Specifies a unique device ID for the Configuration Manager client.
    - **MDMEnrolled**: Specifies whether the device is MDM-enrolled. 
    - **Authority**: Specifies the authority for which the device is enrolled.
    - **ComgmtPolicyPresent**: Specifies whether the Configuration Manager co-management policy exists on the client. If the **MDMEnrolled** value is **0**, the device is not co-managed regardless whether the co-management policy exists on the client.

   > [!Note]    
   > A device is co-managed when the **MDMEnrolled** field and **ComgmtPolicyPresent** fields both have a value of **1**.

- **Deployment policies**:  There are two policies created in **Monitoring** > **Deployments**; one policy for the pilot group and one for production. These policies only report the number of devices where Configuration Manager has applied the policy. It does not consider how many devices are enrolled in Intune, which is a requirement before devices can be co-managed.  

## Check compliance for co-managed devices
Users can use Software Center to check the compliance of their co-managed Windows 10 devices regardless of whether conditional access is managed by Configuration Manager or Intune. Users can also check compliance by using the Company Portal app when conditional access is managed by Intune.

## Next steps
Use the following resources to help you manage the workloads that you switch to Intune:
- [Device compliance policies](https://docs.microsoft.com/intune/device-compliance-get-started)
- [Resource access policies](https://docs.microsoft.com/intune/device-profiles)
- [Windows Update for Business policies](https://docs.microsoft.com/intune/windows-update-for-business-configure)
- [Endpoint Protection for Microsoft Intune](https://docs.microsoft.com/intune-classic/deploy-use/help-secure-windows-pcs-with-endpoint-protection-for-microsoft-intune)
