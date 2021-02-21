# Hardware Trojans

## Question

- What are HW Trojans?
- Which types of HW Trojans exist?
- How do HW Trojans look?
- How can HW Trojans be detected?

## I. What are HW Trojans?

### 1. Definition

- **Malicious modification** of **an integrated circuit** during its design flow which allows to add/remove functionality or reduce reliability.

### 2. Properties

- **Hidden** in Integrated Circuits
- **Silent** most of the time: activated by rare signals or events that do not arise during design simulation and testing
- **Activation** **mechanism** is a trigger
- **Malicious** **function** is a payload

<img src="/Users/vuong/Library/Application Support/typora-user-images/Screen Shot 2021-02-18 at 10.39.13 AM.png" alt="Screen Shot 2021-02-18 at 10.39.13 AM" style="zoom:50%;" />

### 3. Purposes

- **Extract Information**: personal data, encryption key, seed for PRNGs
- **Insert Information**: modified data, weak encryption key, seed for PRNGs, malware

### 4. Application Areas

- **Military products:** production of almost all chips is outsourced to third countries. HW Trojans can be implanted to military products of enemies as a spy
- **Critical Infrastructures**: HW Trojans can be implanted to critical infrastructure to cause damage in a cyber war
- **Consumer Electronics**: HW Trojans can be implanted to consumer electronics to spy consumers and compromise their privacy

### 5. Trojan insertion: Why does it work?

<!--Question: Why is the Trojan insertion difficult to detect?-->

- **Outsource** the ICs production
- Use the **3rd party patents** to design IC
- Use the **electronic design automation tool** to manage complexity
- **Difficult** to guarantee the **trust** of all **steps** in a **design** flow
- **Adding** small number of **gates** can introduce a **malicious circuitry** in the **design**

## II. Taxonomy of HW Trojans

### 1. Criteria

- **Insertion Phase**: insert Trojans at different phases
- **Abstraction Level**: insert Trojans at different design levels
- **Activation mechanisms**: how to activate Trojan
- **Effect of Trojans**
- **Location of the Trojan**
- **Physical characteristics of the Trojan**

### 2. Details

- **Criteria**: Insertion Phase
- **Categories:**
  - **Specification**: **weaken** specification intentionally to **limit** **security**/robustness
  - **Design**: use **untrustworthy** tools and libraries which allow Trojan insertion
  - **Fabrication**: untrustworthy **masks** during fabrication or change of physical characteristics
  - **Assembly and packaging**: addition of **malicious** component to package

- **Criteria**: Abstraction Level
- **Categories**:
  - **System**: change in specification/design can **weaken** system
  - **Development env**: untrustworthy tools and libraries can **change** design
  - **Gates**: addition/deletion of gates and changes of **timing** **behavior**
  - **Transistors**: changes of the size of transistor, dopants and wire

- **Criteria**: Activation Mechanisms
- **Categories**:
  - **Always on**: no special trigger and Trojan consists **payload** **only**
  - **Internal activation**: activated by internal conditions (timer, clock signal, loop)
  - **External activation**: activated by special input values or special ambient condition
- **Criteria**: Effect of Trojans
- **Categories**:
  - **Change the functionality**: invalid functions, wrong computation
  - **Degrade the performance**: reduce the availability of critical system
  - **Leak information**: such as personal information, keys
  - **Denial of service**: destroy system or kill switches
- **Criteria**: Location of Trojans
- **Categories**: 
  - Processor, memory, power supply, clock
  - Other components
- **Criteria**: Physical characteristics of Trojan
- **Categories**:
  - **Distribution**: location of Trojan in the IC
  - **Size**: the smaller Trojans, the harder to detect
  - **Structure**: Trojans may change the layout or not

## III. Categories of HW Trojans work

### 1. Categories

- Behavioral/functional Level
- Multiplexer
- Trojan insertion through **Malicious** design and **Synthesis** tools
- Physical Level with Dopant Trojans
- Gate Level: through Addition of Gate
- Gate Level: through Synchronous Counter
- Gate Level: through Asynchronous Counter
- Gate Level: through Hybrid Counter
- Gate Level Analog Triggers: triggered by Logic Values
- Gate Level Analog Triggers: triggered by Environmental conditions
- Gate Level Analog Triggers: triggered by Analog Payload

### 2. Details

- **Category**: Behavioral/functional Level
- **Work**: 
  - Code is written in high-level language. Payload is triggered by **conditions or a loop** inserted in the code
- **Category**: Multiplexer
- **Work**: 
  - At the gate level, multiplexer can be **tampered** by additional inputs which can change its behavior
- **Category**: Trojan insertion through Malicious design and synthesis tools
- **Work**: 
  - Tools add Trojan into design and **disable integrity** **checks**
- **Category**: Physical Level with Dopant Trojans
- **Work**: 
  - At the physical level, **transistors** can be tampered by their dopants
  - The wrong dopants can change transistors' function differently than expected
  - In such case, **denial of service** can be triggered or **security mechanism** can never be activated

