+++
title = 'Electrical Engineer at Fabrica.AI'
date = 2024-12-31T11:49:22+08:00
draft = false
+++

During my ![Internship at Fabrica.AI](/internship-at-fabrica), I also participated in the planning for the next robot version V5. The primary purpose of V5 was to increase the modularity of the robot such that each module could be replaced without influencing other modules. This was done so as decouple the development of the modules such that incremental upgrades could be done instead of having to embark on a costly and risky full redesign every year. It is meant to be the overhaul to end overhauls. At the same time, electrically the major changes would be 
1) a shift to brushless motors
2) the consolidation of most daughter PCBs into the main PCB
3) Further reduction in noise and increase in reliability.
During my time as an intern, the company was tried to find a suitable full time electrical engineer to do bring V5 into fruition. But after months of searching were still unable to find someone. As such, my boss Jakub decided to offer me the position instead. This meant that I would have to take a year off my studies. Despite some resistance from family and friends, I eventually decided to take on the offer. I felt like it was a good opportunity to take a break from the one and done style of school projects. This job would allow me to dig deeper into the world of electronics, finding root cause of issues and understanding the fine details of real world design. And indeed it did! 
## Shift to brushless motors
I proposed the shift to brushless motors because when paired with good drivers that output sinusoidal waveforms, they would produce less EMC and EMI as compared to brushed motors. There is also the added benefit of much higher power density which allows for higher operating speeds which a secondary goal of V5. I helped to look for a cost effective supplier that offered drivers which communicate by a differential signal such as RS485, CAN Bus or Modbus. We ended up settling on Kinco as they were cost effective and offered a CANbus solution. 

## Consolidation of PCBs
The V4 electronics box was composed of many sub pcbs. Their physical arrangement and mating was also sub optimal, interfacing at different layers and at orthogonal angles with headers. This not only made electrical signaling poor due to large ground loops but also mechanical interfacing with the enclosure poor as the stacking of multiple boards made tolerancing poor. By consolidating the boards it would also made assembly simpler.  
![[IMG_20240220_172147.jpg]]
comparison of V4 and V5 PCBs and electronics drybox.

## Further reducing noise and increasing reliability
After the experience of partially redesigning V4 and characterizing its performance, I strove to further improve the design for V5. 
One particular area of noise emission that was particularly interesting to tackle was the LED driver. Although, I did optimise the layout in V4, I could tell it was still a source of noise that was influencing components around it. Using the spectrum analyser with H and E field probes, there were clearly emissions coming from the led drivers. With the oscilloscope, 300mV Vpp spikes occurring at the switching frequency ~550kHz are clearly visible. 
![led spikes](/led_spikes.png)
![spike close](/spike_close.png)

It took awhile to understand the issue, but with the help of LTspice simulation, I finally found out that the schottky diode I was using had a very high junction capacitance. The junction capacitance acts like a short circuit to ground for a short instant when the LED driver's mosfet turned on. The larger the capacitance, the larger the current spike, this spike then induces ringing with the other circuit parasitics. A new diode was chosen with a much lower capacitance and paired with RCD dampers to absorb the residual oscillations, much better performance was recorded. 
![led_after](/led_after.png) ![](/led_after_close.png)

Another interesting design challenge was the hotswap controllers for the motor driver power supply. It is a high side controller IC that drives an N channel mosfet to provide protection features such as OCP, OVP, ULVO and softstart. Initial design was relatively easy and the first revision worked as expected. However, 1/5 boards encountered an issue where the mosfet died right before robot commissioning. I replaced the mosfet and carried on but a couple weeks later it happened again. This called for a deeper investigation which lasted a month. I made many measurements with the oscilloscope to ensure that there were no voltage spikes, gate ringing, etc. Finally, it was found that the SOA of the mosfets were not good enough. Specifically at the spirito effect region of high Vds and high current that occurs during startup. Due to that mosfet being older and more optimised for fast switching, the current ability at high Vds was only 2A. When measured, the startup current was ~20A for about 100us. A new mosfet was chosen, a gate capacitor was added to linearise the inital capacitor charging which solved the issue. 

## Production of first V5 robot in Shenzhen

After the initial design phase was complete, it was time for the final production and assembly of the V5 robot. Since I was decently proficient not only in electronics design but also mechanical and had some experience in software, I was designated to fly to china for 2 weeks to oversee the production of the first V5 robot. Collaborating with the mechanical and software team back in Singapore, I helped to resolve design issues, alleviate production bottlenecks and documented the assembly process for further review. 

This information was then used to update the design with design for manufacturing and assembly in mind. I also proposed optimisations to the assembly instructions to reduce assembly error and improve consistency. I was then given another opportunity to oversee the production of the last few robots in the second production run. Due to the improvements in design and assembly processes, this run was much smoother. Delivery was on time, final assembly and integration in Singapore took only 2 days compared to the weeks it took for the robots in the first run. 

![Shenzhen](/shenzhen.jpg)

All in all I found my experience as an electrical engineer at Fabrica very rewarding, it has increased my interest to dive deeper into electronics engineering.

