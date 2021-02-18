# Physically Unclonable Functions

## Questions:

1. How do manufacturing variations make hardware unique?
2. Which types of Physically Unclonable Functions exist?
3. How can errors/imperfections be corrected?
4. Which applications do PUFs have?

## I. PUFs Concept

### 1. Definition

- **Idea:** A function, which is embedded into a physical object
- **Work:** When queried with **a challenge $x$**, the PUF generates **a response $y$**. Response $y$ **depends on challenge $x$** and **physical properties of the object**

### 2. Properties of PUFs

- **Unclonability**: the PUFs should be impossible to clone (even for the manufacturer). Ideally, we should have both physical unclonability and mathematical unclonability
- **Robustness**: the same challenge $x$ should always produce (almost) the same response $y$
- **Unpredictability**: responses for challenges not seen before are impossible to predict
- **Tamper-Evidence**: the PUFs can change their challenge-response behavior when attacked invasively

### 3. Enrollment / Verification

- **Enrollment**: read several PUFs responses initially and create a PUF challenge/response db. Likely during manufacturing
- **Verification**: read PUFs responses at a later time and compare to PUFs responses in an enrollment

## II. PUF Types

### 1. Optical PUF

- It uses a laser beam to generate **random speckle pattern** through transparent material. Then the pattern will be recorded and post-processed to produce output.
- **Disadvantage**: 
  - Require an expensive optical hardware 
  - Require an extreme precise measurement for responses

### 2. Arbiter PUF

- Signal races through **series** of arbiters
- Each arbiter is configured by **one bit of a challenge**
- Signal **runtimes** differ at each stage
- Signal will arrive earlier **at one of two paths**
- **Disadvantage**: 
  - Design must be **precisely symmetric** to get random response
  - **Challenge space** is exponentially **large** but its **secret response** is **linear**

### 3. Ring Oscillator PUFs

- Count the **oscillation freq.** of a **pair** of oscillators
- Oscillation freq. depends on the **signal delays**
- **Output bit** **corresponds** to the oscillator being faster
- **Disadvantage**: few physical oscillators generate responses

## III. Memory-Based PUFs

### 1. Advantages

- **Intrinsic**: don't require additional hardware for their operation, so it is cost efficiency
- **Lightweight**
- **Flexible**: multiple keys of variable key length, even after the device has left production, can be created
- **Practical**: keys can be accessed at runtime

### 4. SRAM PUFs

- SRAM **cell** consists of **cross-coupled inverters**
- Both inverters are slightly **different** due to **production variations**
- In theory, there should be **infinite loop at startup**
- In practice, the larger inverter wins and draws **startup value** to a certain bit
- **Disadvantage**: require **reboot** in order to gain **access** to **startup value**

### 5. DRAM PUFs

- DRAM **cell** consists of **a capacitor and a transistor**

- **Bit** is **stored** as **charge** which **leaks** over time. So their **values** need to **refresh** periodically

- When **DRAM refresh** is **disabled**, some cells will lose their charge and their logical value will change

- **Advantage**: 

  - Due to the **manufacturing variations**, some cells decay faster than others, which can be exploited as PUF
  - DRAM PUFs can be **utilized** at runtime without reboot, unlike SRAM PUFs

- **Disadvantage**: Sensitive to temperature

  #### 5.1 Accessing the DRAM PUF

  1. DRAM is ready to use
  2. PUF region is initialized and the DRAM refresh is disabled
  3. PUF cells decay for time $t$
  4. Read the DRAM to extract the PUF measurement
  5. DRAM returns to normal usage

### 6. Rowhammer PUFs

- Write repeatedly to DRAM cells until **errors** occur in memory
- **Location** of errors are unique for each device
- **Strategy**: reserve memory area, write repeatedly and observe bit flips

## IV. Comparison of PUF types

### 1. Voltage Variation

- Arbiter, Ring Oscillator and Latch PUF are sensitive
- Flip-flop (DFF) and SRAM PUF are not

### 2. Temperature Variation

- DFF, Latch, and DRAM PUFs are sensitive
- SRAM is little affected
- Arbiter and Ring Oscillator are not

### 3. Entropy Tests

- Arbiter and Latch PUFs have low entropy and low min-entropy
- Ring Oscillator and DFF PUFs have acceptable entropy and low min-entropy
- SRAM PUF has the highest entropy and highest min-entropy

## V. PUF metrics

### 1. Hamming Weight

- **Property**: Unpredictability
- Compute Hamming Weights of different responses of the same PUF
- **Value** closes to 0.5 indicates no bias in response

### 2. Intra Hamming Distance

- **Property**: Robustness
- Given a particular challenge, compute Hamming Distances between different measurements of the response of the same PUF
- **Value** closes to 0 indicates stability in response

### 3. Inter Hamming Distance

- **Property**: Unclonability
- Given a same challenge, compute Hamming Distances between responses of different PUFs
- **Value** closes to 0.5 indicates unique response per device

### 4. Intra Jaccard Index

- **Property**: Robustness of DRAM decay-based PUF
- Given a particular challenge, Jaccard indices for different measurements of the response of the same PUF
- **Value** closes to 1 indicates stability

### 5. Inter Jaccard Index

- **Property**: Unclonability and Unpredictability of DRAM decay-based PUF
- Given a same challenge, Jaccard indices for responses of different PUFs
- Prefer **value** closes to 0

## VI. Errors / Imperfections

- Fingerprint should be 100% stable to derive key for encryption. If it is not stable, errors must be corrected.

### 1. Enumeration of error patterns

- **Idea**: Generate **hash** for every **possible error** and **check** if **expected** hash is among the hash values
- **Advantage**:
  - Fast for small error ranges
  - Easy to implement
- **Disadvantage**:
  - Grow **exponential** with **complexity** of the error pattern

### 2. Indices to stable bits

- **Idea**: **Mask out** unstable bits and use only the stable bits of the PUF response
- **Advantage**:
  - Fast for small error ranges
  - Easy to implement
  - **Helper data** **independent** of PUF response bits
- **Disadvantage**:
  - Require 100% stable bits which is often not the case
  - **Indices to stable bits** may have PUF characteristics themselves

### 3. Code Offset Method

- **Idea**:
  - Enrollment:
    - Measure the PUF: $r$
    - Choose random $w$ so that $r+w$ is a code word $c$
    - Store Hash $(r+w), w$ 
  - PUF measurement:
    - Measure the PUF: $r’$
    - Error correct $r’+w$ to $c$
    - Hash(c)
- **Advantage**:
  - Can correct all errors that the **relevant error correction code** can correct
  - There is **dependence** on **expected amount**, **type of errors**, **the failure probability** 
- **Disadvantage**:
  - Slow in hardware

## VII. PUF-base applications

- Identification & authentication: PUF response is unique, so it can identify device
- Key storage: no key needs to be store on disk
- Random Number Generators: used as TRNG based on unpredictability property of PUF response

### 1. Hardware Software Binding

- Avoid the device's SW can be executed on another device
- **Bootloader Protection**
  - Use PUF response $S$ to generate key $K$ as $K=SHA(S)$ for the encryption of the stage bootloader 
  - Derive another key within the 2^nd^ stage bootloader to **decrypt kernel file**
  - The firmware can only start on the corresponding device
- **SW integrity Protection**
  - Calculate **checksum** of the **code program** by **hash function** 
  - Bind SW on PUF response
  - When starting the program, recalculate checksum and check the PUF
    - Program starts only if both values are valid