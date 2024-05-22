---
# required metadata

title: Evaluate WSL instance attributes to Windows host device compliance state 
description: Evaluate WSL attributes on a host device for compliance. 
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 5/22/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.suite: ems
search.appverid: MET150
ms.reviewer: ilwu
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier1
- M365-identity-device-management
- highpri
- compliance
---

# Evaluate WSL instance attributes to Windows host device compliance state  

**Applies to**: 
- Windows 10   
- Windows 11   

Create a Microsoft Intune policy that checks the compliance of devices running Windows Subsystem for Linux (WSL). Microsoft Intune incorporates the WSL compliance results into the overall compliance state of the host device so that you can see the whole health of the device.

This article describes how to set up device compliance checks for WSL.  

> [!IMPORTANT]
> This feature is in public preview. For more information, see [Public preview in Microsoft Intune](../fundamentals/public-preview.md).   

## Resources 

These resources are required create your custom compliance script.  

- [Intune plugin for WSL](https://github.com/microsoft/shell-intune-samples/blob/master/Linux/WSL/IntuneWSLPluginInstaller/IntuneWSLPluginInstaller.msi): Use the example Powershell script to get the installer for the Intune plugin.    

- [Custom compliance script](https://github.com/microsoft/shell-intune-samples/blob/master/Linux/WSL/WSL%20Management%20Example/WSLDistroVersionCompliance.ps1): The example Powershell script calculates compliance against WSL distros based on Distro and Distro Version.  

- [JSON for validation](https://github.com/microsoft/shell-intune-samples/blob/master/Linux/WSL/WSL%20Management%20Example/WSLDetectionRule.json): Use the example JSON to define WSL detection rules.  

## Step 1: Install Intune plugin for WSL   

Use the Intune plugin for WSL resource to install the Microsoft Intune plugin for WSL on the target machine.   

## Step 2: Add policy for line-of-business app 

Create an app policy for the Intune plugin installer. The plugin installer is considered a Windows line-of-business app. 

1. In the Microsoft Intune admin center, go to **Apps** > **Windows**.  

2. Enter app information:  
   - **Select file**: Select this option to upload the package file for the Intune plugin installer.  
  - **Name**: Enter **Intune WSL Plugin**. 
  - **Description**: Enter a description for the app. This setting is optional but recommended. 
  - **Publisher**: Enter **Microsoft Intune**.  

3. Select **Next** to go to **Assignments**.  

4. Add Microsoft Entra users under **Required** to assign the policy.  

5. Select **Next** to go to **Review + create**.  

6. Review the summary and then select **Create** to save the policy.  

## Step 3: Set up custom script  
In a command line, complete the following steps:  

1. In lines 23 through 28 of the custom compliance script, modify the following properties to match your organization's requirements:   

  - Distros    

  - Minimum/maximum version    

  - Number of days since last check-in a device can remain compliant  
  
1.  In the JSON for validation resource, modify the following fields with your organization's custom values: 

  - **MoreInfoUrl** - Enter the URL where device users can go to learn more about how to meet compliance requirements.  
 
  - **RemediationStrings**:  Enter helpful information for the device user about the compliance requirement for WSL. 
    
    - **Language** - Example: `en-us`  
    - **Title** - Example: `WSL distros not in compliance with company policy` 
    - **Descriptioon** - Example: `Make sure only allowed distros and versions are registered in WSL.` 



## Step 4: Deploy custom compliance policy  
 Deploy the custom compliance policy to targeted devices.  

 1. In the admin center, go to **Endpoint security** > **Device compliance**.  
 
 1. Go to **Scripts**.   
 
 1. Select **Add** > **Windows 10 and later**.  
 
 1. Enter the basic information for your policy, including name and description. 
 
 1. Select **Next** to go to **Settings**.    
 
 1. Copy and paste your custom compliance script into **Detection Script**. 
 
 1. Leave all other settings as is.  


## Step 5: Create device compliance policy  
Create a new device compliance policy for devices running Windows 10 and later. 

1. In the admin center, go to **Endpoint security** > **Device compliance**. 

1. Go to **Policies**.    

1. Select **Create policy**. 

1. For platform, choose **Windows 10 and later**.  

1. Select **Create**. 

1. Enter the basic information for your policy, including **Name** and **Description**. 

1. Select **Next** to go to **Compliance settings**.    

1. Expand **Custom Compliance**: 
  
  1. Select the custom compliance script file as the discovery script,   
  
  1. Upload your JSON validation file. 

1. Leave all other settings as is. Select **Next**. 

1. Review the summary of your policy, and then select **Create** to save it.  

## Remediation  

A quick way to get a device back to a compliant state is to unregister the non-compliant distro on the device. Use the following command to unregister a distro.   


`wsl --unregister [DISTRONAME]` 


## Troubleshooting  

* **Wsl/Service/CreateInstance/CreateVm/Plugin/ERROR_MOD_NOT_FOUND** 	 

   * Restart the WSL service. In an elevated PowerShell window, run these commands: 
 
     `sc.exe stop wslservice` 

     `wsl.exe echo “test”` 

For WSL troubleshooting help, see [Windows Subsystem for Linux](/windows/wsl/troubleshooting.md).  

## Next steps

[Monitor your policies](compliance-policy-monitor.md).
