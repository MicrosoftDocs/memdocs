---
title: "Create and apply power plans"
titleSuffix: "Configuration Manager"
description: "Create and apply power plans in System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 738eddaa-52e2-467f-b453-821ef2884d47
caps.latest.revision: 6
caps.handback.revision: 0
author: arob98ms.author: angrobemanager: angrobe

---
# How to create and apply power plans in System Center Configuration Manager*Applies to: System Center Configuration Manager (Current Branch)*
Power management in System Center Configuration Manager enables you to apply power plans that are supplied with Configuration Manager to collections of computers in your hierarchy, or to create your own custom power plans. Use the procedure in this topic to apply a built-in or custom power plan to computers.  

> [!IMPORTANT]  
>  You can only apply Configuration Manager power plans to device collections.  

 If a computer is a member of multiple collections, each applying different power plans, then the following actions will be taken:  

-   Power plan: If multiple values for power settings are applied to a computer, the least restrictive value is used.  

-   Wakeup time: If multiple wakeup times are applied to a desktop computer, the time closest to midnight is used.  

 Use the **Computers with Multiple Power Plans** report to display all computers that have multiple power plans applied to them. This can help you discover computers that have power conflicts. For more information about power management reports, see [How to monitor and plan for power management in System Center Configuration Manager](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md).  

> [!IMPORTANT]  
>  Power settings configured by using Windows Group Policy will override settings configured by Configuration Manager power management.  

 Use the following procedure to create and apply a Configuration Manager power plan.  

### To create and apply a power plan  

1.  In the Configuration Manager console, click **Assets and Compliance**.  

2.  In the **Assets and Compliance** workspace, click **Device Collections**.  

3.  In the **Device Collections** list, click the collection to which you want to apply power management settings and then, in the **Home** tab, in the **Properties** group, click **Properties**.  

4.  In the **Power Management** tab of the *<Collection Name\>***Properties** dialog box, select **Specify power management settings for this collection**.  

    > [!NOTE]  
    >  You can also click **Browse** and then copy the power management settings from a selected collection to the selected collection.  

5.  In the **Start** and **End** fields, specify the start and end time for peak (or business) hours.  

6.  Enable **Wakeup time (desktop computers)** to specify a time when a desktop computer will wake from sleep or wake from hibernate to install scheduled updates or software installations.  

    > [!IMPORTANT]  
    >  Power management uses the internal Windows wakeup time feature to wake computers from sleep or hibernate. Wakeup time settings are not applied to portable computers to prevent scenarios in which they might wake when not plugged in. The wake up time is randomized and computers will be woken over a one hour period from the specified wakeup time.  

7.  If you want to configure a custom power plan for peak (or business) hours, select **Customized Peak (ConfigMgr)** from the **Peak plan** drop-down list, and then click **Edit**. If you want to configure a power plan for non-peak (or nonbusiness) hours, select **Customized Non-Peak (ConfigMgr)** from the **Non-peak plan** drop-down list, and then click **Edit**.  

    > [!NOTE]  
    >  You can use the **Computer Activity** report to help you decide the schedules to use for peak and non-peak hours when you apply power plans to collections of computers. For more information, see [How to monitor and plan for power management in System Center Configuration Manager](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md).  

     You can also select from the built-in power plans, **Balanced (ConfigMgr)**, **High Performance (ConfigMgr)** and **Power Saver (ConfigMgr)**, and then click **View** to display the properties of each power plan.  

    > [!NOTE]  
    >  You cannot modify the built-in power plans.  

