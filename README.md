# 🧬 Bio-Inspired Optimization for Insulin Planning

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.10%2B-3776AB?style=for-the-badge&logo=python&logoColor=white" alt="Python 3.10+"/>
  <img src="https://img.shields.io/badge/Jupyter-Notebook-F37626?style=for-the-badge&logo=jupyter&logoColor=white" alt="Jupyter Notebook"/>
  <img src="https://img.shields.io/badge/DEAP-Evolutionary%20Computation-4CAF50?style=for-the-badge" alt="DEAP"/>
  <img src="https://img.shields.io/badge/SciPy-ODE%20Solver-8CAAE6?style=for-the-badge&logo=scipy&logoColor=white" alt="SciPy"/>
  <img src="https://img.shields.io/badge/License-MIT-yellow?style=for-the-badge" alt="License MIT"/>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Domain-Computational%20Biology-blueviolet?style=flat-square" alt="Domain"/>
  <img src="https://img.shields.io/badge/Optimization-Genetic%20Algorithms-orange?style=flat-square" alt="Genetic Algorithms"/>
  <img src="https://img.shields.io/badge/Model-Bergman%20ODE-blue?style=flat-square" alt="Bergman ODE"/>
  <img src="https://img.shields.io/badge/Status-Research%20Prototype-lightgrey?style=flat-square" alt="Status"/>
</p>

---

> **Applying bio-inspired evolutionary algorithms to optimize insulin intervention plans using progressively richer glucose–insulin simulation models.**

---

## 📌 Overview

This project investigates how **genetic algorithms** and other bio-inspired search techniques can be used to plan optimal insulin dosing strategies for glucose control. It progresses from simple rule-based simulations through Bergman-inspired physiological ODE models, combining them with evolutionary optimization to achieve tight glucose regulation.

The research is implemented in a single, self-contained Jupyter notebook: [`Insulin_Optimization.ipynb`](Insulin_Optimization.ipynb).

---

## 🧪 Simulated Patient Profiles

Three virtual patient avatars are used across experiments to represent diverse physiological profiles:

| Avatar | Profile |
|--------|---------|
| **Emily** | Avatars/Emily.png |
| **Lisa** | Avatars/Lisa.png |
| **Sam** | Avatars/Sam.png |

---

## 🗂️ Notebook Sections

The notebook is structured as a progressive workflow across four main sections:

### 1 · Baseline Simulation Models
- Discrete rule-based glucose update equations (6-hour interval steps)
- Accounts for scheduled meals, insulin injections, and exercise events
- Establishes reference trajectories for comparison

### 2 · Optimization Baselines (Discrete Models)
- **Grid Search**: exhaustive sweep over insulin doses on a simplified discrete model
- **Discrete GA**: genetic algorithm without physiological time-delay or decay, exploring the insulin search space

### 3 · DEAP-Based Evolutionary Optimization
- Full evolutionary pipeline using the [DEAP](https://github.com/DEAP/deap) library
- Penalty-based fitness function penalizing hypo- and hyperglycemia
- Two-point crossover, adaptive mutation, and elitism

### 4 · Hybrid ODE + GA Experiments
- Mini Bergman ODE model integrated via `scipy.integrate.solve_ivp`
- GA runs on top of the ODE simulator with convergence diagnostics and trade-off analysis
- Sensitivity analysis on key physiological parameters

---

## 📊 Results

All models are evaluated on a **standardized, trajectory-level metric set** after resampling to a common 1-minute grid, enabling fair cross-model comparison:

| Metric | Description |
|--------|-------------|
| `MAE to target` | Mean absolute error to target glucose of 100 mg/dL |
| `Time in range` | % of time in the safe range 70–180 mg/dL |
| `Below 70 (min)` | Minutes spent in hypoglycemia |
| `Above 180 (min)` | Minutes spent in hyperglycemia |

### Fair-Comparison Summary (1-min resampled)

| Experiment | MAE to 100 | Time in 70–180 | Below 70 (min) | Above 180 (min) | Interpretation |
|---|---:|---:|---:|---:|---|
| **Hybrid ODE + GA** | **0.46** | **100.00%** | **0** | **0** | ✅ Best overall |
| Improved Mini Bergman | 7.47 | 96.37% | 217 | 1 | Good control, hypo-risk episodes |
| Mini Bergman (interval) | 9.14 | 100.00% | 0 | 0 | Stable, less precise than hybrid |
| Grid Search (discrete) | 25.76 | 100.00% | 0 | 0 | Simple baseline, not competitive |
| GA Discrete | 45.39 | 52.28% | 115 | 0 | Weak physiological plausibility |

> ↓ Lower MAE is better · ↑ Higher time-in-range is better

---

## ⚙️ Technology Stack

<p>
  <img src="https://img.shields.io/badge/NumPy-013243?style=flat-square&logo=numpy&logoColor=white" alt="NumPy"/>
  <img src="https://img.shields.io/badge/Pandas-150458?style=flat-square&logo=pandas&logoColor=white" alt="Pandas"/>
  <img src="https://img.shields.io/badge/Matplotlib-11557C?style=flat-square" alt="Matplotlib"/>
  <img src="https://img.shields.io/badge/SciPy-8CAAE6?style=flat-square&logo=scipy&logoColor=white" alt="SciPy"/>
  <img src="https://img.shields.io/badge/DEAP-4CAF50?style=flat-square" alt="DEAP"/>
</p>

| Package | Purpose |
|---------|---------|
| `numpy` | Numerical simulation and array operations |
| `pandas` | Results aggregation and metrics tables |
| `matplotlib` | Glucose trajectory and convergence plots |
| `scipy` | ODE integration (`solve_ivp`) |
| `deap` | Evolutionary algorithm framework |

All dependencies are installed inline via `%pip install` cells in the notebook — no separate setup step required.

---

## 🚀 Getting Started

**Requirements:** Python 3.10+, Jupyter Notebook or VS Code with notebook support.

```bash
# Clone the repository
git clone https://github.com/AMVamsi/Bio-Inspired-Optimization.git
cd Bio-Inspired-Optimization

# Open the notebook
jupyter notebook Insulin_Optimization.ipynb
```

Run all cells top-to-bottom in a fresh kernel. The final section — **Final Results Summary (Standardized Metrics)** — contains the cross-model comparison tables.

---

## 📁 Repository Structure

```
Bio-Inspired-Optimization/
├── Insulin_Optimization.ipynb   # Main research notebook
├── Avatars/                     # Virtual patient avatar images
│   ├── Emily.png
│   ├── Lisa.png
│   └── Sam.png
├── Presentation.pdf             # Project presentation slides
└── README.md                    # This file
```

---

## ⚠️ Disclaimer

This project is **research software** developed for academic exploration of bio-inspired optimization techniques applied to glucose-insulin dynamics. It does **not** constitute medical advice and is **not** intended for clinical use.

---

## 📄 License

This project is licensed under the [MIT License](LICENSE).

---

<p align="center">Made with ❤️ for computational biology research</p>
