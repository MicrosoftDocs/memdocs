---
# required metadata
title: Create provisioning policies for Windows 365
titleSuffix:
description: Learn how to create provisioning policies for Windows 365.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 09/16/2024
ms.topic: how-to
ms.service: windows-365
ms.subservice: windows-365-enterprise
ms.localizationpriority: high
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: mattsha
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection:
- M365-identity-device-management
- tier2
- essentials-manage
---

# Create provisioning policies

Cloud PCs are created and assigned to users based on provisioning policies. These policies hold key provisioning rules and settings that let the Windows 365 service set up and configure the right Cloud PCs for your users. After provisioning policies are created and assigned to the Microsoft Entra user security groups or Microsoft 365 Groups, the Windows 365 service:

1. Checks for appropriate licensing.
2. Configures the Cloud PCs accordingly.

A few things to keep in mind:

- Windows 365 Enterprise

  - If a user in an assigned group doesn’t have a Cloud PC license assigned, Windows 365 won’t provision their Cloud PC.
  - For each Cloud PC license assigned to a user, only one provisioning policy is used to set up and configure the Cloud PC. The Windows 365 service always uses the first assigned policy to provision the Cloud PC.

- Windows 365 Frontline in dedicated mode

  - If you have more users in your Microsoft Entra user group than the number of Cloud PCs available for the selected size, some users might not receive their Cloud PC.
  - If you remove users from your Microsoft Entra user group, their Cloud PC is automatically moved into a [grace period](device-management-overview.md#column-details) .  

- Windows 365 Frontline in shared mode

  - If you remove users from your Microsoft Entra user group, the user loses access to the Cloud PC.
  - If you remove the Microsoft Entra user group from the assignment, the Cloud PCs are automatically deprovisioned.

## Create a provisioning policy

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **Windows 365** (under **Device onboarding**) > **Provisioning policies** > **Create policy**.

   ![Screenshot of create policy.](./media/create-provisioning-policy/create-policy.png)
2. On the **General** page, enter a **Name** and **Description** (optional) for the new policy.

   > [!TIP]
   > Your provisioning policy name cannot contain the following characters: < > & | " ^

3. On the  **General** page, select a **License type**:
    - **Enterprise**: Provision Cloud PCs for Windows 365 Enterprise.
    - **Frontline**: Provision Cloud PCs for [Windows 365 Frontline](introduction-windows-365-frontline.md).
4. If you choose **Frontline**, you must also select a **Frontline type**:
    - **Dedicated**: Provision Cloud PCs in dedicated mode.
    - **Shared**: Provision Cloud PCs in shared mode.
5. On the **General** page, select a **Join type**:
    - **Microsoft Entra Join**: You have two options for **Network**:
        - **Microsoft hosted network**: Select a **Geography** where you want your Cloud PCs provisioned. Then, for [**Region**](requirements.md#supported-azure-regions-for-cloud-pc-provisioning), you can select:
            - **Automatic (Recommended)** (*not supported for Frontline in shared mode*): The Windows 365 service automatically chooses a region within the selected geography at the time of provisioning. Microsoft strongly recommends using the **Automatic** option. This automation decreases the chance of provisioning failure.
            - A specific region: This option makes sure that your Cloud PCs are only provisioned in the region that you choose.
        - **Azure network connection**: Select an ANC to use for this policy.
    - **Hybrid Microsoft Entra join**: You must select an ANC to use for this policy.

### Select an ANC

You must select an [ANC](azure-network-connections.md) for your provisioning policy if you selected either of these two options in the previous section:

- **Join type** = **Hybrid Microsoft Entra Join**
- **Join type** = **Microsoft Entra join** and **Network** = **Azure network connection**

To select an ANC, follow these steps:

1. On the **General** page, for **Azure network connection**, select one or more ANCs. For more information about using multiple ANCs, see [Alternate ANCs](azure-network-connections.md#alternate-ancs).

2. If you select more than one ANC, you can set the priority order for those ANCs. To do so, hover over an ANC > select and drag on the three dots > drag the ANC to a different position in the list.

  As long as the first ANC in the list is **Healthy**, it's always used for provisioning Cloud PCs using this policy. If the first ANC isn't healthy, the policy uses the next ANC in the list that is healthy.

> [!NOTE]
>
>For Frontline shared mode, the ANC must be in the same region.

### Continue creating a provisioning policy

1. On the **General** page, you can check the box so that your users **Use Microsoft Entra single sign-on**. If you want to make sure that users aren't prompted each time they connect to a Frontline shared Cloud PC, see [Hide consent prompt dialog](/azure/virtual-desktop/configure-single-sign-on#hide-the-consent-prompt-dialog).
2. Select **Next**.
3. On the **Image** page, for **Image type**, select one of the following options:
    - **Gallery image**: Choose **Select** > select an image from the gallery > **Select**. Gallery images are default images provided for your use.
    - **Custom image**:  Choose **Select** > select an image from the list > **Select**. The page displays the list of images that you uploaded using the [Add device images](add-device-images.md) workflow.
4. Select **Next**.
5. On the **Configuration** page, under **Windows settings**, choose a **Language & Region**. The selected language pack is installed on Cloud PCs provisioned with this policy.
6. Optional. Select **Apply device name template** to create a Cloud PC naming template to use when naming all Cloud PCs that are provisioned with this policy. This naming template updates the NETBIOS name and doesn't affect the display name of the Cloud PC. When creating the template, follow these rules:
    - Enterprise and Frontline dedicated mode
      - Names must be between 5 and 15 characters.
      - Names can contain letters, numbers, and hyphens.
      - Names can't include blank spaces or underscores.
      - Optional. Use the %USERNAME:X% macro to add the first X letters of the username.
      - Required. Use the %RAND:Y% macro to add a random string of characters, where Y equals the number of characters to add. Y must be 5 or more. Names must contain a randomized string.
    - Frontline shared mode
      - Names must be exactly 15 characters.
      - Names can contain letters, numbers, and hyphens.
      - Names can't include blank spaces or underscores.
      - Prefix must be 7 or less characters.
      - Required. Use the %RAND:Y% macro to add a random string of characters, where Y equals the number of characters to add. Y must be 8 or more. Names must contain a randomized string.

    Example of custom naming templates:

    - ABCDEF-%RAND:8%
    
7. Optional. Under **Additional services**, choose a service to be installed on Cloud PCs provisioned with this policy:
    - **Windows Autopatch** is a cloud service that automates updates for Windows, Microsoft 365 Apps for enterprise, Microsoft Edge, and Microsoft Teams on both physical and virtual devices. For more information, see [What is What is Windows Autopatch?](/windows/deployment/windows-autopatch/overview/windows-autopatch-overview) and the [Windows Autopatch FAQ](https://go.microsoft.com/fwlink/?linkid=2200228). The Windows Autopatch option isn't available for Frontline shared mode.
        - If you already have Windows Autopatch configured to manage your cloud PCs, this option replaces the existing policy. This replacement might disrupt any dynamic distribution that is already configured in Autopatch.
        - When this option is selected, the system assigns devices to a new ring as the last ring of the Autopatch group.
        - To manually enable dynamic distribution for your Cloud PCs, modify your Autopatch Groups dynamic distribution list to include the Entra ID group to which your Cloud PCs are being added.
    - **None**. Manage and update Cloud PCs manually.
8. Select **Next**.
9. On the **Assignments** page, choose **Select groups** > choose the groups you want this policy assigned to > **Select**. Nested groups aren't currently supported.
10. For Windows 365 Frontline dedicated mode, you must also select a Cloud PC size for each group in the policy. Choose **Select one** > select a size under **Available sizes** > **Select**. After you select a size for each group, select **Next**.
11. For Windows 365 Frontline shared mode you must also:
  1. Choose **Select one** > select a size under **Available sizes** > **Select**.
  2. Type in a **Friendly name** > select a **Cloud PC number** > **Next**.
12. On the **Review + create** page, select **Create**. If you used Microsoft Entra hybrid join as the join type, it can take up to 60 minutes for the policy creation process to complete. The time depends on when the Microsoft Entra Connect sync last happened.

After the provisioning policy is created and assigned, Windows 365 automatically starts to provision Cloud PCs.

### Windows 365 Frontline in dedicated mode

Microsoft Entra group members don't receive Cloud PCs if the number of users in the Microsoft Entra user group exceeds the maximum number of Cloud PCs allowed to be provisioned (based on the number of purchased licenses).

Admins can confirm the list of members who received Cloud PCs by reviewing the **Provisioning policy** > choose the policy > review the users in the groups under **Assignments**.

Windows 365 Frontline licenses are for both Frontline Cloud PCs in dedicated mode and shared mode. Frontline Cloud PCs in dedicated mode are prioritized over shared mode when you add licenses.

<!-- ########################## -->
## Next steps

[Edit provisioning policy](edit-provisioning-policy.md).
