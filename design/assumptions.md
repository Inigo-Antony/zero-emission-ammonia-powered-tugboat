# Design Assumptions

This document lists all assumptions made in the ammonia-hydrogen fuel cell tugboat design.

## 1. System-Level Assumptions

| Assumption | Value | Justification |
|------------|-------|---------------|
| Net propulsion power | 1,000 kW (1 MW) | Based on Amogy NH₃ Kraken demonstration |
| Operational endurance | 12 hours | Typical harbour tugboat duty cycle |
| Tank safety margin | 15% | Industry standard for fuel reserves |
| Operating days per year | 250 days | Typical commercial operation |
| Hours per day | 12 hours | Full shift operation |
| Annual operating hours | 3,000 hours | 250 × 12 |

## 2. Fuel Cell System Assumptions

| Assumption | Value | Justification |
|------------|-------|---------------|
| FC module size | 200 kW | Ballard FCwave module specification |
| Number of modules | 10 | Sized for ~80% target utilisation |
| FC electrical efficiency | 50% | Typical PEM FC at rated power (LHV basis) |
| Operating temperature | ~80°C | Standard LT-PEM operating range |
| Operating pressure | ~2 bar | Low-pressure PEM operation |
| Cathode stoichiometry (λ_air) | 2.0 | Ensures adequate oxygen supply |

## 3. Anode Recirculation Assumptions

| Assumption | Value | Justification |
|------------|-------|---------------|
| Anode stoichiometry (λ) | 1.3 | Provides 30% excess H₂ at inlet |
| Fuel utilisation (U_f) | 85% | Balance between efficiency and purge rate |
| Recirculation mode | Continuous purge | Ensures stable combustor fuel supply |
| Anode inlet humidity | Humidified | Membrane humidifier included |

**Key relationships:**
- λ determines anode inlet flow: H₂_inlet = λ × H₂_consumed
- U_f determines fresh feed: H₂_fresh = H₂_consumed / U_f
- Constraint: λ × U_f > 1 (check: 1.3 × 0.85 = 1.105 ✓)

## 4. Ammonia Cracking Assumptions

| Assumption | Value | Justification |
|------------|-------|---------------|
| Cracker type | GHC + HAVAC (two-stage) | Based on Eluwah & Fennell (2024) |
| Catalyst | Ru/Al₂O₃ (Ruthenium) | High activity at moderate temperatures |
| GHC conversion | ~45% | Low-temperature first stage (~600°C) |
| Total conversion | 99.5% | High-temperature second stage (~700°C) |
| Reaction enthalpy | +46 kJ/mol NH₃ | Standard thermodynamic value |
| Heat losses | 10% of reaction heat | Typical reactor thermal losses |
| Operating mode | Autothermal | H₂ combustion provides heat |

## 5. Purification System Assumptions

| Assumption | Value | Justification |
|------------|-------|---------------|
| Molecular sieve NH₃ removal | >99.9% | Protects PSA and fuel cell |
| PSA H₂ recovery | 75% | Typical 4-bed PSA performance |
| PSA H₂ purity | 99.99% | Fuel cell grade requirement |
| PSA operating temperature | ~40°C | After product gas cooling |

## 6. Catalytic Combustor Assumptions

| Assumption | Value | Justification |
|------------|-------|---------------|
| Catalyst | Pt/Pd | Standard H₂ combustion catalyst |
| Burner efficiency | 90% | Heat transfer to cracker |
| Outlet temperature | ~800°C | High-grade heat for cracking |
| NOx emissions | <10 ppm | Catalytic combustion advantage |
| Fuel source | PSA tail gas + anode purge | Waste hydrogen streams |

## 7. Power Electronics Assumptions

| Assumption | Value | Justification |
|------------|-------|---------------|
| DC/DC converter efficiency | 97% | High-efficiency power electronics |
| Inverter efficiency | 95% | Standard marine inverter |
| Motor efficiency | 98% | High-efficiency AC induction motor |
| Battery round-trip efficiency | 95% | LiFePO₃ typical value |
| Battery capacity | 600 kWh | 20 min startup + margin |

## 8. Balance of Plant (BOP) Assumption

