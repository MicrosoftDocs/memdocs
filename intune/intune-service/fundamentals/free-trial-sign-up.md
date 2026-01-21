---
title: Sign Up for Microsoft Intune Free Trial Setup Guide
description: Sign up for a Microsoft Intune free trial and configure your tenant. Learn the setup process, prerequisites, and how to configure domain names. Start evaluating Intune today.
author: nicholasswhite
ms.author: nwhite
ms.date: 01/20/2026
ms.topic: how-to
ms.reviewer: tycast
ms.collection:
- M365-identity-device-management
- highpri
---

# Step 1 - Sign up for a free trial and configure a Microsoft Intune tenant

Sign up for a Microsoft Intune free trial to evaluate mobile device management for your organization. In this article, you learn how to sign up for a free trial, create a new tenant, set up Intune, and prepare your environment for testing.

[!INCLUDE [intune-evaluate](../includes/intune-evaluate.md)]

When you complete the signup process, you automatically create a new tenant. A tenant is a dedicated instance of Microsoft Entra ID that hosts your Intune subscription. After creating the tenant, you can add users and groups, and assign licenses to users.

The free trial is an Enterprise Mobility + Security (EMS) subscription, which includes Microsoft Entra ID P1 or P2 and Microsoft Intune. After the free trial is configured, you can [confirm your free trial licenses](licenses.md#confirm-your-licenses).

You also get access to the following admin centers, which are used by Intune admins:

- **Microsoft Intune admin center** ([https://intune.microsoft.com](https://intune.microsoft.com/)) - Intune admins use this admin center to manage devices, apps, and policies. You can explore the [Intune features and capabilities](what-is-intune.md).

- **Microsoft 365 admin center** ([https://admin.microsoft.com](https://admin.microsoft.com)) - Add and manage users, if you don't use Microsoft Entra ID for this task. You can also manage other aspects of your account, including billing and support.

## Prerequisites

Before you set up Microsoft Intune, review the following requirements:

:::row:::
:::column span="1":::
[!INCLUDE [platform](../../includes/requirements/platform.md)]
:::column-end:::
:::column span="3":::
> - [Supported operating systems and browsers](supported-devices-browsers.md)
:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::
[!INCLUDE [network-connectivity](../../includes/requirements/network-connectivity.md)]
:::column-end:::
:::column span="3":::
> - [Network endpoints for Microsoft Intune](intune-endpoints.md)
:::column-end:::
:::row-end:::

[!INCLUDE [MFA requirement for admin center](../includes/mfa-console.md)]

## Sign up for a free trial

The Intune trial is free for 30 days. If you have an existing work or school account, you can **sign in** with that account and add Intune to your subscription. Or, you can **sign up** for a new account. If you sign up for a new account, you can't combine the new account with an existing work or school account.

To sign up for the Microsoft Intune free trial, use the following steps:

1. Go to the [Microsoft Intune Plan 1 Trial setup account page](https://go.microsoft.com/fwlink/?linkid=2019088).

2. Enter your email address and select **Next**.

    If you already have an account set up with another Microsoft service using your email address, you can sign in with this same account for the Intune trial. Or, you can create a new account. These steps assume you're creating a new account.

    :::image type="content" source="./media/free-trial-sign-up/sign-up-for-intune-01.png" alt-text="Screenshot of the Microsoft Intune set up account page for a free trial- Enter email." lightbox="./media/free-trial-sign-up/sign-up-for-intune-01.png":::

3. Select **Set up account** to create a new account.

   :::image type="content" source="./media/free-trial-sign-up/sign-up-for-intune-02.png" alt-text="Screenshot of the Microsoft Intune set up account page for a free trial - Set up account." lightbox="./media/free-trial-sign-up/sign-up-for-intune-02.png":::

4. Add your name, phone number, company name, company size, and region. Review the remaining information and select **Next**.

   :::image type="content" source="./media/free-trial-sign-up/sign-up-for-intune-03.png" alt-text="Screenshot of the Microsoft Intune set up account page for a free trial - Add account details." lightbox="./media/free-trial-sign-up/sign-up-for-intune-03.png":::
5. Select **Send verification code** to verify the phone number you added.

   :::image type="content" source="./media/free-trial-sign-up/sign-up-for-intune-04.png" alt-text="Screenshot of the Microsoft Intune set up account page for a free trial -  Send verification code." lightbox="./media/free-trial-sign-up/sign-up-for-intune-04.png":::

6. Enter the verification code you receive on your mobile device, and then select **Verify**.

   :::image type="content" source="./media/free-trial-sign-up/sign-up-for-intune-05.png" alt-text="Screenshot of the Microsoft Intune set up account page for a free trial -  Verify code." lightbox="./media/free-trial-sign-up/sign-up-for-intune-05.png":::
7. Add your **Username** and **Domain name** for your trial that represents your business or organization. Your name added before `.onmicrosoft.com`. Select **Save** to check availability. Select **Next** to continue. If you like, you can change this domain name to your custom domain name later.

   :::image type="content" source="./media/free-trial-sign-up/sign-up-for-intune-06.png" alt-text="Screenshot of the Microsoft Intune set up account page for a free trial -  Sign in." lightbox="./media/free-trial-sign-up/sign-up-for-intune-06.png":::

8. Add a payment method. Your card is only used for verification purposes and won't be charged unless you buy something.

   :::image type="content" source="./media/free-trial-sign-up/sign-up-for-intune-06a.png" alt-text="Screenshot of the Microsoft Intune set up account page for a free trial -  Add payment method." lightbox="./media/free-trial-sign-up/sign-up-for-intune-06a.png":::
9. After your account is created, you see your user name. Use this user name to sign in to Intune. You also receive an email message that includes your account information at the email address that you provided during the sign-up process. This email confirms your subscription is active.

   :::image type="content" source="./media/free-trial-sign-up/sign-up-for-intune-07.png" alt-text="Screenshot of the Microsoft Intune set up account page for a free trial -  Confirmation details." lightbox="./media/free-trial-sign-up/sign-up-for-intune-07.png":::

   > [!NOTE]
   > If you select **Get Started**, the **Microsoft 365 admin center** opens. If you select **Manage your subscription**, you see **Your products** and can view details about your Microsoft Intune Trial subscription.

## Sign in to the Intune admin center and create your admin team

If you're not already signed in to the admin center, sign in now:

1. Open your web browser and go to **[https://intune.microsoft.com](https://intune.microsoft.com)**.
1. Use the same user ID that you used to sign in. The user ID looks similar to `yourID@yourdomain.onmicrosoft.com`.

   :::image type="content" source="./media/free-trial-sign-up/azure-portal-signin.png" alt-text="Screenshot of the Microsoft Intune admin center sign in page." lightbox="./media/free-trial-sign-up/azure-portal-signin.png":::

To get the user ID, refer to the email message you received after signing up for the trial.

> [!TIP]
> When working with Microsoft Intune, you get better results by using a browser in regular mode, rather than private mode.

### Assign built-in roles to your admin team

Intune uses role-based access control (RBAC) to manage permissions.

The account that creates the subscription is assigned the Microsoft Entra [Global Administrator role](/entra/identity/role-based-access-control/permissions-reference#global-administrator). This built-in role is a privileged Microsoft Entra role and has more permissions than needed for most Intune tasks.

There are built-in roles specifically created and used to manage Intune. Your goal is to use the least privilege role that can perform the necessary tasks. For this series of articles, the following built-in roles are needed:

| Role | Description |
|---|---|
| **[Intune Administrator](/entra/identity/role-based-access-control/permissions-reference#intune-administrator)** | A Microsoft Entra role that has full access to all features in Microsoft Intune. You can use this account to set up Intune. |
| **[Domain Name Administrator role](/entra/identity/role-based-access-control/permissions-reference#domain-name-administrator)** | A Microsoft Entra role that can add and verify custom domain names in your tenant. This role is only used if you configure a custom domain name in this series, which is optional. |
| **[User Administrator](/entra/identity/role-based-access-control/permissions-reference#user-administrator)** | A Microsoft Entra role that can create and manage user accounts and groups in Intune and Microsoft 365. |
| **[Policy and Profile Manager](../fundamentals/role-based-access-control-reference.md#policy-and-profile-manager)** | An Intune role that can create and manage Intune policies. |
| **[Application Manager](../fundamentals/role-based-access-control-reference.md#application-manager)** | An Intune role that can add and manage apps in Intune. |
| **[Intune Role Administrator](../fundamentals/role-based-access-control-reference.md#intune-role-administrator)** | An Intune role that can create and manage custom roles and add users to Intune roles. |
| **[Global Administrator role](/entra/identity/role-based-access-control/permissions-reference#global-administrator)** | A Microsoft Entra role that sets up Automatic Enrollment for Windows devices. This role is only used once in this series. |

If many admins are testing Intune, then assign their accounts to only the roles they need. For example, if an admin is only responsible for adding and managing apps, assign that admin only to the **Application Manager** role.

- To assign built-in roles to your admin team, see [Assign Microsoft Intune roles for role-based access control](assign-role.md).

We also suggest that you sign out of the Global Administrator role account and sign in with an account that's needed for the Intune task.

For more information about Intune built-in roles, see:

- [Role-based access control (RBAC) with Microsoft Intune](role-based-access-control.md)
- [Built-in role permissions for Microsoft Intune](role-based-access-control-reference.md)

## Confirm the MDM authority

By default, the Mobile Device Management (MDM) authority is set when you create your free trial. You can confirm that the MDM authority is set by using the following steps:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) as the **Intune Administrator** Microsoft Entra role
2. Select **Tenant administration**.
3. View the tenant details. The **MDM authority** should be set to **Microsoft Intune**.

If you see an orange banner that states you didn't set the MDM authority, you can activate it now. The mobile device management (MDM) authority setting determines how you manage your devices. Set the MDM authority before users can enroll devices for management.

### Set the MDM authority to Intune

1. If the MDM authority isn't set, sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) as the **Intune Administrator** Microsoft Entra role.
2. Select the orange banner to open the **Mobile Device Management Authority** setting. The orange banner appears only if you didn't set the MDM authority.

    You can confirm the MDM Authority is set using the steps in [Confirm the MDM authority](#confirm-the-mdm-authority) (in this article).

3. If your MDM Authority isn't set, under **Choose MDM Authority**, set your MDM authority to **Intune MDM Authority**.

   :::image type="content" source="./media/free-trial-sign-up/choose-mdm-authority.png" alt-text="Screenshot of the Microsoft Intune choose MDM Authority page." lightbox="./media/free-trial-sign-up/choose-mdm-authority.png":::

For more information about the MDM authority, see [Set the mobile device management authority](mdm-authority-set.md).

## Configure your custom domain name (optional)

If your organization has its own custom domain that you want to use without **.onmicrosoft.com**, you can change it in the Microsoft 365 admin center. Use the following steps to add, verify, and configure your custom domain name.

> [!IMPORTANT]
> You can't rename or remove the initial **onmicrosoft.com** part of the domain name. However, you can add, verify, or remove *custom* domain names used with Intune to keep your business identity clear. For more information, see [Configure a custom domain name](custom-domain-name-configure.md).

1. Sign in to the [Microsoft 365 admin center](https://admin.microsoft.com) as the **Domain Name Administrator** Microsoft Entra role.

2. In the navigation pane, choose **Setup**.

3. In the **Sign-in and security** section, select **Get your custom domain set up**.

4. Select **Get started** to set up your custom domain.

5. Enter your domain name and select **Use this domain**.

    :::image type="content" source="./media/free-trial-sign-up/domain-custom-add.png" alt-text="Screenshot of Microsoft 365 admin center - Add domain." lightbox="./media/free-trial-sign-up/domain-custom-add.png":::

6. Verify that you're the owner of the domain that you entered. Select the method that you'll use to verify your domain.

    :::image type="content" source="./media/free-trial-sign-up/domain-custom-verify.png" alt-text="Screenshot of Microsoft 365 admin center - Verify domain ownership.":::

    > [!NOTE]
    > For TXT record verification details, see [Create DNS records at any DNS hosting provider for Microsoft 365](/microsoft-365/admin/get-help-with-domains/create-dns-records-at-any-dns-hosting-provider).

## Next steps

In this article, you created a free subscription to try Intune in a test environment. For more information about setting up Intune, see [Set up Intune](deployment-plan-setup.md).

To continue evaluating Microsoft Intune, go to the next step:

> [!div class="nextstepaction"]
> [Step 2 - Create a user and assign a license](quickstart-create-user.md)
