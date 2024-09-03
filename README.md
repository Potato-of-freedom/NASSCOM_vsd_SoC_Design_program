# Day 1: Inception of open-source EDA, OpenLANE and sky130 PDK

Use the OpenLANE flow to do synthesis of the picorv32a design.<br/>
Find the flop ratio in the picorv32a design using the synthesis output.<br/>
<br/>
## Commands to invoke the OpenLANE flow:<br/>
cd Desktop/work/tools/openlane_working_dir/openlane <br/>
'''
./flow.tcl -interactive <br/>
package require openlane 0.9 <br/>
prep -design picorv32a <br/>
run_synthesis <br/>
'''
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
cd Desktop/work/tools/openlane_working_dir/openlane <br/>
./flow.tcl -interactive <br/>
package require openlane 0.9 <br/>
prep -design picorv32a <br/>
run_synthesis <br/>
run_floorplan <br/>

## OpenLANE picorv32a synthesis and floorplan

![Screenshot (321)](https://github.com/user-attachments/assets/3463901c-d5bf-4454-9b00-cc18fec93249)
![Screenshot (322)](https://github.com/user-attachments/assets/a0d761af-bbea-4ff7-a342-c595c17fd10f)

Output <br/>
![Screenshot (323)](https://github.com/user-attachments/assets/11a5f65d-4286-4398-9edd-a3f5a49aded3)

## Commands to use magic to display floorplan
In another terminal tab, run: <br/>
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/31-08_20-55/results/floorplan/ <br/>
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def & <br/>
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
run_placement <br/>
<br/>
In the other terminal tab, run: <br/>
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/31-08_20-55/results/placement/ <br/>
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def & <br/>
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
cd Desktop/work/tools/openlane_working_dir/openlane <br/>
git clone https://github.com/nickson-jose/vsdstdcelldesign <br/>
cd vsdstdcelldesign <br/>
cp /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech . <br/>
magic -T sky130A.tech sky130_inv.mag & <br/>
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
extract all <br/>
ext2spice cthresh 0 rthresh 0 <br/>
ext2spice <br/>
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
ngspice sky130_inv.spice <br/>
plot y vs time a <br/>
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
