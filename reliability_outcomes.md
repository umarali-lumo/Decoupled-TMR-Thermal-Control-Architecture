# Reliability & Availability Outcomes  
*(Technical Teaser – Detailed Derivations Withheld)*

This document summarizes the quantified performance advantages of the proposed architecture. Full step-by-step mathematical derivations, complete Markov chain solutions, and experimental raw data sets are available only upon formal request.

## Classical TMR Reliability Baseline

The sensing layer retains the well-known 2-out-of-3 reliability expression:

$$R_{\text{TMR}} = 3R^{2} - 2R^{3}$$

Illustrative numerical gains:

| Single-Channel Reliability ($R$) | Resulting $R_{\text{TMR}}$ | Relative Improvement |
| :--- | :--- | :--- |
| 0.90 | 0.972 | +8.0% |
| 0.95 | 0.993 | +4.5% |
| 0.99 | 0.9997 | +0.9% |

## MTTF Paradox (Clarified)

Under constant failure rate $\lambda$:

- **Single sensor MTTF** = $\frac{1}{\lambda}$
- **Classical TMR MTTF** = $\frac{5}{6\lambda}$

Although absolute mean lifetime is reduced, mission reliability $R(t)$ is superior for all mission durations shorter than the crossover point $t = \frac{\ln(2)}{\lambda}$. This is the regime relevant to most safety-critical thermal-control missions.

## Diagnostic Contribution – From MTTF to MTBF

By introducing an explicit **degraded-but-still-functional** state (detected by the predictive loop), the architecture becomes repairable. Early visibility of degradation allows maintenance to restore full redundancy before a second failure occurs. Steady-state availability therefore exceeds that of pure masking TMR:

$$A_{\text{proposed}} > A_{\text{classical TMR}}$$

## Quantified Safety Metrics (Experimental Summary)

| Metric | Value | Notes |
| :--- | :--- | :--- |
| Fault Coverage (injected faults) | 97% ± 3.4% | Includes drift, open, and short conditions |
| False-Positive Rate | 0.8% ± 0.55% | Measured over 1,000 fault-free cycles |
| Diagnostic Latency | 250 ms ± 14 ms | Time from fault injection to alert |
| Risk Reduction Factor (RRF) | $\approx 209\times$ | Unannounced secondary failure probability |

The Risk Reduction Factor is computed by comparing the probability of an unannounced second failure under classical silent masking versus the proposed architecture with a representative short repair window.

## Comparative Snapshot

| Capability | Classical TMR | Proposed Framework |
| :--- | :--- | :--- |
| Single-fault masking | Yes | Yes |
| Early degradation visibility | No | Yes |
| Proactive maintenance support | No | Yes |
| Hardware-enforced critical off | Typically no | Yes |
| Availability under repair | Limited | Materially improved |

Exact transition-rate equations, confidence-interval calculations, and Monte-Carlo validation data remain part of the confidential technical package.
