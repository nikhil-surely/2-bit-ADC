## Resolution

Resolution is the smallest detectable change in input voltage.

[
Resolution = (Vmax − Vmin) / (2ⁿ)
]

For a 2-bit ADC:

2² = 4 levels

Example (0–5 V range):

[
Resolution = 5 ÷ 4 = 1.25 V
]

So:

* Each step = **1.25 V**
* Any change smaller than this is not distinguishable

---

## Quantization Error

Since the output is discrete:

[
Maximum error <= Resolution / 2
]

For this ADC:

* Max error = **±0.625 V**

---

## Key Observations

* Flash ADC uses **parallel comparators → very fast**
* Output is a **quantized staircase approximation**
* Increasing number of bits improves accuracy
* Comparator instability (without hysteresis) can cause oscillations near thresholds

---
