[![Actions Status](https://github.com/bobbydilley/JVSCore-Public/workflows/Build/badge.svg)](https://github.com/bobbydilley/JVSCore-Public/actions)

# JVSCore

JVSCore is a user space driver for using JVS I/O boards with Linux. It requires a USB RS485 converter wired to the JVS I/O.

The JVSCore device driver currently supports the following features of a JVS I/O:

- Switches
- Analogue Inputs

## Installation

Installation is done from the git repository as follows:

```
sudo apt install build-essential cmake git
git clone https://github.com/bobbydilley/JVSCore-Public
cd JVSCore-Public
mkdir build && cd build
cmake ..
cmake --build .
cpack
sudo dpkg --install *.deb
```

## Cable

I'd recommend watching the below video from the TecknoGods about how to create a JVS cable.

https://www.youtube.com/watch?v=kqXEYtvGzno


|RS485 Adapter Side|USB To Arcade Side|
|---|---|
|B-|DATA- (White)|
|A+|DATA+ (Green)|
|5-12V|VCC (Red)|
|GND|GND (Black)|

> I'm not 100% sure if the 5-12V line is giving that, or will just take that - so please be careful what you plug in!

## Command Line Usage

To start JVSCore in the terminal to view debug messages, you can start it by typing the following:

```
sudo jvscore
```

The RS485 converter device path is set in `/etc/jvscore.conf`, with any other configuration values that may come in the future. If you only have one serial device plugged in, you shouldn't have to change it! The fuzz value can also be set in this config file. Fuzz is how much the analogue value has to change by before it is reported to the computer. This is useful if you've got super noisy pots!


## Systemd Service

If you'd like JVSCore to run in the background, and automatically connect to JVS I/O boards you can set it to run as a service. To do so type the following:

```
sudo systemctl enable jvscore
sudo systemctl start jvscore
```

JVSCore will constantly look for new JVS I/O devices (up to a maximum of 1) every minute and when these are found will create a joystick device. Once the JVS I/O is unplugged or switched off the joystick device will disappear.

To view the logs that JVSCore creates while running as a service, type the following:

```
sudo journalctl -u jvscore
```

## Adapters known to work

- https://www.ebay.co.uk/itm/Industrial-USB-To-RS485-Converter-Upgrade-Protection-RS485-Converter/323744400265?ssPageName=STRK%3AMEBIDX%3AIT&_trksid=p2057872.m2749.l2649

## Credits

Thank you very much to @chunksin for helping to test and debug issues with the software!
