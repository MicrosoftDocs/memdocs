---
# required metadata

title: Configure Microsoft Launcher for Android Enterprise with Intune 
titleSuffix: 
description: Use Intune configuration policies with Microsoft Launcher. 
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 02/26/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: priyar
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Configure Microsoft Launcher

Microsoft Launcher is an Android application that lets users personalize their phone, stay organized on the go, and transfer from working from their phone to their PC. 

On Android Enterprise fully managed devices, Launcher allows enterprise IT admins to customize managed device home screens by selecting the wallpaper, apps, and icon positions. This standardizes the look and feel of all managed Android devices across different OEM devices and system versions. 

## How to configure the Microsoft Launcher app 

Navigate to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and select **Apps** > **App configuration policies**. Add a configuration policy for **Managed devices** running **Android** and choose **Microsoft Launcher** as the associated app. Click on **Configuration settings** to configure the different available Microsoft Launcher settings. 

## Choosing a Configuration Settings Format 

There are two methods that you can use to define configuration settings for Microsoft Launcher: 

- **Configuration designer** allows you to configure settings with an easy-to-use UI that lets you toggle features on or off and set values. In this method, there are a few disabled configuration keys with value type BundleArray. These configuration keys can only be configured by entering JSON data. 

- **JSON data** allows you to define all possible configuration keys using a JSON script. 

If you add properties with **Configuration Designer**, you can automatically convert these properties to JSON by selecting **Enter JSON data** from the **Configuration settings format** dropdown list as shown below.

   ![Configuration settings format - Use configuration designer](./media/configure-microsoft-launcher/configure-microsoft-launcher-01.png)

## Using Configuration Designer

Configuration designer allows you to select pre-populated settings and their associated values.

   ![Configuration settings format - Enter JSON data](./media/configure-microsoft-launcher/configure-microsoft-launcher-02.png)

The following table lists the Microsoft Launcher available configuration keys, value types, default values, and descriptions. The description provides the expected device behavior based on the selected values. Configuration keys that are disabled in Configuration Designer are not listed in the table.

|    Configuration Key    |    Value type    |    Default value    |    Description     |
|---------------------------------------------------|------------------|---------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    Enrollment Type    |    String     |    Default    |    Allows you to set   the enrollment type this policy should apply to. Currently, the value **Default** refers to **CorporateOwnedBuisnessOnly**. There are no other supported   enrollment types at present.        JSON key name: management_mode_key        |
|    Home Screen App Order User Change   Allowed    |    Boolean    |    True    |    Allows you to specify if the **Home Screen App Order** setting can be changed by the end user.<ul><li>If set to **True**, the app order defined in the policy will only be enforced for the initial deployment. Subsequently, the policy will not be enforced to respect any changes the user may have made.</li><li>If set to **False**, the app order will be enforced on every sync.</li></ul><br>**Note:** The Home Screen App order can only be configured via the JSON editor.<br><br>JSON key name:<br>`com.microsoft.launcher.HomeScreen.AppOrder.UserChangeAllowed`    |
|    Set Grid Size    |    String    |    Auto    |    Allows you to   set the grid size for apps to be positioned on the home screen. You can set   the number of app rows and columns to define grid size in the following format: `columns;rows`. If you   define the grid size, the maximum number of apps that will be shown in a row   on the home screen would be the number of rows you set and the maximum number   of apps that will be shown in a column in the home screen would be the number   of columns you set.<br><br>        JSON key name:<br>`com.microsoft.launcher.HomeScreen.GridSize`    |
|    Set Device Wallpaper    |    String    |    Null    |    Allows you to set a wallpaper of your choice by   entering the URL of the image that you want to set as a wallpaper.<br><br>JSON key name:<br>`com.microsoft.launcher.Wallpaper.URL`    |
|    Set Device Wallpaper User Change   Allowed    |    Bool    |    True    |    Allows you to specify if the Set Device   Wallpaper setting can be changed by the end user.<ul><li>If set to **True**, the wallpaper in the policy will only be enforced for the initial deployment. Subsequently, the policy will not be enforced to respect any changes the user may have made.</li><li>If set to **False**, the wallpaper will be enforced on every sync.</li></ul><br>JSON key name:<br>`com.microsoft.launcher.Wallpaper.URL.UserChangeAllowed`        |
|    Feed Enable    |    Boolean    |    True    |    Allows you to enable the launcher feed on the device when the user swipes to the right on the home screen.<ul><li>If set to **True**, the feed will be enabled.</li><li>If set to **False**, the feed will be disabled.</li></ul><br>JSON key name:<br>`com.microsoft.launcher.Feed.Enabled`    |
|    Feed Enable User Change Allowed    |    Boolean    |    True    |     Allows you to specify if the **Feed Enable** setting can be changed by the end user.<ul><li>If set to **True**, the feed will only be enforced for the initial deployment. Subsequently, the policy will not be enforced to respect any changes the user may have made.</li><li>If set to **False**, the feed will be enforced on every sync.</li></ul><br>JSON key name:`com.microsoft.launcher.Feed.Enabled.UserChangeAllowed`    |

## Enter JSON Data

Enter JSON data to configure all available settings for Microsoft Launcher, as well as the settings disabled in **Configuration Designer**, as shown below.

   ![Configuration Designer - JSON data](./media/configure-microsoft-launcher/configure-microsoft-launcher-03.png)

In addition to the list of configurable settings listed in the Configuration Designer table (above), the following table provides the configuration keys you can only configure via JSON data.

