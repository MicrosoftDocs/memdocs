---
title: Example scenario - deploy Windows Embedded clients
titleSuffix: Configuration Manager
description: See an example scenario for deploying and managing Configuration Manager clients on Windows Embedded devices.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
author: sheetg09
ms.author: sheetg
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# Example scenario for deploying and managing Configuration Manager clients on Windows Embedded devices

*Applies to: Configuration Manager (current branch)*

This scenario demonstrates how you can manage write-filter-enabled Windows Embedded devices with Configuration Manager.If your embedded devices do not support write filters, they behave as standard Configuration Manager clients and these procedures don't apply.  

Coho Vineyard & Winery is opening a visitor center and needs kiosks that run Windows Embedded to run interactive presentations. The building for the new visitor center is not close to the IT department, so the kiosks must be managed remotely. In addition to the software that runs the presentations, these devices must run up-to-date antimalware protection software to comply with the company security policies. The kiosks must run 7 days a week, with no downtime while the visitor center is open.  

 Coho already runs Configuration Manager to manage devices on their network. Configuration Manager is configured to run Endpoint Protection, and install software updates and applications. However, because the IT team has not managed Windows Embedded devices before, the Configuration Manager administrator runs a pilot to manage two kiosks in the reception lobby.   

 To manage these Windows Embedded devices that are write-filter-enabled, Configuration Manager administrator performs the following steps to install the Configuration Manager client, protect the client by using Endpoint Protection, and install the interactive presentation software.  

1. The Configuration Manager administrator (the Admin) reads how Windows Embedded devices uses write filters and how Configuration Manager can make this easier by automatically disabling and then re-enabling the writer filters to persist a software installation.  

    For more information, see [Planning for client deployment to Windows Embedded devices](../../../core/clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md).  

2. Before the Admin installs the Configuration Manager client, the Admin creates a new query-based device collection for the Windows Embedded devices. Because the company uses standard naming formats to identify their computers, the Admin can uniquely identify Windows Embedded devices by the first six letters of the computer name: **WEMDVC**. The Admin uses the following WQL query to create this collection: **select SMS_R_System.NetbiosName from SMS_R_System where SMS_R_System.NetbiosName like "WEMDVC%"**  

    This collection allows the Admin to manage the Windows Embedded devices with different configuration options from the other devices. The Admin will use this collection to control restarts, deploy Endpoint Protection with client settings, and deploy the interactive presentation application.  

    See [How to create collections](../../../core/clients/manage/collections/create-collections.md).  

3. The Admin configures the collection for a maintenance window to ensure that restarts that might be required for installing the presentation application and any upgrades do not occur during opening hours for the visitor center. Opening hours will be 09:00 through 18:00, Monday through Sunday. The Admin configures the maintenance window for every day, 18:30 through 06:00.  

4. For more information, see [How to use maintenance windows](../../../core/clients/manage/collections/use-maintenance-windows.md).  

5. The Admin then configures a custom device client setting to install the Endpoint Protection client by selecting **Yes** for the following settings, and then deploys this custom client setting to the Windows Embedded device collection:  

   - **Install Endpoint Protection client on client computers**  

   - **For Windows Embedded devices with write filters, commit Endpoint Protection client installation (requires restart)**  

   - **Allow Endpoint Protection client installation and restart to be performed outside maintenance windows**  

     When the Configuration Manager client is installed, these settings install the Endpoint Protection client and ensure that it is persisted in the operating system as part of the installation, rather than written to the overlay only. The company security policies require that the antimalware software is always installed and the Admin does not want to run the risk of the kiosks being unprotected for even a short period of time if they restart.  

   > [!NOTE]  
   >  The restarts that are required to install the Endpoint Protection client are a one-time occurrence, which happen during the setup period for the devices and before the visitor center is operational. Unlike the periodic deployment of applications or software definition updates, the next time the Endpoint Protection client is installed on the same device will probably be when the company upgrades to the next version of Configuration Manager.  

    For more information, see [Configuring Endpoint Protection](../../../protect/deploy-use/endpoint-protection-configure.md).  

