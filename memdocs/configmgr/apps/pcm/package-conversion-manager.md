---
title: Package Conversion Manager
titleSuffix: Configuration Manager
description: Learn about Package Conversion Manager to convert packages to applications in Configuration Manager.
ms.date: 11/30/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: overview
author: baladelli
ms.author: baladell
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Package Conversion Manager

*Applies to: Configuration Manager (current branch)*

<!--1357861-->

Package Conversion Manager helps you convert Configuration Manager legacy packages into applications. Applications have additional benefits such as dependencies, requirement rules, detection methods, and user device affinity.

A Configuration Manager application contains files and programs that you deploy to client devices. However, unlike legacy packages and programs, an application provides additional user-centric functionality. For example, an application might contain deployment types for a local installation of a software package, a virtual application package, or a version of the application for mobile devices.

For more information, see the following articles:

- [Introduction to application management](../understand/introduction-to-application-management.md)  
- [Packages and programs](../deploy-use/packages-and-programs.md)  

> [!Important]  
> If you previously installed an older version of Package Conversion Manager, first uninstall it before upgrading your site. This integrated version doesn't require installation, but may conflict with existing versions.  

This integrated version of Package Conversion Manager works on packages in the Configuration Manager current branch site. It's not a standalone tool. If you have packages and programs in an older version of Configuration Manager, first migrate the packages into your current branch site. For more information, see [Migrate data between hierarchies](../../core/migration/migrate-data-between-hierarchies.md).

## Planning

Before you start converting packages into applications, first develop a plan. The following process is an example plan:

- [Define a detailed package conversion plan](#bkmk_define)  

- [Select and prepare packages for conversion](#bkmk_prepare)  

- [Select test packages](#bkmk_test)  

- [Analyze, investigate, and convert packages](#bkmk_analyze)  

- [Test and deploy the applications](#bkmk_deploy)  


### <a name="bkmk_define"></a> Define a detailed package conversion plan

This section describes two sample package conversion plans:  

- [A high-resource test environment](#bkmk_define-high): You have a test environment with the resources, permissions, and architecture to fully replicate your production environment.  

- [A limited-resource test environment](#bkmk_define-limited): You don't have a test environment that fully replicates your production environment.  

Adjust these plans as necessary for other issues specific to your environment.

#### <a name="bkmk_define-high"></a> Sample plan for a high-resource test environment

Your test environment has the resources, permissions, and architecture similar to your production environment. Use the test environment to efficiently analyze and convert all of your packages, and then test all of your Configuration Manager applications. After completing that work, transfer it to the production environment. 

Your package conversion plan may be similar to the following steps:  

1.  Select the packages you want to convert.  

2.  Migrate the packages for conversion into your test environment.  

3.  Prepare the packages for conversion.  

4.  Select test packages.  

5.  Analyze, investigate, and convert the test packages.  

6.  Test the converted applications.  

7.  Analyze and convert the remaining (non-test) packages.  

8.  Export the applications from the test environment. Import them into your production environment.  

#### <a name="bkmk_define-limited"></a> Sample plan for a limited-resource test environment

Your test environment doesn't have the resources, permissions, and architecture similar to your production environment. You can't analyze, test, and convert all of your packages. In this scenario, only analyze, investigate, convert, and test your test packages. Then migrate the remaining packages to the production environment to analyze and convert. 

Your package conversion plan may be similar to the following steps:

1.  Select the packages you want to convert.  

2.  Select test packages.  

3.  Migrate the test packages into your test environment.  

4.  Prepare the test packages for conversion.  

5.  Analyze, investigate, and convert the test packages.  

6.  Test the converted applications.  

7.  Export the test applications from the test environment. Then import them into your production environment.  

8.  Migrate the remaining packages into the production environment and prepare them for conversion.  

9.  Analyze, investigate, and convert the remaining packages in the production environment.  

10. Release the remaining applications to the production environment.  


### <a name="bkmk_prepare"></a> Select and prepare packages for conversion

#### <a name="bkmk_prepare-select"></a> Select the packages that you want to convert

Not all packages are suitable to be converted into applications. Before you begin to convert packages, identify the packages that won't be converted. 

The best types of package for conversion to applications are those that contain user-facing software, for example:  

- Windows Installer files (.msi and .msu)  

- Microsoft Application Virtualization (App-V) programs  

- Windows executable files (.exe)  

The types of package that are best kept as packages and not converted to applications include:

- System maintenance tools. For example, scripts or backup utilities.  

- Packages for software that are out of support.

> [!Tip]  
> After identifying packages that aren't appropriate for conversion into applications, move them to a separate folder in the Configuration Manager console. To create a package folder in the Configuration Manager console:  
> - Right-click the **Packages** node.  
> - Select **Folders**, and then select **Create Folder**.  
> - Enter the folder name, for example `Not Converted`.  
> - Click **OK**.  

#### Prepare the packages for conversion

For each package you want to convert, ensure that they conform to the following conditions:  

- The source files location is a full UNC path, for example `\\Server\Share\File`.  

- Windows Installer files use only one unique product code.  


### <a name="bkmk_test"></a> Select test packages

If possible, your group of test packages should include packages that meet the following criteria:  

- At least one test package with a readiness state of **Automatic**.  

- At least one test package with a readiness state of **Manual**.  

Ideally, your test packages should be core packages, for example:  

- Packages that you know well.  

- Packages that are the most important to your organization.  

- Packages that you can most easily test.  

Identify the packages that are appropriate for testing. Then move them to a separate folder in the Configuration Manager console.


### <a name="bkmk_analyze"></a> Analyze, investigate, and convert packages

#### Analyze packages

To analyze an individual package or a small group, use Package Conversion Manager integrated in the Configuration Manager console. For more information, see [How to analyze and convert packages](how-to-analyze-and-convert.md).  

> [!NOTE]  
> See the **Package Conversion Status** node in the **Monitoring** workspace. It displays summary information about the analysis and conversion processes.  

#### Investigate analysis results

After analyzing the test packages, investigate the packages with a readiness state of **Manual** or **Error**. Determine the reasons why they have that state. Some common reasons for a readiness state of **Manual** or **Error** include:

- The package doesn't contain the information required to create a detection method in an application deployment type.  

- The package doesn't contain the information required to convert collections to global conditions and requirements.  

- The package contains more than one program.  

- The package is dependent on another package that you haven't converted to an application.  

For more information, use the following resources:  

- Review the error messages and fixes in [Technical reference for Package Conversion Manager error messages](error-messages.md)  

- Review the log file **PCMTrace.log**  

- [Troubleshoot Package Conversion Manager](troubleshoot-pcm.md)  

#### Convert the packages

For more information about how to convert packages, see [How to analyze and convert packages](how-to-analyze-and-convert.md).

> [!NOTE]  
> See the **Package Conversion Status** node in the **Monitoring** workspace. It displays summary information about the analysis and conversion processes.  


### <a name="bkmk_deploy"></a> Test and deploy the applications

Test the applications, either in your test environment or your production environment, according to your detailed package conversion plan.



## Recommendations

- Use the **Package Conversion Status** node in the **Monitoring** workspace. It displays summary information about the analysis and conversion processes.  

- Investigate the programs in your packages known as wrappers. Use the Package Conversion Manager plug-in to convert their functions into the equivalent Configuration Manager functionality.  

- Ensure that you thoroughly test each converted application before you deploy it in a production environment.  

## Next steps

[How to analyze and convert packages](how-to-analyze-and-convert.md)
