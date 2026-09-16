---
board: ESP32-C6-DevKitC-1
group: boards
---

The IoT-LAB testbed provides access to the
[Espressif development boards](https://www.espressif.com/en/products/devkits). 

ESP32-C6-DevKitC-1 is an entry-level development board based on ESP32-C6-WROOM-1(U), a general-purpose module with a 8 MB SPI flash. This board integrates complete Wi-Fi, Bluetooth LE, Zigbee, and Thread functions.

<div style="text-align:center">
<img src="{{ '/assets/images/docs/boards/esp32-c6-devkitc-1/' | relative_url}}esp32-c6-devkitc-1.png" style="width:300px;"/>
</div>

## Datasheet and documentation

You can find a lot of documentation on the
[Espressif website](https://docs.espressif.com/projects/esp-dev-kits/en/latest/esp32c6/esp32-c6-devkitc-1/user_guide.html#hardware-revision-details). 

## Firmware compilation & flash

The device cannot yet be flashed directly when starting an experiment. You must first start the experiment, then flash the device afterward. The flashing process currently requires a single merged .bin firmware image flashed at address 0x0.

This means you need to merge the different ESP32 binaries into a single binary before using the IoT-LAB flashing command.
`esptool` provides a merge_bin subcommand for this purpose.
The easiest way to generate the correct command is:
Flash a device once in verbose mode to see the esptool `write_flash` command used internally.

Adapt this command for `merge_bin`:

Replace `write_flash` with `merge_bin`
Remove the options:
`--port, --baud, --before, --after, and -z`
Add:
`-o <output_merged.bin>`

You can then use the generated merged binary with IoT-LAB flashing.

## IoT-LAB special configuration

The serial connection baudrate should be configured at **115200 bauds** in the
firmware.

The UID of the node corresponds to the MAC Address of the Wi-Fi radio chip in station mode.

