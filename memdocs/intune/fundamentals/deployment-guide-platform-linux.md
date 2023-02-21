---
# required metadata

title: Deployment guide for Linux device management | Microsoft Intune  
description: Use our platform deployment guide to set up Linux device management in Microsoft Intune.    
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 11/14/2022  
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: medium

# optional metadata

#ROBOTS:
#audience: 
#ms.devlang:
ms.reviewer: dougeby
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: get-started
ms.collection:
- tier2
- M365-identity-device-management
---

# Deployment guide: Manage Linux devices in Microsoft Intune

This guide describes everything you need to do to protect and manage Linux apps and endpoints using Microsoft Intune, including how to:       

* Prepare your tenant for device enrollment.  
* Create Linux device compliance policies. 
* Add custom compliance settings.   
* Enforce conditional access policies in Microsoft Edge. 
* Support employees and students enrolling their desktops.  

For each section in this guide, review the associated tasks. Some tasks are required and some, like setting up conditional access, are optional. Select the provided links in each section to go to our recommended help docs on Microsoft Learn, where you can find more detailed information and how-to instructions.        
 
## Step 1: Prerequisites  

 Microsoft Intune, Azure Active Directory (AD), and Microsoft Edge power the feature and capabilities for Linux desktop management. Microsoft Intune powers the device management and compliance capabilities. Azure AD powers conditional access, which is used alongside Microsoft Intune compliance policies. Microsoft Edge is the web browser app used to provide protected access to Microsoft 365 web apps. 
 
 Complete the following prerequisites to enable your tenant's endpoint management capabilities:   

* [Add users](users-add.md) and [groups](groups-add.md)
* [Assign licenses to users](licenses-assign.md) 
* [Set mobile device management authority](mdm-authority-set.md) 
* [Have Global Administrator or Intune administrator Azure Active Directory permissions](role-based-access-control.md)  

 For more details and recommendations about how to prepare your organization, onboard, or adopt Intune for mobile device management, see the [Intune setup deployment guide](deployment-guide-intune-setup.md).    

## Step 2: Plan for your deployment  

Use the [Microsoft Intune planning guide](intune-planning-guide.md) to define your device management goals, use-case scenarios, and requirements. It will also help you plan for rollout, communication, support, testing, and validation. For example, because you don't have to be there when employees and students are enrolling their devices, we recommend having a communication plan so that people know where to find information about installing and using Company Portal and Microsoft Edge.  

## Step 3: Create device compliance policies    
Create a device compliance policy to ensure that Linux devices accessing your data are secure and meet your organization's standards. The final stage of the enrollment process is the compliance evaluation, which verifies that the settings on the device meet your policies. Device users must resolve all compliance issues to get access to protected resources.  Intune marks devices that fall short of compliance requirements as *non-compliant* and takes additional action (such as sending the user a notification, restricting access, or wiping the device) according to your *action for noncompliance* configurations.  

You can enforce device compliance policies based on Linux distribution type, version, device encryption, or password complexity. All available compliance settings for Linux are in the Microsoft Intune settings catalog. You can use Azure AD conditional access policies in conjunction with device compliance policies to control access to Microsoft 365 web apps in Microsoft Edge. For example, if an employee tries to access Microsoft Teams in Edge without first enrolling or securing their device, they won't be able to sign in.    

