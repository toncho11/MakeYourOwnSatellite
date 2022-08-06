This repository contains information for techologies used in small satellites.

There are 3 types of small satellites:
* ballon satellites (satelloon)
* cube sattellites (cubesat)
* can sized satellites (cansat)

Here we talk mostly about ballon satellites.

## Communication
You can use a satellite modem. An example is the [RockBLOCK Mk2](https://www.sparkfun.com/products/13745) modem. One needs subscription to the [Iridium satellite network](https://en.wikipedia.org/wiki/Iridium_satellite_constellation). There is 12£ monthly subscription and also you pay per data. Currently it seems expensive: 50£ corresponds to 500 credits where 1 credit is just 50 bytes which means that 50£ = 24kb of data that will not be sufficient for the satellite to send its position contiously, but it could be doable if the satellite is limitted to sending its position 6 times per day.

## Positioning
GPS systems are limmitted to certain altitude and speed. So one needs to either use a device that has none of these restrictions or fly at a lower altitude.
An example high quality GPS is: M8Q-5883.
There are modules that support the 3 global positioning systems: GPS, GLONASS and Galileo. You could also use the one from China called [BeiDou](https://en.wikipedia.org/wiki/BeiDou)
In GPS technology, the term "CoCom Limits" also refers to a limit placed on GPS tracking devices that disables tracking when the device calculates that it is moving faster than 1,000 knots (1,900 km/h; 1,200 mph) at an altitude higher than 18,000 m (59,000 ft).

## Microcontroller
This is the central unit that makes the connection between the different components of the satellite. It should be low-powered, small and robust to atmospheric hardships. It is tempting to think that a small device such as Arduino or RaspberryPi will do the job. But these devices lack the last requiremnt - robustness. There are often used for prototyping and long term use is unknown. We often do not notice that because an Arduino can be easily replaced in non-flying devices. In geneal a full blown OS is not required and it might add complexity and higher power usage. Still an OS such as [QNX](https://blackberry.qnx.com/en) and [ELKS](https://github.com/jbruchon/elks) (used for old x86 computers) could be potentially used. There can even be a variant where an ESP32 microcontroller that emulates a 8086 CPU and allows the ELKS OS to run on it. One could argue that this 8086 emulation is an added complexity, but it is probably the only Linux that runs on a such low-powered device.

## Altitude control
It seems the most simple way to calculate altitude is to use air pressure sensor such as BMP280. Pressure decreases when going up. Altitude can be controlled by dropping ballast from the satellite.

## Power
* battery
* solar panel
* [RAT](https://en.wikipedia.org/wiki/Ram_air_turbine) RAM air turbine - usually used on planes in case of emergency to produce electricity utilizing the speed of the plane

## Resources
* https://github.com/stanford-ssi/balloons-VALBAL
* [Low cost, high endurance, altitude-controlled latex balloon for near-space research (ValBal)](https://stanfordasl.github.io/wp-content/papercite-data/pdf/Suskho.Tedjarati.ea.AERO2017.pdf)
* Orbit calculations: https://www.physicsclassroom.com/class/circles/Lesson-4/Mathematics-of-Satellite-Motion
