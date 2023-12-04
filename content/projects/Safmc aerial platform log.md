+++
title = "SAFMC 2021 Aerial platform"
date = 2021-03-27
description = "Robustness Robustness Robustness"

[extra]
thumbnail = "sadfa"
+++

In parallel with the CV and docking system work, I was personally working on the drone itself and the payload delivery system. The key idea with the whole delivery system was ROBUSTNESS. During a competition, the pilot is under extreme stress, pilot attention and cognitive load is a precious resource. As such, as many failure modes must be identified, risks minimized and contingencies put in place. Nothing should be left to chance to secure victory. 
\
\
With that in mind, I decided to containerize the payloads such that the 3 payload types can be handled universally. One limitation was that the payload had to be delivered free from any foreign objects. Therefore, the container had to release the payload cleanly. We decided to use an electromagnet on the drone to attach the container. The container in turn would have its own self contained power circuity to open trap doors that release the payload. This was triggered by the drone wirelessly using an optocoupler style setup where a led on the drone would light up triggering an ldr on the container. To increase robustness, the system would not only calibrate to ambient light levels at startup, but also use a crude encoding method to send trigger signals. The led will pulse very quickly and the logic on the container looks for large absolute changes in brightness. This way the possibility for false positives was minimized. I even accounted for the possibility that the propellers spinning under bright overhead illumination would emulate the pulsing signal. This scenario was tested showing a large margin of error. 
\
\
From here on there were many other automatic checks implemented for both pilot error and malfunctioning systems. 

- interruptor beams to check for beanbag proper beanbag deployment 
- enstop to check for proper reception of container from delivery vehicle.
\
\
This actually worked during the competition itself where the electromagnet was unable to successfully attract the payload container during one of the rounds. Thanks to the check, my teammate was alerted of this failure and was able to reinitiate the docking sequence successfully. Otherwise, we would likely have lost a whole cycle of time. 
\
\
Finally, we have the drone itself. By this point I was very experienced with building drones, as such this part was quite a breeze. I sized the propellers, motors, ESC, and batteries appropriately for the drone to fly for 10 minutes, the maximum duration of the challenge. In reality this was way overkill as we would expect most fights to last less than 4 minutes if all our systems operate as expected. Regardless, I chose low pitch large diameter propellers and lithium ion 18650 batteries. These are geared for efficiency rather than raw speed and power as the challenge takes place indoors though an obstacle course limiting max speed. The frame was custom designed and milled out of carbon fiber sheets underwater. It nicely incoporates holes and mounts for all devices such as electromagnets with an optimised shape. 

![safmc body](/images/cf_body.jpeg)
![safmc frame](/images/safmc_frame.jpg)


The propellers were protected by custom milled durable and light polycarbonate sheets in the same way as the mecanum wheel. They are milled in one piece with "fingers" that get bent up to to form a cage, providing a higher degree of protection.

![pc propguards](/images/pc_propguards.jpg)
