---
title: "Configuring Endpoint Protection | System Center Configuration Manager"
ms.custom: na
ms.date: 08/05/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: e63f2394-6eb1-4a33-bec5-8377fc62a34e
caps.latest.revision: 21
author: NathBarn

---

# Configuring Endpoint Protection in System Center Configuration Manager
Before you can use Endpoint Protection to manage security and malware on Configuration Manager client computers, set it up using this topic.  
  
## How to Configure Endpoint Protection in Configuration Manager  
 Endpoint Protection in Configuration Manager has dependencies within and outside of the product.  
  
### Configure Endpoint Protection in Configuration Manager  
There are five steps for configuring endpoint protection

1.  Create an Endpoint Protection point site system role.
2.  Configure alerts for Endpoint Protection.
3.  Configure definition update sources for Endpoint Protection clients.
4.  Configure the default antimalware policy and create custom antimalware policies.
5.  Configure custom client settings for Endpoint Protection.
  
> [!IMPORTANT]  
>  If you manage endpoint protection for Windows 10 computers, then you must configure Configuration Manager to update and distribute malware definitions for Windows Defender. Windows Defender is included in Windows 10 but SCEPInstall must still be installed and custom client settings for Endpoint Protection (Step 5) are still required.  

###  <a name="BKMK_Step1"></a> Step 1: Create an Endpoint Protection  Point Site System Role  
You have to install the Endpoint Protection point site system role before you can use Endpoint Protection. Install it on only one site system server, at the top of the hierarchy on a central administration site or a stand-alone primary site. 

Use one of the following procedures depending on whether you want to install a new site system server for Endpoint Protection or use an existing site system server.  
  
> [!IMPORTANT]  
>  When you install an Endpoint Protection point, an Endpoint Protection client is installed on the server hosting the Endpoint Protection point. Services and scans are disabled on this client to enable it to co-exist with any existing antimalware solution that is installed on the server. If you later enable this server for management by Endpoint Protection and select the option to remove any third-party antimalware solution, the third-party product will not be removed. You must uninstall this product manually.  
  
##### To install and configure the Endpoint Protection point site system role: New site system server  
  
1.  In the Configuration Manager console, choose **Administration**.  
  
2.  In the **Administration** workspace, expand **Site Configuration**, and then choose **Servers and Site System Roles**.  
  
3.  On the **Home** tab, in the **Create** group, choose **Create Site System Server**.  
  
4.  On the **General** page, specify the general settings for the site system, and then choose **Next**.  
  
5.  On the **System Role Selection** page, select **Endpoint Protection point** in the list of available roles, and then choose **Next**.  
  
6.  On the **Endpoint Protection** page, select the **I accept the Endpoint Protection license terms** check box, and then choose **Next**.  
  
    > [!IMPORTANT]  
    >  You cannot use Endpoint Protection in Configuration Manager unless you accept the license terms.  
  
7.  On the **Microsoft Active Protection Service** page, select the level of information that you want to send to Microsoft to help develop new definitions, and then choose **Next**.  
  
    > [!NOTE]  
    >  This option configures the Microsoft Active Protection Service settings that are used by default. You can then configure custom settings for each antimalware policy you create. Join Microsoft Active Protection Service to help to keep your computers more secure by supplying Microsoft with malware samples that can help Microsoft to keep antimalware definitions more up-to-date. Also, when you join Microsoft Active Protection Service, the Endpoint Protection client can use the dynamic signature service to download new definitions before they are published to Windows Update. For more information, see [How to create and deploy antimalware policies for Endpoint Protection in System Center Configuration Manager](../../protect/deploy-use/antimalware-policies-for-endpoint-protection.md).  
  
8.  Complete the wizard.  

##### To install and configure the Endpoint Protection point site system role: Existing site system server  
  
1.  In the Configuration Manager console, choose **Administration**.  
  
2.  In the **Administration** workspace, expand **Site Configuration**, choose **Servers and Site System Roles**, and then select the server that you want to use for Endpoint Protection.  
  
