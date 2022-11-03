# Assessment of OpenWRT support for the Arris NVG468MQ Modem

I've seen a lot of requests for OpenWRT support for the NVG468xx. This router is commonly available, quite capable, and supports some interesting features like MoCA. I happen to have a spare one of these so I figured I'd give it a go at installing OpenWRT on it and post the results.

## The Teardown
I'm going to speedrun the teardown as most routers are pretty similar (especially ISP modems like these) and we should get all the info we need from serial output anyways.

There is one Torx T7H screw on the back of the modem as well as two Torx T7H screws hidden underneath the rubber feet on the bottom side of the modem.

After the three Torx screws are removed you should be able to wedge a separation tool (like a spudger or black stick) into the crease between the two sides of the plastic shell and separate them by releasing the plastic clips holding them together.

Once the device is open, take note of the orientation of the antenna wires connected to their respective U.FL connectors on the sides of the board and then disconnect them.

Flip the board over and get out your soldering iron and flux.

Headers were soldered to the SoC UART as well as the ethernet controller UART (it turns out a serial connection to the ethernet controller was entirely unnessecary and I would only add headers to the SoC UART if following this writeup)

![IMG_20221017_005913](https://user-images.githubusercontent.com/92492482/199830727-56748c72-4854-4521-b05d-21e8281f98a1.jpg)

![IMG_20221017_005917](https://user-images.githubusercontent.com/92492482/199830746-1796d8de-27e5-48d8-ab18-7001b771fc5b.jpg)

The pinouts are conveniently silk-screened on the PCB so we don't have to bother with checking voltage on the pins using a multimeter.

![IMG_20221017_011332](https://user-images.githubusercontent.com/92492482/199830840-cf6f3115-d225-4afb-8f89-0f31c11bae34.jpg)

I have routed some jumper wires through the top side of the case so I can access the UART with the device sealed up.

![IMG_20221017_013344](https://user-images.githubusercontent.com/92492482/199831092-bde3717a-b709-4f93-81b2-255c00f6cfc0.jpg)

Now we connect the pins to a UART capable adapter. I will be using my personal favorite serial adapter; The Adafruit FT232H, which is an excellent FTDI breakout board that supports a wide array of protocols like UART, SPI, I2C, GPIO, and even JTAG.

The next step is to review these bootloader logs for things like chip identifiers, drivers and kernel used, flash size/speed/partitioning, and other data to assess OpenWRT compatabillity for the router.
