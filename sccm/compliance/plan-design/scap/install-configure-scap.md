---
title: "Install and configure Security Content Automation Protocol (SCAP) extensions"
titleSuffix: "System Center Configuration Manager"
description: "Install and configure the Security Content Automation Protocol (SCAP) extensions"
ms.custom: na
ms.date: 03/27/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f53b484b-5123-48f0-be2f-4e30318f3d39
caps.latest.revision: 1
caps.handback.revision: 0
author: mestew
ms.author: mstewart
manager: dougeby
robots: noindex,nofollow
---

# Install and Configure the SCAP Extensions for Microsoft System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

> [!Tip]  
> This feature was first introduced in Technical Preview version 1803 as a [pre-release feature](/sccm/core/servers/manage/pre-release-features). This pre-release version of the SCAP extensions can be installed on any currently supported versions of Configuration Manager current branch and LTSB 1606. The install file is located at cd.latest\SMSSETUP\TOOLS\ConfigMgrSCAPExtension\ConfigMgrExtensionsForSCAP.msi starting in 1803 technical preview.   

After preparing the prerequisite infrastructure, you're ready to install and configure the SCAP Extensions for Microsoft System Center Configuration Manager on the computer from which you want to run this process.

## Install SCAP Extensions Configuration Manager

1. Run ConfigMgr\_Extensions\_for\_SCAP.msi to install the tool.
2. In Windows Explorer, go to the folder where you downloaded the **ConfigMgr\_Extensions\_for\_SCAP.msi** file, and then double-click the **ConfigMgr\_Extensions\_for\_SCAP.msi** file. This starts the SCAP Extensions for Microsoft System Center Configuration Manager Installation Wizard.

Complete the **SCAP Extensions for Microsoft System Center Configuration Manager Installation Wizard** using the information in the following table, accepting the wizard&#39;s default values unless you need to specify them.

**Table 1.0** SCAP Extensions for Microsoft System Center Configuration Manager Installation Wizard Process

| Wizard page name | User action |
| --- | --- |
| Welcome and End-User License Agreement |1. Review the license agreement|
| Welcome and End-User License Agreement|2. Click **I accept the terms in the License Agreement**.|
| Welcome and End-User License Agreement|3. Click **Install**.|
| Completed the SCAP Extensions for Microsoft System Center Configuration Manager Installation Wizard |4. Click **Finish**.|
 



The SCAP Extensions for Microsoft System Center Configuration Manager Installation Wizard installs the extensions by default in the Configuration Manager console install folder.



## Download and Install the SCAP Data Stream Files

