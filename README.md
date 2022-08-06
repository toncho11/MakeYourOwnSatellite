This repository contains information techologies used in small satellites.

There are 3 types of small sattelites:
* ballon sattelites
* cube sattelites (cubesat)
* can sized sattellites (cansat)

Here we talk mostly about ballon satellites.

## Communication
An example is RockBlock sattelite modem. One needs subscription to the Iridium Sattelite network. There is 12£ monthly subscription and also you pay per data. Currently it seems expensive: 50£ correspond to 500 credits where 1 credit is just 50 bytes which means that 50£ = 24kb of data that will not sufficient for the sattelite to send its possition contiously, but it could be doable if the sattelite is limitted to sending its possition 6 times per day.

## Postioning
Gps systems are limmitted to certain altitude and speed. So one needs to either use a device that hoas no these restrictions fly at a lower altitude.
An example high quality GPS is: M8Q-5883.
There are mosules that support the 3 global position systems. Probabably not in the same time.

## Microcontroller
This is the central unit that makes the connection between the defferent sensors and communication devices. It should be low powered, small and robust to atmospheric hardships. It is tempting to think that a small device such as Arduino or RaspberryPi will do the job. But these devices lack the last requiremnt - robustness. There are often used for prototyping and long term use is unknown. In geneal a full blown OS is not required and it might add to complexity and higher power usage. Still OS such as QNX and ELKS could be potentially used. There can even be a hybrid variant where ESP32 microcontroller emulates a 8086 CPU and allows the ELKS OS to run on it. One could argue that this 8086 emulation is an added complexity, but it is probably the only Linux that runs on a such low-powered device.

## Altitude control
It seems the most simple way to calculate altitude is to use air pressure sensor such as BMP280. 
Most balloons are filled with hellium. 
Altitude can be controlled by dropping ballast from the sattelite.

## Power
* battery
* solar
* [RAT](https://en.wikipedia.org/wiki/Ram_air_turbine) RAM air turbine - is used on planes in case of emergency to produce electricity utilizing the speed of the plane

## Resources
* https://github.com/stanford-ssi/balloons-VALBAL
* [Low cost, high endurance, altitude-controlled latex balloon for near-space research (ValBal)](https://stanfordasl.github.io/wp-content/papercite-data/pdf/Suskho.Tedjarati.ea.AERO2017.pdf)
* Orbit calculations: https://www.physicsclassroom.com/class/circles/Lesson-4/Mathematics-of-Satellite-Motion