3.  On the **Home** tab, in the **Server** group, choose **Add Site System Roles**.  
  
4.  On the **General** page, specify the general settings for the site system, and then choose **Next**.  
  
5.  On the **System Role Selection** page, select **Endpoint Protection point** in the list of available roles, and then choose **Next**.  
  
6.  On the **Endpoint Protection** page, select the **I accept the Endpoint Protection license terms** check box, and then choose **Next**.  
  
    > [!IMPORTANT]  
    >  You cannot use Endpoint Protection in Configuration Manager unless you accept the license terms.  
  
7.  On the **Microsoft Active Protection Service** page, select the level of information that you want to send to Microsoft to help develop new definitions, and then choose **Next**.  
  
    > [!NOTE]  
    >  This option configures the Microsoft Active Protection Service settings that are used by default. You can configure custom settings for each antimalware policy you create. For more information, see [How to create and deploy antimalware policies for Endpoint Protection in System Center Configuration Manager](../../protect/deploy-use/antimalware-policies-for-endpoint-protection.md).  
  

8.  Complete the wizard.  

###  <a name="BKMK_EPalerts"></a> Step 2: Configure Alerts for Endpoint Protection  
 You can configure Endpoint Protection alerts in Microsoft System Center 2012 Configuration Manager to notify administrators when specific security events occur in your hierarchy. Notifications display in the Endpoint Protection dashboard in the Configuration Manager console, and reports. You can also set them up to be emailed to specified recipients.  
  
 Use the following steps and the supplemental procedures in this topic to configure alerts for Endpoint Protection in Configuration Manager.  

> [!IMPORTANT]  
>  You must have the **Enforce Security** permission for collections to configure Endpoint Protection alerts.  

#### Steps to Configure Alerts for Endpoint Protection in Configuration Manager  
  
1.  In the Configuration Manager console, choose **Assets and Compliance**.  
  
2.  In the **Assets and Compliance** workspace, choose **Device Collections**.  
  
3.  In the **Device Collections** list, select the collection for which you want to configure alerts, and then on the **Home** tab, in the **Properties** group, choose **Properties**.  
  

    > [!NOTE]  
    >  You cannot configure alerts for user collections.  

4.  On the **Alerts** tab of the *<Collection Name\>***Properties** dialog box, select **View this collection in the Endpoint Protection dashboard** if you want to view details about antimalware operations for this collection in the **Monitoring** workspace of the Configuration Manager console.  

    > [!NOTE]  
    >  This option is unavailable for the **All Systems** collection.  
  
5.  On the **Alerts** tab of the *<Collection Name\>***Properties** dialog box, choose **Add**.  
  
6.  In the **Add New Collection Alerts** dialog box, in the **Generate an alert when these conditions apply** section, select the alerts that you want Configuration Manager to generate when the specified Endpoint Protection events occur, and then choose **OK**.  
  
7.  In the  **Conditions** list of the **Alerts** tab, select each Endpoint Protection alert, and then specify the following information:  

    -   **Alert Name** - Accept the default name or enter a new name for the alert.  

    -   **Alert Severity** - In the list, select the alert level to display in the Configuration Manager console.  

