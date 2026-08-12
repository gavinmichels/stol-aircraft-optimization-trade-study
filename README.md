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

## Design Variables
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

### Takeoff Ground Roll
The takeoff ground roll is calculated using a velocity-stepped force balance from brake release to liftoff.

The model accounts for:
- Lift
- Aerodynamic drag
- Propulsive force
- Rolling resistance
- Aircraft mass
- Increasing lift coefficient during the ground roll

### Takeoff Distance Over a 50-ft Obstacle
The takeoff model is extended to estimate the distance required to clear a 50-ft obstacle.

### Landing Ground Roll
Landing ground roll is estimated using the relationship between touchdown kinetic energy and stall speed relative to the baseline aircraft.

### Rate of Climb
Rate of climb is calculated from the difference between available power and power required.

$$ ROC = \frac{P_{available} - P_{required}}{W} $$

### Cruise Speed
Cruise performance is estimated using the aircraft drag model and available propulsive power.

### Aircraft Weight
Aircraft gross weight is estimated as a function of the selected design variables, allowing the effects of wing area, aspect ratio, and engine power to be incorporated into the performance calculations.

---

## Aerodynamic Model
The aerodynamic model uses the fundamental lift and drag relationships:

$$ L = \frac{1}{2}\rho V^2 S C_L $$

$$ D = \frac{1}{2}\rho V^2 S C_D $$

The drag coefficient is modeled as:

$$ C_D = C_{D0} + \frac{C_L^2}{\pi e AR} $$

The model captures the primary relationship between aircraft geometry, lift, drag, and flight performance while remaining suitable for a preliminary design study.

---

## Design Constraints

Configurations are evaluated against the following requirements:

| Requirement | Constraint |
|---|---:|
| Stall Speed | ≤ 45 mph |
| Takeoff Ground Roll | ≤ 250 ft |
| Takeoff Over 50-ft Obstacle | ≤ 600 ft |
| Landing Ground Roll | ≤ 300 ft |
| Rate of Climb | ≥ 1,200 ft/min |
| Cruise Speed | ≥ 110 mph |
| Wing Span | ≤ 38 ft |
| Gross Weight | ≤ 2,400 lb |

All speed calculations within the MATLAB performance models are performed in knots, while the original design requirements are converted to consistent units during constraint evaluation.

---

## Optimization Method
```
Design Variables
↓
Configuration Generation
↓
Performance Calculations
↓
Constraint Evaluation
↓
Feasible Configurations
↓
Weighted Decision Matrix
↓
Optimal Configuration
|
+--------------------+
↓                    ↓
Pareto Analysis      Sensitivity Analysis
```

---

## Repository Structure
```
stol-aircraft-optimization-trade-study/
│
├── README.md
├── main.m
│
├── inputs/
│   ├── designVariables.m
│   ├── aircraftConstants.m
│   └── requirements.m
│
├── models/
│   ├── stallSpeed.m
│   ├── takeoffDistance.m
│   ├── takeoff50ft.m
│   ├── landingDistance.m
│   ├── climbRate.m
│   ├── cruiseSpeed.m
│   └── aircraftWeight.m
│
├── optimization/
│   ├── generateConfigurations.m
│   ├── checkConstraints.m
│   ├── constraintMargins.m
│   └── decisionMatrix.m
│
├── analysis/
│   ├── tradeSpacePlots.m
│   ├── paretoPlot.m
│   └── sensitivityAnalysis.m
│
├── figures/
│   ├── tradeSpace.png
│   ├── paretoFront.png
│   └── sensitivity.png
│
└── report/
    └── STOL_Trade_Study.pdf
```

---

## Results
The optimization identified **14 feasible configurations** satisfying all defined design constraints. The highest-scoring feasible configuration was:

| Parameter | Optimal Configuration |
|---|---:|
| Wing Area | 220 ft² |
| Aspect Ratio | 6.25 |
| Engine Power | 220 hp |
| Flap Configuration | Fowler |
| Gross Weight | 2,347.1 lb |
| Wing Span | 37.08 ft |
| Maximum Lift Coefficient | 2.10 |
| Stall Speed | 38.74 kts |
| Takeoff Ground Roll | 148.68 ft |
| Takeoff Over 50 ft | 425.35 ft |
| Landing Ground Roll | 281.53 ft |
| Rate of Climb | 1,830.8 ft/min |
| Cruise Speed | 99.33 kts |
| Decision Matrix Score | 0.849 |

---

## Pareto Front
The Pareto analysis identified **8 Pareto-optimal configurations**. These configurations primarily consisted of 220 ft² wing-area aircraft using Fowler flaps, with aspect ratios between 6.00 and 6.50 and engine powers between 200 and 220 hp.

---

## Sensitivity Analysis
The sensitivity analysis evaluates the robustness of the optimization result with respect to the weighting factors used in the decision matrix. The baseline optimization assigns a predetermined percentage weight to each performance criterion based on its relative importance to the overall STOL aircraft design objective.

To evaluate the influence of these subjective weighting decisions, the analysis systematically varies the weighting assigned to each criterion while maintaining the remaining criteria within the established weighting framework. The optimal feasible configuration is recalculated at each weighting level, allowing changes in the selected design to be observed.

For each criterion, its weighting is varied from **5% to 45%** in 5% increments. At each weighting level, the decision matrix is recalculated and the highest-scoring feasible configuration is recorded. This process determines whether the selected aircraft configuration remains consistent when the relative importance of individual performance criteria is changed.

The resulting sensitivity analysis provides a measure of confidence in the final design selection. A configuration that remains optimal across a wide range of criterion weights is less dependent on the original weighting assumptions, while significant changes in the selected configuration indicate that the optimization is more sensitive to how the design objectives are prioritized.

| Parameter | Optimal Configuration | Unique Winning Configurations |
|---|---:|---:|
| Takeoff Ground Roll | 5-45% | 2 |
| Takeoff Over 50-ft Obstacle | 5-45% | 2 |
| Landing Ground Roll | 5-45% | 2 |
| Rate of Climb | 5-45% | 3 |
| Cruise Speed | 5-45% | 2 |
| Gross Weight | 5-45% | 3 |
| Wing Span | 5-45% | 2 |

The results indicate that the optimization is relatively robust to changes in the selected criterion weights. Across the tested weighting ranges, only a small number of distinct configurations became the highest-scoring solution. This suggests that the final design is not solely a consequence of the initial weighting assumptions, although criteria such as rate of climb and gross weight exhibit somewhat greater sensitivity than the other objectives.
