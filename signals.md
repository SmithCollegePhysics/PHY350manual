# TeachScope II Signals

This is a secret list of the signals I have detected and characterized (no instructors manual). 

Do not share with students or post in public folder.

:::{table} Detected signals
:label: TS2_signals
:align: center

| signal # | signal type                 | vertical   | timebase  | trigger | level | comments                           |
| ---------| --------------------------  | -----------| --------- | ------- | ----- | ---------------------------------- |
| 1 (0001) | 5V pp 100 Hz square wave, +2.5V dc offset | 1 V/div DC | 2 ms/ div  | Norm    | 2.5 V rising | use 10:1 probe and adjust probe cap to square signal. FFT : 2V at 100 Hz, (1/3) 2V at 300 Hz |
| 2 (0010) | 4V pp 5 kHz sine wave, no offset   | 1 V/div DC | 50 $\mu$s/ div  | Norm    | 0 V rising | can use high res or avg to clean up signal. Use FFT to verify freq! |
| 3 (0011) | 4V pp 1 kHz square wave into tank circuit | 2 V/div dc | 100 $\mu$s/ div | peak detect | 4 V rising | underdamped 4Vpp 70 ns transients. Use peak detect  |
| 4 (0100) | 5V spike with 1.6 $\mu$s pulse width @ 1.02 Hz   | 1 V/div DC | 5 $\mu$s/ div  | peak detect   | 3 V rising | autoset fails! Use peak detect. Use COUNTER to find frequency  | 
| 5 (0101) | 1.5V pp 1 kHz sine wave on +3V dc    | 1 V/div DC | 500 $\mu$s/ div  | Norm  | 3 V rising | step function approx of sine wave. use ac/dc coupling to see offset | 
| 6 (0110) | 6V pp 50 Hz triangle wave, no offset |  |  | Norm    | | autoset works  |
| 7 (0111) | 2.9V pp 12 kHz inverted sawtooth on 1.45 V dc  |  |  |     | | autoset fails. Extra wiggles on ramp that don't average out  | 
| 8 (1000) | asymmetric triangle wave + noise spikes  |  |  |     | | jittery, add bandwidth (BW) limit to trigger properly? | 
| 9 (1001) | 5V pp exp rise & decay at 300 Hz   |  |  |     | | not yet fully characterized  |  
| 10 (1010) |62$\mu$V pseudo triangle-wave at 337 kHz on -100 $\mu$V dc plus HF noise spikes|  |  |     | | truncated exp rise & decay. Use BW to trigger/ remove spikes.  | 
| 11 (1011) | 7.35V pp mod. square wave (step up, ramp down) at 3.15 Hz, no offset  |  |   |   | | Could model using Heaviside step functions | 
| 12 (1100) | +4V spikes at 20 Hz, no offset   |  |  |     | | use COUNTER to find repetition frequency  |  
| 13 (1101) | 5V pp sinc(x) function at 500 Hz  |  |  |     | | use COUNTER to find repetition frequency  |  
| 14 (1110) | 8.75 kHz, 10.6 kHz, 17.5 kHz, 21.2 kHz, 34.9 kHz |  |  |     | | requires FFT: all 5 freq are equal amplitude |  
| 15 (1111) | 1.06V pp sine wave @ f=4 kHz + 132.4 mV pp @  2f  |  |  |     | | requires FFT: looks like single freq sin wave unless view FFT   |  
::: 


