# Raspberry Pi Imager 

.deb download and install locally

## Ubuntu server
For use in installing Ubuntu 24 server to a microSD Card. 
https://cdimage.ubuntu.com/ubuntu/releases/24.04.4/release/

## Imager download and install

https://github.com/raspberrypi/rpi-imager

https://github.com/raspberrypi/rpi-imager/releases

https://github.com/raspberrypi/rpi-imager/releases#release-v2.0.10

The version 2.0.10 deb instance name
rpi-imager-cli_2.0.10_amd64.deb

get the image from the command line
wget https://github.com/raspberrypi/rpi-imager/releases/download/v2.0.10/rpi-imager_2.0.10_amd64.deb

Install the downloaded image, using dot slash indicates to apt to install from the local directory
sudo apt install ./rpi-imager_2.0.10_amd64.deb

Run the imager 
rpi-imager

Run the imager as command line utility
rpi-imager --cli

Check the version was installed.
$ apt list --installed | grep rpi-imager

WARNING: apt does not have a stable CLI interface. Use with caution in scripts.

rpi-imager/now 2.0.10 amd64 [installed,local]


$ rpi-imager --version
Platform: Linux 7.0.0-28-generic (x86_64)
Running as root via pkexec
Original user: york-earwaker
Original UID: 1000
Original home directory: /home/york-earwaker
DISPLAY already set to: :0
XAUTHORITY already set to: /run/user/1000/.mutter-Xwaylandauth.KKSOT3
localuser:root being added to access control list
Set HOME to: /home/york-earwaker
Set XDG_CACHE_HOME to: /home/york-earwaker/.cache
Set XDG_CONFIG_HOME to: /home/york-earwaker/.config
Set XDG_DATA_HOME to: /home/york-earwaker/.local/share
Set XDG_RUNTIME_DIR to: /run/user/1000
Set DBUS_SESSION_BUS_ADDRESS to: unix:path=/run/user/1000/bus
Text scale factor: 1
libcurl initialized globally
CacheManager initialized with background thread
Detected total system memory: 31938 MB on "Linux"
Optimal async queue depth: 256 (available: 18502 MB, budget: 2775 MB, block size: 1024 KB, baseline: 256 )
FileOperations log callback installed
Starting background cache operations
Starting background drive list polling
Registered rpi-imager:// scheme handler at "/home/york-earwaker/.local/share/applications/com.raspberrypi.rpi-imager-uri-handler.desktop"
Raspberry Pi Imager v2.0.10










