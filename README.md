# Toasty


Meet Toasty: The Brave Little Toaster Oven

![Toasty](/images/Toasty1.jpg)  
<p align="center">
  <img src=/images/toasty.gif alt="animated" /> 
</p>

Toasty is an affordable DIY autonomous robotics research platform.  

My long term goal is for Toasty to serve as a long range delivery robot with obstacle avoidance. In the near term, I'm experimenting wtith PointPerfect SSR GNSS corrections from u-blox to achieve cm level accuracy.

Pre-fabricated robotics platforms that can carry heavy loads over long distances are quite expensive. Cost effective Motors, Motor Controllers, and Frames are tough to find. Toasty is an budget, eco-friendly alternative, leveraging recycled materials and the following projects:

For brushless motor control, I referenced the excellent work of lucysrausch in hacking a hoverboard as a cost effective brushless motor solution.
Hoverboards are quite powerful. Most are capable of supporting 200 lbs (90kg) with a top speed of 25 mph (40km/h) and up to 10 miles (16 km) of range with some reprogramming.  
https://github.com/lucysrausch/hoverboard-firmware-hack  
Her repo also contains some examples of projects others have created using hacked hoverboards  

EFeru further modified this code base to include FOC control, offering smoother control and higher speeds.  
https://github.com/EFeru/hoverboard-firmware-hack-FOC  

Randy Mackay's contributions to ArduRover made this project a breeze. Configuring Ardupilot for rover use is documented in detail on the official website.
Link to his YouTube channel with some tutorials:  
https://www.youtube.com/channel/UCm393BzMOyRPUo8MtKp5alg  

The best part of using these components is that minimal programming and configuration is needed to get started.

Hoverboards are out of style and sell for pennies on the dollar on ebay, craigslist, and facebook marketplace. I regularly find listings for $30 boards.
How can you beat a 10S Protected 4.4Ah 36V battery pack with a Charger, Battery Management System, two brushless 350W motors, and a frame capable of carrying 200lbs (90kg)?

The toaster oven is a sturdy aluminum enclosure that requires only basic tools to teardown and modify. You can find these used for $10-15. 
Aluminum extrusions just aren't as fun.

## Bill of Materials:

| Item  | Estimated Cost | Vendor
| ------------- | ------------- | ------------- |
| **Minimum BOM for RC control** |  | 
| Hoverboard | $20-60 | Plenty of used products on FB Marketplace, Craigslist, Ebay, etc.
| Toaster Oven |  $15 | Plenty of used products on FB Marketplace, Craigslist, Ebay, etc.
| Several 3D Printed mounts and enclosures (STL files included in repo) |  $5 | /3D_Prints
| 2x 2in Swivel Casters| $5 | https://www.harborfreight.com/material-handling/tires-casters/swivel-casters/2-inch-x-7-8-eighth-inch-light-duty-swivel-caster-41518.html  |
| RC Receiver for manual control and Arming (FS-iA6B)  | $12 | AliExpress, Amazon
| RC Controller or PS4 controller for manual control (FS-i6X)  | $40 | AliExpress, Amazon
| **Required for autonomous operation** |  |
| Ardupilot compatible flight controller w/ GNSS,Compass | $45-200+ | I used a Pixhawk 4 mini from Sparkfun. I can't vouch for the boards from AliExpress, but there are some lower cost options available. More options available here: https://ardupilot.org/rover/docs/common-autopilots.html#common-autopilotsSparkfun
| Telemetry Radio (BLE or SubGhz)  | $20 | Sparkfun, Amazon, Ebay
| **Optional for enhanced autonomous functions** |  |
| u-blox ZED-F9P/F9R High Precision GNSS Receiver (ZED-F9R also integrates Dead Reckoning)  | $150+ | Future, Digikey, Holybro, Ardusimple, Sparkfun
| Ultrasonic Sensors  | $10 | Sparkfun, Amazon, Ebay
| Cellular Modem for remote control  | $65+ | Sparkfun, Hologram
| Lidar or ToF camera  | TBD | TBD
| Raspberry Pi | $30 | https://www.raspberrypi.com/products/raspberry-pi-4-model-b/

## Block Diagram
![Block Diagram](/images/BlockDiagram.png)  

## Build

Here is an outline of the steps I followed using a Pixhawk 4 mini, Ardupilot,  and a hacked hoverboard. Depending on your choice of controller, you may need to make some modifications.

**Step 1**: Disassemble your hoverboard and Follow instructions on Feru's repo to flash the MCU. Make sure you pick the appropriate input. If you are using Ardupilot like me, select PWM input  
https://github.com/EFeru/hoverboard-firmware-hack-FOC  

**Step 2**: I removed the motor mounts and bolted them directly into the frame of my toaster. This required a couple 3D printed spacers. You may need to get a little creative here, as hoverboard mounts have different geometries and some may require more effort to combine with the toaster frame.
![Toasty](/images/Toasty2.jpg) 

**Step 3**: I 3D printed a few enclosures and mounts for the electronics. See /3D_Prints. I also crimped some custom dupont connector cables to interface between the motor controller and hall sensor cables.
![Toasty](/images/Toasty3.jpg) 

**Step 4**: Test with an RC receiver - Channels 0,1 can be connected directly to the hoverboard motor controller using Pin x for speed and pin x for steering. Place toasty on an elevated surface so the wheels can move freely and ensure throttle and steering are functioning as expected.
![Toasty](/images/Toasty8.jpg) 

**Step 5**: Follow the Ardupoilot Rover steps outlined here: https://ardupilot.org/rover/docs/gettit.html  

**Step 6**: Connect the Pixhawk to the motor controller as shown on the block diagram. I've uploaded a 3D printed mount for the pixhawk in the repo. For convenience, I used velcro to secure the device to the top of the oven compartment.
![Toasty](/images/Toasty5.jpg) 
![Toasty](/images/Toasty9.jpg) 

**Step 7**: Place Toasty on an elevated surface again to safely perform some motor tests. At this stage you should have already performed the RC controller calibration and set the rover to mode x. You're ready to go on your first mission!
![Toasty](/images/toasty4.jpg) 

**Step 8**: Test manual control and follow tuning steps as outlined in Randy's videos here:

https://www.youtube.com/watch?v=mV9Dxp1PX-8  
https://www.youtube.com/watch?v=9zOlvTsHY6k  

**Step 9**: Configure ardupilot to prioritize the appropriate external GNSS. Set up and calibrate magnetometers, and object avoidance sensors. Details are outlined in the ardupilot rover documentation: 

https://ardupilot.org/rover/docs/common-gps-for-yaw.html  
https://ardupilot.org/rover/docs/common-object-avoidance-landing-page.html  

![Toasty](/images/Toasty6.jpg) 
![Toasty](/images/toasty_ardupilot.png) 

## Tips

- Configure maximum setpoints for throttle and steering if using Ardupilot.
- Follow all local laws and regulations for autonomous and remote control vehicles. Test and make configuration changes in an open area away from obstacles. Maintain line of sight.

## To do:
Add obscacle avoidance via Lidar, ToF camera  
Include ROS node for indoor navigation  

## Links:
https://github.com/pixhawk/Hardware/blob/master/FMUv5/Pixhawk4-Pinouts.pdf  
https://www.thingiverse.com/thing:100486  
