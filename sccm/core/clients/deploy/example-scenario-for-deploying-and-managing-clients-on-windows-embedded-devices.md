---
title: "Example scenario - deploy Windows Embedded clients | Microsoft Docs"
description: "See an example scenario for deploying and managing System Center Configuration Manager clients on Windows Embedded devices."
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 10049c89-b37c-472b-b317-ce4f56cd4be7
caps.latest.revision: 8
author: arob98
ms.author: angrobe
manager: angrobe

---
# Example scenario for deploying and managing System Center Configuration Manager clients on Windows Embedded devices

*Applies to: System Center Configuration Manager (Current Branch)*

This scenario demonstrates how you can manage write-filter-enabled Windows Embedded devices with Configuration Manager.If your embedded devices do not support write filters, they behave as standard Configuration Manager clients and these procedures don't apply.  

Coho Vineyard & Winery is opening a visitor center and needs kiosks that run Windows Embedded to run interactive presentations. The building for the new visitor center is not close to the IT department, so the kiosks must be managed remotely. In addition to the software that runs the presentations, these devices must run up-to-date antimalware protection software to comply with the company security policies. The kiosks must run 7 days a week, with no downtime while the visitor center is open.  

 Coho already runs Configuration Manager to manage devices on their network. Configuration Manager is configured to run Endpoint Protection, and install software updates and applications. However, because the IT team has not managed Windows Embedded devices before, Jane, the Configuration Manager administrator, runs a pilot to manage two kiosks in the reception lobby.   

 To manage these Windows Embedded devices that are write-filter-enabled, Jane performs the following steps to install the Configuration Manager client, protect the client by using Endpoint Protection, and install the interactive presentation software.  

1.  Jane reads how Windows Embedded devices uses write filters, and how Configuration Manager can make this easier by automatically disabling and then re-enabling the writer filters, to persist a software installation.  

     For more information, see [Planning for client deployment to Windows Embedded devices in System Center Configuration Manager](../../../core/clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md).  

2.  Before she installs the Configuration Manager client, Jane creates a new query-based device collection for the Windows Embedded devices. Because the company uses standard naming formats to identify their computers, Jane can uniquely identify Windows Embedded devices by the first six letters of the computer name: **WEMDVC**. She uses the following WQL query to create this collection: **select SMS_R_System.NetbiosName from SMS_R_System where SMS_R_System.NetbiosName like "WEMDVC%"**  

     This collection allows her to manage the Windows Embedded devices with different configuration options from the other devices. She will use this collection to control restarts, deploy Endpoint Protection with client settings, and deploy the interactive presentation application.  

     See [How to create collections in System Center Configuration Manager](../../../core/clients/manage/collections/create-collections.md).  

3.  Jane configures the collection for a maintenance window to ensure that restarts that might be required for installing the presentation application and any upgrades do not occur during opening hours for the visitor center. Opening hours will be 09:00 through 18:00, Monday through Sunday. She configures the maintenance window for every day, 18:30 through 06:00.  

4.  For more information, see [How to use maintenance windows in System Center Configuration Manager](../../../core/clients/manage/collections/use-maintenance-windows.md).  

5.  Jane then configures a custom device client setting to install the Endpoint Protection client by selecting **Yes** for the following settings, and then deploys this custom client setting to the Windows Embedded device collection:  

    -   **Install Endpoint Protection client on client computers**  

    -   **For Windows Embedded devices with write filters, commit Endpoint Protection client installation (requires restart)**  

    -   **Allow Endpoint Protection client installation and restart to be performed outside maintenance windows**  

     When the Configuration Manager client is installed, these settings install the Endpoint Protection client and ensure that it is persisted in the operating system as part of the installation, rather than written to the overlay only. The company security policies require that the antimalware software is always installed and Jane does not want to run the risk of the kiosks being unprotected for even a short period of time if they restart.  

    > [!NOTE]  
    >  The restarts that are required to install the Endpoint Protection client are a one-time occurrence, which happen during the setup period for the devices and before the visitor center is operational. Unlike the periodic deployment of applications or software definition updates, the next time the Endpoint Protection client is installed on the same device will probably be when the company upgrades to the next version of Configuration Manager.  

     For more information, see [Configuring Endpoint Protection in System Center Configuration Manager](../../../protect/deploy-use/configure-endpoint-protection.md).  

