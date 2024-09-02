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
## Commands to invoke the OpenLANE flow: <br/>
cd Desktop/work/tools/openlane_working_dir/openlane <br/>
./flow.tcl -interactive <br/>
package require openlane 0.9 <br/>
prep -design picorv32a <br/>
run_synthesis <br/>
run_floorplan <br/>
run_placement <br/>

## OpenLANE picorv32a synthesis, floorplan and placement


