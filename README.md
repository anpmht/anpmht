## 8 channel DAQ device
This project was done to measure stress on the various parts of a two-wheeler vehicle for testing and verification purposes. Strain gauges are used to measure stress on the chassis. A strain gauge is a passive sensor that requires external excitation. Strain gauges change their resistance when bent or stretched. The strain gauges are placed on a Wheatstone bridge configuration to detect the change in resistance, which is given by the Wheatstone bridge in the form of voltage output.

<p align="center">
  <img src="https://github.com/anpmht/anpmht/assets/42551612/c5707748-49d1-403c-9fca-1456b298cd81"  width="20%" >
</p>

This change in voltage is very low (in the range of microvolts to a few millivolts). This small change in voltage cannot be measured directly through the microcontroller accurately, so this signal needs to be amplified by an amplifier to the range where the microcontroller or ADC can read the signal in high resolution. The signal output from the strain gauge or load cell is very weak and prone to external noises. In order to amplify this signal, an amplifier with a high common mode rejection ratio, good EMI filter, and built-in noise immunity to noises from the AC source (50 and 60 Hz) is required.

Depending on the position of the strain gauge on the chassis, the range of voltage output given is also different, and we want to utilize the full range of the ADC's voltage reading capability. Therefore, a programmable amplifier with gain settings from 1/128 to 128 was selected. The amplifier also has a common mode rejection ratio of 116 dB and built-in noise rejection for 50 and 60 Hz. The amplifier also has safety features for over-amplification and input overvoltage protection. Considering all these requirements, ADA4254 was selected for my project.

After selecting the amplifier, a sample test board was designed and tested. This board was designed for testing the capabilities of the amplifier. The designed board can be seen below.

<p align="center">
<img src="https://github.com/anpmht/anpmht/assets/42551612/4888e8d5-5d05-4013-bb50-fae23854b8ad"  width="33%" >
<img src="https://github.com/anpmht/anpmht/assets/42551612/7a98f07a-910b-46c9-9774-4f10c43972f2"  width="40%" >
</p>

After the board was tested and verified to satisfy our requirements regarding amplification range, noise immunity, EMI protection, and fault protection, a full-fledged DAQ system was designed using this amplifier. Another part of the project was selecting an ADC. The ADC should have a high sampling rate, high resolution, be linear on wide voltage ranges, and have differential input reading capability. Considering all these requirements, I selected the ADS1256 as the ADC for this project. It has 24-bit resolution with up to 23 noise-free bits, up to ±0.0010% nonlinearity, a sampling rate of 30 kHz, and four differential channels.

After selecting the ADC, a fast microcontroller was needed to program the amplifier, program the ADC, and extract the data from the ADC. Additionally, I planned on adding about 10 accelerometers as peripherals and some position and RPM sensors to the device, so a high number of I/O pins was needed on the microcontroller. Considering all the requirements, the Teensy 4.1 microcontroller was selected as it has a very large number of I/O pins and operates at 600 MHz.

After selecting the main components, the DAQ board was designed. The final design of the DAQ board is shown below.

<p align="center">
<img src="https://github.com/anpmht/anpmht/assets/42551612/699009b5-df56-4bb3-862a-20f0ec763c6e"  width="30%">
</p>

This board requires a power supply of ±12 volts. The negative supply is needed to amplify the negative differential signals. The amplifier requires a ±12-volt signal and a digital power supply of 5V and 3.3V. The ADS1256 requires two voltage supplies: a 5V supply for the analog part and a 3.3V supply for the digital part. The Teensy 4.1 needs a 5V supply, which is regulated by its internal regulator.

SMA connectors are used to connect the strain gauge signals to the DAQ board, along with shielded cables to shield the signal from the strain gauge to the amplifier. Before the signal goes to the amplifier, the Wheatstone bridge needs to be balanced. For this purpose, 15-turn 100K trimmers are placed on the board, which can pull the signal up or down to balance the Wheatstone bridge under ideal conditions. After that, the signal passes through test points to reach the amplifier. There are test points on both the input and output signals of the amplifier. The amplifier's output signal then passes through a low-pass filter to the differential inputs of the ADC. The ADC also requires an external crystal of 7.68 MHz to perform internal sampling and conversion operations. All the amplifiers and ADCs are connected to the Teensy via SPI lines. The final assembled board of this project is shown below.

<p align="center">
<img src="https://github.com/anpmht/anpmht/assets/42551612/c3bac8ef-68d6-4719-99f6-c17e9932acf5"  width="30%">
</p>

For the implementation of this board to collect road load data from the vehicle, two boards were used to collect data from 16 channels of strain gauges. Additionally, 10 ADXL345 accelerometers were connected to this system, along with two LVDT position sensors to determine acceleration at various positions of the bike and to measure shock displacement.

To integrate the two DAQ boards together, a daughter board was created on the matrix board, which controlled both boards simultaneously. The daughter board facilitated the coordination and synchronization of data acquisition from multiple sensors. The setup is depicted below.

<p align="center">
<img src="https://github.com/anpmht/anpmht/assets/42551612/53de2fd8-1001-4128-a392-1af647ac673f"  width="30%">
</p>

the final implementation of the DAQ system to collect road load data can be seen in the figure below.

<p align="center">
<img src="https://github.com/anpmht/anpmht/assets/42551612/b9c7649c-65d5-42df-88a9-e19875e74379"  width="30%">
</p>

