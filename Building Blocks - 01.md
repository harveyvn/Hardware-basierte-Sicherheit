# Random Number Generation

## Questions:

1. What does **randomness** mean?
2. What are **random values** used for?
3. **How** can random values be **generated**?
4. **How** can the **quality** of random values be **determined**?

## I. The concept of randomness and its applications

### 1. Randomness

- Randomness is the impossibility to determine the **precise and individual** **outcome** of an event using a model, due to **the nature of model itself** and **the lack of model parameters**.

- Implications of randomness to the concepts **Uniformity** and **Independence** of event
  - Uniformity: individual options must be equally probable.
  - Independence: the occurrence of one option must be independent of the occurrence of another option.
- In an **algorithmic definition**, randomness of seq. is the size of smallest Turing machine that generates the sequence. It is called Kolmogorov complexity.

### 2. Randomness in cryptography

- In a cryptographic definition, randomness can prevent attackers from predicting **the outcome of an encryption**. By using as nonce or one-time pads, it can prevent an attack.
- Attackers win or the attack is successful if he can predict the next bits with probability greater than 50%.

## II. Pseudorandom vs. True number generators

- **Pseudorandom number generators** are based on algorithm through a deterministic process.
  - <u>Advantages</u>: Fast
  - <u>Disadvantages</u>: Numbers are not truly random.
    - Attackers get the knowledge of the used Algorithm, so he can predict numbers.
    - The state space of Algorithm is limit, so the output will repeat.
- **True random number generators** are based on physical processes.
  - <u>Advantages</u>: Numbers are truly random.
  - <u>Disadvantages</u>: Process takes time and sometimes requires additional hardware.
  - <u>Example</u>: coins, cards, dice ...
- **Solution - Hybrid approach**:
  - TRNG generates seed.
  - PRNG expands seed to full random numbers.

## III. Pseudorandom number generators

### 1. PRNG Properties

- **Uncorrelated sequences**: seqs. should be serially uncorrelated.
- **Uniformity**: a seq. of random numbers should be uniform
- **Long period**: a generator should be of long period
- **Practicability**:
  - Replicability: for verification and debugging
  - Efficiency: Numbers should be computed efficiently
  - Portability: Work on different architectures and OS

### 2. Dedicated constructions

#### 2.1 Middle-Square Method

- The random number list can converge to 0.
- The random number list can get stuck, likely with zero but also other numbers.
- The random number list can get into short loops.
- Maximal length $8^n$

#### 2.2 Congruential Generators

- If m = 2, the random number list can converge to  $c\mod2$, 1 or 0.
- $x_{n+1} = (ax_n + c) \mod m$ 
- Condition:
  - $a = 4b+1$
  - $c = odd$
  - $m = 2^k$
  - $b, c, k > 0$

### 3. Cryptographic constructions

#### 3.1 Required properties

- The output of PRNGs should be indistinguishable from random output
- Uniformity: the probability of the next bits must be equally probable
- Consistency: the occurrence of one bit must be independent of the occurrence of another bit
- Unpredictability: it is difficult to predict next bit ==(test by Next-bit test)==
- Forward security: given a state of generator, it is hard to predict the prev. outputs. ==(see Backtracking attack)==

#### 3.2 Blum-Blum-Shub

- **Process:**
  - Initialization:
    - $p$ and $q$ are 2 prime number.  $n = p * q$ 
    - Seed $x_0$
  - Random bit generation:
    - $i^{th}$ state = $x_{n+1} = x_{n}^2 \mod n$
    - $i^{th}$ bit = take least significant bit x~i~  ($odd = 1$ $even= 0$)

- **Disadvantages:**
  - Slow because large prime numbers are used and one multiplication per random bit.
  - Good for key generation, bad for cryptographic applications.
- **Solution:**
  - Block cipher can encrypt large blocks of data quickly.
  - Block cipher can generate a large blocks fo pseudo number quickly in sequential manner.

### 4. PRNG Attacks

- **Direct Cryptanalytic Attack**: attackers distinguish between output of PRNG and random number to cryptanalyse the PRNG.
- **Input Based Attack**: attackers use knowledge and control of PRNG input to cryptanalyse^(giaima)^ to PRNG.
  - Known input
  - Chosen input
  - Replayed input
- **State Compromise Extension Attacks**: attackers rely on a breach of security to guess state information.
  - **Backtracking attack**: use the compromised state $S$ of PRNGs to predict prev. outputs. ==(see Forward Security property)==
  - **Permanent compromise attack**: use the compromised state $S$ of PRNGs to predict past and future outputs
  - **Iterative guessing attack**: use the compromised state $S$ of PRNGs at time $t$ and the intervening output of PRNGs to guess the state $S'$ at time $t+\Delta$ 
  - **Meet-in-the-middle attack**: backtracking + iterative guessing attack

## IV. True Random Number Generators

![Screen Shot 2021-02-16 at 8.39.08 PM](/Users/vuong/Library/Application Support/typora-user-images/Screen Shot 2021-02-16 at 8.39.08 PM.png)



### 1. TRNG Post-processing

- **Require** when the physical randomness sources of TRNG introduces **some imperfections**:
  - Implementation errors
  - Contain non-ideal components
  - Introduce correlation
- Post-processing methods remove bias in random sequence.

#### 1.1 Von Neumann Correction

- **Idea** if 0 and 1 have different probabilities.
  - `01 and 10` have equal probability. `11 and 00` have different probability are discarded.
  - Always collect 2 random bits
  - Discard if they are identical
  - Else use the first bit
- **Disadvantage**: significantly reduce the number of bits we can use.
- **Example**:
  - Sequence: 10 10 11 00 01 01 10
  - Output:       1   1              0    0   1

#### 1.2 Parity-based Sampling

- **Idea** is to divide input into **n-bit chunks**
- For each chunk, **a single parity bit** is calculated, then the chunk is **discarded**
- **Output**: n-bit XOR of all the bits of the chunk
- **Disadvantage**: significantly reduce the number of bits we can use to 1/n of the number of the input bits.

#### 1.3 Universal hashing

- Hash functions turn **an arbitrary sized input** into **a fixed-length random output**
- Hash functions chop and mix (substitute and transpose) data to create a new number as output
- A good hash function introduces **few collisions** which is difficult to find data with same hash value
- This method is fully **algebraic**, with no memory of previously hashed data
- **Decimation** rate can be controlled
- **Disadvantage**: Heavy computation due to lots of different operations.

