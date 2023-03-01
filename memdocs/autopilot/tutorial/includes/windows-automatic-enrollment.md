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

In order for Windows Autopilot to work, devices need to be able to enroll in Intune automatically. This can be configured in the Azure portal:

1. Sign in to the [Azure portal](https://portal.azure.com/).

2. Select **Azure Active Directory**.

3. In the **Overview** screen, under **Manage**, select **Mobility (MDM and MAM)**.

4. In the **Mobility (MDM and MAM)** screen, select **Microsoft Intune**.

5. In the **Configure** page, next to **MDM user scope**, select either **All** or **Some**:

   1. If **All** is selected, all Azure AD device will be automatically enrolled in Intune regardless of the user that signs into the device.

   2. If **Some** is selected, only Azure AD devices signed into by users specified in the groups next to **Groups** will be automatically enrolled in Intune. To add groups:

      1. Select the ***x* group*(s)* selected** link next to **Groups**.
      2. In the **Select groups** page, select the desired group(s) to add. Use ctrl+select to select multiple groups.
      3. Once all of the desired group(s) have been selected, select **Select**.

6. In the **Configure** screen, select **Save**.