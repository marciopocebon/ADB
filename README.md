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

### List all active services:

    dumpsys -l |sed 's/^  /      /g'
    Currently running services:
      AAS
      AODManagerService
      CCM
      CocktailBarService
      CodecSolution
      CustomFrequencyManagerService
      DeviceRootKeyService
      DirEncryptService
      DisplaySolution
      DockObserver
      EngineeringModeService
      HqmManagerService
      ImsBase
      OcfKeyService
      ReactiveService
      SEAMService
      SamsungKeyProvisioningManagerService
      SatsService
      SecExternalDisplayService
      SemAuthnrService
      SemMLDAPService
      SemService
      SurfaceFlinger
      SveService
      VaultKeeperService
      accessibility
      account
      activity
      alarm
      android.security.keystore
      application_policy
      appops
      appwidget
      audio
      autofill
      backup
      barbeam
      battery
      batteryproperties
      batterystats
      binder_calls_stats
      bluetooth_manager
      bluetooth_secure_mode_manager
      carrier_config
      cepproxyks
      clipboard
      com.samsung.android.bio.face.IFaceDaemon
      com.samsung.android.camera.iris.IIrisDaemon
      com.samsung.ucs.ucsservice
      commontime_management
      companiondevice
      connectivity
      connmetrics
      consumer_ir
      content
      context_aware
      contexthub
      country_detector
      cover
      cpuinfo
      crossprofileapps
      dbinfo
      desktopmode
      device_identifiers
      device_policy
      deviceidle
      devicestoragemonitor
      diskstats
      display
      dreams
      drm.drmManager
      dropbox
      dsms
      dual_app
      edge
      edm_proxy
      edmnativehelper
      emailksproxy
      enterprise_license_policy
      enterprise_policy
      epdgService
      ethernet
      fingerprint
      freecess.binder.IFrozenBinder
      freecess.packet.IFreecessPacket
      gamemanager
      gamesdk
      gfxinfo
      gpu
      graphicsstats
      gsmaapi
      hardware_properties
      harmony_eas_service
      iccc
      imms
      ims6
      input
      input_method
      iphonesubinfo
      ipsec
      isms
      isub
      jobscheduler
      knox_ccm_policy
      knox_securetimer
      knox_timakeystore_policy
      knox_ucsm_policy
      knox_vpn_policy
      knoxcustom
      knoxguard_service
      launcherapps
      location
      lock_settings
      log_manager_service
      mDNIe
      mate_service
      mdc_service
      mdm.remotedesktop
      media.audio_flinger
      media.audio_policy
      media.camera
      media.camera.proxy
      media.drm
      media.extractor
      media.mediacapture
      media.metrics
      media.player
      media.remotedisplay
      media.resource_manager
      media.smartfitting_manager
      media.sound_trigger_hw
      media_projection
      media_resource_monitor
      media_router
      media_session
      meminfo
      midi
      mobile_payment
      motion_recognition
      mount
      mpos
      multidisplay
      multiwindow
      mum_container_policy
      mum_container_rcp_policy
      netd_listener
      netpolicy
      netstats
      network_management
      network_score
      network_time_update_service
      network_watchlist
      nfc
      notification
      oem_lock
      otadexopt
      overlay
      package
      package_native
      permission
      permission.monitor
      persistent_data_block
      persona
      persona_policy
      phone
      phone_restriction_policy
      pinner
      power
      print
      processinfo
      procstats
      rcp
      recovery
      remoteinjection
      restriction_policy
      restrictions
      saccessory_manager
      samsung.smartfaceservice
      sb_service
      scheduling_policy
      scontext
      sdhms
      sdp
      sdp_log
      search
      sec_key_att_app_id_provider
      sec_location
      secims
      secure_element
      sedenial
      semclipboard
      sensorservice
      sepunion
      serial
      servicediscovery
      settings
      shortcut
      simphonebook
      sip
      slice
      soundtrigger
      spengestureservice
      stats
      statscompanion
      statusbar
      storaged
      storaged_pri
      storagestats
      system_update
      telecom
      telephony.registry
      textclassification
      textservices
      thermalservice
      tima
      timezone
      trust
      uimode
      updatelock
      urspservice
      usagestats
      usb
      user
      vibrator
      virtualspace
      voiceinteraction
      voip
      vr
      vrmanager
      wallpaper
      webviewupdate
      wifi
      wifi_policy
      wificond
      wifip2p
      wifiscanner
      window

