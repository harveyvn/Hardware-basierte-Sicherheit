# Side-Channel Attacks

## I. Introduction to Side-Channel Attack

### 1. Mechanism

- **Physical computation** has some side effects such as:
  - Time
  - Acoustic noise
  - Power Consumption
- Those effects can **leak information** about **the computation**, **inputs** and **outputs**; **creating** so called side-channel, during the **computation of cryptographic primitives and tokens**
- At a result, an attack can **have advantage** and **predict** correctly **value** of **cryptographic components**

### 2. Timing Side-Channel Attack

- Observe the **Timing Behavior** of **computation**
- If the **Timing Behavior** depends on a **cryptographic token**, the token can be leaked

### 3. Power Side-Channel Attack

- Observe the **Power Consumption** of **computation**
- If the **Power Consumption** depends on a **cryptographic token**, the token can be leaked

## II. Power Analysis

### 1. Simple Power Analysis

- An attack consists of a **simple measurement** of the power consumption of computation over time

#### 1.1. Assumption

- Assuming **different bits of secret** can **cause** **different operations** to be **performed**, attackers can not only identify **secret values** basing on the **power consumption measurement** but also **identify different operations** of computation

#### 1.2. Disadvantage

- **Noisy measurement** make **direct identification of key bits** difficult
- **Limits** on the **frequency** of **measurements**
- **Visual analysis** is **difficult**

### 2. Differential Power Analysis

- Attackers **measure** different **power traces**, which **differ** in **one bit of secret**
- Then they use statistical methods to **reveal** bit

#### 2.1. Assumption

- **Power consumption** correlates with **intermediate result** of a **computation**
- **Intermediate result** correlated with **one bit of secret**
- **Precise measurement** of **power traces** need to **be possible**

### 3. Applications

- Identify the **location of HW** in the **computation**
- Identify the **cryptographic algorithm** that is **used** in the **device**
- **Attack symmetric ciphers** by observing **relationship** between **power consumption** and **secret bits**

## III. Countermeasures

### 1. Equalization

- Remove all **dependencies of control flow** on secret
- **Disadvantage**: expensive and might lose optimization

### 2. Randomization

- Randomize **dependency on secret** so that **power trace** is **randomized** while **performing same function**
- **Disadvantage**: might lose optimization

### 3. Masking

-  **Mask secrets** using **random values** and perform computation on **these** **masked values**
-  **Disadvantage**: 
  - Work with **linear operation** only
  - Problem with **non-linear** operation, **issues** arise during **de-masking**
  - Require **new algorithm**