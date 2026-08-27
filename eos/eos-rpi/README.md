# Embedded operating systems for raspberry pi eos-rpi

Exploring operating systems to use in embedded environments for single board computers SBC's.

See also
* Real time operrationg systems rtos [GH](https://github.com/YorkEarwaker/Operating-System/tree/main/rtos), for microcontroller MCU's 

## Notes

Objectives
* Observations on use of a number of operating systems from different groups with raspberry pi embedded systems
* In the first instance concentrating on those which might be used for the AGW project

## Status
TODO
* <todo: consider, collate informaton re os for rpi usage attemtps here, start with tasks matrix markup table>
* <todo: consider, move os install notes from /rpi-z directory in /een repo to this location to simplify /een/rpi-z README.md page >
* <todo: consider, icloud confiiguration, specific to rpi os Trixi + >

DONE
* <done: consider, intent to commit>
* <done: consider, best practice with multiple sd card swap for rpi sbc instance, see link Tips&Tricks Ubunti community in enable ssh sub heading below,  >

## Output - OS install and confiiguration
Consider breakout different OS attempts to different pages 

OS listing - 2026.08.27
| OS Name                 | Micro SD Card | Architecture | SSH alias  | SSH Ubuntu One |
| :---------              | :----------:  | :----------: | :--------- | :---------- |
| RPi OS Trixie Lite      |    64 GB      |     64 bit   | yes        | na          |
| Ubuntu Server 24.04 LTS |    64 GB      |     64 bit   | yes        | na          |


### RPi OS Trixi Lite - install
* <todo: get the entry from sucessful previous attempt >

### RPi OS Trixi Lite -  cli config
Assumuptions 
* minimal config for initial OS install
* headless setup, even with an OS with a desktop
* OpenSSL uid/pwd were set in initial minimal install setup
* UART config set in intial minimal install setup

Wifi
* Status: Success! :)
* 2026.08.12 
* Open a serial screen sesson and log on to raspberry pi sbc, this example uses rpi z2w using a serial bridge chip to uart connection device
```
$ sudo screen /dev/ttyUSB0 115200
```
* In terminal window after logon
* Start the raspi-config command line interface
```
$ sudo raspi-config
```
* A menu option selection is presented see below
* select the `5 Localisation options` menu item
```
Raspberry Pi Zero 2 W Rev 1.0, 512MB


┌─────────┤ Raspberry Pi Software Configuration Tool (raspi-config) ├──────────┐
│                                                                              │
│       1 System Options       Configure system settings                       │
│       2 Display Options      Configure display settings                      │
│       3 Interface Options    Configure connections to peripherals            │
│       4 Performance Options  Configure performance settings                  │
│       5 Localisation Options Configure language and regional settings        │
│       6 Advanced Options     Configure advanced settings                     │
│       8 Update               Update this tool to the latest version          │
│       9 About raspi-config   Information about this configuration tool       │
│                                                                              │
│                                                                              │
│                                                                              │
│                                                                              │
│                                                                              │
│                     <Select>                     <Finish>                    │
│                                                                              │
└──────────────────────────────────────────────────────────────────────────────┘
```
* select the `L4 WLAN Country` menu item
```
┌─────────┤ Raspberry Pi Software Configuration Tool (raspi-config) ├──────────┐
│                                                                              │
│         L1 Locale       Configure language and regional settings             │
│         L2 Timezone     Configure time zone                                  │
│         L3 Keyboard     Set keyboard layout to match your keyboard           │
│         L4 WLAN Country Set legal wireless channels for your country         │
│                                                                              │
│                                                                              │
│                                                                              │
│                                                                              │
│                                                                              │
│                                                                              │
│                                                                              │
│                                                                              │
│                                                                              │
│                     <Select>                     <Back>                      │
│                                                                              │
└──────────────────────────────────────────────────────────────────────────────┘
```
* Select the relevant country from the scroll down menu using arrow keys
* Select the `<Ok>` button using Tab key
* Press Enter/Return to confirm country selection choice
```
          ┌──────────────────────────────────────────────────────────┐
          │ Select the country in which the Pi is to be used         │
          │                                                          │
          │                FI Finland               ↑                │
          │                FM Micronesia            ▒                │
          │                FR France                ▒                │
          │                GB Britain (UK)          ▮                │
          │                GD Grenada               ▒                │
          │                GE Georgia               ▒                │
          │                GF French Guiana         ▒                │
          │                GH Ghana                 ▒                │
          │                GL Greenland             ▒                │
          │                GP Guadeloupe            ↓                │
          │                                                          │
          │                                                          │
          │                                                          │
          │                                                          │
          │              <Ok>                  <Cancel>              │
          │                                                          │
          └──────────────────────────────────────────────────────────┘
```
* You are asked to confirm your country selection
* The `<Ok>` button is preselected and highlighted
* Press Enter/Return to confirm country selection choice
```
          ┌──────────────────────────────────────────────────────────┐
          │                                                          │
          │ Wireless LAN country set to GB                           │
          │                                                          │
          │                                                          │
          │                                                          │
          │                                                          │
          │                                                          │
          │                                                          │
          │                                                          │
          │                                                          │
          │                                                          │
          │                                                          │
          │                                                          │
          │                                                          │
          │                                                          │
          │                                                          │
          │                          <Ok>                            │
          │                                                          │
          └──────────────────────────────────────────────────────────┘
```
* returns you to the raspi-config main menu presented above
* select `<Back>` button followed by the `<Finished>` button to close the raspi-config cli tool
* Run the following command to check WiFi is `enabled`
* Using the NetworkManager Command Line Interface tool` nmcli`
```
$ nmcli radio wifi                                  
enabled
```
* If `diabled` was returned run the following command
```
$ nmcli radio wifi on
```
* View available networks to connect to
* Some example output for the cli `$ nmcli dev wifi list` (generated by Brave ai)
```
$ nmcli dev wifi list
IN-USE  BSSID              SSID                 MODE   CHAN  RATE        SIGNAL  BARS    SECURITY
        24:A4:3C:9E:D2:84  An-Example           Infra  1     195 Mbit/s  100     ▂▄▆█    WPA2
        6C:14:6E:E5:35:F4  Home_Network_5G      Infra  149   405 Mbit/s  92      ▂▄▆█    WPA2
        C8:3A:35:58:B2:60  Office_WiFi          Infra  6     270 Mbit/s  75      ▂▄▆_    WPA2 802.1X
        6C:14:6E:E5:35:F0  Guest_Network        Infra  8     130 Mbit/s  58      ▂▄▆_    WPA2
        D8:32:14:46:81:E8  Neighbor_A           Infra  6     270 Mbit/s  42      ▂▄__    WPA1 WPA2
        F0:2F:A7:CC:69:40  Free_Public_WiFi     Infra  11    65 Mbit/s   28      ▂___    WPA2
        06:1F:5C:FE:AA:DF  Hidden_AP            Infra  1     54 Mbit/s   15      ▂___    --   

```
* Note. You can sort the wifi network output above by issuing the following command `$ nmcli dev wifi list | awk 'NR>1' | sort -k 7 -n -r` replacing the `7` with the column to sort by
* Select a wireless network
* Identify the SSID name `<an-example-ssid>` as the WiFi network to connect to
* Use the following command to connect to the WiFi network `$ sudo nmcli --ask dev wifi connect <an-example-ssid>`
* Replacing `<an_example-ssid>` with the SSID of the wanted WiFi network
* Enter the raspberry pi user password for sudo permission
* Enter the wireless password/key psk of the WiFi router
```
$ sudo nmcli --ask dev wifi connect An-Example
[sudo] password for york-earwaker:  
Push of the WPS button on the router or a password is required to access the wireless network 'An-Example'
Password (802-11-wireless-security.psk): ••••••••••••••••
Device 'wlan0' successfully activated with 'a1900bed-baa9-47a3-affb-b640d0effe5d'.
```
* After successful logon to WiFi network the UUID for that session is returned, the very long alpha-numeric-uuid above
* Run the following command and an * asterisk will appear next the the WiFi network the raspberry pi is connected to
```
$ nmcli dev wifi list
IN-USE  BSSID              SSID        MODE   CHAN  RATE        SIGNAL  BARS  SECURITY 
*       24:A4:3C:9E:D2:84  An-Example  Infra  1     195 Mbit/s  78      ▂▄▆_  WPA2
```

