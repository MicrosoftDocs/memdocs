---
title: "Maintenance tasks for System Center Configuration Manager"
ms.custom: na
ms.date: 2015-12-08
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: 
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 625bb787-6d16-47a0-8b0f-b129cd909ca3
caps.latest.revision: 7
caps.handback.revision: 0
author: Brenduns
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
# Maintenance tasks for System Center Configuration Manager
System Center Configuration Manager sites and hierarchies require regular maintenance and monitoring to provide services effectively and continuously. Regular maintenance ensures that the hardware, software, and the Configuration Manager database continue to function correctly and efficiently. Optimal performance greatly reduces the risk of failure.  
  
 To configure Alerts, and use the Status System to monitor the health of Configuration Manager, see [Use alerts and the status system for System Center Configuration Manager](../../../core/servers/manage/use-alerts-and-the-status-system.md).  
  
-   [Maintenance tasks](#bkmk_MTs)  
  
##  <a name="bkmk_MTs"></a> Maintenance tasks  
 Performing regular maintenance is important to ensure correct site operations. Maintain a maintenance log to document dates that maintenance was conducted, by whom, and any maintenance-related comments about the task conducted.  
  
### When to Perform Common Maintenance Tasks  
 To maintain your site, consider performing regular maintenance on a daily, weekly, and for some tasks, a more periodic schedule. Common maintenance can include both the built-in maintenance tasks and other tasks such as account maintenance to maintain compliance with your company policies.  
  
 Use the following information as a guide to help you plan when to perform different maintenance tasks. Use these lists as a starting point, and add any additional tasks you might require.  
  
 **Daily Tasks**   
The following are maintenance tasks you might consider performing on a daily basis:  
  
-   Verify that predefined maintenance tasks that are scheduled to run daily are running successfully  
  
-   Check the Configuration Manager database status  
  
-   Check site server status  
  
-   Check Configuration Manager site system inboxes for file backlogs  
  
-   Check site systems status  
  
-   Check the operating system event logs on site systems  
  
-   Check the SQL Server error log on the site database computer  
  
-   Check system performance  
  
-   Check Configuration Manager alerts  
  
 **Weekly Tasks**   
The following are maintenance tasks you might consider performing on a weekly basis:  
  
-   Verify that predefined maintenance tasks scheduled to run weekly are running successfully.  
  
-   Delete unnecessary files from site systems  
  
-   Produce and distribute end-user reports if required  
  
-   Back up application, security, and system event logs and clear them  
  
-   Check the site database size and verify that there is enough available disk space on the site database server so that the site database can grow  
  
-   Perform SQL Server database maintenance on the site database according to your SQL Server maintenance plan  
  
-   Check available disk space on all site systems  
  
-   Run disk defragmentation tools on all site systems  
  
 **Periodic Tasks**   
Some tasks do not have to be performed during daily or weekly maintenance, but are important to ensure overall site health, and security and disaster recovery plans are up-to-date. The following are maintenance tasks that you might consider performing on a more periodic basis than the daily or weekly tasks:  
  
-   Change accounts and passwords, if it is necessary, according to your security plan  
  
-   Review the maintenance plan to verify that scheduled maintenance tasks are scheduled correctly and effectively depending on configured site settings  
  
-   Review the Configuration Manager hierarchy design for any required changes  
  
-   Check network performance to ensure changes have not been made that affect site operations  
  
-   Verify that Active Directory settings affecting site operations have not changed. For example, verify that subnets assigned to Active Directory sites that are used as boundaries for Configuration Manager site have not changed  
  
-   Review your disaster recovery plan for any required changes  
  
-   Perform a site recovery according to the disaster recovery plan in a test lab by using a backup copy of the most recent backup created by the Backup Site Server maintenance task  
  
-   Check hardware for any errors or for available hardware updates  
  
-   Check the overall health of the site  
  
###  <a name="BKMK_UseMTs"></a> Maintain the operational health of your site database  
 While your Configuration Manager site and hierarchy perform the tasks that you schedule and configure, site components continually add data to the Configuration Manager database. As the amount of data grows, database performance and the free storage space in the database decline. You can configure site maintenance tasks to remove aged data that you no longer require.  
  
 Configuration Manager provides predefined maintenance tasks that you can use to maintain the health of the Configuration Manager database. Not all maintenance tasks are available at each site, by default, several are enabled while some are not, and all support a schedule that you can configure for when to run.  
  
 Most maintenance tasks periodically remove out-of-date data from the Configuration Manager database. Reducing the size of the database by removing unnecessary data improves the performance and the integrity of the database, which increases the efficiency of the site and hierarchy. Other tasks, such as **Rebuild Indexes**, help maintain the database efficiency, while some, such as the **Backup Site Server** task, help you prepare for disaster recovery.  
  
> [!IMPORTANT]  
>  When you plan the schedule of any task that deletes data, consider the use of that data across the hierarchy. When a task that deletes data runs at a site, the information is removed from the Configuration Manager database, and this change replicates to all sites in the hierarchy. This can affect other tasks that rely on that data. For example, at the central administration site, you might configure Discovery to run one time per month to identify non-client computers, and plan to install the Configuration Manager client to these computers within two weeks of their discovery. However, at one site in the hierarchy, an administrator configures the Delete Aged Discovery Data task to run every seven days with a result that seven days after non-client computers are discovered, they are deleted from the Configuration Manager database. Back at the central administration site, you prepare to push install the Configuration Manager client to these new computers on day 10. However, because the Delete Aged Discovery Data task has recently run and deleted data that is seven days or older, the recently discovered computers are no longer available in the database.  
  
 After you install a Configuration Manager site, review the available maintenance tasks and enable those tasks that your operations require. Review the default schedule of each task, and when necessary, modify the schedule to fine-tune the maintenance task to fit your hierarchy and environment. Although the default schedule of each task should suit most environments, monitor the performance of your sites and database and expect to fine-tune tasks to increase your deployments’ efficiency. Plan to periodically review the site and database performance and to reconfigure maintenance tasks and their schedules to maintain that efficiency.  
  
#### Configure Maintenance Tasks  
 Each Configuration Manager site supports maintenance tasks that help maintain the operational efficiency of the site database. By default, several maintenance tasks are enabled in each site, and all tasks support independent schedules. Maintenance tasks are configured individually for each site and apply to the database at that site; however, some tasks, such as **Delete Aged Discovery Data**, affect the information available in all sites in a hierarchy.  
  
 Only the maintenance tasks that you can configure at a site are displayed in the Configuration Manager console. For a complete list of maintenance tasks by site type, see [Reference for maintenance tasks for System Center Configuration Manager](../../../core/servers/manage/reference-for-maintenance-tasks.md)  
  
 Use the following procedure to help you configure the common settings of maintenance tasks.  
  
###### To configure maintenance tasks for Configuration Manager  
  
1.  In the Configuration Manager console navigate to **Administration** > **Site Configuration** >**Sites**.  
  
2.  Select the site that contains the maintenance task that you want to configure.  
  
3.  On the **Home** tab, in the **Settings** group, click **Site Maintenance**, and then select the maintenance task you want to configure.  
  
    > [!TIP]  
    >  Only the tasks available at the selected site are displayed.  
  
4.  To configure the task, click **Edit**, ensure the **Enable this task** check box is selected, and configure a schedule for when the task runs. If the task also deletes aged data, configure the age of data that will be deleted from the database when the task runs. Click **OK** to close the task **Properties**.  
  
    > [!NOTE]  
    >  For **Delete Aged Status Messages**, you configure the age of data to delete when you configure status filter rules.  
  
5.  To enable or disable the task without editing the task properties, click the **Enable** or **Disable** button. The button label changes depending on the current configuration of the task.  
  
6.  When you are finished configuring the maintenance tasks, click **OK** to complete the procedure.