8.  In the *<power plan name\>***Properties** dialog box, configure the following settings:  

    -   **Name:** Specify a name for this power plan or use the supplied default value.  

    -   **Description:**  Specify a description for this power plan or use the supplied default value.  

    -   **Specify the properties for this power plan:** Configure the power plan properties. To disable a property, clear its check box. For information about the available settings, see [Available power management plan settings](#BKMK_Plans) in this topic.  

        > [!IMPORTANT]  
        >  Enabled settings are applied to computers when the power plan is applied. If you clear a power setting check box, the value on the client computer is not changed when the power plan is applied. Clearing a check box does not restore the power setting to its previous value before a power plan was applied.  

9. Click **OK** to close the *<power plan name\>***Properties** dialog box.  

10. Click **OK** to close the *<Collection Name\>***Settings** dialog box and to apply the power plan.  

##  <a name="BKMK_Plans"></a> Available power management plan settings  
 The following table lists the power management settings available in Configuration Manager. You can configure separate settings for when the computer is plugged in or running on battery power. Depending on the version of Windows you are using, some settings might not be configurable.  

> [!NOTE]  
>  Power settings that you do not configure will retain their current value on client computers.  

|Name|Description|  
|----------|-----------------|  
|**Turn off display after (minutes)**|Specifies the length of time, in minutes, that the computer must be inactive before the display is turned off. Specify a value of **0** if you do not want power management to turn off the display.|  
|**Sleep after (minutes)**|Specifies the length of time, in minutes, that the computer must be inactive before it enters sleep. Specify a value of **0** if you do not want power management to enter sleep on the computer.|  
|**Require a password on wakeup**|A **Yes** or **No** value specifies whether a password is required to unlock the computer when it enters wake from sleep.|  
|**Power button action**|Specifies the action that is taken when the computer’s power button is pressed. Specifies the action that occurs when the user closes the lid of a portable computer. Possible values **Do nothing**, **Sleep**, **Hibernate**, and **Shut down**.|  
|**Start menu power button**|Specifies the action that occurs when you press the computer’s **Start** menu power button. Specifies the action that occurs when the user closes the lid of a portable computer. Possible values **Sleep**, **Hibernate**, and **Shut down**.|  
|**Sleep button action**|Specifies the action that occurs when you press the computer’s **Sleep** button. Specifies the action that occurs when the user closes the lid of a portable computer. Possible values **Do nothing**, **Sleep**, **Hibernate**, and **Shut down**.|  
|**Lid close action**|Specifies the action that occurs when the user closes the lid of a portable computer. Possible values **Do nothing**, **Sleep**, **Hibernate**, and **Shut down**.|  
|**Turn off hard disk after (minutes)**|Specifies the length of time, in minutes, that the computer’s hard disk must be inactive before it is turned off. Specify a value of **0** if you do not want power management to turn off the computer’s hard disk.|  
|**Hibernate after (minutes)**|Specifies the length of time, in minutes, that the computer must be inactive before it enters hibernate. Specify a value of **0** if you do not want power management to enter hibernate on the computer.|  
|**Low battery action**|Specifies the action that occurs when the computer’s battery reaches the specified low battery notification level. Specifies the action that occurs when the user closes the lid of a portable computer. Possible values **Do nothing**, **Sleep**, **Hibernate**, and **Shut down**.|  
|**Critical battery action**|Specifies the action that is taken when the computer’s battery reaches the specified critical battery notification level. Specifies the action that occurs when the user closes the lid of a portable computer. Possible values include **Sleep**, **Hibernate**, and **Shut down**.|  
|**Allow hybrid sleep**|Selecting the **On** or **Off** value specifies whether Windows saves a hibernation file when entering sleep, which can be used to restore the computer's state in the event of power loss while it has entered sleep.<br /><br /> Hybrid sleep is designed for desktop computers and, by default, is not enabled on portable computers. On computers that are running Windows 7, enabling hybrid sleep disables the hibernate functionality.|  
|**Allow standby state when sleeping action**|Selecting the **On** or **Off** value enables the computer to be on standby, which still consumes some power, but enables the computer to wake faster. If this setting is set to **Off**, the computer can only hibernate or turn off.|  
|**Required idleness to sleep (%)**|Specifies the percentage of idle time on the computer processor time required for the computer to enter sleep. For computers running Windows 7, this value is always set to **0**.|  
|**Enable Windows wake up timer for desktop computers**|Selecting the **Enable** or **Disable** value can enable the built-in Windows timer to be used by power management to wake a desktop computer. When a desktop computer is woken by using the Windows wake up timer, it will remain awake for 10 minutes by default to allow time for the computer to install any updates or to receive policy.<br /><br /> Wakeup timers are not supported on portable computers to prevent scenarios in which they might wake when they are not plugged in.|  