8.  Depending on the alert that you select, specify the following additional information:  

    -   **Malware detection** - This alert is generated if malware is detected on any computer in the collection that you monitor. The **Malware detection threshold** specifies the malware detection levels at which this alert is generated:  

        -   **High - All detections** - The alert is generated when there are one or more computers in the specified collection on which any malware is detected, regardless of what action the Endpoint Protection client takes.  

        -   **Medium - Detected, pending action** - The alert is generated when there is one or more computers in the specified collection on which malware is detected, and you must manually remove the malware.  

        -   **Low - Detected, still active** - The alert is generated when there are one or more computers in the specified collection on which malware is detected and is still active.  

    -   **Malware outbreak** - This alert is generated if specified malware is detected on a specified percentage of computers in the collection that you monitor.  
  
        -   **Percentage of computers with malware detected** - Specify a percentage from **1** through **99**.  
  
            > [!NOTE]  
            >  The percentage value is based on the number of computers in the collection, but excludes computers that do not have a Configuration Manager client installed. It includes computers that do not yet have the Endpoint Protection client installed.  
  
    -   **Repeated malware detection** - This alert is generated if specific malware is detected more than a set number of times over a set number of hours on the computers in the collection that you monitor. Set the following information to configure this alert:  
  
        -   **Number of times malware has been detected:** - Specify a number from **2** through **32**.  
  
        -   **Interval for detection (hours):** - Specify a number from **1** through **168**.  
  
    -   **Multiple malware detection** - This alert is generated if more than a set number of malware types are detected over a set number of hours on computers in the collection that you monitor. Specify the following information to configure this alert:  
  
        -   **Number of malware types detected:** Specify a number from **2** through **32**.  
  
        -   **Interval for detection (hours):** Specify a number of hours from **1** through **168**.  
  
9. Choose **OK** to close the *<Collection Name\>***Properties** dialog box.  
  
###  <a name="BKMK_EPdefs"></a> Step 3: Configure Definition Updates for Endpoint Protection  
 You can choose any of several available methods to keep antimalware definitions up to date on client computers in your hierarchy:  
  

-   Updates distributed from Configuration Manager - This method uses Configuration Manager software updates to deliver definition and engine updates to computers in your hierarchy.  

-   Updates distributed from Windows Server Update Services (WSUS) - This method uses your WSUS infrastructure to deliver definition and engine updates to computers.  

-   Updates distributed from Microsoft Update - This method allows computers to connect directly to Microsoft Update in order to download definition and engine updates. This method can be useful for computers that are not often connected to the business network.  

-   Updates distributed from Microsoft Malware Protection Center - This method will download definition updates from the Microsoft Malware Protection Center.  
  
-   Updates from UNC file shares - With this method, you can save the latest definition and engine updates to a share on the network. Clients can install the updates from the share.  
  
 You can configure multiple definition update sources and control the order in which they are assessed and applied. This is done in the **Configure Definition Update Sources** dialog box when you create an antimalware policy.  

> [!IMPORTANT]  
>  If you manage Windows 10 Technical Preview computers, then you must configure Endpoint Protection to update malware definitions for Windows Defender.  
  
#### Configure Definition Update Sources  
   
1.  In the Configuration Manager console, choose **Assets and Compliance**.  
  
2.  In the **Assets and Compliance** workspace, expand **Endpoint Protection**, and then choose **Antimalware Policies**.  
  
3.  Open the properties page of the **Default Antimalware Policy** or create a new antimalware policy. For more information about how to create antimalware policies, see [How to create and deploy antimalware policies for Endpoint Protection in System Center Configuration Manager](../../protect/deploy-use/antimalware-policies-for-endpoint-protection.md).  
  
4.  In the **Definition updates** section of the antimalware properties dialog box, choose **Set Source**.  
  
5.  In the **Configure Definition Update Sources** dialog box, select the sources to use for definition updates. You can choose **Up** or **Down** to modify the order in which these sources are used.  
  
6.  Choose **OK** to close the **Configure Definition Update Sources** dialog box.  
  

####  <a name="BKMK_EPsup"></a> Using Configuration Manager Software Updates to Deliver Definition Updates  
 You can configure Configuration Manager software updates to deliver definition updates to client computers. This is done by configuring automatic deployment rules. Before you begin to create automatic deployment rules, make sure that you have configured Configuration Manager software updates. For more information, see [Introduction to software updates in System Center Configuration Manager](../../sup/understand/software-updates-introduction.md).  

> [!NOTE]  
>  This procedure is only for the items that must be specifically configured for Endpoint Protection. For more information about the Create Automatic Deployment Rule Wizard, see [Manage software updates in System Center Configuration Manager](../../sup/deploy-use/manage-software-updates.md).  

###### To configure an automatic deployment rule to deliver definition updates  
  
1.  In the Configuration Manager console, choose **Software Library**.  
  
