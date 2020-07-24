---
title: Configure Endpoint Protection on a standalone client
titleSuffix: Configuration Manager
description: Learn how to set up Configuration Manager to update and distribute malware definitions for Microsoft Defender.
ms.date: 07/22/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: e63f2394-6eb1-4a33-bec5-8377fc62a34e
author: mestew
ms.author: mstewart
manager: dougeby


---

# Configure Endpoint Protection on a standalone client

*Applies to: Configuration Manager (current branch)*

Your organization may have a number of non-domain joined clients that are not on your network or internet-based. You cannot manage or protect such standalone clients with the Microsoft Endpoint Configuration Manager system. Without any endpoint protection in place, these standalone clients are vulnerable to any potential malware attacks. In order to protect your standalone clients, you can manually configure them with the Endpoint Protection client.

This topic describes how to configure Endpoint Protection on a standalone client.

## Prerequisites for configuring Endpoint Protection on a standalone client

The following list contains the required prerequisites for configuring the Endpoint Protection client software on a standalone client computer.

- You must have access to the Endpoint Protection client installation package, **scepinstall.exe**. This package is available in the **Client** folder of the Configuration Manager installation folder on the site server.
- To deploy the Endpoint Protection client with your organization's required configuration, create and export an antimalware policy. Then specify this policy when you manually install the Endpoint Protection client. For more information, see [How to create and deploy antimalware policies](endpoint-antimalware-policies.md).

To configure Endpoint Protection on a standalone client manually:

- Create an antimalware policy for the standalone client
- Migrate SCEP client installation media from Configuration Manager server to the standalone client
- Install Endpoint Protection on the standalone client

## Create an antimalware policy for the standalone client

Instead of creating a new antimalware policy for your standalone client, you can also use the default policy settings, **ep_defaultpolicy.xml** saved in the **Client** folder of the Configuration Manager installation folder.

After you create the policy in the Configuration Manager console, you must transfer it to your target standalone client.

To create and transfer an antimalware policy for the standalone client:

1. In the **Configuration Manager** console, click **Assets and Compliance**.
2. In the **Assets and Compliance** workspace, expand **Endpoint Protection**, and then click **Antimalware Policies**.
3. On the **Home** tab, in the **Create** group, click **Create Antimalware Policy**.
4. In the **General** section of the **Create Antimalware Policy** dialog box, enter a name and a description for the policy.
5. In the **Create Antimalware Policy** dialog box, configure the settings that you require for this antimalware policy, and then click **OK**. For a list of settings that you can configure, see [List of Antimalware Policy Settings](endpoint-antimalware-policies.md#list-of-antimalware-policy-settings.)
6. Export the newly created policy as an XML:
    1. In the **Antimalware Policies** list, right-click the policy you just created.
    1. Select **Export**.
    1. Save the policy as an XML, for example, **standalone.xml**.
7. Transfer the new antimalware policy XML to the target standalone client on which you want to configure Endpoint Protection.

## Migrate Endpoint Protection client installation package to the standalone client
> [!NOTE]
> Starting in Configuration Manager 1802, you don't need to install the Endpoint Protection agent (SCEPInstall) on Windows 10 devices. If it's already installed on Windows 10 devices, Configuration Manager doesn't remove it. Administrators can remove the Endpoint Protection agent on Windows 10 devices that are running at least the 1802 client version. SCEPInstall.exe may still be present in C:\Windows\ccmsetup on some machines, but new client installations shouldn't download it.

1. Log in to the Configuration Manager server.
2. Navigate to the **Client** folder of the Configuration Manager installation folder.
3. Copy **scepinstall.exe**.
4. Transfer **scepinstall.exe** to the target standalone client on which you want to install the Endpoint Protection client software.

## Install Endpoint Protection on the standalone client
In this step, you will run the installer package (**scepinstall.exe**) and the antimalware policy (previously transferred from the Configuration Manager server) on the command prompt.

To install Endpoint Protection on the standalone client:

1. On the standalone client, open a command prompt as an administrator.
2. Change directory to the folder where you saved the **scepinstall.exe** installer file.
3. Run `scepinstall.exe`, adding any additional command-line properties that you require:

   |  Property   |                                  Description                                   |
   |-------------|--------------------------------------------------------------------------------|
   |    `/s`     |                           Run the installer silently                           |
   |    `/q`     |                        Extract the setup files silently                        |
   |    `/i`     |                           Run the installer normally                           |
   |  `/policy`  | Specify an antimalware policy file to configure the client during installation |
   | `/sqmoptin` |     Opt-in to the Microsoft Customer Experience Improvement Program (CEIP)     |

To install the client with the antimalware policy, run the following command:
```cmd
scepinstall.exe /policy <full path>\<policy file>
```
Replace **full path** with the path where you saved the antimalware policy XML file and **policy file** with the antimalware policy file name.
 
After you enter the command, the installer is extracted and the installation wizard is launched.

3. Follow the on-screen instructions to complete the client installation.

On the last screen of the installation wizard, the option to scan the computer for potential threats after getting the latest updates is selected by default. If this update check succeeds, you don't have to manually install the latest definition update package. 

Alternatively, you can run the update definition package manually after the Endpoint Protection installation is complete. 

## Run update definition package

To manually run the update definition package:

1. Download the latest update definition package.
2. Copy the package to the client computer.
3. Double-click the definition package to install it.

## Change policy settings on an Endpoint Protection configured standaone client
After your standalone client is configured with Endpoint Protection, for any future policy setting changes, you must apply them manually. 
1. Create a new policy or update an existing one in the Configuration Manager console.
2. Export the policy as an XML file and transfer it to the standalone client.
3. Run the following command on the standalone client:

```cmd
C:\Program Files\Microsoft Security Client\ConfigSecurityPolicy.exe <full path>\<policy file>
```
Replace **full path** with the path where you saved the new antimalware policy XML file and **policy file** with the antimalware policy file name.
