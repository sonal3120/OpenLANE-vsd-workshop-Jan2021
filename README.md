# OpenLANE-vsd-workshop-Jan2021
The workshop held virtually from 22-26th Jan 2021 through which we learned RTL to GDS2 flow using open source EDA tools. The workshop consisted of theory as well as the lab sessions.
![](images/day1/cover.JPG)

## Table of content
  * 1.1 Familiarization with tool
  * 1.2 Working on Openlane
  * 1.3 Day 1 - How to start with Openlane and synthesis
  * 1.4 Day 2 - Floorplan and placement
  * 1.5 Day 3 - Analysis of Inverter using MAGIC and NGSPICE

# RTL to GDSII using OpenLANE
As OpneLANE is opensource tool that can be installed on any system using a virtual box .To set up OpenLANE in your local PC with virtual box you need :

1. Ubuntu OS
2. Minimum of 25 GB Disk Space
- For installation refer to following git repos: 
1.https://github.com/nickson-jose/openlane_build_script 
2.https://github.com/efabless/openlane 
3.https://github.com/kunalg123/vsdflow

The steps of openlane flow with all required tools are presented hereby:
![](images/day1/openlane%20flow.JPG)

## The various tools used by OpenLANE in ASIC Flow are :
- #### Synthesis
   - yosys - Performs RTL synthesis
  - abc - Performs technology mapping
  - OpenSTA - Pefroms static timing analysis on the resulting netlist to generate timing reports
- #### Floorplan and PDN
  - init_fp - Defines the core area for the macro as well as the rows (used for placement) and the tracks (used for routing)
  - ioplacer - Places the macro input and output ports
  - pdn - Generates the power distribution network
  - tapcell - Inserts welltap and decap cells in the floorplan
- #### Placement
  - RePLace - Performs global placement
  - Resizer - Performs optional optimizations on the design
  - OpenPhySyn - Performs timing optimizations on the design
  - OpenDP - Perfroms detailed placement to legalize the globally placed components
- #### CTS
  - TritonCTS - Synthesizes the clock distribution network (the clock tree)
- #### Routing 
  - FastRoute - Performs global routing to generate a guide file for the detailed router
  - TritonRoute - Performs detailed routing
  - SPEF-Extractor - Performs SPEF extraction
- #### GDSII Generation
  - Magic - Streams out the final GDSII layout file from the routed def
- #### Checks
  - Magic - Performs DRC Checks & Antenna Checks
  - Netgen - Performs LVS Checks
  
 # Day 1: Familiarization with the opensource platform
- The OpenLANE efabless platform provides a platform to perform the RTL to GDS2 flow using opensource PDK from Google. The pdk folder has all the information and in this project we work on Skywater130. It is a 130nm PDK files. There are three subdirectories that we will be using:
  - Skywater-pdk – Contains all the foundry provided PDK related files, i.e timming libraries, tech files etc
  - Open_pdks – Contains scripts that are used to bridge the gap between closed-source and open-source PDK to EDA tool compatibility, like magic, netgen etc.
  - Sky130A – The open-source compatible PDK files. Inside Sky-130A we have 2 subdirectories: libs.tech and libs.ref
  
#### Working space: openlane_working_dir (open in terminal - cd /work/tools/openlane_working_dir)

![](images/day1/1work%20tools.JPG)

![](images/day1/2openlane%20work%20dir.JPG)

#### The libs.tech folder consist of all the tools and libs.ref folder consist the types of foundary files

![](images/day1/3libs%20tech%20folder.JPG)

![](images/day1/4sky_fd_sc_hd.JPG)
It means Sky PDK foundary, stadard cell, high-density 

## How to invoke OPENLANE
- 1. Get into openlane directory (inside openlane_working_dir, one can see this using command ls -ltr) 
- 2. To invoke openlane, type  ./flow.tcl -interactive
- 3. Now, package needs to be called, type  package require openlane 0.9
- 4. Afterward, prepration of design for the picorv32a take place, type  prep -design picorv32a

![](images/day1/5Open%20Lane.JPG)
![](images/day1/8picorv32%20design.JPG)

- Inside designs folder> picorv32a file is present, to see inside the file, type  less config.tcl
![](images/day1/7Design%20Configtcl.JPG)

## Synthesis
- The systhesis can be performed in the openlane platform (after design prepration), type  %run_synthesis.
- Window after systhesis is performed
![](images/day1/10run_synthesis.JPG)

- Yosys and abc are the tools used in the OpenLANE flow for synthesis. it will create a folder by the name of present date in the runs folder, inside which 'results' consist all the details
![](images/day1/11runs%20folder.JPG)
