# UltraViolet
Electronic EBC/SRM meter, also called colorimeter, to measure the color value of beer based on the Arduino platform.
Determination of the SRM value is done by measuring the attenuation of light with a wavelength  of 430 nm (violet), passing through 1 cm of the beer using a cuvette, hitting a light sensor that measures the intensity. The absorption is then calculated to EBC/SRM by the Arduino and shown on a LED display.

## Small donation
[Yes, I want to make a small donation!](https://www.paypal.me/jankees "PayPal.Me")

## Download firmware
[Take me to the releases of UltraViolet](https://github.com/jankeesv/UltraViolet/releases "Releases of UltraViolet")

## Changelog
| Date          | Remark        |
|:------------- |:------------- |
| 14-3-2018     | Initial setup of the documentation |

## Introduction
### Background on SRM/EBC

| SRM/Lovibond  | Example       | EBC           |
|:------------- |:------------- |:------------- |
| 2 | Pale lager, Witbier, Pilsener, Berliner Weisse | 4 |
| 3 | Maibock, Blonde Ale | 6 |
| 4 | Weissbier | 8 |
| 6 | American Pale Ale, India Pale Ale | 12 |
| 8 | Weissbier, Saison | 16 |
| 10 | English Bitter, ESB | 20 |
| 13 | Biere de Garde, Double IPA | 26 |
| 17 | Dark lager, Vienna lager, Marzen, Amber Ale | 33 |
| 20 | Brown Ale, Bock, Dunkel, Dunkelweizen | 39 |
| 24 | Irish Dry Stout, Doppelbock, Porter | 47 |
| 29 | Stout | 57 |
| 35 | Foreign Stout, Baltic Porter | 69 |
| 40+ | Imperial Stout | 79 |

### What is the UltraViolet?

### Who uses the UltraViolet?

### How does the UltraViolet work?

## Hardware
### Needed parts
The following parts are needed to create the UltraViolet.
* Arduino Nano
* 3W 420nm-430nm UV LED (20mm star base)
* SI1145 UV IR Visible Sensor
* Pushbutton


### Electronic schema

### 3D printed casing

### Construction

## Software
### Use case
Scenario: Basic flow determine color
Summary: The brewer determines the color of the beer by turning on the UltraViolet and folow the instructions given.
Primary actor: Brewer
Steps
1. Brewer turns the Ultraviolet on with holding the measure button.
2. Ultraviolet displays the instruction to fill with water.
3. Brewer takes the cuvette out of the holder and fills it with distilled water.
4. Brewer places the cuvette back in the holder and presses the measure button shortly.
5. Ultraviotet turns on the LED, measures the light intensity, stores the value and turns off the LED.
6. UltraViolet displays the instruction to fill with beer with a dilution of 1:1.
7. Brewer places the cuvette back in the holder and presses the measure button shortly.
8. Ultraviolet turns on the LED, measures the light intensity, turns off the LED and calculates the EBC and SRM values.
9. Ultraviotet displays the EBC and SRM values.
10. Brewer turns the UltraViolet off with holding the measure button.
11. END

Exceptional situations
Scenario: Very dark beer needs dilution
Exception summary: On step 8 there is a very low value measured because the beer is very dark (imperial stout)
Steps
1. Ultraviolet displays a message that the beer is too dark.
2. UltraViolet displays the instruction to dilute the beer with a dilution of 1:1.
3. Ultraviolet stores the dilution value of 2 for the calculation.
4. Continue at step 7 of the basic flow

Scenario: Diluted dark beer needs dilution second time
Exception summary: On step 8 there is a very low value measured because the beer is still very dark (imperial stout), even after dilution.
Steps
1. Ultraviolet displays a message that the beer is too dark.
2. UltraViolet displays the instruction to dilute the already diluted beer with a dilution of 1:1.
3. Ultraviolet stores the dilution value of 4 for the calculation.
3. Continue at step 7 of the basic flow

### State machine diagram

### Calculation SRM/EBC
The absorption is the log of the ratio of the intensity of the light beam entering the sample to the intensity leaving. This difference is multiplied by 12.7 in the SRM system and 25 in the EBC.

A430 = -log10(I/Io)
SRM = 12.7 * D * A430

Io = the intensity when it passes through the distilled water sample.
I = the intensity of the light after it passes through the beer.
D = the dilution factor D=1 for undiluted samples, D=2 for 1:1 dilution etc.
A = the absorbance at 430 nm in 1 cm.

Example: If the light intensity leaving is one one-hundredth the light intensity entering the ratio is 100, the absorption is 2 and the SRM is 25.4.

Conversion can be done using the following formulas

EBC = SRM * 1.97
SRM = EBC * 0.508

[Wikipedia - Standard Reference Method](https://en.wikipedia.org/wiki/Standard_Reference_Method "Standard Reference Method")
[Sciencing - How to calculate absorbance](https://sciencing.com/calculate-absorbance-2650.html "How to calculate absorbance")

### Upgrade firmware

## Small donation
[Yes, I want to make a small donation!](https://www.paypal.me/jankees "PayPal.Me")
