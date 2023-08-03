# Alwin_iiitb_asic_class
This github repository summarizes the progress made in the ASIC class. Quick links:

[Day 1](#day-1)

## Day 1
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
