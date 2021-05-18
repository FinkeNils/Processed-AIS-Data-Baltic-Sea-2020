## Supply Data Baltic Sea 2020

This repository contains supply data in zones of the Baltic Sea as a result of historical vessel movements from 2020 based on automatic identification system (AIS) data provided by the Danish Maritime Authority (DMA).

### Data Description
The processed data is located within the data folder of this repository. The folder contains to three different files.

1. The `supply_in_zone.csv` file contains supply in tons on a weekly basis per zone. The zone column corresponds to the respective zone, the timestamp column to the calendar week and the supply_tons column to amount of supply (generalized over all different types of cargo).
2. The `zones.csv` file contains a list of all zones.
3. The `polygones.pkl` file is a pickle file of a dataframe containing definitions of polygons for the zones found in file `zones.csv`.

### Data Processing
The supply data is derived from AIS signals provided by the Danish Maritime Authority. Since the AIS signals, besides some specifications about the vessel itself, only contain information about the current geo-position of same, further preprocessing steps are necessary to calculate the supply and demand in the different zones of the Baltic Sea. The following parameters, given in AIS signals, are used for the calculations: `timestamp`, `latitude`, `longitude`, `imo`, `mmsi`, `draught`, `destination`. Below screenshot illustrates zones, in which split up the Baltic Sea. To get the polygon definition, please load the `polygones.pkl` in Python using pickle.

To calculate supply and demand in zones based on AIS, following steps have been performed:
1. Get all AIS signals related to one vessel. The `imo` or `mmsi` is a unique identifier for a vessel and can be used to consider every vessel one by one.
2. The tim ewise ordered AIS data (use `timestamp`), more precisely, the geo-position based on `latitude` and `longitude` illustrate the route a the vessel is taking
3. To get supply and demand in zones, the zone in which the vessel is loading (supply zone) and discharging (demand zone) have to be determined. To do so, the vessels `draft` and `destination` give an indication. The point in time, i.e., the AIS signal, in which the `destination` changed compared to the previous signal, denotes the start of a new voyage. Further, if the vessels `draft` has increased, the vessel was loading cargo, thus, the vessel is currently in a supply zone and travels towards a demand zone.
4. Using a vessel database, e.g. Vesselfinder (see below), we determine the vessel maximum capacity in tons, its so called deadweight (dwt).
5. Since the dwt denotes the capacity in tons a vessel can transport, we assume the dwt as the amount of cargo a vessel was loading.
6. Performing such steps for each individual vessel, yields voyages between supply and demand zones including the amount of cargo transported.
7. Aggregating the data on a weekly and zone basis, gives data as provided in the `supply_in_zones.csv` file.

### Baltic Sea Zone Map

![Map](./map.PNG?raw=true "Map")

### References

- Raw AIS Data: https://www.dma.dk/SikkerhedTilSoes/Sejladsinformation/AIS/
- Vessel Database: https://www.vesselfinder.com/de