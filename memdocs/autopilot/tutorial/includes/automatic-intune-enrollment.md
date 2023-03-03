---
author: frankroj
ms.author: frankroj
manager: aaroncz
ms.technology: itpro-deploy
ms.prod: windows-client
ms.topic: include
ms.date: 02/23/2023
ms.localizationpriority: medium
---

In order for Windows Autopilot to work, devices need to be able to enroll in Intune automatically. Enrolling devices in Intune automatically can be configured in the Azure portal:

1. Sign in to the [Azure portal](https://portal.azure.com/).

2. Select **Azure Active Directory**.

3. In the **Overview** screen, under **Manage**, select **Mobility (MDM and MAM)**.

4. In the **Mobility (MDM and MAM)** screen, select **Microsoft Intune**.

5. In the **Configure** page, next to **MDM user scope**, select either **All** or **Some**:

   - If **All** is selected, all users can automatically enroll their devices in Intune.

   - If **Some** is selected, only users specified in the group(s) next to **Groups** can automatically enroll their devices in Intune. To add groups:

      1. Select the link next to **Groups**.
      2. In the **Select groups** page, select the desired group(s) to add.
      3. Once all of the desired group(s) have been selected, select **Select**.

        > [!NOTE]
        >
        > The group(s) selected must be an Azure AD group that contains user objects.

6. In the **Configure** screen, if any changes were made, select **Save**.

> [!TIP]
>
> For Configuration Admins, this process is similar to the Configuration Manager client automatically registering with a site so that the device can be managed.