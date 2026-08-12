# STOL Aircraft Optimization Trade Study

## Overview
This project develops a MATLAB-based preliminary design and optimization framework for a Short Takeoff and Landing (STOL) aircraft. The study evaluates a large design space of aircraft configurations by varying wing area, aspect ratio, engine power, and flap configuration. Each configuration is evaluated using analytical aircraft performance models, screened against defined design requirements, and ranked using a weighted decision matrix. The objective is to identify an aircraft configuration capable of achieving strong short-field performance while maintaining acceptable climb, cruise, weight, and dimensional characteristics. The Aviat Husky A-1C is used as the baseline aircraft for the study.

---

## Project Objectives
- Develop a modular MATLAB framework for preliminary STOL aircraft design
- Evaluate the effects of wing area, aspect ratio, engine power, and flap configuration
- Predict key aircraft performance characteristics
- Evaluate configurations against defined design constraints
- Rank feasible configurations using a weighted decision matrix
- Identify Pareto-optimal aircraft configurations
- Perform sensitivity analysis to evaluate the robustness of the design selection
- Determine an optimal STOL configuration based on the defined performance criteria

---

## Design Variabels
The primary design variables investigated are:
| Design Variable | Range |
|---|---:|
| Wing Area | 165-220 ft² |
| Aspect Ratio | 6.00-9.00 |
| Engine Power | 160-220 hp |
| Flap Configuration | Plain, Slotted, Fowler |

The resulting design space contains **3,276 aircraft configurations**.

---

## Performance Models
Each configuration is evaluated using analytical performance models for:

### Stall Speed
The stall speed is calculated from aircraft weight, wing area, air density, and maximum lift coefficient.

$$ V_s = \sqrt{\frac{2W}{\rho S C_{L_{\max}}}} $$