## Examples:

### Show bluetooth macaddr, bluetooth name and such things:

    dumpsys bluetooth_manager

### List all settngs and if they are true or false:

Settings are sorted for root and user:

     GLOBAL SETTINGS (user 0)
     SECURE SETTINGS (user 0)
     SYSTEM SETTINGS (user 0)
     SECURE SETTINGS (user 95)
     SYSTEM SETTINGS (user 95)


    dumpsys settings
    _id:225 name:lock_screen_show_notifications pkg:com.android.settings value:1 default:1 defaultSystemSet:true
    _id:6 name:volume_bluetooth_sco pkg:android value:7 default:7 defaultSystemSet:true
    _id:192 name:ringtone_set pkg:com.google.android.gsf value:1
    _id:159 name:lock_screen_allow_rotation pkg:android value:0 default:0 defaultSystemSet:true
    _id:2997 name:Flashlight_brightness_level pkg:com.android.systemui value:1001 default:1001 defaultSystemSet:true
    _id:67 name:SEM_VIBRATION_NOTIFICATION_INTENSITY pkg:android value:5 default:5 defaultSystemSet:true
    _id:175 name:call_popup pkg:android value:0 default:0 defaultSystemSet:true
    _id:59 name:install_non_market_apps pkg:android value:1 default:1 defaultSystemSet:true
    .....

### Display Contacts On Sim Card:

    dumpsys simphonebook

### Show hardware info as thermal stuff for cpu, gpu and battery

     dumpsys hardware_properties
    ****** Dump of HardwarePropertiesManagerService ******
    CPU temperatures: [38.0, 38.0]
    CPU throttling temperatures: [55.0, 76.0]
    CPU shutdown temperatures: [115.0, 115.0]
   
### Show all application you have an account on: 

    dumpsys account|grep -i com.*$ -o|cut -d' ' -f1|cut -d} -f1|grep -v com$
    com.microsoft.workaccount
    com.skype.raider
    com.samsung.android.mobileservice
    com.facebook.messenger
    com.google.android.gm.exchange
    .......
    
### Show all notifications listener and so on:

    dumpsys notification
    
### List email addresses registerd on different stuff on device:

    dumpsys | grep -E -o "\b[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,6}\b"
    
### Check state for screen and figoure how device was unlcked last time:

    dumpsys  user
    ...
    State: RUNNING_UNLOCKED
    ...
    Last logged in fingerprint
    .....
    agree Knox Privacy Policy: false
    
### And for example, you can dump data for all of the running services: 
### Dump all data for battery: 

    adb shell dumpsys battery

### Dump stats for your battery:

    adb shell dumpsys batterystats 

### Erase old stats for battery:
 
    dumpsys batterystats --reset 

### Sort Applications By Ram Usage:

     dumpsys meminfo

    Applications Memory Usage (in Kilobytes):
    Uptime: 29602806 Realtime: 57806941

    Total PSS by process:
    265,435K: com.android.systemui (pid 4190)
    264,671K: system (pid 3838)
    171,192K: surfaceflinger (pid 3360)
    152,523K: android.hardware.graphics.composer@2.1-service (pid 3338)
    128,781K: com.sec.android.app.launcher (pid 5597 / activities)
     92,656K: se.kronansapotek.kronan (pid 26729 / activities)
     84,563K: logd (pid 3203)
     80,944K: com.google.android.talk (pid 32314 / activities)
     79,754K: com.google.android.googlequicksearchbox:search 
     
     
     
     
# Tips & Tricks

### Print uptime for your device by days + time

    TZ=UTC date -d@$(cut -d\  -f1 /proc/uptime) +'%j %T' | awk '{print $1-1"d",$2}'

### Add a contact

## Example 1:

    am start -a android.intent.action.INSERT -t vnd.android.cursor.dir/contact -e name "$(dialog --stdout --inputbox 'wuseman' 0 0)" -e postal "$(dialog --stdout --inputbox 'Postal Address' 0 0)" -e phone "$(dialog --stdout --inputbox 'Phone Number' 0 0)" -e email "$(dialog --stdout --inputbox 'Email' 0 0)"
    
## Example 2: 

    am start -a android.intent.action.INSERT -t vnd.android.cursor.dir/contact -e name 'wuseman' -e phone <phone_number>



