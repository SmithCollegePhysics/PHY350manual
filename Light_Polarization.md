---
title: Polarization of light
keywords: ["dc drift", "regulated power supply", "constant current", "constant voltage", "multimeter", "lock-in amplifier", "polarization"] 
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

  - name: Joyce Palmer-Fortune
    affiliation: sc_physics
  - name: and you! 
    affiliation: sc_physics
    
date: 2026-01-26
abstract: |
  We use measurements of the polarization of laser light to introduce some of the challenges involved in making stable dc measurements and some common solutions. 
---

# Setup and Introduction 

In this experiment we will use a diode laser emitting 650 nm red light in combination with a photodiode-based photodetector measuring  light intensity to study light transmission as a function of polarizer angle.  This is an interesting measurement on its own but it is also the first step in investigating Faraday rotation: using a magnetic field to change the polarization angle of polarized light [^Faraday_rotation]. 

## power regulation of laser diodes

Unfortunately, laser diodes are often annoyingly unstable, as small changes in the electrical current supplied to the diode can lead to large changes in output intensity. Small changes in temperature can also produce fluctuations in laser frequency (and intensity), a phenomena known as "mode hopping."  

The figure below illustrates how the output power of the laser (intensity/area) and hence the laser light intensity varies as a function of current through the laser diode.

```{figure} https://cdn1.byjus.com/wp-content/uploads/2022/10/Characteristic-curve-of-laser-diode.png
:label:diode_power
:alt: laser diode power as a function of current
:width: 500px
:align: center


Laser output power as a function of electrical current. [image source](https://byjus.com/physics/laser-diode/)
```



We won't try to control diode temperature today, but we can work to control the input power supplied to the laser diode. The challenge here is that laser diodes are diodes, not ohmic resistors, so some thought is needed as to how to best stabilize the electrical power provided to the laser.  As you can see from the figure of The laser diode requires the voltage across the diode to be above a particular "threshold voltage" before current will flow through the diode --- something necessary for it to output light --- but once above that voltage, a small increase in voltage leads to a large increase in current. 

```{figure} https://components101.com/sites/default/files/inline-images/Graph-between-forward-voltage-and-forward-current.jpg
:label:diode_IV_curve
:alt: a typical current-voltage curve for a 650nm laser diode.
:width: 500px
:align: center


a typical current-voltage curve for a 650nm laser diode. The voltage must be above a threshold value of about 1.8 V before  current starts to flow.  [image source](https://components101.com/diodes/laser-diode-650nm)
```




```{exercise} 
:label: diode-resistance

1. Describe how the absolute resistance $R = V/I$ and  differential resistance $dR = dV/dI$ vary as a function of current for a diode (for currents above zero). 
2. What problems does that pose if you want to stabilize the electrical power $P = VI$ supplied to the diode?  

```

```{solution} diode-resistance
:class:dropdown
:open: false

Discuss this with your lab partner and instructors, then enter your description and thoughts about this into the Jupyter notebook you are using as a notebook for this lab! 
```
```{exercise} 
:label: regulated-power-supplies

Suppose you have an option of controlling either the supplied current or the supplied voltage and can do so within 1%. Which would be the better choice if you want to stabilize the electrical power provided to a laser diode? 
```
```{solution} regulated-power-supplies
:class:dropdown
:open: false

As before, discuss this with your lab partner and instructors, then enter your choice into the Jupyter notebook you are using as a notebook for this lab. 
```
In the next sections, we provide instructions on how to control either the voltage or the current supplied to the laser diode, depending on your preference. 
  
[^Faraday_rotation]:This phenomena was the first indication that light might be an electromagnetic field and is now used to make optical diodes and switches used in fiber-optic communications. 

## setup: regulated power supplies 

One of the most useful tools in a lab for power stabilization is a constant current/constant voltage regulated power supply. These allow you to specify the maximum current and maximum voltage that will be supplied, and whichever limit is hit first is the one that will be regulated. 

For example, suppose you have a 220 ohm resistor. Ohm's law tells you that passing 1 mA of current will produce a voltage across the resistor of 220 mV. 

- If you set the current limit of a constant current/constant voltage regulated to 1.0 mA and the voltage limit to 200 mV, the voltage limit will be reached before the current limit --- the current passing through the resistor will be 0.91 mA, which is less than 1.0 mA --- so the power supply will  hold (keep constant) the voltage at 200 mV. 

- If you instead keep the current limit of a constant current/constant voltage regulated to 1.0 mA but raise the voltage limit to 250 mV, then the current limit will be reached first --- the voltage drop across the resistor will be 220 mV --- and power supply will then hold  the current at 1.0 mA.

- If the resistance actually increases as a function of current (like an incandescent light bulb or a Pt thermometer), then the current will remain 1.0 mA until the resistance reaches 250 ohms. At that point the regulation will switch to constant voltage.

:::{attention}
Every constant-voltage / constant-current regulated power supply does the same thing, but how you make the adjustments varies from one device to another. Ask your instructor now to show you how to set the current and voltage limits for your specific constant-current (CC) /constant-voltage (CV) power supply. You must learn how to do this properly before proceeding further! 
:::