|    Configuration Key    |    Value type    |    Default value    |    Description     |
|----------------------------------------------------------------------------------------------------|-------------------|-------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    Set Allow-Listed Applications<br>JSON key:`com.microsoft.launcher.HomeScreen.Applications`    |    BundleArray    | See: [Set allow-listed applications](configure-microsoft-launcher.md#set-allow-listed-applications)</sup>    |    Allows you to  define the set of apps visible on the home screen from amongst the apps   installed on the device. You can define the apps by entering the app package   name of the apps that you would like to make visible, for example, `com.android.settings` would make settings accessible on the home screen. The   apps that you allow-list in this section should already be installed on the   device in order to be visible on the home screen.<p>Properties:<ul><li>**Package:** The application package name</li><li>**Class:** The application activity, which is specific to a certain app page. It would use the default app page if this value is empty.</li></ul>      |
|    Home Screen App Order<br>JSON key: `com.microsoft.launcher.HomeScreen.AppOrder`    |    BundleArray    |    See: [Home screen app order](configure-microsoft-launcher.md#home-screen-app-order)      |    Allows you to specify the app order on the home screen.<p>Properties:<br><ul><li>**Type:** The only type supported is `application`.</li><li>**Position:** The application icon slot on home screen. This starts from position 1 on the top left, and goes left to right, top to bottom.</li><li>**Package:** The application package name.</li><li>**Class:** The application activity, which is specific to a certain app page. The default app page will be used if this value is empty.</li></ul>    |

### Set allow-listed applications

```JSON
{
    "key": "com.microsoft.launcher.HomeScreen.Applications",
    "valueBundleArray": 
    [
        {
            "managedProperty": [
                {
                    "key": "package",
                    "valueString": ""
                },
                {
                    "key": "class",
                    "valueString": ""
                }
            ]
        }
    ]
}
```

### Home screen app order

```JSON
{
    "key": "com.microsoft.launcher.HomeScreen.AppOrder",
    "valueBundleArray": 
    [
        {
            "managedProperty": [
                {
                    "key": "type",
                    "valueString": "application"
                },
                {
                    "key": "position",
                    "valueInteger": 0
                },
                {
                    "key": "package",
                    "valueString": ""
                },
                {
                    "key": "class",
                    "valueString": ""
                }
            ]
        }
    ]
}
```

The following is an example JSON script with all the available configuration keys included:

```JSON
{
    "kind": "androidenterprise#managedConfiguration", 
    "productId": "app:com.microsoft.launcher", 
    "managedProperty": [
        {
            "key": "management_mode_key", 
            "valueString": "Default"
        }, 
        {
            "key": "com.microsoft.launcher.Feed.Enable.UserChangeAllowed", 
            "valueBool": false
        }, 
        {
            "key": "com.microsoft.launcher.Feed.Enable", 
            "valueBool": true
        }, 
        {
            "key": "com.microsoft.launcher.Wallpaper.Url.UserChangeAllowed", 
            "valueBool": false
        }, 
        {
            "key": "com.microsoft.launcher.Wallpaper.Url", 
            "valueBool": "http://www.contoso.com/wallpaper.png"
        }, 
        {
            "key": "com.microsoft.launcher.HomeScreen.GridSize", 
            "valueString": "5;5"
        }, 
        {
            "key": "com.microsoft.launcher.HomeScreen.Applications", 
            "valueBundleArray": [
                {
                    "managedProperty": [
                        {
                            "key": "package", 
                            "valueString": "com.ups.mobile.android"
                        }, 
                        {
                            "key": "class", 
                            "valueString": ""
                        }
                    ]
                }, 
                {
                    "managedProperty": [
                        {
                            "key": "package", 
                            "valueString": "com.microsoft.teams"
                        }, 
                        {
                            "key": "class", 
                            "valueString": ""
                        }
                    ]
                }, 
                {
                    "managedProperty": [
                        {
                            "key": "package", 
                            "valueString": "com.microsoft.bing"
                        }, 
                        {
                            "key": "class", 
                            "valueString": ""
                        }
                    ]
                }
            ]
        }, 
        {
            "key": "com.microsoft.launcher.HomeScreen.AppOrder.UserChangeAllowed", 
            "valueBool": false
        }, 
        {
            "key": "com.microsoft.launcher.HomeScreen.AppOrder", 
            "valueBundleArray": [
                {
                    "managedProperty": [
                        {
                            "key": "type", 
                            "valueString": "application"
                        }, 
                        {
                            "key": "position", 
                            "valueInteger": 17
                        }, 
                        {
                            "key": "package", 
                            "valueString": "com.ups.mobile.android"
                        }, 
                        {
                            "key": "class", 
                            "valueString": ""
                        }
                    ]
                }, 
                {
                    "managedProperty": [
                        {
                            "key": "type", 
                            "valueString": "application"
                        }, 
                        {
                            "key": "position", 
                            "valueInteger": 18
                        }, 
                        {
                            "key": "package", 
                            "valueString": "com.microsoft.teams"
                        }, 
                        {
                            "key": "class", 
                            "valueString": ""
                        }
                    ]
                }, 
                {
                    "managedProperty": [
                        {
                            "key": "type", 
                            "valueString": "application"
                        }, 
                        {
                            "key": "position", 
                            "valueInteger": 19
                        }, 
                        {
                            "key": "package", 
                            "valueString": "com.microsoft.bing"
                        }, 
                        {
                            "key": "class", 
                            "valueString": ""
                        }
                    ]
                }
            ]
        }
    ]
}
```

## Next steps

- For more information about Android Enterprise fully managed devices, see [Set up Intune enrollment of Android Enterprise fully manage devices](../enrollment/android-fully-managed-enroll.md).
