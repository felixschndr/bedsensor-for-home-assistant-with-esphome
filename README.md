# Introduction
The goal of this project is to create a presence sensor for a bed that reports its state to Home Assistant and thus can be used in automations. This is achieved by using two pressure sensors attached to an ESP32 micro controller which then relays the information about each half of the bed to the home automation server.
# Fundamentals
First, let us cover some of the basics that are necessary for this project.
## What is ESPHome?
ESPHome is an open source platform that allows users to configure microcontrollers and integrate them into smart home systems such as Home Assistant. As such microcontrollers are very inexpensive, they are ideal for implementing your own smart home projects.

ESPHome can be setup quite easily. There is a test version available at [https://web.esphome.io/](https://web.esphome.io/) and it can be self-hosted (for free) with Home Assistant or as an independent Docker container. I will go into further details on this in the [`setup`](#setup-of-esphome) part later.
## Which devices does ESPHome support?
ESPHome *primarily* supports microcontrollers from the ESP8266 and ESP32 families, both manufactured by the Chinese company [*Espressif Systems*](https://www.espressif.com/). Some of the popular microcontrollers that can be used for ESPHome projects include the following:
* ESP8266-based microcontrollers
  * [NodeMCU](https://www.nodemcu.com/)
  * [Wemos D1 Mini](https://www.wemos.cc/en/latest/d1/d1_mini.html)
  * [ESP-01](https://www.utmel.com/components/esp-01-wi-fi-module-esp-01-pinout-programming-and-esp-01-vs-esp8266-faq?id=990)
  * [ESP-12E and ESP-12F](https://www.elecrow.com/blog/things-you-should-know-about-esp8266-wifi-module.html)
* ESP32-based microcontrollers
  * [ESP32 Dev Kit](https://www.espressif.com/en/products/devkits/esp32-devkitc)
  * [Wemos D32](https://www.wemos.cc/en/latest/d32/d32.html)
  * [ESP32-CAM](https://www.arducam.com/esp32-machine-vision-learning-guide/) (an ESP32 based system which offers an onboard camera module for around $7)

ESP32 and ESP8266 are *only* the chips themselves: They are the platforms and are manufactured by *Espressif Systems*. These are *System on a Chip* (SoC) designs, meaning they integrate various components such as CPU, memory, and wireless connectivity onto a single chip.

There are several variants of these chips: Espressif Systems offers different ESP32/ESP8266 chip variants with varying features such as number of cores (single or dual), clock speed, and memory capacity.

These SoCs are then placed on different boards: Several companies produce development boards specifically designed for ESP32/ESP8266 chips. These boards typically include additional components such as voltage regulators, USB ports, and breakout pins for connecting external sensors or devices.

Although ESPHome primarily runs on [ESP32](https://esphome.io/components/esp32) and [ESP8266](https://esphome.io/components/esp8266)-based platforms it also includes limited support for [RP2040](https://esphome.io/components/rp2040)-based chips and chips based on the [LibreTiny](https://esphome.io/components/libretiny) platform.

# Installation and Configuration

In this project we will use the an ESP-32 development board which can be acquired on different platforms like [Amazon](https://www.amazon.com/s?k=ESP32) or [AliExpress](https://www.aliexpress.us/w/wholesale-esp32.html) for less then $10.
## Setup of ESPHome
There are multiple ways to use ESPHome. For testing purposes and initialization of the microcontroller it is possible to use a web hosted version of ESPHome available at [https://web.esphome.io/](https://web.esphome.io/). However this is only a lite variant of ESPHome. For bigger projects it is recommended to self-host ESPHome. There are two ways of doing this:

1. If you have a running Home Assistant instance you can install ESPHome as an add-on. The documentation on how to this can be found [here](https://esphome.io/guides/getting_started_hassio).

   `Note:` This is not always possible. If you have setup Home Assistant with a Docker container refer to option `2`. From the [docs of Home Assistant](https://www.home-assistant.io/addons/):
   > Add-ons are only available if you've used the Home Assistant Operating System or Home Assistant Supervised installation method. If you installed Home Assistant using any other method then you cannot use add-ons.
2. The other way to install ESPHome is to create a container for it. This is a simple a docker-compose example:
   ```yml
   version: '3'

   services:
     esphome:
       image: ghcr.io/esphome/esphome
       volumes:
         - ./data/esphome:/config
         - /etc/localtime:/etc/localtime:ro
       ports:
         - 6052:6052
       environment:
         - USERNAME=admin
         - PASSWORD=mysecretpassword
   ```
   After running `docker-compose up` ESPHome can be accessed via an web browser on `<Hostname/IP of the server>:6052`.
## How to flash an ESP32
## Configuration of device
### Wifi
### Encryption
### GPIO
# Integration into Home Assistant
# Application Example: A bed presence sensor
## Hardware
### Pressure sensor
### Cabling
### Power
## Software
### Requirements
### GPIO Configuration
### Integration into Home Assistant and Configuration of Home Assistant
## Example for an automation
# Conclusion