# Architectural Overview  
*(Technical Teaser – Implementation Details Withheld)*

This document describes the four functional layers of the decoupled TMR thermal control architecture at a conceptual level. Specific component identities, exact component values, Boolean expressions, and truth tables are intentionally omitted and available only upon formal request.

## 1. Isolated Sensing Front-End

**Purpose:** Acquire temperature information from three independent sensors while preventing electrical interaction between channels.

**Key Capability:** High-impedance isolation ensures that a fault (open, short, or impedance change) in any single sensing path cannot load or corrupt the remaining channels. This eliminates a common single-point failure mode found in paralleled or low-impedance sensor networks.

## 2. Majority Decision Matrix

**Purpose:** Produce a single, deterministic control decision from the three conditioned sensor channels.

**Key Capability:** Implements a classical 2-out-of-3 voting principle. A single channel producing an incorrect binary state is automatically out-voted by the agreeing pair, preserving continuous system operation without software intervention.

## 3. Predictive Diagnostic Loop

**Purpose:** Detect progressive sensor degradation *before* the majority voter silently masks it.

**Key Capability:** Continuously forms a dynamic group-average reference from the three isolated channels and evaluates each channel against that reference. When a channel’s deviation exceeds a configurable proportionality window, a localized degradation alert is raised. The primary voting path remains undisturbed.

This transforms the architecture from a pure “masking” system into one that supports proactive maintenance.

## 4. Supervisory Safety Latch

**Purpose:** Provide an autonomous, hardware-enforced Master-Off capability under extreme global conditions (e.g., thermal runaway affecting the group average).

**Key Capability:** An edge-triggered latch captures a critical threshold event and forces the final actuation signal into a safe state regardless of the majority voter output. Clearing the lockout requires deliberate manual intervention, preventing automatic re-energization after a severe fault.

## Layer Interaction Summary

```
Sensors → Isolated Front-End → ┬→ Majority Decision Matrix →┬→ Safety Latch → Actuation
                               │                           │
                               └→ Predictive Diagnostic ───┘
                                      (Alert only)
```

The diagnostic path runs in parallel and never overrides the primary control decision except through the independent safety latch under critical conditions.

## Design Principles Emphasized

- Electrical decoupling between redundant channels  
- Separation of “masking” and “detection” functions  
- Hardware-only critical safety path (no software dependency for the final override)  
- Explicit support for repairable redundancy via early degradation visibility  

Full schematic diagrams, component selections, and discrete logic realizations remain proprietary and are released only under controlled access agreements.