>[!TIP]
>  For an overview of device compliance policies, see [Compliance overview](../protect/device-compliance-get-started.md#device-compliance-policies).     

| Task | Detail | 
| ---- | ------ | 
| [Create a device compliance policy](../protect/create-compliance-policy.md)|Get step-by-step guidance on how to create and assign a device compliance policy for Linux devices. |  
| [Add custom compliance settings](../protect/actions-for-noncompliance.md) | With custom compliance settings, you can write your own Bash scripts to address compliance scenarios not yet included in the device compliance options built into Microsoft Intune. This article describes how to create, monitor, and troubleshoot custom compliance policies for Linux devices. Custom compliance settings require you to [create a custom script](../protect/compliance-custom-json.md) that identifies the settings and value pairs.|  
| [Add actions for noncompliance](../protect/actions-for-noncompliance.md) |Choose what happens when devices no longer meet the conditions of your compliance policy. Examples of actions include sending alerts, remotely locking devices, or retiring devices. You can add actions for noncompliance when you configure a device compliance policy, or later by editing the policy. |  
| Create [a device-based](../protect/create-conditional-access-intune.md) or [app-based](../protect/app-based-conditional-access-intune-create.md) conditional access policy| Set up a conditional access policy to protect and grant access to Microsoft 365 web apps in the Microsoft Edge browser for Linux. Conditional access blocks noncompliant devices from accessing protected work apps in Edge, and grants access to compliant devices. You must have a device compliance policy for conditional access to work with Linux devices. |        

## Step 4: Enroll devices  

Enrollment is supported on Linux desktops running Ubuntu LTS, version 22.04 or 20.04. Employees assigned Intune licenses can enroll their personal Linux devices into Microsoft Intune whenever they want. During enrollment, their device is registered with Azure AD and evaluated for compliance. If you've applied a conditional access policy to Edge, users will be prompted to enroll their devices before they can access Microsoft 365 web apps with their work account.    

As an Intune administrator, you don't need to do anything to enable enrollment for employees, other than what's described under [Prerequisites](deployment-guide-platform-linux.md#step-1-prerequisites). However, it's important to provide them with help resources in case they need guidance during enrollment.  

>[!TIP]
> If you require device encryption, tell your employees prior to device enrollment so that, when possible, they can opt to encrypt their device during OS installation. It's easier and faster than encrypting the device after OS installation. Additionally, make your organization's operating system requirements and password complexity requirements easy to find on your website or in an onboarding email so that employees don't have to delay enrollment to seek out that information.  

| Task | Detail | 
| ---- | ------ | 
|[Install Microsoft Intune app for Linux](../user-help/microsoft-intune-app-linux.md)| Employees must install the Microsoft Intune app on their personal device for enrollment. This article describes how to install, update, and remove the Microsoft Intune app for Linux in the Terminal app. | 
|[Install Microsoft Edge web browser)](https://www.microsoft.com/edge)| To access protected websites and files, employees must have Microsoft Edge web browser, version 102.*X* or later. After they enroll their device, employees can sign into Microsoft Edge with their work account and access websites and files.   |  
|[Enroll Linux device in Intune](../user-help/enroll-device-linux.md)| This article is for device users and describes how to enroll a device with the Microsoft Intune app, and includes system requirements, prerequisites, and next steps. During this step, Microsoft Intune registers the device with Azure AD and creates a device record in Intune. After registration is complete, device compliance checks begin.  |  
|[Check device status and resolve compliance issues](../user-help/check-status-linux.md)| This article is for device users and describes how to resolve compliance issues in the Microsoft Intune app. Compliance checks happen during enrollment and thereafter when the device checks in with Intune. The Intune app notifies employees when they have a noncompliant setting on their device. Intune determines compliance and actions for noncompliance by using your device compliance and conditional access policies.  |  

## Next steps  

* Check out [Walk through Intune admin center](tutorial-walkthrough-endpoint-manager.md) for a tutorial about how to navigate and use Intune. Tutorials are 100 – 200 level content for people new to Intune or a specific scenario.   

* Check out the [Microsoft Tech Community](https://techcommunity.microsoft.com/t5/microsoft-intune-blog/increase-security-enable-quality-collaboration-for-linux/ba-p/3640485) for the latest information and blogs about Linux desktop management.  

* For other versions of this guide, see:   

    *  [Deployment guide: Manage Android devices in Microsoft Intune](deployment-guide-platform-android.md)  
    *  [Deployment guide: Manage iOS devices in Microsoft Intune](deployment-guide-platform-ios-ipados.md)
    *  [Deployment guide: Manage macOS devices in Microsoft Intune](deployment-guide-platform-macos.md)  
  


