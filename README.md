# semi_active_rectifier

![schematic](https://raw.githubusercontent.com/kopchik/semi_active_rectifier/master/pics/schematic.png)
![naked pcb](https://raw.githubusercontent.com/kopchik/semi_active_rectifier/master/pics/pcb.png)
![assembled board](https://raw.githubusercontent.com/kopchik/semi_active_rectifier/master/pics/assembled_board.jpg)
![assembled board from back](https://raw.githubusercontent.com/kopchik/semi_active_rectifier/master/pics/assembled_board_back.jpg)

Losses on a conventional diode bridge rectifier a quite high due to a large drop on diodes. This have the following consequencies:
1. A lot of heat dissipation. This prohibits compact and efficient devices.
1. Reduced output voltage due to two-diode drop.

The best solution would be to an LT4320 circuit that uses fets to rectify the signal. The circuit present here is somewhat less efficient, it lies somewhere in between an LT4320 rectifier and a diode bridge. There are two optimizations done:
1. Using FERD diodes instead of conventional diodes noticeably lowers power dissipation due to lower voltage drop (~0.55V@30A). This contributes ~0.8W (each) of heat dissipation under 3A load.
2. Using two n-fets that shunt two lower diodes, thus dissipating only ~0.35W (each, according to simulation).

Total calculate heat dissipation is 2.3W@25C. I expect the actual dissipation to be lower due to heating (hot ferd/shottkey diodes conduct better).
In comparision, a bridge made of silicon diodes would dissipate about twice more power.

The pcb has a GBU-like shape.

## Some caveats and precautions

1. Not all fets are born equal. The peak current can be more than 30A (inrush current). Most sot23 fets cannot handle that (according to soa). The good news is, the dropout on a mosfet cannot be more than ~0.6V in this circuit because they are shunted by diodes. Still, I decided to use mosfet in powerpak package because they can handle more abuse.
2. Mosfet should be reasonably low Vgs(th), or it will not work well for low voltages.
3. Due to high peak currents (~20A), a mosfet should have Rds(on) of less than some 30mOhm, otherwise most of current will go through the diode. In other words, mosfet drop under peak current should be less than drop on the diode.
4. There's still quite a lot of heat to dissipate. I tried to make the pcb in such a way that it works as a heatsink.
5. My DMM couldn't test FERD diodes. Presumeably due to high leakage.


## Evaluation

I did a quick measurement with DC current.

1. Below 2V input, when fets are closed, the measured dropout of two diodes was 0.6V, the maximum temperature was about 75C on free air. 
   Calculated power dissipation is 1.2W, which is I'd say maximum for this tiny board.
2. At 4V, the measured dropout was 0.295V on a diode, and 0.07V on mosfet. Dissipation: 0.73W. Tolerable :). Calculated Rds(on) of mosfet is 33mOhm. It seems 4V of Vgs is not enough to fully open it as it's supposed to have Rds(on) of less than 15mOhm.
3. A jelly-bean GBU module measured 1.6V drop at 2A, which gives 3.2W dissipation. Meh :(


## Conclusion

The approach has proved to work :)
