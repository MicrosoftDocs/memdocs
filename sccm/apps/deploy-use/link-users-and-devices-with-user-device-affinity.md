---
title: "Link users and devices with user device affinity"
description: "Link users and devices with user device affinity and automatically deploy apps to all devices associated with a user."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5b30b0d5-722d-4d4b-9ed7-5a43de315461
caps.latest.revision: 7
caps.handback.revision: 0
author: mattbriggs
ms.author: mabrigg
manager: angrobe

---
# Link users and devices with user device affinity in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

User device affinity in System Center Configuration Manager (Configuration Manager) associates a user with one or more devices. This can eliminate the need to know the names of a user’s devices to deploy an application to the user. Instead of deploying the application to each of the user’s devices, you deploy the application to the user. Then, user device affinity automatically ensures that the application installs on all devices that are associated with that user.  

 You can define primary devices that typically are the devices that users use on a daily basis to perform their work. When you create an affinity between a user and a device, you gain more app deployment options. For example, if a user requires Microsoft Visio, you can install it on the user’s primary device by using a Windows Installer deployment. However, on a device that's not a primary device, you might deploy Visio as a virtual application. You also can use user device affinity to predeploy software on a user’s device when the user isn't logged on so that, when the user logs on, the app is already installed and ready to run.  

 You must manage user device affinity information for computers. Configuration Manager automatically manages user device affinities for the mobile devices that it enrolls.  

## Manually set up user device affinity  

1.  In the Configuration Manager console, choose **Assets and Compliance** > **Devices**.  

3.  In the list, select a device. Then, on the **Home** tab, in the **Device** group, choose **Edit Primary Users**.  

4.  In the **Edit Primary Users** dialog box, search for and then select the users to add as primary users for the selected device. Choose **Add**.  

    > [!NOTE]  
    > The **Primary Users** list shows users who are already primary users of this device, and the method by which each user-device relationship was assigned.  

## Set up primary devices for a user  

1.  In the Configuration Manager console, choose **Assets and Compliance** > **Users**.  

3.  In the list, select a user. Then, on the **Device** tab, choose **Edit Primary Devices**.  

4.  In the **Edit Primary Devices** dialog box, search for and then select the devices to add as primary devices for the selected user. Choose **Add**.  

    > [!NOTE]  
    > The **Primary Devices** list shows devices that are already set up as primary devices for this user, and the method by which each user-device relationship was assigned.  

## Automatically create user device affinities (Windows PCs only)  
 Configuration Manager reads data about user logons from the Windows Event log. To automatically create user device affinities, you must turn on these two options in the local security policy on client computers to store logon events in the Windows Event log:  

-   **Audit account logon events**  
-   **Audit logon events**  

 To configure these settings, use Windows Group Policy.  

> [!IMPORTANT]  
> If an error causes the Windows event log to generate a high number of entries, a new event log might be created. If this occurs, existing logon events might be no longer be available to Configuration Manager.  
>   
> Be careful when you turn on the **Audit account logon events** and **Audit logon events** settings in Windows XP. By default, the retention policy is 7 days, and it is very likely that these events will fill up the security event log. Standard users won't be able to log on if the event log is full. To prevent this, for the security event log, set the policy **Retention Method** value to **Overwrite events as needed**. For sufficient data for user device affinity, also set the policy maximum security event log size to a reasonable value, such as 5-20 MB.  

### Set up the site to automatically create user device affinities  

1.  In the Configuration Manager console, choose **Administration** > **Client Settings**.  

2.  To modify the default client settings, select **Default Client Settings**, and then, on the **Home** tab, in the **Properties** group, choose **Properties**. To create custom client agent settings, select the **Client Settings** node, and then, on the **Home** tab, in the **Create** group, choose **Create Custom Client Device Settings**.  

    > [!NOTE]  
    > If you modify the default client settings, they will be deployed to all computers in the hierarchy. For more information about configuring client settings, see [How to configure client settings in System Center Configuration Manager](../../core/clients/deploy/configure-client-settings.md).  

