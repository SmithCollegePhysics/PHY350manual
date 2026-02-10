---
title: Introduction to Lock-in Amplifiers
keywords: ["signal capture", "lock-in", "phase detection", "frequency", "synchronization"] 
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
  We investigate how a lock-in amplifier "locks in" to a signal of a particular frequency and phase even when that signal is buried in electronic noise. 
---

# Introduction

:::{iframe} https://www.youtube.com/embed/ZIjBRA2S0NQ?si=XW9ptpjrmlp4wGEh" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen
:width: 100%
How a lock-in amplifier works and some tips on how to use them
:::

```{exercise} 
:label:lock-in-signal-derivation

**Instructions** If in tutorial, please try these calculations now. If in lab, do these calculations after completing rest of lab. Submit your answer as part of your completed version of this markdown notebook. Ask for help with the LaTeX math formatting if needed! 

1. Mathematically show that if you use a lock-in amplifier (or a frequency 'mixer') to multiply an ac sinusoidal signal $V_s \sin{(\omega_s t + \theta_s)}$ with RMS amplitude $V_s$, phase $\theta_s$, and frequency $\omega_s$ by a ac reference $V_r \sin{(\omega_r t + \theta_r)}$, then the result $V_{lock-in} = V_s(t) V_r(t)$ is the sum of two ac signals, one at frequency $\omega_{\textrm{difference}} = \omega_r - \omega_s$ and the other at  $\omega_{\textrm{sum}} = \omega_r + \omega_s$

2. Now show that if and only if the signal modulation frequency $\omega_s$ equals the reference modulation frequency $\omega_r$, the result will include a dc signal at $V_{\textrm{lock-in}} = 
\frac{1}{2} V_s V_r \cos(\theta_s - \theta_r)$, which is a dc signal proportional to the original signal amplitude $V_s$. 

3. There will also be a signal at $\omega_s + \omega_r = 2 \omega_r$. What kind of circuit element does the lock-in amplifier use to eliminate that signal (so as to output only the dc voltage)?  How does it work? 

**Why this is important (and not just clever)**: We will see that if the signal amplitude $V_s$ *slowly* varies with time (compared to the oscillation period $2\pi/\omega_r$) due to a change in some parameter such as temperature, you can now measure that variation using a voltmeter or computer even though the original signal was buried in noise! 

```
```{card} Your derivation:  
:header: Exercise 1: lock-in calculation

$$ V_s(t) = V_s \sin{(\omega_s t + \theta_s)} $$
$$ V_r(t) = V_r \sin{(\omega_r t + \theta_r)} $$

$$ V_s(t) V_r(t) = ...$$ 

and using the following trigonometric identity... 

```

```{solution} lock-in-signal-derivation
:class:dropdown

You can solve this using [trigonometric identities](https://en.wikipedia.org/wiki/List_of_trigonometric_identities#Product-to-sum_and_sum-to-product_identities)  or complex exponentials. 

See also either or both of the following references for guidance (if needed): 
-  [SRS830 basics](https://www.thinksrs.com/downloads/pdfs/manuals/SR830m.pdf) in the SRS830 lock-in manual from Stanford Research Systems  
- [Principles of Lock-in Amplifiers](https://www.zhinst.com/ch/en/whitepapers/principles-of-lock-in-detection) from Zurich Instruments. 
```




:::::{dropdown} Discovery Exercise: signal recovery from noise
:open:

## external trigger off of sync output 

1. Use a function generator to generate a 1 kHz 2mV RMS amplitude sine wave (or as small as possible if 2 mV is too low), then turn on the `sync` output for the generator to output a square wave signal at the same frequency. This will typically be a `TTL` 0 to 5 V square wave but you should check to be sure (and to be sure it is working). To do so, connect the sine wave to channel 1 of an oscilloscope and the sync output to channel 2. Make sure you can trigger off of the sync signal! 

