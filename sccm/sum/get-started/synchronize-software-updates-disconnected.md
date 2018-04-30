---
title: "Synchronize updates with no Internet connection "
titleSuffix: "Configuration Manager"
description: "Run software updates synchronization on the top-level software update point that is disconnected from the Internet."
author: aczechowski
ms.date: 01/23/2017
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 1a997c30-8e71-4be5-89ee-41efb2c8d199
manager: dougeby
ms.author: aaroncz
---

# Synchronize software updates from a disconnected software update point  *Applies to: System Center Configuration Manager (Current Branch)*
 When the software update point at the top-level site is disconnected from the Internet, you must use the export and import functions of the WSUSUtil tool to synchronize software updates metadata. You can choose an existing WSUS server not in your Configuration Manager hierarchy as the synchronization source. This topic provides information about how to use the export and import functions of the WSUSUtil tool.  

 To export and import software updates metadata, you must export software updates metadata from the WSUS database on a specified export server, then copy the locally stored license terms files to the disconnected software update point, and then import the software updates metadata to the WSUS database on the disconnected software update point.  

 Use the following table to identify the export server in which to export the software updates metadata.  

|Software update point|Upstream update source for connected software update points|Export server for a disconnected software update point|  
|---------------------------|-----------------------------------------------------------------|------------------------------------------------------------|  
|Central administration site|Microsoft Update (Internet)<br /><br /> Existing WSUS server|Choose a WSUS server that is synchronized with Microsoft Update by using the software update classifications, products, and languages that you need in your Configuration Manager environment.|  
|Stand-alone primary site|Microsoft Update (Internet)<br /><br /> Existing WSUS server|Choose a WSUS server that is synchronized with Microsoft Update by using the software update classifications, products, and languages that you need in your Configuration Manager environment.|  

 Before you start the export process, verify that software updates synchronization is completed on the selected export server to ensure that the most recent software updates metadata is synchronized. To verify that software updates synchronization has completed successfully, use the following procedure.  

#### To verify that software updates synchronization has completed successfully on the export server  

1.  Open the WSUS Administration console and connect to the WSUS database on the export server.  

2.  In the WSUS Administration console, click **Synchronizations**. A list of the software updates synchronization attempts are displayed in the results pane.  

3.  In the results pane, find the latest software updates synchronization attempt and verify that it completed successfully.  

> [!IMPORTANT]  
>  The WSUSUtil tool must be run locally on the export server to export the software updates metadata, and it also must be run on the disconnected software update point server to import the software updates metadata. In addition, the user that runs the WSUSUtil tool must be a member of the local Administrators group on each server.  

## Export process for software updates  
 The export process for software updates consists of two main steps: to copy the locally stored license terms files to the disconnected software update point, and to export software updates metadata from the WSUS database on the export server.  

 Use the following procedure to copy the local license terms metadata to the disconnected software update point.  

#### To copy local files from the export server to the disconnected software update point server  

1.  On the export server, navigate to the folder where software updates and the license terms for software updates are stored. By default, the WSUS server stores the files at <*WSUSInstallationDrive*>\WSUS\WSUSContent\\, where *WSUSInstallationDrive* is the drive on which WSUS is installed.  

2.  Copy all files and folders from this location to the WSUSContent folder on the disconnected software update point server.  

 Use the following procedure to export the software updates metadata from the WSUS database on the export server.  

#### To export software updates metadata from the WSUS database on the export server  

1.  At the command prompt on the export server, navigate to the folder that contains WSUSutil.exe. By default, the tool is located at %*ProgramFiles*%\Update Services\Tools. For example, if the tool is located in the default location, type **cd %ProgramFiles%\Update Services\Tools**.  

2.  Type the following to export the software updates metadata to a package file:  

     **wsusutil.exe export**  *packagename*  *logfile*  

     For example:  

     **wsusutil.exe export export.cab export.log**  

     The format can be summarized as follows: WSUSutil.exe is followed by the export option, the name of the export .cab file that is created during the export operation, and the name of a log file. WSUSutil.exe exports the metadata from the export server and creates a log file of the operation.  

    > [!NOTE]  
    >  The package (.cab file) and the log file name must be unique in the current folder.  

3.  Move the export package to the folder that contains WSUSutil.exe on the import WSUS server.  

    > [!NOTE]  
    >  If you move the package to this folder, the import experience can be easier. You can move the package to any location that is accessible to the import server, and then specify the location when you run WSUSutil.exe.  

## Import software updates metadata  
 Use the following procedure to import software updates metadata from the export server to the disconnected software update point.  

> [!IMPORTANT]  
>  Never import any exported data from a source that you do not trust. If you import content from a source that you do not trust, it might compromise the security of your WSUS server.  

#### To import metadata to the database of the import server  

1.  At the command prompt on the import WSUS server, navigate to the folder that contains WSUSutil.exe. By default, the tool is located at %*ProgramFiles*%\Update Services\Tools.  

2.  Type the following:  

     **wsusutil.exe import**  *packagename*  *logfile*  

     For example:  

     **wsusutil.exe import export.cab import.log**  

     The format can be summarized as follows: WSUSutil.exe is followed by the import command, the name of package file (.cab) that is created during the export operation, the path to the package file if it is in a different folder, and the name of a log file. WSUSutil.exe imports the metadata from the export server and creates a log file of the operation.  

## Next steps
After you synchronize software updates for the first time, or after there are new classifications or products available, you must [configure the new classifications and products](configure-classifications-and-products.md) to synchronize software updates with the new criteria.

After you syncrhonize software updates with the criteria that you need, [manage settings for software updates](manage-settings-for-software-updates.md).  
