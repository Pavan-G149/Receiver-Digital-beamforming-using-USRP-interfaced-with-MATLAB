# Solution to MATLAB and Simulink Challenge project <162> <Receiver Digital beamforming  using USRP interfaced with MATLAB>
This is a template repo for MATLAB and Simulink Challenge Project solutions.


[Program link](https://github.com/mathworks/MATLAB-Simulink-Challenge-Project-Hub)

[Project description link](https://github.com/mathworks/MATLAB-Simulink-Challenge-Project-Hub/tree/e86687edb8cdb038e7cf15bc09f95bea313c82c1/projects/Build%20a%20wireless%20communications%20link%20with%20software%20defined%20radio)

# Receiver Digital beamforming  using USRP interfaced with MATLAB

This project was chosen to delve into the practical implementation of MIMO technology, a fundamental aspect of modern wireless communication. By using USRPs and Simulink, it provided hands-on experience with state-of-the-art tools and hardware synchronization techniques. The focus on signal reception with varying transmitter positions allowed us to analyze spatial characteristics and optimize receiver performance. This work bridges the gap between theoretical understanding and real-world applications of advanced communication systems. Additionally, it aligns with emerging research trends in improving network reliability and efficiency in diverse scenarios.

# Project details

![Block Diagram](MIMO.png "Block Diagram of MIMO configuration")
**Signal Transmission and Reception**

The transmitter setup consists of a signal generator producing a sine wave at 2.3 GHz with a power level of 15 dBm. This signal is fed into a log-periodic antenna, which is a directional, ultra-wideband antenna capable of operating over a frequency range of 800 MHz to 6.5 GHz. To ensure optimal signal reception, both the transmitter antenna and the receiver array, which also employ directional antennas, must be carefully aligned. Proper alignment is crucial to maximize the received power and minimize signal loss, taking full advantage of the antennas' directional characteristics for efficient communication.

The receiver side of this MIMO (Multiple Input, Multiple Output) system utilizes two USRP N210 devices synchronized with an OctoClock to achieve precise timing and frequency alignment. This setup captures incoming electromagnetic waves at the antennas of the two receivers, processes the signal to compensate for path delay differences, and enhances the signal-to-noise ratio (SNR) of the received signals. The signal processing is performed in MATLAB/Simulink, leveraging blocks such as trigonometric and constant blocks for phase correction and SNR optimization. This system provides an efficient testbed for studying MIMO communication in real-world scenarios.

**Components and Their Roles**

**1. OctoClock**

The OctoClock is a clock distribution module that provides:
- 10 MHz Clock Reference: Ensures that the oscillators of both USRP N210 devices operate in perfect frequency alignment. This synchronization is critical for coherent signal processing in MIMO.
- Pulse-Per-Second (PPS) Signal: Delivers precise time synchronization to the USRPs, aligning their sampling instants to the same time base. This is essential for applications requiring temporal coherence, such as MIMO beamforming.

**2. USRP N210**

The USRP N210 devices function as the hardware receivers in the system. Key roles include:
- Signal Reception: Each USRP receives an electromagnetic wave at its respective antenna. Due to the spatial separation between the antennas, the incoming wave reaches each antenna with a time delay caused by the difference in path lengths.
- Digitization: The received analog signals are converted into digital samples for further processing.

**3. Ethernet Switch**

The Ethernet switch establishes a high-speed communication link between the USRPs and the Host PC. It handles packetized data transfer, ensuring minimal latency and reliable data flow.

**4. Host PC**

The Host PC performs the critical signal processing tasks:
- Delay Compensation: The time delay caused by the path difference is compensated in MATLAB/Simulink. The delay introduces a phase shift in the received signals, which is corrected by multiplying the signals with a calculated phase term.
- Signal Combination: Once the phase shifts are corrected, the signals from both antennas are added coherently. This constructive combination improves the SNR of the received signal, leveraging the spatial diversity provided by the MIMO setup.
- Simulink Implementation: The phase correction and signal combination are implemented using Simulink blocks:

**5. Phase Difference Calculation**

The phase difference Δϕ\Delta\phiΔϕ is computed based on the delay caused by the path difference. Here's the step-by-step process:

1.	Path Delay (Δt): The time delay between the two antennas is proportional to the spatial path difference:
Δt=Δd\c

where:

o	Δd is the path difference (distance difference between antennas and the incoming wavefront),

o	c is the speed of light.

2.	Phase Difference (Δϕ): Using the relation between time delay and phase for a sinusoidal signal:
Δϕ=2πfcΔt

where:

o	fc is the carrier frequency of the signal.

o	Δt is the time delay (calculated above).

Substituting Δt:

Δϕ=2πfcΔd\c

Here Δd=dsin(θ)where θ is the angle as shown in the image 

![Path delay](Pathdelay.png)

# How to run section
**Required Toolboxes:**
1) communication toolbox
2) DSP system toolbox
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
2) Data type Conversion ( 16 bit data is recived from receiverblock we need to convert the data type to process in simulink )
3) Constant block ( to give the phase of π*sin(θ *180/π) to one of the received signal)
4) Trigonometric block ( use cos + jsin ) 
5) Product block ( to introduce the phase shift to received signal)
6) Add block ( To add the received signals one is phase shifted signal)
7) Scope ( to check the received signal and Added signal after phase delay)
8) Spectrum Analyzer ( to check the power of the signal)

