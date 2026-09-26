# DAY 1

Today, I spent the entire time researching and configuring components on kicad. I did the research part off camera. I was initially planning to use the Rockchip RK3566 processor but it was lacking a proper datasheet so transitioned over to a more open Allwinner T527 processor. This thing has a great documentation and its cheap too!

For the RAM, I was honestly so confused between so many different choices. With the ongoing rammagedon, I though the prices would be crazy but I was shocked on seeing a 16Gb chip for as low as $49 on lcsc. It's cheap, right?

Notice anything? I wrote 16"Gb" and not "GB". This was the entire source of my confusion. Turns out 16Gb is actually just 2GB of ram. So yeah $49 definitely pretty expensive for 2GB of ram ;-;

I decided to go with the SAMSUNG K4F6E3S4HM-THCL. Its a pretty popular chip for embedded systems. Then, started wiring the DDR4 ram. I thought it would be hard af but wiring it up was just connecting similarly named pins from the CPU and on the RAM chip. With that, I finished the task!

https://lapse.hackclub.com/timelapse/3uVjpeV-KdUG

# DAY 2

Today was spent on more wiring. But I wired up the power management ic (PMIC) today. Turns out every different cpu has a whole different PMIC! I thought of using the same PMIC as used in the rk3566 but turns out it was incompatible. So, the compatible chip for the Allwinner T527 processor is the AXP717 PMIC.

Then I wired the PMIC according to the datasheet application. Its still a bit confusing but I think chatgpt or claude and elaborate it for me, if I'm unable to comprehend the datasheet contents. I also wired up power for the processor. It had a lot of different voltage requirements but i guess that's what the PMIC is supposed to be used for instead a billion different voltage regulators.

https://lapse.hackclub.com/timelapse/Uc_4LHCtApbX

# Day 3

Today I added wired connectivity to the board. I added stuff like 1 ethernet, 2 usb-a ports, 1 usb-c port, 2 camera connectors, 1 debug terminal, and 1 hdmi output port. The one that was the most confusing here are the camera connectors. We originally planned for 2 cameras (3 now) and I thought that there were enough pins on the cpu for it, but even using the MIPI DSI from the datasheet, there aren't enough pins for 2 cams. So, I'll need to figure something else out tomorrow for 3 cams.

I literally had to change the camera connector pinout 3 times bc for the first time, I thought we were going for a raspberry pi style camera so I copied that pinout. That was wrong. We changed the camera and I didn't look for the specifics of the camera we'd use. So, I thought copying a standard MIPI camera pinout was a good idea. Not a good idea again. The camera my teammate chose was the most niche camera I've ever seen. Then, I copied the final pinout for that specific camera.

Finally, I also added the micro-sd card memory section. Idk why but I went with stacked USB-A ports like a raspberry pi. Probably because it saves space. I forgot what I was thinking then.

https://lapse.hackclub.com/timelapse/OWU4e0SMXuE3
