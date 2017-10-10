---
title: "Endpoint Protection malware definitions"
titleSuffix: "Configuration Manager"
description: "Learn to configure Configuration Manager software updates to deliver definition updates to client computers."
ms.custom: na
ms.date: 10/06/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 3b9c4027-a98b-406b-935c-ccabcfe713df
caps.latest.revision: 21
author: NathBarnms.author: nathbarnmanager: angrobe

---

#  Using Configuration Manager Software Updates to Deliver Definition Updates*Applies to: System Center Configuration Manager (Current Branch)*

 You can configure Configuration Manager software updates to deliver definition updates to client computers. This is done by configuring automatic deployment rules. Before you begin to create automatic deployment rules, make sure that you have configured Configuration Manager software updates. For more information, see [Introduction to software updates in System Center Configuration Manager](/sccm/sum/understand/software-updates-introduction).

> [!NOTE]
>  This procedure is only for the items that must be specifically configured for Endpoint Protection. For more information about the Create Automatic Deployment Rule Wizard, see [Automatically deploy software updates](/sccm/sum/deploy-use/automatically-deploy-software-updates).

## To configure an automatic deployment rule to deliver definition updates

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

14. Optionally, you can filter out superseded updates.   To do so:
  1.  In the **Property filters** list, select the **Superseded** check box.
  2.  In the **Search criteria** list, click **<items to find\>**. Then, in the **Search Criteria** dialog box, in the **Specify the value to search for** list, select **No**.  <br><br>

15. Click **OK** to close the **Search Criteria** dialog box, and then click **Next**.

16. On the **Evaluation Schedule** page of the wizard, select **Enable rule to run on a schedule**, and then configure the schedule by which to download definition updates. At a minimum, set the rule to run two hours after each software update point synchronization. Click **Next**.

17. On the **Deployment Schedule** page of the wizard, configure the following settings:

    -   **Time based on**: Select **UTC** if you want all clients in the hierarchy to install the latest definitions at the same time. The actual installation time will vary within a two-hour window. This setting is a recommended best practice.

    -   **Software available time**: Specify the available time for the deployment that is created by this rule. The specified time must be at least one hour after the automatic deployment rule runs. This helps to ensure that the content has sufficient time to replicate to the distribution points in your hierarchy. Some definition updates might also include antimalware engine updates, which might take longer to reach distribution points.

    -   **Installation deadline**: Select **As soon as possible**.

        > [!NOTE]
        >  Software update deadlines are varied over a two-hour period to prevent all clients from requesting an update at the same time.

18. Click **Next**.

19. On the **User Experience** page of the wizard, in the **User notifications** list, select **Hide in Software Center and all notifications**.   This ensures that the definition updates install silently. Click **Next**.

20. On the **Alerts** page of the wizard, you do not have to configure any alerts. Endpoint Protection in Configuration Manager generates any alerts that might be required. Click **Next**.

21. On the **Download Settings** page of the wizard, select the necessary software updates download behavior, and then click **Next**.

22. On the **Deployment Package** page of the wizard, select an existing deployment package or create a new deployment package to contain the software update files associated with the rule.

    > [!NOTE]
    >  Consider placing definition updates in a package that does not contain other software updates. This strategy keeps the size of the definition update package smaller, which allows it to replicate to distribution points more quickly.

23. On the **Distribution Points** page of the wizard, select one or more distribution points to which the content for this package will be copied, and then click **Next**.

24. On the **Download Location** page of the wizard, select **Download software updates from the Internet**, and then click **Next**.

25. On the **Language Selection** page of the wizard, select each language version of the updates to be downloaded, and then click **Next**.

26. Complete the Create Automatic Deployment Rule Wizard.

27. Verify that the new rule is displayed in the **Automatic Deployment Rules** node of the Configuration Manager console.


> [!div class="button"]
[Next step >](endpoint-antimalware-policies.md)

> [!div class="button"]
[Back >](endpoint-configure-alerts.md)
