---
title: "How to sync iPhone calendar with gnome-calendar"
date: 2022-09-22
---

If you are a Linux user and you own iPhone,
you might know,
how hard it can be to integrate Apple's proprietary services with open-source ones.
Luckily there is an easy way how to synchronize the iCloud calendar with gnome-calendar because Apple is using the CalDAV standard.
You could use NextCloud to host your CalDAV server, but for the sake of simplicity, we will use iCloud calendar.
The system I am running is Fedora 37 Beta with Gnome 43 and iPhone 8 with iOS 15.7.

## Edit: 2025-06-16
Evolution is no longer needed therefore **Step 2** and **Step 3** are marked as deprecated.

*Credit to the rad dude Matt.*

## Step 1: Generate an App-specific password
App-specific passwords are used to connect to your iCloud services.
They are visible for a limited time and can be revoked at any time.
To obtain an app-specific password you need to log into Apple ID
(You can use this [link](https://appleid.apple.com/account/manage)).
Go to `Sign-In and Security` -> `App-specific passwords`
and click *plus sign* button to create a new password.

## NEW Step 2: Add a calendar
To add a new calendar go to `Settings` -> `Online Accounts` -> `Calendar, Contacts and Files (WebDav)`.

Fill the form with values:
|Key|Value|
|-|-|
|Server Address|https://caldav.icloud.com|
|Username|email address for the appleID|
|Password|the app-specific password you created|

After that you hit the Sign In button and you are good to go.

## DEPRECATED Step 2: Make sure you have Evolution installed
To add a CalDAV account to gnome-calendar you need to have Evolution installed
(If you know any other easier way, how to add CalDAV accounts to gnome-calendar, please let me know).

To install Evolution on Fedora use `dnf install evolution` or for Debian-based distros use `apt-get install evolution`.

## DEPRECATED Step 3: Add a calendar account in Evolution
Open Evolution and go to `File` -> `New` -> `Calendar`

Fill the form:
| Key | Value |
|---|---|
| Type | CalDAV |
| Name | leave blank, will be filled automatically |
| Colour | leave blank, will be filled automatically |
| URL | https://caldav.icloud.com |
| User | your Apple ID email |
| Email | leave blank, will be filled automatically |
| Server handles meeting invitations | True |

and click *Find callendars* button.
You will be asked for password.
Enter the app-specific password you obtained earlier and select the calendar you wish to add.

## Done
Well done, you just synchronized your iCloud calendar with gnome-calendar.
