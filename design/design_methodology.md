# Design Methodology

## Overview

This document describes the backward-calculation methodology used to size the ammonia-hydrogen fuel cell propulsion system. Starting from the fixed output requirement (1,000 kW propulsion), we work upstream through each subsystem to determine component sizes.

## 1. Power Chain Sizing (Table 2)

### Calculation Steps

| Step | Component | Efficiency | Calculation | Result |
|------|-----------|------------|-------------|--------|
| 1 | Propeller shaft | — | Fixed target | 1,000 kW |
| 2 | Electric motor | 98% | 1,000 / 0.98 | 1,020 kW |
| 3 | Inverter | 95% | 1,020 / 0.95 | 1,074 kW |
| 4 | DC bus | — | + 50 kW battery | 1,124 kW |
| 5 | DC/DC converter | 97% | 1,124 / 0.97 | 1,160 kW |
| 6 | BOP (30%) | — | P_fc × 0.30 | +500 kW |
| 7 | **FC gross output** | — | **Total** | **1,660 kW** |

### BOP Derivation

```
P_fc = P_dcdc / (1 - BOP_fraction) = 1,160 / 0.70 = 1,657 kW ≈ 1,660 kW
BOP = 0.30 × 1,660 = 498 kW ≈ 500 kW
```

### Fuel Cell Sizing

```
FC capacity = P_fc / target_utilisation = 1,660 / 0.80 = 2,075 kW
Rounded to: 10 modules × 200 kW = 2,000 kW
Actual utilisation: 1,660 / 2,000 = 83%
```

## 2. Hydrogen Mass Balance (Tables 3, 4)

### Fuel Cell Consumption

```
ṁ_H2_consumed = P_fc / (η_fc × LHV_H2)
              = 1,660 / (0.50 × 33.33)
              = 99.6 kg/h
```

### Anode Recirculation

| Stream | Calculation | Flow (kg/h) |
|--------|-------------|-------------|
| H₂ consumed | From above | 99.6 |
| H₂ at anode inlet | λ × consumed = 1.3 × 99.6 | 129.5 |
| Fresh H₂ (from PSA) | consumed / U_f = 99.6 / 0.85 | 117.2 |
| Recycled H₂ | inlet - fresh | 12.3 |
| Anode exhaust | inlet - consumed | 29.9 |
| Purge to combustor | exhaust - recycled | 17.5 |

### PSA Balance

```
H₂ from cracker = 117.2 / 0.75 = 156.2 kg/h
H₂ in PSA tail = 156.2 - 117.2 = 39.0 kg/h → combustor
Total to combustor = 39.0 + 17.5 = 56.5 kg/h
```

## 3. Ammonia Feed Rate (Section 3.3)

### Stoichiometry

```
2NH₃ → 3H₂ + N₂
H₂ yield = (3 × 2.016) / (2 × 17.03) = 0.1776 kg H₂/kg NH₃
```

### Calculation

```
ṁ_NH3 = ṁ_H2_cracker / (yield × conversion)
      = 156.2 / (0.1776 × 0.995)
      = 884 kg/h ≈ 890 kg/h
```

## 4. Autothermal Heat Balance (Table 5)

### Heat Required

```
ΔH = +46 kJ/mol NH₃ (endothermic)
ṅ_NH3 = 890,000 / 17.03 = 52,260 mol/h
Q_reaction = 52,260 × 46 / 3,600 = 668 kW
Q_losses = 668 × 0.10 = 67 kW
Q_required = 735 kW
```

### Heat Available

```
Q_combustion = 56.5 × 33.33 × 0.90 = 1,695 kW
Surplus = 1,695 - 735 = 960 kW (2.3× margin)
```

## 5. Energy Balance (Table 6)

| Stream | Power (kW) | % |
|--------|------------|---|
| **INPUT: NH₃ (LHV)** | **4,600** | **100%** |
| Propulsion + Battery | 1,050 | 22.8% |
| FC waste heat | 1,660 | 36.1% |
| Combustor excess | 983 | 21.4% |
| Electronics losses | 88 | 1.9% |
| Other losses | 819 | 17.8% |
| **TOTAL OUTPUT** | **4,600** | **100%** |

## 6. System Efficiency (Section 3.9)

```
η_system = P_useful / E_input = 1,050 / 4,600 = 22.8% ≈ 23%
```

## References

1. Eluwah & Fennell (2024). HAVAC process. Energy Advances.
2. Amogy NH₃ Kraken tugboat demonstration (2024).
