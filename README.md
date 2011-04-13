## Requirements

  * `wpa_supplicant`
  * `dhcpcd`
  * A gaspar login/password at the EPFL (you get one if you're a student or an employee there)
  * A working wifi adapter (tee hee)

## Installation

Copy `wpa_supplicant.conf` to /etc/
Edit `wpa_supplicant.conf` to replace the `GASPAR_LOGIN` and `GASPAR_PASSWORD` values with your own.

Copy `go-wifi` and `stop-wifi` to somewhere in your `$PATH` (e.g. `/usr/bin/`)
Edit `go-wifi` and `stop-wifi` to set the proper values for `WIRELESS_IF` (default = wlan0) and `KERNEL_MODULE` (default = iwlagn)

A passwordless sudo makes them more comfy, use the `NOPASSWD` directive in `visudo` if you want to enable it (at your own risk!)

## Usage

### Connecting

Do

    go-wifi

to start the network. It might take some time to associate + get an IP address.

You can use `sudo wpa_cli status`, `iwconfig`, and `ifconfig` to check, respectively what `wpa_supplicant` is doing, what wireless access point you're associated to, and if you already have an IP address

### Disconnecting

Do

    stop-wifi

to disconnect from the network. This will kill the DHCP daemon and `wpa_supplicant`

### Reconnecting

The soft way:

    go-wifi

This will tell `wpa_supplicant` to reassociate

The hard way:

    stop-wifi; go-wifi

This will shut down the dhcpcd daemon and `wpa_supplicant`, then try to connect again from scratch

## Licence

[WTFPL 2.0](http://sam.zoy.org/wtfpl/)

Enjoy!
