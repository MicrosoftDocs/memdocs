---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: include
ms.date: 03/12/2020
---
<!--3555750 FKA 1357954 --Don't apply H2/H3 in this include file since they are context driven by article-->
1. In the Configuration Manager console, go to the **Administration** workspace, expand **Cloud Services**, and select the **Co-management** node. Click **Configure co-management** in the ribbon to open the **Co-management Configuration Wizard**.

2. On the **Subscription** page of the wizard, configure the following settings:

    - The **Azure environment** to use. For example, the Azure Public Cloud or the Azure US Government Cloud.<!--4075452-->  

    - Select **Sign In**. Sign in as an Azure AD global administrator, and then select **Next**.  

        > [!TIP]
        > You sign in this one time for the purposes of this wizard. The credentials aren't stored or reused elsewhere.

3. On the **Enablement** page, choose the following settings:

   - **Automatic enrollment into Intune** - Enables automatic client enrollment in Intune for existing Configuration Manager clients. This option allows you to enable co-management on a subset of clients to initially test co-management, and rollout co-management using a phased approach. If a device is  unenrolled by the user, on the next evaluation of the policy, it will re-enroll. <!--3330596-->

      - **Pilot** - Only the Configuration Manager clients that are members of the **Intune Auto Enrollment** collection are automatically enrolled to Intune.
      - **All** - Enable automatic enrollment for all Windows 10, version 1709 or later, clients.

   - **Intune Auto Enrollment** - This collection should contain all of the clients you want to onboard into co-management. It's essentially a superset of all the other staging collections.

   ![Specify Intune auto enrollment collection ](../media/3555750-co-management-onboarding-enablement.png)

      > [!Note]  
      > Starting in version 1806, automatic enrollment isn't immediate for all clients. This behavior helps enrollment scale better for large environments. Configuration Manager randomizes enrollment based on the number of clients. For example, if your environment has 100,000 clients, when you enable this setting, enrollment occurs over several days.<!--1358003-->  
      >
      > Starting in version 1906:
      >
      > - A new co-managed device now automatically enrolls to the Microsoft Intune service based on its Azure Active Directory (Azure AD) *device* token. It doesn't need to wait for a user to sign in to the device for auto-enrollment to start. This change helps to reduce the number of devices with the enrollment status *Pending user sign in*.<!-- 4454491 --> To support this behavior, the device needs to be running Windows 10, version 1803 or later. For more information, see [Co-management enrollment status](../how-to-monitor.md#co-management-enrollment-status).
      >
      > - If you already have devices enrolled to co-management, new devices now enroll immediately once they meet the [prerequisites](../overview.md#prerequisites).<!--4321130-->

4. For internet-based devices that are already enrolled in Intune, copy and save the command line on the **Enablement** page. You'll use this command line to install the Configuration Manager client as an app in Intune for internet-based devices. If you don't save this command line now, you can review the co-management configuration at any time to get this command line.

5. On the **Workloads** page, for each workload, choose which device group to move over for management with Intune. For more information, see [Workloads](../workloads.md). If you only want to enable co-management, you don't need to switch workloads now. You can switch workloads later. For more information, see [How to switch workloads](../how-to-switch-workloads.md).  

    - **Pilot Intune** - Switches the associated workload only for the devices in the pilot collections you'll specify on the **Staging** page. Each workload can have a different pilot collection.
    - **Intune** - Switches the associated workload for all co-managed Windows 10 devices.  

    > [!Important]
    > Before you switch any workloads, make sure you properly configure and deploy the corresponding workload in Intune. Make sure that workloads are always managed by one of the management tools for your devices.  

6. On the **Staging** page, specify the pilot collection for each of the workloads that are set to **Pilot Intune**.

   ![Specify Intune auto enrollment collection ](../media/3555750-co-management-onboarding-staging.png)

7. To enable co-management, complete the wizard.
