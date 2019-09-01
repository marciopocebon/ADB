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
     
# DUMPSTATE

### Dump info about your sim provider and kernel bootloader ID etc.

    dumpstate -v

    ========================================================
    == dumpstate: 2019-08-30 19:31:05
    ========================================================

    Build: PPR1.180610.011.G950FXXS5DSF1
    Build fingerprint: 'samsung/dreamltexx/dreamlte:9/PPR1.180610.011/G950FXXS5DSF1:user/release-keys'
    Bootloader: G950FXXS5DSF1
    Radio: G950FXXS5DSF1
    Network: Comviq
    Linux version 4.4.111-16019454 (dpi@21DHA724) (gcc version 4.9.x 20150123 (prerelease) (GCC) ) #1 SMP PREEMPT Mon Jun 3     20:16:50 KST 2019
    Kernel: Command line: (unknown)
    up 0 weeks, 0 days, 16 hours, 21 minutes
    Uptime: Bugreport format version: 2.0
    Dumpstate info: id=0 pid=26940 dry_run=0 args=dumpstate -v extra_options=

     
# AM

### Open settings:

     am start -n com.android.settings/com.android.settings.Settings

### Open activity to new APN

      am start -a android.intent.action.INSERT  content://telephony/carriers  --ei simId 

### Open hiden menu (require root)

    adb shell su -c "am broadcast -a android.provider.Telephony.SECRET_CODE -d android_secret_code://IOTHIDDENMENU"

# Tips & Tricks

### Print uptime for your device by days + time

    TZ=UTC date -d@$(cut -d\  -f1 /proc/uptime) +'%j %T' | awk '{print $1-1"d",$2}'

### Add a contact

## Example 1:

    am start -a android.intent.action.INSERT -t vnd.android.cursor.dir/contact -e name "$(dialog --stdout --inputbox 'wuseman' 0 0)" -e postal "$(dialog --stdout --inputbox 'Postal Address' 0 0)" -e phone "$(dialog --stdout --inputbox 'Phone Number' 0 0)" -e email "$(dialog --stdout --inputbox 'Email' 0 0)"
    
## Example 2: 

    am start -a android.intent.action.INSERT -t vnd.android.cursor.dir/contact -e name 'wuseman' -e phone <phone_number>

### UUSD CODES LG

     *#546368#*870# 
     LG secret codes
