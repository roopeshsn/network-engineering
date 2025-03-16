# Physical Medium

Sub-layers,

```
 MAC     - L2
-----
 PCS     -|------|
-----     |      |
 PMA      | PHY  |
-----     |      |  L1
 PMD     _|      |
-----     |      |
 Xcvr    _|------|
```

## Sub-layers (in detail)

###  MAC

One stream of data bytes will be sent to the next layer (downstream).

### Physical Coding Sub-layer (PCS)

- Interface between the Physical Medium Attachment (PMA) sub-layer.
- Data Encoding/Decoding (64b/66b)

#### Lane Splitting

- The number of lanes will be different depending on the PMD used.

##### Lane Splitting Examples

###### 10G PCS

<!-- TODO -->

###### 100G PCS

- Possible PMD's are 4 or 10 lanes (4 lanes * 25 G, 10 lanses * 10 G).
- Possible PCS lanes is the LCM of 10 and 4 which is 20 lanes.
- 100 G will be distributes across 20 lanes, which is 5G per lane.

##### Special PCS Block - Alignment Marker

- The Pysical lane can be reordered in the TX and RX systems. For example lane-1 in the TX system might be connected to lane-3 in the RX system.
- We need an identifier for the lanes. This identifier will be inserted for every 16834 blocks
- Helps in reassembling a single 100G or 40G aggregate stream (with all the 64B/66B blocks in the correct order)

### Forward Error Correction (FEC)

- Adds redundant data
- For eg. If the TX system want to transmit the character `W`, the equivalent binary form is `01010111`, it will send the same byte 3 times.
- For each bit position, the receiver compares the bits. If all three are the same, that value is considered the correct bit. If one value is different from the other two, the two majority values are considered the correct bit.

### Physical Medium Attachment (PMD)

- Interface for the input lanes of PCS and output lanes in the transeiver (Lane Multiplexing).
- Clock recovery
- Converts bit streams to electrical signals
- Serdes

### Transeivers

- Different ways to send electrical signals
- Transeiver is an interface between the device's interface and the optical cables.

| Form Factor / Medium     | CR              | SR              | LR              | DR              |
| ------------------------ | --------------- | --------------- | --------------- | --------------- |
| SFP                      | 25G-BASE-CR     | 25G-BASE-SR     | 25G-BASE-SR     |       -         |
| QSFP                     | 100G-BASE-CR4   | 100G-BASE-SR4   | 100G-BASE-LR4   | 100G-BASE-DR    |
| QSFPDD                   | 400G-BASE-CR8   | 400G-BASE-SR8   | 400G-BASE-LR8   | 400G-BASE-DR4   |
| OSFP                     | 400G-BASE-CR8   | 400G-BASE-SR8   | 400G-BASE-LR8   | 400G-BASE-DR4   |

#### Naming Convention

Naming: `<Data Rate><Modulation>-<Media Type><PHY PCS Encoding><Media Lanes>`
Example: 100GBASE-LR4

##### PHY PCS Encoding

R - scRambled Encoding (64B/66B)
X - eXternal sourced coding (4B/5B, 8B/10B)

##### Media Type Codes
| Short Form         | Meaning                                                | Distance or Range                                          |
| ------------------ | ------------------------------------------------------ | ---------------------------------------------------------- |
| C                  | Copper                                                 | 1-3m                                                       |
| S                  | Short                                                  | 300m                                                       |
| D                  | D is 500 is Roman Numeral                              | 500m                                                       |
| F                  | Far or Fiber                                           | 2km                                                        |
| L                  | Long optical wavelength                                | 10km                                                       |
| E                  | Extended or Extra Long                                 | 40km                                                       |
| Z                  | Zuper                                                  | 80km                                                       |
| UNIV               | Universal - both SMF, MMF                              | 40GBASE-UNIV is 150m (MMF) and 500m (SMF)                  |
| BIDI/ SR1.2/ SR4.2 | Bidirectional                                          | 70-100m                                                    |
| SWDM/ CWDM/ DWDM   | Short/ Coarse/ Dense Wavelength Division Multiplexing. | 100m, 2km, 80km                                            |

Note: SWDM/ CWDM/ DWDM - These three differ over choice of wavelengths for reach.

#### Prefixes and Suffixes

These go in front or end of the media code. 
For example: XDR, SR1.2, 2FR4, PLR4

| Prefix or Suffix | Meaning                                                                                                                      |
| ---------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| X-               | Extended - Additional reach over type specified                                                                              |
| P-               | Parallel - Ex. LR4 multiplexes four wavelengths over 1 fiber pair. But PLR4 uses 4 fiber pairs each with the same wavelength |
| -L               | Lite (shorter reach of base-type: SRL, LRL, …)                                                                               |
| V-               | Very … (VSR means “Very Short”)                                                                                              |
| #-               | # pairs (2FR4 means 2 pairs of FR4)                                                                                          |
| -#               | Distance … 800GBASE-DR8 (500m) vs 800GBASE-DR8-2 (2km) in SFF8024 -> has different application codes                         |
| -E               | No FEC Required (QSFP-100G-SR4-E)                                                                                            |
| -C               | Clock able to be broken-out to individual lanes. QDD-400G-SR8-C supports 8x50G, where QDD-400G-SR8 not.                      |
| -1.2, -4.2 -BD   | BIDIrectional (#_links.#waves)                                                                                               |
| MR-              | Multi Rate. SFP-25G-MR-SR is a 10G or 25G SFP transceiver                                                                    |

Note: For -C, Clock exists for each lane

#### Example Transceiver Part Number

Naming Convention: <form factor>-<data rate><modulation> - <mediatype><phy encoding><media lanes>

QSFP-40GBASE-PLRL4
- QSFP Form Factor
- data rate = 40G
- modulation = Baseband
- phy encoding = R
- Media Type = L (Long 10km)
- Prefix = P (Parallel - Across four parallel fibers)
- Suffix = L (Lite - shorter than 10km)
- Media Lanes = 4

#### Form Factors (in detail)

SFP - 1 lane - Up to 25G/lane
SFP56 or SFP100 - 1 lane - Up to 50G/lane
SFP-DD or DSFP - 2 lanes - Up to 100G/lane, DD stands for Double Density, D is DSPF stands for Dual
QSFP - 4 lanes - Up to 25G/lane
QSFP56 or QSFP100 - Up to 50G/lane
QSFP-DD - 8 lanes - Up to 100G/lane
OSPF - 8 lanes - Up to 100G/lane - higher power than QSFP

#### Optics

##### Directly Attached Cable (DAC)

- Up to 7m distance
- Copper cable and transeivers are permanantely attached

##### Base-T Adapters

- Up to 100m distance
- CAT5 or CAT6 cable

##### Active Optical Cable (AOC)

- Up tp 100m distance
- Multimode fiber and transeivers are permanantely attached

##### Optics

- Many flavors - SR, LR, ER, PLR, ZR etc.

##### Coherent Optics

- Up to 120km
- Single Mode Fiber

#### Why Splitting?

For example, a 40G single port can be splitted to four 10G ports. 

Let's see how to do it. There are two options. In both the options the common steps were,
- Check the transceiver type. Ensure it support 40G.
- Default the interface

Say if you want to split the interface et2/1, which is a 40G port to 4 * 10G ports,

##### How? Option-1:

Run the command `transceiver qsfp default-mode 4x10G`. This command makes the device interfaces split into 4 separate 10G lanes and provide 3 additional logical interfaces to configure.

##### How? Option-2:

Run the command `speed forced 10000full` 

Reference:
(FEC)[https://www.techtarget.com/searchmobilecomputing/definition/forward-error-correctionz]
