# 2-Bit Flash ADC – Behaviour Analysis

---

## Circuit Behavior

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