### Enable ssh
* <todo: consider, example via command line interface>
* <note; minimal config example already has use of empty ssh file in /bootfs? partition, install process section likely needs to be moved from /een/rpi-z to here above for cmopleteness >
* SSH login to single board computer with fixed ip address via many OS’s flashed to many micro sd cards [WS](https://discourse.ubuntu.com/t/ssh-login-to-single-board-computer-with-fixed-ip-address-via-many-oss-flashed-to-many-micro-sd-cards/86683)
* use of ~/.ssh/config as described in link above.

```
tbd dummy entry in config file example
```

### Login via ssh
* Status; Success! :) 
* <note; consider, returned error suspected man in the middle attack, WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED! >
* <todo: add success with ~/.ssh/config entry method below >
* After successful Wifi connection of raspberry pi sbc to a WiFi network, as this is the only network connection for the rpi z2w, ignoring special case of usb cable 

To logon via ssh
* Determine the raspberry pi network IP Address
* Use the WiFi admin console to identify the RPi IP Address
* Useing the screen terminal connection to the raspberry pi run
* Which will return ip4 address and ip6 address ... not shown below
```
$ hostname -I
192.168.1.15 ...
```
* Or from you host machine, the one using to connect to the raspberry pi
* Open a terminal window and run `nmap -sn 192.168.1.0/24` replacing the subnet mask an necessary 
* This will return devices on the local network
```
$ nmap -sn 192.168.1.0/24
Starting Nmap 7.94 ( https://nmap.org ) at 2026-08-13 11:30 EDT
Warning: You are not root -- using TCP pingscan rather than ICMP
Nmap scan report for 192.168.1.1
Host is up (0.0032s latency).

Nmap scan report for 192.168.1.15
Host is up (0.015s latency).

Nmap scan report for 192.168.1.20
Host is up (0.0051s latency).

Nmap done: 256 IP addresses (3 hosts up) scanned in 3.45 seconds
```
* Logon via ssh
```
$ ssh raspberrypi@192.168.1.15
```
* Status; Faulure, partial message returned.
* Likely cause new micro sd card with new rpi os install
* <todo: consider, use as example and find work around>
```
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@    WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!     @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
IT IS POSSIBLE THAT SOMEONE IS DOING SOMETHING NASTY!
Someone could be eavesdropping on you right now (man-in-the-middle attack)!
It is also possible that a host key has just been changed.
The fingerprint for the ...
...
Host key for 192.168.1.216 has changed and you have requested strict checking.
Host key verification failed.
```

