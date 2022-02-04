---
# required metadata
title: Create provisioning policies for Windows 365
titleSuffix:
description: Learn how to create provisioning policies for Windows 365.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 02/08/2022
ms.topic: how-to
ms.service: cloudpc
ms.subservice:
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: mattsha
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
---

# Create provisioning policies

Cloud PCs are created and assigned to users based on provisioning policies. These policies hold key provisioning rules and settings that let the Windows 365 service set up and configure the right Cloud PCs for your users. After provisioning policies are created and assigned to the Azure AD user security groups or Microsoft 365 Groups, the Windows 365 service:

1. Checks for appropriate licensing for each user.
2. Configures the Cloud PCs accordingly.

A few things to keep in mind:

- If a user in an assigned group doesn’t have a Cloud PC license assigned, Windows 365 won’t provision their Cloud PC.
- For each Cloud PC license assigned to a user, only one provisioning policy is used to set up and configure the Cloud PC. The Windows 365 service always uses the first assigned policy to provision the Cloud PC.

## Create a provisioning policy

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **Windows 365** (under **Provisioning**) > **Provisioning policies** > **Create policy**.

   ![Screenshot of create policy](./media/create-provisioning-policy/create-policy.png)
2. On the **General** page, enter a **Name** and **Description** (optional) for the new policy.

   > [!TIP]
   > Your provisioning policy name cannot contain the following characters: < > & | " ^

3. On the **General** page, select a join type, followed by the appropriate network. If you select the combination of **Azure AD Join (preview)** and **Microsoft Hosted Network**, you must select a region for Microsoft to host your Cloud PC.
4. For **On-premises network connection**, select the connection to use for this policy > **Next**.
5. On the **Image** page, for **Image type**, select one of the following options:
    - **Gallery image**: Choose **Select** > select an image from the gallery > **Select**. Gallery images are default images provided for your use.
    - **Custom image**:  Choose **Select** > select an image from the list > **Select**. You'll see the list of images that you uploaded using the [Add device images](add-device-images.md) workflow.
6. Select **Next**.
7. On the **Configuration** page, choose a language pack in the dropdown. The selected language pack will be installed on Cloud PCs provisioned with this policy. Select **Next**.
8. On the **Assignments** page, choose **Select groups** > choose the groups you want this policy assigned to > **Select** > **Next**.
9. On the **Review + create** page, select **Create**. If you used Hybrid Azure AD Join as the join type, it can take up to 60 minutes for the policy creation process to complete The time depends on when the Azure AD connect sync last happened.

<!-- ########################## -->
## Next steps

[Edit provisioning policy](edit-provisioning-policy.md).
