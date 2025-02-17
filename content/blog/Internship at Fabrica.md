+++
title = 'Intern at Fabrica.AI'
date = 2023-08-31T11:49:22+08:00
draft = false
+++

It was interesting and fun to intern at Fabrica. Being a small startup, work there was very fast paced. Since I did relatively well at the interview, many of the full timers also put more trust and responsibility on me. As such I was able to work on many interesting problems that pushed my knowledge and understanding further. 

During my time there, I helped solve a couple of issues which helped increase the robot's reliability that eventually allowed it to enter into consistent site deployment. 

The biggest issue was electrical noise. The robot was experiencing many random component failures which was suspected to be caused by electrical noise. When the approach of applying general RC filtering didnt help, more investigation was conducted. It was quickly found that the noise was extremely high throughout the whole robot and as such I convinced my boss that a complete reimplementation was required to solve these issues. 

## Electronics redesign
Delving deeper into the design files, I found several issues that were common causes for noise propagation in PCBs. 
1) The main PCB was a 2 layer board despite being relatively complex and large. This meant that there was no solid ground plane beneath the signal traces for a proper low impedance return path. As such the electromagnetic fields would spread very far and the fields of different signals would cross couple causing interference. 
2) Signals were routed very close together, despite ample space for distribution. Ideally traces should be placed 3 trace widths apart for minimal cross coupling between the fields of adjacent traces. 
3) Connectors to daughter board lacked enough direct ground connections. This again causes long return path loops which increase noise. 
4) The robot used brushed motors which were controlled by PWM and were inherently noisy.
5) Switching LED driver layout was not optimal which increases emits more noise.

The full redesign took steps to fix all of these issues
1) Re-route all traces for the mainboard to be on 4 layers instead of 2. 4 Layers allows both inner layers to be full ground planes, additionally the distance between the signal and ground planes is significantly lower in a 4L board than a 2L board(1.2mm vs 0.2mm) reducing the field spread massively. 
2) Routing was done with sound best practices such as spacing traces apart, adding grounding vias beside signal vias, minimising loop inductance.  
3) Where available unused pins were repurposed to become ground pins for daughter board connections. 
4) Power filtering was added to reduce the transmission of switching EMC from the motors to the rest of the system. Adding capacitors to the power path and ferrites to dissipate high frequency noise. Common mode chokes were also explored. 
5) The layout was changed to make switching loop impedance minimization the highest priority. The flyback diode was also changed to a schottky diode to fix another problem with occasional LED driver failures. The external flyback diode used needs to have a lower forward voltage than mosfet body diode, otherwise the body diode is preferentially forward biased and takes all the flyback load. 
6) Additionally by the advice of consultants, harness were redesigned with shielding to reduce EMI from motor cables and improve shielding of signals. This was something I initally totally overlooked as I was too focused on tackling the issues with the PCB. 

I did the bom sourcing and helped to manage the production of this new batch of pcbs which were delivered towards the end of my 3.5 month internship. I was actually quite nervous during this time as I only knew these concepts on a theoretical basis. Up till that point, I havent actually done routing for such a complex system before. I didnt know how much of difference these measures would make in practice. Fortunately after complete testing of the new electronics, my understanding was validated. There was a 4x reduction in noise from the previous design.  

![old loadcell](/old_shieldedharness_duty10_opp.png)
![new loadcell](/newpcb_shieldedharness_duty10_opp.png)
Loadcell readings which are highly sensitive to noise. Old is above and new below. The old design had much larger spread of readings. Below is much cleaner, with occasional far points that can easily be filtered in code. 

## Bug squashing team
The second major contribution was the participation in the bug squashing team. It was composed of full time employees but I was given the privilege to join due to their trust in me. Efforts were focused on investigating the root causes of bugs, proposing solutions, and implementing permanent fixes. This approach aimed at enhancing the overall robustness of the tile grouting robot by addressing underlying technical or procedural issues. Weekly cross-department meetings provided a platform to collectively address more complex problems.

One issue I am particularly proud of was the resolution of a long standing issue with the short lifetime of motor encoders. It was originally thought of as an electrical issue.  But through some discussion and careful observation by the lead mechanical designer, it was eventually identified to be a mechanical misalignment of the shaft and the encoder. Despite this, a good solution was not found as the 3D printed mount used could not be produced with the right tolerance to provide a tight enough fit.  This inspired me to design an adapter PCB with soldered threaded inserts to for the purpose of holding the encoder rigidly and concentrically. The PCB was also used to add ceramic capacitors to help with the ongoing noise issues. Since this PCB was very small and simple, it was also very cheap to produce and provided a more compact mounting solution than before. I felt that this was a very clean solution to a cross department problem that was effectively solved through my participation in the bug squashing team.  

After a period of time, many such issues were resolved which brought the version 4 robot to a state of reliability where multiple robots could be consistently deployed weekly to the construction site. Before it would only be brought there for a week before big demos or for short testing. This gave us valuable insight into the deployment and operational challenges that were not obvious before during short deployments.

![inten_happy](/IMG_20231107_145203.jpg)
