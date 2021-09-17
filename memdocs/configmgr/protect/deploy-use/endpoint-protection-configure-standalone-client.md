---
title: Configure Endpoint Protection on a standalone client
titleSuffix: Configuration Manager
description: Learn how to configure Endpoint Protection on a standalone client.
ms.date: 07/22/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
author: mestew
ms.author: mstewart
manager: dougeby
ms.localizationpriority: medium
---

# Configure Endpoint Protection on a standalone client

*Applies to: Configuration Manager (current branch)*

Your organization may have a number of standalone clients that you cannot manage or protect with Microsoft Endpoint Configuration Manager. Without any endpoint protection in place, these standalone clients are vulnerable to potential malware attacks. To protect such standalone clients, you can manually configure them with Endpoint Protection, as described in this topic.

To configure Endpoint Protection on a standalone client manually:

- [Create an antimalware policy for the standalone client](#create-an-antimalware-policy-for-the-standalone-client)
- [Transfer Endpoint Protection client installation package to the standalone client](#transfer-endpoint-protection-client-installation-package-to-the-standalone-client)
- [Install Endpoint Protection on the standalone client](#install-endpoint-protection-on-the-standalone-client)

## Prerequisites

The following are the prerequisites for configuring Endpoint Protection on a standalone client:

- You must have access to the Endpoint Protection client installation package, **scepinstall.exe**. You can find this package in the **C:\Program Files\Microsoft Configuration Manager\Client** folder. 
- Make sure that the [January 2017 anti-malware platform update for Endpoint Protection clients](https://support.microsoft.com/help/3209361/january-2017-anti-malware-platform-update-for-endpoint-protection-clie) is installed. 

## Create an antimalware policy for the standalone client

In this step, you create a custom antimalware policy in the Configuration Manager console and then transfer it to the standalone client.

When creating the antimalware policy, you must configure the definition update source to keep the policy definitions up to date on the standalone client. You can configure the definition update source as [Microsoft Update](endpoint-definitions-microsoft-updates.md) and [Microsoft Malware Protection Center](endpoint-definitions-protection-center.md), if your standalone client is connected to the internet. Alternatively, select [network share](endpoint-definitions-network.md) as the definition distribution source and update it periodically with the latest definition update package. 

To create an antimalware policy for the standalone client:

1. In the **Configuration Manager** console, click **Assets and Compliance**.
2. In the **Assets and Compliance** workspace, expand **Endpoint Protection**, and then click **Antimalware Policies**.
3. On the **Home** tab, in the **Create** group, click **Create Antimalware Policy**.
4. In the **General** section of the **Create Antimalware Policy** dialog box, enter a name and a description for the policy.
5. In the **Create Antimalware Policy** dialog box, configure the settings that you require for this antimalware policy, and then click **OK**. For a list of settings that you can configure, see [List of Antimalware Policy Settings](endpoint-antimalware-policies.md#list-of-antimalware-policy-settings).
    > [!NOTE]
    > For the **Definition Updates** setting, select **Updates distributed from Microsoft Update** and **Updates distributed from Microsoft Malware Protection Center** if your standalone client is connected to the internet.  
    > Alternatively, select **Updates from UNC file shares** to distribute the policy definitions through network share. Then, add one or more UNC paths to the location of the definition updates files on a network share.

6. Export the newly created policy as an XML:
    1. In the **Antimalware Policies** list, right-click your policy.
    1. Select **Export**.
    1. Save the policy as an XML, for example, **standalone.xml**.
7. Transfer the new antimalware policy XML to the target standalone client on which you want to configure Endpoint Protection.

## Transfer Endpoint Protection client installation package to the standalone client

In this step, you copy the Endpoint Protection client installation package (**scepinstall.exe**) from the Configuration Manager server and transfer it to the standalone client.

1. Log in to the Configuration Manager server.
2. Navigate to the **Client** folder of the Configuration Manager installation folder (**C:\Program Files\Microsoft Configuration Manager\Client**).
3. Copy **scepinstall.exe**.
4. Transfer **scepinstall.exe** to the target standalone client on which you want to install the Endpoint Protection client software.

## Install Endpoint Protection on the standalone client
In this step, you run the installer package (**scepinstall.exe**) and the antimalware policy (both previously transferred from the Configuration Manager server) from the command prompt on the standalone client.

To install Endpoint Protection on the standalone client:

1. On the standalone client, open a command prompt as an administrator.
2. Change directory to the folder where you saved the **scepinstall.exe** installer file.
3. Enter the following command to run **scepinstall.exe** with the antimalware policy:

    ```cmd
    scepinstall.exe /policy <full path>\<policy file>
    ```

    Replace `full path` with the path where you saved the antimalware policy XML file and `policy file` with the antimalware policy file name.
 
    The installer is extracted and the installation wizard is launched.

4. Follow the on-screen instructions to complete the client installation.

    On the last screen of the installation wizard, the option to scan the computer for potential threats after getting the latest updates is selected by default. You can clear the checkbox to skip the scanning.

## Change antimalware policy settings on a standalone Endpoint Protection client

To change or update the antimalware policy on your standalone Endpoint Protection client: 

1. [Create an antimalware policy for the standalone client](#create-an-antimalware-policy-for-the-standalone-client).
2. Run the following command on the standalone client:

```cmd
C:\Program Files\Microsoft Security Client\ConfigSecurityPolicy.exe <full path>\<policy file>
```

Replace `full path` with the path where you saved the new antimalware policy XML file and `policy file` with the antimalware policy file name.

## Next steps

For information on how to use Endpoint Protection to manage security and malware on Configuration Manager client computers, see [Configure Endpoint Protection](endpoint-protection-configure.md).