---
title: Step 7. Understand Microsoft Edge for Business End User Experience for Windows
description: Step 7. Understand Microsoft Edge for Business end user experience Windows.
ms.date: 10/28/2025
ms.topic: how-to
ms.reviewer: samarti
ms.custom:
ms.collection:
- highpri
- highseo
- FocusArea_Apps_AppManagement
---

# Step 7. Understand Microsoft Edge for Business End User Experience for Windows

Now that you configured your Microsoft Entra Conditional Access policy, app protection policies, app configuration policies, settings catalog, and security baseline, you can launch **Microsoft Edge for Business** using a managed or unmanaged device.

The end user experience in Microsoft Edge for Business is designed to be productive, secure, and user-friendly. This secure enterprise browser experience includes the following features:

1. **Visually distinct work browsing experience**: Microsoft Edge for Business provides a visually distinct work browsing experience with refreshed visual treatment. This experience helps users easily distinguish between their work and personal browsing sessions.

2. **Enterprise personal browsing experience**: Microsoft Edge for Business offers a lightly managed personal browsing experience that lets users access their favorite nonwork sites and services without compromising safety for the enterprise. It also automatically switches from work-related navigation into the work browser.

3. **Automatic switching**: This feature helps enforce context separation between work and personal browsing. It ensures that work-related content doesn't get intermingled with personal browsing, preventing users from accidentally sharing sensitive information with unintended audiences.

4. **Security**: It has powerful, built-in defenses against phishing and malware and natively supports hardware isolation on Windows.

Microsoft Edge for Business provides dedicated work browsing experience that is visually distinct, secure, and user-friendly. It separates work and personal browsing into dedicated browser windows with their own favorites, separate cache, and storage locations.

## Onboarding experience

To evaluate the onboarding experience, launch **Microsoft Edge** from the desktop and perform the sign-in process in your browser. It's important to consider that the device can't be managed by any MDM solution, otherwise you won't be able to enroll into the MAM Service.

1. Locate **Microsoft Edge** on the desktop.
2. Select the **Microsoft Edge** icon and wait for it to load. Once loaded, you see a user icon at the top, left of the browser window.
3. Select the user icon to display your managed account details.
4. Select **Sign in to sync data**.

    :::image type="content" source="./media/securing-data-edge-for-business/securing-data-edge-for-business19.png" alt-text="Sign in to sync data in Microsoft Edge." lightbox="./media/securing-data-edge-for-business/securing-data-edge-for-business19.png":::

5. Enter your **email address** for the tenant.

    :::image type="content" source="./media/securing-data-edge-for-business/securing-data-edge-for-business20.png" alt-text="Let us get you signed in to Microsoft Edge." lightbox="./media/securing-data-edge-for-business/securing-data-edge-for-business20.png":::

6. Enter your **password** for the account.

	> [!NOTE]
	> The sign-in process within your organization might vary. Regardless of the method, completing the sign-in process is essential to add your user profile to Microsoft Edge.
    >
    > Always keep your password secure.

7. Uncheck **Allow my organization to manage my device** and select **OK**.

	:::image type="content" source="./media/securing-data-edge-for-business/securing-data-edge-for-business22.png" alt-text="Stay signed in to all your apps window in Microsoft Edge." lightbox="./media/securing-data-edge-for-business/securing-data-edge-for-business22.png":::

    > [!IMPORTANT]
    > You need to make sure the checkmark is unselected otherwise the device is enrolled into Intune. You should also not select the option **No, sign in the app only** as this won't enroll or ensure MAM is operational for the browser.

8. Wait until you see the message, **You're all set!** Then, select **Done.**

	:::image type="content" source="./media/securing-data-edge-for-business/securing-data-edge-for-business23.png" alt-text="You're all set in Microsoft Edge for Business." lightbox="./media/securing-data-edge-for-business/securing-data-edge-for-business23.png":::

9. Confirm that you're signed-in by clicking on the user icon again.

	> [!NOTE]
	> Now that enrollment is complete your browser is protecting your corporate data.

## App protection notifications

Intune notifies you with various messages if there's a failure. Here are the scenarios:

- **App access blocked message:** This message appears when your applied app protection policy failed the MDT threat level check.

    :::image type="content" source="./media/securing-data-edge-for-business/securing-data-edge-for-business25.png" alt-text="App Access Blocked in Microsoft Edge for Business." lightbox="./media/securing-data-edge-for-business/securing-data-edge-for-business25.png":::

- **Your organization prevents you from copying content from this website:** This message appears when you attempt to move data in a way that your DLP policy blocked.

    :::image type="content" source="./media/securing-data-edge-for-business/securing-data-edge-for-business26.png" alt-text="Copying prevention by app protection policy in Microsoft Edge for Business." lightbox="./media/securing-data-edge-for-business/securing-data-edge-for-business26.png":::

- **Your organization prevents you from printing this website:** This message appears when your applied Level 3 app protection policy failed the printing check.

    :::image type="content" source="./media/securing-data-edge-for-business/securing-data-edge-for-business27.png" alt-text="Printing prevention by app protection policy in Microsoft Edge for Business." lightbox="./media/securing-data-edge-for-business/securing-data-edge-for-business27.png":::

- **Your organization prevents you from downloading this file:** This message appears when your applied Level 3 app protection policy failed downloading apps check.

    :::image type="content" source="./media/securing-data-edge-for-business/securing-data-edge-for-business28.png" alt-text="Download prevention by app protection policy in Microsoft Edge for Business." lightbox="./media/securing-data-edge-for-business/securing-data-edge-for-business28.png":::

- **Offline Grace Period Expired:** This message appears when Intune determines that you have been logged in for an extended period without use.

    :::image type="content" source="./media/securing-data-edge-for-business/securing-data-edge-for-business29.png" alt-text="Offline Grace Period Expired in Microsoft Edge for Business." lightbox="./media/securing-data-edge-for-business/securing-data-edge-for-business29.png":::

## Next step

Continue with [Step 8](mamedge-8-troubleshoot.md) to troubleshoot Microsoft Edge for Business.
