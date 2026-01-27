---
title: Oscilloscope Probes
authors:
  - name: Nathanael (Nat) Fortune
    affiliation: 
    - id: sc_physics
      institution: Smith College
      department: Department of Physics
      city: Northampton
      region: Massachusetts
      country: USA
#            postal_code: 01063
#            phone: +1 (413) 585-3980Department of Physics, Smith College 
    
date: 2026-01-26
abstract: |
  We investigate how and when you need to correct for the low pass filtering of voltage signals introduced by the finite impedance and capacitance of oscilloscope input channels. 
---

# Probes and Impedances

## a quick review of what probably already know about oscilloscopes 

An oscilloscope is a visual voltmeter. Like a handheld battery-operated multimeter, an oscilloscope can measure the electric potential difference $\Delta V$ — the `voltage` — between two different points in an electrical circuit.  The advantage of the oscilloscope over the handheld multimeter is that it can capture and visually display time-varying signal $\Delta V(t)$, and can do so up to very high frequency. If the signal repeats periodically, the oscilloscope can *trigger* off an identifying feature of the signal so as to keep that particular feature at the same point on the oscilloscope screen, thereby producing a synchronous display. 

Unlike a handheld multimeter, however, we are making a `single-ended measurement`, not a `differential measurement`. That is, to measure the voltage *across* a circuit element using the multimeter, we place the tip of the + probe of the voltmeter in contact with one side of the element and the tip of the - probe on the opposite side. Neither probe needs to be in contact with the point of the circuit designated as $V = 0$ — the `circuit ground` — to measure the differential voltage $\Delta V = V_+ - V_-$, and because the voltmeter does not have an explicit ground, it is said to be *floating*.   

The + tip of an oscilloscope probe is likewise placed in electrical contact with a point of interest for the circuit but the negative tip — often terminated in the form of a wire attached to a small aligator clip — is grounded, forcing $V_- = 0$.  The ground is made at the connection of the probe to the oscilloscope. This connection is usually a coaxial connector, with the inner wire corresponding to $ V_+$  and the outer locking connector corresponding to $V_-$. This {underline}`simplifies` the math — $\Delta V = {V_+ - V_-} = V_+ - 0 \equiv V(t)$ [^OneWireVoltmeters],  — but it {underline}`complicates` the measurement, because we have now made the oscilloscope part of the ground return for the electrical circuit! 

What is more, the oscilloscope inputs do not function as ideal voltmeters with infinite impedance.  To a function generator, a typical oscilloscope input looks like a 1 M$\Omega$ resistor in parallel with a small capacitor. This is typically in the range of 5 - 25 pf;  the input capacitance of an R&S RTB20204 oscilloscope is 19 $\pm$ 2 pf (in parallel with the 1 M$\Omega$ resistance). 

[^OneWireVoltmeters]: Alas, this prevalence of single-ended measurements for which $\Delta V(t) = V(t)$  has induced {underline}`confusion` in generations of *electrical engineers, who often graduate thinking a voltage measurement refers to a single point in a circuit (instead of being the potential difference between that point and ground). On their circuit diagrams, the ground wire (or ground plane) disappear (sometimes replaced by a ground point), oscillators, voltmeters, and oscilloscope channels have but one wire connected to the circuit, and power inputs (including grounds) for op amps disappear completely! 

       ![MokuGoLockIn!](./images/OneWireOscillatorsAndVoltmeters.png)
       
       As *physicists*, we know better, but the mistake is understandable: if the oscilloscope ground is already connected to the circuit ground in some other way, you don't even need to connect the alligator clip serving as a ground reference wire to the circuit (and might even use a probe without one)! 

::::{dropdown} Motivating Exercise: High frequency square waves
:open: 

How does the finite impedance of the oscilloscope input affect what is measured for a high frequency square wave? Can we correct for that? 

