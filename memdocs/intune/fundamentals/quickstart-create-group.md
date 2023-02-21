---
# required metadata

title: Quickstart - Create a group to manage users
titleSuffix: Microsoft Intune
description: In this quickstart you will use Microsoft Intune to create a group based on existing users.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 12/16/2021
ms.topic: quickstart
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology:
ms.assetid: 723f4b4e-3090-4811-84ff-6af652abea5a

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: scottduf
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier3
- M365-identity-device-management
---

# Quickstart: Create a group to manage users

In this quickstart, you will use Intune to create a group based on an existing user. Groups are used to manage your users and control your employees' access to your company resources. These resources can be part of your company's intranet or can be external resources, such as SharePoint sites, SaaS apps, or web apps.

If you don't have an Intune subscription, [sign up for a free trial account](free-trial-sign-up.md).

>[!NOTE]
>Intune provides pre-created **All Users** and **All Devices** groups in the console with built-in optimizations for your convenience.

## Prerequisites

- Microsoft Intune subscription - [sign up for a free trial account](../fundamentals/free-trial-sign-up.md).
- To complete this quickstart, you must [create a user](quickstart-create-user.md).

## Sign in to Intune in the Microsoft Endpoint Manager

Sign in to [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) as a [Global administrator or an Intune Service administrator](users-add.md#types-of-administrators). If you have created an Intune Trial subscription, the account you created the subscription with is the Global administrator.

## Create a group

You will create a group that will be used later in this quickstart series. To create a group:

1. Once you've opened the [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431), select **Groups** > **New group**.
2. In the **Group type** dropdown box, select **Security**.
3. In the **Group name** field, enter the name for the new group (for example, **Contoso Testers**).
4. Add a **Group description** for the group.
5. Set the **Membership type** to **Assigned**. 
6. Under **Members**, select the link and add one or more members for the group from the list.

    ![Screenshot of creating a group in Microsoft Intune](./media/quickstart-create-group/quickstart-use-groups-01.png)

7. Click **Select** > **Create**.

Once you have successfully created the group, it will appear in the list of **All groups**. 

## Next steps

In this quickstart, you used Intune to create a group based on an existing user. For more information about adding groups to Intune, see [Add groups to organize users and devices](groups-add.md).

To follow this series of Intune quickstarts, continue to the next quickstart.

> [!div class="nextstepaction"]
> [Quickstart: Set up automatic enrollment for Windows 10 devices](../enrollment/quickstart-setup-auto-enrollment.md)
