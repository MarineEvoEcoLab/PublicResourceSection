
<img src="assets/media/seethroughlargePuritzlogo.png" width="300"> 

# Public Resources

Two anthropogenic stressors that are largely coupled together and driven by diel cycling via respiration and photosynthesis include low dissolved oxygen (hypoxia) and ocean acidification. However, it is relatively unknown what the cumulative effects of these stressors are and, in particular, for marine organisms that experience discrete life stages. **An aquatic system was delevoped in the Puritz Lab to invesitigate the cumulative impacts of hypoxia and ocean acidification at early life stages (Larval and Juvenile) in the Eastern oyster**. This repository  MarineEvoEcoLab/PublicResourceSection provides information on the materials and methods used in that aquatic system.


## Resource 1
### Experimental Flow-through Sea Water System to diurnally cycle pH and dissolved oxygen
This product includes a description of [system design](#System), [code](#Code), [list of parts](#Parts) paramount to the experiment. This work was funded by RI Sea Grant [![RI Sea Grant-1822-2022-104-01](https://img.shields.io/badge/RI_Sea_Grant-R_1822_2022_104_01%20-blue)](https://seagrant.gso.uri.edu/research/2020-2022-research-2/), the University of Rhode Island, and the USDA National Institute of Food and Agriculture, Hatch Formula project accession number 1017848.

<img src="assets/media/sg_noaa_uri_logo-copy-768x187.png" width="150" height="55">

### System Design

[![run with neptune](https://img.shields.io/badge/run%20with-neptune-orange?)](https://www.neptunesystems.com/)

#### Flow Through System

![Hyrule schematic](assets/media/Hyrule.jpg)

**Figure 1** **A)** Break down of system design. Seawater chemistry is altered within the header tanks, within which carbon dioxide and nitrogen gas are used to alter seawater pH and dissolved oxygen. Treated seawater (CO2 and N2 gas) is actively pumped from the high treatment header tank into buckets H1-H4. Unmodified water (Ambient Air) is actively pumped from the control treatment header tank into C1-C4. Buckets 1-3 contain larvae, whereas buckets with probes contain no larvae. **B)** Break down of bucket design. Seawater is actively pumped from the water line through a flow meter which is adjacent to activated carbon. a constant mixing of seawater is maintained with a stir bar/plate. Seawater is passively pumped out of the system through a banjo filter with filter sizes varying between 25 to 55 microns depending on larval development. **C)** Break down of header tank design. Seawater is pumped through 25, 10, and 1 micron filters respectively and into header tanks through an activated carbon sock. Within the header tanks ambient, Carbon Dioxide, and Nitrogen gas is actively pumped to achieve cycling of low/high pH and low/high Dissolved oxygen conditions. Conditioned water is continousley pumped from the header tanks into the buckets.


<p float="left">
<img src="assets/media/Hyrule_photo.jpg" width="437"/>
<img src="assets/media/Bucket_photo.jpg" width="300"/>
</p>

**Tile 1** Photo of Hyrule on the left and Inside H4 bucket on the right.

<p align="center">
<img src="assets/media/gas_setup.jpg" width="450">
</p>

**Tile 2.** Tank configuration with N2 tanks on the right in black and CO2 tanks on the left in grey. Tanks are hooked up in a series to a automatic gas changeover eliminator valves, a micro matic 642, CO2 or neptune solenoids and water pump located within the head tanks. 
 

#### Neptune Hardware Layout

<p align="center">
<img src="assets/media/Hyrule_Neptune.jpg" width="650">
</p>

**Figure 2.** Schematic showing the wiring of the neptune system used in the aquarium design to modulate modulate sea water chemistry. Arrows indicate USB connections with arrows pointing to source module.

<p align="center">
<img src="assets/media/Neptune_Hyrule_Photo.jpg" width="650">
</p>


**Tile 3.** Behind the Flow through system in Tile 1. Neptune Configuration with power bank, brain, and modules used in the aquarium design. AirGas tanks are hooked up to a automatic Gas changeover eliminator valves 6091 which is then attached to a Micro Matic 642. From there gas lines are connected to solenoids within which close or open the lines to let gas into the header tanks via a pump. 

### Code

#### Apex Fusion