6.  With the configuration settings for the client now in place, Jane prepares to install the Configuration Manager clients. Before she can install the clients, she must manually disable the write filter on the Windows Embedded devices. She reads the OEM documentation that accompanies the kiosks and follows their instructions to disable the write filters.  

     Jane renames the device so it uses the company standard naming format, and then installs the client manually by running CCMSetup with the following command from a mapped drive that holds the client source files: **CCMSetup.exe /MP:mpserver.cohovineyardandwinery.com SMSSITECODE=CO1**  

     This command installs the client, assigns the client to the management point that has the intranet FQDN of **mpserver.cohovineyardandwinery.com**, and assigns the client to the primary site named **CO1**.  

     Jane knows that it always takes a while for clients to install and send back their status to the site. So she waits before she confirms that the clients successfully install, assign to the site, and appear as clients in the collection that she created for Windows Embedded devices.  

     As additional confirmation, she checks the properties of Configuration Manager in Control Panel on the devices and compares them to standard Windows computers that are managed by the site. For example, on the **Components** tab, the **Hardware Inventory Agent** displays **Enabled**, and on the **Actions** tab, there are 11 available actions, which include **Application Deployment Evaluation Cycle** and **Discovery Data Collection Cycle**.  

     Confident that the clients are successfully installed, assigned, and receiving client policy from the management point, Jane then manually enables the write filters by following the instructions from the OEM.  

     For more information, see:  

    -   [How to deploy clients to Windows computers in System Center Configuration Manager](../../../core/clients/deploy/deploy-clients-to-windows-computers.md)  

    -   [How to assign clients to a site in System Center Configuration Manager](../../../core/clients/deploy/assign-clients-to-a-site.md)  

7.  Now that the Configuration Manager client is installed on the Windows Embedded devices, Jane confirms that she can manage them in the same way as she manages the standard Windows clients. For example, from the Configuration Manager console, she can remotely manage them by using remote control, initiate client policy for them, and view client properties and hardware inventory.  

     Because these devices are joined to an Active Directory domain, she does not have to manually approve them as trusted clients and confirms from the Configuration Manager console that they are approved.  

     For more information, see [How to manage clients in System Center Configuration Manager](../../../core/clients/manage/manage-clients.md).  

8.  To install the interactive presentation software, Jane runs the **Deploy Software Wizard** and configures a required application. On the **User Experience** page of the wizard, in the **Write filter handling for Windows Embedded devices** section, she accepts the default option that selects **Commit changes at deadline or during a maintenance window (requires restarts)**.  

     Jane keeps this default option for write filters to ensure that the application persists after a restart, so that it is always available to the visitors using the kiosks. The daily maintenance window provides a safe period during which the restarts for installation and any updates can occur.  

     Jane deploys the application to the Windows Embedded devices collection.  

     For more information, see [How to deploy applications with System Center Configuration Manager](../../../apps/deploy-use/deploy-applications.md).  

9. To configure definition updates for Endpoint Protection, Jane uses software updates and runs the Create Automatic Deployment Rule Wizard. She selects the **Definition Updates** template to prepopulate the wizard with settings that are appropriate for Endpoint Protection.  

     These settings include the following on the **User Experience** page of the wizard:  

    -   **Deadline behavior**: The **Software Installation** check box is not selected.  

    -   **Write filter handling for Windows Embedded devices**: The **Commit changes at deadline or during a maintenance window (requires restarts)** check box is not selected.  

     Jane keeps these default settings. Together, these two options with this configuration allow any software update definitions for Endpoint Protection to be installed in the overlay during the day and not wait to be installed and committed during the maintenance window. This configuration best meets the company security policy for computers to run up-to-date antimalware protection.  

    > [!NOTE]  
    >  Unlike software installations for applications, software update definitions for Endpoint Protection can occur very frequently, even multiple times a day. They are often small files. For these types of security-related deployments, it can often be beneficial to always install to the overlay rather than wait until the maintenance window. The Configuration Manager client will quickly re-install the software definition updates if the device restarts because this action initiates an evaluation check and does not wait until the next scheduled evaluation.  

     Jane selects the Windows Embedded devices collection for the automatic deployment rule.  

     For more information, see  
                  Step 3: Configure Configuration Manager Software Updates to Deliver Definition Updates to Client Computers in [Configuring Endpoint Protection in System Center Configuration Manager](../../../protect/deploy-use/configure-endpoint-protection.md)  

