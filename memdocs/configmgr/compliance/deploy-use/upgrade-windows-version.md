---
title: Upgrade Windows devices to a different version
titleSuffix: Configuration Manager
description: Use Configuration Manager to automatically upgrade Windows 11 and Windows 10 devices to a different Windows edition.
ms.date: 09/15/2023
ms.service: configuration-manager
ms.subservice: compliance
ms.topic: upgrade-and-migration-article
author: PalikaSingh
ms.author: palsi
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Upgrade Windows devices to a new edition with Configuration Manager

*Applies to: Configuration Manager (current branch)*

The **Edition Upgrade Policy** lets you automatically upgrade Windows 11 and Windows 10 devices to a different edition.

The following upgrade paths are supported:

- From Windows 11 Pro to Windows 11 Enterprise
- From Windows 11 Home to Windows 11 Education
- From Windows 11 Pro N to Windows 11 Enterprise N
- From Windows 11 Home N to Windows 11 Education N
- From Windows 10 Pro to Windows 10 Enterprise
- From Windows 10 Home to Windows 10 Education
- From Windows 10 Mobile to Windows 10 Mobile Enterprise

The devices must run the Configuration Manager client software. Devices managed by [on-premises MDM](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md) aren't supported.

## Before you start

Before you begin to upgrade devices to the latest version, review the following prerequisites:  

- For desktop editions of Windows 11 and Windows 10: A valid product key for the new version of Windows on all devices you target with the policy. This product key can be a multiple activation key (MAK), or a generic volume licensing key (GVLK). A GVLK is also referred to as a key management service (KMS) client setup key. For more information, see [Plan for volume activation](/windows/deployment/volume-activation/plan-for-volume-activation-client). For a list of KMS client setup keys, see [Appendix A](/windows-server/get-started/kmsclientkeys) of the Windows Server activation guide. <!--496871-->  

- For Windows 10 Mobile: An XML license file from the Microsoft Volume Licensing Service Center (VLSC). This file contains the licensing information for the new version of Windows on all devices you target with the policy. Download the ISO file for **Windows 10 Mobile Enterprise**, which includes the licensing XML.<!-- SCCMDocs#2033 -->

- To manage this policy type, you must be in the Configuration Manager **Full Administrator** security role.

## Configure the policy  

1. In the Configuration Manager console, go to the **Assets and Compliance** workspace, expand **Compliance Settings**, and select the  **Windows Edition Upgrade** node.  

2. On the **Home** tab of the ribbon, in the **Create** group, select **Create Edition Upgrade Policy**.  

3. Select **Create Policy**.  

4. On the **General** page of the **Create Edition Upgrade Policy Wizard**, specify the following information:  

    - **Name** - Enter a name for the edition upgrade policy  

    - **Description** (optional) - Optionally, enter a description for the policy that helps you identify it in the Configuration Manager console  

    - **SKU to upgrade device to** - From the drop-down list, select the target edition of Windows 11 and Windows 10 desktop or Windows 10 Mobile  

    - **License information** - Select one of the following options:  

        - **Product Key** - Enter a valid product key for the target Windows 11 & 10 desktop edition  

            > [!NOTE]  
            > After you create a policy containing a product key, you can't edit the product key later. Configuration Manager obscures the key for security reasons. To change the product key, re-enter the entire key.  

        - **License File** - Select **Browse** to choose a valid license file in XML format. Configuration Manager uses this license file to upgrade Windows 10 Mobile devices.  

5. Complete the wizard.  

## Deploy the policy  

1. In the Configuration Manager console, go to the **Assets and Compliance** workspace, expand **Compliance Settings**, and select the  **Windows Edition Upgrade** node.  

2. Select the Windows edition upgrade policy you want to deploy. On the **Home** tab of the ribbon, in the **Deployment** group, select **Deploy**.  

3. Choose the device collection to which you want to deploy the policy.

4. Select the schedule by which the client evaluates the policy.

5. Complete the wizard.

## Next steps

Monitor this deployment from the **Deployments** node of the **Monitoring** workspace. If you see errors indicating an unsuccessful deployment, for example:

- **Not applicable for this device**
- **Data type conversion failed**

These errors don't mean that the deployment failed. Verify at the targeted device that the upgrade ran successfully.

Once the client evaluates the targeted policy, it applies the upgrade within two hours. [Some versions of Windows](/windows/deployment/upgrade/windows-10-edition-upgrades) may require a restart at that time. Make sure you inform any users to which you deploy the policy, or schedule the policy to run outside of the users' working hours.

If the following error appears in **DcmWmiProvider.log** on the client, check that you're using the proper key for your activation scenario. For more information, see the [Before you start](#before-you-start) section. If you're using a key management service (KMS) for activation, make sure to use a [KMS client setup key](/windows-server/get-started/kmsclientkeys).  <!-- 496871 -->

`Failed to execute CheckApplicabilityMethod with error = 0x80041001 OsEditionUpgradeProvider`

## See also

- [Plan for volume activation](/windows/deployment/volume-activation/plan-for-volume-activation-client)

- [Windows 10 edition upgrade](/windows/deployment/upgrade/windows-10-edition-upgrades)

- [Upgrade Windows 10 editions or switch out of S mode on devices using Microsoft Intune](/mem/intune/configuration/edition-upgrade-configure-windows-10)
