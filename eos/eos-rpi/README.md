# Embedded operating systems for raspberry pi eos-rpi

stub

## Notes

Objectives
* Observations on use of a number of operating systems from different groups with raspberry pi embedded systems

## Status
TODO
* <todo: consider, collate informaton re os for rpi usage attemtps here, start with tasks matrix markup table>
* <todo: consider, move os install notes from /rpi-z directory in /een repo to this location to simplify /een/rpi-z README.md page >
* <todo: consider, icloud confiiguration, specific to rpi os Trixi + >

DONE
* <done: consider, intent to commit>

## Output - OS install and confiiguration
Consider breakout different OS attempts to different pages 

### RPi OS Trixi Lite -  cli config
Assumuptions 
* minimal config for initial OS install
* headless setup, even with an OS with a desktop
* OpenSSL uid/pwd were set in initial minimal install setup
* UART config set in intial minimal install setup

Wifi
* Status: TBD
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
        24:A4:3C:9E:D2:84  An-Example           Infra  1     195 Mbit/s  100     ▂▄▆█  WPA2
        6C:14:6E:E5:35:F4  Home_Network_5G      Infra  149   405 Mbit/s  92      ▂▄▆█    WPA2
*       C8:3A:35:58:B2:60  Office_WiFi          Infra  6     270 Mbit/s  75      ▂▄▆_    WPA2 802.1X
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
* ...

## References

Raspberry Pi
* Configuration, [WS](https://www.raspberrypi.com/documentation/computers/configuration.html), Rpi Docs, 

Command Line Interface tools
* nmcli, [WS](https://networkmanager.dev/docs/api/latest/nmcli.html), interogate the NetworkManager with commands and manage network settings

Screen
* <todo: consider, link to screen >
