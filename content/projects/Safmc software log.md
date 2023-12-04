+++
title = "SAFMC 2021 software log"
date = 2021-03-27
description = "Fix hardware problems in software heh"

[extra]
thumbnail = "sadfa"
+++

Although these changes seemed small, they present huge challenges in regards to the strategy of playing the game. Because only certain beanbags can be used to claim certain tiles, there can exist certain edge cases where due to the unpredictability of the opponent's move, our move in progress could be nullified. This is particularly likely in a closely matched game. Let me explain in an example. Say we are the slightly faster team by 20%, however we would not know this before the game starts.  Therefore of the 2 optimal starting moves of taking the corner or center, it would he prudent to pick the corner. 
\
\
We would then proceed to return to home and pickup a x beanbag with the intention to claim y box next. However, during this process, the opponent played suboptimally and chose tile z. In a normal game of tic tac toe, we would respond with taking tile A. However, due to the interesting mechanic of SAFMC TTT being non turnbased and information incomplete, we would only find out the opponent's move after having chosen the wrong beanbag and travelling to the playfield. At this point we would have to ditch the carried beanbag and travel back to the start to collect the appropriate beanbag. In the process we would not only lose our hard earned advantage but possibility even fall behind the opponent. 
\
\
Essentially the problem boils down to this, the feedback loop between information aquisition and decision making based on said information is delayed. Making decisions based on this outdated information could in certain cases cause us to lose a game. 

With that the solution is clear, we need real time information on the changes to the playfield, even when our drone is physically away. The simplest solution would be to have another camera at the playfield streaming live video. However, this is prevented in the rules, as we were only allowcated 1 FPV channel and additional video transmitters are prohibited. 
\
\
 After some brainstorming with my partner, I we came up with 2 viable solutions. The first would be a turret at the playfield which would dispense pucks with downward facing color sensors. The second would be a computer vision solution. Since neither of us had the experience with computer vision, we naturally gravitated towards the puck dispenser. However, after communicating with the organizers, to our dismay, they decided that no foreign objects were allowed on the TTT board.  
\
\
Thus we had no choice but to pursue the CV method. I contacted a classmate and arranged for him to join our team. Since it was the height of COVID-19 lockdowns, I made a fully functional 1/3 scale model of the TTT grid and setup the vpn infrastructure for our 3rd member to work remotely. 
![CV](/images/safmc_plain_grid.jpg)

Although I had a limited understanding of the details of the implementation, we worked closely to investigate different setups, testing edge cases and fine-tuning. We were able to complete a pretty robust system in good time. 

![CV2](/images/beanbag_close.jpg)
![CV2](/images/beanbag_far.jpg)

![CV](/images/cv_grid.jpg)


