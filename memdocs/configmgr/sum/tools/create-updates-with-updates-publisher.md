---
title: Create updates
titleSuffix: Configuration Manager
description: Create and bundle software updates with System Center Updates Publisher
ms.date: 04/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
author: mestew
ms.author: mstewart
manager: dougeby
ms.localizationpriority: medium
---
# Create  software updates and update bundles with Updates Publisher

*Applies to: System Center Updates Publisher*

With Updates Publisher you can use the  **Create Update** wizard to create your own updates and the **Create Bundle** wizard to create bundles of updates.

Because these two wizards have a similar workflow, the procedure to create an update bundle refers to the procedure for creating updates, with only the relevant differences detailed.

## Use the Create Update wizard
1. In the console go to **Updates Workspace**, and then in the **Getting Started** pane, choose **Update** from the **Home** tab of the ribbon. This opens the **Create Update** wizard.

2. On the **Package** page, use the following information to help you configure the update:

   -   Choose **Browse** to locate the software update package you will use as a package source. Valid sources include .MSI, .MSP, or .EXE files. Updates Publisher requires access to the file to create a file hash. The hash and file name are then used in the update metadata for the update that you are creating.
   

   -   Specify the source location of the content for this update. Normally this is the location where the update binary will be downloaded from during publishing to a WSUS server.  If the **Use a local source to publish software update content** option is selected, then the path is not required.

       Later, when the update is published to a WSUS server, Updates Publisher downloads the binaries for the update from the indicated source location.  If no path is provided then Update Publisher will search the [local source publishing path](updates-publisher-options.md#advanced) for the update binary.

   -   Specify the **Binary language** of the software update.

   -   Specify **Success return codes**, and **Success pending reboot codes** for the update. Separate multiple return codes by using a comma. You can use return codes to determine when update install was successful, and when reboots were required.

       -   Windows installer files and patches (.MSI and .MSP files) automatically set these values, and they cannot be modified.

       -   For .EXE updates, the default codes defined by the .EXE file are used if no return codes are specified.

   -   Specify any command-line arguments that are required to install the software update.

       -   Windows installer files and patches (.MSI and .MSP files) automatically set these values. For these file types the arguments must be specified as **\[name\]=\[value\]**. In addition, all options that start with a **/** (like **/qn**) are not supported for .MSI or .MSP software updates.

       -   For .EXE updates, all arguments are valid.

   >[!NOTE] 
   > You can use Updates Publisher to create only packages that are smaller than 2 GB. Import options are disabled if the software update package is too large.

3. On the **Information** page, specify details about the update that are included when the update is published or exported. Details include localized properties like the updates name (title) and description. Then, you specify more general details such as the classification, vendor, product, and where to learn more about the update.

    __Localized properties:__

   - **Language**: Select a language and then specify a title and description. You can then select additional languages, one at time, with each language supporting its own title and description.

   - **Title**: Enter the name of the update. This name displays in the Updates Workspace of the Updates Publisher console.

   - **Description**: A friendly description of the update. You might include what the update installs, and why or when it should be used.

   **Classification:** The following are common descriptions for the different classifications.

   - **Update**: An update to an application or file that is currently installed.

   - **Critical**: A broadly released update for a specific problem that addresses a critical bug that is not related to security.

   - **Feature Pack**: New product features that are distributed outside of a product release and are typically included in the next full product release.

   - **Security**: A broadly released update for a product-specific issue that is related to security.

   - **Update Rollup**: A cumulative set of hotfixes that are packaged together for easy deployment. These hotfixes can include security updates, critical updates, updates, and so on. An update rollup generally addresses a specific area, such as security or a product feature.

   - **Service Pack**: A cumulative set of hotfixes that are applied to an application. These hotfixes can include security updates, critical updates, software updates, and so on.

   - **Tool**: Specifies a tool or feature that helps complete one or more tasks.

   - **Driver**: An update for driver software.

   **Vendor:** Specify a vendor for the update. You can use the dropdown list to use values from updates that are in the repository. When you specify a vendor, the wizard creates a folder with that vendor name under **All Software Updates** in the **Updates Workspace** if that folder does not already exist. The following are Windows Server Update Services (WSUS) reserved names that cannot be entered for updates you create:
   - Microsoft Corporation
   - Microsoft
   - Update
   - Software Update
   - Tools
   - Tool
   - Critical
   - Critical Updates
   - Security
   - Security Updates
   - Feature Pack
   - Update Rollup
   - Service Pack
   - Driver
   - Driver Update
   - Bundle
   - Bundle Update

   **Product**: Specify the type of product that the update is for. You can use the dropdown list to use values from updates that are in the repository. The same list of WSUS reserved names that cannot be used for **Vendor**, cannot be used for **Product**.

   **More info URL**: Specify the URL where you can find more information about this update. You must use lowercase letters for **https** or **http** when you enter this URL.

