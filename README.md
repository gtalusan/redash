# Broadcom WICED SDK for Amazon Dash

![logo](http://i.imgur.com/7SbDC65.jpg "")

## History

Based on the work of [maximus64](https://github.com/maximus64/amazon-dash-wiced) and [dekuNukem](https://github.com/dekuNukem/Amazon_Dash_Button).  Please visit their repositories for more information.

GPIO table in [maximus64](https://github.com/maximus64/amazon-dash-wiced)'s `platform.c` was thrown out and reversed from [dekuNukem](https://github.com/dekuNukem/Amazon_Dash_Button)'s `Cottonelle.bin` and a sample binary compiled from the `WICED SDK 2.4.1`.  The pin out [here](https://github.com/dekuNukem/Amazon_Dash_Button/blob/master/Pinouts_and_Components.pdf) was also quite handy.

## What Works

* Wi-Fi
* LED
* Button
* UART
* SWD
* SPI flash

## To Do

* I2S microphone (see staging directory for WIP)

## Building

* Download the Broadcom WICED SDK 3.3.1
* Create a git repository out of it
* `git apply` the patches in this repository

## Development tools

* The cheapest eBay Mini ST-Link V2 is what I use to flash firmware.
* Note that the Amazon Dash comes with its internal flash memory write protected, [OpenOCD](http://repo.or.cz/w/openocd.git) can help with unlocking it.
```
stm32f2 unlock 0 # this will also mass erase your Dash's flash
```
* [stlink](https://github.com/texane/stlink) is what I use to flash binaries built without WICED.

## Examples

* Some example code exists in the `snip` directory.
* Build them like this:
```
./make AMAZONDASH-snip.sflash
```

## Building a custom WICED firmware

```
./make AMAZONDASH-snip.sflash download run JTAG=stlink-v2
```

#### Output

```
Starting WICED v3.3.1
Platform AMAZONDASH initialised
Started ThreadX v5.6
Initialising NetX_Duo v5.7_sp2
Creating Packet pools
WWD SDIO interface initialised
WLAN MAC Address : 6C:0B:84:8A:6C:F0
WLAN Firmware    : wl0: Nov  7 2014 16:03:45 version 5.90.230.12 FWID 01-43ca27a5
found spi flash device 0x202015
spi flash has size 0x200000 bytes
about to erase spi flash..
sflash_chip_erase == 0
erasing first block of spi flash..
sflash_sector_erase == 0
sflash_write == 0
sflash_read == 0
memcmp(buf, buf2) == 0
that's all folks!
```
