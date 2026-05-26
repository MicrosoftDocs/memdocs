---
description: "Learn how to cancel a job in Configuration Manager using ICcmAlternateDownloadProvider::CancelJob method."
title: "ICcmAlternateDownloadProvider : CancelJob"
ms.date: 07/25/2017
ms.subservice: sdk
ms.topic: reference
ms.collection: tier3
---
# ICcmAlternateDownloadProvider : CancelJob Method
The **ICcmAlternateDownloadProvider::CancelJob** method, in Configuration Manager, cancels a job.

> [!NOTE]
>  An error should be returned if the job is not found or if cancellation failed.

## Syntax

```
HRESULT CancelJob(
            REFGUID JobID
    );

```

#### Parameters
 `JobID`
 Data type: `REFGUID`

 Qualifiers: [in]

 The job upon which to take action.

## Return Values
 An `HRESULT` code. Possible values include, but aren't limited to, the following one:

 S_OK
 Success implies that discovery was triggered successfully. All other return values indicate failure.

## Requirements

## Runtime Requirements
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).

## Development Requirements
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).
