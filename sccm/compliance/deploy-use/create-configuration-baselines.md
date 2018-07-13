---
title: "Create configuration baselines"
titleSuffix: "Configuration Manager"
description: "Create configuration baselines in System Center Configuration Manager that you can deploy to a collection."
ms.date: 07/13/2018
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 678c9622-c61b-47d1-ba25-690616e431c7
author: aczechowski
manager: dougeby
ms.author: aaroncz
---
# Create configuration baselines in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*


Configuration baselines in System Center Configuration Manager contain predefined configuration items and optionally, other configuration baselines. After a configuration baseline is created, you can deploy it to a collection so that devices in that collection download the configuration baseline and assess their compliance with it.  

 Configuration baselines in Configuration Manager can contain specific revisions of configuration items or can be configured to always use the latest version of a configuration item. For more information about configuration item revisions, see [Management tasks for configuration data](../../compliance/deploy-use/management-tasks-for-configuration-data.md).  

 There are two methods that you can use to create configuration baselines:  

-   Import configuration data from a file. To start the **Import Configuration Data Wizard**, in the **Configuration Items** or **Configuration Baselines** node in the **Assets and Compliance** workspace, click **Import Configuration Data**.  

-   Use the **Create Configuration Baseline** dialog box to create a new configuration baseline.  

To create a configuration baseline by using the **Create Configuration Baseline** dialog box, use the following procedure:  

1.  In the Configuration Manager console, click **Assets and Compliance** > **Compliance Settings** > **Configuration Baselines**.  

2.  On the **Home** tab, in the **Create** group, click **Create Configuration Baseline**.  

3.  In the **Create Configuration Baseline** dialog box, enter a unique name and a description for the configuration baseline. You can use a maximum of 255 characters for the name and 512 characters for the description.  

4.  The **Configuration data** list displays all configuration items or configuration baselines that are included in this configuration baseline. Click **Add** to add a new configuration item or configuration baseline to the list. You can choose from the following items:  

    -   **Configuration Items**  

    -   **Software Updates**  

    -   **Configuration Baselines**  
      > [!IMPORTANT]
      > You must limit each configuration baseline to no more than 1000 software updates.
5.  Use the **Change Purpose** list to specify the behavior of a configuration item that you've selected in the **Configuration data** list. You can select from the following items:  

    -   **Required**: The configuration baseline is evaluated as noncompliant if the configuration item isn't detected on a client device. If it's detected, it's evaluated for compliance  

    -   **Optional**: The configuration item is only evaluated for compliance if the application it references is found on client computers. If the application is not found, the configuration baseline isn't marked as noncompliant (only applicable to application configuration items).  

    -   **Prohibited**: The configuration baseline is evaluated as noncompliant if the configuration item is detected on client computers (only applicable to application configuration items).  

    > [!NOTE]
    >  The **Change Purpose** list is available only if you clicked the option **This configuration item contains application settings** on the **General** page of the **Create Configuration Item Wizard**.  

6.  Use the **Change Revision** list to select a specific or the latest revision of the configuration item to assess for compliance on client devices or select **Always Use Latest** to always use the latest revision. For more information about configuration item revisions, see [Management tasks for configuration data](../../compliance/deploy-use/management-tasks-for-configuration-data.md).  

7.  To remove a configuration item from the configuration baseline, select a configuration item, and then click **Remove**.  

8. Starting in version 1806, select if you want to **Always apply this baseline for co-managed clients**. When checked, this baseline will apply even on clients that are managed by Intune.  This exception might be used to configure settings that are required by your organization but not yet available in Intune. 

9. Optionally, click on **Categories** to assign categories to the baseline for searching and filtering. 

11. Click **OK** to close the **Create Configuration Baseline** dialog box and to create the configuration baseline.  
