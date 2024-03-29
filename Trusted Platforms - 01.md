# Trusted Platform Modules & Intel SGX

## I. Introduction to Trusted System Concepts

### 1. Trusted System

- A system is trusted if it always **behaves** in the **expected manner** for the **intended purpose**

### 2. Trusted Platforms

- Trusted Platforms provide **Trusted Components** in **HW & SW**
- **Trusted Computing Base** should be **minimized** and **compatible** to **commodity systems**
- **Trusted Components** provide a set of **cryptographic and security** functions
  - To create **trust foundation** for SW
  - To provide **protection** to sensitive data

### 3. Goals of Trusted Computing

- Improve **security** of **computing platforms**
- **Reuse** existing **software modules**
- **Applicable** to **different OS**
- **Open** **architecture**
- **Efficient** **portability**
- Allow **realization** of **new applications** and **business models**

### 4. Desired Primitives

#### 4.1. Metric for Code Configuration

- **I/O behavior** of machine based on an **initial state**
- **Represented** by the **hash value** of the **binary code**
- **Problems** arise when **functionality** depends on **codes not included** in **hashing**

#### 4.2. Integrity Verification

- **Computing platform** can export **verifiable information** about its **properties**

#### 4.3. Secure Storage

- To guarantee **data secure** between executions using **traditional untrusted storage** like HDD
- To **encrypt data** and **ensure** to **be** the **only one who can decrypt it**

#### 4.4. Strong Process Isolation

- Assure separations between processes
- Prevents a process from **reading and modifying** other process's memory

#### 4.5. Secure I/O

- Assure the **end-points** of input and output of operations
- A user can **interact securely** with the **intended application**

## II. Trusted Platform Modules

### 1. Chain of Trust

- **Purpose** is to **gain Trust** for Entity $E_n$
  - To trust $E_n$ , we must trust $E_{n-1}$
- $E_0$ launches $E_1$, $E_1$ launches $E_2$
- $E_0, E_1, ... , E_n$ creates ***Chain of Trust***

#### 1.1. Transitive Trust

- **Trust** is **transitive** from $E_0$ to $E_1$ to $E_2$
- Trusting $E_0$ does NOT mean trusting $E_2$
- Trusting $E_2$ requires to trust $E_0$ and $E_1$

### 2. Performing Integrity Measurements

- Each item **measures** the **next item** before **passing the control** to the next item
- **Root of Trust for Measurements** will measure $E_0$
  1. RTM measures $E$
  2. RTM creates Event Structure in SM Event Log
  3. RTM extends values into Register
  4. RTM passes control to $E$

### 3. Trusted Platform Module - TPM

- TPM is **cryptographic co-processor**
- **Embedded** into the **platform motherboard**
- Provide a set of **cryptographic and security functions**, **secure storage** and **platform integrity measurement**
- **Acts** as RTM
- **Vendors** have already shipped their platforms with TPM
- **Components**: SHA-1, Random Number Generation, Key Generation, Platform Configuration Register ...

#### 3.1. Endorsement Key

- **Certified** by EK-**generating** entity
- Endorsement Key is TPM **identity**, embedded in TPM
- **Unique** en-/decryption **key pair**
- **Generated** during TPM manufacturing
- Can be deleted/re-generated by TPM owner
- Readable from TPM

#### 3.2. Endorsement Credential

- **Digital certificate** stating that **EK** has **been** properly **created and embedded** in **TPM**
- **Issues** by **entities** who **generate EK**
- **Includes** TPM manu. name / model number / version / Public EK

#### 3.3. Methods of Proving Ownership to a TPM

- **Prove** the knowledge of the **owner authorization secret** to TPM
- **Assertion** via **physical presence**

### 4. Platform Configuration Registers - PCRs

- It is **shielded location** to **store** **integrity measurement values**
- **Integrity measurement** is done by hashing **the current state of application** and **the prev. $PCR_i$** as follow $PCR_{i+1} \leftarrow SHA1( PCR_I, value )$. This will result a **hash chain**
- Through the **PCR extension**, $PCR_i$ value **depends** on **all previous measurements** in order to **create** ***Chain of Trust***

### 5. Core Root of Trust for Measurement - CRTM

- **Immutable portion** of the **host platform**’s initialization code that executes **after** host platform **resets**
- **CRTM implementations**: BIOS or BIOS Boot Block

## III. Basic Applications

### 1. Secure Storage

- TPM contains **Root of Trust for Storage**, which is represented by **Storage Root Key**
  - **Simulate** unlimited secure storage through **encryption**
  - Generate new key
  - **Encrypt** the **key** by **Storage Root Key**
  - **Encrypt** **data**
  - **Store** encrypted data **outside** TPM
  - When access, **load data from** tradition untrusted storage and **decrypt**

#### 1.1. Binding

- Conventional **asymmetric** encryption
- **Used to** bind data to a specific TPM that know **corresponding** key
- Used with non-migratable key / migratable key
- **No interaction** with TPM required

#### 1.2. Sealing

- Bind data to a **specific TPM**
- Used with non-migratable key
- **Data** can be **decrypted** only if **platform** is in a **pre-defined state**

#### 1.3. Non-migratable key vs Migratable key

- Non-migratable key is **a unique key** bound to **a specific TPM**. Cannot migrate to other TPM
- Migratable key is a **key not bounding** to a specific TPM. Can use or move to other TPM with **suitable authorization**

### 2. Attestation

- **Authentic report** of **state** of platform to **verifier**, signed by **Attestation Identity Key**

## IV. Intel SGX

### 1. Goals

- **Protect** the **execution** of a certain **code fragment**

### 2. Assumptions

- **Security critical code** is isolated in an **enclave**
- Trust CPU only
- Enclaves **not harm** system

### 3. SGX Enclaves

- x86 architecture **extension**
- **Isolated memory regions** of code and data
- **Every access** to enclaves controlled by **CPU controls** 
- **Memory** is **protected** by **encryption** and **integrity protection**

#### 3.1. Access Control

- From enclave to the outside
  - Access to outside will cause exception
  - All **memory accesses** have to follow **segmentation policies**
  - **Enclave** **not allow** to **modify** **policies**
  - Only **unprivileged instructions** available
- From outside to enclaves
  - Access to enclave from outside will cause exception
  - Hardware **prevents jump** to enclave
  - **No direct access** to **internal** enclave
- Enclave to enclave
  - **Secure channels** can be established