---
title: Find help
titleSuffix: Configuration Manager
description: Find resources for additional information about System Center Configuration Manager.
ms.date: 07/13/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 86810629-cf2a-43e8-86a2-847444119fc1
author: aczechowski
ms.author: aaroncz
manager: dougeby

---
# Find help for using System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

This article provides the following sections with multiple resources to find help for using Configuration Manager:  

- [Product documentation](#bkmk_Info)  

- [Sharing product feedback](#product-feedback)  

- [Follow the Configuration Manager team blog](#BKMK_ProductGroupBlog)  

- [Support options and community resources](#BKMK_SupportOptions)  

For help with product accessibility, see [Accessibility features in Configuration Manager](../../core/understand/accessibility-features.md).  


##  <a name="bkmk_Info"></a> Product documentation  

To access the most current product documentation, start at the [library index](https://docs.microsoft.com/sccm/).  

<a name="BKMK_SearchTips"></a>  

For tips on searching, providing feedback, and more information about using the product documentation, see [How to use the docs](/sccm/core/understand/use-docs).  

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
To send feedback on something that you didn't like follow the instructions below:

1. In the upper right corner of the console, click on the smiley face. 
2. In the drop-down menu, select **Send a frown**.
3. Use the text box to explain what you didn't like. 
4. Choose if you would like to share your e-mail address and a screenshot. 
5. Click **Submit Feedback**
     - If you don't have internet connectivity, click on **Save** at the bottom. Follow the instructions in the [Send feedback that you saved for later submission](#BKMK_NoInternet) section to send it to Microsoft.  

### Information sent with feedback
 
   - OS build information
   - Configuration Manager hierarchy ID
   - Product build information
   - Language information
   - Device identifier 
       - HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SQMClient:MachineId

### <a name="BKMK_NoInternet"></a> Send feedback that you saved for later submission

1. Click on **Save** at the bottom of the **Provide feedback** window. 
2. Save the .zip file. If the local machine doesn't have internet access,  copy the file to an internet connected machine. 
3. If needed, copy UploadOfflineFeedback.exe located at `cd.latest\SMSSETUP\Tools\UploadOfflineFeedback\UploadOfflineFeedback.exe`
4. On an internet connected machine, open a command prompt. 
5. Run the following command: `UploadOfflineFeedback.exe -f c:\folder\location_of.zip`
    
    - Optionally, you can specify the following:
        -  `-t, --timeout` Timeout in seconds for sending the data. 0 is unlimited. Default is 30.
        - `-s --silent`  No logging to console (Cannot combine with --verbose)
        - `-v, --verbose` Output verbose logging to console (Cannot combine with --silent)
        - `--help` Displays the help screen
    - For more information about the cd.latest folder, see [The CD.Latest folder](../servers/manage/the-cd.latest-folder.md)

##  <a name="BKMK_FeedbackHub"></a> Product feedback for versions 1802 and earlier
Report potential product defects through the [Feedback Hub app](https://support.microsoft.com/help/4021566/windows-10-send-feedback-to-microsoft-with-feedback-hub-app) built-in to Windows 10. When you **Add new feedback**, be sure to select the **Enterprise Management** category, and then choose from one of the following subcategories:
 - Configuration Manager Client
 - Configuration Manager Console
 - Configuration Manager OS Deployment
 - Configuration Manager Server

Continue to use the [user voice page](https://configurationmanager.uservoice.com/) to vote on new feature ideas in Configuration Manager.


##  <a name="BKMK_ProductGroupBlog"></a> Configuration Manager team blog  
 The Configuration Manager engineering and partner teams use the [Enterprise Mobility + Security blog](https://cloudblogs.microsoft.com/enterprisemobility/?product=system-center-configuration-manager) to provide you with technical information and other news about Configuration Manager and related technologies. Our blog posts supplement the product documentation and support information.  


##  <a name="BKMK_SupportOptions"></a> Support options and community resources  
 The following links provide information about support options and community resources:  

-   [Microsoft support](http://go.microsoft.com/fwlink/?LinkId=243064)  

-   [Configuration Manager Community: System Center Configuration Manager (Current Branch) Survival Guide](http://social.technet.microsoft.com/wiki/contents/articles/33035.system-center-configuration-manager-current-branch-survival-guide.aspx )  

-   [Configuration Manager forums page](https://social.technet.microsoft.com/Forums/en-US/home?category=ConfigMgrCB)  
    <!-- NOTE: the above URL requires "en-US" for the category to work -->