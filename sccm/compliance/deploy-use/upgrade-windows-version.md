---
title: "Upgrade Windows devices to a different version"
titleSuffix: "Configuration Manager"
description: "Automatically upgrade devices that run Windows 10 Desktop or Windows 10 Mobile to a different edition with Configuration Manager."
ms.date: 01/26/2018
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: b0c9db74-841e-46eb-8924-957cde968bf7
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Upgrade Windows devices with the edition upgrade policy in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*


The **Edition Upgrade Policy** lets you automatically upgrade devices that run one of the following Windows 10 versions to a different edition:

- Windows 10 Desktop
- Windows 10 Mobile

The following upgrade paths are supported:

- From Windows 10 Pro to Windows 10 Enterprise
- From Windows 10 Home to Windows 10 Education
- From Windows 10 Mobile to Windows 10 Mobile Enterprise

The devices must be enrolled in Microsoft Intune or run the Configuration Manager client software. This policy is currently not compatible with PCs that are managed by on-premises MDM.

## Before you start  
 Before you begin to upgrade devices to the latest version, review the following prerequisites:  

-   For desktop editions of Windows 10: A valid product key for the new version of Windows on all devices you target with the policy. This product key can be a multiple activation key (MAK), or a generic volume licensing key (GVLK). A GVLK is also referred to as a key management service (KMS) client setup key. For more information, see [Plan for volume activation](https://docs.microsoft.com/windows/deployment/volume-activation/plan-for-volume-activation-client). For a list of KMS client setup keys, see [Appendix A](https://docs.microsoft.com/windows-server/get-started/kmsclientkeys) of the Windows Server activation guide. <!--496871-->  

-   For Windows 10 Mobile: An XML license file from the Microsoft Volume Licensing Service Center (VLSC). This file contains the licensing information for the new version of Windows on all devices you target with the policy.

- To manage this policy type, you must be in the Configuration Manager **Full Administrator** security role.

## Configure the edition upgrade policy  

1.  In the Configuration Manager console, click **Assets and Compliance** > **Compliance Settings** > **Windows 10 Edition Upgrade**.  

3.  On the **Home** tab, in the **Create** group, click **Create Edition Upgrade Policy**.  

4.  Click **Create Policy**.  

5.  On the **General** page of the **Create Edition Upgrade Policy Wizard**, specify the following information:  

    -   **Name** - Enter a name for the edition upgrade policy  

    -   **Description** (optional) - Optionally, enter a description for the policy that helps you identify it in the Intune console  

    -   **SKU to upgrade device to** - From the drop-down list, select the target edition of Windows 10 desktop or Windows 10 Mobile  

    -   **License information** - Select one of:  

        -   **Product Key** - Enter a valid product key for the target Windows 10 desktop edition  

            > [!NOTE]  
            >  After you create a policy containing a product key, you cannot edit the product key later. Configuration Manager obscures the key for security reasons. To change the product key, you must re-enter the entire key.  

        -   **License File** - Click **Browse** to select a valid license file in XML format. Configuration Manager uses this license file to upgrade Windows 10 Mobile devices.  

6.  Complete the wizard.  


## Deploy the edition upgrade policy  

1.  In the Configuration Manager console, click **Assets and Compliance** > **Compliance Settings** > **Windows 10 Edition Upgrade**.  

3.  Select the Windows 10 edition upgrade policy you want to deploy and then, on the **Home** tab, in the **Deployment** group, click **Deploy**.  

4.  In the **Deploy Windows 10 Edition Upgrade** dialog box, first choose the collection to which you want to deploy the policy. Select the schedule by which the client evaluates the policy, and then click **OK**. For PCs that are managed with the Configuration Manager client, you must deploy the policy to a device collection. For PCs that are enrolled with Intune, you can deploy the policy to a user or device collection. 



## Next steps

Monitor this deployment from the **Deployments** node of the **Monitoring** workspace. If you see errors indicating an unsuccessful deployment, for example:
- **Not applicable for this device**
- **Data type conversion failed**

These errors do not mean that the deployment failed. Verify at the targeted PC that the upgrade performed successfully.

Once the client evaluates the targeted policy, it will restart within two hours to apply the upgrade. Ensure you inform any users to which you deploy the policy, or schedule the policy to run outside of the users working hours.

If the following error appears in **DcmWmiProvider.log** on the client, check that you are using the proper key for your activation scenario. For more information, see the [Before you start](#before-you-start) section. If you are using a key management service for activation, make sure to use a [KMS client setup key](https://docs.microsoft.com/windows-server/get-started/kmsclientkeys).  <!-- 496871 -->   

`Failed to execute CheckApplicabilityMethod with error = 0x80041001	OsEditionUpgradeProvider`
