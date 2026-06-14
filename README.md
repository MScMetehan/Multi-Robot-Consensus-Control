<div align="center">
  
# 🤖 Multi-Robot Consensus & Trajectory Tracking
**Robotics and Control II | MSc Control Systems Engineering | University of Padova**

[![MATLAB](https://img.shields.io/badge/MATLAB-R2024a-orange.svg?style=for-the-badge&logo=mathworks)](https://www.mathworks.com/)
[![Simulink](https://img.shields.io/badge/Simulink-Simulation-blue.svg?style=for-the-badge)](https://www.mathworks.com/products/simulink.html)
[![Robotics](https://img.shields.io/badge/Robotics-Autonomous_Systems-success.svg?style=for-the-badge)]()

</div>

---

## 📖 Project Overview
This repository hosts the modeling and control of a multi-agent system comprising **3 Unicycle Mobile Robots**. The mission is to achieve autonomous coordination through a three-phase execution: **Consensus**, **Cartesian Regulation**, and **Trajectory Tracking**.

---

## 🧠 Theoretical Framework & Kinematics

### 1. Unicycle Model
Each agent follows non-holonomic unicycle kinematics:

$$
\begin{bmatrix} \dot{x} \\\\ \dot{y} \\\\ \dot{\theta} \end{bmatrix} = \begin{bmatrix} \cos\theta & 0 \\\\ \sin\theta & 0 \\\\ 0 & 1 \end{bmatrix} \begin{bmatrix} v \\\\ \omega \end{bmatrix}
$$

*Constraints: Wheel radius $\rho_u = 0.01m$, Speed range $r = [-150, 150]$ rad/s.*
### 2. Graph-Based Consensus (Phase I)
Robots agree on a Rendez-vous point $p_{rv}$ using a directed communication graph and a Nearest Neighbor (NN) stochastic matrix $P$:
$$x(k+1) = P \cdot x(k)$$
*Convergence is guaranteed via **Perron-Frobenius Theorem**, ensuring all agents reach the same coordinates within 15 iterations.*

---

## ⚙️ Control Architecture

### Phase II: Cartesian Regulation
To drive the robots to the agreed point regardless of initial orientation, we implemented a sagittal axis error projection:
*   **Error Projection:** $e_p^T = -x \cos\theta - y \sin\theta$
*   **Control Law:** 
    $$v = k_v \cdot e_p^T$$
    $$\omega = k_\omega \cdot (\text{atan2}(y, x) + \pi - \theta)$$
*   **Switching Logic:** System transitions to Phase III when distance $\rho < 0.5m$. A **Boolean Logic block** prevents the system from reverting to regulation once tracking starts.

### Phase III: Trajectory Tracking (Singularity Handling)
Four strategies were evaluated for tracking a circular path ($R=1m, \omega_d=1rad/s$). 

**Key Innovation: Singularity Robustness**
In *Feedback Linearization (XY)*, a singularity occurs at $v=0$ (causing $\omega \to \infty$). We implemented a threshold-based acceleration strategy:

> If $v < v_{th}$, a constant $\omega$ input is provided to accelerate the unicycle, ensuring $v \neq 0$ and maintaining controller stability.

---

## 📊 Performance Comparison
We compared the controllers using **Mean Squared Error (MSE)** and **Mean Input Effort (MIE)**:

| Methodology | MSE (Accuracy) | MIE (Efficiency) | Highlights |
| :--- | :---: | :---: | :--- |
| **Linear State Feedback** | **0.0369** | 2.5208 | Best precision for small errors |
| **Non-Linear Feedback** | 0.0721 | **2.2850** | Most energy efficient |
| **FB Linearization (Point b)**| 0.2011 | 6.6622 | Avoids singularities by design |
| **FB Linearization (XY)**| 0.1452 | 2.2799 | High robustness with threshold logic |

---

## 📁 Repository Structure
* `unicycle.slx` & `unicycle_analysis.slx`: Main Simulink models containing the control logic, switching mechanisms, and unicycle kinematics.
* `script.mlx`: MATLAB Live Script for parameter initialization, graph generation, and performance metrics calculation.
* `RendezVousUnicycleControl.pptx`: Comprehensive presentation detailing the theoretical background, controller design, and simulation results.

---

## 👨‍💻 Contributors
- **Metehan Kurtoğlu** | MSc. Control Systems Engineer
  [LinkedIn](https://www.linkedin.com/in/metehankurtoglu/) | [GitHub](https://github.com/MScMetehan)
- **Leonardo Rossi**
- **Sezer Yakıt**
