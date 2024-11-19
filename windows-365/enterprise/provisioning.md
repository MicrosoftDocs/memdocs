---
# required metadata
title: Provisioning in Windows 365
titleSuffix:
description: Learn how provisioning works in Windows 365.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 11/05/2024
ms.topic: overview
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
---

# Provisioning overview

Provisioning in Windows 365 is the automated process that:

1. Creates a Cloud PC virtual machine.
2. Sets it up for the user.
3. Completes other tasks that prepare it to be used.
4. Creates and presents sign-in credentials that admins can pass onto end users.

Admins need only provide a few configuration details to set up the provisioning process. Then, users who have a Windows 365 license and match the configuration details automatically have a Cloud PC provisioned for them. Provisioning is a one-time per user and per-license process. Any given user and license pair can only have one Cloud PC provisioned for them.

At a high level, the full provisioning process looks like this:

1. You [create a provisioning policy](create-provisioning-policy.md) to manage who gets access to Cloud PCs. The provisioning policies are the engines that build, configure, and make Cloud PCs available to end users. Within a policy, you provide details for the network, the [image](device-images.md) used to create each Cloud PC, and a Microsoft Entra user group.
2. When a user in the Microsoft Entra user group is assigned a Windows 365 license, Windows 365 automatically provisions a Cloud PC for the user. This automation has three stages, which are invisible to the administrator. For more information on this automated process, see the [Details of the automated provisioning process article](automated-provisioning-steps.md).
3. Once provisioned, the end user can then sign in to the Windows Cloud PC from anywhere.

## Provisioning policy objects

A Windows 365 provisioning policy is an object in the Microsoft Intune admin center that orchestrates the creation of a Cloud PC.

As the admin, you provide the following required information when creating a provisioning policy:

- **Network**: A Microsoft-hosted network or an Azure network connection (ANC) dictates how the device joins Microsoft Entra ID and how its network is managed. Depending on the join type, an ANC may have information detailing:
  - The Azure subscription that is associated with the Cloud PC.
  - The domain and Organizational Unit (OU) to join.
  - The Active Directory credentials to use.
- **Image**: A Windows image is used as the reference image for all Cloud PCs provisioned with this policy. You can choose either a gallery image or supply your own custom image.
- **Configuration**: You can control more settings that are configured when the Cloud PC is provisioned.
- **Assignment**:  The assignment identifies one or more Microsoft Entra user groups. Windows 365 automatically provisions a Cloud PC for each licensed user in the policy’s Microsoft Entra user groups. If a user is later added to the user groups, they also get a Cloud PC.

Without this information, Windows 365 can’t provision the Cloud PCs.

After you’ve created the provisioning policy, Windows 365 handles all of the provisioning process to automatically get licensed users their own Cloud PCs. After the Cloud PCs are provisioned, you can inform end users that their Cloud PCs are ready for sign-in.

Changing these configurations doesn’t impact any previously provisioned Cloud PCs. However, any newly provisioned (or reprovisioned) Cloud PCs reflect the updated settings.

### Changes to provisioning policies

After the provisioning of a Cloud PC is complete, it doesn't reoccur unless you manually perform a [reprovision](reprovision-cloud-pc.md).

Changes made to any part of a provisioning policy don't trigger a reprovision. Such changes aren't applied to previously provisioned Cloud PCs. Changes to a provisioning policy will only be applied to Cloud PCs that are provisioned or reprovisioned after the changes.

If a provisioning policy name is changed, it doesn't update the Cloud PC name under All Cloud PCs, and doesn't update the enrollmentProfileName in Microsoft Entra ID.

### Deleting a provisioning policy
A provisioning policy can only be [deleted](delete-provisioning-policy.md) if it’s not assigned to any Microsoft Entra groups.

Removing the targeting of a provisioning policy that was used for successful Cloud PC provisioning puts the Cloud PCs into a grace period. When the grace period expires, the Cloud PCs are deleted automatically.

### Provisioning policy conflict resolution

Provisioning policies are assigned to user groups so there’s the possibility of overlapping groups/users.

If a user is assigned to more than one provisioning policy, provisioning honors the first assigned provisioning policy and ignores all others. It’s best practice to avoid any policy targeting overlaps to ensure consistent provisioning.

## Provisioning retry

When a Cloud PC provisioning fails, it’s retried automatically two times. After it fails three times:

1. The provisioning process is stopped.
2. The Cloud PC is marked as *Failed*.
3. An error message is displayed.

After you’ve resolved the root cause of the error, you can manually trigger a retry of the provisioning process by pressing the **Retry** button in the error dialog.

## Reprovisioning

The [**Reprovision**](reprovision-cloud-pc.md) remote action lets admins reprovision Cloud PCs. This action can be useful when:

- You're testing different Cloud PC configurations.
- Your provisioned Cloud PC is misbehaving.
- The user simply wants to start from a fresh Cloud PC.

The **Reprovision** action can also be used when a Cloud PC is in a **Failed provisioning** state in the Windows 365 provisioning node. You can think of reprovisioning as a similar process to resetting a physical device.

When a Cloud PC is reprovisioned, the Cloud PC is deleted and recreated as a new Cloud PC. All user data, applications, customizations, and the like are deleted.

The Cloud PC will be reprovisioned to the current configured settings in the provisioning policy that is targeting the user's Microsoft Entra group. If the image referenced by the policy has changed, or if any other changes to the policy have been made, the reprovisioned Cloud PC uses the new settings.

[!INCLUDE [Reprovision a Frontline shared Cloud PC](../includes/reprovision-frontline-shared-cloud-pc.md)]

For more information, see [Reprovision a Cloud PC](reprovision-cloud-pc.md).

## Users with multiple Windows 365 licenses

A user may have more than one Windows 365 license, which allows them to have more than one Cloud PC. If a user has more than one license, a Cloud PC with the appropriate specifications is provisioned for each license.

It’s not possible to trigger different provisioning policies for different user licenses. Users with multiple licenses are provisioned multiple Cloud PCs using the same provisioning policy.

## Clean-up

When a Cloud PC provisioning failure occurs, or a Cloud PC is deleted post grace period, Windows 365 cleans up all objects created during the provisioning. The clean-up occurs approximately three hours after the failure.

The following objects are cleaned up:

- Intune objects
- Microsoft Entra device objects
- Azure vNics

Network security groups created for Cloud PCs aren't cleaned up, as there may be other objects relying on those groups.

Any on-premises Microsoft Entra computer accounts that were joined to the domain during provisioning aren't be deleted. Windows 365 doesn't have sufficient permissions to delete on-premises computer objects, so instead the redundant computer objects are disabled. We encourage your organization to clean up these disabled computer objects during  your regular maintenance process.

<!-- ########################## -->
## Next steps

[Learn about Azure network connections](azure-network-connections.md)
