---
title: Switch Configuration Manager workloads to Intune
titleSuffix: Configuration Manager
description: Learn how to switch workloads currently managed by Configuration Manager to Microsoft Intune.
ms.prod: configuration-manager
ms.technology: configmgr-client
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 12/10/2018
ms.topic: conceptual
ms.assetid: 60e2022f-a4f9-40dd-af01-9ecb37b43878
---

# Switch Configuration Manager workloads to Intune

After you [prepare Windows 10 devices for co-management](/sccm/core/clients/manage/co-management-prepare), the next step is to enable automatic client enrollment to Intune. Then when you're ready, start switching specific Configuration Manager workloads to Intune. 


## Setup co-management

1. In the Configuration Manager console, go to the **Administration** workspace, expand **Cloud Services**, and select the **Co-management** node.  

2. On the **Home** tab of the ribbon, in the **Manage** group, choose **Configure co-management**. This action opens the Co-management Configuration Wizard.  

3. On the Subscription page, select **Sign In**. Sign in to your Intune tenant, and then select **Next**.  

4. On the Enablement page, choose either **Pilot** or **All**.  

    This action enables automatic client enrollment in Intune. When you choose **Pilot**, only the Configuration Manager clients that are members of the pilot collection are automatically enrolled to Intune. This option allows you to enable co-management on a subset of clients to initially test co-management, and rollout co-management using a phased approach.  

    Use the displayed command line to deploy the Configuration Manager client as an app in Intune for devices already enrolled in Intune. For more information, see [Windows 10 devices enrolled in Intune](/sccm/core/clients/manage/co-management-prepare#windows-10-devices-enrolled-in-intune).  

5. On the Workloads page, choose whether to switch Configuration Manager workloads to be managed by Intune. You can enable enrollment on the previous page without switching any workloads at this time. 

    The **Pilot Intune** setting switches the associated workload only for the devices in the pilot collection. The **Intune** setting switches the associated workload for all co-managed Windows 10 devices.  

    > [!Important] 
    > Before you switch any workloads, make sure you properly configure and deploye the corresponding workload in Intune. Make sure that workloads are always managed by one of the management tools for your devices.  

6. On the Staging page, configure the following settings:  

    - **Pilot**: The pilot group contains one or more collections that you select. Use this group as part of your phased rollout of co-management. Start with a small test collection, and then add more collections to the pilot group as you roll out co-management to more users and devices. You can change the collections in the pilot group at any time.  

    - **Production**: Configure the **Exclusion group** with one or more collections. Devices that are members of any of the collections in this group are excluded from using co-management.  

7. To enable co-management, complete the wizard.  

<!--1357377-->
Starting in Configuration Manager version 1806, when you switch a co-management workload, the co-managed devices automatically synchronize MDM policy from Microsoft Intune. This sync also happens when you initiate the **Download Computer Policy** action from client notifications in the Configuration Manager console. For more information, see [Initiate client policy retrieval using client notification](/sccm/core/clients/manage/manage-clients#initiate-client-policy-retrieval-using-client-notification).



## Modify your co-management settings

After you enable co-management using the wizard, modify the settings in the co-management properties. In the Configuration Manager console, go to the **Administration** workspace, expand **Cloud Services**, and select the **Co-management** node. Select the co-management object, and then select **Properties** in the ribbon. 



## Supported workloads

The following workloads are currently available for you to switch from Configuration Manager to Intune:

- **Device compliance policies**  

- **Resource access policies**: For more information on these Intune policies, see [Deploy resource access profiles](https://docs.microsoft.com/intune/device-profiles).
    - Email profile  
    - Wi-Fi profile  
    - VPN profile  
    - Certificate profile  

- **Windows Update policies**  

- **Endpoint Protection**: Starting in Configuration Manager version 1802, this workload includes the following features:  
    - Windows Defender Application Guard  
    - Windows Defender Firewall  
    - Windows Defender SmartScreen  
    - Windows Encryption  
    - Windows Defender Exploit Guard  
    - Windows Defender Application Control  
    - Windows Defender Security Center  
    - Windows Defender Advanced Threat Protection  
    - Windows Information Protection  

- **Device Configuration**: Starting in Configuration Manager version 1806<!--1357903-->:  

    - Moving the device configuration workload also moves the **Resource Access** and **Endpoint Protection** workloads  

    - You can still deploy settings from Configuration Manager to co-managed devices even though Intune is the device configuration authority. This exception might be used to configure settings that are required by your organization but not yet available in Intune. Specify this exception on a [Configuration Manager configuration baseline](/sccm/compliance/deploy-use/create-configuration-baselines). Enable the option to **Always apply this baseline even for co-managed clients** when creating the baseline, or on the **General** tab of the properties of an existing baseline.  

- **Office 365 Click-to-Run apps**: Starting in Configuration Manager version 1806<!--1357841-->:  

    - After moving the workload, the app shows up in the **Company Portal** on the device  

    - Office updates may take around 24 hours to show up on client unless the devices are restarted  

    - There's a new global condition, **Are Office 365 applications managed by Intune on the device**. This condition is added by default as a requirement to new Office 365 applications. When you transition this workload, co-managed clients don't meet the requirement on the application. Then they don't install Office 365 deployed via Configuration Manager.  

- **Client apps**: Starting in Configuration Manager version 1806 as a [pre-release feature](/sccm/core/servers/manage/pre-release-features))<!--1357892-->:  

    - After you transition this workload, any available apps deployed from Intune are available in the Company Portal  

    - Apps that you deploy from Configuration Manager are available in Software Center  



## Monitor co-management

After you enable co-management, monitor co-management devices using the following methods:

- [The co-management dashboard](/sccm/core/clients/manage/co-management-dashboard)  

- **SQL view and WMI class**: Query the **v_ClientCoManagementState** SQL view in the Configuration Manager site database or the **SMS_Client_ComanagementState** WMI class. With the information in the WMI class, you can create custom collections in Configuration Manager to help determine the status of your co-management deployment. For details, see [How to create collections](/sccm/core/clients/manage/collections/create-collections). The following fields are available in the SQL view and WMI class:  
  - **MachineId**: Specifies a unique device ID for the Configuration Manager client  
  - **MDMEnrolled**: Specifies whether the device is MDM-enrolled  
  - **Authority**: Specifies the authority for which the device is enrolled  
  - **ComgmtPolicyPresent**: Specifies whether the Configuration Manager co-management policy exists on the client. If the **MDMEnrolled** value is **0**, the device isn't co-managed regardless whether the co-management policy exists on the client.  

    > [!Note]  
    > A device is co-managed when the **MDMEnrolled** field and **ComgmtPolicyPresent** fields both have a value of **1**.  

- **Deployment policies**: Two policies are created in the **Deployments** node of the **Monitoring** workspace. One policy is for the pilot group and one for production. These policies report only the number of devices where Configuration Manager has applied the policy. They don't consider how many devices are enrolled in Intune, which is a requirement before devices can be co-managed.  



## Check compliance for co-managed devices

Users can use Software Center to check the compliance of their co-managed Windows 10 devices whether conditional access is managed by Configuration Manager or Intune. Users can also check compliance by using the Company Portal app when conditional access is managed by Intune.



## Next steps

Use the following resources to help you manage the workloads that you switch to Intune:
- [Device compliance policies](https://docs.microsoft.com/intune/device-compliance-get-started)
- [Resource access policies](https://docs.microsoft.com/intune/device-profiles)
- [Windows Update for Business policies](https://docs.microsoft.com/intune/windows-update-for-business-configure)
- [Endpoint Protection for Microsoft Intune](https://docs.microsoft.com/intune-classic/deploy-use/help-secure-windows-pcs-with-endpoint-protection-for-microsoft-intune)
