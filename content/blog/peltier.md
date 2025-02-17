+++
title = 'Peltier 3D Printer Bed'
date = 2022-10-01T11:49:22+08:00
draft = false
+++

This was a small project I did for thermodynamics module in Y2 of Uni. The premise is simple, heated beds of printers need to be heated for optimal printing quality. To perform their function properly, they have to be constantly heated for long periods of time, however long the print is. This is compounded by the size of the heated bed or if it is used to heat the chamber as well. A print could easily last 12h and draw around 50-100w. Sure, insulation may help but nothing beats a little heat pump action! 

Heat pumps as their namesake, use some energy to move heat from one place to another. This allows them to achieve >100% efficiency with respect to the electrical energy input into the device. I decided to use a peltier as the heat pump. Although it only has a COP of ~2 compared to full cycle compressors, it is compact and easy to work with. The timeline for this project was only about 2 weeks which would make it unrealistic to integrate more sophisticated heat pumps. A peltier is also more compact and has an ideal form factor to fit onto a heated bed. The idea was that instead of using the peltier to provide cooling like it's usually used, I can use the other side to heat the heated bed. 

Here comes the most elegant part about this idea, the cold side of the peltier can be used to cool air for various parts around the printer that requires cooling! There will be a heatsink on the cold side of the peltier to aid in heat transfer into the device. Air will be blown over it to further increase efficiency, that colder air can then be used to cool electronics or channeled to the part cooling duct. 
![elegant meme](/elegant_meme.png)

The actual design and construction of the project was fairly straightforward. I drew up a CAD model of the device, an aluminum plate (100x100mm) identical to that of my old 3d printer acts as the heated bed. An adheasive sticker is placed on top to ensure equivalent thermal properties. To spread the heat from the 40x40mm peltier over the whole bed area, 4 heatpipes are placed diagonally. An aluminum spacer the thickness of the heatpipes and size of the peltier is used for increase contact area. Finally, below that is the peltier and its heatsink on the other side. A radial fan blows air over the heatsink in a duct. 

The aluminum plate and spacer were cut on the waterjet in school. The duct was 3d printed on my printer. All that was left was a little assembly with screws and thermal paste at every interface to ensure proper heat transfer. This was fairly straightforward and took about a day. Afterwhich, my team and I moved on to testing of the device in comparison with a normal heated bed. 
![peltier bed](/peltier_bed.jpg)
![peltier thermal](/peltier_heating1.jpg)

The test setup was as such, I would power both devices at 100W to heat up to operating temperature of 60c. Then the power would be reduced to the level which with it would be at steady state. This power level would be used to compare both devices. 

Unfortunately, the peltier heater was not more efficient then the normal resistive bed. The measurements of power consumption was close enough to be within margin of error. After the initial disappointment wore off, I reflected on why this could be the case. I surmised that it was because the conduction from the hotside of the peltier to the cold side would causes the majority of the losses in efficiency. This would be especially pronounced at steady state as the heat would have plenty of time to propagate back. The ideal solution to this would be to use a different heat pump such as a compressor cycle heat pump. This would completely decouple the hot and cold sides preventing parasitic backwards heat transfer. 

![peltier thermal](/peltier_sandwich.jpg)
![peltier thermal](/peltier_heating2.jpg)


To validate this hypothesis and salvage the project, we decided to compare the 2 systems in a fastest time to heat test instead. Both devices were heated at the same power of 60W and the time taken to heat to 60 degrees from room temperature was taken. This way, conduction effects would be less dominant vs the heating effects. Fortunately, this hypothesis proved to be correct and the peltier heater heated significantly quicker(X) than the resistive bed (X). We presented our findings to our professors in the final presentation where we did well because of the novel idea which appropriately implemented concepts from the course content. (We got 9/10🎉). 

In reflection, it was quite a fun project that has a very interesting premise. As usual it was held down by sub optimal implementation. It was a good proof of concept though. I did know about issues of peltier having back conduction problems but didnt know how much of a problem that would or pose. The interesting thing about this project is that the larger the scale, the more it makes sense. With a large printer it then becomes feasible to be use compressor cycle heat pumps that will work effectively. Especially with extremely large format 3D printers becoming available and popular such as >600mm cube volumes, not only does the power draw and thus the potential savings increase, the print time also scales up dramatically. At my current internship office the bed of the Modix printer 600mm cube printer uses a 1kw ac heater. Imagine the savings! 
