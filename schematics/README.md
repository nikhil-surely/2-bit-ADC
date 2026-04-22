# 2-Bit Flash ADC – Behavior Analysis

## 🔷 Overview

A **2-bit Analog-to-Digital Converter (ADC)** converts a continuous analog input voltage into one of **four discrete digital levels**. This design uses a **flash ADC architecture**, which employs multiple comparators operating in parallel for fast conversion.

---

## 🔷 Circuit Behavior

### 1. Input and Reference Levels

* The input signal ( V_{in} ) is a time-varying analog voltage (e.g., sine wave).
* A resistor ladder generates **three fixed reference voltages**:

  * ( V_1 ) (lowest threshold)
  * ( V_2 ) (mid threshold)
  * ( V_3 ) (highest threshold)

These references divide the input range into **four regions**.

---

### 2. Comparator Operation

Three comparators are used:

* Comparator C1 compares ( V_{in} ) with ( V_1 )
* Comparator C2 compares ( V_{in} ) with ( V_2 )
* Comparator C3 compares ( V_{in} ) with ( V_3 )

Each comparator outputs:

* **HIGH (1)** if ( V_{in} > V_{ref} )
* **LOW (0)** if ( V_{in} < V_{ref} )

---

### 3. Thermometer Code Generation

As ( V_{in} ) increases, comparator outputs switch sequentially:

| Input Range            | C1 | C2 | C3 |
| ---------------------- | -- | -- | -- |
| ( V_{in} < V_1 )       | 0  | 0  | 0  |
| ( V_1 < V_{in} < V_2 ) | 1  | 0  | 0  |
| ( V_2 < V_{in} < V_3 ) | 1  | 1  | 0  |
| ( V_{in} > V_3 )       | 1  | 1  | 1  |

This pattern is called a **thermometer code**, where outputs turn ON progressively.

---

### 4. Binary Encoding

The thermometer code is converted into a **2-bit binary output**:

| C3 | C2 | C1 | Output (B1 B0) |
| -- | -- | -- | -------------- |
| 0  | 0  | 0  | 00             |
| 0  | 0  | 1  | 01             |
| 0  | 1  | 1  | 10             |
| 1  | 1  | 1  | 11             |

* **B1 (MSB)** represents the upper half of the range
* **B0 (LSB)** refines the level within that half

---

## 🔷 Output Characteristics

### 1. Staircase Transfer Function

The ADC produces a **step-like (quantized) output**:

* Continuous input → discrete output levels
* The output changes only when ( V_{in} ) crosses a threshold

---

### 2. Time-Domain Behavior

For a sinusoidal input:

* Comparator outputs switch at different times
* Final binary output forms a **quantized approximation** of the input
* MSB changes slowly, LSB changes more frequently

---

### 3. Quantization

The ADC cannot represent all input values exactly.

* Input range is divided into **4 levels**
* Each level corresponds to a voltage interval

---

## 🔷 Resolution

Resolution is the smallest detectable change in input voltage.

[
\text{Resolution} = \frac{V_{max} - V_{min}}{2^n}
]

For a 2-bit ADC:

[
2^2 = 4 \text{ levels}
]

Example (0–5 V range):

[
\text{Resolution} = \frac{5}{4} = 1.25\text{ V}
]

So:

* Each step = **1.25 V**
* Any change smaller than this is not distinguishable

---

## 🔷 Quantization Error

Since the output is discrete:

[
\text{Maximum error} = \pm \frac{\text{Resolution}}{2}
]

For this ADC:

* Max error = **±0.625 V**

---

## 🔷 Key Observations

* Flash ADC uses **parallel comparators → very fast**
* Output is a **quantized staircase approximation**
* Increasing number of bits improves accuracy
* Comparator instability (without hysteresis) can cause oscillations near thresholds

---

## 🔷 Conclusion

The 2-bit flash ADC successfully converts an analog input into one of four digital levels using parallel comparison. While simple and fast, its low resolution results in coarse approximation. Proper comparator design (e.g., hysteresis) is essential for stable operation.

---