Before you can run the SCAP Extensions to convert SCAP data stream files and then import them into the Compliance Settings feature, you must download the SCAP data stream files from the National Vulnerability Database (NVD) [download page](http://nvd.nist.gov/fdcc/download_fdcc.cfm) Web site. Then copy them into the folder where you installed the SCAP Extensions

Depending on your environment, you may not need all the SCAP data stream files listed on the download page.

To install the SCAP data streams

1. Visit the [NVD Web site](http://nvd.nist.gov/) to identify the SCAP data streams that are required by your organization.
The SCAP data streams published by NIST are organized into multiple bundles, which are also called _checklists_.

2. Download the SCAP data streams from the [NVD Web site](http://nvd.nist.gov/home.cfm), which are stored in compressed files with a .zip file name extension or marked as DataStream XML file.

    >[!IMPORTANT] 
    >There are many SCAP data stream files with the .xml extension that you can download from the NVD. However, only .xml files that include XCCDF (SCAP1.0 and 1.1)/DataStream (SCAP1.2) content are appropriate for use with the SCAP Extensions.

3. Extract the SCAP data streams .zip files/DataStream XML file that you downloaded into the same folder where you installed the SCAP Extensions.

## Convert and Import the SCAP Data Stream Files using the Import SCAP Content Wizard

After getting the SCAP data streams, you're ready to import and convert the data streams to Configuration baselines. The SCAP data streams published by NIST are organized into multiple bundles. Follow NIST&#39;s instructions to verify which bundles to use in your environment. For example, there's a separate bundle for each version of Windows, another version-specific bundle for the firewall configuration, and a bundle for Internet Explorer 8.0. Use the following procedures to accomplish this task.

### To import the SCAP data streams into Configuration Manager

1. Start the Import SCAP Content Wizard from the ribbon of the Configuration Baseline.

     ![Start the import SCAP content wizard from CI baseline ribbon](./media/import-scap-content.png)

2. Select Content Type.

      ![Select Content Type](./media/import-new-scap-content.png)

3. Select the SCAP datastream file, XCCDF, and CPE dictionary file or Oval content file.

     ![Select the SCAP datastream file](./media/select-datastream-file.png)

4. If SCAP 1.2 select the datastream. Then select the benchmark and profile for SCAP 1.x.  Select **Next** to convert the content. You will see a progress bar.

      ![Select the benchmark and profile for SCAP 1.2](./media/select-benchmark-and-profile.png)

5. Confirm the configuration data to be imported.

      ![Confirm the configuration screenshot](./media/confirm-configuration.png)

6. Click**Next** to import the configuration data.

      ![Complete the import](./media/complete-import.png)

## (Alternate method) Convert and Import the SCAP Data Stream Files using the cmd line tool

After getting the SCAP data streams, you may use the Microsoft.Sces.ScapToDcm.exe tool to convert the SCAP data streams into Compliance Settings compliant .cab files. Then import the .cab files into Configuration Manager. The Microsoft.Sces.ScapToDcm.exe tool converts the SCAP data streams into configuration items and configuration baselines that you can access using the Compliance Settings feature in Configuration Manager. The Microsoft.Sces.ScapToDcm.exe tool converts the SCAP data streams into XML manifests. It then packages the XML manifests into a .cab file that you can import into Configuration Manager.

The SCAP data streams published by NIST are organized into multiple bundles. Follow NIST&#39;s instructions to verify which bundles to use in your environment. For example, there's a separate bundle for each version of Windows, another version-specific bundle for the firewall configuration, and a bundle for Internet Explorer 8.0. Use the following procedures to accomplish this task.





## To import the SCAP data streams into Configuration Manager

1. Convert the SCAP data streams into a Compliance Settings compliant .cab file.
2. Import the .cab file into Configuration Manager.

### Convert the SCAP Data Streams into Compliance Settings Compliant .cab Files

Before you can analyze and assess the compliance of your systems, you need to convert the SCAP data streams in XML format into XML manifests that are compliant with Compliance Settings configuration items and configuration baselines. The Microsoft.Sces.ScapToDcm.exe tool converts the SCAP data streams into XML manifests. It then packages the XML manifests into a .cab file that you can later import into Configuration Manager.

#### **To convert the SCAP data streams into Compliance Settings compliant .cab files using the Microsoft.Sces.ScapToDcm.exe tool**

At the command prompt, go to AdminConsole\Bin folder, run Microsoft.Sces.ScapToDcm.exe to generate a Compliance Settings compliant cab and import it to the Configuration Manager site.

   >[!NOTE] 
   > Your account must have read/write permissions for the output folder

**For SCAP 1.0/1.1 content (XCCDF XML file, such as USGCB and DISA content):**

 Microsoft.Sces.ScapToDcm.exe –xccdf &lt;xccdf.xml&gt; -cpe &lt;cpe.xml&gt; -out &lt;outputFolder&gt; [-select benchmark/profile] [-log LogFileName]

   >[!NOTE] 
   >If you don&#39;t specify the benchmark/profile by using the –select parameter, then the tool will generate a DCM cab for each benchmark in the content file.

**For SCAP1.2 content- (DataStream XML file, such as the latest USGCB content-):**

Microsoft.Sces.ScapToDcm.exe –scap &lt;scapdatastreamfile.xml&gt; -out &lt;outputFolder&gt; [-select datastream/benchmark/profile] [-log LogFileName]

   >[!NOTE] 
   > If you don&#39;t specify the datastream/benchmark/profile by using the–select parameter, then the tool will generate a DCM cab for each benchmark in the content file.

**For single OVAL file with external variables:**

Microsoft.Sces.ScapToDcm.exe –oval &lt;singleOvalFile.xml&gt; [-variable &lt;externalVariableFile.xml&gt;] -out &lt;outputFolder&gt; [-log LogFileName]

   >[!NOTE] 
   > If there are multiple values for one variable in the external variable file, then the Microsoft.Sces.ScapToDcm.exe tool will treat the values as an array for this variable.



#### Microsoft.Sces.ScapToDcm.exe. Command-Line Parameters

| **Parameter** | **Usage** | **Required** |
| --- | --- | --- |
| -scap [scap data stream file] | Specify the SCAP data stream file | Yes (for SCAP 1.2 data stream, mutually exclusive with –xccdf and –oval / -variable) |
| -xccdf [xccdf file] | Specify the XCCDF file | Yes (for SCAP 1.0/1.1 XCCDF, mutually exclusive with –scap and –oval / -variable) |
| -cpe [cpe file] | Specify the CPE file | Yes (for SCAP 1.0/1.1 XCCDF, mutually exclusive with –scap and –oval / -variable) |
| -oval [oval file] | Specify the OVAL file | Yes (for standalone OVAL file, mutually exclusive with –xccdf and -scap) |
| -variable [oval external variable file] | Specify the OVAL external variable file | No (Optional for standalone OVAL file when there is an external OVAL variable file, mutually exclusive with –xccdf and -scap) |
| -select [xccdf benchmark/profile] | Select XCCDF benchmark, profile from either the SCAP data stream or XCCDF file | No (We suggest specifying this switch. If not specified, then the tool will generate a cab for all the profiles in all embedded DataStream/benchmarks) |
| -out [output directory] | Specify where to output the DCM cab file | No (if not specified, then the tool will only list the content without conversion) |
| -log [log file] | Specify the log file | No (if not specified, then log is written to Microsoft.Sces.ScapToDcm.log file) |
| -help / -? | Print out tool usage | No |





#### The following command lines are samples for the Microsoft.Sces.ScapToDcm.exe tool:

**SCAP1.2 Content:**

  Microsoft.Sces.ScapToDcm.exe –scap scap\_gov.nist\_USTCB-ie8.xml –out .\mytestfolder –select mySCAPDataStreamID/myBenchMarkID/myProfileID

**SCAP1.0/1.1 Content:**

   Microsoft.Sces.ScapToDcm.exe–xccdf scap\_gov.nist\_Test-WinXP\_xccdf.xml –cpe scap\_gov.nist\_Test-WinXP\_cpe.xml –out .\mytestfolder –select XCCDFBenchmarkID/MyProfileID

**SCAP OVAL Content:**

  Microsoft.Sces.ScapToDcm.exe –oval myOvalFile.xml –variable myOvalExternalVariableFile.xml –out .\mytestfolder

**The following output is sample from the Microsoft.Sces.ScapToDcm.exe tool:**

  Compliance Settings compliant cab file created:

  Validate the schema of SCAP data stream file C:\24SCAP\BVT\_Test\_Data\_Stream.xml

  Successfully validate the schema of SCAP data stream file C:\24SCAP\BVT\_Test\_Data\_Stream.xml

  Process XCCDF Benchmark xccdf\_tst.bvt\_benchmark\_Windows-F

  Process XCCDF Profile: xccdf\_tst.bvt\_profile\_version\_1.0.0.0-BVT Profile #1

  Process OVAL: scap\_tst.bvt\_comp\_Windows-F-oval.xml

  Successfully finished process OVAL: scap\_tst.bvt\_comp\_Windows-F-oval.xml

  Process OVAL: scap\_tst.bvt\_comp\_Windows-F-cpe-oval.xml

  Successfully finished process OVAL: scap\_tst.bvt\_comp\_Windows-F-cpe-oval.xml
   Process SCAP data stream: scap\_tst.bvt\_datastream\_Windows-F.zip
    SCAP Data Stream: [scap\_tst.bvt\_datastream\_Windows-F.zip]

  Version:        [1.2]

  Timestamp:      [2/24/2012]

  Use-case:       [CONFIGURATION]

  CPE Dictionary:  [scap\_tst.bvt\_comp\_Windows-F-cpe-dictionary.xml]

  OVAL:              [Windows-F-cpe-oval.xml]
  Product name:    [National Institute of Standards and Technology]

  Product version: []

  Schema version:  [5.3]

  Timestamp:       [2/24/2012]

  XCCDF Benchmark: [xccdf\_tst.bvt\_benchmark\_Windows-F]

  Version:       [v1.0.0.0]
   Update:        [http://usgcb.nist.gov]

  Timestamp:     [2/24/2012]

  Status:        [accepted]

  Status date:   [2/24/2012]

  Title:         [Ohh New BVT for SCAP 1.2]

 Description:   [My description]

  XCCDF Profile: [xccdf\_tst.bvt\_profile\_version\_1.0.0.0]
 
  OVAL:              [Windows-F-oval.xml]

   Product name:    [scaptool]

   Product version: []

   Schema version:  [5.4]

   Timestamp:       [2/24/2012]

  Start SCAP to DCM conversion...

  Processing SCAP data stream: scap\_tst.bvt\_datastream\_Windows-F.zip

  Processing CPE dictionary: scap\_tst.bvt\_comp\_Windows-F-cpe-dictionary.xml

  …

  Generating CI baseline cab file: C:\28\bbt\xccdf\_tst.bvt\_benchmark\_Windows-F[xccdf\_tst.bvt\_profile\_version\_1.0.0.0].cab

  Successfully generated CI baseline cab file: C:\28\bbt\xccdf\_tst.bvt\_benchmark\_Windows-F[xccdf\_tst.bvt\_profile\_version\_1.0.0.0].cab

  Successfully converted XCCDF profile: xccdf\_tst.bvt\_profile\_version\_1.0.0.0 into DCM baseline xccdf\_tst.bvt\_benchmark\_Windows-F[xccdf\_tst.bvt\_profile\_version\_1.0.0.0].cab

## Next step
> [!div class="nextstepaction"]
> [Import SCAP compliance settings and export compliance results](/sccm/compliance/plan-design/scap/import-scap-compliance-settings)
