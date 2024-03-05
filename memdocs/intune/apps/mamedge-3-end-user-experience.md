---
# required metadata

title: Understand Microsoft Edge for Business end user experience 
titleSuffix:
description: Understand Microsoft Edge for Business end user experience .
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 03/04/2024
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology:

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

# Microsoft Edge for Business end user experience 

Now that we have configured Microsoft Entra conditional access policy and created our first app protection policy for windows, we can launch **Microsoft Edge for Business** in a manage or unmanage device.

The end user experience for Secure Enterprise Browser in Microsoft Edge for Business is designed to be productive, secure, and user-friendly:

1. **Visually Distinct Work Browsing Experience**: Microsoft Edge for Business provides a visually distinct work browsing experience with refreshed visual treatment. This helps users easily distinguish between their work and personal browsing sessions.

2. **Enterprise Personal Browsing Experience**: Microsoft Edge for Business offers a lightly managed personal browsing experience that lets users access their favorite nonwork sites and services without compromising safety for the enterprise. It also automatically switches from work-related navigation into the work browser.

3. **Automatic Switching**: This feature helps enforce context separation between work and personal browsing. It ensures that work-related content doesn't get intermingled with personal browsing, preventing users from accidentally sharing sensitive information with unintended audiences.

4. **Company Branding**: This feature, which is coming soon, will increase familiarity and trust with company branding in the work browser window.

5. **Security**: It has powerful, built-in defenses against phishing and malware and natively supports hardware isolation on Windows.

In conclusion, Microsoft Edge for Business provides dedicated work browsing experience that is visually distinct, secure, and user-friendly. It separates work and personal browsing into dedicated browser windows with their own favorites, separate cache, and storage locations.

### **Enrollment Experience**

To evaluate the enrollment experience, we'll launch **Microsoft Edge** from the Desktop and perform the sign-in process into the browser for the first time. It's important to consider that the device can't be managed by any MDM Solution, otherwise we won't be able to enroll into the MAM Service.

1. Locate **Microsoft Edge** on the desktop.

:::image type="content" alt-text="Windows 11 Desktop  -  Microsoft Edge Icon." source="./media/securing-data-edge-for-business/securing_data_edge_for_business17.png" lightbox="./media/securing-data-edge-for-business/securing_data_edge_for_business17.png":::

2. Select on the **Microsoft Edge** icon and wait for it to load, once loaded select on the right side where the User Icon is located.

:::image type="content" alt-text="Microsoft Edge Sign In Icon." source="./media/securing-data-edge-for-business/securing_data_edge_for_business18.png" lightbox="./media/securing-data-edge-for-business/securing_data_edge_for_business18.png":::

3. Select on **sign in to sync data.**

:::image type="content" alt-text="Sign in to sync data  -  Microsoft Edge." source="./media/securing-data-edge-for-business/securing_data_edge_for_business19.png" lightbox="./media/securing-data-edge-for-business/securing_data_edge_for_business19.png":::

4. Enter **email address**

:::image type="content" alt-text="Let us get you signed in  -  Microsoft Edge." source="./media/securing-data-edge-for-business/securing_data_edge_for_business20.png" lightbox="./media/securing-data-edge-for-business/securing_data_edge_for_business20.png":::

5. Enter **password.**

	:::image type="content" alt-text="Let's get you signed in  -  Microsoft Edge." source="./media/securing-data-edge-for-business/securing_data_edge_for_business21.png" lightbox="./media/securing-data-edge-for-business/securing_data_edge_for_business21.png":::

	> [!NOTE] 
	> The sign-in process within your organization may vary. Regardless of the method, completing the sign-in is essential to add the user profile to Microsoft Edge.

6. Uncheck **allow my organization to manage my device** and select **OK**.

	:::image type="content" alt-text="Stay signed in to all your apps window  -  Microsoft Edge." source="./media/securing-data-edge-for-business/securing_data_edge_for_business22.png" lightbox="./media/securing-data-edge-for-business/securing_data_edge_for_business22.png":::

> [!NOTE] 
> You need to make sure the checkmark is unselected otherwise you will enroll the device into Intune, you also need to avoid clicking on **No, sign in the app only** as this will not enroll or ensure MAM is operational for the browser.

7. wait until you get the **You're all set window in** \> select **Done.**

	:::image type="content" alt-text="You're all set  -  Microsoft Edge for Business." source="./media/securing-data-edge-for-business/securing_data_edge_for_business23.png" lightbox="./media/securing-data-edge-for-business/securing_data_edge_for_business23.png":::

8. Select on the user in the top left corner and confirm the account is **signed in.**

	:::image type="content" alt-text="Managed account  -  Microsoft Edge for Business." source="./media/securing-data-edge-for-business/securing_data_edge_for_business24.png" lightbox="./media/securing-data-edge-for-business/securing_data_edge_for_business24.png":::

	> [!NOTE]
	> Now that enrollment is complete your browser is protecting your corporate data.

9. Assessing the **app protection policy** failing any **health check.**

:::image type="content" alt-text="App Access Blocked  -  Microsoft Edge for Business." source="./media/securing-data-edge-for-business/securing_data_edge_for_business25.png" lightbox="./media/securing-data-edge-for-business/securing_data_edge_for_business25.png":::

10. Assessing the **app protection policy** by Applying a **Level 3** Policy that **will not allow copy**.

:::image type="content" alt-text="Copying prevention by app protection policy  -  Microsoft Edge for Business." source="./media/securing-data-edge-for-business/securing_data_edge_for_business26.png" lightbox="./media/securing-data-edge-for-business/securing_data_edge_for_business26.png":::

11. Assessing the **app protection policy** by Applying a **Level 3** Policy that **will not allow printing**.

:::image type="content" alt-text="Printing prevention by app protection policy  -  Microsoft Edge for Business." source="./media/securing-data-edge-for-business/securing_data_edge_for_business27.png" lightbox="./media/securing-data-edge-for-business/securing_data_edge_for_business27.png":::

12.**: Assessing the app protection policy by Applying a **Level 3** Policy that **will not allow downloading apps from websites.**

:::image type="content" alt-text="Download prevention by app protection policy  -  Microsoft Edge for Business." source="./media/securing-data-edge-for-business/securing_data_edge_for_business28.png" lightbox="./media/securing-data-edge-for-business/securing_data_edge_for_business28.png":::

13. if you leave the **browser logged in for an extended period without use.**

:::image type="content" alt-text="Offline Grace Period Expired  -  Microsoft Edge for Business." source="./media/securing-data-edge-for-business/securing_data_edge_for_business29.png" lightbox="./media/securing-data-edge-for-business/securing_data_edge_for_business29.png":::
