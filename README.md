# How to install Ubuntu server in Raspberry PI 

## Introduction

This recipe shows how to install Ubuntu server on a Raspberry PI board computer (we'll be using version 4), 
without using Raspberry Imager. 

It's necessary a microSD card (>= 16G).

## How to install

0. Insert microSD card;
1. Download Ubuntu server compressed image (.img.xy) from [here](https://ubuntu.com/download/raspberry-pi);
2. Do `xzcat ~/Downloads/<image-file.xz> | sudo dd of=/dev/mmcblk0 bs=32M`, assuming `/dev/mmcblk0` is the MicroSD;
3. Eject the microSD card, and insert into the Raspberry Pi;
4. Run

## Setup

1. By default, the user `ubuntu` (passwd `ubuntu`) is predefined. The first time the new installation is run, it will be prompt a new password. Change it.
2. By default, the keymap is `us`. To change it, do `sudo loadkeys pt` (or other keymap if that's the case)
3. Next, it is necessary to connect to an wifi, if ethernet is not an option. First it's needed to get the name of the Wifi card by showing physical components using the following command:

```shell
$ sudo lshw
```

in my case it was wlan0. Then navigate to `/etc/netplan/` using the cd command the hit Enter

```shell
$ cd /etc/netplan/
```

Use the command ls to list the files and directories under the folder then you now have to edit the .yaml file:

```shell
$ sudo nano 50-cloud-init.yaml
```

Finally, add the following lines to the 50-cloud-init file:

```yaml
wifis:
        wlan0:
            optional: true
            access-points:
                    "SSID-NAME":
                            password: "WIFI-PASSORD"
            dhcp4: yes
```

**NOTE** Make sure not to use tab for space, use the spacebar to create the blank.

Here is the final file code:

```yaml
network:
    ethernets:
        eth0:
            dhcp4: true
            optional: true
    version: 2
    wifis:
        wlan0:
                optional: true
                access-points:
                        "SSID-NAME":
                                password: "WIFI-PASSORD"
                dhcp4: yes
```

Change the SSID-NAME and the WIFI-PASSORD they have to be in quotes. The : after SSID name is required.
Close and save the file using ctrl+x and yes by tipping the letter y
Finally, you need to do some debugs:

```shell
$ sudo netplan –debug try 
$ sudo netplan –debug generate 
$ sudo netplan –debug apply
```

then reboot the pi

```shell
$ sudo reboot
```

4. From this point on, new users and services can be installed, as in any Ubuntu server instance. 
