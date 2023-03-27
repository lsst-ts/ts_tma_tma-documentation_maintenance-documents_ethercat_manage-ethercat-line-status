# ManageEtherCATLineStatus

| **Requested by:** | **GHESA** |
| --- | --- |
| **Doc. Code** | -- |
| **Editor:** | Alberto Izpizua |
| **Approved by:** | Julen García |


## Introduction

This repository has the documentation to diagnose if the EtherCAT line is working properly and to restore the EtherCAT line if it is necessary. The diagnosis shown in this document is very basic, and only allows to now if the EtherCAT line is working properly or not (The NI EtherCAT master does not allow better diagnose). To a deeper diagnose of an issue use the documentation shown in the [EtherCAT Line diagnosis repo](https://gitlab.tekniker.es/publico/3151-lsst/documentation/maintenancedocuments/ethercat/ethercatlinediagnostic).

There are two EtherCAT lines, one attached to the TMA-PXI axis and the other to the AXES PXI. The lines works in a totally independent way.

* TMA-PXI EtherCAT line.
  * Master TMA-PXI (192.168.209.10).
  * Slaves: 
    * Phase power supply.
    * Distributed IOs. They manage the fluid sensors, temperature controllers, limit switches, Bosch motors power supply, and others.
* AXES PXI EtherCAT line.
  * Master AXES PXI (192.168.213.11).
  * Slaves:
    * Azimuth motor drives.
    * Azimuth hall effect sensor.
    * Elevation motor drives.
    * Elevation hall effect sensors.
    * cRIO for EIB synchronization.

## Check EtherCAT status

To check that the EtherCAT status is working properly there are two elements to check. When the EtherCAT line falls down the slave does not update the actual value, so the idea is to check that the actual values are updating.

### TMA-PXI EtherCAT line

Go to Power supply window and check that current has a not constant value in the graph. Also in the Cabinet 0101 Thermal control window, check that the values for the valve feedback and surface temperature are not constant in the graph.

![Power Supply Window](media/OumGkBSoD3.png)

![Cabinet 0101](media/TTXEINzjyi.png)

Also, check that there is no error in the NI Distributed system manager for the TMA-PXI target (192.168.209.10).

![NI Distributed system manager](media/3ezYWjfXeM.png)

### AXES-PXI EtherCAT line

Go to All data view window and select Azimuth Drives. Then in the values table navigate to ensure that all feedback currents are not constant values. Then, change the selection to Elevation drives and check for elevation drives too.

![All data view window](media/eLChudUIwD.png)

Also, check that there is no error in the NI Distributed system manager for the TMA-PXI target (192.168.213.11).

## Restore EtherCAT line

To restore de EtherCAT line use the NI distributed system manager in a PC with access to the TMA VLANs 209 and 213. The PC for Tekniker remote support has this ability.

### TMA-PXI EtherCAT line

<mark >**To restore the EtherCAT line for the TMA-PXI be sure to switch off the next elements**</mark>
* Phase Power supply
* Mirror Cover
* Mirror Cover Locks
* Balancing system
* Deployable Platforms
* Camera Cable Wrap
* Camera rotator
* Azimuth
* Azimuth Cable Wrap
* Azimuth Motor Thermal system
* Elevation Motor Thermal system
* Cabinet 0101 thermal control

Tor steps for restoring the EtherCAT line are:
 1. Select the TMA-PXI target (192.168.209.10) 
 2. Press Change to Configuration button
 3. The EtherCAT line goes to configuration state
 4. Press the Change To Active button
 5. The EtherCAT line goes to active state

![Steps for restoring TMA-PXI EtherCAT line](media/SU61xmZhIP.png)

### AXES PXI EtherCAT line

<mark >**To restore the EtherCAT line for the AXE PXI be sure to switch off the next elements**</mark>
* Azimuth
* Elevation
* Encoder System

Tor steps for restoring the EtherCAT line are:
 1. Select the TMA-PXI target (192.168.213.11) 
 2. Press Change to Configuration button
 3. The EtherCAT line goes to configuration state
 4. Press the Change To Active button
 5. The EtherCAT line goes to active state

![Steps for restoring AXES PXI EtherCAT line](media/lOwEy7aD2g.png)
