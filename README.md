![CoverIm](https://user-images.githubusercontent.com/94695487/142817169-06d03bfe-98de-4e4c-a043-b8af26535f0e.PNG)
 

**Band Gap Reference Workshop**




**Sai Mounica Munukutla**




**BGR WORKSHOP**




Index




●Introduction

●Voltage divider

●Forward bias PN junction

●Base-Emitter Voltage Reference Circuit

**Introduction to BGR**

●Why BGR?

●Applications of BGR

●BGR working principle

●Types of BGR

**Different components of BGR**

●CTAT Voltage

●PTAT Voltage

●Self Biased Current Mirror Circuit

●Reference branch

●Start Up Circuit

**Lab Analysis**

●Tools and PDK

●Design specs, Data, Steps

●Design using spice netlist

●CTAT circuit design and pre-layout simulation

●PTAT circuit design and pre-layout simulation

●Start-up circuit simulation

●Ideal BGR design and pre-layout simulation

●Complete BGR design and simulation

●Layout components


**Introduction:**
    
When we consider a typical integrated circuit, it consists of both Analog as well as digital components. And also, it requires a range of supply voltages. In order to get these voltages we introduce LDOs tin to the ICs.
LDOs provide the linear supply voltage, and the main requirement for the LDO is a reference voltage that is independent of the process, temperature and supply voltage variations. This same reference voltage can also be used for different blocks in the IC such as ADCs and DACs.
We are trying to generate this voltage from a process, voltage and temperature (PVT) independent biasing circuit, that is the Band Gap Reference circuit.

**Voltage Divider:**

Let us analyse the voltage divider circuit and figure out whether or not we can use it for the generation of the reference voltage.

![Voltage_divider_circuit_1](https://user-images.githubusercontent.com/94695487/142810030-7122a7aa-ec40-4c05-8dc7-d8721d8e2df4.jpg)

**Pros:**
-Simple circuit
-One of the easiest ways to generate reference voltage
-Voltage divider has Good temperature coefficient.

**Cons:**
-When we express the sensitivity of the circuit with respect to Vdd, it gives unity. Meaning, whenever there is a change in Vdd, our reference voltage also changes. And this particular scenario is undesirable.
Therefore, the voltage divider cannot pass the PVT independent biasing rule to have a reference voltage.

**Forward bias PN junction:**
The failure of the voltage divider circuit brings the forward bias PN junction into picture.

![PNJunctiom_1](https://user-images.githubusercontent.com/94695487/142810236-ec91a3f1-6fd5-4cff-8e3c-daa775deb52c.jpg)

**Pros:**
-The sensitivity of the forward biased pn junction is less than unity because the biasing current is more than the saturation current.

**Cons:**
-It does not pass the power supply rejection requirement (typically it should be 40-60 dB)
-Temperature coefficient is not ideal. (required in the range of 10-50 ppm/degree celsius Vref= 1v).

**Base-Emitter Voltage Reference Circuit:**
This is an improved version of forward bias PN junction circuit.

![BaseEmitter_1](https://user-images.githubusercontent.com/94695487/142810298-7df14139-c736-4906-8a8e-e42b7d88036e.jpg)

Here we are using a current mirror and a start up circuit to overcome the failures of the previous forward biased pn junction.
**Pros: **
-The above drawn circuit has a good supply rejection. (PSRR)

**Cons:**
-The issue comes with the BJT in the circuit, temperature coefficient is dominated by the BJT. Hence we cannot achieve the desired Tempco using this circuit.

**Introduction to Bandgap reference:**
Let us look into the block diagram of a BGR.

![BGRblock_1](https://user-images.githubusercontent.com/94695487/142810390-87d1c53e-331f-45e2-81d2-cac05807ad0b.jpg)

Using the upper part of the circuit, we are generating a voltage with negative temperature coefficient and another voltage is generated using the below part of the circuit that has a positive temperature coefficient. We are using an amplifier with a gain K so that the negative tempco matches the positive tempco. Once the linear terms get cancelled, we are left with higher order values which is sufficient to give the desired tempco as shown in the above image.

**Note:** We are generating the thermal voltage (Vt in the block diagram) by taking the difference of two forward biased PN junction diodes, biased at two different current densities. 
We obtain the reference voltage that is independent of process, voltage and temperature variations.

![VwrtT](https://user-images.githubusercontent.com/94695487/142810570-b469009c-b076-44a7-b573-2badd8305d74.PNG)

**Advantages of BGR:**
-BGR produces constant voltage regardless of power supply variation, temperature changes, and circuit loading.
-Because of the reference voltage that is independent of PVT variations , it is widely used in almost all the analog blocks in the IC.

** Interesting fact:** BGR (Bandgap reference) gets its name from the fact that the output voltage is close to the band gap energy of silicon at 0 degree kelvin.

**WHY BGR?**
-Battery to generate reference voltage: When we use a battery, voltage drops over the time because of the drainage or continuous use.
-Power Supply to generate reference voltage: Usage of power supply may introduce noise and ripple in the circuit so it is also not desirable to generate Vref.
-Using buried Zener Diode: It introduces thermal noise in the circuit which in turn needs additional equipment and high frequency filtering circuits. And also, we do not have a low voltage zener diode available in the market.

Without a doubt, BGR surpasses all the requirements and also can be used in BiCMOS, bulk CMOS technologies without having any external components.

**Applications of BGR:**
As we discussed , BGR is used in many blocks on Integrated Circuits. Few of the applications are mentioned below.
**-Low dropout regulators (LDOs):**

![LowDropout](https://user-images.githubusercontent.com/94695487/142810761-b4c8a2e7-e8f3-437a-b202-94c5ec1bde6e.PNG)

**- DC to DC buck converters:**

![DC2DCBuck](https://user-images.githubusercontent.com/94695487/142810859-1b307b10-9901-49aa-b425-69127c804dd1.PNG)
           
**-Analog to digital converter (ADC):**

![A2D](https://user-images.githubusercontent.com/94695487/142810944-8dedad43-31f5-470b-ac8b-3f098f3a9a0e.PNG)

**-Digital to Analog converter (DAC):**

![D2A](https://user-images.githubusercontent.com/94695487/142811019-811910d0-5850-47ee-bd62-ce0a32fd1be8.PNG)
    
**BGR working principle:**
How is the BGR output always constant?

![BGRprinci_1](https://user-images.githubusercontent.com/94695487/142811087-46017bab-e53a-44ed-8c4c-c83402c763e2.jpg)

When we add CTAT voltage (mentioned in the below image) and PTAT voltage, we get a constant voltage that is independent of Temperature.
**CTAT:** Complementary to absolute temperature (when temperature increases, voltage decreases and vice-versa).
**PTAT:** Proportional to absolute temperature (when temperature increases, voltage increases and vice-versa).

**Types of BGR:**
We categorised the BGR types depending upon their architecture and application.

-There are two different architectures of BGRs.
1)Using self biased current mirror
2)Using an Operational amplifier.

-There are four different BGRs depending upon their applications.
1)Low-Voltage BGR
2)Low-Power BGR
3)High PSRR (power supply rejection ratio) and low noise BGR
4)Curvature compensated BGR.

I am using a self biased current mirror based BGR. Pros and cons are listed below.
**Pros:**
-Simplest topology
-Easy to design
-Always stable

**Cons:**
-Low power supply rejection ratio.
-Cascode design is needed to reduce PSRR.
-Voltage headroom issues.
-Need of a start up circuit.

**Different Components of BGR:**
-CTAT Voltage generation circuit
-PTAT voltage generation circuit
-Self biased current mirror circuit.
-Reference branch circuit.
-Start - up circuit.

**CTAT Voltage Generation:**
Using the below circuit we are going to generate CTAT voltage.
Here, we are using a variable current source and a BJT of one multiplier.

![CTAT_1](https://user-images.githubusercontent.com/94695487/142811342-4f845065-6fdc-446c-a6d9-8c7534d3468c.jpg)
               
**PTAT Voltage generation:**
Using the below circuit, we are going to generate the PTAT voltage.
R1 design is very critical in PTAT. R1 completely depends upon the power consumption and the silicon area budget. Also it depends on the BJT used in the branch 2 of the circuit.

![PTATImage](https://user-images.githubusercontent.com/94695487/142812243-ef40775a-33cd-471f-ba06-e0e8ff3789aa.PNG)

Characteristics of the above PTAT circuit would look like this.

![PTATchar_1](https://user-images.githubusercontent.com/94695487/142812746-43a62576-2b7d-427c-baf5-b6e67cb4af97.jpg)

**Self biased current mirror circuit:
Current Mirror:**

![CurrentM](https://user-images.githubusercontent.com/94695487/142813161-daa2b79d-7336-4978-b351-39352958396e.PNG)

**Issues with the above circuit:**
-Output is sensitive with respect to VDD.
**Solution:**
-The circuit should bias itself, i.e. Iref should be derived from Iout.

**Self biased current mirror:**

![Scan Nov 21, 2021_1](https://user-images.githubusercontent.com/94695487/142813522-cc006a6e-a86b-40e1-b6b0-b2cef8f622d2.jpg)

-Each diode connected device feeds from a current source, Iout and Iref are independent of VDD.
**Issues:**
-The circuit is governed by one simple equation, Iout= K*Iref, hence it can support any amount of current.
-To overcome this, we need to introduce another constraint into the circuit.

![SBCMOri](https://user-images.githubusercontent.com/94695487/142814337-7b17b3c6-62d0-470b-8489-604a383f1493.PNG)

-Rs has been introduced into the circuit that defines the current.
-Iref and Iout are less dependent on VDD.
-For this circuit, loop gain is always less than one. So by default the circuit is stable.
Issues:
-Degenerate bias point.
-Start-Up problem when supply is turned on.

**Reference Branch:**

![RefBranch_1](https://user-images.githubusercontent.com/94695487/142814764-96b216ef-071a-4ce3-86e3-82c5a049c5d6.jpg)

-Current in MP3 is the same as MP1 and MP2.
-Voltage across BJT Q3 is CTAT type.
-Voltage across resistor R2 is PTAT type.
-Vref= CTAT + PTAT.
-R2 = alpha * R1 (alpha is constant).

**Start Up Circuit:**

![StartUpcir](https://user-images.githubusercontent.com/94695487/142815264-8366ebf0-d7f6-4c2c-8b57-2adf6f5924f4.PNG)

**Complete BGR Circuit:**

![CompleteBGRDraw_1](https://user-images.githubusercontent.com/94695487/142815554-45c66767-6cdb-486a-819c-06aa58ca9836.jpg)

**LAB Analysis:**

**Tools and PDK:**
-PDK used: Google skywater 130nm
-Tool used for pre-layout simulation: NgSpice
-Tool used for Layout design: Magic
-Tool used for DRC & PEX: Magic
-Tool used for LvS verification: Netgen
-Tool used for post layout simulation: NgSpice.

**Design Specs, data and steps:**

**Devices Used:**
-NFet, LVT type, 1.8V, Vth = 0.4V, sky130_fd_pr__nfet_01v8_lvt
-PFet, LVT type, 1.8V, Vth = -0.6V, sky130_fd_pr__pfet_01v8_lvt
-BJT PNP, beta = 12, current range = 1uA - 10uA, sky130_fd_pr__pnp_05v5_W3p4013p40
-RPOLYH, 350ohm, 2.5 ohm/deg cen, sky130_fd_pr__res_high_po

**Design using spice Netlist:**

**PTAT:**

![PTATCode](https://user-images.githubusercontent.com/94695487/142815889-878fe71d-be64-4c0d-aa0a-2a7dfd864c76.PNG)

![PTATPlot](https://user-images.githubusercontent.com/94695487/142816191-6386bf0f-bad8-4f32-b7ed-0505b9cd8404.PNG)

**CTAT:**

![CTATcode](https://user-images.githubusercontent.com/94695487/142816261-332fdb8f-9f90-44c1-a8c0-2456d4d46111.PNG)

![CTATplot](https://user-images.githubusercontent.com/94695487/142816289-e040b6a1-5df4-48dc-a940-038f1e6b114e.PNG)

**Ideal BGR:**

![idealBGRspec1](https://user-images.githubusercontent.com/94695487/142816372-6417767f-cdcd-4501-a320-1ca258bdae18.PNG)

![idealBGRspec2](https://user-images.githubusercontent.com/94695487/142816391-f29fa085-fee9-42fc-b583-84114c6fade2.PNG)

![IdealPlot](https://user-images.githubusercontent.com/94695487/142816411-59536dc4-9689-4d76-a900-a7ef878e2242.PNG)

**Complete BGR design & simulation:**
**ff corner:**

![ffcorner](https://user-images.githubusercontent.com/94695487/142816505-2d133c72-2999-4b47-a6c6-2226a3a7fb07.PNG)

**ss corner:**

![sscorner](https://user-images.githubusercontent.com/94695487/142816559-f3f30fbb-6834-4550-9ef2-e8d3a889a2c4.PNG)

**tt corner:**

![ttcorner](https://user-images.githubusercontent.com/94695487/142816661-f8eb6963-2704-4498-ac99-0b77e960e7da.PNG)

**Layout Components:**
**-Nfet layout:**

![NfetLayout](https://user-images.githubusercontent.com/94695487/142816720-0d2cdecf-33bd-4749-b861-2b948ca8e20a.PNG)

**-Pfet layout:**

![pfetlayout](https://user-images.githubusercontent.com/94695487/142816775-6ffe2105-26f5-4f03-ba1e-8c13cb95d495.PNG)

**-Resistor bank layout:**

![Resistorbanklayout](https://user-images.githubusercontent.com/94695487/142816817-d67a0fd3-3017-4703-8fce-de49d02f5757.PNG)

**-Start up layout:**

![startuplayout](https://user-images.githubusercontent.com/94695487/142816869-1f22c8cd-1503-4c4c-9a7e-946eee26d36d.PNG)

**-Pnp layout:**

![pnpbjt](https://user-images.githubusercontent.com/94695487/142816953-c10d3609-98ce-42f6-bc82-7bd65548c40d.PNG)

**-Entire Top Level:**

![toplevel](https://user-images.githubusercontent.com/94695487/142817017-dd6f7902-5d16-46d5-abd3-9c6a80faaf74.PNG)