| Assumption | Value | Justification |
|------------|-------|---------------|
| **BOP fraction** | **30% of FC output** | Industry benchmark (25-35% range) |

**BOP breakdown (500 kW total):**

| Component | Power (kW) | % of BOP |
|-----------|------------|----------|
| Cathode air compressor | 200 | 40% |
| FC cooling system | 60 | 12% |
| PSA compression | 45 | 9% |
| Seawater pump | 40 | 8% |
| Miscellaneous | 40 | 8% |
| Electric trim heater | 30 | 6% |
| Combustion air blower | 30 | 6% |
| Process control | 30 | 6% |
| Anode recirculation | 15 | 3% |
| NH₃ handling | 10 | 2% |

## 9. Thermal Integration Assumptions

| Assumption | Value | Justification |
|------------|-------|---------------|
| FC waste heat for vaporiser | ~370 kW | NH₃ vaporisation duty |
| FC waste heat rejected | ~1,270 kW | Seawater cooling |
| Product gas cooling | 700°C → 40°C | Multi-stage HEX |
| Vaporiser inlet | -33°C (liquid NH₃) | Refrigerated storage |
| Vaporiser outlet | 25°C (gaseous NH₃) | Before cracker inlet |

## 10. Ammonia Storage Assumptions

| Assumption | Value | Justification |
|------------|-------|---------------|
| Storage condition | -33°C, 1 bar | Refrigerated atmospheric |
| Liquid density | 682 kg/m³ | At storage conditions |
| Tank type | Type C (IMO) | Marine pressure vessel |

## 11. Economic Assumptions

| Assumption | Value | Source |
|------------|-------|--------|
| Green ammonia price | $900/tonne | IMARC Group (2025) |
| Diesel price | $800/tonne | ECHEMI (2025) |
| Carbon price | $100/tonne CO₂ | World Bank Carbon Pricing Dashboard |
| Diesel consumption | 220 kg/h | Equivalent 1 MW diesel system |
| Other costs (maintenance, labour) | 10% of fuel + carbon | Simplified estimate |

## 12. Emission Factor Assumptions

| Fuel | CO₂ Factor | Source |
|------|------------|--------|
| Grey ammonia | 1.9 t CO₂/t NH₃ | Steam methane reforming |
| Blue ammonia | 0.2 t CO₂/t NH₃ | SMR + 90% CCS |
| Green ammonia | 0.0 t CO₂/t NH₃ | Electrolysis + renewables |
| Marine diesel | 3.2 t CO₂/t diesel | Standard combustion factor |

## 13. Simplifying Assumptions

The following simplifications were made for coursework scope:

1. **Component volume and weight**: Not calculated (would require detailed 3D layout)
2. **CAPEX**: Not included (expected to be significant for first-of-kind system)
3. **Transient behaviour**: Steady-state analysis only (startup sequence described qualitatively)
4. **Degradation**: Not modelled (FC capacity provides margin)
5. **Part-load efficiency**: Not calculated (full-load design point only)
6. **Detailed heat exchanger sizing**: Not performed (duties estimated)

## 14. Key References for Assumptions

1. **Eluwah & Fennell (2024)** - HAVAC cracker design, conversion efficiency, operating temperatures
2. **Amogy NH₃ Kraken (2024)** - 1 MW power target, 12-hour endurance, system architecture
3. **Steinberger et al. (2018)** - Anode recirculation strategies, λ and U_f values
4. **Ballard FCwave datasheet** - 200 kW module, 50% efficiency
5. **NIST Chemistry WebBook** - Reaction enthalpy (+46 kJ/mol)

## 15. Assumption Sensitivity

| Assumption | If Higher | If Lower |
|------------|-----------|----------|
| PSA recovery (75%) | Less H₂ to combustor, smaller margin | More NH₃ needed |
| FC efficiency (50%) | Less H₂ needed, higher system η | More NH₃ needed |
| BOP fraction (30%) | Lower system η, more H₂ waste | Higher system η |
| Fuel utilisation (85%) | Less purge, need dead-end mode | More H₂ to combustor |
| Cracker conversion (99.5%) | Less NH₃ slip | NH₃ in fuel cell (damage) |

---

