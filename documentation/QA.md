# Trigger Output FMC Quality Assurance Procedure
## Purpose
The purpose of this document is to have a consistent unified way each Board is tested before deployment. This procedure will be updated periodically to improve QA of the boards.

## Equipment needed
* 2 x MMCX to SMA Cables
* 2 x SMA to BNC adapters
* 1 x SMA to SMA Cable
* Multimeter (Fluke 115 or better)
* Triple output Benchtop Power Supply 
* 2 x FMC Power breakout module [link](https://www.iamelectronic.com/shop/produkt/fpga-mezzanine-card-fmc-power-module/)
* Marble Testing Chassis
* PC to run IOC and Phoebus

## Procedure
### Visual Inspection
Check visual for any board defects. If the board has come back from rework look at the reworked areas carefully under magnification for any shorts etc.

Areas to check with extra scrutiny are around the clock jitter cleaner components.

<div align="center"><b>Record in Testing Log when complete</b></div>
<p></p>

***

### Power Testing
Next the Board will be powered up in various ways to protect other testing hardware.

***

### Looking for Shorts to GND
Using the multimeter check that all voltage test points
have a resistance to board ground greater than 1kΩ.

| SilkscreenedLabel | Nominal Voltage |
| ----------------- | --------------- |
| VDD3P3V           | +3.3V           |
| VADJ              | +2.5V           |
| 12P0V             | +12V            |
| TP5               | +1.8V           |
| TP6               | +3.3V           |
| TP7               | +3.3V           |
| TP8               | +5.45V          |
| TP9               | +1.8V           |


<div align="center"><b>Record in Testing Log when complete</b></div>
<p></p>

***

### 12V/3.3V/2.5V Power Testing
One at a time inject 12V,3.3V & 2.5V using the voltage test points found on the board. Do this with a 1.5A current limit.

Note variance from nominal current if found.

Nominal expected current draw is:
<table border="1"; style="border-collapse: collapse;">
    <tbody>
        <tr><td>12V</td><td>~130mA</td></tr>
        <tr><td>3.3V</td><td>~70mA</td></tr>
        <tr><td>2.5V</td><td>~4mA</td></tr>
    </tbody>
</table>

<div align="center"><b>Record in Testing Log when complete</b></div>
<p></p>

***

### FMC breakout Power Testing
Using a 3 output power supply and two FMC Power breakout modules: Power up all input power rails (12V/3.3V/2.5V) simultaneously

Note variance from nominal current if found.

Nominal expected current draw is:
<table border="1"; style="border-collapse: collapse;">
    <tbody>
        <tr><td>12V</td><td>~130mA</td></tr>
        <tr><td>3.3V</td><td>~70mA</td></tr>
        <tr><td>2.5V</td><td>~4mA</td></tr>
    </tbody>
</table>

<div align="center"><b>Record in Testing Log when complete</b></div>
<p></p>

***

### Power up with Marble
Attach a now power tested quartz to a **powered off** marble testing chassis.

Power up the testing chassis.

Start the IOC.

Ensure proper readback of diagnostic signals (voltage, etc.).

<div align="center"><b>Record in Testing Log when complete</b></div>
<p></p>

***

### EEPROM Programmed

Checkout the branch/revision appropriate to the PCB model to be programmed,
and edit `createEEPROMs.sh` with the appropriate serial numbers.

<div align="center"><b>Record in Testing Log when complete</b></div>

***

### Signal Check - Clock Routing

* Ensure the chassis under test has a EVR input at a nomial 125MHz provided by another chassis
* Route received 125MHz through to the first jitter cleaner (U18) using FMC_LA_1 pin pair
	* Ensure the System can now lock to FMC_GBTCLK0
	* Using the FGPA console run 'fmon' to see the clock also on FMC_LA_0 signal pair

* Route received 125MHz through to the first jitter cleaner (U18) using FMC_LA_18
	* Ensure the System can now lock to FMC_GBTCLK1
	* Using the FGPA console run 'fmon' to see the clock also on FMC_LA_17  signal pair
* Ensure that each scenario locks
<div align="center"><b>Record in Testing Log when complete</b>
</div>

***

### Signal Check - Digital Outputs
- For each Digital Output set up and send an event stream turning all outputs on and off at 1Hz.
- Force 0/1
- Look at each of the 16 output to ensure compliance.

<div align="center"><b>Record in Testing Log when complete</b>
</div>

***

## Start/Completion Validation

Record the git commit of **this QA procedure** in the Testing Log.

Also record the following:
<br>
Tests Performed By: _________________
<br>
Date Initiated: ______________________
<br>
Date Completed: ____________________
<br>
Finally indicate a Pass/Fail if this performed with no deviations or waivers