*#*#34971539#*#* - This code is used to get information about phone camera. It shows following 4 menus:
* Update camera firmware in image (Don't try this option)
* Update camera firmware in SD card
* Get camera firmware version in LG G6
* Get firmware update count

WARNING: Never use the first option otherwise your phone camera will stop working and you'll need to take LG G6 to service center to reinstall camera firmware.

*#*#7594#*#*

This one is favorite one. This code can be used to change the "End Call / Power" button action in your phone. Be default, if you long press the button, it shows a screen asking you to select any option from Silent mode, Airplane mode and Power off.

You can change this action using this code. You can enable direct power off on this button so you don't need to waste your time in selecting the option.

*#*#225#*#* - Events calendar.

*#*#426#*#* - Debug information for Google Play service.Google Play Services first appeared in 2012. In its initial version, it provided a way to access the Google+ API and OAuth 2.0. From those humble beginnings, it has spread to work with a variety of different Google services, allowing apps to communicate with them. Google Play Services is how other apps can access all the different Google APIs.

*#*#759#*#* - Access Google Partner setup (Rlz debug interface).

*#872564# - USB logging control

*#9900# - System dump mode LG G6

*#*#97#*#* - Language and Keyboard settings in LG G6

*#*#46*#*# - Reset Sim in LG G6

*#301279# - HSDPAHSDPA means “High Speed Downlink Packet Access” and is a technique used in the UMTS mobile communication system, the download speeds of currently 3.6 Mbit/s to 7.2 Mbit/s. HSUPA is developed commercially since 2007 in Germany. High Speed Downlink Packet Access (HSDPA, 3.5G, 3G + or UMTS broadband) is a data transmission method of the cellular standards UMTS, which was defined by the 3rd Generation Partnership Project. The method enables DSL-like data rates in mobile networks. HSDPA is available in Germany, among others by the network operators Vodafone, E-Plus, O2, and telecom and in Switzerland by Swisscom, Sunrise and Orange. In Austria operate the A1, T-Mobile, Orange and Three HSDPA networks./HSUPAHSUPA means “High Speed Uplink Packet Access” and is a technique used in the UMTS mobile communication system, the upload speeds up to 5.8 Mbit/s. High Speed Uplink Packet Access (HSUPA) is a transmission method of the UMTS mobile radio standard that allows higher data rates in the uplink and reduces the round trip time (often referred to as ping). HSUPA Category 6 were up to 5.76 Mbit / s and category 9 (Release 9) up to 23 Mbit / s can be achieved. HSUPA is part of Release 9 of UMTS. Control Menu

*#7465625# - View phone lock status
*7465625*638*Code# = Enables Network lock
#7465625*638*Code# = Disables Network lock
*7465625*782*Code# = Enables Subset lock
#7465625*782*Code# = Disables Subset lock
*7465625*77*Code# = Enables SP lock
#7465625*77*Code# = Disables SP lock
*7465625*27*Code# = Enables CP lock
#7465625*27*Code# = Disables CP lock
*7465625*746*Code# = Enables SIM lock
#7465625*746*Code# = Disables SIM lock
*7465625*228# = Activa lock ON
#7465625*228# = Activa lock OFF
*7465625*28638# = Auto Network lock ON
#7465625*28638# = Auto Network lock OFF
*7465625*28782# = Auto subset lock ON
#7465625*28782# = Auto subset lock OFF
*7465625*2877# = Auto SP lock ON
#7465625*2877# = Auto SP lock OFF
*7465625*2827# = Auto CP lock ON
#7465625*2827# = Auto CP lock OFF
*7465625*28746# = Auto SIM lock ON
#7465625*28746# = Auto SIM lock OFF

*#*#273283*255*663282*#*#* - This code opens a File copy screen where you can backup your media files e.g. Images, Sound, Video and Voice memo.

*#*#197328640#*#* - This code can be used to enter into Service mode. You can run various tests and change settings in the service mode.

 
WLAN, GPS and Bluetooth Test Codes:

*#*#232339#*#* OR *#*#526#*#* OR *#*#528#*#* - WLAN test (Use "Menu" button to start various tests)

*#*#232338#*#* - Shows WiFi MAC address MAC (Media Access Control), address is a globally unique identifier assigned to network devices, and therefore it is often referred to as hardware or physical address. MAC addresses are 6-byte (48-bits) in length, and are written in MM:MM:MM:SS:SS:SS format. The first 3-bytes are ID number of the manufacturer, which is assigned by an Internet standards body. The second 3-bytes are serial number assigned by the manufacturer.

*#*#1472365#*#* - GPSThe Global Positioning System (GPS) is a satellite-based radio navigation system developed and operated by the U.S. Department of Defense. GPS permits land, sea, and airborne users to determine their position, velocity and the time 24 hours a day, in all weather, anywhere in the world. test

*#*#1575#*#* - For a more advanced GPS test

*#*#232331#*#* - Bluetooth test Bluetooth is a wireless technology standard for exchanging data over short distances (using short-wavelength UHF radio waves in the ISM band from 2.4 to 2.485 GHz) from fixed and mobile devices, and building personal area networks (PANs). Invented by telecom vendor Ericsson in 1994, it was originally conceived as a wireless alternative to RS-232 data cables. It can connect several devices, overcoming problems of synchronization.

*#*#232337#*# - Shows Bluetooth device address in LG G6

*#*#8255#*#* - This code can be used to launch GTalk Service Monitor. Gtalk Service Monitor and play services monitor are developer options to let you examine and debug the push connections to google talk and google play services. Below these, the "restore default heartbeats" button lets you bring back the original heartbeat exchange settings if you have to. The final button is about making a donation to the developer of this convenient app. and that is it! now, you are left to experiment with the data and wi-fi settings until you land the most comfortable intervals for you.

*#*#36245#*#* - Access email debug information.

Codes to get Firmware version information:

*#*#4986*2650468#*#* - PDA, Phone, H/W, RFCallDate

*#*#1234#*#* OR *#1234# - PDA and Phone firmware information

*#*#1111#*#* - FTA SW Version (1234 in the same code will give PDA and firmware version)

*#12580*369# - Software and hardware info

*#9090# - Diagnostic configuration in LG G6

*#*#2222#*#* - FTA HW Version

*#*#44336#*#* - PDA, Phone, CSCThe Customer Service Code (CSC) plays an important role in the operation of your mobile device. Different countries have different standards for both voice and data communications to a cell phone tower. Although most countries follow the international standard for WiFi connects, there are variations from the standard. The CSC code ensures that your mobile device complies with the standards for your country, and your cell phone operator. The CSC code also determines the source for firmware updates via FOTA or Samsung Kies., Build Time, Changelist number

Codes to launch various Factory Tests:

*#*#0283#*#* - Packet Loopback

*#*#0*#*#* - LCD display test

*#*#0673#*#* OR *#*#0289#*#* - Melody test

*#*#0842#*#* - Device test (Vibration test and BackLight test)

*#*#2663#*#* - Touch screen version LG G6

*#*#2664#*#* - Touch screen test

*#*#0588#*#* - Proximity sensor test

*#*#3264#*#* - RAM version LG G6

 


GSM codes for LG G6

Change PIN For security, you can require a PIN code in order to use your SIM card in any device. This PIN code follows the SIM card from one device to another. A personal unblocking code (PUC), also known as a PIN unlock key (PUK), is used in 3GPP mobile phones to reset a personal identification number (PIN) that has been lost or forgotten. - ** 04 *, then enter the PIN old, and twice a new PIN.
Change PIN2 - ** 042 *, then enter the old The PIN2, and twice the new PIN2.
Unlock SIM-card (PIN) - ** 05 * then enter the PUK and new PIN twice
Unlock SIM-card (PIN2) - ** 052 *, then enter the PUK2 and new PIN2 twice

Call Forwarding (you have to order the service from the operator)
##002# - Cancel all diverts
##004# - Cancel all conditional call forwarding
**004* phone number # - Activate all conditional call forwarding

Unconditional call forwarding (Call Forward All)
###21 - Switch off and deactivate
#21# - Deactivate
**21*phone number# - Enable and Activate
*21# - Activate
*#21# - Check the condition

Diversion in case of "no answer"
###61 - Switch off and deactivate
#61# - Deactivate
**61* phone number# - Enable and Activate
*61# - Activate
*#61# - Check the condition

Setting the call time until the call forwarding option "no answer"
When installing forwarding on "no answer" you can set the time in seconds that the system allows you to hook. If during this time you have not picked up the phone, the incoming call will be diverted.
Example: - ** 61 * + ** 709576617601234 # 30 - set the waiting time of 30 seconds
Set timeout - ** 61 * Phone Number ** N #, N = 5..30 (seconds)
Remove the previous installation - ## 61 #

Diversion in case of "not available"
# ## 62 - Switch off and deactivate
# 62 # - Deactivate
** 62 *phone number# - Enable and Activate
* 62 # - Activate
* # 62 # - Check the condition

Diversion in case of "busy"
###67 - Switch off and deactivate
#67# - Deactivate
**67*phone number# - Enable and Activate
*67# - Activate
*#67# - Check the condition

Call Barring (you have to order the service from the operator)
Change the password for all bans (default - 0000)
- ** 03 * 330 * old password * new password * new password #




 Barring of all outgoing calls
**33*password# - Activate
#33*password# - Deactivate
*#33# - Check the condition

Barring of all calls
**330*password# - Activate
#330*password# - Deactivate
*#330# - Check the condition

Barring of all outgoing international calls
**331*password# - Activate
#331*password# - Deactivate
*#331# - Check the condition

Barring of all outgoing calls
**333*password# - Activate
#333*password# - Deactivate
*#333# - Check the condition

Barring of all incoming calls
**353*password# - Activate
#353*password# - Deactivate
*#353# - Check the condition

Barring all incoming calls when roaming
**351*password# - Activate
#351*password# - Deactivate
*#351# - Check the condition

Call waiting (you have to order the service from the operator)
*43# - Activate
#43# - Deactivate
*#43# - Check the condition

Transfer your phone number (Anti ANI)
#30#phone number - Block
*30#phone number - Allow
*#30# - Check the condition

Show phone number of the caller you (ANI)
#77# - Block
*77# - Allow
*#77# - Check the condition

Smart menu
GP - *111#
Rob - *140#
Banglalink - *789#
