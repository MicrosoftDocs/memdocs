---
# required metadata

title: Manage user-device linking for Windows PCs 
titleSuffix: Microsoft Intune
description: How to link a user to an Intune-managed Windows PC.
keywords:
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 01/01/2018
ms.topic: archived
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: medium
ms.assetid: 53c99d63-c312-442a-8a71-de1b10fcd39b

# optional metadata

#audience:
#ms.devlang:
ms.reviewer: owenyen
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-classic-keep
ms.collection: M365-identity-device-management
---

# Manage user-device linking for Windows PCs

[!INCLUDE [classic-portal](../includes/classic-portal.md)]

The information in this topic applies only to Windows desktops that you are managing as PCs by using the Intune software client. 

Before you can deploy software to a user, you must link the user to a PC. You can link a user to multiple PCs, but each PC can be linked to only one user. Users are automatically linked to any PCs that they enroll in Intune by using the company portal.

For more information about a device's primary user, see [Find primary user](../intune/remote-actions/find-primary-user.md).

To link a user to a PC:

1. In the [Microsoft Intune administration console](https://manage.microsoft.com/), choose **Groups** &gt; **All Devices** (or another group that contains the PC you want to link to a user).

2. Select the PC that you want to link a user, and then choose **Link User**.

   The **Link User** dialog box displays a list of available users with their display name, user ID, and the number of PCs to which each user is currently linked. If a user is already linked to the selected PC, that user’s name and user ID are displayed under **Current user**. If the PC is not linked to any user, **No User** appears under **Current User**.

3. Do one of the following:

   - To leave the PC linked to its current user, if there is one, choose **Cancel**.

   - To remove the link to the current user, if there is one, choose <strong>Remove link **&gt;** OK</strong>.

   - To link the PC to a new user, in the **All users** list, select a user. Confirm that the user data is correct, and then choose **OK**.

> [!TIP]
> If you want to restrict end users ability to link themselves to PCs, enable the option **Restrict users' ability to link themselves to PCs** in the **Microsoft Intune Agent Settings** policy.

## See also

[Common Windows PC management tasks with the Intune software client](common-windows-pc-management-tasks-with-the-microsoft-intune-computer-client.md)
