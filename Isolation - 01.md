# Covert Channels

## I. Covert Channels

### 1. Definition

- **Communication Paths** that were **neither designed nor intended** to **transfer information** between **system processes**

### 2. Examples

- **Storage-based** Covert Channel: high process encodes classified info. to **file metadata**
- **Timing-based** Covert Channel: high process encodes classified info. to **CPU loads**

### 3. Side Channels vs Covert Channels

#### 3.1. Side Channels

- **Un**intentional Leakage
- Electromagnetic Emanation/Power Consumption correlates with a computation

#### 3.2. Covert Channels

- **In**tentional Leakage
- Covert Channels can **encode and embed** data into **Side Channels Emanation**
- **Binary payload** will be **encoded** into **distinct computation** to generate **distinct** EE/PC

### 4. Generic Attack Scenario

#### 4.1. Transmitter

- **Isolated** from Receiver - **high level** security
- **Contain** sensitive Data to be **extracted**
- **Infected** by attacker's code
- Attacker's code can **encode** data and **transmit** via Covert Channel

#### 4.2. Receiver

- **Isolated** from Transmitter - **low level** security
- **Controlled** by attacker's code
- **Monitor** Covert Channel to **capture** Signal's **Preamble**
- **Decode** Payload

![Screen Shot 2021-02-23 at 11.52.52 AM](Screen Shot 2021-02-23 at 11.52.52 AM.png)

## II. Types of Covert Channels

### 1. Physical / Out-of-Band

- Use a **shared physical medium**
- **Example**:
  - **Acoustic**: Ultrasonic Wave $\rightarrow$ Microphone
  - **Radio & Electromagnetic**: Emanation from Electronic components $\rightarrow$ EM Antena
  - **Optical**: LED $\rightarrow$ Camera

### 2. Software / Micro-architectural

- Use a **shared system resources**
- **Example:**
  - **Exploit** **differences** between **access** to **cached** and **non-cached** memory
  - **Speculative** execution attack

### 3. Network

- Use **traditional network** as a **shared medium**
- **Example:**
  - **Modify** custom TCP/IP headers, fields, timestamps
  - Modify **Package transmission rate**

## III. Properties of Covert Channels

### 1. Signal-to-Noise Ratio

- **Transmission** can be **affected** by **internal/external noise**
- **Error-correcting code** can correct transmission error
- $SNR = 10*log (\frac{P_{signal}}{P_{noise}}) dB$

### 2. Modulation Scheme

- **Define** how **binary payload** is **modulated** into the **channel’s signal**
- Example: **Amplitude**-Shift Keying, **Frequency**-Shift Keying

### 3. Capacity

- **Depend** on the **channel characteristics** and **modulation scheme**
- $Capacity = Bandwidth * log_2(1 + SNR)$

### 4. Covertness

- **Imperceptible** to **humans present** in the **environment**
- **Covert** to **adversary aware** of the **channel and modulation**

## IV. Applications of Covert Channels

### 1. Data Exfiltration

- **Extract sensitive data** from **an isolated machine** **without** use of **traditional communication channel**

### 2. Inter-process Covert Channels

- **Communication** between **two processes on same machine**, logically **isolated** by the **OS**

### 3. Cross-device Tracking

- User’s device **receive covert signals** from **another device**, they might be **located near each other** and likely **belong to the same user**

### 4. Location Tracking

- Use **Ultrasonic Covert Channels** to establish **Location Tracking**

### 5. Web Tracking

- Use covert channel to **transmit web session ID** from **isolated web page** to **another** webpage

## V. Countermeasures

### 1. Disadvantages





