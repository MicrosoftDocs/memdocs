---
title: App Health Analyzer
titleSuffix: Configuration Manager
description: A how-to guide for assessing compatibility with the App Health Analyzer in Desktop Analytics.
ms.date: 12/03/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 2af150a4-0c18-4b40-8492-c04c5d154596
author: aczechowski
ms.author: aaroncz
manager: dougeby
robots: noindex,nofollow
---

# How to assess compatibility with App Health Analyzer

> [!Note]  
> This information relates to a preview service which may be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here.  

The App Health Analyzer toolkit for Desktop Analytics is built on core solutions & methodology which Microsoft has built to evaluate desktop apps for compatibility issues. It uses innovative techniques to focus your validation efforts for desktop apps including LOB's by providing risk rating along with remediations you can take. The toolkit includes the App Readiness report to help you assess app readiness for your windows upgrades. It also has great integration story with desktop analytics to help customers mitigate upgrade issues through actionable insights.

Download the toolkit from the [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=57276). Always download and use the most current version.

The tool performs static analysis of an application for compatibility insights which is already installed on a device instead of package analysis of an app installer. It doesn't require any user intervention to launch or run the app but instead assesses all installed applications from add/remove programs list from control panel on a device. 

This approach doesn't require a customer to maintain or generate app installer for apps which are legacy/LOB and are not actively managed anymore. The tool will assess the app in its installed state to identify compatibility issues. All apps are assessed for pre-defined compatibility rules aka "signals" which are common prevalent issues reported when enterprises go through an OS upgrade. The compatibility insights also have remediations or fixes which users can take to unblock apps with 
issues.

> [!Important]  
> The toolkit doesn't support features to repair or fix your apps. If you create an app readiness report, the report does provide insights & guidance wherever applicable, to help remediate your apps before upgrading.  

The download is an MSI file that you can use to install the AHA Toolkit on a user's computer. After it is installed, when you run the toolkit, a UI wizard guides you to the process of creating app readiness report. There are batch files in the package that can be run from the command line or used with scripts. This is useful if you need to collect readiness information from users throughout your enterprise in a more automated manner. For more information, see [Getting app risk assessment for multiple machines in an enterprise](). 



## Configure

This section guides through the configuration settings you need to do run the toolkit on a device or on multiple machines.

### Requirements and limitations for using the toolkit
Before installing and using the Toolkit, you should be aware of the following requirements:
- Windows 7 Service Pack 1 (SP1) or later  
- Microsoft .NET Framework 4.5.1 or later  
- Device(s) enrolled in Desktop Analytics service, related requirements are covered in the section below  

This topic explains how to configure a single machine or multiple machines across your organization to run or deploy the tool. Following steps must be followed for either scenario:

a. Make sure to install the latest compatibility and related updates.
<!--is this already in the DA prereqs? would you use this outside of DA?-->
If you don't already have these updates installed, you can download the applicable version from the Microsoft Update Catalog or deploy it using Windows Server Update Services (WSUS) or your software distribution solution, such as System Center Configuration Manager. These requirements are identical to one's you would need for onboarding to desktop analytics solution