#### 2.1. Gate Level

- **Category**: Gate Level through Addition of Gate
- **Work**:
  - Trigger is implemented by additional logic in such rare conditions that payload is rarely activated
- **Category**: Gate level through Synchronous Counter
- **Work**:
  - Called time-bomb
  - Counter triggers Trojan when counting up to a certain value
- **Category**: Gate Level through Asynchronous Counter
- **Work**:
  - Counter triggers Trojan when a certain condition arrivers at the counter
- **Category**: Gate Level through Hybrid Counter
- **Work**:
  - Counter triggers Trojan when a certain clock value is reached and a certain condition arrivers at the counter

#### 2.1. Gate Level Analog Triggers

- **Category**: Gate Level triggered based on logic values
- **Work**:
  - Trigger checks for condition among **various variables**
  - If condition is met repeatedly, a **capacitor** is charged which will trigger Trojan
- **Category**: Gate level triggered by Environmental conditions
- **Work**:
  - Sensor checks for environmental conditions.
  - If condition is met, it triggers the Trojan
- **Category**: Gate level triggered by Analog Payload
- **Work**:
  - Trojan payload can be Analog
  - Errors (short circuit) can be inserted intentionally into the system (connected wires to GND or VDD) which can break algorithm of circuit

## IV. Countermeasures

### 1. Disadvantages

Most methods:

- Assume a **particular** Trojan model
- Cannot **guarantee** detection - Only provide confidence level (==Reverse Engineering==)
- **Prone** to False Positive (==Blue Chip==)
- Lack of **resolution** to **outright** show Trojan location
- Have not been **validated** **experimentally** (only simulations, homebrew Trojans) (==IC finderprint==)
- Have **unacceptable** **overhead ** (==HW assisted functionality monitoring==)

### 2. Categories

- **Detection**:
  - **Determine** if any Trojans exist in the ICs
- **Diagnosis**:
  - **Distinguish** the Trojans in term of **type**, **location**, **characteristics**
- **Prevention**:
  - **Increase difficulty** to **insert** Trojans
  - **Enhance** the **efficiency** of detection & diagnosis methods
  - **Prevent** the successful trojan insertion during IC development and design

### 3. Methods

#### 3.1. Prevention during IC development and Design

- Eliminate **free space** in an IC to prevent Trojan insertion
- **Obfuscation** of circuit **functionality** to make it difficult for attackers to understand the logic
- **Disadvantage**:
  - Useless if attackers use better optimization, logic, placement techniques
  - The effectiveness of obfuscation depends on the expert of designer and the capability of attacker

#### 3.2. Reverse Engineering

- Use **sample manufactured ICs** to
  - perform **de-metallization** using **Chemical and Mechanical Polishing**
  - image **re-construction** and **analysis** using **Scanning Electron Microscope**
- **Disadvantage**:
  - Expensive and time consuming
  - Not scale well
  - Results can't be **extrapolated** to all ICs
  - **Adversary** might **affect** to only a **small number**

#### 3.3. Runtime Testing

- Implemented through **operation transparency** or **hardware assisted functionality monitoring**
- **Operation transparency** can be **enabled on demand** through a **key-based special mode** in order to test **rare events** or **heuristically identified cases**
- **Functionality monitoring** is the assistance of HW
  - **Dedicated HW** implements framework to monitor system at runtime
  - It will deploy countermeasure on **deviation**
- **Disadvantage**:
  - Cannot guarantee detection
  - HW ass. func. mon. has unacceptable overhead + **manufacturing cost**

#### 3.4. Blue Chip

- Identify **unused circuit portion** in the **design level**
- Insert HW to this area in order to **generate exception**
- If there is Trojan in this area, this HW will generate exception and deliver to SW layer to prevent the payload trigger
- **Disadvantage**:
  - **Difficult** to completely **predict** the **correct behavior** of ICs to prevent False Positive

#### 3.5. Logic Testing

- Based on **Multiple Excitation of Rare Occurrence Method**
- Enumerate rare nodes in a given netlist
- Excite potential Trojan trigger nodes multiple times to their rare values individually
- Generate a compact set of test vectors
- **Disadvantage**:
  - Assume a **particular** Trojan model
  - Cannot **guarantee** detection

#### 3.6. IC Fingerprinting

- **Signature** is created on the golden model, which indicates **the anticipated behavior HW-free Trojans**
- If an IC violates this model, a different signature will be generated which indicates IC is infected by Trojans
- Usually **path delay** or **power trace**, **supplemented** by de-noising techniques
- **Disadvantage**:
  - Have not been **validated** **experimentally** (only simulations)
  - No **actual measurement** and **real noise**

#### 3.7. Path Delay Fingerprinting

- Based on **Multiple paths** and **Extensive statistical characterization**
- Detects Trojans with 0.13% area, under 7.5% process variation
- **Disadvantage**:
  - Heavy computation for large IC

