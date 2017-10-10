---
title: "Configure Endpoint Protection Client"
titleSuffix: "Configuration Manager"
description: "Learn how to configure custom client settings for Endpoint Protection that can be deployed to computer collections in your hierarchy."
ms.custom: na
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: e63f2394-6eb1-4a33-bec5-8377fc62a34e
caps.latest.revision: 21
author: NathBarnms.author: nathbarnmanager: angrobe

---

# Configure Custom Client Settings for Endpoint Protection*Applies to: System Center Configuration Manager (Current Branch)*
This procedure configures custom client settings for Endpoint Protection which can be deployed to collections of computers in your hierarchy.

> [!IMPORTANT]
>  Only configure the default Endpoint Protection client settings if you are sure that you want them applied to all computers in your hierarchy.

## To enable Endpoint Protection and configure custom client settings

1.  In the Configuration Manager console, click **Administration**.

2.  In the **Administration** workspace, click **Client Settings**.

3.  On the **Home** tab, in the **Create** group, click **Create Custom Client Device Settings**.

4.  In the **Create Custom Client Device Settings** dialog box, provide a name and a description for the group of settings, and then select **Endpoint Protection**.

5.  Configure the Endpoint Protection client settings that you require. For a full list of Endpoint Protection client settings that you can configure, see the Endpoint Protection section in [About client settings in System Center Configuration Manager](../../core/clients/deploy/about-client-settings.md).

   > [!IMPORTANT]
   >  You must install the Endpoint Protection site system role before you can configure client settings for Endpoint Protection.

6.  Click **OK** to close the **Create Custom Client Device Settings** dialog box. The new client settings are displayed in the **Client Settings** node of the **Administration** workspace.

7.  Before the custom client settings can be used, you must deploy them to a collection. Select the custom client settings you want to deploy and then, in the **Home** tab, in the **Client Settings** group, click **Deploy**.

8.  In the **Select Collection** dialog box, choose the collection to which you want to deploy the client settings and then click **OK**. The new deployment is shown in the **Deployments** tab of the details pane.

Client computers will be configured with these settings when they next download client policy. To initiate policy retrieval for a single client, see the Initiate Policy Retrieval for a Configuration Manager Client section in [How to manage clients in System Center Configuration Manager](../../core/clients/manage/manage-clients.md).

## How to Provision the Endpoint Protection Client in a Disk Image in Configuration Manager
You can install the Endpoint Protection client on a computer that you intend to use as a disk image source for Configuration Manager operating system deployment. This computer is typically called the reference computer. After you create the image of the operating system, you can then use Configuration Manager operating system deployment to deploy the image that can contain software packages, including Endpoint Protection, to your client computers.

Use the procedures in this topic to help you install and configure the Endpoint Protection client on a reference computer

### Prerequisites for Installing the Endpoint Protection Client on the Reference Computer
The following list contains the required prerequisites for installing the Endpoint Protection client software on a reference computer.

-   You must have access to the Endpoint Protection client installation package, **scepinstall.exe**. This package can be found in the **Client** folder of the Microsoft System Center Configuration Manager installation folder on the site server.

-   To ensure that the Endpoint Protection client is deployed with the configuration that is required in your organization, create an antimalware policy, and then export that policy. You can then specify the antimalware policy to use when you manually install the Endpoint Protection client. For more information, see [How to create and deploy antimalware policies for Endpoint Protection in System Center Configuration Manager](endpoint-antimalware-policies.md).

   > [!NOTE]
   >  The **Default Client Antimalware Policy** cannot be exported.

