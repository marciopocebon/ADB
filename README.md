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

### Setup ADB server via Wi-Fi

    adb tcpip <port>
    
### Connect to ADB server: 

    adb connect <device_ip>

# Restarts the adbd daemon listening on USB

    adb usb
    
### Reboot - Default, system reboot

    adb reboot

### Reboot - Recovery Mode

    reboot recovery

### Reboot - Bootloader Mode

    reboot bootloader

### List Connected Devices: 

    adb devices

### Enter ADB shell:

    adb shell

### Enter ADB shell if there is multiple devices connected:

    adb -s <id_from_adb_devices> shell 

### To print device serial no: 

    adb get-serialno

### Create a bugreport: 

    adb bugreport

### Install an app:

    adb install <apk_file>

### Install an app and keep all it's data from a previous setup: 

    adb install -r <apk_file>

### Uninstall an app: 

    adb uninstall <apk_file>
   
### Set date: 

    date MMDDYYYY.XX;am broadcast -a android.intent.action.TIME_SET

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
    
# ADB package manager

### List all packages installed on device

    pm list packages

### List enabled packages

    pm list packages -e
    
### List disabled packages

    pm list packages -d

### List third party packages installed by user

    pm list packages -3

### List users

    pm list users

### List permission groups

    pm list permission-groups

### List features
 
    pm list features

### Uninstall any installed package:

    pm uninstall --user 0 com.package.name

### Uninstall multiple apps:

    for packages in com.package1 com.package2; do 
        adb shell pm uninstall --user 0 "${packages}"
    done 

### Clear application data:

    pm clear PACKAGE_NAME

### List permission groups: 

    pm list permission-groups 


### List instrumentation:

    pm list instrumentation

### Grant permission to an app (Example Only For Grant): 

    pm grant com.application android.permission.READ_LOGS
    
    
### Revoke permission to an app (Example Only For Revoke): 

    pm revoke com.application android.permission.READ_LOGS

### Reset all permissions for an app:

    pm reset-permissions -p your.app.package
    
# LOGCAT

### Default options: 

* V — Verbose (lowest priority)
* D — Debug
* I — Info (default priority)
* W — Warning
* E — Error
* F — Fatal
* S — Silent (highest priority, on which nothing is ever printed)

### For get output colorized with logcat:

    adb logcat ... -v color

### Displays current log buffer sizes:

    adb logcat -g 	

### Sets the buffer size (K or M):

    adb logcat -G 16M 	

### Clear the log buffer:

    adb logcat -c

### Enables ALL log messages (verbose mode)

    adb logcat *:V 	

### Dump everything to a file:

    adb logcat -f <filename> 	Dumps to specified file

### Display PID with the log info 

    adb logcat -v process

### Display the raw log message, with no other metadata fields

    adb logcat -v raw

### Display the date, invocation time, priority/tag, and PID of the process issuing the message

    adb logcat -v time

#### Display the priority, tag, and the PID and TID of the thread issuing the message

    adb logcat -v thread

### Display the date, invocation time, priority, tag, and the PID and TID of the thread issuing the message

    adb logcat -v threadtime

### Display all metadata fields and separate messages with blank lines

    adb logcat -v long
    
### Log multiple options (-b ... -b ....): 

    adb logcat -b main -b radio -b events

# DUMPSYS

### Dump all data for battery: 

    adb shell dumpsys battery

### Dump stats for your battery:

    adb shell dumpsys batterystats 

### Erase old stats for battery:
 
    dumpsys batterystats --reset 

# Tips And Tricks

# Add a contact

## Example 1:

    am start -a android.intent.action.INSERT -t vnd.android.cursor.dir/contact -e name "$(dialog --stdout --inputbox 'wuseman' 0 0)" -e postal "$(dialog --stdout --inputbox 'Postal Address' 0 0)" -e phone "$(dialog --stdout --inputbox 'Phone Number' 0 0)" -e email "$(dialog --stdout --inputbox 'Email' 0 0)"
    
## Example 2: 

    am start -a android.intent.action.INSERT -t vnd.android.cursor.dir/contact -e name 'wuseman' -e phone <phone_number>