2.  In the **Software Library** workspace, expand **Software Updates**, and then choose **Automatic Deployment Rules**.  
  
3.  On the **Home** tab, in the **Create** group, choose **Create Automatic Deployment Rule**.  
  
4.  On the **General** page of the **Create Automatic Deployment Rule Wizard**, specify the following information:  

    -   **Name**: Enter a unique name for the automatic deployment rule.  

    -   **Collection**: Select the collection of client computers to which you want to deploy definition updates.  

        > [!NOTE]  
        >  You cannot deploy definition updates to a collection of users.  
  
5.  Choose **Add to an existing Software Update Group**.  
  
6.  Make sure that the  **Enable the deployment after this rule is run** check box is selected, and then choose **Next**.  
  
7.  On the **Deployment Settings** page of the wizard, in the **Detail level** list, select **Minimal**, and then click **Next**.  

    > [!NOTE]  
    >  From the **Detail level** list, select **Minimal** (Configuration Manager with no Service Pack) or **Only error messages** (Configuration Manager). This will reduce the number of state messages returned by definition deployment. This configuration helps reduce the CPU processing usage on the Configuration Manager servers.  

8.  In the **Property filters** list, select the **Update Classification** check box.  
  
9. In the **Search criteria** list, choose **<items to find\>**. Then, in the **Search Criteria** dialog box, in the **Specify the value to search for** list, select **Definition Updates**.  
  
10. Choose **OK** to close the **Search Criteria** dialog box.  
  
11. In the **Property filters** list, select the **Product** check box.  
  
12. In the **Search criteria** list, choose **<items to find\>**. Then, in the **Search Criteria** dialog box, in the **Specify the value to search for** list, select **Forefront Endpoint Protection 2010** for Windows 8.1 and earlier or **Windows Defender** for Windows 10 and later.  
  
13. Choose **OK** to close the **Search Criteria** dialog box, and then choose **Next**.  
  
14. In the **Property filters** list, select the **Superseded** check box.  
  
15. In the **Search criteria** list, choose **<items to find\>**. Then, in the **Search Criteria** dialog box, in the **Specify the value to search for** list, select **No**.  
  
16. Choose **OK** to close the **Search Criteria** dialog box, and then choose **Next**.  
  
17. On the **Evaluation Schedule** page of the wizard, select **Enable rule to run on a schedule**, and then configure the schedule by which to download definition updates. At a minimum, set the rule to run two hours after each software update point synchronization. Click **Next**.  

18. On the **Deployment Schedule** page of the wizard, configure the following settings:  

    -   **Time based on**: Select **UTC** if you want all clients in the hierarchy to install the latest definitions at the same time. The actual installation time will vary within a two-hour window. This setting is a recommended best practice.  

    -   **Software available time**: Specify the available time for the deployment that is created by this rule. The specified time must be at least one hour after the automatic deployment rule runs. This helps to ensure that the content has sufficient time to replicate to the distribution points in your hierarchy. Some definition updates might also include antimalware engine updates, which might take longer to reach distribution points.  

    -   **Installation deadline**: Select **As soon as possible**.  

        > [!NOTE]  
        >  Software update deadlines are varied over a two-hour period to prevent all clients from requesting an update at the same time.  
  
19. Choose **Next**.  
  
20. On the **User Experience** page of the wizard, in the **User notifications** list, select **Hide in Software Center and all notifications**.   This ensures that the definition updates install silently. Click **Next**.  
  
21. On the **Alerts** page of the wizard, you do not have to configure any alerts. Endpoint Protection in Configuration Manager generates any alerts that might be required. Choose **Next**.  
  
22. On the **Download Settings** page of the wizard, select the necessary software updates download behavior, and then choose **Next**.  
  
23. On the **Deployment Package** page of the wizard, select an existing deployment package or create a new deployment package to contain the software update files associated with the rule.  
  
    > [!TIP]  
    >  Consider placing definition updates in a package that does not contain other software updates. This strategy keeps the size of the definition update package smaller, which allows it to replicate to distribution points more quickly.  
  
