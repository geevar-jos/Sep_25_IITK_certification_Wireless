# Massive MIMO Receiver Performance Analysis

A Python-based simulation environment to evaluate the **achievable rate** of Massive MIMO systems. This project demonstrates how increasing the number of Base Station (BS) antennas impacts the performance of common **linear receivers**, especially under **power-scaling laws**.

---

## How Massive MIMO Works

**Massive MIMO (Multiple-Input Multiple-Output)** is a key technology for 5G and beyond. Unlike conventional MIMO (few antennas), Massive MIMO scales the number of BS antennas to **tens or hundreds** (denoted by **$M$**) to serve **multiple users** (denoted by **$K$**) simultaneously on the same time-frequency resource.

### Key Principles

1. **Channel Hardening**  
   As $M \to \infty$, random channel fluctuations average out and the channel behaves more like a deterministic link.

2. **Favorable Propagation**  
   With many antennas, channel vectors of different users become nearly **orthogonal**, allowing the BS to separate users with minimal interference using simple linear processing.

3. **Power Scaling**  
   Users can reduce transmit power significantly while maintaining high rates due to the large **array gain** from the antenna array.

---

## Linear Receivers Simulated

This project simulates two commonly used linear receivers for symbol estimation at the BS:

### 1) Maximal Ratio Combining (MRC)

**MRC** is the simplest linear receiver. It maximizes the SNR for each user without explicitly suppressing inter-user interference.

- **Mechanism:** Multiply the received signal by the conjugate of the user’s channel vector which is shown to maximise received SNR.
- **Massive MIMO Context:** Although MRC can suffer from strong inter-user interference in conventional systems, it becomes highly effective in Massive MIMO because user channels become nearly orthogonal as $M$ increases.
- **Analytical Bound:** The code includes an analytical bound for MRC, showing the rate converges to a predictable value as $M$ grows.

### 2) Zero Forcing (ZF)

**ZF** is a more advanced receiver that explicitly removes inter-user interference.

- **Mechanism:** Uses the pseudo-inverse of the channel matrix:
  \[
  G^\dagger = (G^H G)^{-1} G^H
  \]
- **Trade-off:** While ZF eliminates interference, it can **amplify noise**, especially when the channel matrix is ill-conditioned (e.g., small $M$ or correlated users).

---

## MRC vs ZF: What Changes in Massive MIMO?

ZF often provides higher rates in low-to-medium antenna regimes because it actively cancels interference.  
However, in Massive MIMO deployments, **MRC is frequently preferred** due to its simplicity and scalability.

| Feature | Maximal Ratio Combining (MRC) | Zero Forcing (ZF) |
|---|---|---|
| **Complexity** | Extremely low (per-user processing) | High (matrix inversion) |
| **Interference** | Ignored (naturally vanishes as $M$ grows) | Actively suppressed |
| **Noise** | Robust against noise | Can amplify noise at low SNR |
| **Scalability** | Easy to distribute | Harder to distribute (centralized inversion) |

### The “Massive” Advantage
When $M \gg K$, interference terms in MRC naturally vanish. This makes **simple, low-complexity MRC** perform nearly as well as (and in some low-SNR / power-scaling settings, sometimes better than) more complex methods like ZF.
