# Alwin_iiitb_asic_class
This github repository summarizes the progress made in the ASIC class. Quick links:

[Day 0](#day-0)

## Day 0
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

<img width="1048" alt="yosys" src="https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/f14cb7e5-a5ec-4b89-93c5-823df2f8dd9e">
</details>

<details>  
<summary> Iverilog </summary>
    
I installed iverilog using the following command:

```
sudo apt-get install iverilog
```

Below is the screenshot showing sucessful launch:

<img width="1048" alt="iverilog" src="https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/768ba79b-701b-4ec7-ba28-9b0aa8d4e851">

</details>

<details>  
    
<summary> Gtkwave </summary>

I installed iverilog using the following command:

```
sudo apt-get install gtkwave
```

Below is the screenshot showing sucessful launch:

<img width="1048" alt="gtkwave" src="https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/a554ecec-7b1c-472a-83c1-ccc20e9a35d5">

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

<img width="1048" alt="ngspice" src="https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/ea53d1d2-ba18-474a-ae73-d8d2e1a1512f">

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

<img width="1064" alt="magic" src="https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/253d3715-ff47-4b27-8621-fc0052cbe245">

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

<img width="1085" alt="sta" src="https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/a5ec621c-62da-46ad-b207-67c65290e03e">

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

<img width="1085" alt="openlane" src="https://github.com/alwinshaju08/Alwin_iiitb_asic_class/assets/69166205/5f6964c6-7021-4660-98ac-cd274dae696e">

</details>