24. On the **Distribution Points** page of the wizard, select one or more distribution points to which the content for this package will be copied, and then choose **Next**.  
  
25. On the **Download Location** page of the wizard, select **Download software updates from the Internet**, and then choose **Next**.  
  
26. On the **Language Selection** page of the wizard, select each language version of the updates to be downloaded, and then choose **Next**.  
  
27. Complete the Create Automatic Deployment Rule Wizard.  

28. Verify that the new rule is displayed in the **Automatic Deployment Rules** node of the Configuration Manager console.  

#### Using Windows Server Update Services (WSUS) to Deliver Definitions  

 If you use WSUS to keep your antimalware definitions up to date, you can configure it to automatically approve definition updates. Although using Configuration Manager software updates is the recommended method to keep definitions up to date, you can also configure WSUS as a method to allow users to manually initiate definition updates. Use the following procedures to configure WSUS as a definition update source.  
  
##### To synchronize Endpoint Protection definition updates in Configuration Manager  
  
1.  In the Configuration Manager console, choose **Administration**.  
  
2.  In the **Administration** workspace, expand **Site Configuration**, and then choose **Sites**.  
  
3.  Select the site that contains your software update point. In the **Settings** group, choose **Configure Site Components**, and then choose **Software Update Point**.  
 
4.  On the **Classifications** tab of the **Software Update Point Component Properties** dialog box, select the **Definition Updates** check box.  

5.  Specify the **Products** updated with WSUS:  

    -   For Windows 8.1 and earlier, on the **Products** tab of the **Software Update Point Component Properties** dialog box, select the **Forefront Endpoint Protection 2010** check box.  

    -   For Windows 10 and later, on the **Products** tab of the **Software Update Point Component Properties** dialog box, select the **Windows Defender** and **Windows Technical Preview 2** check boxes.  
  
6.  Choose **OK** to close the **Software Update Point Component Properties** dialog box.  
  
##### To synchronize Endpoint Protection definition updates in standalone WSUS  
Use this procedure when your WSUS server is not integrated into your Configuration Manager environment.  
  
1.  In the WSUS administration console, expand **Computers**, choose **Options**, and then choose **Products and Classifications**.  
  
2.  Specify the **Products** updated with WSUS:  

    -   For Windows 8.1 and earlier, on the **Products** tab of the **Software Update Point Component Properties** dialog box, select the **Forefront Endpoint Protection 2010** check box.  

    -   For Windows 10 and later, on the **Products** tab of the **Software Update Point Component Properties** dialog box, select the **Windows Defender** and **Windows Technical Preview 2** check boxes.  

3.  On the **Classifications** tab of the **Products and Classifications** dialog box, select the **Definition Updates** and **Updates** check boxes.  
  
##### Approve Definition Updates  
 Endpoint Protection definition updates must be approved and downloaded to the WSUS server before they are distributed to clients that request the list of available updates. Clients connect to the WSUS server to check for applicable updates and then request the latest approved definition updates.  
 
1.  In the WSUS administration console, choose **Updates**, and then choose **All Updates** or the classification of updates that you want to approve.  
  
2.  In the list of updates, right-click the update or updates you want to approve for installation, and then choose **Approve**.  
  
3.  In the **Approve Updates** dialog box, select the computer group for which you want to approve the updates, and then choose **Approved for Install**.  
  
  
 
##### To configure an automatic approval rule  

In addition to manual approval, you can  set an automatic approval rule for definition updates and Endpoint Protection updates. This will configure WSUS to automatically approve Endpoint Protection definition updates downloaded by WSUS. 
  
1.  In the WSUS administration console, choose **Options**, and then choose **Automatic Approvals**.  
  
2.  On the **Update Rules** tab, choose **New Rule**.  
  
3.  In the **Add Rule** dialog box, under **Step 1: Select properties**, select the **When an update is in a specific classification** check box.  
  
4.  Under **Step 2: Edit the properties**, choose **any classification**.  
  