### Ubuntu Server 24 install 
Status: Success! :)
* Rationale for this is to have second OS for AGW project to acomplish dual compliation on for RPi OS and one for Ubuntu Server 24 OS
* Find deltas in compilation process from successful deployment and test

Write Ubuntu Server 24 to micro SD card
* Put the micro SD card into a micro SD card adapter and insert adapter into host machine
* Open the disk imager Raspberry Pi Imager 2.0.10.x
* Select the RPi device type to flash drive for
```
Device
Raspberry Pi Zero 2 W
```
* Next
* Get preinstalled file previously downloaded manually
* Downloaded 5 August 2026 from Ubuntu web site
```
OS>Use Custom
ubuntu-24.04.4-preinstalled-server-arm64+raspi.img.xz
```
* Next
* Select your storage device
* tick exclude system drives to avoid accidentally overwriting the hosts hd/ssd 
* A micro SD adapter with 64 GB micro SD in this instance
* The micro SD can be smaller 32 GB or less, look at the RPi docs web site for micro SD card sizing guidance
* Click on the SD card shown to select it for flashing
```
Storage
Exclude system drives
Internal SD card reader (Verbatim SD)
58.2 GB
Mounted as /media/york-earwaker/Verbatim SD
```
* Next
* In this instance the customization menu option was not selected
```
Customization
```
* Write the image to the SD card selected
```
Write image
Review your choices and write image to the storage device

Summary
Device             Raspberry Pi Zero 2 W
Operating system   ubuntu-24.04.4-preinstalled-server-arm64+raspi.img.xz
Storage            Internal SD card reader (Verbatim SD)
```
* WRITE
* Pop up appears, two buttons Cancel and ...
* Select the button 'I UNDERSTAND, ERASE AND WRITE'
```
You are about to ERASE all data on: Internal SD card reader (Verbatim SD)
This action is permanent and cannot be undone
```
* Writing image screen is shown
* With a cancel write button, selecting this will cancel the write but the micro sd card has already been erased.
```
Writing image
Writing in progress - do not disconnect the storage device

                    Writing... 28%
===========-----------------------------------------

```
* Writing image
* Verification after writing
```
Writing image
Writing in progress - do not disconnect the storage device

                    Verifying... 37%
==================-----------------------------------
           Verifying written data (51.1 MB's)
```
* Done
* Select the finish button
```
Writing complete!

Your choices
Device             Raspberry Pi Zero 2 W
Operating system   ubuntu-24.04.4-preinstalled-server-arm64+raspi.img.xz
Storage            Internal SD card reader (Verbatim SD)

The storage device was ejected automatically. You can now remove it safely.
```
* Finish
* After pressing finish the Raspberry Pi Imager closes automatically
* There are now two sd card disk images available
* On Ubuntu Desktop they appear in the left hand side panel
* Remove the micro SD adapter from the host device
* Remove the micro sd card from the adapter and insert the micro SD card into the Raspberry Pi Zero 2 W and power on the RPi Z2W. Alternatively if you are using a micro sd card adapter extension cable with the Raspberry Pi Zero 2 W - highly recommended - put the micro sd adapter still containing the micro sd care into the extension cable and power on the RPi Z2W.

