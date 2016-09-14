---
title: "Configuring Endpoint Protection in System Center Configuration Manager"
ms.custom: na
ms.date: 2016-08-05
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
translation.priority.ht:
  - cs-cz
  - de-de
  - en-gb
  - es-es
  - fr-fr
  - hu-hu
  - it-it
  - ja-jp
  - ko-kr
  - nl-nl
  - pl-pl
  - pt-br
  - pt-pt
  - ru-ru
  - sv-se
  - tr-tr
  - zh-cn
  - zh-tw
---
# Configure Endpoint Protection in System Center Configuration Manager
Before you can use Endpoint Protection to manage security and malware on Configuration Manager client computers, you must perform the configuration steps detailed in this topic.  

## How to Configure Endpoint Protection in Configuration Manager  
 Endpoint Protection in Configuration Manager has external dependencies and dependencies in the product.  

### Steps to Configure Endpoint Protection in Configuration Manager  
 Use the following table for the steps, details, and more information about how to configure Endpoint Protection.  

> [!IMPORTANT]  
>  If you manage endpoint protection for Windows 10 computers, then you must configure Configuration Manager to update and distribute malware definitions for Windows Defender. Windows Defender is included in Windows 10 but SCEPInstall must still be installed and custom client settings for Endpoint Protection (**Step 5** below) are still required.  

