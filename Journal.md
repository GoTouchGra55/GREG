# Week 1

## DAY 1

Today, I spent the entire time researching and configuring components on kicad. I did the research part off camera. I was initially planning to use the Rockchip RK3566 processor but it was lacking a proper datasheet so transitioned over to a more open Allwinner T527 processor. This thing has a great documentation and its cheap too!

For the RAM, I was honestly so confused between so many different choices. With the ongoing rammagedon, I though the prices would be crazy but I was shocked on seeing a 16Gb chip for as low as $49 on lcsc. It's cheap, right?

Notice anything? I wrote 16"Gb" and not "GB". This was the entire source of my confusion. Turns out 16Gb is actually just 2GB of ram. So yeah $49 definitely pretty expensive for 2GB of ram ;-;

I decided to go with the SAMSUNG K4F6E3S4HM-THCL. Its a pretty popular chip for embedded systems. Then, started wiring the DDR4 ram. I thought it would be hard af but wiring it up was just connecting similarly named pins from the CPU and on the RAM chip. With that, I finished the task!

https://lapse.hackclub.com/timelapse/3uVjpeV-KdUG

## DAY 2

Today was spent on more wiring. But I wired up the power management ic (PMIC) today. Turns out every different cpu has a whole different PMIC! I thought of using the same PMIC as used in the rk3566 but turns out it was incompatible. So, the compatible chip for the Allwinner T527 processor is the AXP717 PMIC.

Then I wired the PMIC according to the datasheet application. Its still a bit confusing but I think chatgpt or claude and elaborate it for me, if I'm unable to comprehend the datasheet contents. I also wired up power for the processor. It had a lot of different voltage requirements but i guess that's what the PMIC is supposed to be used for instead a billion different voltage regulators.

https://lapse.hackclub.com/timelapse/Uc_4LHCtApbX

## Day 3

Today I added wired connectivity to the board. I added stuff like 1 ethernet, 2 usb-a ports, 1 usb-c port, 2 camera connectors, 1 debug terminal, and 1 hdmi output port. The one that was the most confusing here are the camera connectors. We originally planned for 2 cameras (3 now) and I thought that there were enough pins on the cpu for it, but even using the MIPI DSI from the datasheet, there aren't enough pins for 2 cams. So, I'll need to figure something else out tomorrow for 3 cams.

I literally had to change the camera connector pinout 3 times bc for the first time, I thought we were going for a raspberry pi style camera so I copied that pinout. That was wrong. We changed the camera and I didn't look for the specifics of the camera we'd use. So, I thought copying a standard MIPI camera pinout was a good idea. Not a good idea again. The camera my teammate chose was the most niche camera I've ever seen. Then, I copied the final pinout for that specific camera.

Finally, I also added the micro-sd card memory section. Idk why but I went with stacked USB-A ports like a raspberry pi. Probably because it saves space. I forgot what I was thinking then.

https://lapse.hackclub.com/timelapse/OWU4e0SMXuE3

## Day 4

Today I cleaned up the camera config. Yesterday, I had cheated a bit by only making one camera functional and the other pretty much disabled. So, I added a multiplexer so that I could switch electronically between the two cameras. This was very simple to add as all the pins were pretty much self-explanatory on the MUX.

Then, I added the connectors for all extra devices to be used with the rover. I added connectors for a LiDAR, a 5" LCD display, 6x ToF sensors, and a breakout. For the 5" lcd, I had to use a separate regulator for the backlights and I also had to use another multiplexer for the ToF sensors as using up that many I2C pins would be painful to route and redundant. After that, I cleaned everything up and fixed any erros that I had made.

Finally, I've finished the schemati- SHIT. I forgot the motor driver section. Tomorrow, I'll work on the motor drivers then.

https://lapse.hackclub.com/timelapse/n_8mE_Owrke_

## Day 5

