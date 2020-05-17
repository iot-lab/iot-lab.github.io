---
board: IoT-LAB M3
group: boards
---

The IoT-LAB M3 board has been designed specially for the IoT-LAB testbed. It is based on a STM32 (ARM Cortex M3) micro-controller with an ATMEL radio interface in 2.4 GHz and 4 sensors. In terms of dimensions, it has a form factor (i.e. the CAD design of the embedded system) of 4 cm wide and 5 cm long.

<div class="row mb-3">
    <div class="col-12 col-lg-6">
        <img class="img-fluid" src="{{ '/assets/images/docs/boards/iot-lab-m3/' | relative_url }}m3-impl.png" />
    </div>
    <div class="col-12 col-lg-6">
        <img class="img-fluid" src="{{ '/assets/images/docs/boards/iot-lab-m3/' | relative_url }}m3-impl2.png" />
    </div>
</div>

## MCU
The IoT-LAB M3 board takes its name from the **CPU** it is equipped with: the [Cortex M3](https://developer.arm.com/ip-products/processors/cortex-m/cortex-m3) manufactured by [ARM](https://www.arm.com). The Cortex M3 is a 32-bit CPU set to a maximum speed of 72 MHz. The Cortex M3 is integrated into the STM32 **MCU** ([<i class="far fa-file-pdf"/> STM32F103REY]({{ site.baseurl }}{% link assets/misc/docs/iot-lab-m3/stm32f103re.pdf %})) manufactured by [STMicroelectronics](https://www.st.com/), more commonly known as ST. The STM32 MCU is equipped with 64 KB of **RAM** and 256 KB of **ROM**. An example of a connected object employing the use of this same MCU is the Apple TV 4 remote control.

## Radio chip
The radio chip [<i class="far fa-file-pdf"/> AT86RF231]({{ site.baseurl }}{% link assets/misc/docs/iot-lab-m3/AT86RF231.pdf %}) manufactured by [Atmel](https://fr.wikipedia.org/wiki/Atmel) (purchased in 2016 by [Microchip](https://www.microchip.com)) communicates over the 2.4 GHz ISM frequency band. This radio chip was designed to implement the MAC layer of the IEEE 802.15.4 standard, used by the Zigbee communication protocol, among others. The maximum bandwidth is 256 kbits/s. A small, 9 mm long ceramic antenna is welded onto the circuit. This type of radio technology falls into the “short-range” category, with maximum distances of 40/50 meters indoors and up to around 100 meters outdoors. Depending on these technical specifications, the radio chip consumes up to 14 mA when transmitting at maximum power. It is interconnected with the MCU on the SPI bus, enabling rapid data exchange. It is also connected to a GPIO port on the MCU in order to control the waking up of the radio chip in the event of it being set to standby mode.

## External NOR flash memory
A 128-Mbits external NOR flash memory (N25Q128A13E1240F) is connected to the MCU via the SPI bus in order to enable rapid data transfer. This memory is useful when it comes to storing data acquired by sensors while a program is running. Another use case is for OTA (Over The Air) updates to the MCU’s firmware. Some embedded operating systems
partition this ROM memory in order to download and store different versions of the firmware.

## Sensors
4 sensors connected to the MCU via the I2C bus are embedded into the IoT-LAB M3 board:
- the **light** sensor:
  this measures ambient light intensity in lux.
  [<i class="far fa-file-pdf"/> ISL29020]({{ site.baseurl }}{% link assets/misc/docs/iot-lab-m3/ISL29020.pdf %})
- the **pressure** and **temperature** sensor:
  this measures atmospheric pressure in hPa.
  [<i class="far fa-file-pdf"/> LPS331AP]({{ site.baseurl }}{% link assets/misc/docs/iot-lab-m3/LPS331AP.pdf %})
- the **accelerometer/magnetometer**:
  this provides feedback on an object’s acceleration, and can be used to detect movement. By determining a threshold, it generates a change of state on one of the MCU’s digital inputs/outputs in order to create an interrupt, which can be used to bring the MCU out of standby mode.
  [<i class="far fa-file-pdf"/> LSM303DLHC]({{ site.baseurl }}{% link assets/misc/docs/iot-lab-m3/LSM303DLHC.pdf %})
- the **gyroscope**:
  this measures the orientation of an object in space and can be used, for example, to determine the orientation of the screen of a tablet or a smartphone.
  [<i class="far fa-file-pdf"/> L3G4200D]({{ site.baseurl }}{% link assets/misc/docs/iot-lab-m3/L3G4200D.pdf %})

## LEDs
3 LEDs (red, green and orange) are connected to the MCU via the digital inputs/outputs. Usually, these are used to notify of MCU actions or application states. Even if you use the boards remotely, do not hesitate to use the LEDs as usual; it sometimes gives us an interesting visual feedback of users activity, like this one observed in 2017.

<div class="col col-lg-6 offset-lg-3">
    <video autoplay muted loop class="embed-responsive-item" width="100%">
      <source src="{{ '/assets/images/docs/boards/iot-lab-m3/' | relative_url }}bradbury.mp4" type="video/mp4">
      <img src="{{ 'assets/images/docs/boards/iot-lab-m3/' | relative_url }}bradbury.jpg" class="img-thumbnail">
    </video>
</div>

## Power supply
The M3 node can be supplied in 3.3 V in two different ways:
- via the USB port
- via the external battery

In terms of the energy consumption of the different hardware devices, it should be noted that, at full power, the MCU consumes 14 mA, to which we must add the energy consumption of the other hardware devices. The radio chip, for example, consumes 14 mA when transmitting and 12 mA when receiving.

Typical use cases for constrained connected objects often require the use of a battery. In order to maximise the lifespan of objects, the energy-saving strategy employed involves switching the MCU and its various different components to standby mode once the object has finished processing. In the
case of the STM32 MCU, consumption is reduced to 1 mA when in sleep mode, and remains below 1 μA in standby mode. The AT86RF231 radio chip supports the same type of features, with comparable energy savings.

## Programming
You can reset, debug and program the STM32 on JTAG through the FTDI4232H connected to the USB. This component allows also a UART link to the STM32.

## Architecture

<div class="col col-lg-8 offset-lg-2" markdown="1">
![]({{ '/assets/images/docs/boards/iot-lab-m3/' | relative_url }}m3-archi.png){: .img-fluid }
</div>

[<i class="far fa-file-pdf"/> Complete schematics](http://github.com/iot-lab/iot-lab/wiki/Docs/iot-lab-m3-schematics.pdf)<br>
<small>* Note that the second UART on Open Node connector is not useable (wires RX an TX inversed).</small>

## Testbed integration
The Open Node connector gives access to 3 STM32/GPIO and the STM32/I2C. Two power lines are accessible on this connector :
  * a + 5.0 volts for the board power supply
  * a 3.3 volts for the consumption monitoring of the STM32, the RF component and the sensors

interaction w/ Control Node?
{: .text-warning }
