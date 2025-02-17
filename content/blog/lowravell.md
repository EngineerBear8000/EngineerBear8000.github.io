+++
title = 'Split Wireless Keyboard'
date = 2021-01-31T16:03:17+08:00
draft = false
+++

Awhile back I fell into the rabbit hole of mechanical keyboards and as it goes when I fall, I fall in DEEP. Fortunately, this was actually a blessing this time. The journey of most who catch the bug starts out with gaming keyboards which progress to mechanical keyboards. Then they might buy kits or keycaps and switches to make a custom keyboard. Still others design their own keyboards. Then there's q further niche of ergonomic keyboards, starting with ortholinear keyboards, split keyboards and then split ortho column staggered keyboards. 

![winnie the pooh meme](/keyboard_meme.jpg)

At each step along the way adventurers usually buy a keyboard, only to discover the next level down, or up? And desire a keyboard of the next tier, always chasing the endgame keyboard. I instead took the express train down to hell and decided to go from a free membrane keyboard to a keyboard with the most keywords, a custom designed split wireless ergo low profile column staggered keyboard. 👍

The idea was that at the time, there were barely any split keyboard that was low profile but also wireless. I only found 1 such board called the caravell, it however used the nrf series of chips which during the great chip shortage of 2021 was backordered on all major distributors for months. This promoted me to think of the ESP32 family of chips. They have built in Bluetooth and we're widely supporte, which made me wonder why nobody has made any keyboard with these chips. Granted their efficiency is lower than the nrf family, but for a keyboard I didn't mind chucking in a 18650 and calling it a day.

Additionally the second major motivation for pursuing this project was my desire to improve my pcb design skills. Up till then, I had only designed small and relatively simple pcbs. Mainly breakout boards that used through hole components. I had watched many videos on SMD pcb design and therefore felt decently confident that I had the required knowledge to avoid any major pitfalls and rookie mistakes. However, nothing beats real experience. So I also treated this project as a learning experience and was willing to spend more money to invest in myself. A functional product would be the cherry on top. 

I started this project as I do any project, copious amounts of research. I cloned the caravell github and looked at the general layout and architecture. I didn't really like that it was powered by coin cells and wanted a USB rechargeable device. I targeted my next area of research to battery powered microcontroller projects. Also with it being battery powered, I wanted to have as low sleeping power or quiescent current consumption as possible. I found this video series by Andreas Speicess on esp32s and battery powered boards particularly informative. 
https://youtube.com/playlist?list=PL3XBzmAj53RnZPeWe799F-uoXERBldhn9&si=yjhQitq0VkORwanx

He goes through many important considerations when designing a battery powered microcontroller board and has a super handy spreadsheet of boards and they're quiescent current consumptions. From that list, I inspected the schematics of the boards with the highest efficiencies to figure out what chips they use. For example, the choice of LDO is especially influential on the deep sleep efficiency.  From here, I also copied the schematics of various essential blocks of components such as usb to uart chips, dual power source switching circuits etc. 

I was hoping to find a LDO that was already used in an existing board which I could copy wholesale as I initally didn't have the confidence to select the appropriate supporting passives. I looked through a couple boards but many of the popular chips used were out of stock during the chip shortage. Eventually, I found a video by Phil's Lab which explained well how to select LDOs and construct the circuit. Afterwhich, I quickly found a suitable chip from the thousands available on mouser and digikey. 

The next major block is the ESP32 microcontroller with usb to uart chip, which was easier than usual because the ESP32 WROOM module already incoporates the crystal oscillator for the clock, the only things required were reset/boot buttons. The usb to uart block was easily lifted from other opensourced boards such as adafruits feather series. I used the cp2104 which was extremely popular with other boards. The block includes BJTs to automatically put the ESP into boot mode for programming and reset upon completion. 

The last major block was the battery charging circuit. This, I set out to design from scratch because chips and boards commonly used in hobbyist projects only had charging currents up to 1A. In an era of fast charging, how can we be content with anything less than 2A? Even if it was overkill for keyboards, it's a matter of personal pride for me. I looked on digikey and easily found the MP2615. Which could do 1 or 2 cell charging. It even has presets for me to adjust the max voltage to 4.1 instead of 4.2 volts for battery life preservation. I rewatched a bunch of videos on buck converter design and layout to refresh my memory on switching converter design. Afterwards referring to the datasheets application note and suggested layout, I constructed the circuit in kicad. 
![lowravell_schematic](/lowravell_schematic.png)

After all these, it was simply a matter of connecting all blocks together. I took the caravell switch layout and increased the pinky row stagger to a full row instead of half as i felt that it was more ergonomic that way. From my research, half row pinky staggers were decended from a direct flattening of originally curved and raised ergo keyboards. I replaced all the diodes in the matrix to be SMD diodes and rerouted the matrix for the practice.  
![lowravell_layout](/lowravell_layout.png)


Finally, I sent the board to JLCPCB for production, ordered the BOM from digikey and some low profile choc switches. Keeping with the theme of ergonomics, I ordered light 35g linear switches. 

While waiting for the production of the actual PCBs, I made a simple breakout board for the ESP32 dev board to a keyboard matrix. I used this to work through the firmware setup. I decided to try a port of the most popular keyboard firmware QMK for ESP32s called MK32. The official project had very limited support for wireless chipsets and only supported for the nrf series at the time. It required some finagling to get working as it was an unmaintained project. What worked in the end was using the docker image to get a specific version of ESP32IDF and flashing a particular board configuration. 

After the pcbs came, I assembled the board but realised that i messed up in a couple of places. None were super critical but required buying new components. 

1) I accidentally used a totally different footprint for the LDO on the actual PCB. I initiated put a different schematic symbol as a placeholder and only renamed it but didnt change its associated footprint. 
2) The current shunt resistor was 0.1 Ohm vs 50mOhm. That made the battery charging current only 1A. The ic I bought was a slightly different variant in the same series that used a 50mOhm reference instead. Variants matter! 
3) The Schottky diode I choose for the power switching between usb and battery power was a signal diode not a power diode. The high resistance caused battery power to not work as the voltage drop across it was too high. 
4) I somehow bought the wrong size inductor. No explanation. 

Its ok lessons learnt, in fact I was lucky that the errors didn't cause require a new board order. I was fully expecting to have to do that. With some minor surgery and a little jank soldering, most major blocks worked. I could flash firmware onto the board, it connects by Bluetooth and actuates keys. Only the battery power didnt work because I only figured out the diode problem later on. I then bought new chips with the correct specifications and resoldered them for a completely functional board.

![lowravell](/lowravell.jpg)