4. On the **Optional Info** page, you can configure details that provide additional information about the update.

   -   **Bulletin ID**: Bulletin IDs are usually, but not always, provided by update vendors.

   -   **Article ID**: If a software update article is available, the Article ID can be useful to individuals seeking additional information about the update.

   -   **CVE IDs:** List one or more Common Vulnerabilities and Exposures (CVE) identifiers that provide security information about the update or update bundle. When listing more than one, use a semicolon to separate the CVEs as in this example: *CVE1;CVE2.*

   -   **Support URL:** List the URL that contains support information for this update, if available. You must use lowercase letters for **https** or **http** when you enter this URL.

   -   **Severity:** Set the severity level for this update.

   -   **Impact:** The following options can be used to specify impact:
       -   **Normal –** Use this to indicate the update requires typical installation procedures.
       -   **Minor –** Use this to indicate the update requires minimal installation procedures.
       -   **Requires exclusive handling –** Use this to indicate the update must be installed by itself, exclusive from any other updates.   <br /><br />

   -   **Restart Behavior:** Use this to provide information about the updates restart behavior. This setting does not affect the actual behavior of the update install.

       -   **Never reboots**: The computer never performs a system restart after installing the software update.
       -   **Always requires reboot**: The computer always performs a system restart after installing the software update.
       -   **Can request reboot**: After installing the software update, the computer requests a system restart only if a restart is necessary. The user has the option to postpone the restart. This is the default value. <br /><br />

5. On the **Prerequisite** page, specify the prerequisites that must be installed on a computer before this update can install. Prerequisites can be **detectoids** or other updates. Detectoids are high-level rules like one that requires the computers CPU to be a 64-bit processor. Detectoids can also specify specific updates that must be installed before this update can install.

   -   For better performance, use detectoids instead of creating *installable* and *installed rules* that perform the same check or action.

   Use the search option for **Available software updates and detectoids** to help you find specific updates or detectoids. For example, search on **CPU** to find the detectoids that let you limit installation based on specific CPU architecture.

   You can select one or more items at a time to add as a prerequisite. When adding prerequisites, the selected detectoids are added as one or more groups. To qualify for installation, a computer must meet the requirement of at least one member of each group that you configure:

   -   When you click **Add Prerequisite,** all items you have selected are added to separate, individual, groups. To qualify for this update, a computer must meet the prerequisite in this group and pass requirements for any additional groups that are configured.

   -   When you click **Add Group,** all items you have selected are added to a single group. To qualify for this update, a computer must meet at least one of the prerequisites in this group and pass requirements for any additional groups that are configured.

6. On the **Supersedence** page, specify the updates that are replaced (superseded) by this update. When this update is published, Configuration Manager will mark each update that is superseded as **Expired**. Clients will then install this update instead of the superseded updates.

7. On the **Applicability** page use the **Rule Editor** to define a set of rules that determine whether a device needs this update. (This page is similar to the **Installed** page, that follows it.)

   To add a new rule, click on ![New Rule](media/newrule.png). This opens the Applicability Rule page where you can configure rules.

   Types of rules you can create include:

   -   **File** – Use this rule to require that a device have a file with properties that meet one or more criteria you specify before this update can be applied.

   -   **Registry –** Use this type to specify registry details that must be present before a device qualifies to install this update.

   -   **System –** This rule uses system details to determine applicability. You can choose between defining a Windows version, a Windows language, processor architecture, or specify a WMI query to identify the devices operating system.

   -   **Windows Installer –** Use this rule type to determine applicability based on an installed .MSI or Windows Installer patch (.MSP). You can also determine if specific components or features are installed as part of the requirement.

       > [!IMPORTANT]  
       > On managed devices, the Windows Update Agent cannot detect Windows Install packages that are installed per-user. When you use this rule type, configure additional applicability rules, like file versions or registry key values, so that the Windows Installer package can be properly detected regardless of a per-user or per-system basis.

   -   **Saved rule –** This option lets you find and use rules you *created in the Rules Workspace*.

       After you create a rule, you can use the other icons to modify the rule, and if there are multiple rules, to define relationships between those rules.

   When you are done creating and adding rules, click **OK** in the **Create Rule Set** dialog box to save that set. You can then create a **New** rule and add that to the set as well.

   When you have multiple rules or rule sets to add to an update, you can use the logical operators in the **Rule Editor** to determine conditions between the rules, and in which order they process.

8. On the **Installed** page use the **Rule Editor to** define a set of rules that determine whether a device has already installed the update you are configuring. (This page is similar to the **Applicability** page, that proceeds this page.)

   This page of the wizard supports configuring rules with the same options and criteria as the **Applicability** page.

   When the wizard completes, the new update is added to a node in the **Updates Workspace** that is identified by the **Vendor** and **Product** name you used for that update.

## Use the Create Bundle wizard
Because this wizard uses the same workflow as the [Create Update wizard](#use-the-create-update-wizard), use that workflow, but note the following difference for bundles:

1.  To start the wizard, in the console go to **Updates Workspace**, and then select **Bundle** from the **Home** tab of the ribbon.

2.  Unlike the Create Update wizard, there is no Package page when creating a bundle.

3.  On the **Information** page, specify details about the update bundle that are included when the update is published, or exported.

4.  On the **Optional Info** page, you can configure details that provide additional information about the update bundle. The available options are the same as for creating an update. However, options for Impact and Restart Behavior are not available as they do not apply to bundles.

5.  On the **Prerequisite** page, specify the prerequisites that must be installed on a computer before this bundle can install. These rules are the same as seen for individual updates.

6.  On the **Supersedence** page, specify the updates that are replaced (superseded) by this update bundle. These rules are the same as seen for individual updates.

7.  On the **Members** page, you select updates to add to the update bundle. Only updates you have created or imported to Updates Publisher are available.

When the wizard completes, the new update bundle is added to a node in the **Updates Workspace** that is identified by the **Vendor** name you used for the update bundle.
