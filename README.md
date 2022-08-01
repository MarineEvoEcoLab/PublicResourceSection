
# Public Resources ![Puritz Lab Logo](assets/media/#gh-light-mode-only)

[![run with neptune](https://img.shields.io/badge/run%20with-neptune-orange?)](https://www.neptunesystems.com/)

## Introduction

**MarineEvoEcoLab/PublicResourceSection** provides information on the materials and methods used in the experimental aquarium design. This includes a description of [system design](#System), [list of parts](#Parts), and [code](#Code) paramount to the experiment. 

# System Design

## Flow Through System

![Hyrule schematic](assets/media/Hyrule.jpg)

**Figure 1** **A)** Break down of system design. Seawater chemistry is altered within the header tanks, within which carbon dioxide and nitrogen gas are used to alter seawater pH and dissolved oxygen. Treated seawater (CO2 and N2 gas) is actively pumped from the high treatment header tank into buckets H1-H4. Unmodified water (Ambient Air) is actively pumped from the control treatment header tank into C1-C4. Buckets 1-3 contain larvae, whereas buckets with probes contain no larvae. **B)** Break down of bucket design. Seawater is actively pumped from the water line through a flow meter which is adjacent to activated carbon. a constant mixing of seawater is maintained with a stir bar/plate. Seawater is passively pumped out of the system through a banjo filter.


<p float="left">
<img src="assets/media/Hyrule_photo.jpg" width="437"/>
<img src="assets/media/Bucket_photo.jpg" width="300"/>
</p>

**Tile 1** Photo of Hyrule on the left and Inside H4 bucket on the right.

<p align="center">
<img src="assets/media/gas_setup.jpg" width="450">
</p>

## Neptune Hardware Layout

<p align="center">
<img src="assets/media/Hyrule_Neptune.jpg" width="650">
</p>

**Figure 2.** Schematic showing the wiring of the neptune system used in the aquarium design to modulate modulate sea water chemistry. Arrows indicate USB connections with arrows pointing to source module.

<p align="center">
<img src="assets/media/Neptune_Hyrule_Photo.jpg" width="650">
</p>

**Tile 3.** Neptune Configuration with power bank, brain, and modules used in the aquarium design. 

# Code

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

# Parts


**Table 1.** Summary of parts and their model number used in the aquarium design. 
| Name                                            | Model #  |
|-------------------------------------------------|----------|
| Power Supply                                    | EB832    |
| Apex Controller Base Unit                       | APEXNG   |
| PM1 Module                                      | PM1      |
| PM3 Module                                      | PM3      |
| Temperature Probe                               | PRBTMPJR |
| Double Junction pH Probe                        | PRBPHDJ  |
| Oxygaurd Dissolved Oxygen Probe                 | PRBDO    |
| CO2 Solenoid                                    | MA955    |
| Neptune Solenoid                                | SV-1     |
| Magnetic Stirrer                                | MS5      |
| Water Pump                                      | E160713  |
| Automatic Gas Changeover Eliminator Valves 6091 | 6091     |
| Micro Matic 642                                 | 6422     |