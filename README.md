# ADB

This is my private cheatsheet for ADB that I have decided to share since there is few good wikis for adb out there that has all in one place, so hopefully someone will enjoy this repo.

I wont include adb shell in any of my commands since I working on the device and not via shell I dont want to include adb shell. For all who prefering to work via a terminal like powershell or terminal just add "adb shell" infront of the commands. 

# Basic

### Start ADB server:

    adb start-server 

### Stop ADB server:

    adb stop-server

### Kill ADB server: 

    adb kill-server

### System reboot

    adb reboot

### Recovery mode

    reboot recovery

### Bootloader mode

    reboot bootloader

### List Connected Devices: 

    adb devices

### Enter ADB shell:

    adb shell

### Enter ADB shell if there is multiple devices connected:

    adb -s <id_from_adb_devices> shell 


### Push a file (Transfer a file FROM pc > device)

    push mypicture.png /storage/on/device

### Push a folder (Transfer a folder FROM pc > device)

    push myfolder /storage/on/device

### Pull a file (Transfer a file FROM device > pc)

    adb pull /storage/on/device/mypicture.png /path/on/pc

### Pull a folder (Transfer a folder FROM device > pc)

    adb pull /storage/on/device /path/on/pc

### Pull all files inside a folder to a path (Transfer all files in a folder FROM device > pc)

    adb pull /storage/on/device/ /path/on/pc # Notice the trial slash
    
    