Apex programming is designed to turn on or off devices plugged into Energy bars depending on logical arguments. For a tutorial on Apex programming and creating virtual outputs see [Neptune Apex Programming Tutorials, Part 5: Virtual Outputs](https://www.reef2reef.com/ams/neptune-apex-programming-tutorials-part-5-virtual-outputs.703/)

Below are real examples of virtual outputs design for manipulating seawater chemistry following diurnal cycling.

 **pH Control:**

<details close>
<summary>C02_H2_DEC</summary>
<br>

```
 Fallback OFF
 Set OFF
 OSC 000:00/000:05/000:20 Then ON
 If pH_Hi < 7.00 Then OFF
 If Time 20:30 to 20:00 Then OFF
 ```
</details>

<details close>
<summary> CO2_HC_LP</summary> 
<br>

```
 Fallback OFF
 Set OFF
 OSC 000:00/000:01/001:29 Then ON
 If pH_Hi < 7.01 Then OFF
 If Time 00:00 to 20:30 Then OFF
```
</details>


<details close>
<summary> CO2_HC_LP2 </summary>
<br>

```
 Fallback OFF
 Set OFF
 OSC 000:00/000:01/001:29 Then on
 If Time 03:00 to 00:00 Then OFF
 If pH_Hi < 7.05 Then OFF
```
</details>

<details close>

<summary> CO2_HC Port </summary>
<br>

 ```
Fallback OFF 
Set OFF
If Output CO2_HC_DEC = ON Then ON
If Output CO2_HC_LP = ON Then ON
If Output CO2_HC_LP2 = ON Then ON
If pH_Hi < 6.80 Then OFF
 ```
</details>

 

 **Dissolved Oxygen (DO)**

<details close>
<summary> N2_HC_LP</summary>
<br>

```
 Fallback OFF
 Set OFF
 If Time 00:00 to 03:00 Then ON
 If DO_Hi < 02.0 Then OFF
```
</details>


<details close>
<summary> N2_HC_INC</summary>
<br>

```
 Fallback OFF
 Set OFF
```
</details>


<details close>
<summary> N2_HC</summary>
<br>

 ```
 Fallback OFF
 Set OFF
 If Output N2_HC_LP = ON Then ON
 If Output N2_HC_INC = ON Then ON
 If Time 20:00 to 00:00 Then ON
 If DO_Hi < 01.5 Then OFF
 ```
</details>

**Ambient Air**

<details close>
<summary> HI_AIR</summary>
<br>

 ```
 Fallback OFF
 Set OFF
 If Time 03:00 to 20:00 Then ON
 ```
</details>


<details close>
<summary> CON_AIR</summary>
<br>

 ```
 Fallback OFF
 Set ON
 ```
</details>

#### Pulling Data From Apex Fusion

Logged data from Apex Fusion is archived and stored in XML format. For an overview of how to access this data see [chapter 10 of the comprehensive reference manual](https://www.neptunesystems.com/downloads/docs/Comprehensive_Reference_Manual.pdf).

An example of Pulling Apex Fusion Data in R as implemented in our aquatic design can be found [HERE](assets/docs/ApexDataPull.rmd).

**Table 1.** Example Dataframe of Apex Fusion data extracted from the R script described above.
|   | Date.Time       | T1_HB | T1_HiBucket | pH_HB | pH_HiBucket | T1_Hi | T1_HiHead | pH_Hi | pH_HiHead |
|---|-----------------|-------|-------------|-------|-------------|-------|-----------|-------|-----------|
| 4 | 1/31/2022 11:44 | T1_HB | 16.9        | pH_HB | 7.99        | T1_Hi | 13.9      | pH_Hi | 8.27      |
| 5 | 1/31/2022 11:45 | T1_HB | 17          | pH_HB | 7.99        | T1_Hi | 14.1      | pH_Hi | 8.22      |
| 6 | 1/31/2022 11:46 | T1_HB | 16.8        | pH_HB | 8.01        | T1_Hi | 15.3      | pH_Hi | 8.18      |
| 7 | 1/31/2022 11:47 | T1_HB | 16.5        | pH_HB | 8.11        | T1_Hi | 17.2      | pH_Hi | 8.14      |
| 8 | 1/31/2022 11:48 | T1_HB | 16.3        | pH_HB | 8.12        | T1_Hi | 18.7      | pH_Hi | 8.11      |


### Parts

**Table 2.** Summary of parts and their model number used in the aquarium design.
| Name                                            | Model #  | Manufacturer | weblink |
|-------------------------------------------------|----------|--------------|---------|
| Power Supply                                    | EB832    | Neptune Systems |  https://www.bulkreefsupply.com/energybar-832-neptune-systems.html  | 
| Apex Controller Base Unit                       | APEXNG   | Neptune Systems  | https://www.bulkreefsupply.com/apex-controller-base-unit-neptune-systems.html  |
| PM1 Module                                      | PM1      | Neptune Systems  | https://www.bulkreefsupply.com/ph-orp-probe-module-pm1-neptune-systems.html  |
| PM3 Module                                      | PM3      | Neptune Systems  | https://www.bulkreefsupply.com/dissolved-oxygen-module-pm3-neptune-systems.html  |
| Temperature Probe                               | PRBTMPJR | Neptune Systems  | https://www.bulkreefsupply.com/temperature-probe-neptune-systems.html  |
| Double Junction pH Probe                        | PRBPHDJ  | Neptune Systems  | https://www.bulkreefsupply.com/lab-grade-double-junction-ph-probe-neptune-systems.html  |
| Oxygaurd Dissolved Oxygen Probe                 | PRBDO    | Neptune Systems  | https://www.bulkreefsupply.com/lab-grade-dissolved-oxygen-probe-neptune-systems.html  |
| CO2 Solenoid                                    | MA955    | Milwaukee Instruments  | https://www.bulkreefsupply.com/milwaukee-ma955-co2-solenoid-valve.html  |
| Neptune Solenoid                                | SV-1     | Neptune Systems  | https://www.bulkreefsupply.com/sv-1-solenoid-valve-neptune-systems.html  |
| Magnetic Stirrer                                | MS5      | Tisch Scientific  | https://scientificfilters.com/lab-equipment-special-price/tisch-mini-magnetic-stirrer-ts-ms-5c?gclid=Cj0KCQjwrs2XBhDjARIsAHVymmT-i2hpgUS7YMSBF2uD-g-T79o3N3w46xLvKUs2P7sAv_hIvv8pyD4aApH1EALw_wcB  |
| Pump                                            | E160713  | Danner Manufacturing  | https://www.thepondguy.com/product/pondmaster-magnetic-drive-water-pump-250/?p=PPCGSHOP&gclid=Cj0KCQjwrs2XBhDjARIsAHVymmSGRK_ekBB5eV9z9XOFn093nkTI3SpVzF76020cXL-5gI6JvJUJaMIaAtfWEALw_wcB  |
| Automatic Gas Changeover Eliminator Valves      | 6091     | Assurance Valve Systems  | https://kegman.net/products/automatic-gas-changeover-eliminator-valves-6091?gclid=Cj0KCQjwrs2XBhDjARIsAHVymmT2BhWED9NU_RLcWsDQKkdDqJfhvJIS2U7Dcf9-N77AbF2GuKb-hhwaArVsEALw_wcB |
| Micro Matic 642                                 | 6422     | Micromatic  | https://www.kegerator.com/micromatic-premium-series-primary-double-gauge-regulator/642.html  |
| Adjustable Irrigation Drippers                  | EZT360 | Tempo Inc. | https://www.dripdepot.com/item/adjustable-dripper-connection-type-threads-pattern-360-degree  |

### Acknowledgements
 
This experimental system represents the hard and tireless work of several individuals.  Graduate students Amy Zyck and Megan Guidry have worked over multiple seasons and semesters troubleshooting this project, and Dr. Alex Hooks was vital to many improvements in 2022.  2020 [URI Coastal Fellows](https://web.uri.edu/coastalfellows/) Seraphina Satkowski came back to work on this project with the lab in 2021 along with 2021 Fellows Madeline Kistler and Joe Maiorano (who came back as a post-bac in 2022). 2022 URI Coastal Fellows working on this system include Hailee Carlson, Ben Poepsel, and Halle Peterlin, along with 2022 [Science and Engineering](https://web.uri.edu/cels/diversity-and-inclusion/sef/) Fellow Lydia Cross.  Lastly, graduate student Gabe Barrett contributed to data scripts and setup this repository.  
 
 
This work was funded by RI Sea Grant [![RI Sea Grant-1822-2022-104-01](https://img.shields.io/badge/RI_Sea_Grant-R_1822_2022_104_01%20-blue)](https://seagrant.gso.uri.edu/research/2020-2022-research-2/), the University of Rhode Island, and the USDA National Institute of Food and Agriculture, Hatch Formula project accession number 1017848.