2. Now disconnect the sync signal from channel 2 and connect it instead to the `external trigger` input for the oscilloscope. Switch the trigger channel from `2` to `ext` or `external` and verify that the oscilloscope is still triggering and that you can view and accurately measure the RMS amplitude and frequency of the sine wave signal on channel 1. 

## comparison of oscilloscope and lock-in amplifier 

For comparison, let's also connect the function generator outputs to a lock-in amplifier.   

1. **Reference**: set the lock-in reference to `external` and `square wave` rather than sine wave if you are given the option.  Once you have the settings adjusted, use a  BNC `T` connector so that the sync output from the function generator can go to both the `reference in` of the lock-in amplifier and the external trigger input of the oscilloscope.
 
2.  **Signal input**: set to single-ended mode (A) rather than differential voltage mode (A-B) or current input mode (I). You can also set the coupling mode and grounding mode. We recommend starting with `ac` for coupling mode and  `float`[^float] for grounding mode, but the alternatives will also work here.  Once you have the settings adjusted, use another BNC `T` connector so that the signal output from the function generator can  go to both the channel A voltage input of the lock-in and channel 1 of the oscilloscope. 

3. On the lock-in, select AUTO MEASURE or AUTO GAIN + AUTO PHASE. These are the lock-in equivalent of `AUTOSET` on the oscilloscope. Then adjust the time constant to 0.1 sec, 12 db/oct. The period of a 1 kHz signal is 1 msec, so a single time constant of 0.1 seconds 6 db/oct effectively averages over 100 periods of a 1 kHz signal. 

## trial measurement of a 'clean' signal

1. Use the oscilloscope measurement tools to measure the signal RMS amplitude and frequency to within 1 percent. You may need to do some signal averaging to make the displayed measurement values sufficiently stable. Make a note of the values and the averaging time (if averaging more than 1 signal). The averaging time is the number of averaged cycles x duration of one cycle.  Example: If your signal is 10 ms/div, the duration of one trigger cycle is 10 ms/div x 10 div/screen = 100 ms. 

2. The lock-in will report the RMS amplitude of the input signal as $R$ in volts PLUS the phase shift of the input signal relative to the reference signal as $\theta$ in degrees. Alternatively, it will report the `in phase` component $X = R \cos(\theta)$ and the `out of phase`component $Y = R \sin(\theta)$. If the signal is not stable to within 1 percent, increase the time constant one step [^steps] at a time until it is. You can also increase the db/oct [^db] from 12 to 18 to 24.  Make a note of the values and the time constant settings required to make the displayed measurement value sufficiently stable. As an appoximation of the averaging time, take the time constant and then multiply by 3 for each additional RC filters used (x1 for 6 db/oct, x3 for 12 db/oct, x9 for 18 db/oct, x27 for 24 db/oct )

3. How do the measurement stabilities and averaging times compare for the two methods? 

## measurement of noisy signals

1. For this part of the experiment, you'll need to be able to add two voltages electronically using a voltage `summer` or `adder` [^summing_circuit] [op-amp circuit](https://vakits.com/op-amp-ic-development-design-kit-lm7411650). Our particular summing circuit in this lab takes $A$ and $B$ as inputs and outputs $-(A+B)$. The output signal is inverted because it uses an inverting amplifier to do the sum.  Commercial units will output $A+B$. 

2. You'll also need two channel function generator with a noise option for one of the channels output (or a second generator with a noise setting). In our lab, we'll use a Rigol 1022 with two independent outputs in addition to the sync output (available at the rear of the device). Be careful: channel B is ABOVE channel A --- {\underline}`not` BELOW -- and each channel has its own on/off button (in addition to the two power switches for the function generator itself). 


3. To start with, we'll use a 10 mV RMS amplitude sine wave at 1 kHz and a Gaussian noise generator with a signal 'amplitude' of  10 mV RMS.  Connect the  sine wave signal from channel 1 of the function generator to one of the summing circuit inputs and the noise signal from channel 2 of the function generator to the other. Then connect the output from the summing circuit to both your favorite channel on the oscilloscope and the `A` input of the lock-in amplifier. 

