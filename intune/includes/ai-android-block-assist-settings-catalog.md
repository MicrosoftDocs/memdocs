---
author: MandiOhlinger
ms.topic: include
ms.date: 10/30/2025
ms.author: mandia
ms.custom: include file
---

<!-- This include file is used in the manage-ai-android guide in /memdocs. -->

This step creates a settings catalog policy that configures the **Block assist content sharing with privileged apps** setting.

This setting blocks assist content, like screenshots and app details, from being sent to a privileged app, like an assistant app. The setting can be used on Android AI capabilities, like Circle to Search. This setting doesn't affect general screenshot abilities.

1. In the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices > Configuration > Create > New policy**.
2. Enter the following properties:

    - **Platform**: Select **Android Enterprise**.
    - **Profile type**: Select **Settings catalog**.

3. Select **Create**.
4. In **Basics**, enter a **Name** for the profile, and select **Next**.
5. Select **Add settings**.
6. Select the **General** category > **Block assist content sharing with privileged apps** setting. Set its value to **True**.
