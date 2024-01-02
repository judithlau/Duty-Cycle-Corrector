# Duty-Cycle-Corrector
A module to modify the duty cycle of specific high frequency input signal on specified steps 

## Architecture
The modification of duty cycle is implemented through controlling tr/tf of a output signal from the 50\:50 input waveform.

The core module comes from alternative implementation of current starving current source(*CSCS*) mentioned at following texts). 

- traditional CSCS: controlled by a bias voltage ([^1])
  
	![image](https://github.com/judithlau/Duty-Cycle-Corrector/assets/52502238/5b17906e-b75f-4d03-9134-9e22bd61a8e2)

- this project implemented with **transistor scaling** which the input voltage is digital(with 0,1).
  
	![圖片1](https://github.com/judithlau/Duty-Cycle-Corrector/assets/52502238/5ad18c9d-17c2-4c6a-b305-d530a4d45943)

## PDK
This project is done with TSMC 180nm PDK.

## Finished work
- V1_DCC_COARSE module (5Jan):
	A module that would modify an **ideal 200Mhz input signal (with tr/tf = 150ps)** from duty cycle = 50% to 40 ~ 60% with step = 2%

	Designed with redundant stage cascaded.
## Incoming work
- V2_DCC_COARSE module with redundant stage cascaded
	- Fine tune the postlayout of coarse module.
	- Cascade a redundant stage for preparation to connect a FINE module(modifying input signal 50% to 47% ~ 53% with step 0.3%)  
		![image](https://github.com/judithlau/Duty-Cycle-Corrector/assets/52502238/ab7d1403-3029-4e23-b626-0f1c4dbdf42a) [^2]
## Version1. (V1_DCC_COARSE module)Independent COARSE module (5Jan)

### Result:
![image](https://github.com/judithlau/Duty-Cycle-Corrector/assets/52502238/b8bf5773-92a4-4208-a401-1bf2620ddf32)

testing path: 
/V1_DCC_COARSE_5JAN/DCC_COARSE_TT_TB/adexl → COARSE_TEST → RUN

The layout used is a collaborated work, therefore not attached for testing, please use the schematic testing.

The schematic is able to produce the rough duty cycle wanted. However, in postlayout, the results varied a lot. Initially, it is guessed to be the problem of ignoring parasitic components at the stage of schematic simulation.

### Follow-up improvement to do:
- Add parasitic component according to the design rules
- Re-engineer the cascading core modules
- Fine-tune the tr/tf of COARSE output to specified symmetric value for FINE module.
###
[^1]: https://ieeexplore.ieee.org/document/1328311
[^2]: A graph from EESM5000 FALL23 Project2 description.