You'll continue to use the function generator sync output as the external trigger input for the oscilloscope and the reference input for the lock-in. Be sure the sync output remains synched to channel 1 rather than channel 2!   

4. Compare what you measure for the sinusoidal signal in the presence of electronic noise  using the oscilloscope and the lock-in amplifier for the following settings (complete the table) 

:::{table} recovering signal from noise: measured amplitudes 
:label: signal-recovery-table
:align: center

| sine wave | noise     | oscilloscope      | settings |  lock-in | settings | comments| 
| --------- | --------- | ----------------- | -------- | -------- | -------- | ------- |
| 10 mV RMS | off       | V_{RMS} $\pm$ ?   | x s/div, N avg | V_{RMS} $\pm$ ? | Tc, db/oct | do both work equally well? | 
| 10 mV RMS | 10 mV RMS | V_{RMS} $\pm$ ?   | x s/div, N avg | V_{RMS} $\pm$ ? | Tc, db/oct | how do the two instruments compare?  | 
| 10 mV RMS | 100 mV RMS |  |  |  |  | is one clearly better?  | 
| 2.5 mV RMS | 250 mV RMS |  |  |  |  | does oscilloscope still work?   | 
:::

5. Why do you think the lock-in amplifier better able to recover a signal buried in noise? 

:::::




[^float]:The ac/dc coupling option is the same as on an oscilloscope, but the  float/ground option is something new.  It has to do with whether the rotating outer shell of the BNC coax connector is directly connected to ground or is connected via a small resistor (typically 100 - 1000 ohm) to reduce ground currents. When measuring in single-ended mode `A`, you should usually choose 'float.' When measuring in differential voltage mode `A-B`, you usually choose `ground`. 

[^steps]: Depending on the particular lock-in you are using, the next steps up might be 0.3 s and 1.0 sec or 0.2 s, 0.5 s, and 1.0 s.  

[^db]: each increase in db/oct setting adds another low-pass filter to the output. So 6 db/oct means one 6db/oct RC low pass filter, 12 db/oct means two, etc. Most analog lock-ins are limited to 12 db/oct but modern digital lock-ins offer up to 24 db/oct. 

