# semi_active_rectifier


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


## TODO:

[] Test it
[] Post pics
