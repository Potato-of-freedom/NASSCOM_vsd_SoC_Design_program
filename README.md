# Day 1: Inception of open-source EDA, OpenLANE and sky130 PDK

Use the OpenLANE flow to do synthesis of the picorv32a design.<br/>
Find the flop ratio in the picorv32a design using the synthesis output.<br/>
<br/>
## Commands to invoke the OpenLANE flow:<br/>
```
cd Desktop/work/tools/openlane_working_dir/openlane
./flow.tcl -interactive
package require openlane 0.9
prep -design picorv32a
run_synthesis
```
## OpenLANE picorv32a synthesis output:
FLOP RATIO

![Screenshot (318)](https://github.com/user-attachments/assets/9cf259fc-cece-4a9e-bd58-ae8fcfa0ed4c)
![Screenshot (319)](https://github.com/user-attachments/assets/972f9376-8e4b-40d6-82ca-dd534239ae61)
![Screenshot (320)](https://github.com/user-attachments/assets/20cc228f-1fa9-49f5-a604-f6e3bbd65195)

FLOP RATIO = Number of D Flip Flops/Total Number of cells = 0.108 <br/>
<br/>
# Day 2: Good floorplan vs Bad floorplan and introduction to library cells

Use the OpenLANE flow to run synthesis, floorplan and placement of the picorv32a design. <br/>
Display the generated floorplan using magic <br/>

## Commands to invoke the OpenLANE flow: <br/>
```
cd Desktop/work/tools/openlane_working_dir/openlane
./flow.tcl -interactive
package require openlane 0.9
prep -design picorv32a
run_synthesis
run_floorplan
```
## OpenLANE picorv32a synthesis and floorplan

![Screenshot (321)](https://github.com/user-attachments/assets/3463901c-d5bf-4454-9b00-cc18fec93249)
![Screenshot (322)](https://github.com/user-attachments/assets/a0d761af-bbea-4ff7-a342-c595c17fd10f)

Output
![Screenshot (323)](https://github.com/user-attachments/assets/11a5f65d-4286-4398-9edd-a3f5a49aded3)

## Commands to use magic to display floorplan
In another terminal tab, run: <br/>
```
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/31-08_20-55/results/floorplan/
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def &
```
<br/>

## Floorplan: 
![Screenshot (325)](https://github.com/user-attachments/assets/57918e45-6715-4084-8067-11c33d274409)
## Verifying features of floorplan:
Equidistant ports <br/>
![Screenshot (326)](https://github.com/user-attachments/assets/573bdbfe-3545-4c5c-8ea1-0e8c13a36a34)
Diagonally equidistant cells
![Screenshot (327)](https://github.com/user-attachments/assets/5fcde12f-e8d2-42b2-9894-6a82e83ae941)
Unplaced standard cells
![Screenshot (329)](https://github.com/user-attachments/assets/14c93d83-3f2a-4739-bd9f-c53033578b67)

## Command to run placement and display result
```
run_placement
```
<br/>

In the other terminal tab, run: <br/>
```
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/31-08_20-55/results/placement/ 
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def & 
```
<br/>

## After placement:
![Screenshot (330)](https://github.com/user-attachments/assets/3106326f-8a3e-41c1-9805-47dad6e6d60d)
![Screenshot (331)](https://github.com/user-attachments/assets/522427e0-c835-4894-a129-60d034b0be3f)
<br/>

# Day 3: Design library cell using Magic Layout and ngspice characterization
Clone and load custom inverter standard cell design using Magic. <br/>
Edit the spice file and do post-layout simulations using ngspice. <br/>
<br/>

## Commands to clone the git repository and load the custom inverter file
```
cd Desktop/work/tools/openlane_working_dir/openlane 
git clone https://github.com/nickson-jose/vsdstdcelldesign 
cd vsdstdcelldesign 
cp /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech . 
magic -T sky130A.tech sky130_inv.mag & 
```
<br/>

![Screenshot (334)](https://github.com/user-attachments/assets/c249f192-f5b0-440b-8bb0-7475ed1b4a51)
Inverter
![Screenshot (335)](https://github.com/user-attachments/assets/06b61a2d-c54f-4295-a34a-7ed4694268cd)
NMOS and PMOS identification
![Screenshot (338)](https://github.com/user-attachments/assets/02ad169b-9f2b-4663-85dd-3673325cd8bf)
![Screenshot (337)](https://github.com/user-attachments/assets/11b57635-45a8-417a-90b9-829ff6eae673)
Drain and MOS connectivity
![Screenshot (339)](https://github.com/user-attachments/assets/893dfd9f-f6b0-429f-ae20-6d13daa43de6)
![Screenshot (341)](https://github.com/user-attachments/assets/b15c81a1-4d2a-4806-9490-2974215d6d41)
<br/>

## Commands to extract spice file
In the tknon window, run: <br/>
<br/>

```
extract all <br/>
ext2spice cthresh 0 rthresh 0 <br/>
ext2spice <br/>
```
<br/>

spice file
![Screenshot (342)](https://github.com/user-attachments/assets/7a64211e-3794-4c7f-b8de-65053f1d890e)
Created spice file
![Screenshot (343)](https://github.com/user-attachments/assets/83412945-559c-4609-a61a-47894bec2f62)
Edited spice file for transient analysis
![Screenshot (344)](https://github.com/user-attachments/assets/70ad4c5b-a1f0-4ec0-98b3-306bc12d3610)
<br/>

## Commands to run ngspice simulation run
<br/>

```
ngspice sky130_inv.spice <br/>
plot y vs time a <br/>
```
<br/>

![Screenshot (345)](https://github.com/user-attachments/assets/ef02dc23-fcbc-46fc-9b81-b97caa36feb4)
<br/>

## Rise transition time calculation
20% (0.660)
![Screenshot (349)](https://github.com/user-attachments/assets/427e2971-97dc-4adb-a9c2-dda12e2da200)
80% (2.64)
![Screenshot (350)](https://github.com/user-attachments/assets/0cf9a5e2-63b2-4091-85e1-c82a4216561c)
Calculation
![Screenshot (352)](https://github.com/user-attachments/assets/38c8b675-7d85-462f-a96a-80d728b89c4f)
<br/>

Rise transition time = Time taken for output to reach 80% - Time taken for output to reach 20% = 0.04258 ns <br/>
<br/>

## Fall transition time calculation
20% (0.660)
![Screenshot (353)](https://github.com/user-attachments/assets/535cd739-8e1f-42e6-b1c4-04f9c82d2385)
80% (2.64)
![Screenshot (354)](https://github.com/user-attachments/assets/0355ad99-b879-4689-aa16-9bcfbbfec597)
Calculation
![Screenshot (355)](https://github.com/user-attachments/assets/3c092f27-cb6f-4cec-ab3c-b9049441ff0d)
<br/>

Fall transition time = Time taken for output to fall to 20% - Time taken for output to fall to 20% = 0.05989 ns <br/>
<br/>

## Rise cell delay calculation
50% (1.65) 
![Screenshot (357)](https://github.com/user-attachments/assets/12c144cc-f0b6-4c60-9158-451bda626b6c)
Calculation
![Screenshot (358)](https://github.com/user-attachments/assets/1821215a-32cd-49a6-a413-a77604efc62a)
<br/>

Rise cell delay = Time taken for output to rise to 50% - Time taken for input to fall to 50% = 2.029 ns <br/>
<br/>

## Rise cell delay calculation
50% (1.65)
![Screenshot (360)](https://github.com/user-attachments/assets/fdbee5af-53ca-4d6d-bb64-c1760f090f46)
Calculation
![Screenshot (361)](https://github.com/user-attachments/assets/d32f0cc0-dfe5-4a50-8b97-f4e4d31fed35)
<br/>

Fall cell delay = Time taken for output to fall to 50% - Time taken for input to rise to 50% = 3.6056 ns <br/>
<br/>

# Day 4: Pre-layout timing analysis and importance of good clock tree

* Prepare and verify the design to load into the flow. <br/>
* Generate lef files from the custom inverter layout. <br/>
* Add new generated extra lef into the flow in config.tcl <br/>
* Reduce slack violations in synthesis. <br/>
* Run synthesis and placement and verify the cell is accepted into the flow. <br/>
* Post-synthesis timing analysis using openSTA. <br/>
* Do timing ECO fixes. <br/>
* Use the new netlist to run floorplan, placement and CTS. <br/>
* Do post-CTS timing analysis. <br/>
<br/>

## Conditions to check before inserting into the flow
* The input and output ports of the standard cell should lie on the intersection of the vertical and horizontal tracks. <br/>
* The width of the standard cell should be odd multiples of the horizontal track pitch. <br/>
* The height of the standard cell should be even multiples of the vertical track pitch. <br/>
<br/>

## Commands to open custom inverter layout
```
cd Desktop/work/tools/openlane_working_dir/openlane/vsdstdcelldesign
magic -T sky130A.tech sky130_inv.mag &
```

Tracks.info of sky130_fd_sc_hd
![Screenshot (362)](https://github.com/user-attachments/assets/c11a5916-111d-4586-ad35-45eb39b59d39)
<br/>

## Commands to set grids as tracks of locali layer and saving
In the tkon window, run:
```
help grid
grid 0.46um 0.34um 0.23um 0.17um
save sky130_vsdinv.mag
```
<br/>

tkon window and grid syntax
![Screenshot (364)](https://github.com/user-attachments/assets/4e6c9c05-66dc-4e9a-ba9d-7eb10ac7ed7d)
<br/>

Verifying conditions: <br/>

![Screenshot (367)](https://github.com/user-attachments/assets/b66d351e-9999-4460-9feb-ce0b696d4215)
![Screenshot (366)](https://github.com/user-attachments/assets/e46fad12-d96b-4063-9b8b-ddd063d00f6f)
<br/>

Saving the final layout with a custom name:
![Screenshot (368)](https://github.com/user-attachments/assets/9a2800cf-adf6-4f17-ac66-04e64ef1a08a)
<br/>

Verify the saved directory:
![Screenshot (369)](https://github.com/user-attachments/assets/497cbfed-32dc-4eb3-80f6-4eb978e9ea56)
<br/>

Open the newly saved layout and generate lef from layout
![Screenshot (370)](https://github.com/user-attachments/assets/2f2d57b2-641c-41bb-abe3-115a0219df3c)
![Screenshot (371)](https://github.com/user-attachments/assets/8d4f8230-6a79-493f-808c-4620b2bd1829)
<br/>

Newly created lef file
![Screenshot (373)](https://github.com/user-attachments/assets/2db7f9c2-89cc-4dcb-bb39-3f5de388c1c7)
<br/>

## Commands to copy libs and lef to picorv32a design src
```
cp sky130_vsdinv.lef ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/
cp libs/sky130_fd_sc_hd__* ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/
```
<br/>

Verifying the files in the src directory 
![Screenshot (375)](https://github.com/user-attachments/assets/c16b8117-525b-4cf0-90c0-1b9922e7da29)
<br/>

## Commands to edit 'config.tcl' to change the lib files and add extra lefs 
```
set ::env(LIB_SYNTH) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__typical.lib"
set ::env(LIB_FASTEST) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__fast.lib"
set ::env(LIB_SLOWEST) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__slow.lib"
set ::env(LIB_TYPICAL) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__typical.lib"

set ::env(EXTRA_LEFS) [glob $::env(OPENLANE_ROOT)/designs/$::env(DESIGN_NAME)/src/*.lef]
```
<br/>

Edited config.tcl file
![Screenshot (376)](https://github.com/user-attachments/assets/a4cc227c-c93e-42f7-8732-b11f16dcd798)
<br/>

## Commands to invoke OpenLANE flow and including the new lef
```
cd Desktop/work/tools/openlane_working_dir/openlane
docker
./flow.tcl -interactive
package require openlane 0.9
prep -design picorv32a
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs
run_synthesis
```
<br/>

Design preparation, variable assignment and synthesis
![Screenshot (378)](https://github.com/user-attachments/assets/5f08989e-416f-48b5-a0a6-49795bbf1646)
![Screenshot (380)](https://github.com/user-attachments/assets/10063568-5268-4059-bd41-de2409d2731c)
<br/>

Note down design values like chip area, tns and wns before improving timing
![Screenshot (381)](https://github.com/user-attachments/assets/ef730dfe-dfa1-4aa9-b154-7d3ebdd414a2)
![Screenshot (379)](https://github.com/user-attachments/assets/51f45350-b338-4005-abd6-2cb993a6d808)
<br/>

## Command to change parameters and improve timing and synthesis
```
prep -design picorv32a -tag 01-09-_12-06 -overwrite
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs
echo $::env(SYNTH_STRATEGY)
set ::env(SYNTH_STRATEGY) "DELAY 3"
echo $::env(SYNTH_BUFFERING)
echo $::env(SYNTH_SIZING)
set ::env(SYNTH_SIZING) 1
echo $::env(SYNTH_DRIVING_CELL)
run_synthesis
```
<br/>

Updated lef with the custom inverter
![Screenshot (373)](https://github.com/user-attachments/assets/db12db90-3e60-44f3-9839-e43ab670471d)
<br/>

Preparation and synthesis
![Screenshot (383)](https://github.com/user-attachments/assets/cceec874-98ee-4e94-b231-a13a4fd6b6e4)
![Screenshot (385)](https://github.com/user-attachments/assets/b35d745a-7b9c-4b90-b169-e00de0d66b2a)
<br/>

Comparing previous timing values with the improved one
![Screenshot (387)](https://github.com/user-attachments/assets/bbad5efe-b0f1-4b2d-bd88-017274c82f24)
![Screenshot (386)](https://github.com/user-attachments/assets/844067a8-d669-4885-9de4-beb1d4630a98)
<br/>

Areas have increased and the worst negative slack decreased to 0. <br/>
<br/>

Use the improved netlist to run floorplan
```
run_floorplan
```

