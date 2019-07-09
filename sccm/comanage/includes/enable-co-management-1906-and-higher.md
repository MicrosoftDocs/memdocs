---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.topic: include
ms.date: 07/19/2019
ms.collection: M365-identity-device-management
---
<!--3555750 FKA 1357954-->
1. In the Configuration Manager console, go to the **Administration** workspace, expand **Cloud Services**, and select the **Co-management** node. Click **Configure co-management** in the ribbon to open the **Co-management Onboarding Wizard**.  

2. On the **Subscription** page of the wizard, select **Sign In**. Sign in to your Intune tenant, and then select **Next**.  

3. On the **Enablement** page, choose your **Automatic enrollment into Intune** setting, either **Pilot** or **All**.

   - This action enables automatic client enrollment in Intune for existing Configuration Manager clients. When you choose **Pilot**, only the Configuration Manager clients that are members of the pilot collection are automatically enrolled to Intune. This option allows you to enable co-management on a subset of clients to initially test co-management, and rollout co-management using a phased approach.  
   - Starting in version 1806, automatic enrollment isn't immediate for all clients. This behavior helps enrollment scale better for large environments. Configuration Manager randomizes enrollment based on the number of clients. For example, if your environment has 100,000 clients, when you enable this setting, enrollment occurs over several days.<!--1358003-->  

4. On the **Enablement** page,  specify an **Intune Auto Enrollment** collection.

   - The **Intune Auto Enrollment** collection should contain all of the clients you want to onboard into co-management. It's essentially a superset of all the other staging collections.

   ![Specify Intune auto enrollemnt collection ](../media/3555750-co-management-onboarding-enablement.png)

5. If you have internet-based devices that are already enrolled in Intune, copy the command line on the **Enablement** page. You can use this command line to install the Configuration Manager client as an app in Intune.

6. On the **Workloads** page, for each workload, choose which device group to move over for management with Intune. For more information, see [Workloads](/sccm/comanage/workloads).  

    If you only want to enable co-management, you don't need to switch workloads now. You can switch workloads later. For more information, see [How to switch workloads](/sccm/comanage/how-to-switch-workloads).  

    The **Pilot Intune** setting switches the associated workload only for the devices in the pilot collection. The **Intune** setting switches the associated workload for all co-managed Windows 10 devices.  

    > [!Important]
    > Before you switch any workloads, make sure you properly configure and deploy the corresponding workload in Intune. Make sure that workloads are always managed by one of the management tools for your devices.  

7. On the **Staging** page, specify the collection for each of the workloads that are set to **Pilot Intune**.

   ![Specify Intune auto enrollemnt collection ](../media/3555750-co-management-onboarding-staging.png)

8. To enable co-management, complete the wizard.