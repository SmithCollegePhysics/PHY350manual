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

## preliminary experiments
Complete the preliminary experiments and set up in `dc_power_regulation.md` before proceeding with this experiment. 

## main experiment
In this experiment, you want to determine and then plot the {underline}`laser light intensity` (in units of photodiode output voltage) as a function of {underline}`relative angle` between the two polarizers through which the light is passing. We will compare that to the predictions of `Malus's law.` 

We also want to measure the {underline}`uncertainty` in our photodiode output voltage measurement and then include error bars showing our measured uncertainty on our plots. The histogram and statistics modes of the multimeter can be useful here. Note that you can connect the multimeter directly to the photomultiplier output. Alternatively, if you are using the lock-in amplifier, note that the measured value on the lock-in can be output as a voltage, and you could use the multimeter to measure the mean and std dev of the lock-in measurement! 

In our initial setup, there are two polarizers through which the laser light passes. These polarizers are already fully aligned, so the relative angle $\theta = \theta_2 - \theta_1 $ between the two is equal to 0 degrees. The second polarizer can be rotated in steps of 15 degrees. This will allow us to determine how the intensity of light passing through the polarizers varies as a function of relative angle. 

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







