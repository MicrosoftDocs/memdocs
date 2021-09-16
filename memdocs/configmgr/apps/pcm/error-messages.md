---
title: Error messages
titleSuffix: Configuration Manager
description: Learn about the error messages from Package Conversion Manager.
ms.date: 08/24/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: reference
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: medium
---

# Technical reference for Package Conversion Manager error messages

*Applies to: Configuration Manager (current branch)*

<!--1357861-->

This article describes the error messages that Package Conversion Manager displays. It also includes the possible causes of the error, and methods to correct the error. Package Conversion Manager logs error messages in **PCMTrace.log**. For more information, including how to control the verbosity level, see [Log files](troubleshoot-pcm.md#log-files).


#### Application creation failed with the following exception

The specified exception occurred during the submission of the application object to the Configuration Manager server.

Check your permissions in Configuration Manager, validate your connectivity, and then retry. If those actions don't fix the problem, examine the **PCMtrace.log** file (verbosity level 4) and **SMSProv.log**.


#### Conversion Error – APPLIES TO A PACKAGE TRANSFORM STATUS

A general exception occurred during the conversion of the package. Look in the **PCMtrace.log** file (verbosity level 4).

Check the user permissions for the network share (package data source), validate your connectivity, and then retry. If those actions don't fix the problem, examine the **PCMtrace.log** file (verbosity level 4).


#### Did not find a converted package and its resultant application in the workflow outputs
The application (converted package/program) was deleted.

Modify the dependent package/program to ensure that the dependent package/program exists.


#### Objects were not created successfully
There are several possible causes.

Check your permissions in Configuration Manager, validate your connectivity, and then retry. If those actions don't fix the problem, examine the **PCMtrace.log** file (verbosity level 4) and the **SMSProv.log** file.


#### Please close the wizard and resolve any issues with the selected package. See PCMTrace.Log for more details
There are several possible causes.

Check your permissions in Configuration Manager, validate your connectivity, and then retry. If those actions don't fix the problem, examine the **PCMtrace.log** file (verbosity level 4) and the **SMSProv.log** file.


#### Some Deployment Types are missing Detection Methods. All Deployment Types must have Detection Methods
Detection methods are missing from the program.

Add one or more detection methods during the **Fix and Convert** process.


#### There was an error preparing the package for conversion
There are several possible causes.

Check your permissions in Configuration Manager, validate your connectivity, and then retry. If those actions don't fix the problem, examine the **PCMtrace.log** file (verbosity level 4) and the **SMSProv.log** file.


