---
title: Example scenario to deploy and monitor security software updates
titleSuffix: "Configuration Manager"
description: "Use this example scenario of how to use software updates in Configuration Manager to deploy and monitor security software updates for Microsoft monthly releases."
author: aczechowski
manager: dougeby
ms.date: 10/06/2016
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: c32f757a-02da-43f2-b055-5cfd097d8c43
ms.author: aaroncz
---
# Example scenario for using System Center Configuration Manager to deploy and monitor the security software updates released monthly by Microsoft*Applies to: System Center Configuration Manager (Current Branch)*
This topic provides an example scenario of how you can use software updates in System Center Configuration Manager to deploy and monitor the security software updates that Microsoft releases monthly.  

 In this scenario, John is the Configuration Manager administrator at Woodgrove Bank. John needs to create a software update deployment strategy with the following conditions and requirements:  

- Active software update deployment occurs one week after Microsoft releases the security software updates on the second Tuesday of each month. This event is typically referred to as Patch Tuesday.  

- Software updates are downloaded and staged on distribution points. Then a deployment is tested to a subset of clients before John fully deploys the software updates in his production environment.  

- John must be able to monitor the software updates' compliance by month or by year.  

  This scenario assumes that the software update point infrastructure has already been implemented. Use the following information to plan for and configure software updates in Configuration Manager.  

|Process|Reference|  
|-------------|---------------|  
|Review the key concepts for software updates.|[Introduction to software updates](../understand/software-updates-introduction.md)|  
|Plan for software updates. This information helps you to plan for capacity considerations, determine the software update point infrastructure, software update point installation, synchronization settings, and client settings for software updates.|[Plan for software updates](../plan-design/plan-for-software-updates.md)|  
|Configure software updates. This information helps you to install and configure software update points in your hierarchy and helps to configure and synchronize software updates.<br /><br /> In this scenario, John configures the software updates synchronization schedule to occur on the second Wednesday of each month to ensure that he retrieves the latest security software updates from Microsoft.|[Synchronize software updates](../get-started/synchronize-software-updates.md)|  

 The following sections in this topic provide example steps to help you to deploy and monitor Configuration Manager security software updates in your organization.

##  <a name="BKMK_Step1"></a> Step 1: Create a software update group for yearly compliance  
 John creates a software update group that he can use to monitor compliance for all of the security software updates that he releases in 2016. He performs the steps in the following table.  

|Process|Reference|  
|-------------|---------------|  
|From the **All Software Updates** node in the Configuration Manager console, John adds criteria to display only security software updates that are released or revised in year 2015 that meet the following criteria:<br /><br /><ul><li>**Criteria**: Date Released or Revised</li><li>**Condition**: is greater than or equal to specific date<br />**Value**: 1/1/2015</li><li>**Criteria**: Update Classification<br />**Value**: Security Updates</li><li>**Criteria**: Expired <br />**Value**: No</li></ul>|No additional information|
|John adds all of the filtered software updates to a new software update group with the following requirements:<br /><br /><ul><li>**Name**: Compliance Group - Microsoft Security Updates 2015</li><li>**Description**: Software updates|[Add software updates to an update group](add-software-updates-to-an-update-group.md)|  

##  <a name="BKMK_Step2"></a> Step 2: Create an automatic deployment rule for the current month  
 John creates an automatic deployment rule for the security software updates that are released by Microsoft for the current month. He performs the steps in the following table.  

|Process|Reference|  
|-------------|---------------|  
|John creates an automatic deployment rule with the following requirements:<br /><br /><ol><li>On the **General** tab, John configures the following:<br /> <ul><li>Specifies **Monthly Security Updates** for the name.</li><li>Selects a test collection with limited clients.</li><li>Selects **Create a new Software Update Group**.</li><li>Verifies that **Enable the deployment after this rule is run** is not selected.</li></ul></li><li>On the **Deployment Settings** tab, John selects the default settings.</li><li>On the **Software Updates** page, John configures the following property filters and search criteria:<br /><ul><li>Date Released or Revised **Last 1 month**.</li><li>Update Classification **Security Updates**.</li></ul></li><li>On the **Evaluation** page, John enables the rule to run on a schedule for the **second Thursday** of every **month**. John also verifies that his synchronization schedule is set to run on the **second Wednesday** of every **month**.</li><li>John uses the default settings on the Deployment Schedule, User Experience, Alerts, and Download Settings pages.</li><li>On the **Deployment Package** page, John specifies a new deployment package.</li><li>John uses the default settings on the Download Location and Language Selection pages.</li></ol>|[Automatically deploy software updates](automatically-deploy-software-updates.md)|  

##  <a name="BKMK_Step3"></a> Step 3: Verify that software updates are ready to deploy  
 On the second Thursday of every month, John verifies that the software updates are ready to deploy. He performs the following step.  

|Process|Reference|  
|-------------|---------------|  
|John verifies that software updates synchronization completed successfully.|[Software updates synchronization status](monitor-software-updates.md#BKMK_SUSyncStatus)|  

##  <a name="BKMK_Step4"></a> Step 4: Deploy the software update group  
 After John verifies that the software updates are ready to deploy, he deploys the software updates. He performs the steps in the following table.  

|Process|Reference|  
|-------------|---------------|  
|John creates two test deployments for the new software update group. He considers the following environments for each deployment:<br /><br /> **Workstation test deployment**: John considers the following for the workstation test deployment:<br /><br /><ul><li>Specifies a deployment collection that contains a subset of workstation clients to verify the deployment.</li><li>Configures the deployment settings that are appropriate for the workstation clients in his environment.</li></ul><br />**Server test deployment**: John considers the following for the server test deployment:<br /><br /><ul><li>Specifies a deployment collection that contains a subset of server clients to verify the deployment.</li><li>Configures the deployment settings that are appropriate for the server clients in his environment.</li></ul>|[Deploy software updates](deploy-software-updates.md)|  
|John verifies that the test deployments have successfully deployed.|[Software updates deployment status](monitor-software-updates.md#BKMK_SUDeployStatus)|  
|John updates the two deployments with new collections that include his production workstations and servers.|No additional information|  

##  <a name="BKMK_Step5"></a> Step 5: Monitor compliance for deployed software updates  
 John monitors compliance of his software update deployments. He performs the step in the following table.  

|Process|Reference|  
|-------------|---------------|  
|John monitors the software updates deployment status in the Configuration Manager console and checks the software update deployment reports available from the console.|[Monitor software updates in System Center Configuration Manager](../../sum/deploy-use/monitor-software-updates.md)|  

##  <a name="BKMK_Step6"></a> Step 6: Add monthly software updates to the yearly update group  
 John adds the software updates from the monthly software update group to the yearly software update group. He performs the step in the following table.  

|Process|Reference|  
|-------------|---------------|  
|John selects the software updates from the monthly software update group and adds the software updates to the software updates group that he created for yearly compliance. He tracks the software update compliance and creates various reports for his management.|[Add software updates to a deployed update group](add-software-updates-to-an-update-group.md)|  

John has successfully completed his monthly deployment for security software updates. He continues to monitor and report on software update compliance to ensure that the clients in his environment are within acceptable compliance levels.  

##  <a name="BKMK_MonthlyProcess"></a> Recurring monthly process to deploy software updates  
 After the first month that John deploys software updates, he performs steps three through six to deploy the monthly security software updates released by Microsoft.  