-   If you want to install the Endpoint Protection client with the latest definitions, you must download these from the [Microsoft Malware Protection Center](http://go.microsoft.com/fwlink/?LinkID=200965).

### How to Install the Endpoint Protection Client Software on the Reference Computer
You can install the Endpoint Protection client locally on the reference computer from a command prompt. To do so, you must first obtain the installation file **scepinstall.exe**. You can also install the client with an preconfigured antimalware policy or with an antimalware policy that you previously exported.

## To install the Endpoint Protection client from a command prompt

1.  Copy **scepinstall.exe** from the **Client** folder on the System Center Configuration Manager installation media to the computer on which you want to install the Endpoint Protection client software.

2.  Open a command prompt with administrator privileges, navigate to the folder where **scepinstall.exe** is located, and then run the following command, adding any additional command line properties that you require:

   ```
   scepinstall.exe
   ```

    You can specify one of the following command line properties:

   |Property|Description|
   |--------------|-----------------|
   |/s|Specifies that a silent installation will be performed.|
   |/q|Specifies that a silent extraction of the setup files will be performed.|
   |/i|Specifies that a normal installation should be performed.|
   |/noreplace|Specifies that third-party antimalware software is not uninstalled during setup.|
   |/policy|Specifies an antimalware policy file to be used to configure the client during installation.|
   |/sqmoptin|Specifies that this client software installation is opted in to the Microsoft Customer Experience Improvement Program.|

3.  Follow the on-screen instructions in order to complete the client installation.

4.  If you downloaded the latest update definition package, copy the package to the client computer, and then double-click the definition package to install it.

   > [!NOTE]
   >  After the Endpoint Protection client installation is completed, the client automatically performs a definition update check. If this update check succeeds, you do not have to manually install the latest definition update package.

## To install the client software with an antimalware policy from the command prompt

1.  Copy **scepinstall.exe** and the exported or preconfigured antimalware policy to the computer on which you want to install the Endpoint Protection client software.

2.  Open a command prompt with administrator privileges, navigate to the folder where **scepinstall.exe** and the antimalware policy are located, and then run the following command:

   ```
   scepinstall.exe /policy <full path>\<policy file>
   ```

3.  Follow the on-screen instructions in order to complete the client installation.

4.  If you downloaded the latest definition package, copy the package to the client computer, and then double-click the definition package to install it.

   > [!NOTE]
   >  After the Endpoint Protection client installation is completed, the client automatically performs a definition update check. If this update check succeeds, you do not have to manually install the latest definition update package.

## Verify that the Endpoint Protection Client is Installed Correctly
After you install the Endpoint Protection client on your reference computer, verify that the client is working correctly.

### To verify that the Endpoint Protection client is installed correctly

1.  On the reference computer, open **System Center Endpoint Protection** from the Windows notification are.

2.  On the **Home** tab of the **System Center Endpoint Protection** dialog box, verify that **Real-time protection** is set to **On**.

3.  Verify that **Up to date** is displayed for **Virus and spyware definitions**.

4.  To help make sure that your reference computer is ready for imaging, under **Scan options**, select **Full**, and then click **Scan now**.

### How to Prepare the Endpoint Protection Client for Imaging
After you verify that the Endpoint Protection client is installed correctly on the reference computer, you can prepare the computer for imaging. Perform the following steps to prepare the Endpoint Protection client for imaging.


For more information about operating system deployment in Configuration Manager, see [Manage operating system images with System Center Configuration Manager](/sccm/osd/get-started/manage-operating-system-images).

### To prepare the Endpoint Protection client for imaging

1.  On the reference computer, log on as a user that has administrative privileges.

2.  Download and install **PsTools** from the [Windows SysInternals Site](http://go.microsoft.com/fwlink/?LinkId=215263) on TechNet.

3.  Open an elevated command prompt, navigate to the folder in which you installed PsTools, and then type the following command

   ```
   Psexec.exe -s -i regedit.exe
   ```

   > [!IMPORTANT]
   >  Use caution while you are running the Registry Editor in this manner; the -s option in PsExec.exe runs the Registry Editor with LocalSystem privileges.

4.  In the Registry Editor, navigate to each of the following registry keys and delete them.

   > [!IMPORTANT]
   >  You must delete the registry keys as the last step before imaging the reference computer. The registry keys are recreated when the Endpoint Protection client starts. If you restart the reference computer, you must delete the registry keys again.

   -   **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\InstallTime**

   -   **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastScanRun**

   -   **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastScanType**

   -   **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastQuickScanID**

   -   **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastFullScanID**

   -   **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\RemovalTools\MRT\GUID**

After you complete the preceding steps, you can prepare the reference computer for imaging. For more information about operating system deployment in Configuration Manager, see [Manage operating system images with System Center Configuration Manager](/sccm/osd/get-started/manage-operating-system-images).

When an image that contains the Endpoint Protection client software is deployed, the Endpoint Protection client will automatically report information to the Configuration Manager site to which the computer is assigned, and policy applicable to the client computer is downloaded and applied.