### constant voltage regulation. 

The simplest laser diode power supplies provide a constant voltage to the laser, so let's start with that and see how the laser behaves. The voltage needed depends on the laser. We want to be above the threshold voltage but not exceed the current limit for the diode (above which it will burn out)! A typical operating voltage for 650 nm laser diodes like ours is 4 V. 

:::{tip} how to adjust the voltage supplied to the laser diode

1. For protection, start with a current limit of zero, then raise the current limit to 40 mA.
2. Then set the voltage limit to the minimum value before connecting to the laser diode and turning on the output.
3. Slowly raise the voltage limit up to 4.0 V. For these diodes, the expected current at this voltage is less than 40 mA, so the power supply will be in constant voltage mode --- you can confirm this by checking that the CV light is on and the CC light is off  --- and will therefore endeavor to supply a constant 4.0 V.  

Note: The digital displays of many regulated power supplies do not have sufficient resolution for our purposes. In our setup, we have therefore inserted a high resolution dc ammeter into the circuit so as to better measure (and set) the current.

:::

### constant current regulation

More advanced laser diode power supplies allow you to specify a desired current if you prefer, so let's learn how to do that as well. As a starting point, we suggest regulating at 25 mA for these particular laser diodes. 

:::{tip} how to adjust the current supplied to the laser diode

1. For protection, set a voltage limit of 4 V if you haven't already done so. 
2. Make a note of the numerical value for the  current passing through the laser diode while the power supply is in constant voltage mode. Remember to use the higher accuracy dc ammeter display rather than the power supply display to measure the current.  
3. Now decrease the current limit until the the actual current is less than the numerical value you just recorded.
4. You should see the light on the regulated power supply switch from CV to CC mode, indicating the power supply is now current limited. If not, decrease just a bit more until you do! Continue to decrease the current to the desired value. 25 nm is a good starting point. 
5. If needed, increase the voltage limit slightly to keep the supply in CC mode. Do not exceed 5 V for now. 
:::

For now, leave your laser diode in constant current mode. 


## setup: photodiode and voltmeter
The last step before performing our polarization measurements it  to measure the laser diode light intensity. For this purpose, we use a photodiode that outputs a current proportional to the light intensity and a graphical multimeter than can measure and display dc voltage data as a numerical average, as a trendline (to reveal time-dependent drift in the average value), and as a histogram (to reveal variation in measured values due to fluctuations).  

### photodiode (photodetector) 
In the simplest (unpowered) photodiode setups, you then put the photodiode in series with a resistor and then measure the voltage across the resistor to determine the current. TeachSpin photodiodes are often of this type. This is easy to implement, but the maximum current that can be output by the photodiode is limited, so you must check to see that the photodiode has not saturated.  In more advanced (powered) setups, a transimpedance amplifier is used to measure the current. The output of the amplifier is a voltage proportional to the current (and thus the light intensity). This is more costly, but can measure current and light intensity over a much greater range. It can also amplify the signal if needed.  In our setup, we will use a powered photodiode from ThorLabs with adjustable gain to measure the light intensity and a graphical multimeter in dc voltage mode to measure the output voltage from the detector. 

### multimeter 

The multimeter we are using for this task has multiple display modes, including numerical, bar, trendline, and histogram. There is also a statistics function you can engage to find mean and standard deviation (assuming a Gaussian distribution due to random variation in measured values). 

:::{tip} starting settings for the multimeter 

1. Connect the photodetector to the multimeter: Power on your photodetector and multimeter. Select DC Volts on the multimeter, connect the voltage output of the photodetector to the voltage input of the multimeter, then adjust the gain of your powered photodetector (or the resistance value of the resistor in series with your unpowered photodiode) so that the voltage output is in the 0.1 V to 1.0 V range. You can then switch the multimeter from AUTO to 1V.
2. Recommended multimeter settings when in DC Volts: select 1V range, reduce averaging time from 10 PLC (power line cycle) to 1 PLC (1/60 sec), and turn OFF Autozero. This will give a shorter wait time between each measurement and faster response when in trendline or histogram mode. 
3. Switch display mode from numerical to histogram. To switch between display modes, you push the button to the right of the display labeled 'display' , then the menu button below the display titled 'number'. You can then switch between them by repeatedly engaging that menu button. The trendline and histogram display modes have additional menu buttons that allow you to clear previous data, autoscale the results, and calculate/reset statistics.  Try these out!
:::

# Our experiments

## Preliminary Experiment 1 

In this experiment, you will these different display modes and functions to establish whether the fluctuations appear to be described by a Gaussian distribution (bell curve) about an average value, and if so, what the mean value and standard deviation are for that distribution. If they aren't described by a simple Gaussian distribution, explain why, and what you would use for a measure of uncertainty instead of the standard deviation. 

Take screenshots (or photos) of your histogram displays for inclusion in your jupyter lab notebook. 

