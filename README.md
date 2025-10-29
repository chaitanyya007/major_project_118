# major_project_118
# 🧭 Hybrid Quantum Reinforcement Learning for Vehicle Routing Problem (VRP)

### 🧠 Based on the paper: *“Solving Vehicle Routing Problem Using Grover Adaptive Search Algorithm (GAS)”*

---

## 📘 Overview

This project implements and extends quantum approaches to the **Vehicle Routing Problem (VRP)** — one of the most important NP-hard combinatorial optimization problems.  
Our work is inspired by and builds upon the paper *“Solving Vehicle Routing Problem Using Grover Adaptive Search Algorithm (GAS)”*, and introduces a **Hybrid Quantum Reinforcement Learning (QRL)** model as an improved and adaptive alternative.

The project has been fully developed and tested using **Google Colab**, leveraging both **Qiskit** and **PennyLane** frameworks.

---

## 🚛 Problem Definition — Vehicle Routing Problem (VRP)

The **VRP** asks:  
> “Given a set of cities and a fleet of vehicles starting from a central depot, what is the optimal set of routes such that each city is visited exactly once, total distance (or cost) is minimized, and vehicle constraints are respected?”

### Constraints:
- Each city must be visited **exactly once**.  
- Each route must **start and end** at the depot.  
- The **total cost/distance** of all routes should be **minimized**.  
- Vehicle capacity or route constraints (for extended versions) must be satisfied.

---

## ⚛️ Base Paper — Grover Adaptive Search Algorithm (GAS) for VRP

The base paper applied the **Grover Adaptive Search Algorithm**, an extension of **Grover’s quantum search algorithm**, to search for optimal VRP solutions.  
GAS combines the **amplitude amplification** principle of Grover’s algorithm with a **classical adaptive thresholding mechanism**, iteratively refining the search space.

### 🧩 Key concepts from the paper:
1. **Representation:**
   - Each route configuration is encoded as a **quantum state** over a register of qubits.
   - The **oracle** marks states corresponding to valid/low-cost routes.
2. **Grover Diffusion Operator:**
   - Amplifies the amplitudes of marked (good) states.
3. **Adaptive Threshold:**
   - A dynamic classical threshold updates after each iteration, improving convergence toward the global minimum.
4. **Hybrid Nature:**
   - The algorithm alternates between quantum (search/amplification) and classical (evaluation/threshold update) steps.

### 🧠 Limitation:
While effective for small search spaces, GAS struggles to scale as the number of cities grows because:
- The number of possible routes grows factorially.
- The number of qubits required grows rapidly.
- No learning mechanism adapts to patterns or experience.

---

## 🚀 Our Contribution — Hybrid Quantum Reinforcement Learning (QRL) for VRP

To overcome GAS’s limitations, we developed a **Hybrid Quantum Reinforcement Learning model** that combines:
- The **exploration power of quantum circuits**, and
- The **adaptive learning of reinforcement learning agents.**

Our QRL model aims to learn routing patterns through repeated interaction and reward feedback — reducing dependency on brute-force quantum search.

---

## 🧩 Implementation Details

### ⚙️ Frameworks Used
| Component | Framework |
|------------|------------|
| Quantum Simulation | **PennyLane** |
| Classical Reinforcement Learning & Environment | **Python + NumPy + custom logic** |
| Quantum Gate Design & GAS reference | **Qiskit** |
| Training / Visualization | **Google Colab + Matplotlib** |

---

### 🔢 Quantum Setup
- **Number of qubits:** 6  
  (chosen not per city but per encoded state feature to control complexity)
- **Encoding scheme:** Amplitude encoding of route configurations.
- **Quantum layer:** Implemented via PennyLane QNode.
- **Classical layer:** Reward-based learning loop updates parameters of the quantum circuit.

---

### 🧮 Datasets
We tested on multiple scaled datasets:

| Dataset | Cities | Vehicles | Description |
|----------|---------|-----------|--------------|
| Dataset 1 | 10 | 2 | Small-scale VRP for initial training |
| Dataset 2 | 15 | 3 | Mid-scale test with moderate complexity |
| Dataset 3 | 20 | 4 | Larger instance for performance evaluation |

Each dataset defines city coordinates, distance matrices, and vehicle constraints.

---

### 🧠 Hybrid QRL Algorithm Flow

1. **Initialization**
   - Initialize quantum circuit parameters (randomly or pre-trained).
   - Initialize RL environment with cities and vehicles.

2. **Episode Loop**
   - Encode the current route/state into quantum input.
   - Quantum circuit outputs route probabilities.
   - RL agent samples route based on quantum outputs.

3. **Reward Computation**
   - Calculate cost = total route distance.
   - Reward = inverse of cost (lower cost → higher reward).

4. **Parameter Update**
   - Use gradient-based update (via PennyLane’s `qml.grad`) to adjust quantum parameters based on reward feedback.

5. **Termination**
   - Continue training until reward convergence or fixed episode limit.

---

### ⚡ Comparison with GAS

| Aspect | Grover Adaptive Search (Base Paper) | Hybrid Quantum RL (Our Work) |
|--------|--------------------------------------|-------------------------------|
| Type | Quantum Search | Quantum + Classical Learning |
| Adaptivity | Threshold-based | Reward-based learning |
| Scalability | Limited (qubit explosion) | More scalable (fixed 6 qubits) |
| Exploration | Random sampling | Policy-driven exploration |
| Performance | Effective for small VRPs | Consistent learning across instances |

---

## 📊 Results & Observations

- **QRL model** gradually learned efficient routes without brute-force search.
- **Reward curves** showed stable improvement over episodes.
- **Route costs** decreased across training epochs.
- Compared to GAS, QRL showed:
  - Better convergence for mid-sized problems (10–20 cities).
  - Lower computational overhead per iteration.
  - Higher adaptability to different city distributions.

---



