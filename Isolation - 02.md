# Micro-architectural Attacks

## I. Definition

### 1. Microarchitecture

- SW/HW **Interface** to **enhance performance** and **implement instructions** in HW
- **Transparent** for **processes** and **programmers**

### 2. Micro-architectural Attack

- **Combination** of attacks
  - **Covert Channels** for the **purpose** of **Information Leakage** & **Privilege Escalation**
  - By using **Side Channels** for **targeting** the specific **Computer Microarchitecture**

### 3. Pipelining & Out of Order Execution

- **Pipelining**
  - **Several stages** in each execution for an **instruction**
  - When one stage finishes, a next command will be loaded
- **Out of Order Execution**
  - Execution of Command **not correspond** to the order in program
  - Execution of Command is **changed** to **prevent stalls**

### 4. Memory Hierarchy

- Use the **locality** of most **memory accesses** to provide **fast memory access**
- **Copy** recently **accessed objects** and their **neighbors** to **smaller memory**

### 5.  Isolation

- **Separation memory area** between processes
- Covert Channels aim to **break** isolation between processes

## II. Meltdown

### 1. Definition

- Exploit **side effect** Out of Order Execution
- Read **Arbitrary Kernel-Memory Locations**
- It **breaks** all **security mechanism** provided by **Address Space Isolation**
- **Not depend** on **OS** or **SW vulnerabilities**

### 2. Countermeasure

- No Out of Order Execution
- **Strict Hardware-based** separation of **Kernel** and other **SWs**
- **Isolation of Kernel-Memory Locations** by using **SW**

