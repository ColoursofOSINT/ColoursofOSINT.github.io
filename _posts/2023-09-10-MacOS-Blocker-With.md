---
title: MacOS Application Blocker 
date: 2023-09-7 12:00:00 +0800
categories: [Technology, MacOS]
tags: [macos, time-mangement]     # TAG names should always be lowercase
toc: true
math: true
---

# The Problem 
I spend too much time on my Mac on distracting websites and apps. I am also fairly advanced in my knowledge of MacOS applications, their functions and the various methods they use start and stay running, thus I can disable most blockers with ease.

# Cold Turkey Blocker 
Blocks apps and websites.[^1] The only blocker I found that is possible to prevent myself from disabling, with almost complete privacy and a large customization.

# Privacy Impovements
Whenever a page is blocked, the block page loads "getcoldturkey.com/blocked", which provides various page customization functions, but their are (albeit privacy respecting) analytics. To block the block page, edit the hosts file by opening terminal and enter: 

`
sudo nano /private/etc/hosts
`

Enter, 

`
0.0.0.0 getcoldturkey.com
`

Close and save with 'Ctrl + O' then 'enter'.

# Ways to Bypass and Solutions
One can cause it to cease functioning as a result of damaging the application or its supports.

## Removing Contents 
Applications cannot be deleted (moved to the trash) while running, and Cold Turkey restarts immediately after quit. Their contents can be deleted, though. Right select, choose to view contents, delete them and quit the application by opening it, and hiting "Cmd + Q".

Or run the following 

```
sudo rm -i /Applications/Cold Turkey Blocker.app/Contents
```

Then quit the application.

## Removing LaunchAgents
Run the follow scripts as an admin to stop the blocker from restarting after close or at login.
```
rm -i /Users/[yourname]/Library/LaunchAgents/launchkeep.cold-turkey.plist
```
```
sudo rm -i /Library/LaunchAgents/launchkeep.cold-turkey-all-users.plist
```

Then quit coldturkey.

## Remove Databases 
Cold Turkey stores usage information and blocklists at:
`
sudo rm -i/Library/Application Support/Cold Turkey
`

Remove them:
```
sudo rm -ir /Library/Application Support/Cold Turkey
```

# Block 
Make another admin account and run the following as that user:

```
sudo chflags uchg /Library/Application\ Support/Cold\ Turkey
```
```
sudo chflags uchg /Library/LaunchAgents/launchkeep.cold-turkey-all-users.plist
```
```
sudo chflags uchg /Users/[yourname]/Library/LaunchAgents/launchkeep.cold-turkey.plist
```

These files can no longer be removed, without the other Admin's permission.

[^1]: https://getcoldturkey.com/
