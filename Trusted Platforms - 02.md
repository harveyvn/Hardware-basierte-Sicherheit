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



## III. Attestation of Physical Attacks