[^summing_circuit]: You can build one from a kit --- we did! — or you can buy a [commercial unit](https://www.thinksrs.com/products/sim980.html). If you build from a kit, you will also need a power supply to power the op-amps in the kit. We use a power supply that outputs both +12 V and -12 V to ground (or higher).

:::::{dropdown} Follow-up Exercise: following a signal through a lock-in amplifier
:open:

In this exercise, we use the [TeachSpin SPLIA1-A](https://www.teachspin.com/signal-processor-lock-in) signal processor/lock-in amplifier to experimentally follow what happens to a sinusoidal signal as it moves from stage to stage inside a lock-in amplifier.  

## initial setup

We want to use the TeachSpin SPLIA1-A to produce a dc signal proportional to the amplitude of a 1 kHz sine wave. 

1. Configure channel 1 of your two channel function generator to be a 1 kHz sine wave with an amplitude of 10 mV RMS. This will be $V_s(t)$ , the signal we want to measure. 

2. Configure channel 2 of your two channel function generator to be a 1 kHz sine wave with an amplitude of 1 V RMS. This will be $V_r(t)$ , the reference signal for our lock-in. 

3. Configure the channel 2 output to be in-phase (*phase-aligned*)  with channel 1. Your instructor can show you how to do this! 

:::{note} why a sinusoidal reference signal? 
The TeachSpin SPLIA1-A is an analog lock-in and like many analog lock-ins, it requires a *sinusoidal* reference signal. To accomplish this, we will disconnect the TTL square wave sync output previously used as a reference signal (for our commercial lock-in), replacing that with a second sine wave synchronized to the firsrt.
:::

4. Connect the channel 2 output from the function generator to (a) the external trigger input of your oscilloscope and (b) the external reference input of the lock-in amplifier. Adjust trigger settings on the scope and reference input settings on the lock-in as needed to be compatible with a 1 V rms sine wave instead of a 5 V TTL square wave.  

## lock-in processing stages 

### The preamp

1. Connect the channel 1 output from the function generator to (a) channel 1 of your oscilloscope and (b) the `A` voltage input of the TeachSpin preamp. We will be measuring in `A - GND` single-ended voltage mode rather than `A-B` differential voltage mode, so switch input `A` of the preamp to `AC` coupling and input `B` of the preamp to ground (GND). 

2. Connect the output of the preamp to channel 2 of your oscilloscope, then adjust the preamp gain to produce a sinusoidal signal with an RMS amplitude between 0.1 V and 1.0 V. 

:::{note} choosing the right amplifier gain
The electronics in the TeachSpin lock-in work best in the 200 mV to 2 V pp range, and will  saturate at higher voltages . If you adjust the amplification at each stage of the lock-in to produce a voltage output no greater than 1 V RMS(including noise spikes), you will maximize the signal/noise without saturating the op-amps inside the instrument. For other considerations (such as the frequency dependence of the amplifier gain) consult [this online summary](https://www.teachspin.com/signal-processor-lock-in) or the full manual. 
:::

3. Use the oscilloscope to compare the original signal at the preamp input to that at the preamp output. Tip: adjust the oscilloscope voltage/division settings to overlay the output signal (channel 2) on top of the input signal (channel 1).  

- do they both measure the same RMS amplitude (after correcting for preamp gain)?
- is one signal quieter --- higher signal/noise ratio --- than the other? Why? 

### The bandpass filter

Another feature of many analog lock-in amplifiers is a band pass filter used to remove noise at frequencies well below and above the reference frequency prior to multiplying the signal by the reference. We now want to tune the bandpass filter so that its resonant frequency matches that of our input signal. 

1. Set the filter type to Chebyshev,  run a short BNC cable between the preamp output and the bandpass input, and a standard BNC from the bandpass output to channel 3 of the oscilloscope. If you have a two channel oscilloscope, replace channel 2 with this output. 

2. Adjust the Chebyshev filter frequency to maximize the amplitude of the output signal. The center frequency of the filter should turn out to be approximately 1 kHz! 

3. Again adjust the oscilloscope voltage/division settings to overlay the output signal from the bandpass filter (channel 3) over the preamp output signal (channel 2) and the original signal (channel 1). 

- How does the bandpass filter output signal compare with the previous signals? 
- Does the filter introduce a phase shift? How much? 

4. Now compare the amplitude of the bandpass filter for the following settings: Chebyshev, Q = 2, and Q = 5. Notice how the signal amplitude changes.  

5. To explore the tradeoffs between signal amplitude, stability, and phase shifts that guide the choice of Q value, consult the lock-in manual and/or discuss with your instructor. For now, however, return the bandpass filter setting to Chebyshev! 

### The phase shifter 

We now want to adjust the reference signal $V_r(t)$ so that it and the input signal $V_s(t)$ are in phase. 

1. To monitor the phase difference, use a short BNC cable to connect the 1V 1kHz sinusoidal reference signal from channel 2 of the function generator to the phase shifter input, then run a standard BNC cable from the phase shifter output to channel 4 of the oscilloscope. 

2. Adjust the phase shifter until the output signal on channel 4 is in phase with the signal coming out of the bandpass filter. Note that there is a fine adjustment and a course adjustment (which changes the phase by +90 or -90 degrees). You may need to work with both to bring the signals into phase with each other. 

### The lock-in module

We now want to see what happens when we modulate the (amplified and filtered) input signal using the reference signal. 

:::{note} what does the external reference signal actually do?
In a digital lockin, the square wave TTL reference signal generates a sine wave phase-locked to the square wave, and the input signal is  mathematically multiplied by this phase-locked sine wave (in the manner explored in [](#lock-in-signal-derivation)). 

In this and most other analog lockin amplifiers, the reverse happens! Instead of using a square wave reference to create a sine wave reference signal, the sine wave reference signal is used to effectively generate a symmetric square wave reference that alternates between -1 and 1. It does this by flipping a switch  everytime there is a zero crossing of the reference. This switch reverse the + and - leads of the input signal. The effect is the same {underline}`as if you were to multiply the input signal by a symmetric square wave` that alternated between a value of +1 and -1. 
:::

1. Replace the cable running from the phase shifter output to channel 4 of the oscilloscope with a short BNC cable running from the phase shifter output to the lock-in reference input. 

2. Replace the cable running from the bandpass filter output to channel 3 of the oscilloscope with a short BNC cable running from the bandpass filter output to the lock-in signal input, then connect this lock-in signal output to channel 3. 

3. Use the oscilloscope to compare the lock-in module signal output to the lock-in module signal input. Adjust the phase shifter signal by +90 and -90 degrees to see the effect that has, then return to your original phase shifter settings. Now make fine adjustments to the phase to make the output signal from the lock-in module as symmetric as possible. 

4. Describe what the output signal looks like when the reference and signal are **in phase**. What would the average of this in phase signal be over one full period?   {underline}`Take a screenshot to paste into your copy of this markdown file along with your answers.` 

5. What does the output signal look like when the reference and signal are 90 degrees **out of phase**? What would the average of this out of phase signal be over one full period? {underline}`Take a screenshot to paste into your copy of this markdown file along with your answers.`   

6. Return the phase shift adjustment to bring the two signals in-phase as before, then adjust the gain of the amplifier in this module as needed to bring the peak amplitude of the output signal of the lock-in module into the 0.2 V to 2.0 V range.

### The low-pass filter (time-constant) 

Let's now follow the signal through the last circuit in a lock-in amplifier: the low-pass filter. 

1. Use a BNC `T` connector to add a connection between the lock-in module output and the low pass RC filter that controls the lock-in `time constant`. 

2. Use a BNC `T` connector to pass the output signal from the low-pass filter/ time constant module to channel 4 of the oscilloscope and also to a hand-held dc voltmeter. 

3. To start, try a 0.1 s, 12 db/oct time constant, then increase the time constant if needed until you achieve 1 percent stability for the dc voltage output.

4. Adjust the gain of the time constant module to produce a dc output somewhere in the range between 0.2 V and 2 V. 

5. Take the dc output voltage, then divide by the gains at each step of amplification. Example: if the preamp has a gain of 100, the lockin-module has a gain of 5, and the time-constant module has a gain of 2, then the total gain is 100 x 5 x 2 = 1000, so you would divide the dc output voltage by 1000. Finally, mulitiply that result by a temporarily mysterious factor of 1.11. This should match the RMS amplitude of the original input signal! Wow!

`````{exercise} The mystery factor
:label: multiplicative-factor

Numerically calculate the average of $\sin(x)$ from $x = 0$ to $x = \pi$ and compare it to the square root of the average of  $\sin^2(x)$ from $x = 0$ to $x = \pi$ (The RMS average). Use this to explain where our mystery factor of 1.11 comes from! 


:::::



# concluding investigation

:::{note} non-sinusoidal periodic signals

The lock-in amplifier has generated a dc voltage that is proportional to the amplitude of the sinusoidal input signal. But what about non-sinusoidal input signals? 

1. Using a commercial lock-in capable of looking at higher harmomics of an input signal, reducing the amplitude of a sinusoidal signal that is output by a function generator by a factor of 2, then return the signal back to its original amplitude.  Are the signal amplitudes proportional? And does the RMS amplitude of the signal from the function generator match that measured by the lock-in in both cases?

2. Repeat the previous measurements for a symmetric square wave. Are the measured signals proportional to the amplitude of the square wave output by the function generator?  Does the measured value match the RMS amplitude of the square wave output? 

3. These measurements have all been done at a frequency $f_r = \omega_r / (2\pi)$. Now adjust the lock-in to measure the signal at the following harmonics: $f = 2 f_r$, $f= 3 f_r$, $f = 4 f_r$, and $f=5 f_r$. What is the lock-in measuring? Explain in terms of Fourier components. 


:::


 
  



