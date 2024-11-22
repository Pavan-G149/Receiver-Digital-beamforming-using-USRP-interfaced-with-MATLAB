# Solution to MATLAB and Simulink Challenge project <162> <Receiver Digital beamforming  using USRP interfaced with MATLAB>
This is a template repo for MATLAB and Simulink Challenge Project solutions.

Please add the following items:

[Program link](https://github.com/mathworks/MATLAB-Simulink-Challenge-Project-Hub)

[Project description link](https://github.com/mathworks/MATLAB-Simulink-Challenge-Project-Hub/tree/e86687edb8cdb038e7cf15bc09f95bea313c82c1/projects/Build%20a%20wireless%20communications%20link%20with%20software%20defined%20radio)

# Receiver Digital beamforming  using USRP interfaced with MATLAB
This project was chosen to delve into the practical implementation of MIMO technology, a fundamental aspect of modern wireless communication. By using USRPs and Simulink, it provided hands-on experience with state-of-the-art tools and hardware synchronization techniques. The focus on signal reception with varying transmitter positions allowed us to analyze spatial characteristics and optimize receiver performance. This work bridges the gap between theoretical understanding and real-world applications of advanced communication systems. Additionally, it aligns with emerging research trends in improving network reliability and efficiency in diverse scenarios.

# Project details
A description of the implementation and the approached adopted.
![Block Diagram](MIMO.png "Block Diagram of MIMO configuration")

# How to run section
**Required Toolboxes:**
1) communication toolbox
2) DSP toolbox
3) Signal Processing Toolbox
4) Communications Toolbox Support Package for USRP Radio

**Initial Setup**
1) Connect the USRP's in MIMO configuration  as shown in Block Diagram.
2) Configure the USRP's in Matlab
    Matlab --> Add-Ons --> Manage Add-Ons --> Communications Toolbox Support Package for USRP Radio click setup (click the settings it will show Setup) --> select Select Ethernet based radio ( we are using N210 USRP) --> select the check box to manually configure the computer network interface --> if status is avaliable click next --> Test the radio connection ( connected USRP IP Addresses will be shown) then finish the setup.

**Simulink Model**
![Simulink Model](Simulink_Model_Block_diagram.png "Simulink Model Block diagram")

**Blocks used:**
1) SDRu Receiver  <-- Communications Toolbox Support Package for USRP Radio
2) Data type Conversion
3) Constant block ( to give the phase of U+03C0 *sin(theta)
4) Trigonometric block ( use cos + jsin )
5) Product block
6) Add block
7) Scope ( to check the received signal and Added signal after phase delay)
# Demo
Add a video or animated gif/picture to showcase the code in operation.
  
# Reference
Add reference papers, data, or supporting material that has been used, if any.
