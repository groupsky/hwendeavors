title: ESP8266 with NodeMcu
date: 2015/04/01
comments: true
---
[NodeMCU](http://nodemcu.com/index_en.html) is [Lua](http://www.lua.org) based firmware for [ESP8266](https://espressif.com/en/products/esp8266). Long story short - instead of writing in C you are able to use Lua which allows for faster prototyping (at least in theory!).

## Pre-requisites

### Hardware

* **ESP8266** - [Olimex MOD-WIFI-ESP8266-DEV](https://www.olimex.com/Products/IoT/MOD-WIFI-ESP8266-DEV) is best for development - fits on breadboard and leaves 2 rows of pins, while the [NodeMcu Development Kit](http://nodemcu.com/index_en.html#fr_54747661d775ef1a3600009e) featuring integrated serial to usb cover a whole breadboard and you need to use jump wires instead of dupont wires. The other modules suitable for development are ESP-7, ESP-8 and ESP-12, but they don't fit on standard breadboard so you want to order some adapter plates.
* **USB-UART cable** - any serial cable should do, but there are some [modules with integrated 3V3 power supply](http://www.aliexpress.com/wholesale?SearchText=usb+uart+6pin)
* **Power supply** - it's best to obtain a combined [3.3V and 5V power supply](http://www.aliexpress.com/w/wholesale-mb102-power-supply.html?SearchText=mb102+power+supply&CatId=4099) as some components require 5V.
* **AC-DC adapter** or **USB cable** - 5V@500mA or better, preferably 9V@1A. The ESP itself consumes up to 300mA so make sure you have enough supply or you will experience very strange behavior from the ESP.
* **Breadboard** - any size will suffice
* **Dupont wires** or **Jump wires** - mostly male-to-male, but some male-to-female should be available
* [OPT] **Logic Level Converter** - the more channels the better and definitely [two-way](http://www.aliexpress.com/w/wholesale-logic-level-converter.html?SearchText=logic+level+converter&CatId=502)
* [OPT] **Switch buttons** - just to ease entering flash mode and restart. The NodeMcu DevKit has those integrated

### Software

* **Text editor** - anyone (except Notepad due to it's notorious BOM). I'm big fan on [Atom IDE](http://atom.io/) so you may give it a try.
* **Serial Terminal** - [PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) for win, [picocom](https://code.google.com/p/picocom/) available in dep repos, mac - ???
* [**luatool**](https://github.com/4refr0nt/luatool) - for loading lua files
* [**esptool**](https://github.com/themadinventor/esptool) - for burning images
* [**NodeMCU**](https://github.com/nodemcu/nodemcu-firmware/releases) - just take the latest build

## Setting up

{% asset_img esp_bb.png %}
{% asset_link esp.fzz Get the Fritzing file %}

The most important things to wire are (for Olimex module):

1. Pin 1: 3.3V - power supply +3.3V
2. Pin 2: GND - power supply GND
3. Pin 3: GPIO1 - connect to UART TX
4. Pin 4: GPIO3 - connect to UART RX

On ESP-7,-8 and -12 you need to connect

1. Pin 3: CH_PD - power supply +3.3V
2. Pin 8: VCC - power supply +3.3V
3. Pin 9: GND - power supply GND
4. Pin 15: RXD - connect to UART TX
5. Pin 16: TXD - connect to UART RX

## Flashing NodeMcu

1. [Download](https://github.com/nodemcu/nodemcu-firmware/releases) the latest release. Integer version seems more stable for the moment.
2. Connect GPIO0 (pin 21 on Olimex module) to power supply GND to enter flash mode
3. Power on or restart the ESP module
4. Flash the downloaded firmware
``` bash
esptool.py write_flash 0x00000 nodemcu_integer_0.9.6-dev_20150331.bin
```
5. Start your terminal at baudrate **9600bps**
``` bash
picocom -b 9600 /dev/ttyUSB0
```
6. Hit `Enter`
7. You should see the lua prompt
``` lua
>
```

Now you're ready to start develop.


## Useful resources
* [NodeMcu API](https://github.com/nodemcu/nodemcu-firmware/wiki/nodemcu_api_en)
* [ESP8266 Wiki](https://github.com/esp8266/esp8266-wiki/wiki)
* [ESP8266 Comunity Forum](http://www.esp8266.com/)