Log into Ubuntu Server 24 instance over serial bridge connection to Raspberry Pi Zero 2 W
* Status: tbd
* Assumtption the Raspberry Pi Zero 2 W is connected to the host machine via a serial bridge chip device.
* The serial bridge chip device is using UART xyz GPIO pins to connect to the Raspberry Pi Zero 2 W
* The serial bridge chip device is plugged into USB A port on the host machine

First log on
* Open a cli terminal on the host machine
* Make a serial screen connection from the local host to the Raspberry Pi Zero 2 W

Open a terminal window 
* ensure the serial board chip device is connected
```
$ lsusb
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 001 Device 002: ID 0cf3:e300 Qualcomm Atheros Communications QCA61x4 Bluetooth 4.0
Bus 001 Device 003: ID 138a:0091 Validity Sensors, Inc. VFS7552 Touch Fingerprint Sensor
Bus 001 Device 004: ID 04f3:24a1 Elan Microelectronics Corp. Touchscreen
Bus 001 Device 005: ID 0c45:6713 Microdia Integrated_Webcam_HD
Bus 001 Device 006: ID 10c4:ea60 Silicon Labs CP210x UART Bridge
Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
```
* Retrieve port to use for serial connection
```
$ sudo dmesg | grep -i tty
[sudo] password for <your-user-name>: 
[    0.010264] ACPI: SSDT 0x000000007855AE40 00050D (v02 INTEL  TbtTypeC 00000000 INTL 20160422)
[    0.167761] printk: legacy console [tty0] enabled
[   18.666544] Bluetooth: RFCOMM TTY layer initialized
[ 6902.300476] usb 1-2: cp210x converter now attached to ttyUSB0
```
* in another separate terminal window
* open a serial screen session up with the Raspberry Pi Zero 2 W
```
$ sudo screen /dev/ttyUSB0 115200
```
* use default Ubuntu username: ubuntu and default password: ubuntu
* the system will prompt to change the uid and pwd the first time the Ubuntu Server 24 instance is logged into
* in a screen session the initial screen is entirely empty, enter the user name ubuntu, then the password prompt appears enter the password ubuntu
* the following exchange was after an initial user id password authentiction error.
```
Authentication token manipulation error

Ubuntu 24.04.4 LTS ubuntu ttyS0

ubuntu login: ubuntu
Password: 
You are required to change your password immediately (administrator enforced).
Changing password for ubuntu.
Current password: 
New password: 
Retype new password: 
Welcome to Ubuntu 24.04.4 LTS (GNU/Linux 6.8.0-1047-raspi aarch64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/pro

 System information as of Tue Feb 10 03:24:06 UTC 2026

  System load:  0.12              Swap usage:  0%       Users logged in: 0
  Usage of /:   3.8% of 56.75GB   Temperature: 43.5 C
  Memory usage: 43%               Processes:   126

The list of available updates is more than a week old.
To check for new updates run: sudo apt update


The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.

To run a command as administrator (user "root"), use "sudo <command>".
See "man sudo_root" for details.

ubuntu@ubuntu:~$ 
```
* Ubuntu 24.04 LTS is now sucessfully running on the Raspberry Pi Zero 2 W.

