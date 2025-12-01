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

2. **Enterprise personal browsing experience**: Microsoft Edge for Business offers a lightly managed personal browsing experience that lets users access their favorite nonwork sites and services without compromising safety for the enterprise.

3. **Context separation**: Work and personal browsing data are kept separate to reduce the risk of sharing sensitive information with unintended audiences.

4. **Security**: It has built-in defenses against phishing and malware and natively supports hardware isolation on Windows.

Microsoft Edge for Business provides dedicated work and personal browsing experiences with separate favorites, cache, and storage locations.

## Onboarding experience

To evaluate the onboarding experience, launch **Microsoft Edge** from the desktop and perform the sign-in process in your browser. The device can't be managed by any MDM solution, otherwise it won't be able to enroll into the MAM service.

1. Locate **Microsoft Edge** on the desktop.
2. Select the **Microsoft Edge** icon and wait for it to load. Once loaded, you see a user icon at the top-left of the browser window.
3. Select the user icon to display your managed account details.
4. Select **Sign in to sync data**.

    :::image type="content" source="./media/securing-data-edge-for-business/securing-data-edge-for-business19.png" alt-text="Sign in to sync data in Microsoft Edge." lightbox="./media/securing-data-edge-for-business/securing-data-edge-for-business19.png":::

5. Enter your **email address** for the tenant.

    :::image type="content" source="./media/securing-data-edge-for-business/securing-data-edge-for-business20.png" alt-text="Let us get you signed in to Microsoft Edge." lightbox="./media/securing-data-edge-for-business/securing-data-edge-for-business20.png":::

6. Enter your **password** for the account.

    > [!NOTE]
    > The sign-in experience varies by organization. Completing the sign-in process is required to add your work profile to Microsoft Edge.

    > [!NOTE]
    > A user experience update and admin property for controlling automatic MDM enrollment is rolling out in late 2025. This setting determines whether users on Entra ID–registered devices are prompted to MDM-enroll during the [Add Your Work or School Account to a Windows Device](https://support.microsoft.com/windows/add-your-work-or-school-account-to-a-windows-device-a6505ceb-1a20-4b15-889c-250175481506) flow. To control this behavior, configure the **Disable MDM enrollment when adding a work or school account** setting. For more information, see [Enable MDM automatic enrollment for Windows](../enrollment/windows-enroll.md).

7. Select **Yes** to sign in and register the device. Do not select **No, sign in to the app only**, as this prevents enrollment and MAM from being applied to the browser.

:::image type="content" source="./media/securing-data-edge-for-business/securing-data-edge-for-business22.png" alt-text="Prompt asking whether to sign in to all apps, websites, and services on the device, with options for Yes or No, this app only." lightbox="./media/securing-data-edge-for-business/securing-data-edge-for-business22.png":::

8. If your organization does not opt to use the new property in public preview to manage the MDM option display, select **No**. Selecting Yes will enroll your device into Intune and will not enable MAM.

:::image type="content" source="./media/securing-data-edge-for-business/securing-data-edge-for-business23a.png" alt-text="Prompt asking whether to allow your organization to manage the device, with options for Yes or No." lightbox="./media/securing-data-edge-for-business/securing-data-edge-for-business23a.png":::

9. Confirm that you're signed in by selecting the user icon again.

> [!NOTE]
> After enrollment is complete, the browser begins protecting your corporate data.

## App protection notifications

Intune displays notifications when a policy requirement isn’t met. The following messages can appear:

- **App access blocked message:** Appears when the app protection policy fails the device threat level check.

    :::image type="content" source="./media/securing-data-edge-for-business/securing-data-edge-for-business25.png" alt-text="App Access Blocked in Microsoft Edge for Business." lightbox="./media/securing-data-edge-for-business/securing-data-edge-for-business25.png":::

- **Your organization prevents you from copying content from this website:** Appears when a data movement action is blocked by your DLP policy.

    :::image type="content" source="./media/securing-data-edge-for-business/securing-data-edge-for-business26.png" alt-text="Copying prevention by app protection policy in Microsoft Edge for Business." lightbox="./media/securing-data-edge-for-business/securing-data-edge-for-business26.png":::

- **Your organization prevents you from printing this website:** Appears when printing is blocked by the applied Level 3 policy.

    :::image type="content" source="./media/securing-data-edge-for-business/securing-data-edge-for-business27.png" alt-text="Printing prevention by app protection policy in Microsoft Edge for Business." lightbox="./media/securing-data-edge-for-business/securing-data-edge-for-business27.png":::

- **Your organization prevents you from downloading this file:** Appears when downloads are blocked by the applied Level 3 policy.

    :::image type="content" source="./media/securing-data-edge-for-business/securing-data-edge-for-business28.png" alt-text="Download prevention by app protection policy in Microsoft Edge for Business." lightbox="./media/securing-data-edge-for-business/securing-data-edge-for-business28.png":::

- **Offline Grace Period Expired:** Appears when Intune determines the user has been offline longer than the allowed period.

    :::image type="content" source="./media/securing-data-edge-for-business/securing-data-edge-for-business29.png" alt-text="Offline Grace Period Expired in Microsoft Edge for Business." lightbox="./media/securing-data-edge-for-business/securing-data-edge-for-business29.png":::

## Next step

[:::image type="content" source="./media/securing-data-edge-for-business/securing-data-edge-for-business-steps-08.png" alt-text="Step 2 to create an app protection policy.":::](mamedge-8-troubleshoot.md)

Continue with [Step 8](mamedge-8-troubleshoot.md) to troubleshoot Microsoft Edge for Business.