```{exercise} 
:label:ringdown


Configure a function generator to output a 1 MHz 0 to +5V square wave [^0_5V], then connect it to an input channel of your oscilloscope. You should see a signal like the figure below. Compare it to a 1 kHz square wave, then switch back. 

Notice that at the higher frequency, (a) the rising and falling voltages of the square wave are no longer instantaneous and (b) there are brief oscillations following each voltage step. 


![Direct measurement of 1 MHz signal using 1 Mohm impedance oscilloscope input](./images/Direct_connection_at_1MHz.PNG)


Hey: Is your voltage measurment off by a factor of 2? If so, your function generator is probably set to 50 $\Omega$ or "low-Z" [^50_ohm] instead of  "high Z" [^high_Z].   The 50 $\Omega$ option assumes the function generator will be connected to a circuit or instrument with a 50 $\Omega$ impedance input; the high-Z option assumes it will be connected to a circuit or instrument with an infinite impedance through which no current flows (an ideal voltmeter). The input impedance of an oscilloscope is finite[^finite_impedance] rather than infinite but it is much closer to that of an ideal voltmeter than a 50 $\Omega$ resistor. Change output options[^output_options] and try again! 

[^0_5V]: If using the internal function generator in an R&S RTB2004, select a 5 Vpp square wave then add a + 2.5V dc offset. 

[^high_Z]: function generators don't actually measure the amplitude of the output voltage. Instead, they assume you will connect the output to the input of an instrument (or circuit) with a known impedance. The most common assumption is infinite impedance ("high-Z"), but many modern function generators give you a 50 ohm option as well. Be sure to check! 

[^50_ohm]: Some instruments (e.g. photomultipliers) require that instruments connected to them (such as oscilloscopes or counter-timers) have a 50 ohm impedance. Setting the function generator to 50 ohm allows you to use it to simulate a photomultiplier (or similar instrument) but you still need the connection to your oscilloscope or counter-timer to terminate in  50 $\Omega$ impedance.  One way to do this is to connect a BNC  "tee" connector to the oscilloscope channel input, connect one of the two remaining inputs to the signal cable and the other to a 50 ohm "terminator". This puts the 1 M$\Omega$ impedance of the channel input in parallel with a 50 ohm resistor, effectively reducing the impedance seen by the signal source to 50 ohm. 

[^finite_impedance]:A typically oscilloscope input behaves as if it has a  1 Mohm resistor plus a small capacitance in parallel with the voltmeter input. In the low frequency limit, this corresponds to an impedance of 1 Mohm. This is much closer to infinity than it is to 50 ohms, so we should select "high-Z" as our option. At high frequency, the capacitance lowers the effective impedance. Can you think how we might correct for this? 

[^output_options]: If you are using the R&S RTB2004 internal function generator, you can see if the generator is set to 50 $\Omega$ or "high Z" by looking to the right of the `Gen` touchscreen button at the bottom of the display. 

**Question**: What kind of circuit could lead the distortion of the square wave signal seen following each change in oscillator voltage from 0 to +5 V (and again from +5 V to 0)? 


:::{hint} Hint 1: time delay
:class: dropdown
 draw the circuit created by connecting the function generator to the input of the oscilloscope. Include the effective resistance and capacitance of the voltage input for this non-ideal voltmeter. 
 
What kind of filter does this behave as: low-pass or high-pass? Explain why. 
 
How will that affect the time response to high-frequency transients such as the steps in voltage for a square wave?  
:::

:::{hint} Hint 2: oscillations
:class: dropdown
Now add an inductor in parallel with the RC circuit. This creates a circuit with a resonant frequency Under what circumstances does voltage across the RC circuit oscillate?  
:::



```
````{solution} ringdown
:label: ringdown-solution
:class: dropdown
Without the inductance, we have an RC low-pass filter with a cutoff frequency of $f_c = \frac{1}{2\pi RC}$. For the R&S RTB2004, $f_c = 8.4 kHz$ ! 


When we add inductance, we have a resonant circuit with a resonant frequency $f_r$ given by 
$f_r = \frac{1}{2\pi \sqrt{LC}}$ . For the R&S RTB2004, this resonant frequency is 115 MHz. 






![RLC_circuit](https://techweb.rohm.com/wp-content/uploads/2025/06/05_parallel_rlc_circuit.webp)

````

:::

   


:::::{attention} How an oscilloscope probe connects the oscilloscope to the circuit





::::{tab-set}
:::{tab-item} 1:1 probe 
:sync: tab1
 ![1xprobe!](./images/1xProbe.png)


:::
:::{tab-item} 10:1 probe
:sync: tab2
 ![10xprobe!](./images/10xProbe.png)
:::
::::

:::::

To make a *differential measurement* across a circuit element for which neither end is at ground, you need a two channel oscilloscope — each channel is a single-ended voltmeter — and two independent voltage probes: connecting the + tip of the first  oscilloscope probe to one point of the circuit, the + tip of the second oscilloscope probe to another point of the circuit,  connect the first probe to channel 1, connect the second probe to channel 2, and then finally mathematically calculate the difference $V_2(t) - V_1(t)$. This is because connecting $V_-$ of an oscilloscope to a point on the circuit that isn't ground would immediately tie that point to oscilloscope ground, shorting the circuit and changing the voltage $\Delta V$ you wanted to make.  

Alternatively, you can connect the two probes to a differential amplifier to do the subtraction electronically, then connect its output to a single channel of the oscilloscope.  

Technically, it doesn't have to be an oscilloscope probe. It could just be a coax cable with a BNC coax connector on one end and two wires with alligator clips on the other. Functionally, this is the same as a `1x oscilloscope probe`. 

## measuring changes what is measured! 

A fundamental rule of experimental physics is that measuring changes what is measured. In quantum physics this is fundamental to our understanding of the Schrödinger wavefunction as a linear superposition of observable states, but it is no less true on a practical basis in a lab measuring the temperature of a superconducting transition with a platinum resistor, the lifetime of a muon undergoing radioactive decay inside a plastic scintillator, or the electric potential difference — the voltage! — between two points in an electronic circuit. 

Sending electrical current through a Pt resistive thermometer to measure its temperature dependent resistance warms the thermometer, inserting a plastic scintillator into the path of a passing negatively charged muon to detect the muon's arrival and decay changes how long the muon lasts,  and connecting the  finite 1 M$\Omega$ 35 pf oscilloscope input t to measure the time varying volage across a circuit element alters the shape and size of the signal that is measured! 

There is a difference of course — a quantum measurement typically changes the physical state of what you are measuring while a classical measurement typically does not induce a phase transition in a material (unless you are trying to — so our focus is usually on reducing these systematic errors to a level significantly smaller than the variation in signal we are seeking to measure. This is what textbooks and theorists refer to as an "ideal" measurement, one for which we can either ignore or correct for the influence of the measurement instrument on what we measure. 