Create user
* Good practice not to sign in as system root
```
ubuntu@ubuntu:~$ sudo adduser citizen-developer
info: Adding user `citizen-developer' ...
info: Selecting UID/GID from range 1000 to 59999 ...
info: Adding new group `citizen-developer' (1001) ...
info: Adding new user `citizen-developer' (1001) with group `citizen-developer (1001)' ...
info: Creating home directory `/home/citizen-developer' ...
info: Copying files from `/etc/skel' ...
New password: 
Retype new password: 
passwd: password updated successfully
Changing the user information for citizen-developer
Enter the new value, or press ENTER for the default
        Full Name []: 
        Room Number []: 
        Work Phone []: 
        Home Phone []: 
        Other []: 
Is the information correct? [Y/n] y
info: Adding new user `citizen-developer' to supplemental / extra groups `users' ...
info: Adding user `citizen-developer' to group `users' ...
ubuntu@ubuntu:~$ sudo usermod -aG sudo citizen-developer
ubuntu@ubuntu:~$ su - citizen-developer
Password: 
To run a command as administrator (user "root"), use "sudo <command>".
See "man sudo_root" for details.

citizen-developer@ubuntu:~$ sudo whoami
[sudo] password for citizen-developer: 
root
citizen-developer@ubuntu:~$ 
```

### Disable login as system root
* <todo: consider, disable system root login>

Enable SSH for the  new user `citizen-developer`
* <todo: consider, enable ssh for citizen-develoer user >
### Enable ssh
* <todo: consider, example via command line interface>
* <note; minimal config example already has use of empty ssh file in /bootfs? partition, install process section likely needs to be moved from /een/rpi-z to here above for cmopleteness >
* SSH login to single board computer with fixed ip address via many OS’s flashed to many micro sd cards [WS](https://discourse.ubuntu.com/t/ssh-login-to-single-board-computer-with-fixed-ip-address-via-many-oss-flashed-to-many-micro-sd-cards/86683)
* use of ~/.ssh/config as described in link above.

```
tbd dummy entry in config file example
```

### Login via ssh
* Status; ?
* <todo: consider, add process text, >

## References

Raspberry Pi
* Configuration, [WS](https://www.raspberrypi.com/documentation/computers/configuration.html), Rpi Docs, 

Command Line Interface tools
* nmcli, [WS](https://networkmanager.dev/docs/api/latest/nmcli.html), interogate the NetworkManager with commands and manage network settings

Screen
* <todo: consider, link to screen >
