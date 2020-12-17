---
# required metadata

title: ExchangePowerShell policy mapping from Basic Mobility and Security to Intune
titleSuffix: Microsoft Intune
description: A detailed list of the policy map between Basic Mobility and Security ExchangePowerShell settings and Intune.
keywords:
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 12/18/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: dagerrit
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: seodec18
ms.collection: M365-identity-device-management
---

# Exchange PowerShell settings mapping from Basic Mobility and Security to Intune

This article provides mapping details between Basic Mobility and Security to Intune. Specifically, this page maps ExchangePowerShell policies to the equivalent policies in Microsoft Endpoint Manager admin center. Because Intune offers more flexibility, each Basic Mobility and Security policy will translate into multiple Intune and Azure Active Directory (Azure AD) policies to achieve the same result.

If you’re migrating from Basic Mobility and Security to Intune, you can use the [Migration evaluation tool](migrate-to-intune.md) to automate much of this mapping.

For information on the Exchange PowerShell script, see [New-DeviceConfigurationRule]( https://docs.microsoft.com/powershell/module/exchange/new-deviceconfigurationrule.md?view=exchange-ps).

## CameraEnabled
For iOS/iPadOS, this setting is only supported on iOS 7.1+ in Basic Mobility and Security.

For Android, this setting is only supported on the following devices in Basic Mobility and Security:
- Samsung Knox
- Android 5 through Android 9

Three configuration policies:
- **Devices** > **Windows** > **Configuration profiles** > profile name > **Properties** > **Configuration settings Edit** > **General** > **Camera**
- **Devices** > **iOS/iPadOS** > **Configuration profiles** > profile name > **Properties** > **Configuration settings Edit** > **Built-in Apps** > **Block camera**
- **Devices** > **Android** > **Configuration profiles** > choose a profile with type **Device administrator** > **Properties** > **Configuration settings Edit** > **General** > **Camera**

## RegionRatings
For iOS/iPadOS, this setting is only supported on iOS 6+ in Basic Mobility and Security.

One configuration profile:
- **Devices** > **iOS/iPadOS** > **Configuration profiles** > profile name > **Properties** > **Configuration settings Edit** > **App Store, Doc Viewing, Gaming** > **Ratings region**

    | Exchange PowerShell setting value |  Ratings region value |
    | --- | --- |
    | $null | Not region configured |
    | au |  Australia |
    | ca |  Canada |
    | de |  Germany |
    | fr |  France |
    | gb |  United Kingdom |
    | ie |  Ireland |
    | jp |  Japan |
    | nz |  New Zealand |
    | us |  United States |

## MoviesRating
For iOS/iPadOS, this setting is only supported on iOS 6+ in Basic Mobility and Security.

The **Ratings region** setting must be set to something other than **Not region configured** to see **Movies**.

One configuration profile:
- **Devices** > **iOS/iPadOS** > **Configuration profiles** > profile name > **Properties** > **Configuration settings Edit** > **App Store, Doc Viewing, Gaming** > **Ratings region** must be set to a region > **Movies**

    | Exchange PowerShell setting value |  Movies value |
    | --- | --- |
    | AllowAll | Allow All Movies |
    | DontAllow | Don’t Allow Movies |
    | $null |  |
    | AURatingG | G |
    | AURatingPG | PG |
    | AURatingM | M |
    | AURatingMA15plus | MA15+ |
    | AURatingR18plus | R18+ |
    | CARatingG | G |
    | CARatingPG | PG |
    | CARating14A | 14A |
    | CARating18A | 18A |
    | CARatingR | R |
    | DERatingab0Jaren | Ab 0 Jahren |
    | DERatingab6Jahren | Ab 6 Jahren |
    | DERatingab12Jahren | Ab 12 Jahren |
    | DERatingab16Jahren | Ab 16 Jahren |
    | DERatingab18Jahren | Ab 18 Jahren |
    | FRRating10minus | 10 |
    | FRRating12minus | 12 |
    | FRRating16minus | 16 |
    | FRRating18minus | 18 |
    | GBRatingU | U |
    | GBRatingUc | UC |
    | GBRatingPG | PG |
    | GBRating12 | 12 |
    | GBRating12A | 12A |
    | GBRating15 | 15 |
    | GBRating18 | 18 |
    | IERatingG | G |
    | IERatingPG | PG |
    | IERating12 | 12 |
    | IERating15 | 15A |
    | IERating16 | 16 |
    | IERating18 | 18 |
    | JPRatingG | G |
    | JPRatingPG12 | PG-12 |
    | JPRatingRdash15 | R15+ |
    | JPRatingRdash18 | R18+ |
    | NZRatingG | G |
    | NZRatingPG | PG |
    | NZRatingM | M |
    | NZRatingR13 | R13 |
    | NZRatingR15 | R15 |
    | NZRatingR16 | R16 |
    | NZRatingR18 | R18 |
    | NZRatingR | 5 |
    | USRatingG | G |
    | USRatingPG | PG |
    | USRatingPG13 | PG13 |
    | USRatingR | R |
    | USRatingNC17 | NC17 |

## TVShowsRating
For iOS/iPadOS, this setting is only supported on iOS 6+ in Basic Mobility and Security.

The **Ratings region** setting must be set to something other than **Not region configured** to see **TV Shows**.

One configuration profile:
- **Devices** > **iOS/iPadOS** > **Configuration profiles** > profile name > **Properties** > **Configuration settings Edit** > **App Store, Doc Viewing, Gaming** > **Ratings region** must be set to a region > **TV Shows**

    | Exchange PowerShell setting value |  TV Shows value |
    | --- | --- |
    | AllowAll | Allow All TV Shows |
    | DontAllow | Don’t Allow TV Shows |
    | $null |  |
    | AURatingP | P |
    | AURatingC | C |
    | AURatingG | G |
    | AURatingPG | PG |
    | AURatingM | M |
    | AURatingMA15plus | MA15++ |
    | AURatingAv15plus | AV15+ |
    | CARatingC | C |
    | CARatingC8 | C8 |
    | CARatingG | G |
    | CARatingPG | PG |
    | CARating14plus | 14+ |
    | CARating18plus | 18+ |
    | DERatingab0Jaren | Ab 0 Jahren |
    | DERatingab6Jahren | Ab 6 Jahren |
    | DERatingab12Jahren | Ab 12 Jahren |
    | DERatingab16Jahren | Ab 16 Jahren |
    | DERatingab18Jahren | Ab 18 Jahren |
    | FRRating10minus | -10 |
    | FRRating12minus | -12 |
    | FRRating16minus | -16 |
    | FRRating18minus | -18 |
    | GBRatingCaution | Caution |
    | IERatingGA | GA |
    | IERatingCh | CH |
    | IERatingYA | YA |
    | IERatingPS | PS |
    | IERatingMA | MA |
    | JPRatingExplicitAllowed | Explicit Allowed |
    | NZRatingG | G |
    | NZRatingPG | PG |
    | NZRatingM | M |
    | NZRatingG | G |
    | NZRatingPGR | PGR |
    | NZRatingAO | AO |
    | USRatingTVY | TV-Y |
    | USRatingTVY7 | TV-Y7 |
    | USRatingTVG | TV-G |
    | USRatingTVPG | TV-PG |
    | USRatingTV14 | TV-14 |
    | USRatingTVMA | TV-MA |

## AppsRating
For iOS/iPadOS, this setting is only supported on iOS 6+ in Basic Mobility and Security.

One configuration profile:
- **Devices** > **iOS/iPadOS** > **Configuration profiles** > profile name > **Properties** > **Configuration settings Edit** > **App Store, Doc Viewing, Gaming** > **Ratings region** must be set to a region > **Apps**

    | Exchange PowerShell setting value |  Apps value |
    | --- | --- |
    | AllowAll | Allow All App |
    | DontAllow | Don’t Allow Apps|
    | $null | Not configured |
    | Rating9Plus | 9+ |
    | Rating12Plus | 12+ |
    | Rating17Plus | 17+ |

## AllowVoiceDialing
For iOS/iPadOS, setting supported on iOS 6+ in Basic Mobility and Security.

Intune doesn’t offer an **Allow** value. Use the **Not configured** instead, which leaves the decision to the end user.

One configuration profile:
- **Devices** > **iOS/iPadOS** > **Configuration profiles** > profile name > **Properties** > **Configuration settings Edit** > **Wireless** > **Block voice dialing while device is locked**

    | Exchange PowerShell setting value |  Block voice dialing while device is locked value |
    | --- | --- |
    | $true | Not configured |
    | $false |  Yes |
    | $null |  Not configured |

## AllowVoiceAssistant
For iOS/iPadOS, this setting is only supported on iOS 6+ in Basic Mobility and Security.

Intune doesn’t offer an **Allow** value. Use the **Not configured** instead, which leaves the decision to the end user.

One configuration policy:
- **Devices** > **iOS/iPadOS** > **Configuration profiles** > profile name > **Properties** > **Configuration settings Edit** > **Built-in Apps** > **Block Siri**

    | Exchange PowerShell setting value |  Block Siri value |
    | --- | --- |
    | $true | Not configured |
    | $false |  Yes |
    | $null |  Not configured |

## AllowAssistantWhileLocked
For iOS/iPadOS, this setting is only supported on iOS 6+ in Basic Mobility and Security.

Intune doesn’t offer an **Allow** value. Use the **Not configured** instead, which leaves the decision to the end user.

One configuration profile:
- **Devices** > **iOS/iPadOS** > **Configuration profiles** > profile name > **Properties** > **Configuration settings Edit** > **Built-in Apps** > **Block Siri while device is locked**

    | Exchange PowerShell setting value |  Block Siri while device is locked value |
    | --- | --- |
    | $true | Not configured |
    | $false |  Yes |
    | $null |  Not configured |

## AllowPassbookWhileLocked
For iOS/iPadOS, this setting is only supported on iOS 6+ in Basic Mobility and Security.

Intune doesn’t offer an **Allow** value. Use the **Not configured** instead, which leaves the decision to the end user.

One configuration profile:
- **Devices** > **iOS/iPadOS** > **Configuration profiles** > profile name > **Properties** > **Configuration settings Edit** > **Locked Screen Experience ** > **Block Wallet notifications in lock screen**

    | Exchange PowerShell setting value |  Block Wallet notifications in lock screen value |
    | --- | --- |
    | $true | Not configured |
    | $false |  Yes |
    | $null |  Not configured |

## MaxPasswordGracePeriod
For iOS/iPadOS, this setting is only supported on iOS 6+ in Basic Mobility and Security.

One configuration profile:
- **Devices** > **iOS/iPadOS** > **Configuration profiles** > profile name > **Properties** > **Configuration settings Edit** > **Password** > **Maximum minutes after screen lock before password is required**

    | Exchange PowerShell setting value |  Maximum minutes after screen lock before password is required value |
    | --- | --- |
    | dd:hh:mm:ss | Not configured |
    | 0 |  Immediately |
    | 1 |  1 Minute |
    | 5 | 5 Minutes |
    | 15 | 15 Minutes |
    | 1 hour | 1 hour|
    | 4+ hours | 4 hours |

## PasswordQuality
For Android, this setting is only supported on Android 4+ in Basic Mobility and Security.

In Intune, 6 is the highest value.

Several password settings shown in Office 365 Security and Compliance portal depend upon this setting have certain minimum values.

One configuration profile:
- **Devices** > **Android** > **Configuration profiles** > profile name > **Properties** > **Configuration settings Edit** > **Password** > **Required password type**

    | Exchange PowerShell setting value |  Required password type value| Description |
    | --- | --- | --- |
    | 0 |  0 | Default, no enforcement |
    | 0 |  0 | Default, no enforcement |
    | 2 |  2 |Low security biometric |
    | 1 |  1 | Any, something. |
    | 3 | 3 |At least numeric, PIN |
    | 7 | 7 |At least numeric complex, no repeating, no ordered pin |
    | 4 | 4 | At least alphabetic, password containing at least one alphabetic/symbol |
    | 5 | 5 | Alphanumeric, password containing at least both numeric and alphabetic/symbol |
    | 6 | 6 | At least alphanumeric with symbols, password containing at least a letter, a numeric, a symbol. |
    | >7 | 6 | At least alphanumeric with symbols, password containing at least a letter, a numeric, a symbol. |

## SystemSecurityTLS
For iOS/iPadOS, this setting is only supported on iOS 6+ in Basic Mobility and Security.

One configuration profile:
- **Devices** > **iOS/iPadOS** > **Configuration profiles** > profile name > **Properties** > **Configuration settings Edit** > **General** > **Block untrusted TLS certificates**

    | Exchange PowerShell setting value |  Block untrusted TLS certificates value |
    | --- | --- |
    | Block | Yes |
    | Not configured | Not configured |

