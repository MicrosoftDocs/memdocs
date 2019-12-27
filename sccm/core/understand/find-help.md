---
title: Find help
titleSuffix: Configuration Manager
description: Find resources for additional information about Configuration Manager.
ms.date: 05/02/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 86810629-cf2a-43e8-86a2-847444119fc1
author: aczechowski
ms.author: aaroncz
manager: dougeby

ms.collection: M365-identity-device-management
---
# Find help for using Configuration Manager

*Applies to: Configuration Manager (current branch)*

This article provides the following sections with multiple resources to find help for using Configuration Manager:  

- [Product documentation](#bkmk_Info)  

- [Sharing product feedback](#product-feedback)  

- [Follow the Configuration Manager team blog](#BKMK_ProductGroupBlog)  

- [Support options and community resources](#BKMK_SupportOptions)  

For help with product accessibility, see [Accessibility features](/sccm/core/understand/accessibility-features).  



##  <a name="bkmk_Info"></a> Product documentation  

To access the most current product documentation, start at the [library index](https://docs.microsoft.com/sccm/).  

<a name="BKMK_SearchTips"></a>  

For tips on searching, providing feedback, and more information about using the product documentation, see [How to use the docs](/sccm/core/understand/use-docs).  



<a name="product-feedback"></a>

## <a name="BKMK_1806Feedback"></a> Product feedback starting with version 1806

Starting in Configuration Manager version 1806, you can send product feedback directly from the console. If you need to attach logs, use [Feedback Hub](#BKMK_FeedbackHub). You can do the following things: <!--1357542-->

- **Send a smile**: Send feedback on what you liked.
- **Send a frown**: Send feedback on what you didn't like.
- **Send a suggestion**: Takes you to the [UserVoice website](https://configurationmanager.uservoice.com/) to share your idea.

  ![Submit feedback in Configuration Manager 1806](media/1806-send-a-smile.png)


### Send a smile

To send feedback on something that you liked follow the instructions below: 
1. In the upper right corner of the console, click on the smiley face. 
2. In the drop-down menu, select **Send a smile**.
3. Use the text box to explain what you liked. 
4. Choose if you would like to share your e-mail address and a screenshot. 
5. Click **Submit Feedback**
     - If you don't have internet connectivity, click on **Save** at the bottom. Follow the instructions in the [Send feedback that you saved for later submission](#BKMK_NoInternet) section to send it to Microsoft. 

![Submit feedback form in Configuration Manager 1806](media/1806-feedback-form.png)


### Send a frown

To send feedback on something that you didn't like, follow the instructions below:

1. In the upper right corner of the console, click on the smiley face. 
2. In the drop-down menu, select **Send a frown**.
3. Use the text box to explain what you didn't like. 
4. Choose if you would like to share your e-mail address and a screenshot. 
5. Click **Submit Feedback**
     - If you don't have internet connectivity, click on **Save** at the bottom. Follow the instructions in the [Send feedback that you saved for later submission](#BKMK_NoInternet) section to send it to Microsoft.  

### Send a suggestion

When you **Send a suggestion**, you're directed to [UserVoice](https://configurationmanager.uservoice.com/), a third-party website, to share your idea. The Configuration Manager product team uses the following UserVoice status values:

- **Noted** - We understand the request and it makes sense. We've added it to our backlog.
- **Planned** - We've started coding for this feature and expect it to show up in a tech preview build within the next few months.
- **Started** - The feature is now in a tech preview. Go check it out, and give us feedback. Let us know if the feature is on the right track or not. Put additional feedback in the comments section of the original request for others to see and comment on. We’ll read that and use the feedback to try to improve the feature.
- **Completed** - The first version of the feature is in a production build. This status doesn’t mean we're 100% done with the feature, and will no longer improve it. But it does mean that v1 of the features is in a production build, and you can start using it for real. We're marking it completed because:
  - We want you to know the feature is production ready.
  - We want to give back your UserVoice votes so you can use them on other items.
  - You can file new Design Change Requests to this feature to help us know the next most important improvement for this feature.

### Information sent with feedback

When you **Send a smile** or **Send a frown**, the following information is sent with the feedback:

- OS build information
- Configuration Manager hierarchy ID
- Product build information
- Language information
- Device identifier 
    - HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SQMClient:MachineId



### <a name="BKMK_NoInternet"></a> Send feedback that you saved for later submission

1. Click on **Save** at the bottom of the **Provide feedback** window. 
2. Save the .zip file. If the local machine doesn't have internet access,  copy the file to an internet connected machine. 
3. If needed, copy UploadOfflineFeedback folder located at `cd.latest\SMSSETUP\Tools\UploadOfflineFeedback\`
    - For more information about the cd.latest folder, see [The CD.Latest folder](../servers/manage/the-cd.latest-folder.md)

4. On an internet connected machine, open a command prompt. 
5. Run the following command: `UploadOfflineFeedback.exe -f c:\folder\location_of.zip`
    
    - Optionally, you can specify the following parameters:
        -  `-t, --timeout` Timeout in seconds for sending the data. 0 is unlimited. Default is 30.
        - `-s --silent`  No logging to console (Cannot combine with --verbose)
        - `-v, --verbose` Output verbose logging to console (Cannot combine with --silent)
        - `--help` Displays the help screen

## <a name="bkmk_feedbackid"></a> Confirmation of console feedback

<!--3556010-->
Starting in version 1902, when you send feedback through the Configuration Manager console or UploadOfflineFeedback.exe,  it shows a confirmation message. This message includes a **Feedback ID**, which you can give to Microsoft as a tracking identifier.

- To copy the **Feedback ID**, select the copy icon next to the ID, or use the **CTRL** + **C** key shortcut.
  - This ID isn't stored on your computer, so make sure to copy it before closing the window.
- Clicking on **Do not show this message again** will suppress the dialog box and prevent it from appearing in the future.

   ![Feedback confirmation from the console in Configuration Manager 1902](media/1902-feedback-id-example.png)
- The **UploadOfflineFeedback** command tool writes the **FeedbackID** to the console unless -s or --silent is used.

  ![Feedback confirmation from UploadOfflineFeedback.exe in Configuration Manager 1902](media/1902-offline-feedback-id-example.png)

##  <a name="BKMK_FeedbackHub"></a> Product feedback for versions 1802 and earlier

Report potential product defects through the [Feedback Hub app](https://support.microsoft.com/help/4021566/windows-10-send-feedback-to-microsoft-with-feedback-hub-app) built-in to Windows 10. When you **Add new feedback**, be sure to select the **Enterprise Management** category, and then choose from one of the following subcategories:
- Configuration Manager Client
- Configuration Manager Console
- Configuration Manager OS Deployment
- Configuration Manager Server

Continue to use the [UserVoice page](https://configurationmanager.uservoice.com/) to vote on new feature ideas in Configuration Manager. The Configuration Manager product team uses the following UserVoice status values:

- **Noted** - We understand the request and it makes sense. We've added it to our backlog.
- **Planned** - We've started coding for this feature and expect it to show up in a tech preview build within the next few months.
- **Started** - The feature is now in a tech preview. Go check it out, and give us feedback. Let us know if the feature is on the right track or not. Put additional feedback in the comments section of the original request for others to see and comment on. We’ll read that and use the feedback to try to improve the feature.
- **Completed** - The first version of the feature is in a production build. This status doesn’t mean we're 100% done with the feature, and will no longer improve it. But it does mean that v1 of the features is in a production build, and you can start using it for real. We're marking it completed because:
  - We want you to know the feature is production ready.
  - We want to give back your UserVoice votes so you can use them on other items.
  - You can file new Design Change Requests to this feature to help us know the next most important improvement for this feature.

##  <a name="BKMK_ProductGroupBlog"></a> Configuration Manager team blog  

The Configuration Manager engineering and partner teams use the [Enterprise Mobility + Security blog](https://cloudblogs.microsoft.com/enterprisemobility/?product=system-center-configuration-manager) to provide you with technical information and other news about Configuration Manager and related technologies. Our blog posts supplement the product documentation and support information.  


##  <a name="BKMK_SupportOptions"></a> Support options and community resources  

The following links provide information about support options and community resources:  

-   [Microsoft support](https://aka.ms/cmcbsupport)  

-   [Configuration Manager Community: Configuration Manager (Current Branch) Survival Guide](https://social.technet.microsoft.com/wiki/contents/articles/33035.system-center-configuration-manager-current-branch-survival-guide.aspx )  

-   [Configuration Manager forums page](https://social.technet.microsoft.com/Forums/en-US/home?category=ConfigMgrCB)  
    <!-- NOTE: the above URL requires "en-US" for the category to work -->
