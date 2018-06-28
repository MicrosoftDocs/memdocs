---
title: Deploy and monitor SCAP compliance
titleSuffix: Configuration Manager
description: Deploy the SCAP compliance settings as configuration baselines, monitor compliance, and export the results.
ms.date: 07/13/2018
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 0bdcb018-bac2-4540-b786-6242bac73ff4
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Deploy and monitor SCAP compliance in Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

After you have [converted and imported](/sccm/compliance/plan-design/scap/install-configure-scap#bkmk_convert-and-import) the SCAP data stream files, see the following next steps:  

- [Deploy](#bkmk_deploy) the configuration baselines to collections to assess devices for SCAP compliance  

- [Monitor](#bkmk_monitor) the compliance data returned from the targeted clients  

- [Export](#bkmk_export) the compliance results to SCAP format  



## <a name="bkmk_deploy"></a> Deploy SCAP configuration baselines

First create the device collections for the computers that you want to assess for SCAP compliance. For more information, see [Create collections](/sccm/core/clients/manage/collections/create-collections).  

Now you're ready to deploy the configuration baselines that you imported to these device collections. For more information, see [How to deploy configuration baselines](/sccm/compliance/deploy-use/deploy-configuration-baselines).  

> [!Tip]  
> Repeat this process for each configuration baseline that you want to deploy to each device collection. At a minimum, deploy each configuration baseline to at least one device collection.



## <a name="bkmk_monitor"></a> Monitor the SCAP compliance data 

Before exporting the compliance data back to SCAP format, you need to verify that the site has collected the data. After you deploy a configuration baseline to a device collection, the Configuration Manager client on each computer in the collection automatically gathers the compliance information. Then the compliance information is stored in the Configuration Manager database.

View the status of the configuration baseline deployment in Configuration Manager to ensure that the appropriate data has been collected by the Configuration Manager clients. It's important to verify that the appropriate compliance data has been collected in Configuration Manager because it can help you validate the XCCDF/DataStream results files that you create later in the process.

For more information, see [Monitor compliance settings](/sccm/compliance/deploy-use/monitor-compliance-settings).


### Validate the XCCDF/Datastream results

1. In the Configuration Manager console, go to the **Assets and Compliance** workspace, expand **Compliance Settings**, and select the **SCAP Dashboard**.  

2. Select the configuration baseline, Assignment, SCAP File, Datastream, Benchmark, and Profile (if applicable).  

3. Click **Show Report**
 ![Example SCAP report](./media/scap-report.png)



## <a name="bkmk_export"></a> Export compliance results to SCAP format

The next step in the process is to export the compliance data to SCAP format, which is an ARF report file in XML/human-readable format. The SCAP Extensions Export wizard and Microsoft.Sces.DcmToScap.exe command-line tool export a separate XCCDF/DataStreamARF results file for each configuration baseline. These files correspond to each XCCDF/DataStream input file that the Microsoft.Sces.ScapToDcm.exe tool uses to create each configuration baseline.


### Manually export with the console wizard

> [!Note]  
> This section describes the manual process to export the compliance results with the Configuration Manager console. To automate this process, see the next section to [Automatically export with the command-line tool](#bkmk_auto-export).  


1. Start the **Export SCAP Report** wizard by right-clicking the **SCAP Dashboard** node.  
![Start the Export SCAP Report wizard from SCAP Dashboard](./media/import-from-scap-dashboard.png)

2. Select the Configuration Baseline, Assignment, and SCAP Content Type.  
![Select baseline](./media/select-ci-baseline.png)

3. Choose the location of the SCAP datastream file, XCCDF/CPE file, or Oval content and variable files.  
![Choose datastream](./media/export-scap-report-datastream.png)

4. Specify the organization name, and choose the folder location to export the SCAP report.  
 ![Choose datastream](./media/specify-org-export.png)
   > [!Tip]  
   > This page of the wizard displays the command line you would use with the **DcmToScap.exe** tool to automate the same process.  

5. Confirm the settings.  
 ![Choose datastream](./media/confirm-export.png)

6. Choose **Next** to export the report. Complete the wizard.  
 ![Complete the export](./media/complete-report-export.png)


### <a name="bkmk_auto-export"></a> Automatically export with the command-line tool

Open the command prompt, and go to the Configuration Manager **AdminConsole\Bin** folder. Use one of the following command-line examples:  

> [!NOTE]  
> Your account must have read permissions for the Configuration Manager provider. You also need write permissions for the folder specified in the `–out` parameter of the command line.

**For SCAP 1.0/1.1 content (such as USGCB and DISA content):**  

`Microsoft.Sces.DcmToScap.exe -baseline BaselineCIID -assignment AssignmentID –xccdf <xccdf.xml> -cpe <cpe.xml>  -select <xccdfBenchmark/profile> -out <outputResultFolder> [-log logFileName]`  

  > [!NOTE]  
  > If there are multiple benchmark/profile in the content, use the `–select` parameter to specify the benchmark/profile which has been evaluated on the clients.  

**For SCAP1.2 content (such as the latest USGCB content):**  

`Microsoft.Sces.DcmToScap.exe -baseline BaselineCIID -assignment AssignmentID -select <datastream/xccdfBenchmark/profile> -out <outputResultFolder> [-log logFileName]`  

   > [!NOTE]  
   > If there are multiple datastream/benchmark/profile in the content, use the `–select` parameter to specify the datastream/benchmark/profile which has been evaluated on the clients.  

**For single OVAL file with external variables:**  

`Microsoft.Sces.DcmToScap.exe -baseline BaselineCIID -assignment AssignmentID –oval <singleOvalFile.xml> [-variable <externalVariableFile.xml>] -out <outputResultFolder> [-log logFileName]`  

   > [!NOTE]  
   > The Microsoft.Sces.DcmToScap.exe only generates OVAL definition results report for each target machine. The ARF report isn't generated.  


#### How to get the BaselineCIID and AssignmentID

In the Configuration Manager console, go to the **Assets and Compliance** workspace, expand **Compliance Settings**, and select **Configuration Baselines**. The `BaselineCIID` is the identifier (ID) for the configuration baseline.  
![Get the CI ID and Assignment ID](./media/get-to-baselines.png)

Select the desired configuration baseline, and click the **Deployments** tab. The `AssignmentID` is the identifier (ID) for the configuration baseline deployment to a device collection. If the Assignment ID isn't displayed, right-click the column header, and select **Assignment ID**.  
![Get the CI ID and Assignment ID](./media/get-to-baselines.png)


#### Microsoft.Sces.DcmToScap.exe command-line parameters

| Parameter | Usage | Required |
| --- | --- | --- |
| `-baseline [Baseline CI ID]` | Specify the Configuration Baseline | Yes |
| `-assignment [Assignment ID]` | Specify the Configuration Baseline deployment | Yes |
| `-organization [organization name]` | Specify the organization name, which would be displayed in report. It can be separated by `;` to specify a multi-line organization name. | No |
| `-type [thin/full/fullnosc]` | Specify the OVAL result type: thin result, or full result, or full result without system characteristic. | No (if not specified, then the default value is full) |
| `-scap [scap data stream file]` | Specify the SCAP data stream file | Yes (for SCAP 1.2 data stream, mutually exclusive with –xccdf and –oval / -variable) |
| `-xccdf [xccdf file]` | Specify the XCCDF file | Yes (for SCAP 1.0/1.1 XCCDF, mutually exclusive with –scap and –oval / -variable) |
| `-cpe [cpe file]` | Specify the CPE file | Yes (for SCAP 1.0/1.1 XCCDF, mutually exclusive with –scap and –oval / -variable) |
| `-oval [oval file]` | Specify the OVAL file | Yes (for standalone OVAL file, mutually exclusive with –xccdf and -scap) |
| `-variable [oval external variable file]` | Specify the OVAL external variable file | No (Optional for standalone OVAL file when there's an external OVAL variable file, mutually exclusive with –xccdf and -scap) |
| `-select [xccdf benchmark/profile]` | Select XCCDF benchmark, profile from either the SCAP data stream or XCCDF file | Yes (a selection must be made to generate a report so that you can match the corresponding DCM baseline in Configuration Manager database |
| `-out [output directory]` | Specify where to output the Compliance Settings cab file | No (if not specified, then the tool would only list the content without conversion) |
| `-log [log file]` | Specify the log file | No (if not specified, then log is written to Microsoft.Sces.DcmToScap.log file) |
| `-help` or `-?` | Print out tool usage | No |

 > [!TIP]  
 > You can specify the `-?`, `–h`, or `–help` parameter to display the syntax of the Microsoft.Sces.DcmToScap.exe tool and a list of the parameters.

By default, the Microsoft.Sces.DcmToScap.exe tool accesses the Configuration Manager database using your credentials. The Microsoft.Sces.DcmToScap.exe tool requires a minimum of read access to the Configuration Manager database.

After running the tool, verify that the following files exist: 
- **ARF** report: `_ARF_xxxx.xml_` and/or **Human-readable** report: `xxx.txt`
- **Cyberscope** report: `LASR_xxx.xml`
- **ConsumedOval** report: `xx-oval-<machineName>.xml`
- **XCCDF Benchmark result** report: `xccdf_xxx.xml` 



## Next step
> [!div class="nextstepaction"]
> [Troubleshooting](/sccm/compliance/plan-design/scap/troubleshooting-scap)
