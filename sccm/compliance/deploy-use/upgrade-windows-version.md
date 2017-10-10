---
title: "Upgrade Windows devices to a different version"
description: "Automatically upgrade devices that run Windows 10 Desktop, Windows 10 Mobile, or Windows 10 Holographic to a different edition with Configuration Manager."
ms.custom: na
ms.date: 07/31/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b0c9db74-841e-46eb-8924-957cde968bf7
caps.latest.revision: 8
caps.handback.revision: 0
author: arob98
ms.author: angrobe
manager: angrobe

---

# Upgrade Windows devices with the edition upgrade policy in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*


The System Center Configuration Manager **Edition Upgrade Policy** lets you automatically upgrade devices that run one of the following Windows 10 versions to a different edition:

- Windows 10 Desktop
- Windows 10 Mobile
<!-- - Windows 10 Holographic -->

The following upgrade paths are supported:

- From Windows 10 Pro to Windows 10 Enterprise
- From Windows 10 Home to Windows 10 Education
- From Windows 10 Mobile to Windows 10 Mobile Enterprise
<!-- - From Windows 10 Holographic Pro to Windows 10 Holographic Enterprise -->

The devices must be enrolled in Microsoft Intune or run the Configuration Manager client software. This policy is currently not compatible with PCs that are managed by on-premises MDM.

## Before you start  
 Before you begin to upgrade devices to the latest version, you will need one of the following:  

-   A product key which is valid to install the new version of Windows on all devices you target with the policy (for desktop operating systems)  

-   A licence file from Microsoft which contains the licensing information to install the new version of Windows on all devices you target with the policy (for Windows 10 Mobile<!-- and Windows 10 Holographic-->).

- To create and deploy this policy type, you must have been assigned the Configuration Manager **Full Administrator** security role.

## Configure the edition upgrade policy  

1.  In the Configuration Manager console, click **Assets and Compliance** > **Compliance Settings** > **Windows 10 Edition Upgrade**.  

3.  On the **Home** tab, in the **Create** group, click **Create Edition Upgrade Policy**.  

4.  Click **Create Policy**.  

5.  On the **General** page of the **Create Edition Upgrade Policy Wizard**, specify the following information:  

    -   **Name** - Enter a name for the edition upgrade policy.  

    -   **Description** (optional) - Optionally, enter a description for the policy that helps you identify it in the Intune console.  

    -   **SKU to upgrade device to** - From the drop-down list, select the version of Windows 10 Desktop, <!-- Windows 10 Holographic,--> or Windows 10 Mobile that you want to upgrade targeted devices to.  

    -   **License information** - Select one of:  

        -   **Product Key** - Enter a valid Windows 10 product key that will be used to upgrade devices you target that run Windows 10 Desktop operating systems.  

            > [!NOTE]  
            >  After you create a policy containing a product key, you cannot edit the product key later. This is because the key is obscured for security reasons. To change the product key, you must re-enter the entire key.  

        -   **License File** - Click **Browse** to select a valid license file in XML format that will be used to upgrade devices you target that run <!--Windows 10 Holographic and -->Windows 10 Mobile operating systems.  

6.  Complete the wizard.  

The new policy is displayed in the **Windows 10 Edition Upgrade** node of the **Assets and Compliance** workspace.  

## Deploy the edition upgrade policy  

1.  In the Configuration Manager console, click **Assets and Compliance** > **Compliance Settings** > **Windows 10 Edition Upgrade**.  

3.  Select the Windows 10 edition upgrade policy you want to deploy and then, on the **Home** tab, in the **Deployment** group, click **Deploy**.  

4.  In the **Deploy Windows 10 Edition Upgrade** dialog box, choose the collection to which you want to deploy the policy and the schedule by which the policy will be evaluated, and then click **OK**. For PCs that are managed with the Configuration Manager client, you must deploy the policy to a device collection. For PCs that are enrolled with Intune, you can deploy the policy to a user or device collection. 



## Next steps

When you monitor the deployment you just created from the **Deployments** node of the **Monitoring** workspace, you might see errors indicating the deployment was unsuccessful like:
- **Not applicable for this device**
- **Data type conversion failed**

These errors do not mean that the deployment failed. Verify at the targeted PC that the upgrade performed successfully.

Once the policy reaches a targeted Windows PC and is evaluated, it will be restarted within two hours to apply the upgrade. Ensure you inform any users to which you deploy the policy, or schedule the policy to run outside of the users working hours.
