# Axe Effect

Axe Effect is an SNMP-capable WiFi temperature (and humidity) sensor, designed specifically for server rack installations.

The device is designed to be simple to use, and provides accurate, real-time temperature and relative humidity data to the SNMP monitoring software of your choice.

## Hardware Setup

Configuration of Axe Effect is handled through a serial connection, via the device's USB-Micro port. Connect Axe Effect to a PC using a USB-Micro cable, and use a serial terminal of your choice.

Serial Settings

```
Baud: 115,200
Data Bits: 8
Stop Bits: 1
Parity: None
```

Once the terminal connection is active, press `ENTER` to access the Main Menu.

```menu
(I)nfo
(C)onfig
(F)actory Defaults
(R)eset device
(Q)uit console
```

`(I)nfo` - Provides current running information about the device. This includes current sensor readout, current WiFi configuration and IP address, as well as SNMP and community information.

`(C)onfig` - Device setup. General configuration options for Axe Effect.

`(F)actory` Defaults - Reset Axe Effect configuration to factory defaults. This includes WiFi information, IP address, and SNMP community info.

`(R)eset` device - Reboots Axe Effect. If configuration changes have been made previously without rebooting, changes will take effect after restart.

`(Q)uit` console - Exits the main menu. Log information is displayed with the menu is not active.

## Configuration Menu

`Set Log le(V)el` - There are seven options, with INFO being the default. Logs are displayed in real-time via the serial console, outside of the main menu.

## Network Config

`Set (N)etwork` Name - Enter the SSID of your WiFi access point. Axe Effect Beta currently supports Wireless (802.11n), single-band (2.4 GHz) connections.

`Change WIFI (P)assword` - Enter the authentication password for your wireless network. Axe Effect Beta currently supports WPA2 PSK and WPA3 PSK passwords.

`Set (H)ostname` - Set the NETBIOS Hostname of the device. The default is "AxeEffect".

`(U)se DHCP` - By default, Axe Effect will obtain an IP Address via DHCP. Pressing (U) will enable manual IP address configuration.

`(I)P Address` - Enter your desired IP Address (AAA.BBB.CCC.DDD)

`Net (M)ask` - Enter your desired Netmask

`(G)W IP Address` - Enter your desired network gateway IP address

## SNMP Config

`Set (C)ommunity` - Enter your SNMP v1/v2c community name. Default is "public". Axe Effect Beta currently supports SNMP v1 and SNMP v2c.

`Set System Con(T)act` - Enter the SNMP system contact for Axe Effect. This field is readable via SNMP. Examples: name, email address, phone number

`Set System (L)ocation` - Enter the location of Axe Effect. This field is readable via SNMP. Examples: Homelab Rack, Datacenter, Living Room

`Set System (D)escription` - Enter the description of this device. This field is readable via SNMP.

When you have finished configuring Axe Effect, there are three options at the bottom of the screen.

`(W)rite config to flash` - This writes the current configuration to Axe Effect, but does not reboot. Changes only take effect after the device is restarted.

`Write config and (R)eset device` - This writes the current configuration to Axe Effect and reboots the device. Changes take effect immediately after rebooting.

`(Q)uit to main menu` - Changes to the configuration are ignored, and your are returned to the main menu.

## Firmware Updates

Firmware updates will periodically be made available to patch bugs or add new features.

To flash the firmware on Axe Effect:

  1) Power down the device by removing the USB-micro cable
  2) While holding the firmware flash button on the top case, connect Axe Effect to a PC via a MicroUSB cable.
  3) Axe Effect will appear on your PC as a USB Flash device. Drag and Drop the new firmware file onto the drive (typically a `*.uf2` file).
  4) Once the file is transferred, Axe Effect will automatically reboot.
  5) It is recommended to Factory Reset Axe Effect after updating the firmware, as memory address locations for specific functions may have changed, causing unintended behavior or instability.

## SNMP Information

For temperature data, Axe Effect is using the standard [ENTITY-SENSOR-MIB](https://www.circitor.fr/Mibs/Html/E/ENTITY-SENSOR-MIB.php). It is available by default in most SNMP monitoring software, or can  be added by downloading the `.mib` file from the link.

Temperature is reported via the entPhySensorValue field, using OID `1.3.6.1.2.1.99.1.1.1.4`. Data is reported as a 4-digit value, representing hundredths of a ºC. For example, `2304` would be read as `23.04`ºC.

The ENTITY-SENSOR-MIB contains display configuration, that should be read by most SNMP monitoring software to properly display the temperature. Some software may only read the raw value, and may require adding a custom divisor to the value (val/100). PRTG, for example, displays the raw data without additional configuration. Observium by default will show the properly formatted value.

Over the coming weeks, we are planning on adding specific and detailed instructions for properly reading the sensor data in a variety of SNMP monitoring software.

In a future firmware update, we will be adding humidity sensor readouts in addition to temperature. The sensor will be at OID `1.3.6.1.2.1.99.1.1.2.4.0`, and displays a 5-digit value representing relative humidity in thousandths of a percent. A value of 40525 would be a reading of 40.525% RH.

This OID is NOT a standard component of the ENTITY-SENSOR-MIB, and may require custom configuration in your monitoring software to display. With the upcoming firmware release, we will also be publishing information around supporting SNMP monitoring software.

## Bug Reports

Please report any bugs found to our [GitHub repository](https://github.com/CraftComputing/CraftComputingProjectAxeEffect/issues). Please include the firmware version number in your report, which can be found in the top-left of the Main Menu (ex: `HEAD-61023cf`).