```{exercise}
:label:photodiode-signal 

1. carry out experiment 1 with the laser diode power supply in constant current mode. 
2. repeat experiment 1 with the laser diode power supply in constant voltage mode 
3. Do the results support your choice of constant current or constant voltage regulation in [](#regulated-power-supplies) ?  Yes, no, or too much drift to tell? 

```
Return your power supply to {underline}`constant current` mode for now. 

## Preliminary Experiment 2

In this experiment, we want to figure out a way to distinguish between the various sources of light detected by the photodetector. In particular, we would like to subtract off  the contribution of the room lights so that we can calculate  the contribution from the laser light alone. 

```{exercise}
:label:light-sources
:class:dropdown
:open: false

1. Come up with a couple of simple ways to distinguish between the laser light and the room light in your measurements, then discuss these with your instructor. 
2. Try out one or both of your tests and report the results (in your Jupyter lab notebook). 
3. How practical is  if you need to keep readjusting the apparatus (polarizer angles, etc) and if others are also in the room? 
```

## Preliminary Experiment 3

IN this experiment, we want to figure out a way to completely eliminate the contribution of the room lights from our measurement. Towards this end, we call your attention to a voltage-operated LCD shutter taped to the diode laser output. Applying 5 V closes the shutter (light blocked); applying zero volts opens the shutter (light unblocked). 

```{exercise}
:label:LCD-shutter
:class:dropdown
:open: false 



1. Devise a plan using any combination of the following instruments to measure the light intensity due to the laser light alone: a dc power supply for the shutter, an ac power supply for the shutter (square wave output of a function generator), the graphical multimeter, and a lock-in amplifier. 

2. Discuss your plan with your instructor and get help with the setup if needed. 

3. Try out your measurement setup. If it works, turning on and off the room lights should not affect your measured result! 

4  CHeck that you are in constant current mode, then carry out the measurement in full and report your result for the voltage signal and the uncertainty in that result due to the laser light intensity alone. 

5. In your Jupyter lab notebook, be sure to explain how you arrived at your answer,  showing your calculations step by setp. 
```
Repeat this measurement for constant voltage mode, then explain which mode you prefer on the basis of your results. 

# Main Experiment: Polarization of light 

## introductory information

In this experiment, you want to determine and then plot the {underline}`laser light intensity` (in units of photodiode output voltage) as a function of {underline}`relative angle` between the two polarizers through which the light is passing. 

We also want to measure the {underline}`uncertainty` in our photodiode output voltage measurement and then include error bars showing our measured uncertainty on our plots. The histogram and statistics modes of the multimeter can be useful here. Note that you can connect the multimeter directly to the photomultiplier output. Alternatively, if you are using the lock-in amplifier, note that the measured value on the lock-in can be output as a voltage, and you could use the multimeter to measure the mean and std dev of the lock-in measurement! 

In our initial setup, there are two polarizers through which the laser light passes. These polarizers are already fully aligned, so the relative angle $\theta = \theta_2 - \theta_1 $ between the two is equal to 0 degrees. The second polarizer can be rotated in steps of 15 degrees. 

## Data collection

:::{note}
set your laser power supply to your choice of `constant current` or `constant voltage`. Leave it there for the full experiment. 
:::

Carry out measurements every 15 degrees for a relative angle between the two polarizers varying from 0 to 360 degrees (one full rotation). 

Record  the voltage measurements you need as a function of relative polarizer angle. Remember to record the voltage  {underline}`due to the laser light alone` and the uncertainty in that measured voltage! It might be convenient to enter this directly into a spreadsheet and save it as a csv file.


## Data analysis


1. Plot the data as a function of relative polarizer angle, including error bars! Your plot will of course depend on how you define your uncertainty. If in terms of standard deviation $\sigma$, we suggest setting your uncertainty to $2\sigma$ as a starting point.  
2. Look up `Malus's law` for the predicted variation of light transmission as a function of relative polarizer angle, then create a function in python that describes that function. Include an offset coefficient if needed.
3. Use the SciPy curve fit routine to adjust the coefficients in your function to come up with a best fit to your data
4. determine the goodness of fit from the reduced chi-square value. If it seems implausibly low and your data isn't noisy, you might retry with an uncertainty set to $1\sigma$. 
5. Plot your data and the fit as a continuous function of angle  on the same graph so that you can visually compare the two. You'll want at least 1000  points -- even better, use 3600! ---  so as to get a smoother curve.

```{attention}

It is convenient to record the data in degrees but remember you should convert all your angles to radians before using them in calculations involving trigonometric functions (such as $\sin(2 \theta)$ and curve-fitting routines! 
```

Does your data agree with the prediction of `Malus's law?` within the uncertainty of your data?  


## Upload results

1. save your Jupyter lab notebook
2. from the Kernel menu, select `restart Kernel and run all cells`
3. If your Jupyter notebook runs without any errors, generating all the graphs and calculations you need, save again, then download the notebook (and data files that the notebook uses).

 Upload your notebook and associated data files to your data respository. If on OSF.IO, remember to grant access to your instructors as collaborators! 







