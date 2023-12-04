+++
title = "Singapore Amazing Flying Machine Competition 2021 category D1"
date = 2021-03-27
description = "A victory long time coming"

[extra]
thumbnail = "sadfa"
+++

check date

Where do I even start? Ive been taking part in SAFMC for 8 years at that point in time. Originally in Category C and after that in D1. I am personally very proud of this achievement as it brought together all of the knowledge and skills I have acquired in the years prior. 
\
\
The challenge was similar to that we had been working on for the previous few years, with a couple of notable additions. It goes as follows, 2 teams fly their drones semi autonomously(through FPV systems). They play tic tac toe in real time against one another by picking up beanbags from the starting area and placing them on a grid at the other end of the playfield. 

![safmc playfield](/images/safmc2021_playfield.png)

\
The crucial new additions were that only specific shaped beanbags can claim specific tiles on the tic tac toe grid. Square tiles claim the north south east and west tiles, pyramid beanbags claim the diagonal tiles and the middle tile can only be claimed by the eraser. 
![safmc playfield](/images/safmc2021_tiles.png)

Where I led a team to design a drone system to autonomously pickup payload, and fly through an obstacle course and deliver them to a tic tac toe playfield against opponents in real time. I was the team lead and architected the major systems required to complete the challenge competitively. 1) Including, a lightweight and efficient drone that is capable of operating for 10 minutes while carrying the payload. 2) A companion holonomic platform to perform payload delivery to the drone fully autonomously with failsafe feedback mechanisms. 3) A computer vision system to detect opponent moves and assist the pilot by computing the optimal move to win in the dynamic and unconventional tic tac toe. I was personally responsible for designing and fabricating the drone. This involved CAD and CAM of custom carbon fiber frame, CNC milling of carbon fiber sheets under a flooded work envelope. CNC milling of polycarbonate propguards. Choosing and assembly of appropriate electronics such as power systems and flight controller onto frame. Additionally, total BOM was kept below our team’s $1200 budget as we participated as an independent team and funded the endeavour from our personal savings. 