Today, I've planned to make the schematic for the motor driver. Hopefully this doesn't take too long. So, I started off with cubemx. I had to use an stm32g4 series mcu because, I really didn't want this driver to be on the SBC. That would make the sbc way too cluttered and also noisy. So, I setup some pins and timers in cubemx. It was around this time that something crashed on the system and the recording was stopped. So, I just have a random 10min lapse.

https://lapse.hackclub.com/timelapse/YH5z8TwuD9Iz

Then, I opened up kicad and set up the mcu with decoupling capacitors, reset circuitry, crystal, etc. After that, I added a drv8262 motor driver. I used this because it supported two motors instead of just one. That would mean I'd have to use only 3 of these for the 6 planned motors. The first symbol I imported for the driver was very confusing to me, so i replaced it with a "better" version.

Even after that, it took me a lot of time to figure out the pinouts. The board had multiple pins with the same name. I figured out that it was to accomodate for the huge current requirements for the motors. Also, the driver had a different pinout for single and dual motor modes. I had added some incorrect configs in cubemx, so retraced my steps and reconfigured the project. Next, it was pretty much smooth sailing. I added the power circuitry from an old project as it had a pretty similar power i/o requirement. I eventually added the CAN to both the stm32 and the t527.

Then, I changed the 2x18 pin connector to a 2x19 pin version to include the two CAN pins. Finally, I assigned the footprints to both the driver and the driver. I realized that a couple of the footprints were missing models, so i manually assigned models to those. With that, I concluded the schematics for the SBC + Motor Driver. I'll be routing the pcbs in the following week!

https://lapse.hackclub.com/timelapse/VLZOeNz0L1pe

# Week 2

# Day 1

Firstly, I added M2 mounting holes and also fixed some footprint issues for the motor driver. After that, I did some decoupling capacitor placement for the mcu. I also routed the localized sections together and used copper pours for the parts expecting high currents. That's basically all of what I've done today.

https://lapse.hackclub.com/timelapse/X0dPpF9x8SwO

# Day 2

Today, I planned out the placements for the motor drivers. It was tedious due to the oddly long nature of the motor connectors. I put them vertically on each other as horizontal would take too much space. This looks pretty good tbh. After that, I placed remaining motor driver components like the decoupling caps, resistors, bulk capacitor, etc. Then, I connected some of the localized components together with the whole board.

https://lapse.hackclub.com/timelapse/TpOebbLc9Wzu

# Day 3

Today, I connected the motor drivers to the mcu itself. Previously, it was only routed locally. After that, I cleaned up some of the older routes. I also figured out that I had accidentally mixed up the internal power supply to the external through a silly error. So, I fixed that and also fixed the corresponding routes.

https://lapse.hackclub.com/timelapse/athXvKkx-Ld6

# Day 4

Today, I connected the motor encoders to the mcu. This also resulted in some revised routes. After that, I had to resolving some plane issues. Then, I moved over a few sections to make the board more compact as it was just way too big and scattered. The motor driver is now complete.

https://lapse.hackclub.com/timelapse/TlkEq0aHov0p

# Day 5

Today, I started work on routing the sbc itself. This was very confusing as I've never worked with an sbc before. I tried to use vias but they didnt really want to work. So, I found out that I was supposed to use micro vias. I also tried to connect long distance traces together but later changed my mind as I don't think that it's a good idea. I'd rather keep the traces short and tidy instead of long and weird. Then, I followed a similar concept in the ram. I only routed together the grouped components. Gonna do more work tomorrow.

https://lapse.hackclub.com/timelapse/h11k2Ic1V0Ab

# Day 6

Today, I wired up some local routes in the sbc. I wanted to start with the RAM but as a beginner to custom sbc designs, shits pretty intimidating yk. So, I routed the ethernet section first. Then, I routed up some crystals and finally the SD card memory section. I wanted to keep the labels at first so I spent some time "prettyfying" the component placements, but then later changed my mind as it took too fricking long to do and imo just looked trash.

https://lapse.hackclub.com/timelapse/Ca1tS8nBZieB