| OS version | Updates | 
|------------|---------|
| Windows 10 | The latest cumulative updates must be installed on Windows 10 devices to make sure that the required compatibility updates are installed. You can find the latest cumulative update on the [Microsoft Update Catalog](https://catalog.update.microsoft.com/) |
| Windows 8.1 | [KB2976978](http://catalog.update.microsoft.com/v7/site/Search.aspx?q=KB2976978)<br>Performs diagnostics on the Windows 8.1 systems that participate in the Windows Customer Experience Improvement Program. These diagnostics help determine whether compatibility issues might be encountered when latest Windows operating system is installed. <br>For more information about this update, see [support article](https://support.microsoft.com/kb/2976978).<br>NOTE: KB2976978 is a critical update, so it should already be installed by your management tool. You should, however, verify that it was deployed. |
| Windows 7 SP1 | [KB2952664](http://catalog.update.microsoft.com/v7/site/Search.aspx?q=KB2952664)<br>Performs diagnostics on the Windows 7 SP1 systems that participate in the Windows Customer Experience Improvement Program. These diagnostics help determine whether compatibility issues might be encountered when the latest Windows operating system is installed.<br>For more information about this update, see [support article](https://support.microsoft.com/kb/2952664).<br>NOTE: KB2952664 is a critical update, so it should already be installed by your management tool. You should, however, verify that it was deployed.|

> [!Important]  
> All the cumulative updates mentioned above should be from July 18 update or later, as it is the min version required for running the toolkit. Also, restart devices after you install the compatibility updates for the first time.  


b. Set Telemetry levels/CommercialId via Policy Settings or Preference registry key settings
<!--is this already in the DA prereqs? would you use this outside of DA?-->

There are many policies that can be centrally managed to control AHA/desktop analytics configuration. These policies also have preference registry key equivalents. Policy settings override preference settings if both are set. These requirements are identical to one's needed for onboarding to desktop analytics solution.

These policies are under HKLM\SOFTWARE\Policies\Microsoft\Windows\DataCollection whereas preference registry keys are outlined in the table below:

| | | 
|-|-|
| Allow Telemetry (Windows 10) | Basic Telemetry: HKLM\Software\Microsoft\Windows\CurrentVersion\Policies\DataCollection\AllowTelemetry (Set AllowTelemetry = 1 or higher)<br>0: maps to Tel Setting Security<br>1: maps to Tel Setting Basic <br>2: maps to Tel Setting Enhanced <br>3: maps to Tel Setting Full | 
| CommercialDataOptIn (Windows 7 and 8.1) | HKLM\Software\Microsoft\Windows\CurrentVersion\Policies\DataCollection\CommercialDataOptIn<br>Set CommercialDataOptIn= 1, It is required for AHA or Desktop Analytics. |
| CommercialId (For all machines on Windows 7/8.1/10) | HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection\CommercialId<br>For your device(s) to show up in analytics, they must be configured with your organization unique Commercial ID. We strongly recommend using the existing CommercialId if you are a current desktop analytics user. |


> [!Tip]  
> You can use the registry entry files from the setup folder in the package, just execute them and it will set the required regkeys. However, you need to set the CommercialId manually.  

You can also set these values by using Group Policy (in Computer Configuration > Administrative Templates > Windows Components > Data Collection and Preview Builds) or by using Mobile Device Management (in Provider/ProviderID/CommercialID). This can be done via pushing a group policy on those specific machines through ConfigMgr or other software deployment system. 

For reference again, the corresponding preference registry values are available in HKLM\Software\Microsoft\Windows\CurrentVersion\Policies\DataCollection and can be configured by the deployment script. If a given setting is configured by both preference registry settings and policy, the policy values will override.

For more information, see the following articles:
- [Configure Windows diagnostic data in your organization](https://docs.microsoft.com/windows/configuration/configure-windows-diagnostic-data-in-your-organization)  
- [Windows 7, Windows 8, and Windows 8.1 Appraiser Telemetry Events, and Fields](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-8.1-and-8/appraiser-diagnostic-data-events-and-fields)  
- [Windows 10, version 1703 basic level Windows diagnostic events and fields](https://docs.microsoft.com/windows/configuration/basic-level-windows-diagnostic-events-and-fields-1703)  
- [Windows 10, version 1709 enhanced diagnostic data events and fields used by Windows Analytics](https://docs.microsoft.com/windows/configuration/enhanced-diagnostic-data-windows-analytics-events-and-fields)  


> [!Important]  
> If the device(s) are enrolled on desktop service and configurated appropriately by using the deployment script, then you should face no issues running or deploying the toolkit and the data should flow into your OMS workspace. We have found that our Desktop Analytics customers have faced issues with data sharing due to proxy server issues for outbound traffic. So if you are a non-desktop Analytics customer some best practices on overcoming proxy server issues are documented on Enrolling devices in Windows Analytics



## Generate an app readiness report 

Learn how to interpret various insights and how to leverage them for your readiness assessments.

1. Copy the AHA msi installer on your machine. The script will install the .NET 4.5.1 version by default if it's not found on the machine as it is a pre-requisite to run AHA.  

2. Select the appropriate OS architecture (32 or 64 bit) and run the installer. Accept the license agreement to finish the installation.  

3. Toolkit by default gets installed on C:\Program Files\Microsoft Corporation\Microsoft App Health Analyzer  

4. Click the App Health Analyzer icon from the start menu, accept the permissions to run the tool in elevated mode, you may see error dialogs if any of the required telemetry settings are not set, refer to the configuration section if you missed any steps. You can always use the registry entry files to set them up quickly.  

5. The toolkit should be launched thereafter, a UI wizard will guide you through all the apps assessed.  

6. Here is preview of the UI experience, you can minimize the window to continue with your other tasks/applications while the toolkit runs in the background.

From the Stat menu, find **App Health Analyzer** in the **Microsoft App Health Analyzer** group.

{screenshot of tool}


### App readiness report features

1. **Get started** tab gives an overview of the signals supported in this current version along with possible remediations.  

2. **Insights** tab provides a view of all the apps assessed and various signals used for identifying compatibility issues along with risk assessment. These apps can be filtered by signals on the left menu.  

    - You can export these insights as a csv by using "Export CSV" Functionally.  

    - You can also rerun the tool by clicking the "Rescan Application" icon if you have installed any new applications.  

    - You can report the troubleshooting ID in left panel if you see no insights in the report even though the machines have installed apps.  

3. **Desktop Analytics** tab gives an overview of how App Health Analyzer can be leveraged to provide app readiness insights for apps across your enterprise.         



## Assess app risk on multiple machines

It's easy enough to install and run the AHA on a single user's computer to create an app readiness report. But what if you're an IT Pro for a large organization planning to upgrade to latest windows for a department or branch office? 

Along with the UI wizard version of the toolkit, you can also deploy AHA to run on a small set of representative devices (pilot) machines within your enterprise to get advanced app insights. If the users run the UI wizard version of the tool, your insights will be specific to your machine. The better alternative is to use the command line capabilities of the toolkit and use a script to run the toolkit to collect the information on behalf of the user. The diagnostic data is collected and sent to desktop analytics service automatically if the device(s) is already enrolled and pre-configured.

Here is the workflow on how you can leverage the toolkit with Desktop Analytics

{workflow diagram}


### Prerequisites before deployment 

All targeted machines should be configured for desktop analytics. Do verify that you have at least few successful runs and the data is showing up in your OMS workspace before doing a broader deployment. We recommend you deploy AHA package to pilot machines through Config Manager, install and run in silent mode. The package contains a separate batch file for non-UI mode "run_silent.cmd". This is useful if you need to collect readiness information from a subset of machines in your enterprise in a more automated manner.  Refer to some of the best practices from desktop analytics deployment guidance.

Key things to keep in mind:
- Make sure you deploy installer to all on your pilot ring, pre-upgrade before deploying Target OS. Run the toolkit at least once on a pilot group for a deployment plan to get effective readiness insights.
- Desktop Analytics has inbuilt functionality to recommend pilot groups for your deployment plans. It is recommended to run the toolkit on whole of this population set to get 100% coverage on your important windows apps. 
- Make sure in your schedule config manager task you run the silent mode from command line with admin privileges. By default, "run_silent.cmd" is located under:
C:\Program Files\Microsoft Corporation\Microsoft App Health Analyzer
- Schedule to run when the user is not logged in or using the machine. 
- Schedule the task to run every 30 days to get the latest readiness insights from your devices to help them stay current.   
- Here is preview of UI experience in desktop analytics for the insights you will get for your desktop apps including LOB's.

Readiness insights in desktop analytics

a. Contoso app has a detected driver dependency

{screenshot}

b. Contoso app has a highly adopted alternate version available

{screenshot}


## Troubleshooting

This topic covers the troubleshooting steps and most common operational issues you might encounter with configuring and using App Health Analyzer.
If you've followed the steps from the configuration document and are still encountering problems, following these additional steps might help:
1. Run the Upgrade Readiness Script in pilot mode to check if there are no pending issues with configuration.
    - Remember to edit the Runconfig.bat file, set CommercialIdValue = "Your unique commercial ID" if you are analytics customer.
    - Look for commercialIDValue in the script, by default it is set to  commercialIDValue=Unknown, change it as described above and save the script. Eg: "commercialIDValue= ab36a3c6-35e9-46ac-96d4-4b715ed5c024
    - Always run the script as Administrator.

2. If you find exit codes which resembles errors by running Upgrade Readiness Script, share the logs with us. Provide a storage location for log information. You can store log information on a remote file share or a local directory. If the script is blocked from creating the log file for the given path, it creates the log files in the drive with the Windows directory. Example: %SystemDrive%\UADiagnostics

3. If no issues were detected by the script and you are still facing issues with the toolkit, then issue can be with AHA toolkit. 

    - Initiate the tool in verbose mode. The batch file to run the tool in this mode is run_verbose.cmd or you can also run this mode from the start menu. To diagnose certain machine(s) the batch file 'run_verbose.cmd' can also be triggered from config manager console to collect the logs. By default, the file is located under: 'C:\Program Files\Microsoft Corporation\Microsoft App Health Analyzer\run_verbose.cmd'

    - This run will generate the logs which will help us troubleshoot the potential causes.

    - Logs will be saved under /LogCollection folder in the installed location, zip the file and send it our way. Default location for log collection is: 'C:\Program Files\Microsoft Corporation\Microsoft App Health Analyzer\LogCollection\'

    - Send the logs to AHASupport, we will follow up for further investigations.

Few common problems.
a. I don't see AHA welcome screen.
b. I don't see any insights in the app readiness report even though I have apps installed on my machine. Note: Include the troubleshooting ID from the UI with the event logs from step 3.
c. I ran the tool, but nothing happened. 

For all these scenarios, try troubleshooting with steps 1 & 2 first, if everything looks good, and you are still facing issues share AHA diagnostic logs outlined in step 3.

If you are completely blocked from running the tool and have no clue on how to proceed, share the logs following steps 2 & 3 with us. You can reach out to AHASupport, attach the logs, we will follow up within 1-2 business days.

If you have feedback or questions about the toolkit, please contact the [App Health Analyzer Team](mailto:ahacore@microsoft.com).

