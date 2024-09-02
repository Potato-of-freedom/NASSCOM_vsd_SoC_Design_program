# Day 1: Inception of open-source EDA, OpenLANE and sky130 PDK

Use the OpenLANE flow to do synthesis of the picorv32a design.<br/>
Find the flop ratio in the picorv32a design using the synthesis output.<br/>
<br/>
## Commands to invoke the OpenLANE flow:<br/>
cd Desktop/work/tools/openlane_working_dir/openlane <br/>
./flow.tcl -interactive <br/>
package require openlane 0.9 <br/>
prep -design picorv32a <br/>
run_synthesis <br/>

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
run_placement <br/>

## OpenLANE picorv32a synthesis, floorplan and placement

![Screenshot (321)](https://github.com/user-attachments/assets/3463901c-d5bf-4454-9b00-cc18fec93249)
![Screenshot (322)](https://github.com/user-attachments/assets/a0d761af-bbea-4ff7-a342-c595c17fd10f)

Output <br/>
![Screenshot (323)](https://github.com/user-attachments/assets/11a5f65d-4286-4398-9edd-a3f5a49aded3)

## Commands to use magic to display floorplan

cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/31-08_20-55/results/floorplan/ <br/>
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def & <br/>
<br/>
## Placed floorplan:
![Screenshot (325)](https://github.com/user-attachments/assets/57918e45-6715-4084-8067-11c33d274409)
