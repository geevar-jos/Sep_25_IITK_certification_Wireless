# MIMO Receiver and Capacity Analysis (MATLAB)

This repository contains MATLAB codes for analyzing **MIMO receiver performance** and **MIMO capacity optimization**. The focus is on understanding how different linear receivers behave across SNR regimes and how intelligent power allocation improves MIMO capacity.

---

## Overview

The MATLAB code is divided into two main themes:

1. **Receiver-side processing**  
   Performance comparison of **Zero Forcing (ZF)** and **Linear MMSE (LMMSE)** receivers in terms of BER in Project_03.

2. **Transmitter-side optimization**  
   Capacity comparison between **equal power allocation** and **optimal (water-filling) power allocation** in MIMO systems in Project_04.

---

## Receiver Performance: ZF vs LMMSE

The receiver-related scripts simulate a Rayleigh fading MIMO system with digital modulation (in this case, QPSK) and evaluate **BER versus SNR**.

### Key Observations

- **Low SNR regime**
  - ZF suffers from significant noise amplification due to channel inversion.
  - LMMSE introduces regularization, reducing noise enhancement.
  - As a result, **LMMSE achieves lower BER than ZF at low SNR**.

- **High SNR regime**
  - Noise becomes negligible compared to signal power.
  - The LMMSE regularization term effectively vanishes.
  - **LMMSE converges to ZF**, and both receivers exhibit nearly identical performance.

### Takeaway
LMMSE provides a robust trade-off between interference suppression and noise resilience, making it preferable in practical systems operating over a wide SNR range.

---

## MIMO Capacity and Power Allocation

The capacity-related scripts evaluate the achievable rate of a MIMO channel under different transmit power allocation strategies.

### Equal Power Allocation

- Power is distributed uniformly across all transmit streams.
- Simple to implement but inefficient when channel gains vary.
- Power is wasted on weak spatial modes.

### Water-Filling (Optimal Power Allocation)

- Power is allocated based on channel strength.
- Strong eigenmodes receive more power, while weak modes may receive little or none.
- This strategy **maximizes achievable MIMO capacity** under a total transmit power constraint of the Base Station (BS).

### Key Observation

- Across all SNR values, **water-filling consistently achieves higher capacity** than equal power allocation.
- The performance gap becomes more pronounced when channel singular values are highly unequal.

---

## File Summary

- **`Project_03_ZF_MMSE_Receiver.m`**  
  BER comparison of ZF and LMMSE receivers.

- **`Project_04_MATLAB_MIMO_Optimization.m`**  
  Capacity comparison of equal power vs water-filling allocation.

- **`OPT_CAP_MIMO.m`**  
  Implements optimal (water-filling) capacity computation.

- **`EQ_CAP_MIMO.m`**  
  Implements equal power capacity computation.

- **`mimo_capacity.m`**  
  Generic utility for computing MIMO capacity.

---

## Conclusion

- LMMSE outperforms ZF at low SNR due to reduced noise amplification.
- LMMSE naturally converges to ZF at high SNR.
- Water-filling is the optimal power allocation strategy for maximizing MIMO capacity.
- Simple linear receivers and power allocation strategies can approach optimal performance when used in the right operating regimes.

---