6. With the configuration settings for the client now in place, the Admin prepares to install the Configuration Manager clients. Before the Admin can install the clients, they must manually disable the write filter on the Windows Embedded devices. The Admin reads the OEM documentation that accompanies the kiosks and follows their instructions to disable the write filters.  

    The Admin renames the device so it uses the company standard naming format, and then installs the client manually by running CCMSetup with the following command from a mapped drive that holds the client source files: **CCMSetup.exe /MP:mpserver.cohovineyardandwinery.com SMSSITECODE=CO1**  

    This command installs the client, assigns the client to the management point that has the intranet FQDN of **mpserver.cohovineyardandwinery.com**, and assigns the client to the primary site named **CO1**.  

    The Admin knows that it always takes a while for clients to install and send back their status to the site. So the Admin waits before they confirm that the clients successfully install, assign to the site, and appear as clients in the collection that they created for Windows Embedded devices.  

    As additional confirmation, the Admin checks the properties of Configuration Manager in Control Panel on the devices and compares them to standard Windows computers that are managed by the site. For example, on the **Components** tab, the **Hardware Inventory Agent** displays **Enabled**, and on the **Actions** tab, there are 11 available actions, which include **Application Deployment Evaluation Cycle** and **Discovery Data Collection Cycle**.  

    Confident that the clients are successfully installed, assigned, and receiving client policy from the management point, the Admin then manually enables the write filters by following the instructions from the OEM.  

    For more information, see:  

   -   [How to deploy clients to Windows computers](../../../core/clients/deploy/deploy-clients-to-windows-computers.md)  

   -   [How to assign clients to a site](../../../core/clients/deploy/assign-clients-to-a-site.md)  

7. Now that the Configuration Manager client is installed on the Windows Embedded devices, the Admin confirms that they can manage them in the same way as they manage the standard Windows clients. For example, from the Configuration Manager console, the Admin can remotely manage them by using remote control, initiate client policy for them, and view client properties and hardware inventory.  

    Because these devices are joined to an Active Directory domain, the Admin does not have to manually approve them as trusted clients and confirms from the Configuration Manager console that they are approved.  

    For more information, see [How to manage clients](../../../core/clients/manage/manage-clients.md).  

8. To install the interactive presentation software, the Admin runs the **Deploy Software Wizard** and configures a required application. On the **User Experience** page of the wizard, in the **Write filter handling for Windows Embedded devices** section, they accept the default option that selects **Commit changes at deadline or during a maintenance window (requires restarts)**.  

    The Admin keeps this default option for write filters to ensure that the application persists after a restart, so that it is always available to the visitors using the kiosks. The daily maintenance window provides a safe period during which the restarts for installation and any updates can occur.  

    The Admin deploys the application to the Windows Embedded devices collection.  

    For more information, see [How to deploy applications with Configuration Manager](../../../apps/deploy-use/deploy-applications.md).  

9. To configure definition updates for Endpoint Protection, the Admin uses software updates and runs the Create Automatic Deployment Rule Wizard. They select the **Definition Updates** template to prepopulate the wizard with settings that are appropriate for Endpoint Protection.  

     These settings include the following on the **User Experience** page of the wizard:  

   - **Deadline behavior**: The **Software Installation** check box is not selected.  

   - **Write filter handling for Windows Embedded devices**: The **Commit changes at deadline or during a maintenance window (requires restarts)** check box is not selected.  

     The Admin keeps these default settings. Together, these two options with this configuration allow any software update definitions for Endpoint Protection to be installed in the overlay during the day and not wait to be installed and committed during the maintenance window. This configuration best meets the company security policy for computers to run up-to-date antimalware protection.  

     > [!NOTE]  
     >  Unlike software installations for applications, software update definitions for Endpoint Protection can occur very frequently, even multiple times a day. They are often small files. For these types of security-related deployments, it can often be beneficial to always install to the overlay rather than wait until the maintenance window. The Configuration Manager client will quickly re-install the software definition updates if the device restarts because this action initiates an evaluation check and does not wait until the next scheduled evaluation.  

     The Admin selects the Windows Embedded devices collection for the automatic deployment rule.  

     For more information, see  
               Step 3: Configure Configuration Manager Software Updates to Deliver Definition Updates to Client Computers in [Configuring Endpoint Protection](../../../protect/deploy-use/endpoint-protection-configure.md)  

