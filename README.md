## 8 channel DAQ device
this project was done to meassure stress on the various parts of two wheeler vehicle for testing and verification purpose. Strain gauges are used to meassure stress on the chassis. Strain gauge is a passssive sensor that requires external excitation. strain gauges change their ressisstance when bent or stretched. The strain gauges are placed on a wheatsstone bridge configuration to detect the change in ressistance which is given by the wheatsstone bridge in the form of voltage output.

<p align="center">
  <img src="https://github.com/anpmht/anpmht/assets/42551612/c5707748-49d1-403c-9fca-1456b298cd81"  width="20%" >
</p>

this change in voltage is very low (in the renge of microvolts to few millivolts). This small change in voltage cannot be measured directly through the microcontroller accurately, so this signal needss to be amplified by an amplifier to the range where the microcontroller or and ADC can read the sisgnal in high resolution. the signal output from the sstrain gauge or load cell is very weak and prone to external noises. in order to amplify this signal an amplifier with high common mode rejection ratio, good EMI filter and built in noise immunity to noisess from the AC source (50 and 60 HZ is required). Depending on the posistion of the strain gauge on the chassis the range of voltage output given is also different and we want to utilize full range of ADC's voltage reading capabilityk, so a programmable amplifier with gain sestting from 1/128 to 128 was sseslected. the amplifier alsso has common mode rejection ratio of 116 DB and buitl in noise rejection for 50 and 60 hz. the amplifier also has safety features for over amplification and input overvoltage protection. Consisdering all theses requirements ADA4254 was sseslected for my project. after selecting the amplifier a sample test board was dessigned and tessted. this board was designed for tessting the capabilitiess of the amplifier. the designed board can be sseen below.

<p align="center">
<img src="https://github.com/anpmht/anpmht/assets/42551612/4888e8d5-5d05-4013-bb50-fae23854b8ad"  width="33%" >
<img src="https://github.com/anpmht/anpmht/assets/42551612/7a98f07a-910b-46c9-9774-4f10c43972f2"  width="40%" >
</p>

after the board was tessted and verified that it ssatissfies our requirement regarding amplification range, noise immunity, EMI protection and fault prtection a full fledged DAQ ssysstem was dessigned using this amplifier. After the amplifier selection another part of the project is to select an ADC. The ADC shsould have high sasmpling rate, High resolution, should be linier on wide voltage ranges, should have differential input reading capability. considering all theses requirements i selected ADSS1256 as ADC for this project. It has 24 bit resolution with upto 23 noises free bits, upto ±0.0010% Nonlinearity, sampling rate of 30Khz and four differential channels. After selecting the ADC a fast microcontroller was needed to Program the amplifier, program the ADC and extract the data from the ADC. on top of that i also plan on adding about 10 accelerometer as peripherals and some possition and RPM sensors to the device so high number of I/O pins was needed on the microcontroller. Considering all the requirements Teensy_4.1 microcontroller was selected as it has very large number of I/O pins and operates on 600 MHZ. After selecting the main components DAQ board was designed. the final dessign of the DAQ board is as shown below.

<p align="center">
<img src="https://github.com/anpmht/anpmht/assets/42551612/699009b5-df56-4bb3-862a-20f0ec763c6e"  width="30%">
</p>

this board needs a power supply of +-12 volts. the negative supply is needed to amplify the negative differential sisgnalss. the amplifier needs +- sisgnal of 12 volts and a digital power supply of 5V and 3.3V. ADS1256 requires two voltage supply. 5V supply for analog part and 3.33 volt ssupply for digital part. teenssy_4.1 needs a ssupply of 5V which is regulated by internal regulator.

SMA connectors are used to connect strain gauge ssignal to the DAQ board along with shielded cables to shield the signal from sstrain gauge to the amplifier. before the sisgnal goes to the amplifier the wheatsstone bridge needs to be balanced so 15 turn 100K trimmers sare placed on board which can pull the sisgnal up or down to balance the  wheatsstone bridge in ideal condition. after that the signal passses sthrough tesst points to the amplifier. there are tesst points on both input and output signal on the amplifier. the amplifier output signal is then passsesd through  low pass filter to the differential inputs of the ADC through a low pass filter. the ADC also needs a external crystal of 7.68 MHZ to perform internal ssampling and conversison operation. All the amplifiers and ADCs are connected to teensy via spi lines. the final assssembleed board of this project is as shown.

<p align="center">
<img src="https://github.com/anpmht/anpmht/assets/42551612/c3bac8ef-68d6-4719-99f6-c17e9932acf5"  width="30%">
</p>

for the inplementation of this board to collece the road load data of the vehicle two boards were used to collect 16 channel data from strain gauge. 10 adxl345 accelerometers were also connected to this sysstem along with two LVDT position sensors to determine acceleration at various positions of bike and to determine displacement of shock. to integrate two daq boards together a daughter board was created on the matrix board which controlled both the boards together as shown below.

<p align="center">
<img src="https://github.com/anpmht/anpmht/assets/42551612/53de2fd8-1001-4128-a392-1af647ac673f"  width="30%">
</p>

the final implementation of the DAQ ssysstem to collect road load data can be seen in the figure below.

<p align="center">
<img src="https://github.com/anpmht/anpmht/assets/42551612/b9c7649c-65d5-42df-88a9-e19875e74379"  width="30%">
</p>

