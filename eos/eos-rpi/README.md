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


## References

Raspberry Pi
* Configuration, [WS](https://www.raspberrypi.com/documentation/computers/configuration.html), Rpi Docs, 