10. The Admin decides to configure a maintenance task that periodically commits all changes on the overlay. This task is to support the software update definitions deployment, to reduce the number of updates that accumulate and must be installed again, each time the device restarts. In the Admin's experience, this helps the antimalware programs run more efficiently.  

    > [!NOTE]  
    >  These software update definitions would be automatically committed to the image if the embedded devices ran another management task that supported committing the changes. For example, installing a new version of the interactive presentation software would also commit the changes for software update definitions. Or, installing standard software updates every month that install during the maintenance window could also commit the changes for software update definitions. However, in this scenario, where standard software updates do not run and the interactive presentation software is unlikely to be updated very often, it might be months before the software definition updates are automatically committed to the image.  

     The Admin first creates a custom task sequence that has no settings other than the name. They run the Create Task Sequence Wizard:  

    1. On the **Create a New Task Sequence** page, the Admin selects **Create a new custom task sequence**, and then clicks **Next**.  

    2. On the **Task Sequence Information** page, the Admin enters **Maintenance task to commit changes on embedded devices** for the task sequence name, and then clicks **Next**.  

    3. On the **Summary** page, the Admin selects **Next**, and completes the wizard.  

       The Admin then deploys this custom task sequence to the Windows Embedded devices collection, and configures the schedule to run every month. As part of the deployment settings, they select the **Commit changes at deadline or during a maintenance window (requires restarts)** check box to persist the changes after a restart. To configure this deployment, the Admin selects the custom task sequence that they just created, and then on the **Home** tab, in the **Deployment** group, they click **Deploy** to start the Deploy Software Wizard:  

    4. On the **General** page, the Admin selects the Windows Embedded devices collection, and then clicks **Next**.  

    5. On the **Deployment Settings** page, the Admin selects the **Purpose** of **Required**, and then clicks **Next**.  

    6. On the **Scheduling** page, the Admin clicks **New** to specify a weekly schedule during the maintenance window, and then clicks **Next**.  

    7. The Admin completes the wizard without any further changes.  

       For more information, see  
                 [Manage task sequences to automate tasks](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md).  

11. For the kiosks to run automatically, the Admin writes a script to configure the devices for the following settings:  

    - Automatically log on, using a guest account that has no password.  

    - Automatically run the interactive presentation software on startup.  

      The Admin uses packages and programs to deploy this script to the Windows Embedded devices collection. When the Admin runs the Deploy Software Wizard, they again select the **Commit changes at deadline or during a maintenance window (requires restarts)** check box to persist the changes after a restart.  

      For more information, see [Packages and programs](../../../apps/deploy-use/packages-and-programs.md).  

12. The following morning, the Admin checks the Windows Embedded devices. They confirm the following:  

    - The kiosk is automatically logged on by using the guest account.  

    - The interactive presentation software is running.  

    - The Endpoint Protection client is installed and has the latest software update definitions.  

    - That the device restarted during the maintenance window.  

      For more information, see:  

    - [How to monitor Endpoint Protection](../../../protect/deploy-use/monitor-endpoint-protection.md)  

    - [Monitor applications with Configuration Manager](../../../apps/deploy-use/monitor-applications-from-the-console.md)  

13. The Admin monitors the kiosks and reports the successful management of them to their manager. As a result, 20 kiosks are ordered for the visitor center.  

     To avoid the manual installation of the Configuration Manager client, which requires manually disabling and then enabling the write filters, the Admin ensures that the order includes a customized image that already includes the installation and site assignment of the Configuration Manager client. In addition, the devices are named according to the company naming format.  

     The kiosks are delivered to the visitor center a week before it opens. During this time, the kiosks are connected to the network, all device management for them is automatic, and no local administrator is required. The Admin confirms that the kiosks are functioning as required:  

    -   The clients on the kiosks complete site assignment and download the trusted root key from Active Directory Domain Services.  

    -   The clients on the kiosks are automatically added to the Windows Embedded devices collection and configured with the maintenance window.  

    -   The Endpoint Protection client is installed and has the latest software update definitions for antimalware protection.  

    -   The interactive presentation software is installed and runs automatically, ready for visitors.  

14. After this initial setup, any restarts that might be required for updates occur only when the visitor center is closed.  
