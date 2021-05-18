## Supply Data Baltic Sea 2020

This repository contains supply data in zones of the Baltic Sea as a result of historical vessel movements from 2020 based on automatic identification system (AIS) data provided by the Danish Maritime Authority (DMA).

### Data Description
The processed data is located within the data folder of this repository. The folder contains to three different files.

1. The `supply_in_zone.csv` file contains supply in tons on a weekly basis per zone. The zone column corresponds to the respective zone, the timestamp column to the calendar week and the supply_tons column to amount of supply (generalized over all different types of cargo).
2. The `zones.csv` file contains a list of all zones.
3. The `polygones.pkl` file is a pickle file of a dataframe containing definitions of polygons for the zones found in file `zones.csv`.

### Data Processing
The supply data is derived from AIS signals provided by the 

![Alt text](./map.PNG?raw=true "Map")

### References
https://www.dma.dk/SikkerhedTilSoes/Sejladsinformation/AIS/