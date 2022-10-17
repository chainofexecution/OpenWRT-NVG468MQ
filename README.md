# Installing OpenWRT on the Arris NVG468MQ Modem

I've seen a lot of requests for OpenWRT support for the NVG468xx. This router is commonly available, quite capable, and supports some interesting features like MoCA. I happen to have a spare one of these so I figured I'd give it a go at installing OpenWRT on it and post the results.

## The Teardown
I'm going to speedrun the teardown as most routers are pretty similar (especially ISP modems like these) and we should get all the info we need from serial output anyways.

There is one Torx T7H screw on the back of the modem as well as two Torx T7H screws hidden underneath the rubber feet on the bottom side of the modem.

After the three Torx screws are removed you should be able to wedge a separation tool (like a spudger or black stick) into the crease between the two sides of the plastic shell and separate them by releasing the plastic clips holding them together.

Once the device is open, take note of the orientation of the antenna wires connected to their respective U.FL connectors on the sides of the board and then disconnect them.

Flip the board over and get out your soldering iron and flux.

Headers were soldered to the SoC UART as well as the ethernet controller UART (it turns out a serial connection to the ethernet controller was entirely unnessecary and I would only add headers to the SoC UART if following this writeup)

The pinouts are conveniently silk-screened on the PCB so we don't have to bother with checking voltage on the pins using a multimeter.

There is also a JTAG port you could tap into but I will avoid using it for this writeup as UART easier to use and the goal of this write up is to make the OpenWRT install process for this router to be as accessible as possible.

I have routed some jumper wires through the top side of the case so I can access the UART with the device sealed up.

Now we connect the pins to a UART capable adapter. I will be using my personal favorite serial adapter; The Adafruit FT232H, which is an excellent FTDI breakout board that supports a wide array of protocols like UART, SPI, I2C, GPIO, and even JTAG.

