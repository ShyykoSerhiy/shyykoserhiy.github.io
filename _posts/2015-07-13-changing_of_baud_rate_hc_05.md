---
layout: post
comments: true
title: Changing the baud rate of HC-05 bluetooth module to work with MultiWii.
---

HC-05 is cheap yet capable and easy to use Bluetooth SPP (Serial Port Protocol) module and it can be used to control your
quadcopter which runs MultiWii. There is one catch though. Default Baud rate of HC-05 is 9600 and that's a problem, because
MultiWii software expects serial input-output device to operate at 115200. Gladly it's fairly easy to change Baud rate of HC-05
if you have USB-TTL adapter or Adruino. In this post I'll show how to change Baud using USB-TTL adapter.

### Requirenments
For this method to work you'll need:

1. USB-TTL adapter. I've used this one(FTDI Basic Breakout Arduino USB-TTL 6 PIN 3.3 5V): ![FTDI adapter that I've used](/assets/2015-07-13/ftdi.jpg).
2. Wires to connect HC-05 and USB-TTL.
3. PC or Mac.
4. Arduino IDE(We'll need serial monitor only.)

### How to connect with FTDI
At first we need to connect HC-05 with USB-TTL adapter. Connect your HC-05 to match the table below:

| HC-05 |            | USB-TTL adapter |
|-------|------------|-----------------|
| TXD   | connect to | TXD             |
| RXD   | connect to | RXD             |
| GND   | connect to | GND             |
| VNC   | connect to | +5              |

![Connection](/assets/2015-07-13/connection.jpg)

### How to get to the AT mode
At first we need to find out which type of HC-05 breakout you have: with or without "switch" button. If you have HC-05
with "switch" button then to enter AT mode just press and hold "switch" button before powering USB-TTL adapter. HC-05 will
slowly blink every 2 seconds to indicate that it's in AT mode. If there is no "switch" button you'll need to hot wire PIN
\#34 on HC-05 before powering USB-TTL adapter. And again after powering HC-05 will slowly blink every 2 seconds to
indicate that it's in AT mode.(I've used second method before I realized that my HC-05 actually had "switch" button for that)
![Switch button](/assets/2015-07-13/switchbutton.jpg)

To summarize this are the steps to enter into AT mode:
### First way (if you have "switch" button on your HC-05)
* Step 1: Press and hold "switch" button
* Step 2: Supply power to USB-TTL. Then the HC-05 will enter to AT module.

### Second way (if you don't have "switch" button on your HC-05)
* Step 1: Connect PIN34 to the power supply PIN(VCC).
* Step 2: Supply power to USB-TTL (the PIN34 is also supplied with high level since the PIN34 is connected with
power supply PIN). Then the HC-05 will enter to AT module.

### Chaning Baud rate in Arduino IDE Serial Monitor
Now we just need to open Arduino IDE and change Baud rate.

* Step 1: Download Arduino IDE
* Step 2: Open Arduino IDE and select correct Serial Port (Tools->Serial Port->"SomePortGoesHere" (in my case it was /dev/tty.usbserial))
* Step 3: Open Serial Monitor (Tools->Serial Monitor)
* Step 4: Check that communication Baud rate is 38400, line endings are "Both NL and CR".
* Step 5: Print "AT" to check that connection is OK.(Response should be OK)
* Step 6: Print "AT+UART" to see current Baud rate config
* Step 7: Print "AT+UART=115200,0,0" to set new Baud rate(first param 115200 - Baud rate(bits/s), second param 0 - stop bit(0---1 bit, 1---2 bits,
0), third param 0 - parity bit(0----None, 1----Odd parity, 2----Even parity))
* Step 8: Print "AT+UART" to check current Baud rate config
![Changing of Baud rate animation](/assets/2015-07-13/demo.gif).

That's it. We've changed the Baud rate of HC-05. Now we can use it with MultiWii.

In case you'll want to change some other HC-05 config(bluetooth name, passkey, etc) here is list the of AT commands:
<a href="/assets/2015-07-13/hc-05.pdf">HC-05 AT command set</a>
