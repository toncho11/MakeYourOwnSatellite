This repository contains information concerning technologies used in small satellites.

There are 3 types of small satellites:
* balloon satellites ([satelloon](https://en.wikipedia.org/wiki/Balloon_satellite)), does not leave the atmosphere, can be freeflying or tethered
* cube satellites ([cubesat](https://en.wikipedia.org/wiki/CubeSat)) , 10 x 10 x 10cm, less than 2 kg, does leave the atmosphere
* can sized satellites ([cansat](https://en.wikipedia.org/wiki/CanSat)), 66mm diameter and 115mm height, mass below 350g, does not leave the atmosphere, are launched by a small rocket (but do not reach orbit velocity) and usually descent using a small parachute

Here we talk mostly about balloon satellites. Balloon satellites can be used for high altitude photography and even telescopes. These can be built by amateurs.

## Communication
* You can use a satellite modem. An example is the [RockBLOCK Mk2](https://www.sparkfun.com/products/13745) modem. One needs subscription to the [Iridium satellite network](https://en.wikipedia.org/wiki/Iridium_satellite_constellation). There is 12£ monthly subscription and also you pay per data. Currently it seems expensive: 50£ corresponds to 500 credits where 1 credit is just 50 bytes which means that 50£ = 24kb of data that will not be sufficient for the satellite to send its position contiously, but it could be doable if the satellite is limitted to sending its position 6 times per day.
* Another option is to use the APRS protocol. With the new [LoRa](https://github.com/lora-aprs/LoRa_APRS_iGate) protocol greater distances can be achieved, but if there are no nearby APRS iGates (Internet connected gate) or relays the data will not be received. Code and available hardware for iGates are available [here](https://github.com/lora-aprs/LoRa_APRS_iGate). Code and LoRa GPS trackers are available [here](https://github.com/lora-aprs/LoRa_APRS_Tracker). Relay systems that forward the message until an iGate is reached do exist and some countries are well covered.

## Positioning
GPS systems are limited to certain altitude and speed. This is known as "CoCom Limits", it is an artificial limit placed on GPS tracking devices that disables tracking when the device calculates that it is moving faster than 1,000 knots (1,900 km/h; 1,200 mph) at an altitude higher than 18,000 m (59,000 ft). So one needs to either use a device that has none of these restrictions or fly at a lower altitude.
An example high quality GPS is: M8Q-5883. There are modules that support the 3 global positioning systems: GPS, GLONASS and Galileo. Limits of GLONASS and Galileo are unknown. One could also use the one from China called [BeiDou](https://en.wikipedia.org/wiki/BeiDou).
Another option is to use the APRS iGates to send the position of the baloon. This solution is not perfect, but it does not require montly subscription.

Alternative positioning can be taking a photo below the satellite, transmitting the photo back to a ground station and performing a map-matching as described in this [article](https://www.mdpi.com/1424-8220/18/11/3836/htm). But this techology is rather used in conjunction with other positioning technologies.

## Microcontroller
This is the central unit that makes the connection between the different components of the satellite. It should be low-powered, small and robust to atmospheric hardships. It is tempting to think that a small device such as Arduino or RaspberryPi will do the job. But these devices lack the last requirement - robustness. They are often used for prototyping and long term use is unknown. We often do not notice that because an Arduino can be easily replaced in non-flying devices.  

So we have the option to either use a micro controller such as Arduino/ESP32 or a more powerful one of type Raspberry Pi. In the case of the former (Arduino) you need to directly program it.

### All in one microcontroller
The following boards have GPS module and are capable of LoRa APRS communication:
* TTGO T-Beam V0.7 (433MHz SX1278)
* TTGO T-Beam V1 (433MHz SX1278)
* [PICOAPRSLITE APRS TRx](https://www.wimo.com/en/picoaprslite)

So they are ready to send their position over the free APRS network. 

### Hardware non x86 comatible (ARM)
* Raspberry Pi (and clones)

### Hardware x86 compatible
The following are low powered mini computers that can be integrated with the other circuits of the satellite:
* [86duino-zero](https://www.cnx-software.com/2013/11/27/39-86duino-zero-is-an-x86-arduino-compatible-board-that-supports-dos-windows-and-linux/)
* [Intel Gallileo Development Board](https://www.cnx-software.com/2013/11/06/69-intel-gallileo-development-board-combines-x86-processor-and-arduino-compatibility/)
* There can even be a variant where an [ESP32 microcontroller](https://en.wikipedia.org/wiki/ESP32) can emulate a 8086 CPU and allow ELKS to run on it. This can be done using the [FabGL ESP32 Board](https://www.tindie.com/products/fabgl/fabgl-esp32-board-16mb-flash-4-mb-psram-33v-io/). One could argue that this 8086 emulation is an added complexity, but ELKS is probably the only Linux like OS that runs on a such low-powered device

In general a full blown OS is not required and it might add complexity and higher power usage. Examples of suitable OSs are [QNX](https://blackberry.qnx.com/en) and [ELKS](https://github.com/jbruchon/elks) (used for old x86 computers).

## Altitude control
A helium balloon can reach 30-40 km height in the atmosphere (outer space starts at 960 km above Earth). It seems the most simple way to calculate altitude is to use an air pressure sensor such as BMP280 or [BMP388](https://www.adafruit.com/product/3966) as an [altimeter](https://en.wikipedia.org/wiki/Altimeter). Pressure decreases when going up. Altitude can be controlled by dropping ballast from the satellite.

## Balloon
There are several companies that provide a "weather baloon". Some come with complete kits. 
* https://www.highaltitudescience.com/products/600-g-near-space-balloon
* https://www.stratoflights.com/en/shop/weather-balloon-200/

## Sensors
https://techxplore.com/news/2022-08-sensor-smart-materials-drone.html

## Power
* battery
* solar panel
* [RAT](https://en.wikipedia.org/wiki/Ram_air_turbine) - a RAM air turbine - usually used on planes in case of emergency to produce electricity utilizing the speed of a plane. Alternatively it could be used on a balloon satellite, but its weight makes it impractical.

## Camera
The camera is positioned towards the ground. Stabilisation can be performed using [icavet-rigging](https://www.publiclab.org/wiki/picavet-rigging).

## Resources
* https://github.com/stanford-ssi/balloons-VALBAL
* [Low cost, high endurance, altitude-controlled latex balloon for near-space research (ValBal)](https://stanfordasl.github.io/wp-content/papercite-data/pdf/Suskho.Tedjarati.ea.AERO2017.pdf)
* Orbit calculations: https://www.physicsclassroom.com/class/circles/Lesson-4/Mathematics-of-Satellite-Motion