10. Jane decides to configure a maintenance task that periodically commits all changes on the overlay. This task is to support the software update definitions deployment, to reduce the number of updates that accumulate and must be installed again, each time the device restarts. In her experience, this helps the antimalware programs run more efficiently.  

    > [!NOTE]  
    >  These software update definitions would be automatically committed to the image if the embedded devices ran another management task that supported committing the changes. For example, installing a new version of the interactive presentation software would also commit the changes for software update definitions. Or, installing standard software updates every month that install during the maintenance window could also commit the changes for software update definitions. However, in this scenario, where standard software updates do not run and the interactive presentation software is unlikely to be updated very often, it might be months before the software definition updates are automatically committed to the image.  

     Jane first creates a custom task sequence that has no settings other than the name. She runs the Create Task Sequence Wizard:  

    1.  On the **Create a New Task Sequence** page, she selects **Create a new custom task sequence**, and then clicks **Next**.  

    2.  On the **Task Sequence Information** page, she enters **Maintenance task to commit changes on embedded devices** for the task sequence name, and then clicks **Next**.  

    3.  On the **Summary** page, she selects **Next**, and completes the wizard.  

     Jane then deploys this custom task sequence to the Windows Embedded devices collection, and configures the schedule to run every month. As part of the deployment settings, she selects the **Commit changes at deadline or during a maintenance window (requires restarts)** check box to persist the changes after a restart. To configure this deployment, she selects the custom task sequence that she just created, and then on the **Home** tab, in the **Deployment** group, she clicks **Deploy** to start the Deploy Software Wizard:  

    1.  On the **General** page, she selects the Windows Embedded devices collection, and then clicks **Next**.  

    2.  On the **Deployment Settings** page, she selects the **Purpose** of **Required**, and then clicks **Next**.  

    3.  On the **Scheduling** page, she clicks **New** to specify a weekly schedule during the maintenance window, and then clicks **Next**.  

    4.  She completes the wizard without any further changes.  

     For more information, see  
                  [Manage task sequences to automate tasks in System Center Configuration Manager](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md).  

11. For the kiosks to run automatically, Jane writes a script to configure the devices for the following settings:  

    -   Automatically log on, using a guest account that has no password.  

    -   Automatically run the interactive presentation software on startup.  

     Jane uses packages and programs to deploy this script to the Windows Embedded devices collection. When she runs the Deploy Software Wizard, she again selects the **Commit changes at deadline or during a maintenance window (requires restarts)** check box to persist the changes after a restart.  

     For more information, see [Packages and programs in System Center Configuration Manager](../../../apps/deploy-use/packages-and-programs.md).  

12. The following morning, Jane checks the Windows Embedded devices. She confirms the following:  

    -   The kiosk is automatically logged on by using the guest account.  

    -   The interactive presentation software is running.  

    -   The Endpoint Protection client is installed and has the latest software update definitions.  

    -   That the device restarted during the maintenance window.  

     For more information, see:  

    -   [How to monitor Endpoint Protection in System Center Configuration Manager](../../../protect/deploy-use/monitor-endpoint-protection.md)  

    -   [Monitor applications with System Center Configuration Manager](/sccm/apps/deploy-use/monitor-applications-from-the-console)  

13. Jane monitors the kiosks and reports the successful management of them to her manager. As a result, 20 kiosks are ordered for the visitor center.  

     To avoid the manual installation of the Configuration Manager client, which requires manually disabling and then enabling the write filters, Jane ensures that the order includes a customized image that already includes the installation and site assignment of the Configuration Manager client. In addition, the devices are named according to the company naming format.  

     The kiosks are delivered to the visitor center a week before it opens. During this time, the kiosks are connected to the network, all device management for them is automatic, and no local administrator is required. Jane confirms that the kiosks are functioning as required:  

    -   The clients on the kiosks complete site assignment and download the trusted root key from Active Directory Domain Services.  

    -   The clients on the kiosks are automatically added to the Windows Embedded devices collection and configured with the maintenance window.  

    -   The Endpoint Protection client is installed and has the latest software update definitions for antimalware protection.  

    -   The interactive presentation software is installed and runs automatically, ready for visitors.  

14. After this initial setup, any restarts that might be required for updates occur only when the visitor center is closed.  
