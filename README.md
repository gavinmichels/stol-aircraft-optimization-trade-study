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
