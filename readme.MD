## Setting up 802.1X at home: a personal journey


### Purpose

To setup a free-standing FreeRADIUS server and access point to enable risk free config testing on a home LAN. This readme assumes as
little technical knowledge as possibe.

### Requirements

- A machine which can run Linux docker containers (i.e. a machine running Linux or MacOS).

- A home LAN. A standard router with at least one free ethernet port is sufficient.

- An access point, in addition to any router providing your Internet connection, which supports WPA Enterprise / 802.1X WiFi authentication. This was tested with a Netgear DGN2000 which does. An old Sky Hub I checked did not.



### Rasberry Pi as access point

Tested on the original Raspberry Pi, model B using a USB hub to provide ethernet via a USB/ethernet converter and a Wifi dongle.

Download the Raspberry Pi OS from [here](https://www.raspberrypi.org/software/operating-systems/)

Extract the .img file from the zip and enter the directory containing it in the terminal.

Enter `sudo blkid` to see a list of attached disks. Attach/insert an SD card to your machine and enter `sudo blkid` to see which device
has been allocated to the SD card. In my case it was /dev/sdf.

Enter:

```
sudo dd if=./2021-05-07-raspios-buster-armhf-lite.img of=/dev/sdf bs=4M
```

...where '2021-05-07-raspios-buster-armhf-lite.img' is the name of the .img file, which may be different and /dev/sdf is the device
identified above.

When dd has finished running remove and re-attach the SD card. It should automount the 'boot' partition. Within this create a new, empty
file called .ssh.