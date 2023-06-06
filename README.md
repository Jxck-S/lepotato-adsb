# AML-S905X-CC (Le Potato) ADS-B Guide


## Requirements
- Le Potato Board
- Micro USB Power Supply
- SDR and Antenna
- Micro SD Card  and Reader
- Le Potato Firmware, Raspbian or Debian

## Raspbian Firmware
- Firmware Install guide https://hub.libre.computer/t/raspbian-11-bullseye-for-libre-computer-boards/82
- Firmware downloads https://distro.libre.computer/ci/raspbian/11/
- Download and extract the image

### Flashing the Image
- Download / Install Win32DiskImager https://sourceforge.net/projects/win32diskimager/
- Open Win32DiskImager and flash the image to your SDCard


### Enabling SSH
- To enable SSH by default, create a blank file called ssh with no file extension.

### Add a User
- To setup an user by default, create a file called userconf.txt with one line in the format username:encrypted-password and replace username with the username you would like to use and encrypted-password generated from openssl passwd -6.

### Startup, Boot and Connect
- Plug in the SD card, ethernet and power
- Wait for it to boot, find the boards IP, with an IP scanner like Fing or look in your routers DHCP
- Connect via SSH via SSH command or a tool like Putty https://www.putty.org/


#### Update
- run ```sudo su```
- run ```apt update```
- run ```apt upgrade```

### Setting up the ADS-B programs
- Plugin the SDR and Antenna
- Run the readsb auto install script. This installs readsb the adsb decoder and tar1090 the ads-b interface.
```
sudo bash -c "$(wget -O - https://github.com/wiedehopf/adsb-scripts/raw/master/readsb-install.sh)"
sudo reboot
```


### Access the web interface
```http://(ip of device)/tar1090```

- tar1090 tutorial https://github.com/wiedehopf/tar1090#tar1090

#### If Issues
- check if sdr is detected with ```lsusb```
- check readsb status ```systemctl status readsb```

### Feed to Websites
- Feeding your ADS-B data to websites of your choice
- FlightAware, FR24, ADSBExchange, TheAirTraffic
- Example TheAirTraffic
```
curl -L -o /tmp/tatfeed.sh https://raw.githubusercontent.com/Jxck-S/tat-feeder/master/install.sh
sudo bash /tmp/tatfeed.sh
```

- Check feed status at https://theairtraffic.com/feed/myip/
