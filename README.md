## Quartus Prime Lite Edition and ModelSim on Linux

Examples are according to NTUEE Switching Circuit and Logic Design (SCLD) course.

### Install Quartus Prime Lite Edition

1. Go to <https://www.altera.com/downloads/fpga-development-tools/quartus-prime-lite-edition-design-software-version-25-1-linux>. Change the version to the latest one in the drop-down menu of `Version` if a new version exists.
2. Under `Installer (Recommended) > Quartus Prime Lite Edition Installer (SFX)`, click `Download`. You will get a file named `qinst-lite-linux-*std-*.run`, e.g., `qinst-lite-linux-25.1std-1129.run`.
3. Go to the directory where the file locates and execute:
  ```
  chmod +x qinst-lite-linux-*std-*.run
  ./qinst-lite-linux-*std-*.run
  ```
4. Select `Cyclone IV device support` on top of the default ones.
5. Check `Agree to Altera Software License Agreement`.
6. Click `Download & Install`.
7. Wait until it's done and click `Ok` and `Close`.

### Install ModelSim

1. Go to <https://www.altera.com/downloads/simulation-tools/modelsim-fpgas-standard-edition-software-version-20-1-1>. Change the version to the latest one in the drop-down menu of `Version` if a new version exists.
2. Under `Linux Software > ModelSim Software`, click `Download`. You will get a file named `ModelSimSetup-*-linux.run`, e.g., `ModelSimSetup-20.1.1.720-linux.run`.
3. Go to the directory where the file locates and execute:
  ```
  chmod +x ModelSimSetup-*-linux.run
  ./ModelSimSetup-*-linux.run
  ```
4. Click `Next`.
5. Select `ModelSim - Intel FGPA Starter Edition`.
6. Click `Next`.
7. Check `I accept the agreement`.
8. Click `Next`.
9. Click `Next`.
10. Click `Next`.
11. Wait until it's done and click `Finish`.

### Install Required Libraries

Execute:
```
sudo dpkg --add-architecture i386
sudo apt update
sudo apt install libxext6:i386 libx11-6:i386 libxft2:i386 libstdc++6:i386 libxrender1:i386 libfontconfig1:i386 -y
```

### Desktop

Execute the following with `25.1std` replaced with the actual directory name:
```
cat > ~/.local/share/applications/quartus.desktop <<EOF
[Desktop Entry]
Type=Application
Name=Quartus Prime Lite Edition
Comment=Intel Quartus Prime Lite Edition Design Software
Exec=$HOME/altera_lite/25.1std/quartus/bin/quartus
Icon=$HOME/altera_lite/25.1std/quartus/adm/quartusii.png
Terminal=false
Categories=Development;
EOF
```

### Configure ModelSim Path

1. In `$HOME/.bashrc`, add `$HOME/intelFPGA/20.1/modelsim_ase/bin` to `$PATH` with `20.1` replaced with the actual directory name.
2. Open `Quartus Prime Lite Edition`.
3. Go to `Tools > Options > EDA Tool Options`.
4. Set `ModelSim` to `$HOME/intelFPGA/20.1/modelsim_ase/bin` with `20.1` replaced with the actual directory name.

### Examples

#### Lab0

1. Create a project directory (e.g., `~/SCLD/Lab0`).
2. Copy `NTUEE_LogicDesign_Lib` directory to it.
3. Open `Quartus Prime Lite Edition`.
4. Click `Files` > `New Project Wizard`.
5. In `What is the working folder for this project?`, browse and choose or paste the project directory in an absolute path (no `~`, `$HOME`, etc.).
6. Type a project name (e.g., `Lab0`) in `What is the name of this project?`.
7. Click `Next`.
8. Choose `Empty project`.
9. Click `Next`.
10. Click `User Libraries`.
11. In `Project libraries`, check `Use project's relative path` and paste `./NTUEE_LogicDesign_Lib/elements` to `Project library name`.
12. Click `Add`.
13. Click `Ok`.
14. Click `Next`.
15. In `Device family` > `Family`, choose `Cyclone IV E`.
16. In `Show in 'Available devices' list`, paste `EP4CE115F29C7` to `Name filter`.
17. In `Available devices`, click the row with `Name` `EP4CE115F29C7`.
18. Click `Finish`.
19. Click `File` > `New` > `Block Diagram/Schematic File` > `Ok`.
20. Click the symbol of an AND gate.
21. In `Libraries`, expand `./NTUEE_LogicDesign_Lib/elements`, click `and_2`, and click `Ok`.
22. Place the AND gate on the block diagram.
23. Click the downside triangle beside the symbol of 3 input/output pins with `in` on it.
24. Choose `Input` and place two input pins connected to the two inputs of the AND gate.
25. Click the downside triangle beside the symbol of 3 input/output pins with `in` on it.
26. Choose `Output` and place an output pin on the block diagram.
27. Click the symbol of a thin wire in the shape of L rotated 180 degrees.
28. Drag from the output of the AND gate to the output pin to place a wire to connect them.
29. Click the save symbol.
30. Click `Save`.
31. Click the right-sided triangle symbol to start compilation.
32. Wait until it shows `Quartus Prime Full Compilation was successful.`.
33. Click `File` > `New` > `University Program VWF` > `Ok`.
34. Right-click on the empty block in the left part of the pop-up window of `Simulation Waveform Editor`.
35. Click `Insert Node or Bus…` > `Node Finder…` > `List`.
36. Select all three rows in `Nodes Found:` and click `>`.
37. Click `Ok`.
38. Click `Ok`.
39. Click `Simulation` > `Simulation Settings`.
40. Remove `-novopt ` from the fifth line (starting with `vsim`).
41. Click `Save`.
42. Select some intervals in the two input pins and set their value by clicking the symbols labeled with 0, 1, Z on the top.
43. Click `Simulation` > `Run Functional Simulation`.
44. Click `Yes` if a pop-up window is shown asking whether to save, and click `Save`. Files with the extension `vwf` are used to store waveforms and can be copied and pasted to simulate existing waveforms.
45. Close the pop-up window of `Simulation Waveform Editor`.
46. Click `File` > `Create / Update` > `Create HDL Design File from Current File…`.
47. Check `Verilog HDL` and click `Ok`.
48. Click `File` > `Save Project`.
49. Close `Quartus Prime Lite Edition`.

