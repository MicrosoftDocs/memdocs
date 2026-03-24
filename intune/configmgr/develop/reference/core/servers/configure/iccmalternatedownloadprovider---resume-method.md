---
title: "ICcmAlternateDownloadProvider : Resume"
description: "The ICcmAlternateDownloadProvider::Resume method instructs the provider to resume a given job."
ms.date: 07/25/2017
ms.subservice: sdk
ms.topic: reference
ms.collection: tier3
---
# ICcmAlternateDownloadProvider : Resume Method
The **ICcmAlternateDownloadProvider::Resume** method, in Configuration Manager, instructs the provider to resume a given job.

## Syntax

```
HRESULT Resume(
            REFGUID JobID
    );

```

#### Parameters
 `JobID`
 Data type: `REFGUID`

 Qualifiers: [in]

 The job on which to take action.

## Remarks

> [!NOTE]
>  The provider must support Resume being called on a job that is not suspended. In that case, it should simply do nothing and not report an error. An error should be returned if the job is not found or if resuming failed.

## Return Values
 An `HRESULT` code. Possible values include, but aren't limited to, the following one:

 S_OK
 Success implies that discovery was triggered successfully. All other return values indicate failure.

## Requirements

## Runtime Requirements
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).

## Development Requirements
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).
