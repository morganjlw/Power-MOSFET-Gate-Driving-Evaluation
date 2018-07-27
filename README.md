# MOSFET Gate Driving Design Analysis

MOSFET Gate Driving design is analyzed using theoretical calculations and supported by simulations. 

This gate drive design is controlled by an isolated PWM output. Code for Arduino, Raspberry Pi, and STM MCU implementations is provided. 

## MOSFET

Quickly turning on and off a MOSFET is achieved by quickly charging and discharging the gate. MOSFET input capacitance is described by the following equivalent circuit and corresponding equations. 

![](https://github.com/morganjlw/MOSFET-and-IGBT-Gate-Driving/blob/master/mosfet.JPG)

<img src="https://latex.codecogs.com/gif.latex?C_{iss}&space;=&space;C_{gs}&space;&plus;&space;\frac{C_{gd}C_{gs}}{C_{gd}&space;&plus;&space;C_{gs}}\approx&space;C_{gs}&space;&plus;&space;C_{gd}&space;\:[\mathrm{F}]\\&space;\indent&space;Q_{g}&space;=&space;V_{GS(th)}C_{iss}&space;\:[\mathrm{C}]\\&space;\indent&space;I_{Gate}&space;=&space;\frac{Q_{g}}{t_{d(on)}}&space;\:[\mathrm{A}]&space;\\" title="C_{iss} = C_{gs} + \frac{C_{gd}C_{gs}}{C_{gd} + C_{gs}}\approx C_{gs} + C_{gd} \:[\mathrm{F}]\\ \indent Q_{g} = V_{GS(th))}C_{iss} \:[\mathrm{C}]\\ \indent I_{Gate} = \frac{Q_{g}}{t_{d(on)}} \:[\mathrm{A}] \\" />

As an example, we will analyze designing a low-side switch with the Internation Rectifier IRLZ24N using (di/dt) and (dv/dt) protections (RCD networks not considered).   

![](https://github.com/morganjlw/MOSFET-and-IGBT-Gate-Driving/blob/master/images/mosfet.JPG)

Some relevant IRLZ24N performance figures are included below:

![](https://github.com/morganjlw/MOSFET-and-IGBT-Gate-Driving/blob/master/IRLZ24Ndatasheetfigures/figures1and2.JPG)

![](https://github.com/morganjlw/MOSFET-and-IGBT-Gate-Driving/blob/master/IRLZ24Ndatasheetfigures/figures3and4.JPG)

![](https://github.com/morganjlw/MOSFET-and-IGBT-Gate-Driving/blob/master/IRLZ24Ndatasheetfigures/figures5to8.JPG)

The component datasheet shows that (though vary depending on Drain-Source Voltage and other parameters):

<img src="https://latex.codecogs.com/gif.latex?C_{iss}&space;=&space;480&space;\:\mathrm{pf}&space;\\&space;\indent&space;Q_{g}&space;=&space;15&space;\:\mathrm{nC}&space;\\&space;\indent&space;V_{gs(th)}&space;=&space;10&space;\:\mathrm{V}&space;\\" title="C_{iss} = 480 \:\mathrm{pf} \\ \indent Q_{g} = 15 \:\mathrm{nC} \\ \indent V_{gs(th)} = 10 \:\mathrm{V} \\" />

Assuming we require the gate to charge in 20 ns, we can derive the gate drive current requirement:



Assuming we overdrive the Gate voltage to ~15V to ensure saturation and we are switching at 10kHz:



Totem-pole drivers are first considered, though specialized integrated are readily available in the market. A totem-pole configuration consists of NPN and PNP transistors connected in series by their Emitters. 

![](https://github.com/morganjlw/MOSFET-and-IGBT-Gate-Driving/blob/master/images/totempoledrive.jpg)
