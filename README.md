
# Public Resources ![Puritz Lab Logo](assets/media/#gh-light-mode-only)

[![run with neptune](https://img.shields.io/badge/run%20with-neptune-orange?)](https://www.neptunesystems.com/)

## Introduction

**MarineEvoEcoLab/PublicResourceSection** provides information on the materials and methods used in the experimental aquarium design. This includes a description of [system design](#System), [list of parts](#Parts), and [code](#Code) paramount to the experiment. 

# System Design

![Hyrule schematic](assets/media/Hyrule.jpg)

**Figure 1** **A)** Break down of system design. Seawater chemistry is altered within the header tanks, within which carbon dioxide and nitrogen gas are used to alter seawater pH and dissolved oxygen. Treated seawater (CO2 and N2 gas) is actively pumped from the high treatment header tank into buckets H1-H4. Unmodified water (Ambient Air) is actively pumped from the control treatment header tank into C1-C4. Buckets 1-3 contain larvae, whereas buckets with probes contain no larvae. **B)** Break down of bucket design. Seawater is actively pumped from the water line through a flow meter which is adjacent to activated carbon. a constant mixing of seawater is maintained with a stir bar/plate. Seawater is passively pumped out of the system through a banjo filter.


<p float="left">
<img src="assets/media/Hyrule_photo.jpg" width="437"/>
<img src="assets/media/Bucket_photo.jpg" width="300"/>
</p>

**Tile 1** Photo of Hyrule on the left and Inside H4 bucket on the right.


<p>
<img src="assets/media/Hyrule_Neptune.jpg" width="650">
</p>

**Figure 2.**

<p>
<img src="assets/media/Hyrule_NeptunePhoto.jpg" width="650">
</p>

**Tile 2.**




# Parts

Full Parts list.... need help with this. 

Want to embed a markdown dataframe with materials and urls

# Code

Below is Apex code used to control seawater chemistry cycling.


 **pH Control:**

<details open>
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

<details open>
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


<details open>
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

<details open>

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

<details open>
<summary> N2_HC_LP</summary>
<br>

```
 Fallback OFF
 Set OFF
 If Time 00:00 to 03:00 Then ON
 If DO_Hi < 02.0 Then OFF
```
</details>


<details open>
<summary> N2_HC_INC</summary>
<br>

```
 Fallback OFF
 Set OFF
```
</details>


<details open>
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

<details open>
<summary> HI_AIR</summary>
<br>

 ```
 Fallback OFF
 Set OFF
 If Time 03:00 to 20:00 Then ON
 ```
</details>


<details open>
<summary> CON_AIR</summary>
<br>

 ```
 Fallback OFF
 Set ON
 ```
</details>