#### FA4

1. Create a project named `FA4` similar to `Lab0`.
2. Click `File` > `New` > `Block Diagram/Schematic File` > `Ok`.
3. Implement a full adder only with gates under `NTUEE_LogicDesign_Lib`.
4. Right-click a pin, click `Properties`, type the new name in `Pin name(s)`, and click `Ok` to rename the augend, addend, carry-in, sum, and carry-out pins to `x`, `y`, `Ci`, `S`, and `Co` respectively.
5. Save the file as `FullAdder1.bdf`.
6. Click `File` > `New` > `Block Symbol File` > `Ok`.
7. Use the drawing tools, that is, from the bold letter A symbol to the curved line symbol, to draw things on the full adder.
8. Drag from the outer edge to the inner edge to add input pins named `x` and `y` respectively on the downside, input pin named `Ci` on the right side, output pin named `S` on the upside, and output pin named `Co` on the left side.
9. Save the file as `FullAdder1.bsf`. Note that names matter since `.bdf` and `.bsf` with the same name will be automatically linked.
10. Click `File` > `New` > `Block Diagram/Schematic File` > `Ok`.
11. Click the symbol of an AND gate. The full adder module will be shown under `Project` and can be used.
12. Design a four-bit parallel adder with four full adders and use `gnd_1` as a logic 0 input for `Ci` of the LSB full adder. (`vcc_1` can be used as a logic 1 input.)
13. An array of `n` pins named `array_name` can be declared by naming each pin as `array_name[0]` to `array_name[n-1]` or naming a pin as `array_name[n-1..0]`. Both ways, the pin with index `i` is named `array_name[i]`. Declare arrays of input pins `A[3..0]`, `B[3..0]` and an array of output pins `S[3..0]`. Add an output pin `Co` for the output `Co` of the MSB full adder.
14. A pin and a wire with the same name are linked automatically. Link `x`s to `A`, `y`s to `B`, and `S`s to `S` with `[0]` being the LSB.
15. Save the file as `FA4.bdf`.
16. Compile.
17. Copy the given `Lab1_1.vwf` to the project directory.
18. Click `File` > `Open`, select `All Files (*.*)` in `Files of type`, select `Lab1_1.vwf`, and click `Open`. Pins with the same name are connected automatically.
19. Remove `-novopt ` and save.
20. Run functional simulation.
21. Close `Simulation Waveform Editor`.

Optional advanced waveform:

1. Click `File` > `New` > `University Program VWF` > `Ok`.
2. Click `Insert Node or Bus…` > `Node Finder…` > `List`.novopt -
3. Select `A`, `B` of `Type` `Input Group`, `S` of `Type` `Output Group`, and `Co` of `Type` `Output`, and Ok.
4. Set radix in `Edit` > `Radix`.
5. Select some intervals and `Ctrl+Alt+R` to generate random values.
6. Remove `-novopt ` and save to a new `.vwf` file.
7. Run functional simulation.
8. Create Verilog HDL design file from `FullAdder1.bdf` and `FA4.bdf` respectively.

#### Verilog Teatbench

Create the testbench file in project directory and run:
```
vlib [whatever_directory_name]
vlog [all-Verilog-files-needed]
vsim -c [testbench_module_name] -do "run -all; quit"
```
or with timing checks during simulation disabled
```
vlib [whatever_directory_name]
vlog +notimingchecks [all-Verilog-files-needed]
vsim -c [testbench_module_name] -do "run -all; quit"
```
The modules provided by `NTUEE_LogicDesign_Lib` is in `NTUEE_LogicDesign_Lib/verilog/elements.v`.