**SDRu Receiver block parameters**
![SDRu Receiver Block](SDRu_Receiver_Block.png "SDRu Receiver block parameters")

- Platform: N200/N210/USRP2 ( we are using N21o USRP)
- IP Address: Select the IP address of the USRP
- Channel mapping: We are using USRP for receiving the signal only, so choose 1.
- Center Frequency: Give the transmitting signal frequency. We are transmitting 2.3 GHz signal with amplitude of 15dBm.
- LO offset: Use the deafult value 0.
- Gain: Addjust the gain of the received signal by comparing the both received signal strengths at 0 degree phase shift.
- PPS Source: We are using Octo clock for PPS generation, so select External.
- Clock Source: We are using Octo clock for 10 MHz clock Generation, so select External.
- Decimation factor: Choose the values 4 to 512 which are multiples of 4. This factor crucial for sampling frequency addjust it for based on requirements.
- Transport data type: Use Default int16.
- Output data type: Same as the Transport data type.
- Sample per frame: Depends on host computer running capabalities, for this project we used 1 sample per frame.
- Give the Simulation time and run the simulink model, we gave 1 sec simulation time.
# Demo
Here you can find the detail explanation of this project and simulation --> [Receiver-Digital-beamforming-using-USRP-interfaced-with-MATLAB
](https://drive.google.com/file/d/1MBm7_SqjuEqHJ_ImjQLpN-ywFEBipmkL/view)
# Simulation results
**1) Phase shift θ= 0 degree**
- USRP1 Received power= 93.37 dBm
- USRP2 Received power= 94.13 dBm
- Combined Power= 99.29 dBm

![Phase shift 0](phase0.png "Phase shift θ= 0 degree")
**2) Phase shift θ= 10 degree**
- USRP1 Received power= 91.66 dBm
- USRP2 Received power= 90.67 dBm
- Combined Power= 92.95 dBm

![Phase shift 10](phase10.png "Phase shift θ= 10 degree")
**3) Phase shift θ= 15 degree**
- USRP1 Received power= 78.26 dBm
- USRP2 Received power= 80.88 dBm
- Combined Power= 85.16 dBm

![Phase shift 15](phase15.png "Phase shift θ= 15 degree")
**4) Phase shift θ= 20 degree**
- USRP1 Received power= 71.88 dBm
- USRP2 Received power= 79.89 dBm
- Combined Power= 82.45 dBm

![Phase shift 20](phase20.png "Phase shift θ= 20 degree")

The simulation results demonstrate that beamforming effectively enhanced the Signal-to-Noise Ratio (SNR) by coherently combining phase-aligned signals from two antennas, confirming the practical viability of this method. Properly adjusting the phase shift between signals from different antennas proved essential for maximizing received power. Additionally, varying the transmitter's position from 0° to 20° relative to the receiver array showed a reduction in received signal strength, emphasizing the critical role of precise antenna alignment and beamforming in achieving optimal signal reception.

# Conclusion
The project successfully demonstrated the practical implementation of MIMO configuration for enhanced signal reception using a synchronized USRP-based receiver setup. The use of two antennas placed at a λ/2 distance, combined with external clock synchronization via an Octo Clock, ensured accurate signal acquisition and phase alignment. By introducing phase delay to account for path differences and combining the signals, an improvement in SNR was observed, validating the effectiveness of the approach. The analysis of received power variations with changing transmitter positions provided valuable insights into spatial signal dynamics. This work highlights the potential of MIMO systems for advanced communication networks.
# Reference
- [Build Your Own Phased Array Beamformer](https://www.youtube.com/watch?v=2QXKuEYR4Bw)
