# Project Sandcastle - Linux build with built-in RAMDisk

## Disclaimer
These are modified versions of the scripts found on the Project Sandcastle website and a script from the pongoOS repo I do not take credit for these nor am I associated with the development of either project.

If you would prefer to use the original copies the things changed are as follows:
* Removed `load-linux.mac`
* Added load_linux.py from [here](https://github.com/checkra1n/pongoOS/blob/master/scripts/load_linux.py)
* Then just follow the instructions below

## MAC:
Download and install the latest checkra1n from [here](http://checkra.in)
Open a terminal window and run `/Applications/checkra1n.app/Contents/MacOS/checkra1n -cp` then run `./load_linux.py -k Linux.lzma -d dtbpack`

## Linux:
Download the latest checkra1n from [here](http://checkra.in)
Open a terminal window and run `checkra1n -cp` then run `./load_linux.py -k Linux.lzma -d dtbpack`


The Linux build comes with a baked in RAMDisk.
It will automatically bring up X windows after boot.
It will also create a gadget USB interface on the host computer and if you set the IP address of the interface to 172.16.1.2/255.255.255.0  you will be able to access the iPhone at 172.16.1.1.
Once its booted you can login via ssh with root/alpine.

## To use Bluetooth:
`hciconfig hci0 up`
`bt-adapter -d`
```Searching...
[47:29:F5:32:D1:C0]
  Name: (NULL)
  Alias: 47-29-F5-32-D1-C0
  Address: 47:29:F5:32:D1:C0
  Icon: (NULL)
  Class: 0x0
  LegacyPairing: 0
  Paired: 0
  RSSI: -70
```

## To use Wi-Fi:
`iw wlan0 scan`
```BSS 11:22:52:3c:67:20(on wlan0)
	last seen: 97.608s [boottime]
	TSF: 0 usec (0d, 00:00:00)
	freq: 2412
	beacon interval: 100 TUs
	capability: ESS Privacy Sh
...
```

`wpa_passphrase SSID PASSWORD > /etc/wpa_supplicant.conf`
`wpa_supplicant -Dnl80211 -iwlan0 -c/etc/wpa_supplicant.conf -B`
`udhcpc -i wlan0`

## Run doom:
`chocolate-doom`

## Run X windows manager:
`fluxbox`
