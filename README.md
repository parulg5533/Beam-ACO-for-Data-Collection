# Beam-ACO for Mobile Sink Path Planning


**Author:** Parul Garg
**GitHub:** [github.com/parulg5533](https://github.com/parulg5533)  
**Date:** June 2025  

---

## 🚀 Project Overview

In wireless sensor networks, a **mobile sink** must visit distributed sensor nodes to retrieve data while minimizing overall energy consumption, respecting individual node time-windows, and satisfying service-time constraints. This repository implements a **hybrid Beam-Search-guided Ant Colony Optimization (Beam-ACO)** approach to tackle this complex path-planning problem.

### Key Innovations

- **Beam-ACO hybridization**: Combines the global exploration strengths of Ant Colony Optimization (ACO) with the focused candidate filtering of Beam Search
- **Dynamic constraint handling**: Integrates time-window enforcement and local repair heuristics to guarantee feasible routes
- **Convergence control**: Monitors pheromone distribution convergence and triggers resets to avoid premature stagnation

---

## 📚 Table of Contents

1. [Features](#-features)  
2. [Algorithm Details](#-algorithm-details)  
3. [Installation & Setup](#️-installation--setup)  
4. [Usage & Examples](#-usage--examples)  
6. [Notebook Structure](#-notebook-structure)  
7. [Results & Visualization](#-results--visualization)  
8. [Contributing](#-contributing)  
9. [FAQ](#-faq) 
11. [Contact](#-contact)

---

## 🔍 Features

- **Energy Model**: Customizable travel-energy function based on distance, speed, and sink mobility parameters
- **Time-Window Constraints**: Each sensor node enforces an earliest/latest service window; violations trigger repair routines
- **Beam-ACO Core**:
  - **Pheromone Initialization**: Uniform start, adaptive evaporation
  - **Heuristic Information**: Inverse-distance matrix biases exploration
  - **Beam Filtering**: Retains top-k candidate routes per iteration
  - **Convergence Detection**: Monitors pheromone variance; resets when over-converged
- **Local Improvement**: Post-processing repair heuristic to eliminate residual violations
- **Visualization**:
  - 2D map of node locations and final path
  - Energy-vs-iteration convergence curves

---

## 🧮 Algorithm Details

### 1. Initialization
- Load node coordinates $(x_i, y_i)$, time-windows $[a_i, b_i]$, service times $s_i$
- Set number of ants $m$, beam width $k$, pheromone evaporation rate $\rho$, exploration factor $q_0$

### 2. Beam-ACO Main Loop (Max Iterations)
- For each ant in current beam:
  1. Construct partial route starting at depot
  2. At each step, choose next node via a random-proportional rule combining pheromone $\tau_{ij}$ and heuristic $\eta_{ij}$
  3. Prune to top-k full routes by lexicographic ranking on (total energy, total violation)
- Update global pheromones on best-so-far and beam survivors; apply evaporation
- Compute convergence metric $C = \frac{\max(\tau)-\min(\tau)}{\text{mean}(\tau)}$. If $C > C_{\text{threshold}}$, reset pheromones to uniform

### 3. Post-Processing
- Take best-so-far route, apply local swap/move operations to fix any remaining time-window breaches
- Recompute energy cost and report final metrics

---

## ⚙️ Installation & Setup

### 1. Clone Repository
```bash
git clone https://github.com/yourusername/beam-aco-mobile-sink.git
cd beam-aco-mobile-sink
```

### 2. Create Virtual Environment (optional but recommended)
```bash
python3 -m venv venv
source venv/bin/activate   # Linux/macOS
# venv\Scripts\activate    # Windows
```

### 3. Install Dependencies
```bash
pip install -r requirements.txt
# or manually install:
pip install matplotlib numpy jupyter
```

### 4. Launch Notebook
```bash
jupyter notebook beam-aco.ipynb
```

---

## 🎯 Usage & Examples

### Adjust Core Parameters
In the first cell of `beam-aco.ipynb`, you can tweak:

| Variable | Description | Default |
|----------|-------------|---------|
| `num_ants` | Number of ants per iteration | 50 |
| `beam_width` | Beam size (top-k solutions retained) | 10 |
| `rho` | Global pheromone evaporation rate | 0.1 |
| `q0` | Exploration threshold (0…1) | 0.9 |
| `conv_threshold` | Convergence reset threshold | 0.01 |
| `max_iterations` | Maximum ACO loop iterations | 1000 |

### Run & Visualize

1. Run all cells
2. Inspect printed metrics:
   - Best energy cost (Joules)
   - Total number of time-window violations
3. View plots: final path map & convergence curve

---

## 📋 Notebook Structure

1. **Imports & Data Setup**
2. **Energy & Heuristic Matrices**
3. **Violation & Comparison Functions**
4. **Beam-ACO Implementation**
5. **Post-Processing Repairs**
6. **Results Output & Plotting**

---

## 📈 Results & Visualization

### Final Path Plot
- Sensor nodes as blue dots
- Mobile sink route as a red polyline

### Convergence Plot
- Energy cost vs. iteration number
- Markers indicate pheromone-reset events

---

## 🤝 Contributing

Contributions are very welcome! Please:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/my-feature`)
3. Commit your changes (`git commit -m "Add new heuristic"`)
4. Push to branch (`git push origin feature/my-feature`)
5. Open a Pull Request describing your changes

Please ensure code is well-documented and notebook cells are cleared before committing.

---

## ❓ FAQ

**Q: Can I use this on dynamic node sets?**  
A: Yes, modify the data loading cell to ingest your node list and time windows.

**Q: How do I choose beam width?**  
A: Smaller widths focus search but risk missing good solutions; larger widths increase diversity at cost of runtime.

**Q: Is parallelization supported?**  
A: Not currently—future work may integrate multiprocessing for ant construction.

---



## 📬 Contact

For questions or suggestions, open an issue or contact Your Name at parul_2301cs35@iitp.ac.in

Follow me on GitHub: [@parulg5533](https://github.com/parulg5533)