5.  Clear all check boxes except **Definition Updates**, and then choose **OK**.  
  
6.  In the **Add Rule** dialog box, under **Step 1: Select properties**, select the **When an update is in a specific product** check box.  
  
7.  Under **Step 2: Edit the properties**, choose **any product**.  
  
8.  Clear all check boxes except **Forefront Endpoint Protection** for Windows 8.1 and earlier or **Windows Defender** for Windows 10 and later, and then choose **OK**.  
  
9. Under **Step 3: Specify a name**, enter a name for the rule, and then choose **OK**.  
  
10. In the **Automatic Approvals** dialog box, select the check box for the newly created rule and then choose **Run rule**.  
  

> [!NOTE]  
>  To maximize performance on your WSUS server and client computers, decline old definition updates. To accomplish this task, you can configure automatic approval for revisions and automatic declining of expired updates. For more information, see [Microsoft Knowledge Base article 938947](http://go.microsoft.com/fwlink/p/?LinkId=204078).  

#### Using Microsoft Update to Download Definitions  

 When you choose to download definition updates from Microsoft Update, clients will check the Microsoft Update site at the interval defined in the **Definition updates** section of the antimalware policy dialog box.  
  
 This method can be useful when the client does not have connectivity to the Configuration Manager site or when you want users to be able to initiate definition updates.s Clients must have access to Microsoft Update on the Internet to be able to use this method to download definition updates.  
  
#### Using the Microsoft Malware Protection Center to Download Definitions  
 You can configure clients to download definition updates from the Microsoft Malware Protection Center. This option is used by Endpoint Protection clients to download definition updates if they have not been able to download updates from another source. This update method can be useful if there is a problem with your Configuration Manager infrastructure that prevents the delivery of updates. Clients must have access to Microsoft Update on the Internet to be able use this method to download definition updates.  
  
#### To configure definition downloads from a file share  
 You can manually download the latest definition updates from Microsoft and then configure clients to download these definitions from a shared folder on the network. Users can also initiate definition updates when you use this update source. Clients must have read access to the shared folder to be able to download definition updates.  
  
 For more information about how to download the definition and engine updates to store on the file share, see [Install the latest Microsoft Forefront Security definition updates](http://www.microsoft.com/security/portal/Definitions/HowToForeFront.aspx).  
  
1.  In the Configuration Manager console, choose **Assets and Compliance**.  
  
2.  In the **Assets and Compliance** workspace, expand **Endpoint Protection**, and then choose **Antimalware Policies**.  
  
3.  Open the properties page of the **Default Antimalware Policy** or create a new antimalware policy. For more information about how to create antimalware policies, see [How to create and deploy antimalware policies for Endpoint Protection in System Center Configuration Manager](../../protect/deploy-use/antimalware-policies-for-endpoint-protection.md).  
  
4.  In the **Definition updates** section of the antimalware properties dialog box, choose **Set Source**.  
  
5.  In the **Configure Definition Update Sources** dialog box, select **Updates from UNC file shares**.  
  
6.  Choose **OK** to close the **Configure Definition Update Sources** dialog box.  
  
7.  Choose **Set Paths**. Then, in the **Configure Definition Update UNC Paths** dialog box, add one or more UNC paths to the location of the definition updates files on a network share.  
  
8.  Choose **OK** to close the **Configure Definition Update UNC Paths** dialog box.  
  
### Step 4: Create and deploy antimalware policy for Endpoint Protection  

 The default antimalware policy is applied when the Endpoint Protection client is installed. Any custom policies you have deployed are applied by default, within 60 minutes of deploying the client. Ensure that you have configured antimalware policies before you deploy the Endpoint Protection client.See [How to create and deploy antimalware policies for Endpoint Protection in System Center Configuration Manager](../../protect/deploy-use/antimalware-policies-for-endpoint-protection.md). 
  
###  <a name="BKMK_EPclient"></a> Step 5: Configure Custom Client Settings for Endpoint Protection  
 
This procedure configures custom client settings for Endpoint Protection which can be deployed to collections of computers in your hierarchy.  
  
> [!IMPORTANT]  
>  Do not configure the default Endpoint Protection client settings unless you are sure that you want them applied to all computers in your hierarchy.  
  
1.  In the Configuration Manager console, choose **Administration**.  
  
2.  In the **Administration** workspace, choose **Client Settings**.  
  
3.  On the **Home** tab, in the **Create** group, choose **Create Custom Client Device Settings**.  
  
4.  In the **Create Custom Client Device Settings** dialog box, provide a name and a description for the group of settings, and then select **Endpoint Protection**.  

5.  Configure the Endpoint Protection client settings that you require. For a full list of Endpoint Protection client settings that you can configure, see the Endpoint Protection section in [About client settings in System Center Configuration Manager](../../core/clients/deploy/about-client-settings.md).  

    > [!IMPORTANT]  
    >  You must install the Endpoint Protection site system role before you can configure client settings for Endpoint Protection.  
  
6.  Choose **OK** to close the **Create Custom Client Device Settings** dialog box. The new client settings are displayed in the **Client Settings** node of the **Administration** workspace.  
  
7.  Before the custom client settings can be used, you have to deploy them to a collection. Select the custom client settings you want to deploy and then, in the **Home** tab, in the **Client Settings** group, choose **Deploy**.  
  
8.  In the **Select Collection** dialog box, choose the collection to which you want to deploy the client settings and then choose **OK**. The new deployment is shown in the **Deployments** tab of the details pane.  
  
 Client computers will be configured with these settings when they next download client policy. To initiate policy retrieval for a single client, see the Initiate Policy Retrieval for a Configuration Manager Client section in [How to manage clients in System Center Configuration Manager](../../core/clients/manage/manage-clients.md).  
  
## How to provision the endpoint protection client in a disk image in Configuration Manager
  
 You can install the Endpoint Protection client on a computer that you intend to use as a disk image source for Configuration Manager operating system deployment. This computer is typically called the reference computer. After you create the image of the operating system, you can then use Configuration Manager operating system deployment to deploy the image that can contain software packages, including Endpoint Protection, to your client computers.  

 Use the procedures in this topic to help you install and configure the Endpoint Protection client on a reference computer  
  
### Prerequisites for installing the Endpoint Protection client on the reference computer  
 Here are prerequisites for installing the Endpoint Protection client software on a reference computer.  
  
-   You must have access to the Endpoint Protection client installation package, **scepinstall.exe**. This package can be found in the **Client** folder of the Microsoft System Center 2012 Configuration Manager installation folder on the site server.  

-   To ensure that the Endpoint Protection client is deployed with the configuration that is required in your organization, create an antimalware policy, and then export that policy. You can then specify the antimalware policy to use when you manually install the Endpoint Protection client. For more information, see [How to create and deploy antimalware policies for Endpoint Protection in System Center Configuration Manager](../../protect/deploy-use/antimalware-policies-for-endpoint-protection.md).  

    > [!NOTE]  
    >  The **Default Client Antimalware Policy** cannot be exported.  

  
-   If you want to install the Endpoint Protection client with the latest definitions, you must download them from the [Microsoft Malware Protection Center](http://go.microsoft.com/fwlink/?LinkID=200965).  
  
### How to install the Endpoint Protection client software on the reference computer  
 You can install the Endpoint Protection client locally on the reference computer from a command prompt. 

First, obtain the installation file **scepinstall.exe**. You can also install the client with an preconfigured antimalware policy or with an antimalware policy that you previously exported.  
  
  
1.  Copy **scepinstall.exe** from the **Client** folder on the System Center 2012 Configuration Manager installation media to the computer on which you want to install the Endpoint Protection client software.  

2.  Open a command prompt with administrator privileges, navigate to the folder where **scepinstall.exe** is located, and then run the following command, adding any additional command line properties that you require:  

    ```  
    scepinstall.exe  
    ```  

     You can specify one of the following command line properties:  

    |Property|Description|  
    |--------------|-----------------|  
    |/s|Silent installation|  
    |/q|Silent extraction of the setup files|  
    |/i|Normal installation|  
    |/noreplace|Third-party antimalware software is not uninstalled during setup|  
    |/policy|Specifies an antimalware policy file to be used to configure the client during installation.|  
    |/sqmoptin|Specifies that this client software installation is opted in to the Microsoft Customer Experience Improvement Program.|  

3.  Follow the on-screen instructions in order to complete the client installation.  

4.  If you downloaded the latest update definition package, copy the package to the client computer, and then double-click the definition package to install it.  

    > [!NOTE]  
    >  After the Endpoint Protection client installation is completed, the client automatically performs a definition update check. If this update check succeeds, you do not have to manually install the latest definition update package.  

##### To install the client software with an antimalware policy from the command prompt  

1.  Copy **scepinstall.exe** and the exported or preconfigured antimalware policy to the computer on which you want to install the Endpoint Protection client software.  

2.  Open a command prompt with administrator privileges, navigate to the folder where **scepinstall.exe** and the antimalware policy are located, and then run the following command:  

    ```  
    scepinstall.exe /policy <full path>\<policy file>  
    ```  

3.  Follow the on-screen instructions in order to complete the client installation.  

4.  If you downloaded the latest definition package, copy the package to the client computer, and then double-click the definition package to install it.  

    > [!NOTE]  
    >  After the Endpoint Protection client installation is completed, the client automatically performs a definition update check. If this update check succeeds, you do not have to manually install the latest definition update package.  

### Verify that the Endpoint Protection Client is Installed Correctly  
 After you install the Endpoint Protection client on your reference computer, verify that the client is working correctly.  
   
1.  On the reference computer, open **System Center Endpoint Protection** from the Windows notification area.  
  
2.  On the **Home** tab of the **System Center Endpoint Protection** dialog box, verify that **Real-time protection** is set to **On**.  

3.  Verify that **Up to date** is displayed for **Virus and spyware definitions**.  

4.  To help make sure that your reference computer is ready for imaging, under **Scan options**, select **Full**, and then click **Scan now**.  
  
### How to prepare the Endpoint Protection client for imaging  

 After you verify that the Endpoint Protection client is installed correctly on the reference computer, you can prepare the computer for imaging. Perform the following steps to prepare the Endpoint Protection client for imaging.  

 For more information about operating system deployment in Configuration Manager, see [Manage operating system images with System Center Configuration Manager](../../osd/deploy-use/manage-operating-system-images.md).  
 
1.  On the reference computer, log on as a user with administrative privileges.  
  
2.  Download and install **PsTools** from the [Windows SysInternals Site](http://go.microsoft.com/fwlink/?LinkId=215263) on TechNet.  

3.  Open an elevated command prompt, navigate to the folder in which you installed PsTools, and then type the following command  

    ```  
    Psexec.exe -s -i regedit.exe  
    ```  

    > [!IMPORTANT]  
    >  Use caution while you are running the Registry Editor in this manner; the -s option in PsExec.exe runs the Registry Editor with LocalSystem privileges.  

4.  In the Registry Editor, navigate to each of the following registry keys and delete them.  

    > [!IMPORTANT]  
    >  You must delete the registry keys as the last step before imaging the reference computer. The registry keys are recreated when the Endpoint Protection client starts. If you restart the reference computer, you must delete the registry keys again.  

    -   **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\InstallTime**  

    -   **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastScanRun**  

    -   **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastScanType**  

    -   **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastQuickScanID**  

    -   **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastFullScanID**  

    -   **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\RemovalTools\MRT\GUID**  
  
 After you complete these steps, you can prepare the reference computer for imaging. For more information about operating system deployment in Configuration Manager, see [Manage operating system images with System Center Configuration Manager](../../osd/deploy-use/manage-operating-system-images.md).  
  
 When an image that contains the Endpoint Protection client software is deployed, the Endpoint Protection client will automatically report information to the Configuration Manager site to which the computer is assigned, and policy applicable to the client computer is downloaded and applied.

