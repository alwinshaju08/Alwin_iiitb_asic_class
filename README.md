# Alwin_iiitb_asic_class
This github repository summarizes the progress made in the ASIC class. Quick links:

[Day-0-Installation](#day-0-Installation)

[Day-1-Introduction to Verilog RTL design and Synthesis](#Day-1--Introduction-to-Verilog-RTL-design-and-Synthesis)

[Day-2-Timing libs,hierarchical,flat synthesis,efficient flop coding styles](#Day-2-Timing-libs-hierarchical-flat-synthesis-efficient-flop-coding-styles)

[Day-3-Combinational and sequential optmizations](#day-3-Combinational-and-sequential-optmizations)

[Day-4-GLS, blocking vs non-blocking and Synthesis-Simulation mismatch](#5-DAY4--GLS-blocking-vs-non-blocking-and-Synthesis-Simulation-mismatch)]


[Acknowledgement](#acknowledgement)

[Reference](#reference)

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

 **Example- 5**

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

![Screenshot from 2023-08-10 16-33-21](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/f9e8f641-8927-4a5c-90be-eb8cc740d5df)

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


![Screenshot from 2023-08-10 16-34-39](https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/7f74441f-9d3f-44c1-8946-dcf51018ba87)

 
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
 
#### 4.2.1 Basic

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


## Day-4-GLS, blocking vs non-blocking and Synthesis-Simulation mismatch
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

## Acknowledgement
- Kunal Ghosh, VSD Corp. Pvt. Ltd.
- Skywater Foundry
- Chatgtp
- Kanish R,Colleague,IIIT B
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
