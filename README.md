# Alwin_iiitb_asic_class
This github repository summarizes the progress made in the ASIC class. Quick links:

- [Day-0-Installation](#day-0-Installation)

- [Day-1-Introduction to Verilog RTL design and Synthesis](#Day-1--Introduction-to-Verilog-RTL-design-and-Synthesis)

- [Day-2-Timing libs,hierarchical,flat synthesis,efficient flop coding styles](#Day-2-Timing-libs-hierarchical-flat-synthesis-efficient-flop-coding-styles)

- [Day-3-Combinational and sequential optmizations](#day-3-Combinational-and-sequential-optmizations)

- [Day-4-GLS, blocking vs non-blocking and Synthesis-Simulation mismatch](#5-DAY4--GLS-blocking-vs-non-blocking-and-Synthesis-Simulation-mismatch)

- [Day-5-if, case, for loop and for generate](#6-Day-5-if-case-for-loop-and-for-generate)

- [Day 6-Introduction to RISC-V ISA And GNU compiler toolchain ](#Day6--Introduction-to-RISC-V-ISA-And-GNU-compiler-toolchain)

- [Word of Thanks](#Word-of-Thanks)

- [Reference](#reference)

## Day-0-Installation
<details>
 <summary> Summary </summary>
	
I installed the needed tools.

</details>	
	
 <details>
 <summary> Yosys </summary>
I installed Yosys using the following commands:
     
```
$ git clone https://github.com/YosysHQ/yosys.git
$ cd yosys-master 
$ sudo apt install make 
$ sudo apt-get install build-essential clang bison flex \
    libreadline-dev gawk tcl-dev libffi-dev git \
    graphviz xdot pkg-config python3 libboost-system-dev \
    libboost-python-dev libboost-filesystem-dev zlib1g-dev
$ make 
$ sudo make install
```
     
Below is the screenshot showing sucessful launch:

<img width="1085" alt="yosys" src="https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/4048f403-62c7-4be1-9bc3-64d9d43e68ea">
</details>

<details>  
<summary> Iverilog </summary>
    
I installed iverilog using the following command:

```
sudo apt-get install iverilog
```

Below is the screenshot showing sucessful launch:

<img width="1085" alt="iverilog" src="https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/e2e0ae1e-ef20-4b91-a21a-2d82768702f5">

</details>

<details>  
    
<summary> Gtkwave </summary>

I installed gtkwave using the following command:

```
sudo apt-get install gtkwave
```

Below is the screenshot showing sucessful launch:

<img width="1085" alt="gtkwave" src="https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/0e6ac3aa-0886-4c4e-b553-a50466c08758">
</details>

<details>

<summary> Ngspice </summary>

I downloaded the tarball from https://sourceforge.net/projects/ngspice/files/ to a local directory and unpacked it using the following commands:

```
tar -zxvf ngspice-40.tar.gz
cd ngspice-40
mkdir release
cd release
../configure  --with-x --with-readline=yes --disable-debug
make
sudo make install

```
Below is the screenshot showing sucessful launch:

<img width="1085" alt="ngspice" src="https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/bcf2a79e-e185-40a2-b17d-1ed8b496c2d4">

</details>

<details>

<summary> Magic </summary>

I installed magic using the following commands:

```
sudo apt-get install m4
sudo apt-get install tcsh
sudo apt-get install csh
sudo apt-get install libx11-dev
sudo apt-get install tcl-dev tk-dev
sudo apt-get install libcairo2-dev
sudo apt-get install mesa-common-dev libglu1-mesa-dev
sudo apt-get install libncurses-dev

```
Below is the screenshot showing sucessful launch:

<img width="1085" alt="magic" src="https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/d66883ee-6262-4e1e-a4a9-186f96e0fb4d">

</details>

<details>

<summary> OpenSTA </summary>

I installed and built OpenSTA (including the needed packages) using the following commands:

```
sudo apt-get install cmake clang gcctcl swig bison flex
git clone https://github.com/The-OpenROAD-Project/OpenSTA.git
cd OpenSTA
mkdir build
cd build
cmake ..
make

```
Below is the screenshot showing sucessful launch:

<img width="1085" alt="opensta" src="https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/594acfb4-e266-41c3-aba3-4bcd15ce946a">
</details>

<details>

<summary> OpenLANE</summary>

I installed and built OpenLANE (including the needed packages) using the following commands:

```
sudo apt-get update
sudo apt-get upgrade
sudo apt install -y build-essential python3 python3-venv python3-pip make git

sudo apt install apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt update

sudo apt install docker-ce docker-ce-cli containerd.io

sudo docker run hello-world

sudo groupadd docker
sudo usermod -aG docker $USER
sudo reboot 

# After reboot
docker run hello-world

```
Below is the screenshot showing sucessful launch:

<img width="1085" alt="openlane" src="https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/ec437280-7862-478b-bfbf-9da7d730892e">

</details>

# Day-1-Introduction to Verilog RTL design and Synthesis
<details>
<summary>Introduction to Verilog RTL design and Synthesis</summary>

**RTL Design**: In simple terms RTL design or Register Transfer Level design is a method in which we can transfer data from one register to another. In RTL design we write code for Combinational and Sequential circuits in HDL(Hardware Description Language) like Verilog or VerilogHDL which can model logical and hardware operation. RTL design can be one code or set of verilog codes. **One key note is that we need to write RTL design with optimized and synthesizable (realizable as physical gates)**.

**Sample RTL design outline:**

	module module_name (port list);
		//declarations;
		//initializations;
		//continuos concurrent assigments;
		//procedural blocks;
	endmodule

**Test Bench**: Using Verilog we can write a test bench to apply stimulus to the RTL design and verify the results of the design by instantiating design with in test bench. Up-front verification becomes very important as design size increases in size and complexity while any project progresses. This ensures simulation results matches with post synthesis results. A test bench can have two parts, the one generates input signals for the model to be tested while the other part checks the output signals from the design under test. It can be represented as follows.
![Capture2](https://user-images.githubusercontent.com/104454253/166088950-634be5a4-7d5a-4b43-9990-711f8f660aaf.JPG)

**Simulation**: RTL design is checked for adherence to its design specification using simulation by giving sample inputs. This helps finding and fixing bugs in the RTL design in the early stages of design development. 

**Simulator**: Simulator is the tool used for this process. It looks for changes on input signals to evaluate outputs. No change in output if there is no change in input signals
Here is the flow of frondend design:
![Capture1](https://user-images.githubusercontent.com/104454253/166088866-80a4e792-7db7-4bf2-b3b5-b4b9b92452a8.JPG)

<details>
 <summary> Introduction to open source simulator iverilog and gtkwave </summary>
	
**iverilog**: iverilog stands for Icarus Verilog. Icarus Verilog is an implementation of the Verilog hardware description language. It supports the 1995, 2001 and 2005 versions of the standard, portions of SystemVerilog, and some extensions.

**Gtkwave**: GTKWave is a fully featured GTK+ based wave viewer for Unix, Win32, and Mac OSX which reads LXT, LXT2, VZT, FST, and GHW files as well as standard Verilog VCD/EVCD files and allows their viewing. 
</details>

### Lab examples using iverilog and gtkwave

We were introducted to Linux operating system and were made aware of the basic commands. Using **git clone** command we've cloned library files like standard cell library, primitives which are used for synthesis and few verilog codes for practice.
![WhatsApp Image 2023-08-08 at 7 26 11 AM(2)](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/b256013c-440a-494a-af13-8b6ee89aa416)
![WhatsApp Image 2023-08-08 at 7 26 11 AM(1)](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/45a367ca-2db5-4381-848f-66f6e36bd95e)
![WhatsApp Image 2023-08-08 at 7 26 11 AM](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/dde88c97-efef-4178-9c93-15623953efe8)
In this session, I've performed simulation of multiplexer. I've added both the RTL design code and test bench code in iverilog to generate vcd file which I used in gtkwave generator to get the output waveformes after simulation. The output was generated by taking the inputs from the testbench code. 


Here is the code :<br />

	module good_mux (input i0 , input i1 , input sel , output reg y); 
		always @ (*)
		begin
			if(sel)
			y <= i1;
			else 
			y <= i0;
		end
	endmodule


	`timescale 1ns / 1ps
	module tb_good_mux;
	// Inputs
	reg i0,i1,sel;
	// Outputs
	wire y;
      		// Instantiate the Unit Under Test (UUT), name based instantiation
		good_mux uut (.sel(sel),.i0(i0),.i1(i1),.y(y));
		//good_mux uut (sel,i0,i1,y);  //order based instantiation
	initial begin
		$dumpfile("tb_good_mux.vcd");
		$dumpvars(0,tb_good_mux);
		// Initialize Inputs
		sel = 0;
		i0 = 0;
		i1 = 0;
		#300 $finish;
	end
	always #75 sel = ~sel;
	always #10 i0 = ~i0;
	always #55 i1 = ~i1;
	endmodule

</details>

<details>
 <summary> Introduction to Yosys synthesizer </summary>

**Synthesis**: Synthesis transforms the simple RTL design into a gate-level netlist with all the constraints as specified by the designer. In simple language, Synthesis is a process that converts the abstract form of design to a properly implemented chip in terms of logic gates.

Synthesis takes place in multiple steps:
- Converting RTL into simple logic gates.
- Mapping those gates to actual technology-dependent logic gates available in the technology libraries.
- Optimizing the mapped netlist keeping the constraints set by the designer intact.

**Synthesizer**: It is a tool we use to convert out RTL design code to netlist. Yosys is the tool I've used in this workshop.
Here is the flow of above processess.

![rtl-netlist](https://user-images.githubusercontent.com/104454253/166097298-41d913ee-640d-4e1e-9e70-5bf427f35ef4.JPG)

**Yosys**:Yosys is a framework for RTL synthesis and more. It currently has extensive Verilog-2005 support and provides a basic set of synthesis algorithms for various application domains. Yosys is the core component of most our implementation and verification flows.

I was given an overview of the operation of the tool and the files we'll need to provide the tool to give the required netlist. We give RTL design code, .lib file which has all the building blocks of the netlist. Using these two files, Yosys synthesizer generates a netlist file. .lib basically is a collection of logical modules like, And, Or, Not etc.... These are equivalent gate level representation of the RTL code. 

Below are the commands to perform above synthesis.

- RTL Design  - read_verilog
- .lib        - read_liberty
- netlist file- write_verilog

**Operational flow of Yosys Synthesizer**

![Synthesizer](https://user-images.githubusercontent.com/104454253/166094901-27c70c0d-8ef2-4a34-a4b2-7307af492698.JPG)

**Verification of Synthesized design**: In order to make sure that there are no errors in the netlist, we'll have to verify the synthesized circuit. The netlist verification flow can be seen in the below image:

![Synthesisgtkwave](https://user-images.githubusercontent.com/104454253/166095185-f82dbbe0-afb4-43ac-8ec6-6b75491d6b58.JPG)

The gtkwave output for the netlist should match the output waveform for the RTL design file. As netlist and design code have same set of inputs and outputs, we can use the same testbench and compare the waveforms.

**Introduction to loigc synthesis**: Below is the snippet RTL code and equivalent digital circuit:

![sample rtl](https://user-images.githubusercontent.com/104454253/166097112-0fb5685c-fe88-4ca0-8ecf-bc014de46088.JPG)

In the above image, mapping of code and digital circuit is done using Synthesis.

**.lib**: It is a collection of logical modules like, And, Or, Not etc...It has different flvors of same gate like 2 input AND gate, 3 input AND gate etc... with different performace speed.

**Need for different flavours of gate**: In order to make a faster circuit, the clock frequency should be high. For that the time period of the clock should be as low as possible. However, in a sequential circuit, clock period depends on three factors so that data is not lost or to be glitch free.

For the below circuit the three factors are
- Clock to Q of flipflop A
- Propagation delay of combinational circuit
- Setuptime of flipflop B
![Timedelay circuit](https://user-images.githubusercontent.com/104454253/166098730-33bf0734-abec-466f-abe2-a2ac6813b5e0.JPG)

The equation is as follows

![Time](https://user-images.githubusercontent.com/104454253/166097710-2c1099e3-6323-496c-8eb7-12ee04c12096.JPG)

As per the above equation, for a smaller propagation delay, we need faster cells.
But again, why do we have faster cells? This is to ensure that there are no HOLD time violations at B flipflop.
**This complete collection forms .lib**

**Faster Cells vs Slower Cells**: 
Load in digital circuit is of **Capacitence**. Faster the charging or dicharging of capacitance, lesser is the celll delay. However, for a quick charge/ discharge of capacitor, we need transistors capable of sourcing more current i.e, we need WIDE TRANSISTORS. 

Wider transistors have lesser delay but consume more area and power. Narrow transistors are other way around. Faster cells come with a cost of area and power.

**Selection of the Cells**: We'll need to guide the Synthesizer to choose the flavour of cells that is optimum for implementation of logic circuit. Keeping in view of previous observations of faster vs slower cells,to avoid hold time violations, larger circuits, sluggish circuits, we offer guidance to synthesizer in the form of **Constraints**.

Below is an illustration of Synthesis.

![Screenshot (44)](https://user-images.githubusercontent.com/104454253/166099264-e3842e91-1a27-44ae-830c-0757dc5b1a5e.png)

### Labs on Yosys introduction
Invoking Yosys:

![yosys](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/eb5549da-64f2-4d68-8979-57a2143262ce)

Snippet below illustrates reading .lib, design and choosing the module to synthesize:

![Screenshot from 2023-08-08 10-21-40](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/26ff7142-0f8f-4cd5-9849-c036b197bbd4)

**Generating Netlist**: The logic of good_mux will be realizable using gates in the sky130_fd_sc_hd__tt_025C_1v80.lib file

![Screenshot from 2023-08-08 10-22-51](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/c7694b33-1b54-493b-b6bc-85d040e35d3a)

Below is the snippet showing the synthesis results and synthesized circuit for multiplexer.

![Screenshot from 2023-08-08 10-23-45](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/791ad35c-5de0-498a-9905-12bd9ca2f0a4)

**Netlist code**:

![Screenshot from 2023-08-08 10-42-51](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/b429c86e-0065-4291-8618-23fe19702754)

![Screenshot from 2023-08-08 10-25-52](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/e25cc2dc-193f-470d-bee6-6281d9679dce)

**Simplified netlist code**: This code consisits of additional switch. To further simplify, we use below command

![Screenshot from 2023-08-08 10-51-35](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/ff04b444-6e37-4573-b8f9-a8c9c1d4b1ab)

![Screenshot from 2023-08-08 10-44-30](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/53a60bf5-6834-4ec2-875a-40440bf0f428)

```
$ yosys
yosys> read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
yosys> read_verilog good_mux.v 
yosys> synth -top good_mux 
yosys> abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
yosys> show

yosys> write_verilog good_mux_netlist.v 
yosys> !vim good_mux_netlist.v 

yosys> write_verilog -noattr good_mux_netlist.v
yosys> !vim good_mux_netlist.v 

```
</details>

# Day-2-Timing libs, hierarchical, flat synthesis, efficient flop coding styles
<details>
<summary>Introduction to timing .libs</summary>

### LAB- Introduction to dot Lib
This lab guides us through the .lib files where we have all the gates coded in. According to the below parameters the libraries will be characterized to model the variations.

![lib1](https://user-images.githubusercontent.com/104454253/166105787-19a638a3-fe01-4fcf-828d-0b56a6acb8f7.JPG)

With in the lib file, the gates are delared as follows to meet the variations due to process, temperatures and voltages.

![Screenshot from 2023-08-09 17-09-04](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/246de5aa-04a8-4ee3-9220-458653f8dd5e)

For the above example, for all the 32 cominations i.e 2^5 (5 is no.of variables), the delay, power and all the related parameters for each gate are mentioned.

![Screenshot from 2023-08-09 17-08-37](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/293b0222-7471-4f5a-b626-910ad9e92d20)

This image displays the power consumtion comparision.

![lib5](https://user-images.githubusercontent.com/104454253/166107259-6fa398a4-2099-4da3-9b93-818c2c3f2404.JPG)

Below image is the delay order for the different flavor of gates.

![delay_libraries](https://user-images.githubusercontent.com/104454253/166187423-d21465e1-abc3-4ad0-a534-60f8e706ab6f.JPG)

 </details>

 <details>
<summary> LAB- Hierarchical synthesis and flat synthesis </summary>

**multiple_module**<br />

	module sub_module2 (input a, input b, output y);
		assign y = a | b;
	endmodule
	
	module sub_module1 (input a, input b, output y);
		assign y = a&b;
	endmodule


	module multiple_modules (input a, input b, input c , output y);
	wire net1;
	sub_module1 u1(.a(a),.b(b),.y(net1));  //net1 = a&b
	sub_module2 u2(.a(net1),.b(c),.y(y));  //y = net1|c ,ie y = a&b + c;
	endmodule

This is the schematic as per the connections in the above module.

![submodel](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/80bb4a1b-4fcd-42c9-8e8b-72ee65a625c1)

However, the yosys synthesizer generates the following schematic instead of the above one and with in the submodules, the connections are made

```
$ yosys
yosys> read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
yosys> read_verilog multiple_modules.v
yosys> synth -top multiple_modules
yosys> show multiple_modules 

```
![Screenshot from 2023-08-10 06-14-30](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/6a5fc933-a6b3-4b11-a19d-fcad8a5ccb43)

The synthesizer considers the module hierarcy and does the mapping accordting to instantiation. Here is the hierarchical netlist code for the  multiple_modules:

	module multiple_modules(a, b, c, y);
		  input a;
 		 input b;
 		 input c;
		  wire net1;
 		 output y;
 	  sub_module1 u1 (.a(a),.b(b),.y(net1) );
	  sub_module2 u2 (.a(net1),.b(c),.y(y));
	endmodule
	
	module sub_module1(a, b, y);
 	 wire _0_;
 	 wire _1_;
 	 wire _2_;
 	 input a;
 	 input b;
 	 output y;
 	 sky130_fd_sc_hd__and2_0 _3_ (.A(_1_),.B(_0_),.X(_2_));
 	 assign _1_ = b;
 	 assign _0_ = a;
 	 assign y = _2_;
	endmodule

	module sub_module2(a, b, y);
  	wire _0_;
 	 wire _1_;
 	 wire _2_;
  	input a;
  	input b;
 	 output y;
 	 sky130_fd_sc_hd__lpflow_inputiso1p_1 _3_ (.A(_1_),.SLEEP(_0_),.X(_2_) );
 	 assign _1_ = b;
 	 assign _0_ = a;
 	 assign y = _2_;
	endmodule

Flattened netlist:

In flattened netlist, the hierarcies are flattend out and there is single module i.e, gates are instantiated directly instead of sub_modules. Here is the flattened netlist code for the  multiple_modules:

	module multiple_modules(a, b, c, y);
 		 wire _0_;
  		 wire _1_;
 		 wire _2_;
 		 wire _3_;
		 wire _4_;
		 wire _5_;
 		 input a;
 		 input b;
 		 input c;
 		 wire net1;
 		 wire \u1.a ;
		 wire \u1.b ;
		 wire \u1.y ;
		 wire \u2.a ;
		 wire \u2.b ;
 		 wire \u2.y ;
  		output y;
 		 sky130_fd_sc_hd__and2_0 _6_ (
  		  .A(_1_),
  		 .B(_0_),
   		 .X(_2_)
  		);
 		 sky130_fd_sc_hd__lpflow_inputiso1p_1 _7_ (
  		  .A(_4_),
 		  .SLEEP(_3_),
  		  .X(_5_)
 		 );
 		 assign _4_ = \u2.b ;
 		 assign _3_ = \u2.a ;
 		 assign \u2.y  = _5_;
 		 assign \u2.a  = net1;
		 assign \u2.b  = c;
 		 assign y = \u2.y ;
		 assign _1_ = \u1.b ;
		 assign _0_ = \u1.a ;
		 assign \u1.y  = _2_;
		 assign \u1.a  = a;
		 assign \u1.b  = b;
 		 assign net1 = \u1.y ;
		endmodule

The commands to get the hierarchical and flattened netlists is shown below:

**yosys> write_verilog -noattr multiple_modules_hier.v**

8. Executing Verilog backend.
Dumping module `\multiple_modules'.
Dumping module `\sub_module1'.
Dumping module `\sub_module2'.

**yosys> !gvim multiple_modules_hier.v**

11. Shell command: gvim multiple_modules_hier.v

**yosys> flatten**

12. Executing FLATTEN pass (flatten design).
Deleting now unused module sub_module1.
Deleting now unused module sub_module2.
<suppressed ~2 debug messages>

**yosys> write_verilog -noattr multiple_modules_flat.v**

13. Executing Verilog backend.
Dumping module `\multiple_modules'.

**yosys> !gvim multiple_modules_flat.v**

14. Shell command: gvim multiple_modules_flat.v

This is the synthyesized circuit for a flattened netlist. Here u1 and u2 are flattened and directly or gates are realized.

![lab51](https://user-images.githubusercontent.com/104454253/166112988-1b02eea6-a6e8-4a7e-8eee-0772182f914f.JPG)

Here is the synthesized circuit of sub_module1. We are also generating module level synthesis so that if there is a top module with multiple and same sub_modules, we can synthesize it once and can use and connect the same netlist multiple times in the top module netlist.

Another reason to generate module level synthesis and then stictch them together is to avoid errors in a top module if its massive and consists of several sub modules. Generating netlist for synthesis and then stiching it together in top level becomes easier and reduces risk of output mismatch.

We control this synthesis using **synth -top <module_name>** command

![lab52](https://user-images.githubusercontent.com/104454253/166113791-5c245c1c-727a-4f15-aaec-9fef1b817aec.JPG)

 </details>
 
<details>
	<summary>Various Flop coding styles and optimization</summary>
	
**Why Flops and Flop coding styles**

In this session, the discussion was about how to code various types of flops and various styles of coding a flop.

**Why a Flop?**

 In a combinational circuit, the output changes after the propagation delay of the circuit once inputs are changed. During the propagation of data, if there are different paths with different propagation delays, there might be a chance of getting a glitch at the output.<br />
 If there are multiple combinational circuits in the design, the occurances of glitches are more thereby making the output unstable.<br />
To curb this drawback, we are going for flops to store the data from the cominational circuits. When a flop is used, the output of combinational circuit is stored in     it and it is propagated only at the posedge or negedge of the clock so that the next combinational circuit gets a glitch free input thereby stabilising the output.
 
 We use initialize signals or control pins called **set** and **reset** on a flop to initialize the flop, other wise a garbage value to sent out to the next combinational circuit. These control pins can be synchronous or asynchronous.

### Lab- flop synthesis simulations

**d-flipflop with asynchronous reset**- Here the output **q** goes low whenever reset is high and will not wait for the clock's posedge, i.e irrespective of clock, the output is changed to low.

![asyn](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/ff524bd6-0952-48b5-9e05-4992d13cb62b)
 
	 module dff_asyncres ( input clk ,  input async_reset , input d , output reg q );
		always @ (posedge clk , posedge async_reset)
		begin
			if(async_reset)
				q <= 1'b0;
			else	
				q <= d;
		end
	endmodule

**Simulation**:

![Screenshot from 2023-08-10 06-18-49](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/e5f28498-b4dd-4be5-8837-4c732351ef7c)

**Synthesized circuit**:

![Screenshot from 2023-08-10 06-24-31](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/cca2575d-9f9e-4f81-bf1d-2230e5024e42)

**d-flipflop with asynchronous set**- Here the output **q** goes high whenever set is high and will not wait for the clock's posedge, i.e irrespective of clock, the output is changed to high.
 

	module dff_async_set ( input clk ,  input async_set , input d , output reg q );
		always @ (posedge clk , posedge async_set)
		begin
			if(async_set)
				q <= 1'b1;
			else
				q <= d;
		end
	endmodule

**Simulation**:

![Screenshot from 2023-08-10 06-29-39](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/bc503e0b-7e9b-466c-b7cb-1d806f6baccd)

**Synthesized circuit**:


![Screenshot from 2023-08-10 06-35-34](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/417c745c-5278-441e-b70b-6fc33861d70d)


**d-flipflop with synchronous reset**- Here the output **q** goes low whenever reset is high and at the positive edge of the clock. Here the reset of the output depends on the clock.



	module dff_syncres ( input clk , input async_reset , input sync_reset , input d , output reg q );
		always @ (posedge clk )
		begin
			if (sync_reset)
				q <= 1'b0;
			else	
				q <= d;
		end
	endmodule

**Simulation**:

![Screenshot from 2023-08-10 06-32-32](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/77e5a2d7-40e6-43bc-acd4-1921968864e0)

**Synthesized circuit**:

![Screenshot from 2023-08-10 06-37-44](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/def48f40-9d42-4a2f-9689-daca09709d9b)

**d-flipflop with synchronous and asynchronbous reset**- Here the output **q** goes low whenever asynchronous reset is high where output doesn't depend on clock and also when synchronous reset is high and posedge of clock occurs.

![asynsyn](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/3abae8d4-0874-40a5-9e51-3515e30afdd0)

	module dff_asyncres_syncres ( input clk , input async_reset , input sync_reset , input d , output reg q );
		always @ (posedge clk , posedge async_reset)
		begin
			if(async_reset)
				q <= 1'b0;
			else if (sync_reset)
				q <= 1'b0;
			else	
				q <= d;
		end
	endmodule

**Simulation**:

![Screenshot from 2023-08-10 06-41-19](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/dfa4dde4-3b87-4a32-91de-569894974dde)

**Synthesized circuit**:

![Screenshot from 2023-08-10 06-43-45](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/b9cb8141-1f48-4d44-94f9-d981fee6f407)

</details>

<details>
	
<summary> Interesting optimisations </summary>

This lab session deals with some automatic and interesting optimisations of the circuits based on logic. In the below example, multiplying a number with 2 doesn't need any additional hardeware and only needs connecting the bits from **a** to **y** and grounding the LSB bit of y is enough and the same is realized by Yosys.

	module mul2 (input [2:0] a, output [3:0] y);
		assign y = a * 2;
	endmodule

**Synthesized circuit**:

![Screenshot from 2023-08-10 13-06-07](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/1c3324c9-7f38-4e5c-a27c-3f35b54e6c93)

When it comes to multiplying with powers of 2, it just needs shifting as shown in the below image:

![mul2](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/fe739548-f9d5-43b3-92a8-67d87c8f5191)

**Netlist for the above schematic**

![Screenshot from 2023-08-10 13-09-41](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/e80a2c59-5d34-4951-8d25-d5f0108b2daf)

Special case of multiplying **a** with **9**. The result is shown in the below image:

![mul9](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/0867ed5b-9fb1-44ef-93c1-d48ebbc984bb)

The schematic for the same is shown below:

![Screenshot from 2023-08-10 13-12-25](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/d24c06b6-0250-4ed4-b2fb-2ea7b7b08dcc)

**Netlist for the above schematic**

![Screenshot from 2023-08-10 13-13-57](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/292f924c-e05c-42eb-b987-459b8c838f2c)
 
</details>

# Day3-Combinational and sequential optmizations
<details>
<summary> Combinational logic optimization with examples </summary>

Optimising the combinational logic circuit is squeezing the logic to get the most optimized digital design so that the circuit finally is area and power efficient. This is achieved by the synthesis tool using various techniques and gives us the most optimized circuit.

**Techniques for optimization**:
- Constant propagation which is Direct optimizxation technique
- Boolean logic optimization using K-map or Quine McKluskey

Here is an example for **Constant Propagation**

![optimizations1](https://user-images.githubusercontent.com/104454253/166127772-9ff3dc8e-c5e2-4621-8070-d300df31667e.JPG)

In the above example, if we considor the trasnsistor level circuit of output Y, it has 6 MOS trasistors and when it comes to invertor, only 2 transistors will be sufficient. This is achieved by making A as contstant and propagating the same to output.

Example for **Boolean logic optimization**:

Let's consider an example concurrent statement **assign y=a?(b?c:(c?a:0)):(!c)**

The above expression is using a ternary operator which realizes a series of multiplexers, however, when we write the boolean expression at outputs of each mux and simplify them further using boolean reduction techniques, the outout **y** turns out be just **~(a^c)**

Command to optimize the circuit by yosys is **yosys> opt_clean -purge**

**Example-1**

![IMG_1861](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/d8df4dab-f4a6-4885-8dd9-5561c6450b93)

	module opt_check (input a , input b , output y);
		assign y = a?b:0;
	endmodule

**Optimized circuit**

![Screenshot from 2023-08-10 15-37-40](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/c5d4e651-6e9e-40a2-8895-e92a0796e619)

**Example-2**

	module opt_check2 (input a , input b , output y);
		assign y = a?1:b;
	endmodule

![Screenshot from 2023-08-10 15-38-23](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/c038deb1-4e4c-48e7-a520-12e4275ec5c4)

 **Example-3**

	module opt_check3 (input a , input b, input c , output y);
		assign y = a?(c?b:0):0;
	endmodule

![Screenshot from 2023-08-10 15-39-00](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/f6729e2a-5503-4e6f-bd26-4da43ae99ce5)

 **Example-4**

	module opt_check4 (input a , input b , input c , output y);
		assign y = a?(b?(a & c ):c):(!c);
	endmodule

![Screenshot from 2023-08-10 15-39-24](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/a8016b15-cc64-42c7-91f0-69c3a4a85751)

 **Example- 5**:Here there is multiple modules present so we will try to check whether those module are being used or not by using following commands:

```
yosys:read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
yosys:read_verilog multiple_module_opt2.v
yosys:synth -top multiple_module_opt2
yosys:abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
yosys:flatten
yosys:opt_clean -purge
yosys:show

```

 

	module sub_module(input a , input b , output y);
		assign y = a & b;
	endmodule

	module multiple_module_opt2(input a , input b , input c , input d , output y);
		wire n1,n2,n3;
		sub_module U1 (.a(a) , .b(1'b0) , .y(n1));
		sub_module U2 (.a(b), .b(c) , .y(n2));
		sub_module U3 (.a(n2), .b(d) , .y(n3));
		sub_module U4 (.a(n3), .b(n1) , .y(y));
	endmodule

**Before Flatten**

![Screenshot from 2023-08-10 16-33-21](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/f9e8f641-8927-4a5c-90be-eb8cc740d5df)

**After Flatten**

![Screenshot from 2023-08-14 03-29-45](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/e16e8f44-2815-4bbf-9aa7-4f1b83dae702)

**Example-6**


		module sub_module1(input a , input b , output y);
		 assign y = a & b;
		endmodule

		module sub_module2(input a , input b , output y);
		 assign y = a^b;
		endmodule

		module multiple_module_opt(input a , input b , input c , input d , output y);
		wire n1,n2,n3;
		sub_module1 U1 (.a(a) , .b(1'b1) , .y(n1));
		sub_module2 U2 (.a(n1), .b(1'b0) , .y(n2));
		sub_module2 U3 (.a(b), .b(d) , .y(n3));

		assign y = c | (b & n1); 
		endmodule

**Before Flatten**

![Screenshot from 2023-08-10 16-34-39](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/7f74441f-9d3f-44c1-8946-dcf51018ba87)

**After Flatten**

![Screenshot from 2023-08-14 03-22-41](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/42a74a39-0f92-4df5-81ca-7de25a2b40bb)
 
</details>

<details>
<summary>Sequential Logic Optimization with examples
</summary>

Below are the various techniques used for sequential logic optimisations:<br />
-Basic
  - Sequential contant propagation
- Advanced
  - State optimisation
  - Retiming
  - Sequential Logic Cloning (Floor Plan Aware Synthesis)
 
#### Basic

**Sequential contant propagation**- Here only the first logic can be optimized as the output of flop is always zero. However for the second flop, the output changes continuously, therefor it cannot be used for contant propagation.

![IMG_1862](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/64d09728-6e85-49b9-a8c6-4fca7b650cb9)

#### Advanced
**State Optimisation**: This is optimisation of unused state. Using this technique we can come up with most optimised state machine.

**Cloning**: This is done when performing PHYSICAL AWARE SYNTHESIS. Lets consider a flop A which is connected to flop B and flop C through a combination logic. If B and C are placed far from A in the flooerplan, there is a routing path delay. To avoid this, we connect A to two intermediate flops and then from these flops the output is sent to B and C thereby decreasing the delay. This process is called cloning since we are generating two new flops with same functionality as A.

**Retiming**: Retiming is a powerful sequential optimization technique used to move registers across the combinational logic or to optimize the number of registers to improve performance via power-delay trade-off, without changing the input-output behavior of the circuit. 

**Example-1**<br />
Here flop will be inferred as the output is not constant. <br />

	module dff_const1(input clk, input reset, output reg q);
		always @(posedge clk, posedge reset)
		begin
			if(reset)
				q <= 1'b0;
			else
				q <= 1'b1;
		end
	endmodule

**Simulation**

![Screenshot from 2023-08-10 16-42-20](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/c6683476-a75f-4ffe-b30b-b7b906c468fa)

**Synthesis**<br />
In the synthesis report, we'll see that a Dflop was inferred in this example.

![Screenshot from 2023-08-10 17-00-46](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/ce467143-864e-41cf-b226-acc72f0e69b9)

![Screenshot from 2023-08-10 16-56-45](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/d8df7da0-ede8-4b49-9f40-38d06efbd448)


**Example-2**<br />
Here flop will not be inferred as the output is always high. <br />

	module dff_const2(input clk, input reset, output reg q);
		always @(posedge clk, posedge reset)
		begin
			if(reset)
				q <= 1'b1;
			else
				q <= 1'b1;
		end
	endmodule



**Simulation**

![Screenshot from 2023-08-10 16-43-58](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/0b3c3b54-ab1e-44ca-8b4a-d07320e7eb37)

**Synthesis**

![Screenshot from 2023-08-10 17-03-13](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/70da170d-b659-4d34-b0a0-a4db84a3f752)

![Screenshot from 2023-08-10 17-04-23](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/66d01bb4-e50a-49e6-acaf-a7cf6917cec1)

**Example-3**

		module dff_const3(input clk, input reset, output reg q);
		reg q1;

		always @(posedge clk, posedge reset)
		begin
			if(reset)
			begin
				q <= 1'b1;
				q1 <= 1'b0;
			end
			else
			begin
				q1 <= 1'b1;
				q <= q1;
			end
		end
		endmodule


**Simulation***

![Screenshot from 2023-08-10 16-44-45](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/ab33f9ff-b456-4358-8e1d-999d7cdfe025)

**Synthesis**

![Screenshot from 2023-08-10 17-05-10](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/79e72a0f-db7e-4edf-9695-81d66228061b)

![Screenshot from 2023-08-10 17-07-47](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/8dfff9cb-8107-4aa3-b892-c59072ee33db)

**Example4**

		module dff_const4(input clk, input reset, output reg q);
		reg q1;

		always @(posedge clk, posedge reset)
		begin
			if(reset)
			begin
				q <= 1'b1;
				q1 <= 1'b1;
			end
		else
			begin
				q1 <= 1'b1;
				q <= q1;
			end
		end
		endmodule

**Simulation***

![Screenshot from 2023-08-10 16-45-21](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/c5bedf32-0edf-4d3c-a1d3-968c60e39402)

**Synthesis**

![Screenshot from 2023-08-10 17-09-12](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/8647320e-058f-413c-b625-91bfc64378a2)

![Screenshot from 2023-08-10 17-09-41](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/ed25d6a2-e512-482b-9efc-44eb249e8d59)

**Example5**

		module dff_const5(input clk, input reset, output reg q);
		reg q1;
		always @(posedge clk, posedge reset)
			begin
				if(reset)
				begin
					q <= 1'b0;
					q1 <= 1'b0;
				end
			else
				begin
					q1 <= 1'b1;
					q <= q1;
				end
			end
		endmodule

**Simulation***

![Screenshot from 2023-08-10 16-45-53](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/05819ff1-766e-47ba-bcc4-b6db22d93455)

**Synthesis**

![Screenshot from 2023-08-10 17-10-21](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/2edf31b0-181b-4db2-b2e4-9861ec1d7cc3)

![Screenshot from 2023-08-10 17-11-05](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/41275734-79ad-4782-8a67-eb0527499a2a)
 
</details>

<details>
<summary> Sequential optimisation of unused outputs </summary>

**Example1**

		module counter_opt (input clk , input reset , output q);
		reg [2:0] count;
		assign q = count[0];
		always @(posedge clk ,posedge reset)
		begin
			if(reset)
				count <= 3'b000;
			else
				count <= count + 1;
		end
		endmodule

**Synthesis**

![Screenshot from 2023-08-10 17-22-33](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/bb78deec-c9a6-4abd-8ad8-193bf6ce2389)

![Screenshot from 2023-08-10 17-22-58](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/42617423-b018-455e-b059-f49d9e807a0f)

**Updated counter logic-** 

	module counter_opt (input clk , input reset , output q);
		reg [2:0] count;
		assign q = {count[2:0]==3'b100};
		always @(posedge clk ,posedge reset)
		begin
		if(reset)
			count <= 3'b000;
		else
			count <= count + 1;
		end
	endmodule

**Synthesis**

All the other blocks in synthesizer are for incrementing the counter but the output is only from the three input NOR gate.

![Screenshot from 2023-08-10 17-25-40](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/a4f9fb95-809c-41a9-b375-c6bc5d5e17a6)

![Screenshot from 2023-08-10 17-27-21](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/5e8879d9-ea18-4b8d-94ef-2984f9faf9a2)
 
</details>


## Day-4-GLS,blocking vs non-blocking and Synthesis-Simulation mismatch

<details> 
<summary>GLS, Synthesis-Simulation mismatch and Blocking, Non-blocking statements</summary>

### GLS Concepts And Flow Using Iverilog

**What is GLS- Gate Level Simulation?**:<br />
GLS is generating the simulation output by running test bench with netlist file generated from synthesis as design under test. Netlist is logically same as RTL code, therefore, same test bench can be used for it.

**Why GLS?**:<br />
We perform this to verify logical correctness of the design after synthesizing it. Also ensuring the timing of the design is met.

Below picture gives an insight of the procedure. Here while using iverilog, we also include gate level verilog models to generate GLS simulation.

![Screenshot (49)](https://user-images.githubusercontent.com/104454253/166256679-1ac9167a-1358-4c60-bbdb-0f6423f0faa3.png)

### Synthesis Simulation Mismatch

There are three main reasons for Synthesis Simulation Mismatch:<br />
- Missing sensitivity list in always block
- Blocking vs Non-Blocking Assignments
- Non standard Verilog coding

**Missing sensitivity list in always block:**<br />

If the consider - Example-2, we can see the only **sel** is mentioned in the sensitivity list. During the simulation, the waveforms will resemble a latched output but the simulation of netlist will not infer this as the synthesizer will only look at the statements with in the procedural block and not the sensitivity list.

As the synthesizer doen't look for sensitivity list and it looks only for the statements in procedural block, it infers correct  circuit  and if we simulate the netlist code, there will be a synthesis simulation mismatch.

To avoid the synthesis and simulation mismatch. It is very important to check the behaviour of the circuit first and then match it with the expected output seen in simulation and make sure there are no synthesis and simulation mismatches. This is why we use GLS.

**Blocking vs Non-Blocking Assignments**:

Blocking statements execute the statemetns in the order they are written inside the always block. Non-Blocking statements execute all the RHS and once always block is entered, the values are assigned to LHS. This will give mismatch as sometimes, improper use of blocking statements can create latches. Get to see at Example4

</details>

<details>
	<summary> Lab- GLS Synth Sim Mismatch </summary>

 **Example-1** There is no mismatch in this example as the netlist simulation and rtl simulation waveform are similar only

	module ternary_operator_mux (input i0 , input i1 , input sel , output y);
		assign y = sel?i1:i0;
	endmodule
	
**Simulation**

![Screenshot from 2023-08-12 05-18-39](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/35d1205f-9aa5-4043-ab08-f039e7af0ce1)

**Synthesis**

![Screenshot from 2023-08-12 05-21-59](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/7c678233-6303-483b-a9e1-d8e0135c87c3)

**Netlist Simulation**

![Screenshot from 2023-08-12 05-25-36](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/ae119fbc-ed04-460f-9d12-26da345c55e8)

# Example-2

	module bad_mux (input i0 , input i1 , input sel , output reg y);
		always @ (sel)
		begin
			if(sel)
				y <= i1;
			else 
				y <= i0;
		end
	endmodule

**Simulation**

![Screenshot from 2023-08-12 05-35-53](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/f1897682-f9e1-499a-99b8-95492ff3bea2)

**Synthesis**

![Screenshot from 2023-08-12 05-38-57](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/d83f1d1f-47a4-46a7-9e09-7f444a8cd2ed)

**Netlist Simulation**

![Screenshot from 2023-08-12 05-40-37](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/f42fee9c-21a4-46c4-a9ba-b5f57312e96d)

**MISMATCH**<br /> Here first pic shows the netlist simulation which corrects the bad_mux design which was only changing waveform when sel was triggered while for a mux to work properly it should be sensitivity to all the input signals


![WhatsApp Image 2023-08-12 at 5 52 52 AM](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/b1a4f8e2-3e59-4385-8943-058c7714b3da)

**Example-3**

	module good_mux (input i0 , input i1 , input sel , output reg y);
		always @ (*)
		begin
			if(sel)
				y <= i1;
			else 
				y <= i0;
		end
	endmodule
	
**Simulation**

![Screenshot from 2023-08-12 05-59-35](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/d3d005c0-f1a3-40f8-b9da-00b412dc6b21)

**Synthesis**

![Screenshot from 2023-08-12 06-00-45](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/8c6a6b9e-32e0-4b19-a2a2-1247a654937a)

**Netlist Simulation**

![Screenshot from 2023-08-12 06-02-20](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/c9f87f13-427c-4924-98f4-d2dbac8a14a4)

</details>

<details>
	<summary>Lab- Synthesis simulation mismatch blocking statement</summary>

 Here the output is depending on the past value of x which is dependednt on a and b and it appears like a flop.

# Example4

	module blocking_caveat (input a , input b , input  c, output reg d); 
	reg x;
	always @ (*)
		begin
		d = x & c;
		x = a | b;
	end
	endmodule

**Simulation**

![Screenshot from 2023-08-12 06-06-51](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/fd69fdfc-e59f-4842-88ed-13506db0f340)

**Synthesis**

![Screenshot from 2023-08-12 06-09-46](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/d349fd0a-f338-41fd-9505-9b001d82ce50)

**Netlist Simulation**

![Screenshot from 2023-08-12 06-11-09](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/cccf31dd-40e4-46bd-a15f-4abecb763ed9)

**MISMATCH** 

![WhatsApp Image 2023-08-12 at 6 23 55 AM](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/cc04e484-5040-4150-b204-a928642cb8ab)

Here this how the circuit should behave but this correct waveform is only obtained while doing netlist simulation.
Here first pic show the netlist simulation which shows the proper working of the dut while the last pic shows the improper working of dut as we have used blocking statement here which causes synthesis simulation mismatch which is sorted out by GLS while providing netlist simulation  

![WhatsApp Image 2023-08-12 at 6 18 55 AM](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/b22ac58b-7d1b-4e68-a587-ba03f256264d)

</details>

## Day-5- if, case, for loop and for generate

<details>
<summary> If and Case constructs </summary>
	
 ### 6.1.1 If construct
 
The construct **if** is mainly used to create priority logic. In a nested if else construct, the conditions are given priority from top to bottom. Only if the condition is satisfied, if statement is executed and the compiler comes out of the block. If condition fails, it checks for next condition and so on as shown below.

**Syntax for nested if else**

	if (<condition 1>)
	begin
	-----------
	-----------
	end
	else if (<condition 2>)
	begin
	-----------
	-----------
	end
	else if (<condition 3>)
	.
	.
	.
	
**Dangers with IF**:

If use a bad coding style i.e, using incomplete if else constructs will infer a latch. We definetly don't require an unwanted latch in a combinational circuit.
When an incomplete construct is used, if all the conditions are failed, the input is latched to the output and hence we don't get desired output unless we need a latch.

This can be shown in below example:

![WhatsApp Image 2023-08-12 at 4 18 43 PM](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/945687cf-2a00-4838-98df-94e52ff0d303)

### Case construct

**Syntax**

	case(statement)
	  case1: begin
  	       --------
		 --------
		 end
 	 case2: begin
    	     --------
		 --------
		 end
 	 default:
	 endcase
 
 In case construct, the execution checks for all the case statements and whichever satisfies the statement, that particular statement is executed.If there is no match, the default statement is executed. But here unlike if construct, the execution doesn't stop once statement is satisfied, but it continues further.
 
**Caveats in Case**<br />
Caveats in case occur due to two reasons. One is **incomplete case statements** and the other is **partial assignments in case statements.**

</details>

<details>
<summary> Lab- Incomplete IF </summary>

This incomplete if construct forms a connection between i0 and output y i.e, D-latch with input as i1 and i0 will be the enable for it.<br />
**Example-1**

	module incomp_if (input i0 , input i1 , input i2 , output reg y);
	always @ (*)
	begin
		if(i0)
			y <= i1;
	end
	endmodule

**Simulation**

![Screenshot from 2023-08-12 16-30-30](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/8283800a-196d-46fd-9d07-8688a16621b4)

**Synthesis**

![Screenshot from 2023-08-12 16-33-34](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/09ecc29f-143c-4077-b289-0dafb52394eb)

**Example-2**<br />
The below code is equivalent to two 2:1 mux with i0 and i2 as select lines with i1 and i3 as inputs respectively. Here as well, the output is connected back to input in the form of a latch with an enable input of **OR** of i0 and i2.

	module incomp_if2 (input i0 , input i1 , input i2 , input i3, output reg y);
		always @ (*)
		begin
			if(i0)
				y <= i1;
			else if (i2)
				y <= i3;
		end
	endmodule

**Simulation**

![Screenshot from 2023-08-12 16-35-18](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/e0bc98aa-09c5-4a9b-9cea-dbe350024759)

**Synthesis**

![Screenshot from 2023-08-12 16-36-57](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/c21e5477-7a74-43f1-9d94-bc2e123a3cc2)
 
</details>

<details>
<summary> Lab- incomplete overlapping Case </summary>

**Example-1**<br />
Thie is an example of incomplete case where other two combinations 10 and 11 were not included. This is infer a latch for the multiplexer and connect i2 and i3 with the output.

	module incomp_case (input i0 , input i1 , input i2 , input [1:0] sel, output reg y);
		always @ (*)
		begin
		case(sel)
			2'b00 : y = i0;
			2'b01 : y = i1;
		endcase
		end
	endmodule

**Simulator**

![Screenshot from 2023-08-12 16-44-24](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/64b64b5f-bf32-4379-8c4a-28d69ae74344)

**Synthesis**


![Screenshot from 2023-08-12 16-45-30](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/504fd175-6a30-4366-86b3-b07c234eb516)

**Example-2- Complete case**

This is the case of complete case statements as the default case is given. If the actual case statements don't execute, the compiler directly executes the default statements and a latch is not inferred.

	module comp_case (input i0 , input i1 , input i2 , input [1:0] sel, output reg y);
	always @ (*)
	begin
		case(sel)
			2'b00 : y = i0;
			2'b01 : y = i1;
			default : y = i2;
		endcase
	end
	endmodule

**Simulation**

![Screenshot from 2023-08-12 16-47-12](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/e3164978-62a6-43ab-86c7-aaeaaa716d93)

**Synthesis**

![Screenshot from 2023-08-12 16-47-58](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/52223f30-f7a4-4307-a625-dcad2fcb6a6d)

**Example-3**<br />
In the below example, y is present in all the case statements and it had particular outut for all cases. There no latch is inferred in case of y. 
When it comes to x, it is not assigned for the input 01, therefore a latch is inferred here.

	module partial_case_assign (input i0 , input i1 , input i2 , input [1:0] sel, output reg y , output reg x);
	always @ (*)
	begin
		case(sel)
			2'b00 : begin
				y = i0;
				x = i2;
				end
			2'b01 : y = i1;
			default : begin
		         	  x = i1;
				  y = i2;
			 	 end
		endcase
	end
	endmodule

**Simulation**

![Screenshot from 2023-08-12 16-55-55](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/41a6f161-8f5f-4b0b-bce9-adacba988ec0)

**Synthesis**

![Screenshot from 2023-08-12 16-57-27](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/595640ca-928e-490d-a637-2b310ea47f78)

**Example-4-Bad case construct**

	module bad_case (input i0 , input i1, input i2, input i3 , input [1:0] sel, output reg y);
	always @(*)
	begin
		case(sel)
			2'b00: y = i0;
			2'b01: y = i1;
			2'b10: y = i2;
			2'b1?: y = i3;
			//2'b11: y = i3;
		endcase
	end
	endmodule
	
**Simulation**

![Screenshot from 2023-08-12 16-59-05](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/c64019ae-6937-498d-a48f-3530edcc4d46)

**Synthesis**

![Screenshot from 2023-08-12 17-00-09](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/17d30970-521c-4d9b-8ef4-26efc593c85b)

**Netlist simulation** As we can see from the simulation wave form and difference in netlist waveform here the invalid case is getting fixed by the tool which we should avoid to do so in the code

![Screenshot from 2023-08-12 17-04-44](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/3783ebe3-a673-427f-bc72-152d6f992a49)
 
</details>

<details>
<summary> For Loop and For Generate </summary>

**For Loop**<br />
- For look is used in always block
- It is used for excecuting expressions alone

**Generate For loop**<br />
- Generate for loop is used for instantaing hardware
- It should be used only outside always block

For loop can be used to generate larger circuits like 256:1 multiplexer or 1-256 demultiplexer where the coding style of smaller mux is not feesible and can have human errors since we would need to include huge number of combinations.

FOR Generate can be used to instantiate any number of sub modules with in a top module. For example, if we need a 32 bit ripple carry adder, instead of instantiating 32 full adders, we can write a generate for loop and connect the full adders appropriately.

 
</details>

<details>
<summary> Lab- For and For Generate </summary>

**Example-1- Mux using generate**<br />
Here for loop is used to design a 4:1 mux. This can also be written using case or if else block, however, for a large size mux, only for loop model is feasible.

	module mux_generate (input i0 , input i1, input i2 , input i3 , input [1:0] sel  , output reg y);
		wire [3:0] i_int;
		assign i_int = {i3,i2,i1,i0};
		integer k;
	always @ (*)
		begin
		for(k = 0; k < 4; k=k+1) begin
			if(k == sel)
			y = i_int[k];
			end
		end
	endmodule

**Simulation**

![Screenshot from 2023-08-12 17-15-00](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/509d585f-0142-463b-9e9f-dee440a8fcf2)

**Synthesis**

![Screenshot from 2023-08-12 18-09-27](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/9ac06b1f-bcdd-4e8f-b7bc-309dc0480d39)

**Netlist Simulation**

![Screenshot from 2023-08-12 18-10-29](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/e9c86d8b-63ab-4ec8-8155-101c88c7a4d4)

**Example-2-Demux using Case**

	module demux_case (output o0 , output o1, output o2 , output o3, output o4, output o5, output o6 , output o7 , input [2:0] sel  , input i);
	reg [7:0]y_int;
	assign {o7,o6,o5,o4,o3,o2,o1,o0} = y_int;
	integer k;
	always @ (*)
	begin
	y_int = 8'b0;
	case(sel)
		3'b000 : y_int[0] = i;
		3'b001 : y_int[1] = i;
		3'b010 : y_int[2] = i;
		3'b011 : y_int[3] = i;
		3'b100 : y_int[4] = i;
		3'b101 : y_int[5] = i;
		3'b110 : y_int[6] = i;
		3'b111 : y_int[7] = i;
	endcase
	end
	endmodule

**Simulation**

![Screenshot from 2023-08-12 17-22-38](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/ed70a9cf-918d-4c57-a508-c199514a2358)

**Synthesis**

![Screenshot from 2023-08-12 18-05-19](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/b8206f75-d0d2-4c77-8cce-e423bbc23c32)

**Netlist Simulation**

![Screenshot from 2023-08-12 18-06-09](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/51d79542-5b6c-4392-99aa-a9ff6c1b01f3)

**Example-3-Demux using Generate**

The code in above example is big and also there is a chance of human error wile writing the code. However, using for loop as shown below, this drawback can be elimiated to a great extent.

	module demux_generate (output o0 , output o1, output o2 , output o3, output o4, output o5, output o6 , output o7 , input [2:0] sel  , input i);
	reg [7:0]y_int;
	assign {o7,o6,o5,o4,o3,o2,o1,o0} = y_int;
	integer k;
	always @ (*)
	begin
		y_int = 8'b0;
		for(k = 0; k < 8; k++) begin
			if(k == sel)
			y_int[k] = i;
		end
	end
	endmodule

**Simulation**

![Screenshot from 2023-08-12 17-33-59](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/608e3311-b492-4d0d-b7af-b87515da69ae)

**Synthesis**

![Screenshot from 2023-08-12 18-01-51](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/50f970dc-2366-496d-bd97-32b27f0b6ff5)

**Netlist Simulation**

![Screenshot from 2023-08-12 18-03-44](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/43d9a809-3d62-4564-8582-4fca22d6ee94)

**Example-4- Ripple carry adder using fulladder**

In this Ripple carry adder example, unlike instantiating fulladder for 8 times, generate for loop is used to instantiate the fulladder for 7 times and only for first full adder, it is instantiated seperately. Using the same code, just by changing bus sizes and condition of for loop, we can design any required size of ripple carry adder.

	module rca (input [7:0] num1 , input [7:0] num2 , output [8:0] sum);
	wire [7:0] int_sum;
	wire [7:0]int_co;

	genvar i;
	generate
		for (i = 1 ; i < 8; i=i+1) begin
			fa u_fa_1 (.a(num1[i]),.b(num2[i]),.c(int_co[i-1]),.co(int_co[i]),.sum(int_sum[i]));
		end

	endgenerate
	fa u_fa_0 (.a(num1[0]),.b(num2[0]),.c(1'b0),.co(int_co[0]),.sum(int_sum[0]));


	assign sum[7:0] = int_sum;
	assign sum[8] = int_co[7];
	endmodule

	module fa (input a , input b , input c, output co , output sum);
 	assign {co,sum} =a+b+c;
	endmodule

**Simulation**

![Screenshot from 2023-08-12 17-42-53](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/ee7872b7-3fe7-4cd6-a6fd-1b2c27da8ee4)

**Synthesis**

![Screenshot from 2023-08-12 17-56-54](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/5ca69c7a-f6b4-4243-9675-5a858bbae07c)

![Screenshot from 2023-08-12 17-57-15](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/d64d3189-252b-4e34-b5ab-5f8b04573fbb)

**Netlist Simulation**

![Screenshot from 2023-08-12 17-58-45](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/00ea0d62-bf07-491b-832c-8b7e14f52f03)
 
</details>

# Day 6-Introduction to RISC-V ISA And GNU compiler toolchain 

<details>
  <summary>Introduction to RISC-V ISA </summary>

  RISC-V ISA is a base integer ISA and must be present in any implemenatation along with some optional extension. The RISC-V has been designed to support extensive customization and specialization which can be extended  with  one  or  more  optional  instruction-set  extensions,  but  the  base  integer instructions cannot be redefine. The different instructions included in RISC-V are listed below.

1. Pseudo instructions - For e.g- mv,li,ret etc
2. Base integer instruction (RV64I, RV32I)-For e.g-lui,addi etc
3. Multiply extension (RV64M) -For e.g- mulw,divw etc
4. Single and double floating point instruction (RV64F, RV64D) -For e.g- flw,fadd etc
5. Application binary instruction 
6. Memory allocation and stack pointer

The detail of the RISC-V instructions set manual can be found [here](https://riscv.org/wp-content/uploads/2017/05/riscv-spec-v2.2.pdf).

Each base integer set is characterized by the  width  of the register (XLEN) and size of the user address space. The most important advantage of RISC-V is that it is an open standard instruction which is easily available for academics and commercial purposes free of cost.

</details>

<details>
  <summary>GNU compile toolchain</summary>

  The GNU compile toolchain is a set of programming tools in LINUX system that can be use for compiling a code to generate certain executable program, library and debugger and whose detail can be found in references. RISC-V is one such toolchain which supports C and C++ cross compiler. It supports two build modes: a generic ELF/Newlib toolchain and a more sophisticated Linux-ELF/glibc toolchain and the github link for the same can be found in references. 

1. Compiler and linker which transform the source code into an executable program
2. Libraries which provide interfaces to the operating system 
3. Debugger which is used to test and debug created program

To start off a c program to compile sum from 1 to n was written whose  codes given below as [sum1to6.c]

```

#include <stdio.h>

int main () {
	int i,sum = 0, n = 6;
	for (i = 1; i <=n; ++i) {
		sum += i;
	}
	printf("The sum of the number from 1 to %d is %d\n", n,sum);
	return 0;
	}

```

In case RISC-V GNU toolchain the follwing commands are executed

- To use the RISC-V gcc compiler or simulator, type
  
```
riscv64-unknown-elf-gcc  -o <object filename.o> <filename.c>

```
Here -01 gives 15 instructions set while -0fast gives us 12 instructions set(ubuntu) here in macos we get 15 instructions

More generic command with different options:

    `riscv64-unknown-elf-gcc <compiler option -O1 ; Ofast> <ABI specifier -lp64; -lp32; -ilp32> <architecture specifier -RV64 ; RV32> -o <object filename> <C      filename>`
    
-  To list the details of a file
  
  ```
ls -ltr <filename.o>

```

<img width="682" alt="Screenshot 2023-08-18 at 11 33 19 PM" src="https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/c768b542-363a-4a6f-87b0-754f5d9a3484">

- To deassemble the object file 

```

riscv64-unknown-elf-objdump <object file> -d <object filename.o>

```

- Below image shows the disassembled file `sum1to6.o` with `main` function highlighted.


```

riscv64-unknown-elf-objdump <object file> -d <object filename.o> | less

```

<img width="682" alt="Screenshot 2023-08-18 at 11 33 45 PM" src="https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/27322cef-c5db-4cbe-942f-4889623380cd">

```
/main
n

```
This code helps in seeing the main file:

<img width="1440" alt="Screenshot 2023-08-18 at 11 34 06 PM" src="https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/0ddce653-dfe2-4331-a82d-8b4ec1fc1d1f">

here we can check the instruction set is 15 by subtracting  10214-101ac = 58\4=15 instruction sets 

After running the above code line a number of things can be done as demonstrated in the image below. The code can be manually debugged, part of it can be run and contents of registers can be checked.

```:q``` to quit. 





  </details>

## Word of Thanks
I sciencerly thank **Mr. Kunal Gosh**(Founder/**VSD**) for helping me out to complete this flow smoothly.

## Acknowledgement
- Kunal Ghosh, VSD Corp. Pvt. Ltd.
- Skywater Foundry
- Chatgpt
- Kanish R,Colleague,IIIT B
- Sumanto Kar,VSD Corp.
- Pruthvi Parate,Colleague,IIIT B
- Bhargav D V ,Colleague,IIIT B
- Emil Jayanth Lal,Colleague,IIIT B
- DantuNandini,Senior,IIIT B
- Mariam Rakka
- Nanditha Rao, Professor, IIITB 
- Madhav Rao, Professor, IIITB
- Manikandan,Professor,IIITB
  
## Reference 

- https://github.com/YosysHQ/yosys.git
- https://github.com/The-OpenROAD-Project/OpenSTA.git
- https://github.com/kunalg123
- https://www.vsdiat.com
- https://github.com/mariamrakka
- https://github.com/dantunandinidevi
- https://en.wikipedia.org/wiki/Toolchain
- https://en.wikipedia.org/wiki/GNU_toolchain
- https://github.com/riscv/riscv-gnu-toolchain
- https://github.com/KanishR1
