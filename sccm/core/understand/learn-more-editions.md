---
title: Learn More about licensing and branches
titleSuffix: Configuration Manager
description: Use this topic to learn about the licensing requirements for the installation options available with the October 2016 release of System Center Configuration Manager, which include the Current Branch version 1606, Long-Term Servicing Branch (LTSB), and Evaluation installation of the Current Branch.
ms.date: 12/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 495b87ae-41a4-49ba-abe2-d4f7d22ac0d4
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Licensing and branches for System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch), (Long-Term Servicing Branch)*

Use this topic to learn about the licensing requirements for the installation options available with the October 2016 release of System Center Configuration Manager version 1606. These installation options include the Current Branch version 1606, the Long-Term Servicing Branch (LTSB), and the evaluation installation of the Current Branch version 1606.

**Licensing overview:**   
Customers with active Software Assurance (SA) on System Center Configuration Manager licenses or with equivalent subscription rights as of October 1, 2016 have rights to use the October 2016 version 1606 release of System Center Configuration Manager. Customers with rights to System Center Configuration Manager on or after October 1, 2016 will find two licensed options upon installation: Current Branch and Long-Term Servicing Branch (LTSB).


**Licensing specifics:**  
[Complete terms and conditions for the products you purchase through Microsoft Volume Licensing programs can be found here](https://go.microsoft.com/fwlink/?LinkId=800052).


## System Center Configuration Manager licensed branches  
This topic references the Software Assurance agreement (or equivalent subscription rights), which is the Microsoft licensing agreement that grants rights to install and use Configuration Manager.


|Branch|Licensing|Details|
|----------------|---------------------|--------------------|
|Current Branch | Requires an active Software Assurance agreement (or equivalent rights) to Configuration Manager. </br></br> See [Software Assurance and the Current Branch](#software-assurance-and-the-current-Branch) in this topic.| Supported for use in production environments that want to receive regular quality and feature updates from Microsoft. </br></br> This branch provides access to use all features and improvements. </br></br> For versions of Configuration Manager released prior to 1710, support is for 12 months. Beginning with the 1710 release, each update version remains in support for 18 months from its general availability release date. See [Support for System Center Configuration Manager current branch versions](/sccm/core/servers/manage/current-branch-versions-supported) for more details.|
|Long-Term Servicing Branch (LTSB)| Requires a current Software Assurance agreement with Microsoft at the time of release (October 1st, 2016) </br></br> See [Software Assurance and the LTSB](#software-assurance-and-the-ltsb) in this topic. | Supported for use in production environments. Intended for use by customers that have let their Software Assurance (SA) or equivalent subscriptions rights to Configuration Manager expire after October 1st 2016. </br></br> This branch is limited when compared to the Current Branch. </br></br> Critical security updates for Configuration Manager are made available to this branch but no new features are made available. |
|Evaluation installation of the Current Branch| Does not require a Software Assurance agreement with Microsoft. | [Evaluation installs](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection) are always the Current Branch, and can be used for 180 days. </br></br> The evaluation installation can be upgraded to a full installation of the Current Branch. You cannot upgrade an evaluation installation to the Long-Term Servicing Branch.|

In addition to the Current Branch, LTSB, and evaluation installation of the Current Branch, a [Technical Preview of System Center Configuration Manager](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview) is also available. This is a limited build of Configuration Manager that lets you try out new features that might be added to the Current Branch in a future update. You install the Technical Preview using different media than the licensed versions. For more information see the documentation for the [Technical Preview](/sccm/core/get-started/technical-preview).


## Licensed branches
Customers with active Software Assurance (SA) on System Center Configuration Manager licenses or with equivalent subscription rights as of October 1, 2016 have rights to use the October 2016 version 1606 release of System Center Configuration Manager. Customers with rights to System Center Configuration Manager version 1606 on or after October 1, 2016 will find two licensed options upon installation:
-	**Current Branch**
-	**Long-Term Servicing Branch (LTSB)**


See the table in the previous section for more information.


## Software Assurance agreements and System Center Configuration Manager
The status of Software Assurance on your System Center Configuration Manager licenses, or equivalent subscription rights, on or after October 1, 2016, determines the branch you can install and use.


### Software Assurance and the Current Branch
Rights to use System Center Configuration Manager Current Branch can be provided by:
-  **System Center:** Customers with active SA on System Center Standard or Datacenter licenses can install and use the Current Branch option of System Center Configuration Manager.

-  **System Center Configuration Manager:** Customers with active SA on System Center Configuration Manager licenses, or with equivalent subscription rights, can install and use the Current Branch option of System Center Configuration Manager.

If you have active SA on System Center Configuration Manager licenses (or equivalent subscription rights) on or after October 1, 2016:
- You can install and use the Current Branch.
- If you allow SA or subscription to lapse, you must uninstall the Current Branch.

### Software Assurance and the LTSB
 If you have an active SA on System Center Configuration Manager licenses (or equivalent subscription rights) on or after October 1, 2016:
 - You can install and use the LTSB. Customers who have perpetual rights to System Center Configuration Manager, or who allow thier SA or subscription to lapse, can install the version of System Center Configuration Manager LTSB that is current at the time of lapse.

LTSB is based on Current Branch version 1606, and has the following limitations:
  - There is no support to convert a Current Branch to the LTSB. If you currently have a Current Branch site, you must install the LTSB as a new site.  

  - LTSB does not support all the capabilities of the Current Branch. Limitations are detailed in [Introduction to the  Long-Term Servicing Branch](introduction-to-the-ltsb.md) and its related documentation. These limitations include a limited feature set, limited upgrade options, and a separate product support lifecycle.  


### Software Assurance expiration date
Beginning with the October 2016 release of the version 1606 baseline media for System Center Configuration Manager, you can specify the expiration date of your Software Assurance agreement. The **Software Assurance expiration date** is an optional value you can specify as a convenient reminder when you run Configuration Manager Setup or later from within the Configuration Manager console.

>  [!NOTE]   
>  Microsoft does not validate the expiration date you specify, and does not use this date for license validation.  Instead, you can use it as a reminder of your expiration date. This is useful because Configuration Manager periodically checks for new software updates offered  online, and your Software Assurance license status should be current to be eligible to use these additional updates.    

**To specify the date:**
- When you run Setup from the System Center Configuration Manager version 1606 baseline media, you can specify the value on the **Product Key** page of the Setup wizard.

- In the Configuration Manager console, in **Hierarchy Settings Properties**, you can specify the value on the **Licensing** tab.

For more information about Software Assurance licensing and the Current Branch of System Center Configuration Manager, see [Licensing and branches for System Center Configuration Manager](/sccm/core/understand/learn-more-editions).


## Resources for Licensing information
Use the following links to learn more about product licensing details.

**Microsoft Volume Licensing Service Center (VLSC) links:**
- [Overview of VLSC](https://www.microsoft.com/en-us/Licensing/existing-customer/vlsc-training-and-resources.aspx)

- [Microsoft Volume Licensing Product Terms](https://go.microsoft.com/fwlink/?LinkId=800052)

- Volume license customers can get a summary of their licenses from the [Volume License Service Center](https://www.microsoft.com/Licensing/servicecenter/default.aspx). Go to the **Licenses** menu, and click **Licenses Summary** for an overview of licenses.

**VLSC Videos:**
- [Training videos on how VLSC works](https://www.microsoft.com/en-us/Licensing/existing-customer/vlsc-training-and-resources.aspx#tab=2)  

- [Where to look up your active Software Assurance agreement](https://www.microsoft.com/showcase/video.aspx?uuid=fe1846cb-1d26-49fc-b064-57b25dcc31a0) (starting around 43 seconds in)  

- [How to get permissions for VLSC](https://www.microsoft.com/showcase/video.aspx?uuid=ac4ed1ca-d0a9-43cd-89fa-74ccb555dec4). You can delegate VLSC read and write permissions to other people in your organization.
