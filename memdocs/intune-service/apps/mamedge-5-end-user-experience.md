---
# required metadata

title: Step 5. Understand Microsoft Edge for Business end user experience for Windows
titleSuffix:
description: Step 5. Understand Microsoft Edge for Business end user experience Windows.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 03/26/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high

# optional metadata

#audience:
#ROBOTS: 
ms.reviewer: samarti
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: 
ms.collection:
- tier1
- highpri
- highseo
- FocusArea_Apps_AppManagement
---

# Step 5. Understand Microsoft Edge for Business end user experience for Windows

Now that you've configured your Microsoft Entra Conditional Access policy and created your first app protection policy for Windows, you can launch **Microsoft Edge for Business** using a managed or unmanaged device.

The end user experience in Microsoft Edge for Business is designed to be productive, secure, and user-friendly. This secure enterprise browser experience includes the following features:

1. **Visually distinct work browsing experience**: Microsoft Edge for Business provides a visually distinct work browsing experience with refreshed visual treatment. This helps users easily distinguish between their work and personal browsing sessions.

2. **Enterprise personal browsing experience**: Microsoft Edge for Business offers a lightly managed personal browsing experience that lets users access their favorite nonwork sites and services without compromising safety for the enterprise. It also automatically switches from work-related navigation into the work browser.

3. **Automatic switching**: This feature helps enforce context separation between work and personal browsing. It ensures that work-related content doesn't get intermingled with personal browsing, preventing users from accidentally sharing sensitive information with unintended audiences.

4. **Security**: It has powerful, built-in defenses against phishing and malware and natively supports hardware isolation on Windows.

Microsoft Edge for Business provides dedicated work browsing experience that is visually distinct, secure, and user-friendly. It separates work and personal browsing into dedicated browser windows with their own favorites, separate cache, and storage locations.

## Onboarding experience

To evaluate the onboarding experience, launch **Microsoft Edge** from the desktop and perform the sign-in process in your browser. It's important to consider that the device can't be managed by any MDM solution, otherwise you won't be able to enroll into the MAM Service.

1. Locate **Microsoft Edge** on the desktop.
2. Select the **Microsoft Edge** icon and wait for it to load. Once loaded, you'll see a user icon at the top, left of the browser window.
3. Select the user icon to display your managed account details.
4. Select **Sign in to sync data**.

    :::image type="content" alt-text="Sign in to sync data  -  Microsoft Edge." source="./media/securing-data-edge-for-business/securing-data-edge-for-business19.png" lightbox="./media/securing-data-edge-for-business/securing-data-edge-for-business19.png":::

5. Enter your **email address** for the tenant.

    :::image type="content" alt-text="Let us get you signed in  -  Microsoft Edge." source="./media/securing-data-edge-for-business/securing-data-edge-for-business20.png" lightbox="./media/securing-data-edge-for-business/securing-data-edge-for-business20.png":::

6. Enter your **password** for the account.

	> [!NOTE] 
	> The sign-in process within your organization may vary. Regardless of the method, completing the sign-in process is essential to add your user profile to Microsoft Edge.
    >
    > Always keep your password secure.

7. Uncheck **Allow my organization to manage my device** and select **OK**.

	:::image type="content" alt-text="Stay signed in to all your apps window  -  Microsoft Edge." source="./media/securing-data-edge-for-business/securing-data-edge-for-business22.png" lightbox="./media/securing-data-edge-for-business/securing-data-edge-for-business22.png":::

    > [!IMPORTANT] 
    > You need to make sure the checkmark is unselected otherwise you will enroll the device into Intune, you should also not select the option **No, sign in the app only** as this will not enroll or ensure MAM is operational for the browser.

8. Wait until you see the message, **You're all set!** Then, select **Done.**

	:::image type="content" alt-text="You're all set  -  Microsoft Edge for Business." source="./media/securing-data-edge-for-business/securing-data-edge-for-business23.png" lightbox="./media/securing-data-edge-for-business/securing-data-edge-for-business23.png":::

9. Confirm that you're signed-in by clicking on the user icon again.

	> [!NOTE]
	> Now that enrollment is complete your browser is protecting your corporate data.

## App protection notifications

Intune will notify you with various messages in the event of a failure. Here are the scenarios:

- **App access blocked message:** This message appears when your applied app protection policy has failed the MDT threat level check.

    :::image type="content" alt-text="App Access Blocked - Microsoft Edge for Business." source="./media/securing-data-edge-for-business/securing-data-edge-for-business25.png" lightbox="./media/securing-data-edge-for-business/securing-data-edge-for-business25.png":::

- **Your organization prevents you from copying content from this website:** This message appears when you attempt to move data in a way that is blocked by your DLP policy.

    :::image type="content" alt-text="Copying prevention by app protection policy - Microsoft Edge for Business." source="./media/securing-data-edge-for-business/securing-data-edge-for-business26.png" lightbox="./media/securing-data-edge-for-business/securing-data-edge-for-business26.png":::

- **Your organization prevents you from printing this website:** This message appears when your applied Level 3 app protection policy has failed the printing check.

    :::image type="content" alt-text="Printing prevention by app protection policy - Microsoft Edge for Business." source="./media/securing-data-edge-for-business/securing-data-edge-for-business27.png" lightbox="./media/securing-data-edge-for-business/securing-data-edge-for-business27.png":::

- **Your organization prevents you from downloading this file:** This message appears when your applied Level 3 app protection policy has failed downloading apps check.

    :::image type="content" alt-text="Download prevention by app protection policy - Microsoft Edge for Business." source="./media/securing-data-edge-for-business/securing-data-edge-for-business28.png" lightbox="./media/securing-data-edge-for-business/securing-data-edge-for-business28.png":::

- **Offline Grace Period Expired:** This message appears when Intune determines that you have been logged in for an extended period without use.

    :::image type="content" alt-text="Offline Grace Period Expired - Microsoft Edge for Business." source="./media/securing-data-edge-for-business/securing-data-edge-for-business29.png" lightbox="./media/securing-data-edge-for-business/securing-data-edge-for-business29.png":::

## Next step

[![Step 6 to troubleshoot Microsoft Edge for Business.](./media/securing-data-edge-for-business/securing-data-edge-for-business-steps-06.png)](mamedge-6-troubleshoot.md)

Continue with [Step 6](mamedge-6-troubleshoot.md) to troubleshoot Microsoft Edge for Business.
