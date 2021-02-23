# Convert Channels

## I. Convert Channels

### 1. Definition

- **Communication Paths** that are **neither designed nor intended** to **transfer information** between **system processes**

### 2. Examples

- **Storage-based** Convert Channel: high process encodes classified info. to **file metadata**
- **Timing-based** Convert Channel: high process encodes classified info. to **CPU loads**

### 3. Side Channels vs Convert Channels

#### 3.1. Side Channels

- **Un**intentional Leakage
- Electromagnetic Emanation/Power Consumption correlates with a computation

#### 3.2. Convert Channels

- **In**tentional Leakage
- Convert Channels can **encode and embed** data into **Side Channels Emanation**
- **Binary payload** will be **encoded** into **distinct computation** to generate **distinct** EE/PC

### 4. Generic Attack Scenario

#### 4.1. Transmitter

- **Isolated** from Receiver - **high level** security
- **Contain** sensitive Data to be **extracted**
- **Infected** by attacker's code
- Attacker's code can **encode** data and **transmit** via Convert Channel

#### 4.2. Receiver

- **Isolated** from Transmitter - **low level** security
- **Controlled** by attacker's code
- **Monitor** Convert Channel to **capture** Signal's **Preamble**
- **Decode** Payload

![Screen Shot 2021-02-23 at 11.52.52 AM](/Users/vuong/Library/Application Support/typora-user-images/Screen Shot 2021-02-23 at 11.52.52 AM.png)

## II. Types and Properties of Covert Channels

### 1. Physical / Out-of-Band

- Use a **shared physical medium**
- **Example**:
  - **Acoustic**: Ultrasonic Wave $\rightarrow$ Microphone
  - **Radio & Electromagnetic**: Electromagnetic Emanation $\rightarrow$ EM Antena
  - **Optical**: LED Camera

### 2. Software / Micro-architectural

- Use a **shared system resources**
- **Example:**
  - **Exploit** **differences** between **access** to **cached** and **non-cached** memory
  - **Speculative** execution attack

### 3. Network

- Use **traditional network** as a **share medium**
- **Example:**
  - **Modify** custom TCP/IP headers, fileds, timestamps
  - Modify **Package transmission rate**

