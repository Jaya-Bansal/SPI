# Serial-Peripheral-Interface
## Objective
1. To understand the SPI communication protocol and its advantages like less latency and more throughput over UART and I2C.
2. To implement the logic using Verilog and therefore, establish the SPI communication between 2 FPGA boards.
3. To do waveform analysis and verify the feasibility of the state machine that we have designed.
4. To verify the full-duplex communication i.e. correct data is transmitted and received.

## Block Diagram in the top-level
<img width="724" src="https://user-images.githubusercontent.com/103300115/236622123-04aad6eb-5cec-4baa-a7f4-7da2b9228e0d.png">

## Details about the sub-blocks
<ol>
  <li> <b>Master Block:</b>
<ul>
  <li>This is the device that initiates the process of communication and controls the data transfer.
  <li>The master device generates the clock signal and selects the slave device with which it wants to communicate.
  <li>It typically consists of shift registers for receiving and transmitting data, a clock generator, and a control logic.
</ul>
  <li> <b>Slave Block:</b>
<ul>
<li>This is a device that receives and responds to commands initiated by the master device. 
<li>It listens for the chip select signal from the master and responds with the appropriate data. 
<li>It typically consists of a shift register and control logic for decoding the control signals from the SPI master. The shift register is used to hold the data that is being transmitted or received, while the control logic is responsible for generating the appropriate control signals for the chip select line and the MISO (Master-In-Slave-Out) and MOSI (Master-Out-Slave-In) lines.
<li>This device needs to be synchronized with the master clock signal.
  </ul>
  <li> <b>Wires:</b>
<ul>
  <li> <b> SCLK ( Serial Clock ):</b> Used to synchronize the data transfer between the master and slave devices.
  <li> <b> CS ( Chip select ):</b> Used to select the slave device with which the master wants to communicate.
  <li> <b> MOSI ( Master-out, Slave-in ):</b> Used to transmit data from the master to the slave device.
  <li> <b> MISO ( Master-in, Slave-out ):</b> Used to transmit data from the slave to the master device.
  </ul>
  <li> <b>Shift registers:</b>
<ul>
  <li> These are storage elements that would be storing the received data or the data to be transmitted.
  <li> We would be implementing the 8-bit registers.
  <li> The registers would be working according to the FIFO rule i.e. the bit that was stored first would be transmitted first.
  </ul>
  </ol>

## Detailed steps of Project implementation
<ol>
  <li><b>Ideation and Brainstorming:</b>
    <ul>
   <li> Our team began the project by conducting ideation and brainstorming sessions to gain a better understanding of the fundamentals of the SPI protocol, as well as its advantages over other communication protocols.
 <li>Once we had a clear understanding of the requirements, we proceeded to create a top-level design for our implementation, which included a block diagram to outline the various components and their interactions.
<li>To ensure proper functionality, we then designed a finite state machine to govern the behaviour of our implementation. 
<li>This helped to ensure that the various components of our implementation worked together in a coordinated and efficient manner. 
<li>Overall, this approach helped us to develop a clear roadmap for our project and ensured that we remained focused on the key requirements throughout the implementation process.
    </ul>
  <li><b>Implementation</b>
    <ul>
      <li>During the ideation stage, we developed a comprehensive block diagram and FSM to serve as a roadmap for the logic programming process. 
      <li>Our first step was to design the master module in compliance with all required specifications.
      <li>We then created a slave module with an identical FSM, but with miso and mosi functionalities reversed to facilitate communication.
      <li>To enable full duplex communication, we designed a top module that seamlessly connected the master and slave modules.
      <li>As we were implementing the 4-wire single slave version of the SPI protocol, the master module is responsible for synchronizing a single slave.
    </ul>
  <li><b>Testing:</b>
    <ul>
      <li>Testing is a crucial component of hardware programming, and as such, we allocated significant time to debugging and validating our code. 
<li>To ensure accuracy at every level, we created testbenches for the sub-blocks and conducted individual tests on the master and slave blocks.
 <li>Our focus was on verifying one-way communication (half-duplex) between the blocks initially, which proved successful as evidenced by the waveform analysis of the sub-blocks.
<li>Subsequently, we proceeded to test the top module, which facilitated the two-way communication.
<li> This proved to be the most challenging part of the testing process as most of the checkpoints were internal for the top module. Therefore, debugging took longer than anticipated.
<li>Despite the challenges, we remained diligent in our efforts and committed to resolving any issues that arose.
    </ul>
</ol>

## Finite State Machine (FSM)/ Flowchart
<img width="724" src="https://user-images.githubusercontent.com/103300115/236622722-a19538cc-5c1d-456c-9959-96dc09756030.png">

## Xilinx Simulation Results of sub-blocks
<ul>
  <li>Master block</li>
  <br/>
  <img width="724" alt="waveform_spi" src="https://user-images.githubusercontent.com/99636505/236382193-65a6d91c-204c-45a6-9083-46f90387a18e.png">
  <br/>
  <li>Slave block</li>
  <br/>
  <img width="724" alt="waveform_spi" src="https://user-images.githubusercontent.com/99636505/236420663-a9417960-be57-4da6-9821-7d3eb8e54a61.png">
  <li>Top-level block</li>
  <br/>
  <img width="724" alt="waveform_spi" src="https://user-images.githubusercontent.com/103300115/236622822-733fe75d-e900-457c-b382-221564d07459.png">
  </ul>
  
  ## Conclusion
  The SPI Master module will accomplish the following:
  <ul>
<li> Converting 8-bit parallel data received by the host into serial data and transmitting it to the slave.
<li> Receive serial data from the slave, convert it to parallel data, and output it through the parallel port.
<li> Output the input signal required by the slave, the clock signal SCLK, and the chip select signal CS.
  </ul>
The SPI Slave module will accomplish the following:
<ul>
<li> Receive serial data from the master performing the desired operations based on the commands received.
<li> Output the input signal required by the master.
</ul>

## References
<ul>
<li> https://hackaday.io/project/119133-rops/log/144622-starting-with-verilog-and-spi
<li> https://www.fpga4fun.com/SPI2.html
<li> https://fastbitlab.com/spi-behind-scene-data-communication-principle/
<li> https://www.researchgate.net/publication/339088398_FPGA_Implementation_of_SPI_Bus_Communication_Based_on_State_Machine_Method
</ul>





