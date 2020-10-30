---
title: Find help
titleSuffix: Configuration Manager
description: Find resources for additional information about Configuration Manager.
ms.date: 11/20/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: how-to
ms.assetid: 86810629-cf2a-43e8-86a2-847444119fc1
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Find help for using Configuration Manager

*Applies to: Configuration Manager (current branch)*

There are several resources that you can use to find help with Configuration Manager. Whether you're just getting started or an experienced administrator, use the following resources in this article when you need assistance:

- Send a smile or file a frown with [product feedback](#product-feedback)

- [Product documentation](#product-documentation)

- [Follow the Configuration Manager team blog](#configuration-manager-team-blog)

- [Support options and community resources](#support-options-and-community-resources)

For help with product accessibility, see [Accessibility features](accessibility-features.md).

To get support for co-management, tenant attach, and analytics features, see [How to get support in Microsoft Endpoint Manager admin center](../../../get-support.md).

## Product feedback

From the Configuration Manager console, you can share feedback directly to the Microsoft product group. In the upper right corner of the console, select the smiley face icon.  There are three types of feedback:

![Submit feedback in Configuration Manager](media/console-share-feedback.png)

- **Send a smile** (**ALT** + **SHIFT** + **7**): Send feedback on what you liked.

- **Send a frown** (**ALT** + **SHIFT** + **8**): Send feedback on what you didn't like, and how Microsoft can improve it.

- **Send a suggestion** (**ALT** + **SHIFT** + **9**): Open the [Configuration Manager UserVoice website](https://configurationmanager.uservoice.com/) to share your idea. For more information, see [Send a suggestion](#send-a-suggestion).

There's also an option to **Contact support** (**ALT** + **SHIFT** + **0**), which opens the [Microsoft support for business portal](https://aka.ms/cmcbsupport).

<!--3180826-->
Starting in version 2010, there's a new wizard to send feedback with a redesigned workflow. It includes the following changes:

- It requires a description of the feedback
- Select from a list of issue categories for the console workspace
- It includes tips for how to write useful feedback
- You can attach additional files
- A summary page displays your feedback ID, and includes any error messages with suggestions to resolve them.

> [!NOTE]
> This new wizard is only in the Configuration Manager console. [Support Center](../support/support-center.md) has a similar feedback experience, which doesn't change.

### Prerequisites

- Update the Configuration Manager console to the latest version

- On the computer where you run the console, allow it to access the following internet endpoints to send diagnostic data to Microsoft:

  - `https://*.events.data.microsoft.com/`
  - `https://*.blob.core.windows.net/`

### How to send a smile

To send feedback on something that you like about Configuration Manager:

1. In the upper-right corner of the Configuration Manager console, select the smiley face icon. Choose **Send a smile**.

1. On the first page of the **Provide feedback** wizard:

    - **Tell us what you liked**: Enter a detailed description of why you're filing this feedback.

    - **You can contact me about this feedback**: To allow Microsoft to contact you about this feedback if necessary, select this option and specify a valid email address.

    - **Include screenshot**: Select this option to add a screenshot. By default it uses the full screen, select **Refresh** to capture the latest image. Select **Browse** to select a different image file.

    [![Screenshot of Provide feedback wizard to send a smile](../../media/3180826-send-a-smile.png)](../../media/3180826-send-a-smile.png#lightbox)

1. Select **Next** to send the feedback. You may see a progress bar as it packages the content to send.

1. When the progress is complete, select **Details** to see the transaction ID or any errors that occurred.

    [![Screenshot of Provide feedback wizard completion page](../../media/3180826-provide-feedback-complete.png)](../../media/3180826-provide-feedback-complete.png#lightbox)

### How to send a frown

Before you file a frown, prepare your information:

- If you have multiple issues, send a separate report for each issue. Don't include multiple issues in a single report.

- Provide clear details on the issue. Share any research that you've gathered so far. More detailed information is better to help Microsoft investigate and diagnose the issue.

- Do you need immediate assistance? If so, contact Microsoft support for urgent issues. For more information, see [Support options and community resources](../../../../understand/find-help.md#BKMK_SupportOptions).

- Is this feedback a suggestion to improve the product? If so, share a new idea on UserVoice. For more information, see [Send a suggestion](../../../../understand/find-help.md#send-a-suggestion).

- Is the issue with the product documentation? You can file feedback directly on the documentation. For more information, see [Doc feedback](../../../../../../use-docs.md#about-feedback).

To send feedback on something that you didn't like about the Configuration Manager product:

1. In the upper-right corner of the Configuration Manager console, select the smiley face icon. Choose **Send a frown**.

1. On the first page of the **Provide feedback** wizard:

    - **Issue category**: Select a category that's most appropriate for your issue.

    - Describe your issue with as much detail as possible.

    - **You can contact me about this feedback**: To allow Microsoft to contact you about this feedback if necessary, select this option and specify a valid email address.

    [![Screenshot of Provide feedback wizard to send a frown](../../media/3180826-describe-issue.png)](../../media/3180826-describe-issue.png#lightbox)

1. On the **Add more details** page of the wizard:

    - **Include screenshot**: Select this option to add a screenshot. By default it uses the full screen, select **Refresh** to capture the latest image. Select **Browse** to select a different image file.

    - **Include additional files**: Select **Attach** and add log files, which can help Microsoft better understand the issue. To remove all attached files from your feedback, select **Clear all**. To remove individual files, select the delete icon to the right of the file name.

    [![Screenshot of Add more details page in Provide feedback wizard](../../media/3180826-add-more-details.png)](../../media/3180826-add-more-details.png#lightbox)

1. Select **Next** to send the feedback. You may see a progress bar as it packages the content to send.

1. When the progress is complete, select **Details** to see the transaction ID or any errors that occurred.

If you don't have internet connectivity:

- The **Provide feedback** wizard still packages your feedback and files.

- The final summary page shows an error that it couldn't send the feedback.

- Select the option to **Save a copy of feedback and attachments**. For more information on how to send it to Microsoft, see [Send feedback that you saved for later submission](../../../../understand/find-help.md#BKMK_NoInternet).

If the **Provide feedback** wizard successfully submits your feedback, but fails to send the attached files, use the same instructions for no internet connectivity.

### Share feedback in version 2006 and earlier

<!--1357542-->

1. In the upper right corner of the console, select the smiley face.

1. In the drop-down menu, select **Send a smile** or **Send a frown**.

1. Use the text box to explain what you liked or what you didn't like.

1. Choose if you would like to share your e-mail address and a screenshot.

1. Select **Submit Feedback**.
  If you don't have internet connectivity, select **Save** at the bottom. For more information, see [Send feedback that you saved for later submission](#BKMK_NoInternet).

![Submit feedback form in Configuration Manager 1806](media/1806-feedback-form.png)

### Status messages for send a smile
<!--5891852-->
Starting in Configuration Manager 2002, when you **Send a smile** or **Send a frown**, it creates a status message when you submit the feedback. This improvement provides a record of:

- When you submitted the feedback
- Who submitted it
- The feedback ID
- The message ID identifies if the feedback submission was successful:
  - 53900: Success
  - 53901: Failed

View status messages from **Monitoring** > **System Status** > **Status Message Queries**. Start with the **All Status Messages** query and select your time frame. When the messages load, select **Filter messages**, and filter for message ID 53900 or 53901.

Status messages aren't created if you [Send feedback that you saved for later submission](find-help.md#BKMK_NoInternet).

[![Status message for successfully submitting feedback](./media/5891852-send-smile-status-message.png)](./media/5891852-send-smile-status-message.png#lightbox)

### Send a suggestion

When you **Send a suggestion**, it opens the Configuration Manager site on [UserVoice](https://configurationmanager.uservoice.com/), a third-party website. The Configuration Manager product team uses the following UserVoice status values:

- **Noted**: We understand the request and it makes sense. We've added it to our backlog.

- **Planned**: We've started coding for this feature and expect it to show up in a technical preview build within the next few months.

- **Started**: The feature is now in a technical preview release. Try it out, and share feedback from the console. Let us know if the feature is on the right track or not. Or you can share additional feedback in the UserVoice comments section of the original request.

- **Completed**: The first version of the feature is in a current branch production build. This status doesn't mean we're 100% done with the feature. It means that the first version of the feature is in a current branch release, and you can start using it in your production environment. We're marking it completed because:

  - We want you to know the feature is production-ready.

  - We want to give back your UserVoice votes so you can use them on other items.

  - You can file new ideas for this feature. Help us know the next most important improvement for this feature.

### Information sent with feedback

When you **Send a smile** or **Send a frown**, the feedback includes the following information:

- OS build information

- Configuration Manager hierarchy ID

- Product build information

- Language information

- Device identifier: `HKLM\SOFTWARE\Microsoft\SQMClient:MachineId`

### <a name="BKMK_NoInternet"></a> Send feedback that you saved for later submission

You can save your feedback locally and submit it later. Use this process if the current computer doesn't have internet-access.

1. At the bottom of the **Provide feedback** window, select **Save a copy of feedback and attachments**.

1. Save the .zip file. If the local machine doesn't have internet access, copy the file to an internet-connected machine.

1. If needed, copy the **UploadOfflineFeedback** folder from the site server located at `cd.latest\SMSSETUP\Tools\UploadOfflineFeedback\`.

    > [!NOTE]
    > For more information about the cd.latest folder, see [the CD.Latest folder](../servers/manage/the-cd.latest-folder.md).

1. On an internet-connected machine, open a command prompt.

1. Run the following command: `UploadOfflineFeedback.exe -f c:\folder\location_of.zip`

#### UploadOfflineFeedback tool usage

The UploadOfflineFeedback tool supports the following command-line parameters:

- `-f`, `--file` (**Required**): The path to the saved feedback file to send.
- `-t`, `--timeout`: Timeout in seconds for sending the data. `0` is unlimited. Default is `30`.
- `-s`, `--silent`: Don't log any output to the command prompt. You can't combine this parameter with `--verbose`.
- `-v`, `--verbose`: Log verbose output to the command prompt. You can't combine this parameter with `--silent`.
- `--help`: Display this usage information.
- `--version`: Display the tool version.

Starting in version 1910, the UploadOfflineFeedback utility supports the use of a proxy server. You can specify the following parameters:

- `-x`, `--proxy`: Specify the proxy server address.
- `-o`, `--port`: Specify the port for the proxy server.
- `-u`, `--user`: Specify the user name to authenticate to the proxy server.
- `-w`, `--password`: Specify the password for the specified user name. If you use an asterisk (`*`), the tool prompts for the password. The password isn't displayed in the prompt. This value is recommended. Including the password in plain text on the command line is less secure.
- `-i`, `--SkipConnectionCheck`: Skips the network connection check, and just starts to upload the feedback with the specified settings.

### Confirmation of console feedback
<!--3556010-->
When you send feedback, it shows a confirmation message. This message includes a **Feedback ID**, which you can give to Microsoft as a tracking identifier.

- In the Provide feedback window from the console, it displays the feedback ID on the final page. To copy it, select the copy icon next to the ID, or use the **CTRL** + **C** key shortcut. This ID isn't stored on your computer, so make sure to copy it before you close the window.

- The **UploadOfflineFeedback** command tool writes the **FeedbackID** to the console unless you use `--silent`.

  ![Feedback confirmation from UploadOfflineFeedback.exe in Configuration Manager](media/1902-offline-feedback-id-example.png)

- Starting in Configuration Manager 2002, the status message includes the feedback ID.

## Product documentation

To access the most current product documentation, start at the [library index](/memdocs/configmgr/).

For tips on searching, providing feedback, and more information about using the product documentation, see [How to use the docs](../../../use-docs.md).

## Configuration Manager team blog

The engineering and partner teams use the [Configuration Manager blog](https://techcommunity.microsoft.com/t5/Configuration-Manager-Blog/bg-p/ConfigurationManagerBlog) to provide you with technical information and other news about Configuration Manager and related technologies. Our blog posts supplement the product documentation and support information.

## Support options and community resources

The following links provide information about support options and community resources:

- [Microsoft support](https://aka.ms/cmcbsupport)

- [Configuration Manager forums on Microsoft Q&A](/answers/products/mem)

- [Configuration Manager Community: Configuration Manager (Current Branch) Survival Guide](https://social.technet.microsoft.com/wiki/contents/articles/33035.system-center-configuration-manager-current-branch-survival-guide.aspx)

## Next steps

[Accessibility features](accessibility-features.md)

[How to use the docs](../../../use-docs.md)

[How to use the console](../servers/manage/admin-console.md)

[Software Center user guide](software-center.md)

[How to get support in Microsoft Endpoint Manager admin center](../../../get-support.md)
