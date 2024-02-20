---
description: Learn how to use the LoadPDF method to import a specified package definition file into the package definition file store.
title: LoadPDF Method
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 37670a60-5ee3-4fc4-b9b3-6c44e6858201
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# LoadPDF Method in Class SMS_PDF_Package
The `LoadPDF` Windows Management Instrumentation (WMI) class method, in Configuration Manager, imports a specified package definition file into the package definition file store.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 LoadPDF(  
     String PDFFileName,  
     String PDFFile,  
     UInt32 PDFID,  
     String RequiredIconNames[]  
);  
```  

#### Parameters  
 `PDFFileName`  
 Data type: `String`  

 Qualifiers: [in,SizeLimit("100")]  

 Full path and file name of the package definition file. The SMS Provider copies the file to the \Smsinstalldir\Scripts\\<localeid\>\Pdfstore\\<pdfid\> directory and replaces the .pdf file name extension with an .sms file name extension.  

 `PDFFile`  
 Data type: `String`  

 Qualifiers: [in]  

 Text of the package definition file itself.  

 `PDFID`  
 Data type: `UInt32`  

 Qualifiers: [out]  

 Assigned package definition file ID.  

 `RequiredIconNames`  
 Data type: `String` Array  

 Qualifiers: [out]  

 List of icons referenced by the package definition file that must be loaded separately through the [LoadIconForPDF Method in Class SMS_PDF_Package](../../../../../develop/reference/core/servers/configure/loadiconforpdf-method-in-class-sms_pdf_package.md) method.  

## Return Values  
 An `SInt32` data type that indicates 0 for success or one of the following bit field warning flags for failure.  

|Flag|Description|  
|----------|-----------------|  
|WARN_BAD_RUN (0)|Invalid run information specified.|  
|WARN_BAD_RESTART (1)|Invalid restart information specified.|  
|WARN_BAD_CANRUNWHEN (2)|Invalid CanRunWhen information specified.|  
|WARN_BAD_ASSIGNMENT (3)|Invalid assignment information specified.|  
|WARN_BAD_DEPENDPROG (4)|Invalid DependentProgram information specified.|  
|WARN_BAD_SPECIFYDRIVE (5)|Invalid SpecifyDrive information specified.|  
|WARN_BAD_ESTDISKSPACE (6)|Invalid EstimatedDiskSpace information specified.|  
|WARN_NO_SUPPCLINFO (7)|No SupportedClients information specified.|  
|WARN_BAD_SUPPCLINFO (8)|Invalid SupportedClients information specified.|  
|WARN_VER1PDF (9)|Version 1.0 file used.|  
|WARN_REMPRONOUKEY(10)|The remove program is set but no uninstall key is given.|  

## Remarks  
 When your application imports a package definition file that has the same `Name`, `Publisher`, `Version`, and `Language` properties as an existing package definition file, the existing package definition file is overwritten, including the file icons and programs. The value specified in the `PDFID` parameter is retained.  

## Example Code  
 The following example shows how to load a package definition file into the package definition file package store.  

```  
Const ForReading = 1  

Dim fs, f                         ' File system object and file object.  
Dim clsPDF As SWbemObject         ' SMS_PDF_Package class definition.  
Dim ReturnCode As Long            ' Return code value from LoadPDF method.  
Dim PDFID As Long                 ' Package definition file identifier generated from LoadPDF.  
Dim PDFContent As String          ' Package definition file file content.  
Dim ReqIconNames() As Variant     ' Required icon names from LoadPDF.  
Dim Icon() As Byte                ' Icon used as input to LoadIconForPDF method.  
Dim i, j As Integer  
Dim FileSize As Integer           ' Size of the icon file.  

Set Services = GetObject("winmgmts:\root\sms\<sitecode>")  

' Open the package definition file file and read the content into a string.  
Set fs = CreateObject("Scripting.FileSystemObject")  
Set f = fs.OpenTextFile(<path\filename>, ForReading)  
PDFContent = f.ReadAll  
f.Close  

' Load the package definition file into the package definition file store. Use the PDFID and ReqIconNames   
' Variables in the LoadIconForPDF method.  
Set clsPDF = Services.Get("SMS_PDF_Package")  
ReturnCode = clsPDF.LoadPDF(<path\filename>, _  
                            PDFContent, _  
                            PDFID, _  
                            ReqIconNames)  

' You must load all the icons for the package definition file if the package definition file contains icons.  
For i = LBound(ReqIconNames) To UBound(ReqIconNames)  
    Open <path> & ReqIconNames(i) For Binary Access Read As #1  
    FileSize = LOF(1) - 1  
    ReDim Icon(FileSize)  
    For j = 0 To FileSize  
        Get #1, , Icon(j)  
    Next  
    Close #1  

    clsPDF.LoadIconForPDF PDFID, ReqIconNames(i), Icon  
Next  
```  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_PDF_Package Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_pdf_package-server-wmi-class.md)
