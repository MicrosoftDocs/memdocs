---
# required metadata

title: Incomplete user enrollments report in Intune
titleSuffix: Microsoft Intune
description: Learn about the Incomplete user enrollments report.
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 2/22/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: 
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
---

# Incomplete user enrollments report

This report tells you where in the Company Portal enrollment process users are not completing the enrollment process.

To see the report, choose **Intune** > **Device enrollment** > **Incomplete user enrollments**.

Using this information, you can update your onboarding documents to help users complete enrollment. For example, if many users are quitting at the Terms of Use, you might investigate that area and make it more intuitive for users.

## What is an incomplete enrollment?

An incomplete enrollment is when a user does any of the following:

- Explicitly chooses an action to halt enrollment
- Closes the Company Portal during enrollment
- Spends more than 30 minutes between enrollment sections

If a user chooses to stop enrollment and restart multiple times, it shows up as multiple attempts and multiple incomplete enrollments. If a user waits for 30 minutes between different enrollment screens, it is considered multiple incomplete enrollments.

## What does the report show?

The reports include data for iOS/iPadOS and Android devices.

The reports show data for the past two weeks, but you can filter the report to show any period up to 30 days in the past.

You can filter the date range, operating system, and enrollment section by choosing **Filter**.

### Number and percentage tiles

At the top of the report, you can see the number and percentage of incomplete enrollments in relation to all enrollments.

- Initiated enrollments: The number of enrollments attempted.
- Incomplete enrollments: The number of attempted enrollments that didn't result in a fully enrolled and compliant device.
- Incomplete rate: The percentage of enrollment attempts that were abandoned (Abandoned enrollments / Initiated enrollments).

### Line graph

The line graph shows the daily incomplete enrollments for each of the four core enrollment sections:

- Setup checklist
- Platform screens
- Terms of use
- Compliance/Activation

### User abandonment actions

The following tables show the list of user actions that qualify as prompting an incomplete enrollment. To see examples of enrollment screens, you can watch the [iOS](https://channel9.msdn.com/Series/IntuneEnrollment/iOS-Enrollment) and [Android](https://channel9.msdn.com/Series/IntuneEnrollment/Android-Enrollment) enrollment videos. 


#### Setup checklist section

| Action name | Screen or flow | Platform | Action |
| ---- |---- |---- |---- |
| EnrollmentWrapUp | Prompt to open page in Company Portal | iOS/Android | **Cancel** |
| EnrollmentWrapUp | Enrolling device screen until finish of **Loading company resources** | iOS/Android | Took > 30 minutes |
| DeviceCategory | Device Category selection (if admin configured) until click **Done** | iOS/Android | Took > 30 minutes |
| PreEnrollmentWizard | Set up access screen when having started enrollment but returned to Set up access | iOS/Android| **Postpone** |
| PreEnrollmentWizard | Set up access screen until clicking **Next** on the **What's Next** screen | iOS/Android | Took > 30 minutes |

#### Platform screens section

| Action name | Screen or flow | Platform | Action |
| ---- |---- |---- |---- |
| iOSProfileLaunch | Prompt to show a configuration profile | iOS/iPadOS | **Ignore** |
| iOSProfileLaunch | Installing profile screen | iOS/iPadOS | **Cancel** |
| iOSProfileLaunch | Prompt to trust the profile's source to enroll the device | iOS/iPadOS | **Cancel** |
| iOSProfileLaunch | Install profile screen until profile is installed | iOS/iPadOS | Took > 30 minutes |
| AndroidPermissions | Device administrator activation screen | Android | **Cancel** |
| AndroidPermissions | From prompt for approval to make and manage phone calls until device administrator **Activate** | Android | Took > 30 minutes |
| KnoxActivation | KLMS agent activation (Samsung only) | Android| **Cancel** |
| KnoxActivation | KLMS agent activation until **Confirm** | Android | Took > 30 minutes|

#### Terms of use section

| Action name | Screen or flow | Platform | Action |
| ---- |---- |---- |---- |
| TermsofUse | Terms of use (if admin configured) | iOS/Android | **Decline All** |
| TermsofUse | Terms of use until **Accept all** | iOS/Android | Took > 30 minutes |

#### Compliance/Activation section

| Action name | Screen or flow | Platform | Action |
| ---- |---- |---- |---- |
| Compliance | Device compliance (if admin configured) shows as non-green on access setup post enrollment| iOS/Android | **Postpone** |
| Compliance | Device compliance shows as non-green until updated to show green | iOS/Android | Took > 30 minutes |
| Activation | Enrollment activation  (if admin configured) shows as non-green on access setup | iOS/Android | **Postpone** |
| Compliance | Device activation shows as non-green until updated to show green | iOS/Android | Took > 30 minutes |

## Next steps

After checking on your incomplete enrollment rates, you can review the [enrollment options](enrollment-options.md) to see if you can make any changes to improve enrollment.
