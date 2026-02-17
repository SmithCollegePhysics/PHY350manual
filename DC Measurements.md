---
title: DC measurement challenges and solutions
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
    
date: 2026-01-26
abstract: |
  We use measurements of polarization of light to introduce some of the challenges involved in making stable dc measurements and some common solutions. 
---

# Introduction

In this experiment we will use a diode laser emitting 650 nm red light to measure light transmission as a function of polarizer angle.  This is an interesting measurement on its own but it is also the first step in investigating Faraday rotation: using a magnetic field to change the polarization angle of polarized light [^Faraday_rotation]. 

[^Faraday_rotation]:This phenomena was the first indication that light might be an electromagnetic field and is now used to make optical diodes and switches used in fiber-optic communications. 

## motivating experiment: regulated power supplies 

:::{note}  
:label: regulated-power-supplies

In your lab setup for today, you will use a photodiode to measure the light intensity of laser light passing through rotatable polarizers. Unfortunately, laser diodes are notoriously unstable: they tend to "mode hop" in response to changes in temperature and  power and this mode hopping leads to changes in frequency and output intensity. What's more, laser diodes are diodes, not ohmic resistors, so some thought is needed as to how to best stabilize the electrical power provided to the laser. 

![hockey puck shape of diode IV curve](https://cdn1.byjus.com/wp-content/uploads/2022/10/Characteristic-curve-of-laser-diode.png 'laser diode power as a function of current')

1. How can we measure the stability of our laser diode?
2. Laser diodes are diodes, not ohmic resistors: if we want to stabilize the power supplied to our laser, is it better to use a constant voltage or constant current power supply? 
:::

```{image} https://cdn1.byjus.com/wp-content/uploads/2022/10/Characteristic-curve-of-laser-diode.png
:label:diode_power
:alt: laser diode power as a function of current
:width: 500px
:align: center

laser diode power as a function of current. [Source](https://byjus.com/physics/laser-diode/)
```