|Steps|Details|  
|-----------|-------------|  
|**Step 1:** Create an Endpoint Protection point site system role.|The Endpoint Protection point site system role must be installed before you can use Endpoint Protection. It must be installed on one site system server only, and it must be installed at the top of the hierarchy on a central administration site or a stand-alone primary site. See [Step 1: Create an Endpoint Protection Point Site System Role](../../protect/deploy-use/configure-endpoint-protection.md#BKMK_Step1) in this topic.|  
|**Step 2:** Configure alerts for Endpoint Protection.|Alerts inform the administrator when specific events have occurred, such as a malware infection. Alerts are displayed in the **Alerts** node of the **Monitoring** workspace, or optionally can be emailed to specified users. See [Step 2: Configure Alerts for Endpoint Protection](../../protect/deploy-use/configure-endpoint-protection.md#BKMK_EPalerts).|  
|**Step 3:** Configure definition update sources for Endpoint Protection clients.|Endpoint Protection can be configured to use various sources to download definition updates. See [Step 3: Configure Definition Updates for Endpoint Protection](../../protect/deploy-use/configure-endpoint-protection.md#BKMK_EPdefs).|  
|**Step 4:** Configure the default antimalware policy and create any custom antimalware policies.|The default antimalware policy is applied when the Endpoint Protection client is installed. Any custom policies you have deployed are applied by default, within 60 minutes of deploying the client. Ensure that you have configured antimalware policies before you deploy the Endpoint Protection client.See [How to create and deploy antimalware policies for Endpoint Protection in System Center Configuration Manager](../../protect/deploy-use/antimalware-policies-for-endpoint-protection.md).|  
|**Step 5:** Configure custom client settings for Endpoint Protection.|Use custom client settings to configure Endpoint Protection settings for collections of computers in your hierarchy.<br /><br /> Note: Do not configure the default Endpoint Protection client settings unless you are sure that you want these settings applied to all computers in your hierarchy. See [Step 5: Configure Custom Client Settings for Endpoint Protection](../../protect/deploy-use/configure-endpoint-protection.md#BKMK_EPclient) in this topic.|  

###  <a name="BKMK_Step1"></a> Step 1: Create an Endpoint Protection  Point Site System Role  
 Use one of the following procedures depending on whether you want to install a new site system server for Endpoint Protection or use an existing site system server.  

> [!IMPORTANT]  
>  When you install an Endpoint Protection point, an Endpoint Protection client is installed on the server hosting the Endpoint Protection point. Services and scans are disabled on this client to enable it to co-exist with any existing antimalware solution that is installed on the server. If you later enable this server for management by Endpoint Protection and select the option to remove any third-party antimalware solution, the third-party product will not be removed. You must uninstall this product manually.  

##### To install and configure the Endpoint Protection  point site system role: New site system server  

1.  In the Configuration Manager console, click **Administration**.  

2.  In the **Administration** workspace, expand **Site Configuration**, and then click **Servers and Site System Roles**.  

3.  On the **Home** tab, in the **Create** group, click **Create Site System Server**.  

4.  On the **General** page, specify the general settings for the site system, and then click **Next**.  

5.  On the **System Role Selection** page, select **Endpoint Protection point** in the list of available roles, and then click **Next**.  

6.  On the **Endpoint Protection** page, select the **I accept the Endpoint Protection license terms** check box, and then click **Next**.  

    > [!IMPORTANT]  
    >  You cannot use Endpoint Protection in Configuration Manager unless you accept the license terms.  

7.  On the **Microsoft Active Protection Service** page, select the level of information that you want to send to Microsoft to help develop new definitions, and then click **Next**.  

    > [!NOTE]  
    >  This option configures the Microsoft Active Protection Service settings that are used by default. You can then configure custom settings for each antimalware policy you create. Join Microsoft Active Protection Service, to help to keep your computers more secure by supplying Microsoft with malware samples that can help Microsoft to keep antimalware definitions more up-to-date. Additionally, when you join Microsoft Active Protection Service, the Endpoint Protection client can use the dynamic signature service to download new definitions before they are published to Windows Update. For more information, see [How to create and deploy antimalware policies for Endpoint Protection in System Center Configuration Manager](../../protect/deploy-use/antimalware-policies-for-endpoint-protection.md).  

8.  Complete the wizard.  

##### To install and configure the Endpoint Protection point site system role: Existing site system server  

1.  In the Configuration Manager console, click **Administration**.  

2.  In the **Administration** workspace, expand **Site Configuration**, click **Servers and Site System Roles**, and then select the server that you want to use for Endpoint Protection.  

3.  On the **Home** tab, in the **Server** group, click **Add Site System Roles**.  

4.  On the **General** page, specify the general settings for the site system, and then click **Next**.  

5.  On the **System Role Selection** page, select **Endpoint Protection point** in the list of available roles, and then click **Next**.  

6.  On the **Endpoint Protection** page, select the **I accept the Endpoint Protection license terms** check box, and then click **Next**.  

    > [!IMPORTANT]  
    >  You cannot use Endpoint Protection in Configuration Manager unless you accept the license terms.  

7.  On the **Microsoft Active Protection Service** page, select the level of information that you want to send to Microsoft to help develop new definitions, and then click **Next**.  

    > [!NOTE]  
    >  This option configures the Microsoft Active Protection Service settings that are used by default. You can configure custom settings for each antimalware policy you configure. For more information, see [How to create and deploy antimalware policies for Endpoint Protection in System Center Configuration Manager](../../protect/deploy-use/antimalware-policies-for-endpoint-protection.md).  

8.  Complete the wizard.  

###  <a name="BKMK_EPalerts"></a> Step 2: Configure Alerts for Endpoint Protection  
 You can configure Endpoint Protection alerts in Microsoft System Center 2012 Configuration Manager to notify administrative users when specific security events occur in your hierarchy. Notifications display in the Endpoint Protection dashboard in the Configuration Manager console, in reports, and you can configure them to be emailed to specified recipients.  

 Use the following steps and the supplemental procedures in this topic to configure alerts for Endpoint Protection in Configuration Manager.  

> [!IMPORTANT]  
>  You must have the **Enforce Security** permission for collections to configure Endpoint Protection alerts.  

#### Steps to Configure Alerts for Endpoint Protection in Configuration Manager  

1.  In the Configuration Manager console, click **Assets and Compliance**.  

2.  In the **Assets and Compliance** workspace, click **Device Collections**.  

3.  In the **Device Collections** list, select the collection for which you want to configure alerts, and then on the **Home** tab, in the **Properties** group, click **Properties**.  

    > [!NOTE]  
    >  You cannot configure alerts for user collections.  

4.  On the **Alerts** tab of the *<Collection Name\>***Properties** dialog box, select **View this collection in the Endpoint Protection dashboard** if you want to view details about antimalware operations for this collection in the **Monitoring** workspace of the Configuration Manager console.  

    > [!NOTE]  
    >  This option is unavailable for the **All Systems** collection.  

5.  On the **Alerts** tab of the *<Collection Name\>***Properties** dialog box, click **Add**.  

6.  In the **Add New Collection Alerts** dialog box, in the **Generate an alert when these conditions apply** section, select the alerts that you want Configuration Manager to generate when the specified Endpoint Protection events occur, and then click **OK**.  

7.  In the  **Conditions** list of the **Alerts** tab, select each Endpoint Protection alert, and then specify the following information:  

    -   **Alert Name** – Accept the default name or enter a new name for the alert.  

    -   **Alert Severity** – In the list, select the alert level to display in the Configuration Manager console.  

8.  Depending on the alert that you select, specify the following additional information:  

    -   **Malware detection** - This alert is generated if malware is detected on any computer in the collection that you monitor. The **Malware detection threshold** specifies the malware detection levels at which this alert is generated:  

        -   **High – All detections** - The alert is generated when there are one or more computers in the specified collection on which any malware is detected, regardless of what action the Endpoint Protection client takes.  

        -   **Medium – Detected, pending action** - The alert is generated when there is one or more computers in the specified collection on which malware is detected, and you must manually remove the malware.  

        -   **Low – Detected, still active** - The alert is generated when there are one or more computers in the specified collection on which malware is detected and is still active.  

    -   **Malware outbreak** - This alert is generated if specified malware is detected on a specified percentage of computers in the collection that you monitor.  

        -   **Percentage of computers with malware detected** – The alert is generated when the percentage of computers with malware that is detected in the collection exceeds the percentage that you specify. Specify a percentage from **1** through **99**.  

            > [!NOTE]  
            >  The percentage value is based on the number of computers in the collection, but excludes computers that do not have a Configuration Manager client installed. It includes computers that do not yet have the Endpoint Protection client installed.  

    -   **Repeated malware detection** - This alert is generated if specific malware is detected more than a specified number of times over a specified number of hours on the computers in the collection that you monitor. Specify the following information to configure this alert:  

        -   **Number of times malware has been detected:** - The alert is generated when the same malware is detected on computers in the collection more than the specified number of times. Specify a number from **2** through **32**.  

        -   **Interval for detection (hours):** Specify the detection interval (in hours) in which the number of malware detections must occur. Specify a number from **1** through **168**.  

    -   **Multiple malware detection** - This alert is generated if more than a specified number of malware types are detected over a specified number of hours on computers in the collection that you monitor. Specify the following information to configure this alert:  

        -   **Number of malware types detected:** The alert is generated when the specified number of different malware types are detected on computers in the collection. Specify a number from **2** through **32**.  

        -   **Interval for detection (hours):** Specify the detection interval, in hours, in which the number of malware detections must occur. Specify a number from **1** through **168**.  

9. Click **OK** to close the *<Collection Name\>***Properties** dialog box.  

###  <a name="BKMK_EPdefs"></a> Step 3: Configure Definition Updates for Endpoint Protection  
 With Endpoint Protection in Microsoft System Center 2012 Configuration Manager, you can use any of several available methods to keep antimalware definitions up to date on client computers in your hierarchy. The information in this topic can help you to select and configure these methods.  

 To update antimalware definitions, you can use one or more of the following methods:  

-   Updates distributed from Configuration Manager – This method uses Configuration Manager software updates to deliver definition and engine updates to computers in your hierarchy.  

-   Updates distributed from Windows Server Update Services (WSUS) – This method uses your WSUS infrastructure to deliver definition and engine updates to computers.  

-   Updates distributed from Microsoft Update – This method allows computers to connect directly to Microsoft Update in order to download definition and engine updates. This method can be useful for computers that are not often connected to the business network.  

-   Updates distributed from Microsoft Malware Protection Center – This method will download definition updates from the Microsoft Malware Protection Center.  

-   Updates from UNC file shares – With this method, you can save the latest definition and engine updates to a share on the network. Clients can then access the network to install the updates.  

 You can configure multiple definition update sources and control the order in which they are assessed and applied. This is done in the **Configure Definition Update Sources** dialog box when you create an antimalware policy.  

> [!IMPORTANT]  
>  If you manage Windows 10 Technical Preview computers, then you must configure Endpoint Protection to update malware definitions for Windows Defender.  

#### How to Configure Definition Update Sources  
 Use the following procedure to configure the definition update sources to use for each antimalware policy.  

###### To configure definition update sources  

1.  In the Configuration Manager console, click **Assets and Compliance**.  

2.  In the **Assets and Compliance** workspace, expand **Endpoint Protection**, and then click **Antimalware Policies**.  

3.  Open the properties page of the **Default Antimalware Policy** or create a new antimalware policy. For more information about how to create antimalware policies, see [How to create and deploy antimalware policies for Endpoint Protection in System Center Configuration Manager](../../protect/deploy-use/antimalware-policies-for-endpoint-protection.md).  

4.  In the **Definition updates** section of the antimalware properties dialog box, click **Set Source**.  

5.  In the **Configure Definition Update Sources** dialog box, select the sources to use for definition updates. You can click **Up** or **Down** to modify the order in which these sources are used.  

6.  Click **OK** to close the **Configure Definition Update Sources** dialog box.  

####  <a name="BKMK_EPsup"></a> Using Configuration Manager Software Updates to Deliver Definition Updates  
 You can configure Configuration Manager software updates to deliver definition updates to client computers. This is done by configuring automatic deployment rules. Before you begin to create automatic deployment rules, make sure that you have configured Configuration Manager software updates. For more information, see [Introduction to software updates in System Center Configuration Manager](../../sup/understand/software-updates-introduction.md).  

> [!NOTE]  
>  This procedure is only for the items that must be specifically configured for Endpoint Protection. For more information about the Create Automatic Deployment Rule Wizard, see [Manage software updates in System Center Configuration Manager](../../sup/deploy-use/manage-software-updates.md).  

###### To configure an automatic deployment rule to deliver definition updates  

1.  In the Configuration Manager console, click **Software Library**.  

2.  In the **Software Library** workspace, expand **Software Updates**, and then click **Automatic Deployment Rules**.  

3.  On the **Home** tab, in the **Create** group, click **Create Automatic Deployment Rule**.  

4.  On the **General** page of the **Create Automatic Deployment Rule Wizard**, specify the following information:  

    -   **Name**: Enter a unique name for the automatic deployment rule.  

    -   **Collection**: Select the collection of client computers to which you want to deploy definition updates.  

        > [!NOTE]  
        >  You cannot deploy definition updates to a collection of users.  

5.  Click **Add to an existing Software Update Group**.  

6.  Make sure that the  **Enable the deployment after this rule is run** check box is selected, and then click **Next**.  

7.  On the **Deployment Settings** page of the wizard, in the **Detail level** list, select **Minimal**, and then click **Next**.  

    > [!NOTE]  
    >  From the **Detail level** list, select **Minimal** (Configuration Manager with no Service Pack) or **Only error messages** (Configuration Manager). This will reduce the number of state messages returned by definition deployment. This configuration helps reduce the CPU processing usage on the Configuration Manager servers.  

8.  In the **Property filters** list, select the **Update Classification** check box.  

9. In the **Search criteria** list, click **<items to find\>**. Then, in the **Search Criteria** dialog box, in the **Specify the value to search for** list, select **Definition Updates**.  

10. Click **OK** to close the **Search Criteria** dialog box.  

11. In the **Property filters** list, select the **Product** check box.  

12. In the **Search criteria** list, click **<items to find\>**. Then, in the **Search Criteria** dialog box, in the **Specify the value to search for** list, select **Forefront Endpoint Protection 2010** for Windows 8.1 and earlier or **Windows Defender** for Windows 10 and later.  

13. Click **OK** to close the **Search Criteria** dialog box, and then click **Next**.  

14. In the **Property filters** list, select the **Superseded** check box.  

15. In the **Search criteria** list, click **<items to find\>**. Then, in the **Search Criteria** dialog box, in the **Specify the value to search for** list, select **No**.  

16. Click **OK** to close the **Search Criteria** dialog box, and then click **Next**.  

17. On the **Evaluation Schedule** page of the wizard, select **Enable rule to run on a schedule**, and then configure the schedule by which to download definition updates. At a minimum, set the rule to run two hours after each software update point synchronization. Click **Next**.  

18. On the **Deployment Schedule** page of the wizard, configure the following settings:  

    -   **Time based on**: Select **UTC** if you want all clients in the hierarchy to install the latest definitions at the same time. The actual installation time will vary within a two-hour window. This setting is a recommended best practice.  

    -   **Software available time**: Specify the available time for the deployment that is created by this rule. The specified time must be at least one hour after the automatic deployment rule runs. This helps to ensure that the content has sufficient time to replicate to the distribution points in your hierarchy. Some definition updates might also include antimalware engine updates, which might take longer to reach distribution points.  

    -   **Installation deadline**: Select **As soon as possible**.  

        > [!NOTE]  
        >  Software update deadlines are varied over a two-hour period to prevent all clients from requesting an update at the same time.  

19. Click **Next**.  

20. On the **User Experience** page of the wizard, in the **User notifications** list, select **Hide in Software Center and all notifications**.   This ensures that the definition updates install silently. Click **Next**.  

21. On the **Alerts** page of the wizard, you do not have to configure any alerts. Endpoint Protection in Configuration Manager generates any alerts that might be required. Click **Next**.  

22. On the **Download Settings** page of the wizard, select the necessary software updates download behavior, and then click **Next**.  

23. On the **Deployment Package** page of the wizard, select an existing deployment package or create a new deployment package to contain the software update files associated with the rule.  

    > [!NOTE]  
    >  Consider placing definition updates in a package that does not contain other software updates. This strategy keeps the size of the definition update package smaller, which allows it to replicate to distribution points more quickly.  

24. On the **Distribution Points** page of the wizard, select one or more distribution points to which the content for this package will be copied, and then click **Next**.  

25. On the **Download Location** page of the wizard, select **Download software updates from the Internet**, and then click **Next**.  

26. On the **Language Selection** page of the wizard, select each language version of the updates to be downloaded, and then click **Next**.  

27. Complete the Create Automatic Deployment Rule Wizard.  

28. Verify that the new rule is displayed in the **Automatic Deployment Rules** node of the Configuration Manager console.  

#### Using Windows Server Update Services (WSUS) to Deliver Definitions  
 If you use WSUS to keep your antimalware definitions up to date, you can configure it to auto-approve definition updates. Although using Configuration Manager software updates is the recommended method to keep definitions up to date, you can also configure WSUS as a method to allow users to manually initiate definition updated. Use the following procedures to configure WSUS as a definition update source.  

##### Configuring Update Synchronization  
 To configure Configuration Manager software updates to synchronize Endpoint Protection definition updates, use the following procedure.  

###### To synchronize Endpoint Protection definition updates in Configuration Manager  

1.  In the Configuration Manager console, click **Administration**.  

2.  In the **Administration** workspace, expand **Site Configuration**, and then click **Sites**.  

3.  Select the site that contains your software update point. In the **Settings** group, click **Configure Site Components**, and then click **Software Update Point**.  

4.  On the **Classifications** tab of the **Software Update Point Component Properties** dialog box, select the **Definition Updates** check box.  

5.  Specify the **Products** updated with WSUS:  

    -   For Windows 8.1 and earlier, on the **Products** tab of the **Software Update Point Component Properties** dialog box, select the **Forefront Endpoint Protection 2010** check box.  

    -   For Windows 10 and later, on the **Products** tab of the **Software Update Point Component Properties** dialog box, select the **Windows Defender** and **Windows Technical Preview 2** check boxes.  

6.  Click **OK** to close the **Software Update Point Component Properties** dialog box.  

 Use the following procedure to configure Endpoint Protection updates when your WSUS server is not integrated into your Configuration Manager environment.  

###### To synchronize Endpoint Protection definition updates in standalone WSUS  

1.  In the WSUS administration console, expand **Computers**, click **Options**, and then click **Products and Classifications**.  

2.  Specify the **Products** updated with WSUS:  

    -   For Windows 8.1 and earlier, on the **Products** tab of the **Software Update Point Component Properties** dialog box, select the **Forefront Endpoint Protection 2010** check box.  

    -   For Windows 10 and later, on the **Products** tab of the **Software Update Point Component Properties** dialog box, select the **Windows Defender** and **Windows Technical Preview 2** check boxes.  

3.  On the **Classifications** tab of the **Products and Classifications** dialog box, select the **Definition Updates** and **Updates** check boxes.  

##### Approving Definition Updates  
 Endpoint Protection definition updates must be approved and downloaded to the WSUS server before they are offered to clients that request the list of available updates. Clients connect to the WSUS server to check for applicable updates and then request the latest approved definition updates.  

###### To approve definitions and updates in WSUS  

1.  In the WSUS administration console, click **Updates**, and then click **All Updates** or the classification of updates that you want to approve.  

2.  In the list of updates, right-click the update or updates you want to approve for installation, and then click **Approve**.  

3.  In the **Approve Updates** dialog box, select the computer group for which you want to approve the updates, and then click **Approved for Install**.  

 In addition to manual approval, you can also set an automatic approval rule for definition updates and Endpoint Protection updates. This will configure WSUS to automatically approve Endpoint Protection definition updates downloaded by WSUS.  

###### To configure an automatic approval rule  

1.  In the WSUS administration console, click **Options**, and then click **Automatic Approvals**.  

2.  On the **Update Rules** tab, click **New Rule**.  

3.  In the **Add Rule** dialog box, under **Step 1: Select properties**, select the **When an update is in a specific classification** check box.  

4.  Under **Step 2: Edit the properties**, click **any classification**.  

5.  Clear all check boxes except **Definition Updates**, and then click **OK**.  

6.  In the **Add Rule** dialog box, under **Step 1: Select properties**, select the **When an update is in a specific product** check box.  

7.  Under **Step 2: Edit the properties**, click **any product**.  

8.  Clear all check boxes except **Forefront Endpoint Protection** for Windows 8.1 and earlier or **Windows Defender** for Windows 10 and later, and then click **OK**.  

9. Under **Step 3: Specify a name**, enter a name for the rule, and then click **OK**.  

10. In the **Automatic Approvals** dialog box, select the check box for the newly created rule and then click **Run rule**.  

> [!NOTE]  
>  To maximize performance on your WSUS server and client computers, decline old definition updates. To accomplish this task, you can configure automatic approval for revisions and automatic declining of expired updates. For more information, see [Microsoft Knowledge Base article 938947](http://go.microsoft.com/fwlink/p/?LinkId=204078).  

#### Using Microsoft Update to Download Definitions  
 When you select to download definition updates from Microsoft Update, clients will check the Microsoft Update site at the interval defined in the **Definition updates** section of the antimalware policy dialog box.  

 This method can be useful when the client does not have connectivity to the Configuration Manager site or when you want users to be able to initiate definition updates.  

> [!IMPORTANT]  
>  Clients must have access to Microsoft Update on the Internet to be able to use this method to download definition updates.  

#### Using the Microsoft Malware Protection Center to Download Definitions  
 You can configure clients to download definition updates from the Microsoft Malware Protection Center. This option is used by Endpoint Protection clients to download definition updates if they have not been able to download updates from another source. This update method can be useful if there is a problem with your Configuration Manager infrastructure that prevents the delivery of updates.  

> [!IMPORTANT]  
>  Clients must have access to Microsoft Update on the Internet to be able use this method to download definition updates.  

#### Downloading Definitions from a Share on the Network  
 You can manually download the latest definition updates from Microsoft and then configure clients to download these definitions from a shared folder on the network. Users can also initiate definition updates when you use this update source.  

> [!NOTE]  
>  Clients must have read access to the shared folder to be able to download definition updates.  

 For more information about how to download the definition and engine updates to store on the file share, see [Install the latest Microsoft Forefront Security definition updates](http://www.microsoft.com/security/portal/Definitions/HowToForeFront.aspx).  

###### To configure definition downloads from a file share  

1.  In the Configuration Manager console, click **Assets and Compliance**.  

2.  In the **Assets and Compliance** workspace, expand **Endpoint Protection**, and then click **Antimalware Policies**.  

3.  Open the properties page of the **Default Antimalware Policy** or create a new antimalware policy. For more information about how to create antimalware policies, see [How to create and deploy antimalware policies for Endpoint Protection in System Center Configuration Manager](../../protect/deploy-use/antimalware-policies-for-endpoint-protection.md).  

4.  In the **Definition updates** section of the antimalware properties dialog box, click **Set Source**.  

5.  In the **Configure Definition Update Sources** dialog box, select **Updates from UNC file shares**.  

6.  Click **OK** to close the **Configure Definition Update Sources** dialog box.  

7.  Click **Set Paths**. Then, in the **Configure Definition Update UNC Paths** dialog box, add one or more UNC paths to the location of the definition updates files on a network share.  

8.  Click **OK** to close the **Configure Definition Update UNC Paths** dialog box.  

### Step 4: Create and deploy antimalware policy for Endpoint Protection  
 See [How to create and deploy antimalware policies for Endpoint Protection in System Center Configuration Manager](../../protect/deploy-use/antimalware-policies-for-endpoint-protection.md).  

###  <a name="BKMK_EPclient"></a> Step 5: Configure Custom Client Settings for Endpoint Protection  
 This procedure configures custom client settings for Endpoint Protection which can be deployed to collections of computers in your hierarchy.  

> [!IMPORTANT]  
>  Do not configure the default Endpoint Protection client settings unless you are sure that you want them applied to all computers in your hierarchy.  

##### To enable Endpoint Protection and configure custom client settings  

1.  In the Configuration Manager console, click **Administration**.  

2.  In the **Administration** workspace, click **Client Settings**.  

3.  On the **Home** tab, in the **Create** group, click **Create Custom Client Device Settings**.  

4.  In the **Create Custom Client Device Settings** dialog box, provide a name and a description for the group of settings, and then select **Endpoint Protection**.  

5.  Configure the Endpoint Protection client settings that you require. For a full list of Endpoint Protection client settings that you can configure, see the Endpoint Protection section in [About client settings in System Center Configuration Manager](../../core/clients/deploy/about-client-settings.md).  

    > [!IMPORTANT]  
    >  You must install the Endpoint Protection site system role before you can configure client settings for Endpoint Protection.  

6.  Click **OK** to close the **Create Custom Client Device Settings** dialog box. The new client settings are displayed in the **Client Settings** node of the **Administration** workspace.  

7.  Before the custom client settings can be used, you must deploy them to a collection. Select the custom client settings you want to deploy and then, in the **Home** tab, in the **Client Settings** group, click **Deploy**.  

8.  In the **Select Collection** dialog box, choose the collection to which you want to deploy the client settings and then click **OK**. The new deployment is shown in the **Deployments** tab of the details pane.  

 Client computers will be configured with these settings when they next download client policy. To initiate policy retrieval for a single client, see the Initiate Policy Retrieval for a Configuration Manager Client section in [How to manage clients in System Center Configuration Manager](../../core/clients/manage/manage-clients.md).  

## How to Provision the Endpoint Protection Client in a Disk Image in Configuration Manager  
 You can install the Endpoint Protection client on a computer that you intend to use as a disk image source for Configuration Manager operating system deployment. This computer is typically called the reference computer. After you create the image of the operating system, you can then use Configuration Manager operating system deployment to deploy the image that can contain software packages, including Endpoint Protection, to your client computers.  

 Use the procedures in this topic to help you install and configure the Endpoint Protection client on a reference computer  

### Prerequisites for Installing the Endpoint Protection Client on the Reference Computer  
 The following list contains the required prerequisites for installing the Endpoint Protection client software on a reference computer.  

-   You must have access to the Endpoint Protection client installation package, **scepinstall.exe**. This package can be found in the **Client** folder of the Microsoft System Center 2012 Configuration Manager installation folder on the site server.  

-   To ensure that the Endpoint Protection client is deployed with the configuration that is required in your organization, create an antimalware policy, and then export that policy. You can then specify the antimalware policy to use when you manually install the Endpoint Protection client. For more information, see [How to create and deploy antimalware policies for Endpoint Protection in System Center Configuration Manager](../../protect/deploy-use/antimalware-policies-for-endpoint-protection.md).  

    > [!NOTE]  
    >  The **Default Client Antimalware Policy** cannot be exported.  

-   If you want to install the Endpoint Protection client with the latest definitions, you must download these from the [Microsoft Malware Protection Center](http://go.microsoft.com/fwlink/?LinkID=200965).  

### How to Install the Endpoint Protection Client Software on the Reference Computer  
 You can install the Endpoint Protection client locally on the reference computer from a command prompt. To do so, you must first obtain the installation file **scepinstall.exe**. You can also install the client with an preconfigured antimalware policy or with an antimalware policy that you previously exported.  

##### To install the Endpoint Protection client from a command prompt  

1.  Copy **scepinstall.exe** from the **Client** folder on the System Center 2012 Configuration Manager installation media to the computer on which you want to install the Endpoint Protection client software.  

2.  Open a command prompt with administrator privileges, navigate to the folder where **scepinstall.exe** is located, and then run the following command, adding any additional command line properties that you require:  

    ```  
    scepinstall.exe  
    ```  

     You can specify one of the following command line properties:  

    |Property|Description|  
    |--------------|-----------------|  
    |/s|Specifies that a silent installation will be performed.|  
    |/q|Specifies that a silent extraction of the setup files will be performed.|  
    |/i|Specifies that a normal installation should be performed.|  
    |/noreplace|Specifies that third-party antimalware software is not uninstalled during setup.|  
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

##### To verify that the Endpoint Protection client is installed correctly  

1.  On the reference computer, open **System Center Endpoint Protection** from the Windows notification are.  

2.  On the **Home** tab of the **System Center Endpoint Protection** dialog box, verify that **Real-time protection** is set to **On**.  

3.  Verify that **Up to date** is displayed for **Virus and spyware definitions**.  

4.  To help make sure that your reference computer is ready for imaging, under **Scan options**, select **Full**, and then click **Scan now**.  

### How to Prepare the Endpoint Protection Client for Imaging  
 After you verify that the Endpoint Protection client is installed correctly on the reference computer, you can prepare the computer for imaging. Perform the following steps to prepare the Endpoint Protection client for imaging.  

 For more information about operating system deployment in Configuration Manager, see [Manage operating system images with System Center Configuration Manager](../../osd/deploy-use/manage-operating-system-images.md).  

##### To prepare the Endpoint Protection client for imaging  

1.  On the reference computer, log on as a user that has administrative privileges.  

2.  Download and install **PsTools** from the [Windows SysInternals Site](http://go.microsoft.com/fwlink/?LinkId=215263) on TechNet.  

3.  Open an elevated command prompt, navigate to the folder in which you installed PsTools, and then type the following command  

    ```  
    Psexec.exe –s –i regedit.exe  
    ```  

    > [!IMPORTANT]  
    >  Use caution while you are running the Registry Editor in this manner; the –s option in PsExec.exe runs the Registry Editor with LocalSystem privileges.  

4.  In the Registry Editor, navigate to each of the following registry keys and delete them.  

    > [!IMPORTANT]  
    >  You must delete the registry keys as the last step before imaging the reference computer. The registry keys are recreated when the Endpoint Protection client starts. If you restart the reference computer, you must delete the registry keys again.  

    -   **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\InstallTime**  

    -   **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastScanRun**  

    -   **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastScanType**  

    -   **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastQuickScanID**  

    -   **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastFullScanID**  

    -   **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\RemovalTools\MRT\GUID**  

 After you complete the preceding steps, you can prepare the reference computer for imaging. For more information about operating system deployment in Configuration Manager, see [Manage operating system images with System Center Configuration Manager](../../osd/deploy-use/manage-operating-system-images.md).  

 When an image that contains the Endpoint Protection client software is deployed, the Endpoint Protection client will automatically report information to the Configuration Manager site to which the computer is assigned, and policy applicable to the client computer is downloaded and applied.
