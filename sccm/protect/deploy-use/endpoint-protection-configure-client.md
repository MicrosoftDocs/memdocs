---
title: Configure Endpoint Protection
titleSuffix: Configuration Manager
description: Learn how to configure custom client settings for Endpoint Protection.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: e63f2394-6eb1-4a33-bec5-8377fc62a34e
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Configure custom client settings for Endpoint Protection

*Applies to: System Center Configuration Manager (Current Branch)*

This procedure configures custom client settings for Endpoint Protection, which you can deploy to collections of devices in your hierarchy.

> [!IMPORTANT]  
>  Only configure the default Endpoint Protection client settings if you're sure that you want them applied to all computers in your hierarchy. 



## To enable Endpoint Protection and configure custom client settings

1. In the Configuration Manager console, click **Administration**.  

2. In the **Administration** workspace, click **Client Settings**.  

3. On the **Home** tab, in the **Create** group, click **Create Custom Client Device Settings**.  

4. In the **Create Custom Client Device Settings** dialog box, provide a name and a description for the group of settings, and then select **Endpoint Protection**.  

5. Configure the Endpoint Protection client settings that you require. For a full list of Endpoint Protection client settings that you can configure, see the Endpoint Protection section in [About client settings](/sccm/core/clients/deploy/about-client-settings#endpoint-protection).  

   > [!IMPORTANT]  
   >  Install the Endpoint Protection site system role before you configure client settings for Endpoint Protection.  

6. Click **OK** to close the **Create Custom Client Device Settings** dialog box. The new client settings are displayed in the **Client Settings** node of the **Administration** workspace.  

7. Next, deploy the custom client settings to a collection. Select the custom client settings you want to deploy. In the **Home** tab, in the **Client Settings** group, click **Deploy**.  

8. In the **Select Collection** dialog box, choose the collection to which you want to deploy the client settings and then click **OK**. The new deployment is shown in the **Deployments** tab of the details pane.  

Clients are configured with these settings when they next download client policy. For more information, see [Initiate policy retrieval for a Configuration Manager client](/sccm/core/clients/manage/manage-clients#BKMK_PolicyRetrieval).  



## How to provision the Endpoint Protection client in a disk image

Install the Endpoint Protection client on a computer that you intend to use as a disk image source for Configuration Manager OS deployment. This computer is typically called the reference computer. After you create the OS image, then use Configuration Manager OS deployment to deploy the image.

> [!Important]  
> Windows 10 and Windows Server 2016 have Windows Defender installed by default. You don't need this procedure on those versions of Windows.  

Use the following procedures to help you install and configure the Endpoint Protection client on a reference computer.


### Prerequisites

The following list contains the required prerequisites for installing the Endpoint Protection client software on a reference computer.

- You must have access to the Endpoint Protection client installation package, **scepinstall.exe**. Find this package in the **Client** folder of the Configuration Manager installation folder on the site server.  

- To deploy the Endpoint Protection client with your organization's required configuration, create and export an antimalware policy. Then specify this policy when you manually install the Endpoint Protection client. For more information, see [How to create and deploy antimalware policies](/sccm/protect/deploy-use/endpoint-antimalware-policies).  

  > [!NOTE]  
  >  You can't export the **Default Client Antimalware Policy**.  

- If you want to install the Endpoint Protection client with the latest definitions, download them from [Windows Defender Security Intelligence](https://www.microsoft.com/wdsi).  

> [!NOTE]  
> Starting in Configuration Manager 1802, you don't need to install the Endpoint Protection agent (SCEPInstall) on Windows 10 devices. If it's already installed on Windows 10 devices, Configuration Manager doesn't remove it. Administrators can remove the Endpoint Protection agent on Windows 10 devices that are running at least the 1802 client version. SCEPInstall.exe may still be present in C:\Windows\ccmsetup on some machines, but new client installations shouldn't download it. <!--503654-->


### How to install the Endpoint Protection client on the reference computer

Install the Endpoint Protection client locally on the reference computer from a command prompt. First get the installation file **scepinstall.exe**. For more information, see [Install the Endpoint Protection client from a command prompt](#bkmk_manual-install).

If necessary, also include a preconfigured antimalware policy or with an antimalware policy that you previously exported. 



## <a name="bkmk_manual-install"></a> To install the Endpoint Protection client from a command prompt

1. Copy **scepinstall.exe** from the **Client** folder of the Configuration Manager installation folder to the computer on which you want to install the Endpoint Protection client software.  

2. Open a command prompt as an administrator. Change directory to the folder with the installer. Then run `scepinstall.exe`, adding any additional command-line properties that you require:


   |  Property   |                                  Description                                   |
   |-------------|--------------------------------------------------------------------------------|
   |    `/s`     |                           Run the installer silently                           |
   |    `/q`     |                        Extract the setup files silently                        |
   |    `/i`     |                           Run the installer normally                           |
   |  `/policy`  | Specify an antimalware policy file to configure the client during installation |
   | `/sqmoptin` |     Opt-in to the Microsoft Customer Experience Improvement Program (CEIP)     |


3. Follow the on-screen instructions to complete the client installation.  

4. If you downloaded the latest update definition package, copy the package to the client computer, and then double-click the definition package to install it.  

   > [!NOTE]  
   >  After the Endpoint Protection client install completes, the client automatically performs a definition update check. If this update check succeeds, you don't have to manually install the latest definition update package.  

#### Example: install the client with an antimalware policy

`scepinstall.exe /policy <full path>\<policy file>`



## Verify the Endpoint Protection client installation

After you install the Endpoint Protection client on your reference computer, verify that the client is working correctly.

1.  On the reference computer, open **System Center Endpoint Protection** from the Windows notification area.  

2.  On the **Home** tab of the **System Center Endpoint Protection** dialog box, verify that **Real-time protection** is set to **On**.  

3.  Verify that **Up-to-date** is displayed for **Virus and spyware definitions**.  

4.  To make sure that your reference computer is ready for imaging, under **Scan options**, select **Full**, and then click **Scan now**.  



## Prepare the Endpoint Protection client for imaging

Perform the following steps to prepare the Endpoint Protection client for imaging:

1. On the reference computer, sign in as an administrator.  

2. Download and install **PsExec** from [Windows SysInternals](https://docs.microsoft.com/sysinternals/downloads/psexec).  

3. Run a command prompt as an administrator, change directory to the folder where you installed PsTools, and then type the following command:  

   `psexec.exe -s -i regedit.exe`  

   > [!IMPORTANT]  
   >  Use caution when you run the Registry Editor in this manner. PsExec.exe runs it in the LocalSystem context.  

4. In the Registry Editor, delete the following registry keys:  

   > [!IMPORTANT]  
   >  Delete these registry keys as the last step before imaging the reference computer. The Endpoint Protection client recreates these keys when it starts. If you restart the reference computer, delete the registry keys again.  

   -   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\InstallTime`  

   -   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastScanRun`  

   -   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastScanType`  

   -   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastQuickScanID`   

   -   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastFullScanID`  

   -   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\RemovalTools\MRT\GUID`

You're now ready to prepare the reference computer for imaging.

When you deploy an OS image that contains the Endpoint Protection client, it automatically reports information to the device's assigned Configuration Manager site. The client downloads and applies any targeted antimalware policy.  



## See also

For more information about OS deployment in Configuration Manager, see [Manage OS images](/sccm/osd/get-started/manage-operating-system-images).

