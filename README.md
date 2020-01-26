# Xiaomi-Bluetooth-Digital-Thermometer

Last month I brought a bundle of 3 bluetooth (thermometer)[https://www.aliexpress.com/item/4000358588436.html?spm=a2g0s.9042311.0.0.5a204c4d9Ag1aE] from AliExpress.

I made this repo to kept the details about how to connect and monitor the devices from a Linux box.

![](termometer.png?rax=true)

# TL;DR;

## Searchin for the devices
The device name is LYWSD03MMC in my case

```
% sudo hcitool lescan
A4:C1:38:XX:XX:XX LYWSD03MMC
A4:C1:38:XX:XX:XX LYWSD03MMC
A4:C1:38:XX:XX:XX LYWSD03MMC
```

## Connecting to the device

Using `gatttool` you will be able to connect and enable the notifications.

First start gatttool in interactive mode to access the prompt
```
gatttool -b a4:c1:38:XX:XX:XX  -I
[a4:c1:38:XX:XX:XX][LE]>
```

The type the following commands

```
[a4:c1:38:XX:XX:XX][LE]>connect
Attempting to connect to a4:c1:38:XX:XX:XX
Connection successful
```

Now enable the notifications to get the measured values:

```
[a4:c1:38:XX:XX:XX][LE]>char-write-req 0x0038 0100
Characteristic value was written successfully
```

After this command notification should start to appears every 1 second

```
Notification handle = 0x0036 value: 4d 07 3d 99 0b
Notification handle = 0x0036 value: 4d 07 3d 99 0b
Notification handle = 0x0036 value: 4e 07 3d 99 0b
Notification handle = 0x0036 value: 4e 07 3d 99 0b
Notification handle = 0x0036 value: 50 07 3d 99 0b
Notification handle = 0x0036 value: 4f 07 3d 99 0b
Notification handle = 0x0036 value: 4d 07 3d 99 0b
Notification handle = 0x0036 value: 4c 07 3d 99 0b
Notification handle = 0x0036 value: 4e 07 3d 99 0b
Notification handle = 0x0036 value: 4b 07 3d 99 0b
```

![](real-device.png?raw=true "Real thermometer")



```
4b 07 3d 99 0b
----- --
 \     \-Humidity in % 0x3D = 61%
  \_ Temperature in Hex (0x074B = 1867) 1867 / 10 = 10.67
```