3.  For **User and Device Affinity**, set the following:  

    -   **User device affinity threshold (minutes)**. Set the number of minutes of device usage before a user device affinity is created.  

    -   **User device affinity threshold (days)**. Set the number of days over which the usage-based affinity threshold is measured.  

    -   **Automatically configure user device affinity from usage data**. To let the site automatically create user device affinities, from the drop-down list, select **True**. If you select **False**, you must approve all user device affinity assignments.  

    > [!TIP]  
    > **Example:** If you set **User device affinity threshold (minutes)** to **60** minutes and you set **User device affinity threshold (days)** to**5** days, the user must use the device for at least 60 minutes over a period of 5 days to automatically create a user device affinity.  

After an automatic user device affinity is created, Configuration Manager continues to monitor the user device affinity thresholds. If the user’s activity for the device falls below the thresholds you've set, the user device affinity is removed. Set **User device affinity threshold (days)** to a value of at least **7** days to avoid situations in which an automatically configured user device affinity might be lost while the user is not logged on, for example, during the weekend.  

## Import user device affinities from a file  
 To create many relationships at one time, you can import a file that has the details for multiple user device affinities. For this procedure, the subject devices must have been discovered and exist as resources in the Configuration Manager database, or the procedure will fail.  

1.  In the Configuration Manager console, choose **Assets and Compliance** > **Users** or **Devices**.  

2.  On the **Home** tab, in the **Create** group, choose **Import User Device Affinity**.  

3.  In the Import User Device Affinity Wizard, on the **Choose Mapping** page, set this information:  

    -   **File name**. Specify a comma-separated values (CSV) file that has a list of users and devices between which you want to create an affinity. In this file, each user-and-device pair must be on its own row, with values separated by a comma. Use this format: <*Domain*>&#92;<*user name*>,<*device NetBIOS name*>.  

    -   **This file has column headings for reference purposes**. If the .csv file has a top-row header, select this option and the header row is ignored during the import.  

4.  If the file you are importing has more than two items in each row, you can use **Column** and **Assign** to specify which columns represent users and devices, and which columns to ignore during import.  

5.  Choose **Next**, and then finish the Import User Device Affinity Wizard.  

## Let users create their own device affinities  
 With the next procedures, you can set up a user to create their own user device affinity in the Software Center app.  

### Set up the site to allow user-created user device affinity requests  

1.  In the Configuration Manager console, choose **Administration** > **Client Settings**.  

2.  To modify the default client settings, select **Default Client Settings**, and then, on the **Home** tab, in the **Properties** group, choose **Properties**. To create custom client agent settings, select the **Client Settings** node, and then, on the **Home** tab, in the **Create** group, choose **Create Custom Client User Settings**.  

    > [!NOTE]  
    > If you modify the default client settings, they will be deployed to all computers in the hierarchy. For more information about configuring client settings, see [Configure client settings](../../core/clients/deploy/configure-client-settings.md).  

3.  Select the client setting **User and Device Affinity** and then, in the **Allow user to define their primary devices** drop-down list, select **True**.  

### Set up a user device affinity  

1.  In the Application Catalog, choose **My Systems**.  

2.  Select the option **I regularly use this computer to do my work**.  

## Manage user device affinity requests from users  
 When the client setting **Automatically configure user device affinity from usage data** is set to **False**, you must approve all user device affinity assignments.  

### Approve or reject a user device affinity request  

1.  In the Configuration Manager console, choose **Assets and Compliance**.  

2.  In the **Assets and Compliance** workspace, select the user or device collection for which you want to manage affinity requests.  

3.  On the **Home** tab, in the **Collection** group, choose **Manage Affinity Requests**.  

4.  In the **Manage User Device Affinity Requests** dialog box, select an affinity request, and then choose **Approve** or **Reject**.  
