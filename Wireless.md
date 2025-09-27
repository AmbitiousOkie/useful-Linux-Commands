# Wireless

* `sudo lsusb -vv`
* `sudo airmon-ng`
* `sudo modinfo ath9k_htc`
* `lsmod`
* `sudo rmmod ath`
* `sudo iwlist wlan0 frequency`
* `sudo iw list`
* `sudo iw dev wlan0 scan`
* `sudo iw dev wlan0 scan | egrep "DS Parameter set|SSID:"`
* `sudo iw dev wlan0 interface add wlan0mon type monitor`
* `sudo ip link set wlan0mon up`
* `sudo iw dev wlan0mon info`
* `sudo iw dev wlan0mon interface del`
* `sudo iw reg get`
* `sudo rfkill list`
* `sudo rfkill block 1`
* `sudo rfkill list 1`
* `sudo rfkill unblock 1`
* `sudo rfkill unblock all`

`sudo iw dev wlx00c0cab6d97c interface add wlan0mon type monitor`

# Linux Command Notes: Wireless & Device Management

This document provides a breakdown of common Linux commands used for inspecting USB devices, managing kernel modules, and configuring wireless network interfaces.

---

### `sudo lsusb -vv`

This command lists information about all the USB devices connected to your system in a very verbose format.

* **`sudo`**: Executes the command with administrator (root) privileges.
* **`lsusb`**: The command to list USB devices.
* **`-vv`**: The "very verbose" flag. It provides the most detailed output possible, including device descriptors, configurations, and capabilities. This is useful for deep hardware diagnostics.

---

### `sudo airmon-ng`

Part of the Aircrack-ng wireless security suite, this command is used to enable and disable **monitor mode** on wireless network interfaces. Running it without any arguments lists the available wireless interfaces and their status.

---

### `sudo modinfo ath9k_htc`

This command displays detailed information about a specific kernel module.

* **`modinfo`**: The command to show information about a kernel module.
* **`ath9k_htc`**: The name of the kernel module being inspected. In this case, it's a common driver for Atheros-based USB Wi-Fi adapters. The output includes the module's author, description, license, and any parameters it accepts.

---

### `lsmod`

The `lsmod` command shows which **kernel modules** are currently loaded into the kernel. The output includes the module's name, its size in memory, and whether other modules are dependent on it. It's a quick way to see all active drivers and modules on your system.

---

### `sudo rmmod ath`

This command is used to remove or unload a kernel module.

* **`rmmod`**: The command to remove a module.
* **`ath`**: The name of the module to be removed. Note that you cannot remove a module if another loaded module depends on it.

---

### `sudo iwlist wlan0 frequency`

This command lists all the available frequencies and channels that a specific wireless interface can operate on.

* **`iwlist`**: A tool to query wireless interfaces for specific information.
* **`wlan0`**: The name of the wireless interface being queried.
* **`frequency`**: The specific parameter to query.

---

### `sudo iw list`

The `iw` command is a modern tool for configuring wireless devices. The `list` argument shows the capabilities of all wireless devices on your system. This includes supported modes (like station, AP, monitor), available frequency bands and channels, and other hardware-level features.

---

### `sudo iw dev wlan0 scan`

This command initiates a scan for nearby wireless networks on the specified interface.

* **`iw dev wlan0`**: Specifies that the operation is for the device named `wlan0`.
* **`scan`**: The action to perform. The output is a detailed list of all detected Access Points, including their SSID, signal strength, and security protocols.

---

### `sudo iw dev wlan0 scan | egrep "DS Parameter set|SSID:"`

This is a chained command that scans for networks and then filters the output to show only the essential information.

* **`sudo iw dev wlan0 scan`**: Performs the network scan.
* **`|`**: The "pipe" operator, which sends the output of the first command as the input for the second command.
* **`egrep "DS Parameter set|SSID:"`**: Filters the scan results to show only lines containing the SSID (the network name) and the "DS Parameter set" (which indicates the channel the network is on).

---

### `sudo iw dev wlan0 interface add wlan0mon type monitor`

This command creates a new **virtual network interface** specifically for operating in monitor mode.

* **`interface add wlan0mon`**: Adds a new interface named `wlan0mon`.
* **`type monitor`**: Sets the mode of this new interface to "monitor," which allows it to capture all raw 802.11 wireless traffic in the air, not just packets addressed to your device.

---

### `sudo ip link set wlan0mon up`

This command activates or "brings up" the specified network interface. After creating the `wlan0mon` monitor mode interface, you must run this command to enable it before you can use it.

---

### `sudo iw dev wlan0mon info`

This command displays detailed information about the specified wireless interface, such as its MAC address, its current type (e.g., monitor), and the channel it's currently set to.

---

### `sudo iw dev wlan0mon interface del`

This command deletes a virtual network interface. It's used to remove the `wlan0mon` interface and stop monitor mode, returning your wireless card to its normal state.

---

### `sudo iw reg get`

This command displays the system's current wireless **regulatory domain**. This information is important because it dictates which Wi-Fi channels and transmission power levels are legally allowed in your geographic region to prevent interference with other services.

---

### `sudo rfkill list`

The `rfkill` utility is used to enable or disable wireless transmitters. The `list` command shows all wireless devices on your system (e.g., Wi-Fi, Bluetooth) and their status. It will tell you if a device is **soft blocked** (disabled by software) or **hard blocked** (disabled by a physical switch).

---

### `sudo rfkill block 1`

This command applies a software-level block to disable a wireless device. The number (`1`) corresponds to the index number of the device shown in the `sudo rfkill list` output.

---

### `sudo rfkill list 1`

This command shows the status of only the device with the specified index number (`1`), rather than listing all devices.

---

### `sudo rfkill unblock 1`

This command removes a software-level block from a wireless device, enabling it. The number (`1`) corresponds to the device's index number.

---

### `sudo rfkill unblock all`

This command removes all software-level blocks from all wireless devices managed by `rfkill`, effectively enabling all of them at once.



## Working with ALFA Drivers
Ubuntu and derivatives

https://docs.alfa.com.tw/Support/Linux/RTL8812AU/

```
git clone https://github.com/aircrack-ng/rtl8812au.git
cd rtl8812au
make
sudo make install
find /lib/modules/`uname -r`/ -name "88XXau.ko"
```

Disconnect and reconnect the USB dongle

## Wireshark Filters

## Display Filters 

`wlan.fc.type == 2`

`(wlan.fc.type == 2) && ~(wlan.fc.subtype == 0)`

## Capture Filters

`(wlan addr1 3A:30:F9:0F:E1:95) or (wlan addr2 3A:30:F9:0F:E1:95) or (wlan addr3 3A:30:F9:0F:E1:95) or (wlan addr4 3A:30:F9:0F:E1:95)`

