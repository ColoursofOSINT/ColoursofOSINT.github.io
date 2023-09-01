---
title: MacOS Privacy Preserving Automatic Bluetooth Shutoff
date: 2023-08-31 12:00:00 +0800
categories: [MacOS]
tags: [macos, privacy, bluetooth]     # TAG names should always be lowercase
toc: true
---

# Bluetooth Exposure

Bluetooth is useful for quick connections to other devices, whether for file sharing, audio, or imput control. However, because Bluetooth beacons emit a uniquely identifiable signal, they can be used for short range tracking[^Footnote-1]. For example, a mall might track the movement of its patrons as they move through stores. This technology was used for COVID tracking, and although it may be useful for some, it's also a privacy risk. 

# Apple Devices

Apple devices are more vulerable to this type of tracking as they have stonger broadcasts and even manually turning off Bluetooth does not shut off beaconing[^Footnote-2]. Some Android phones also allow users to automaticaly shut of bluetooth after an ajustable time spent disconnected. 

# Mac OS Goals

In order to shut off bluetooth on a Mac after 15 mins of disconnection, the follow format may be used. 

![Dark View](https://raw.githubusercontent.com/ColoursofOSINT/ColoursofOSINT.github.io/master/assets/img/images/Bluetooth.png){: .dark }
![Light View](https://raw.githubusercontent.com/ColoursofOSINT/ColoursofOSINT.github.io/master/assets/img/images/Bluetooth.drawio.png){: .light }
_Code Planning for Shutoff_

# Mac OS Script
```bash

#!/bin/bash

# Check if Bluetooth is powered on
if blueutil --power | grep -q '1'; then
    echo "Bluetooth is turned on."

    # Check if there are connected devices
    if blueutil --connected | grep -q '.'; then
        echo "Bluetooth devices are connected."
    else
        echo "No Bluetooth devices are connected."
        sleep 5  # Wait for 15 minutes
        
        # Check for connected devices again
        if blueutil --connected | grep -q '.'; then
            echo "Bluetooth devices are now connected. Bluetooth will not be turned off."
        else
            # Turn off Bluetooth
            blueutil --power 0
            echo "Bluetooth has been turned off."
        fi
    fi

else
    echo "Bluetooth is turned off."
fi

```
{: .nolineno }

# Mac OS Scheduling 
> LaunchAgents can also be for the scheduling of bluetooth shutoff.
{: .prompt-info }

To run every 30 minutes using crontab, run: 

```
crontab -e
```
Then to activate the file every 30 minutes, schedule the following:

```
30 * * * * /path/to/file
```

To exit and save the cron editor, press 'esc', then ':', then 'w' and then 'q'. Hit 'enter' or 'return' and check that the crontab is running with:


```
crontab -l
```

The response should be: 

```
30 * * * * /path/to/file
```

[^Footnote-1]: https://www.theregister.com/2021/10/22/bluetooth_tracking_device/
[^Footnote-2]: https://www.tomsguide.com/news/bluetooth-device-tracking
