+++
title = "SAFMC 2021 docking"
date = 2021-03-27
description = "now kiss"

[extra]
thumbnail = "sadfa"
+++


The next major challenge was the task of picking up the beanbags without human intervention. From our experience in prior years, landing a drone precisely enough to pick up objects is difficult. Its doable but even for a skilled pilot, it takes time to line up well. Basically we needed a system that can allow the pilot to land with lower precision, and then maneuver to align with the payload afterwards. 
\
\
I had several ideas for this problem. Each with their own pluses and minuses. 
1) an xy plotter integrated into the drone frame. Drone can land roughly on top of the payload and the toolhead will drag it back to the center. Downsides, drone carries significant dead weight half the time. 
2) holonomic wheels on the legs of the drone that allow the drone to drive over the payload. Downsides, drone carries some dead weight, less elegant solution, basically a hybrid car. 
3) A large kinematic coupling landing pad that couples with the drone's legs, elegant solution. Downsides,  provides smaller tolerance of landing precision. 
4) A holonomic drive delivery vehicle that allows the drone to land arbitrarily and subsequently mates with it to deliver the payload. Elegant solution, large landing tolerance, no dead weight. Downsides, difficultly of execution. 
\
\
Our team decided to pursue the kinematic coupling as it was theoretically the most elegant solution. 

![dock closed](/images/kinematic_dock_closed.jpeg)
![dock open](/images/kinematic_dock_open.jpeg)

One major obstacle to the realization of any of our ground based solutions was the challenge's limitation of ground aids to be smaller than 150x150x100mm. 
\
\
The drone's wheelbase itself was already larger than 150mm. This meant that the 4 quadrants of the landing pad would have to expand outwards in order to align with the legs of the drone. Even then, the tolerance of landing area would only be 75x75mm. I 3d printed a simple practice pad to practice landing while world on the expanding mechanism was still in progress. This proved too small for me to stick the landing in good time. 
\
\
As such, I iterated on this design by extending the quadrants with foldable flaps. These would fold up for storage and drop down once the landing pad expanded for deployment, extending the landing area by about 50mm on each axis. Even still, I was unable to stick landings consistently on the first try. Additionally, the expanding mechanism now required a triple expanding joint and was bordering on exceeding all dimension limits. 
![flaps dock](/images/dock_with_flaps.jpg)
\
\
After the 2 weeks of pursuing this approach, I discussed the challenges and results with my team and we decided to abadon the idea in favour of the holonomic drive delivery vehicle. This was significantly more complex as it would involve not only building the vehicle platform, but also a docking system. However, this method potentially provided one of the largest tolerance to landing among all proposed strategies. 
\
\
The main design constraint was again trying to keep the vehicle under the 150x150mm size limit. The second softer constraint was to maintain a profile as low as possible so as to minimize the height of the drone. We started off by buying mecanum wheels from AliExpress and modeling the vehicle based off that in concert with hobby servos that were modified for continuous rotation. This provided an extremely low platform for the payload to sit. The preliminary design was printed for a test fit with the payload carrier. Unfortunately, the carrier was just sightly too big for the current design but there was no way the carrier could be shrunk more. Thus, my teammate and I spent the next week redesigning and machining the hub of the mecanum wheels to shave off 2mm off either side. 

insert mechanum videos and pics
\
\
With the vehicle platform complete, we turned our attention to the docking system. My plan was to use a 2 stage system. First, when the drone initally lands, the car gets it's relative position to the drone by locating an aruco code stuck in front. This would allow it to use the mecanum wheels to manuvure the car right to the front of the drone and face the correct orientation. At this point, the aruco marker would no longer be visible therefore the car would transition to using an ir beacon system to perform final precise alignment and entry under the drone. 
\
\
My teammate got to work on this system while I continued to work on the drone itself. During this process, there was a slight setback where we were unable to get the aruco marker detection to work reliably in all lighting scenarios due to our inexperience in computer vision. We did try a couple of things to correct the problem but were unsuccessful. Dispite that, we carried on with the ir beacon system and found it to be more flexible than expected. It was able to both correct the orientation and translation of the drone from as far as 30cm. The only downside was it is unable to correct for errors greater than about 30 degrees in a cone spreading out from the front of the drone. With some inital flight testing, we deemed this satisfactory as even I could land it precisely enough for docking to occur on the first try.  
insert docking videos