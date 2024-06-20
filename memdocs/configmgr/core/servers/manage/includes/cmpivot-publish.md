---
ms.author: gokarthi
author: gowdhamankarthikeyan
ms.service: configuration-manager
ms.topic: include
ms.date: 08/02/2021
ms.localizationpriority: medium
---
<!--This file is shared by the CMPivot overview article, cmpivot.md, and the Contribute to Community hub, community-hub-contribute.md, article for 9965423-->

## <a name="bkmk_publish"></a> Publish query to Community hub from CMPivot

*(Applies to version 2107 or later)*

Starting in version 2107, you can publish a CMPivot query to the Community hub directly from the CMPivot window. Submitting your queries directly through CMPivot makes contributing to the Community hub easier.

You'll need the following requirements for CMPivot and for contributing to the Community hub:

- Meet all of the [CMPivot prerequisites and permissions](../cmpivot.md#prerequisites)
- Enable [Community hub](../community-hub.md).
   - If needed, install the Microsoft Edge WebView2 extension from the [Configuration Manager console notification](../community-hub.md#bkmk_webview2).
- A GitHub account that's [joined to Community hub](../community-hub-contribute.md#join-the-community-hub-to-contribute-content)
   - You must accept the invitation sent in the email otherwise you won't be able to contribute content.

1. Go to the **Assets and Compliance** workspace then select the **Device Collections** node.
1. Select a target collection, target device, or group of devices then select **Start CMPivot** in the ribbon to launch the tool.
1. From the CMPivot window, select the Community hub icon on the menu.

    :::image type="content" source="../media/7137169-hub-icon.png" alt-text="Community hub icon":::

1. Select **Sign in**, then sign into GitHub.
1. Create a CMPivot query, then select **Run Query** to verify it functions as expected.
   - Optionally, select the folder icon to access your favorites list to use a query you've already created.
1. Select the **Publish** link at top of CMPivot's Community hub window when you're ready to submit your query.

   :::image type="content" source="../media/9965423-publish.png" alt-text="Screenshot of the Community hub window in CMPivot showing the publishing tab":::

1. Give your query a **Name** and **Description**, then select the **Publish** button to send your query to the Community hub.
1. Once the contribution is complete, you can access your query anytime from the **Me** tab.
1. To view the GitHub pull request (PR), go to [https://github.com/Microsoft/configmgr-hub/pulls](https://github.com/Microsoft/configmgr-hub/pulls). You can also access the PR link from the **Your hub** page in the **Community hub** node.
   - PRs shouldn't be submitted directly to the GitHub repository.

> [!NOTE]
> - Currently, when you publish a query through CMPivot, you can't edit or delete it after publishing.
> - Community hub is only available in CMPivot when you run it from the Configuration Manager console. Community hub isn't available from [standalone CMPivot](../cmpivot.md#install-cmpivot-standalone). <!--9442715, 9310040, 9391017-->
