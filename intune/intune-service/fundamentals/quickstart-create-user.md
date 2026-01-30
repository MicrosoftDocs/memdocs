---
title: Create a user in Intune and assign a license
description: Learn how to create a user in Microsoft Intune and assign an Intune license to this user.
services: microsoft-intune
author: paolomatarazzo
ms.author: paoloma
ms.topic: how-to
ms.date: 01/20/2026
ms.reviewer: jlynn
ms.collection:
- M365-identity-device-management
---

# Step 2 - Create a user in Intune and assign the user a license

In this article, you create a user and then assign the user an Intune license. When you use Intune, each person you want to have access to company data must have their own user account. To manage access control, Intune admins can configure users at any time.

[!INCLUDE [intune-evaluate](../includes/intune-evaluate.md)]

## Prerequisites

:::row:::
:::column span="1":::
[!INCLUDE [licensing](../../includes/requirements/licensing.md)]
:::column-end:::
:::column span="3":::
> - A Microsoft Intune subscription. [Sign up for a free trial account](../fundamentals/free-trial-sign-up.md).
:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::
[!INCLUDE [rbac](../../includes/requirements/rbac.md)]
:::column-end:::
:::column span="3":::
> Sign into the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and the [Microsoft 365 admin center](https://go.microsoft.com/fwlink/p/?LinkId=698854) with the following role:
> - Built-in **[User Administrator](/entra/identity/role-based-access-control/permissions-reference#user-administrator)** Microsoft Entra role
:::column-end:::
:::row-end:::

## Create a user

A user needs a user account to enroll in Intune device management. You use this user account in other steps in this series.

To create a new user:

1. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Users** > **All users** > **New user**:

   :::image type="content" alt-text="Screenshot that shows how to add a new user in Microsoft Intune." source="./media/quickstart-create-user/create-user.png" lightbox="./media/quickstart-create-user/create-user.png":::

2. In the **Name** box, enter a name, such as *Dewey Kellum*:

   :::image type="content" alt-text="Screenshot that shows how to add user details in Microsoft Intune." source="./media/quickstart-create-user/create-user-02.png" lightbox="./media/quickstart-create-user/create-user-02.png":::

3. In the **User name** box, enter a user identifier, such as `Dewey@contoso.onmicrosoft.com`.

    > [!NOTE]
    > If you didn't configure your customer domain name, use the verified domain name you used to create the Intune subscription (or [free trial](free-trial-sign-up.md#sign-up-for-a-free-trial)).

4. Select **Show password** and remember the automatically generated password so that you can sign in to a test device.
5. Select **Create**.

## Assign a license to a user

After you create a user, assign an Intune license to the user in the [Microsoft 365 admin center](https://go.microsoft.com/fwlink/p/?LinkId=698854). When you assign a license, the user can enroll their device into Intune.

To assign an Intune license to a user:

1. In the [Microsoft 365 admin center](https://go.microsoft.com/fwlink/p/?LinkId=698854), select **Users** > **Active Users**, and then select the user you created.
2. Select the **Licenses and Apps** tab.
3. In **Select location**, select a location for the user. It might be already set.
4. In **Licenses**, select the **Intune** check box. You can select any other license that includes Intune. The [product name](/entra/identity/users/licensing-service-plan-reference) you see is also the service plan in Azure management.

   :::image type="content" alt-text="Select the location and Intune license in the Microsoft 365 admin center." source="./media/quickstart-create-user/create-user-03.png" lightbox="./media/quickstart-create-user/create-user-03.png":::

   > [!NOTE]
   > This setting uses one of your licenses for the user. If you're using a trial environment, you reassign this license to a real user in a live environment.

5. Select **Save changes**.

The new active Intune user shows that they're using an **Intune** license.

For more information, see [Add users individually or in bulk](/microsoft-365/admin/add-users/add-users).

## Assign licenses to many users or groups

The following steps allow you to assign Intune licenses to multiple users all at once:

1. In the [Microsoft 365 admin center](https://go.microsoft.com/fwlink/p/?LinkId=698854), select **Billing** > **Licenses**. You see all licensable products that are available for your organization.
2. Select the license you want to assign.
3. Select **Users** or **Groups**, and then select **Assign licenses**.
4. Select all the users or all the groups you want to assign the license to > **Assign licenses**.
   A notification shows the status and outcome of the process. If the assignment to the group can't be completed (for example, because of preexisting licenses in the group), you can select the notification to view details.

   The user accounts now have the permissions needed to use the service and enroll devices into management.

> [!TIP]
> You can also assign Intune licenses to users by using School Data Sync (SDS). For more information, see [Overview of School Data Sync](/schooldatasync/school-data-sync-overview).

## Clean up resources

You can continue using this user in other steps of this series. When finished with this series, you can delete the user.

To delete the user:

1. In the [Microsoft 365 admin center](https://go.microsoft.com/fwlink/p/?LinkId=698854), select **Users** > **Active users**.
2. Select the user you want to delete > **Delete user** > **Close**.

   :::image type="content" source="./media/quickstart-create-user/create-user-04.png" alt-text="Screenshot that shows how to delete a user in the Microsoft 365 admin center.":::

## Next steps

In this article, you created a user and assigned an Intune license to that user. For more information on adding users to Intune, see [Add users and grant administrative permission to Intune](users-add.md).

To continue evaluating Microsoft Intune, go to the next step:

> [!div class="nextstepaction"]
> [Step 3 - Create a group to manage users](quickstart-create-group.md)
