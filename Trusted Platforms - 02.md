# Collective Remote Attestation Protocols

## I. Attestation of Device Swarms

### 1. Naive Approach

- Attestation reports are **sent individually** to the **verifier**
- **Disadvantage**: not scale to large networks!

### 2. Collective Approach

- Attestation reports are **aggregated** among **provers**

#### 2.1. Approach

- Attestation **challenge** is **broadcasted** to all **provers**
- A **virtual spanning tree topology** is arranged in the network
- Attestation **responses** are **aggregated**  along the **tree** to the **verifier**
- Verifier uses **the aggregated response** to **verify** the **integrity** of **all prover** 

#### 2.2. Advantages

- **Attestation burden** is **distributed** across network
- **Log runtime** in **tree-based** network topology
- Scalable

## II. Attestation of Dynamic Networks

### 1. Goals

- Prevent **physical** attack: DoS attacks
- Work for **Dynamic Network** and **Disruptive Network Topology**
- Work for **Low-end embedded devices**

### 2. Approach

- **Minimize communication** between devices
- Apply **Disruptive-tolerant Networking Techniques**
- **Individual authenticated** attestation **response**

### 3. Distributed Attestation Protocol

- Devices **propagate** **initial message** from **Verifier**
- **Neighboring** devices **exchange** attestation **proofs**
- Verifier takes a report from any device and verifies it

### 4. Report Aggregation

- Device Identifier List
- Attestation Proof

### 5. Novel Techniques to Compress Attestation Reports

- MAC-Smart: **On-demand aggregation** of attestation reports
- MAC-Truncation: **Tradeoff** between **security** and **performance**

## III. Attestation of Physical Attacks

### 1. Idea to Prevent Physical Attack

- To physically attack a device, an attacker needs to take the device offline for amount of time
- All **devices share** **a session key** which is **replaced periodically**
- **Physically compromised device** cannot obtain the newest session key, which is used for attestation

### 2. SCAPI Protocol

- Initialization phase:
  - **Network operator** initializes the TEE of all devices with the secret $sk_{cur}$ $sk_{next}$
- Session Key Update phase:
  - **Leader device** distributes $sk_{next}$ each session period $\delta$ ( <= $\delta_{attack} / 2$)
  - $sk_{next}$  is only obtained by devices which hold newest $sk_{cur}$ 
  - After each session period $\delta$, devices update $sk_{cur} := sk_{next}$
- Attestation phase:
  - **Operator** executes existing **collective SW attestation protocol**
  - Devices **authenticate and encrypt** all **communication** using $sk_{cur}$
  - **Detect** devices with **compromised SW** 

### 3. Advantage

- **Scalable** protocol that **detects** SW and HW attacks
- **Decrease** **exchanges messages** in each phase to $O(n)$
- **Precise** device identification if less than $n/2$ **devices are compromised**
- **Robustness extension** that **recovers** from **device and network outages**