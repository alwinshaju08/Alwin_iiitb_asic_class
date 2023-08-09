# Alwin_iiitb_asic_class
This github repository summarizes the progress made in the ASIC class. Quick links:

[Day-0](#day-0)

[Day-1-Introduction to Verilog RTL design and Synthesis](#Day-1--Introduction-to-Verilog-RTL-design-and-Synthesis)

[Day-2-Timing libs,hierarchical,flat synthesis,efficient flop coding styles](#Day-2-Timing-libs-hierarchical-flat-synthesis-efficient-flop-coding-styles)

[Day-3](#day-3)

[Acknowledgement](#acknowledgement)

[Reference](#reference)

## Day-0
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

![telegram-cloud-photo-size-5-6314223892675276833-y](https://user-images.githubusercontent.com/110079648/183962587-1dde8169-5e72-43b6-920b-f488ee000e44.jpg)

However, the yosys synthesizer generates the following schematic instead of the above one and with in the submodules, the connections are made

```
$ yosys
yosys> read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
yosys> read_verilog multiple_modules.v
yosys> synth -top multiple_modules
yosys> show multiple_modules 

```
image-- 

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
	
**Why Flops and Flop coding styles part1**

In this session, the discussion was about how to code various types of flops and various styles of coding a flop.

**Why a Flop?**

 In a combinational circuit, the output changes after the propagation delay of the circuit once inputs are changed. During the propagation of data, if there are different paths with different propagation delays, there might be a chance of getting a glitch at the output.<br />
 If there are multiple combinational circuits in the design, the occurances of glitches are more thereby making the output unstable.<br />
To curb this drawback, we are going for flops to store the data from the cominational circuits. When a flop is used, the output of combinational circuit is stored in     it and it is propagated only at the posedge or negedge of the clock so that the next combinational circuit gets a glitch free input thereby stabilising the output.
 
 We use initialize signals or control pins called **set** and **reset** on a flop to initialize the flop, other wise a garbage value to sent out to the next combinational circuit. These control pins can be synchronous or asynchronous.

### Lab- flop synthesis simulations

**d-flipflop with asynchronous reset**- Here the output **q** goes low whenever reset is high and will not wait for the clock's posedge, i.e irrespective of clock, the output is changed to low.



 
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
