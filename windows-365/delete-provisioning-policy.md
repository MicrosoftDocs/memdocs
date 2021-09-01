---
# required metadata
title: Delete provisioning policies from Windows 365
titleSuffix:
description: Learn how to delete provisioning policies from Windows 365 devices.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 08/02/2021
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

# Delete provisioning policies from Cloud PCs

Only a provisioning policy that has no assignments can be deleted. You can remove assignments by following the steps in [Edit provisioning policy](edit-provisioning-policy.md). After completing those steps, follow the steps below to delete a provisioning policy.

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Devices** > **Windows 365** (under **Provisioning**) > **Provisioning policies**.
![Screenshot of delete policy](./media/delete-provisioning-policy/delete-policy.png)
2. Select the ellipses (**…**) next to the policy you want to delete > **Delete**.
3. Select **Confirm** when asked to delete the policy.

<!-- ########################## -->
## Next steps

[Learn more about provisioning](provisioning.md).
