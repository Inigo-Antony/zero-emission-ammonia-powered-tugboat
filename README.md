# Ammonia-Hydrogen Fuel Cell Tugboat Design

[![Python 3.8+](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/downloads/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

A thermodynamic and economic analysis tool for designing zero-emission ammonia-powered marine propulsion systems using PEM fuel cells.

![System Block Diagram](diagrams/system_block_diagram.png)

## Overview

This project presents the design of a **1 MW zero-emission tugboat propulsion system** using ammonia as a hydrogen carrier. The system converts liquid ammonia to electrical power through on-board cracking and PEM fuel cells, achieving true zero-emission operation suitable for harbour environments.

### Key Features

- **Autothermal Operation**: Waste hydrogen from PSA tail gas and anode purge provides cracking heat
- **Anode Recirculation**: Continuous purge mode ensures stable combustor operation (85% fuel utilisation)
- **Complete Mass & Energy Balance**: Rigorous thermodynamic calculations with validation checks
- **Economic Analysis**: OPEX comparison with diesel baseline including carbon pricing

## Design Specifications

| Parameter | Value | Notes |
|-----------|-------|-------|
| Net propulsion power | 1,000 kW | At propeller shaft |
| Operational endurance | 12 hours | Without refuelling |
| Fuel cell capacity | 2,000 kW | 10 × 200 kW modules |
| FC gross output | 1,660 kW | At design point |
| FC utilisation | 83% | Margin for degradation |
| Balance of Plant | 500 kW | 30% of FC output |
| NH₃ consumption | 890 kg/h | At full power |
| System efficiency | 23% | LHV basis |
| Tank capacity | ~13 tonnes | 12h + 15% margin |
| Local emissions | Zero | CO₂, SOx, PM |

## Installation

```bash
# Clone the repository
git clone https://github.com/Inigo-Antony/zero-emission-ammonia-powered-tugboat.git
cd zero-emission-ammonia-powered-tugboat

# Run the calculator (no dependencies required)
python src/tugboat_calculator.py
```

## Results Summary

### Power Chain (Table 2)

| Component | Efficiency | Output (kW) | Input (kW) |
|-----------|------------|-------------|------------|
| Propeller shaft | — | 1,000 | — |
| Electric motor | 98% | 1,000 | 1,020 |
| Inverter | 95% | 1,020 | 1,074 |
| Battery (+50 kW) | — | 1,074 | 1,124 |
| DC/DC converter | 97% | 1,124 | 1,160 |
| Balance of Plant (30%) | — | — | +500 |
| **FC gross output** | — | — | **1,660** |

### Hydrogen Mass Balance (Tables 3, 4)

| Parameter | Value |
|-----------|-------|
| Fresh H₂ feed (from PSA) | 117.2 kg/h |
| Recycled H₂ (from anode) | 12.3 kg/h |
| H₂ at anode inlet (λ=1.3) | 129.5 kg/h |
| H₂ consumed (reaction) | 99.6 kg/h |
| Anode exhaust | 29.9 kg/h |
| Continuous purge to burner | 17.5 kg/h |

### Autothermal Heat Balance (Table 5)

| Parameter | Value |
|-----------|-------|
| H₂ to combustor (PSA tail + anode purge) | 56.5 kg/h |
| Combustion energy (LHV) | 1,883 kW |
| Heat available (90% burner efficiency) | 1,695 kW |
| Cracker heat requirement (reaction) | 668 kW |
| Heat losses (~10%) | 67 kW |
| **Surplus heat** | **960 kW** |

### Energy Balance (Table 6)

| Energy Stream | Power (kW) | Percentage |
|--------------|------------|------------|
| **Input: NH₃ (LHV)** | **4,600** | **100%** |
| Propulsion + Battery | 1,050 | 22.8% |
| FC Waste Heat | 1,660 | 36.1% |
| Combustor Excess Heat | 983 | 21.4% |
| Electronics Losses | 88 | 1.9% |
| Exhaust and Other | 819 | 17.8% |
| **Total Output** | **4,600** | **100%** |

### System Efficiency (Section 3.9)

```
η_system = P_useful / E_input = 1,050 / 4,600 = 22.8% ≈ 23%
```

### Economic Comparison (Table 7)

| Cost Component | Green NH₃ | Diesel Baseline |
|----------------|-----------|-----------------|
| Fuel cost | $2,400,000 | $528,000 |
| Carbon cost | $0 | $211,000 |
| Other costs (10%) | $240,000 | $74,000 |
| **Total OPEX** | **$2,640,000** | **$813,000** |
| **Premium** | **3.25×** | baseline |

### Lifecycle Emissions (Table 8)

| Fuel Pathway | CO₂ (t/yr) | vs Diesel |
|--------------|------------|-----------|
| Diesel (baseline) | 2,110 | — |
| Grey NH₃ (@1.9) | 5,070 | +141% |
| Blue NH₃ (@0.2) | 534 | -75% |
| **Green NH₃** | **0** | **-100%** |

## Project Structure

```
zero-emission-ammonia-powered-tugboat/
├── README.md
├── LICENSE
├── requirements.txt
├── src/
│   ├── __init__.py
│   └── tugboat_calculator.py
├── design/
│   └── design_methodology.md
│   └── assumptions.md
├── diagrams/
│   └── system_block_diagram.png
├── results/
│   └── sample_output.txt
└── design-report/
    └── Zero-Emission-Ammonia_Tugboat-Power-System-Design.pdf
```

## References

1. Eluwah, C. & Fennell, P.S. (2024). Hybrid Air-Volt Ammonia Cracker (HAVAC) process. *Energy Advances*, 3(10), 2627-2647.
2. Amogy (2024). NH₃ Kraken Tugboat Demonstration.

## License

MIT License - see [LICENSE](LICENSE)

## Author

**Inigo** - MSc Sustainable Energy Systems, University of Birmingham and IIT Madras

*Originally developed as part of MSc coursework and further refined independently*
