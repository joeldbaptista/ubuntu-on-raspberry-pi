# How to install Ubuntu server in Raspberry PI 

## Introduction

This recipe shows how to install Ubuntu server on a Raspberry PI board computer (we'll be using version 4), 
without using Raspberry Imager. 

It's necessary a microSD card (>= 16G).

## How to

0. Insert microSD card;
1. Download Ubuntu server compressed image (.img.xy) from [here](https://ubuntu.com/download/raspberry-pi);
2. Do `xzcat ~/Downloads/<image-file.xz> | sudo dd of=/dev/mmblk0 bs=32M`, assuming `/dev/mmblk0` is the MicroSD;
3. Eject the microSD card, and insert into the Raspberry Pi;
4. Run
