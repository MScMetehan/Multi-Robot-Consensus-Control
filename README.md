# Multi-Robot-Consensus-Control
Simulation and control of 3 unicycle mobile robots for consensus agreement and circular trajectory tracking using MATLAB/Simulink.

<div align="center">
  
# 🤖 Multi-Robot Consensus & Trajectory Tracking
**Robotics and Control II Project | MSc Control Systems Engineering | University of Padova**

[![MATLAB](https://img.shields.io/badge/MATLAB-R2024a-orange.svg?style=for-the-badge&logo=mathworks)](https://www.mathworks.com/)
[![Simulink](https://img.shields.io/badge/Simulink-Simulation-blue.svg?style=for-the-badge)](https://www.mathworks.com/products/simulink.html)
[![Robotics](https://img.shields.io/badge/Robotics-Autonomous_Systems-success.svg?style=for-the-badge)]()
[![Control Systems](https://img.shields.io/badge/Control-Non--Linear-purple.svg?style=for-the-badge)]()

</div>

---

## 📖 Overview
This repository contains the simulation, modeling, and control architectures for a multi-agent robotic system (3 Unicycle Mobile Robots). The core objective of this project is to achieve cooperative autonomous behavior by combining **Graph Theory (Consensus)**, **Cartesian Regulation**, and **High-Precision Trajectory Tracking**.

This project serves as a comprehensive demonstration of applying non-linear control theories to solve non-holonomic constraints in mobile robotics.

---

## 🎯 Mission Objectives
The mission is executed in three seamless autonomous phases:
1. **Rendez-vous (Consensus):** The 3 unicycle robots communicate over a directed graph to mathematically agree on a common meeting point without a central command.
2. **Regulation:** The robots navigate to the agreed consensus point, resolving their initial posture differences.
3. **Tracking:** Upon approaching the target, the robots switch to a tracking mode to collectively follow a continuous circular trajectory.

---

## ⚙️ Control Architecture & Methodologies

### 1. Phase I: Graph-Based Consensus
- Utilized an adjacency matrix and directed graph topologies for inter-robot communication.
- Implemented **Perron-Frobenius Theorem** to ensure network convergence.
- Achieved a consensus accuracy threshold of `0.01` within a maximum of `15` iterations.

### 2. Phase II: Cartesian Regulation
- Designed robust Cartesian controllers to drive the unicycles toward the consensus point.
- Established a switching threshold distance (ρ = 0.5m) to smoothly transition from regulation to circular tracking without instability.

### 3. Phase III: Circular Trajectory Tracking
To ensure precise path following, we implemented and compared **four distinct control strategies**:
* **Linear State Feedback:** Linearized the system around the error dynamics for localized tracking.
* **Non-Linear State Feedback:** Utilized adaptive gains (damping and natural frequency) to handle large initial errors.
* **Feedback Linearization (Point b):** Shifted the control reference to a point on the sagittal axis to completely eliminate control singularities.
* **Feedback Linearization (XY):** Direct cartesian tracking featuring a custom velocity-threshold strategy to handle instances where translational velocity is zero (v=0).

---

## 📊 Performance & Results
We evaluated the tracking controllers based on **Mean Squared Error (MSE)** (accuracy) and **Mean Input Effort (MIE)** (energy consumption).

| Control Methodology | MSE (Tracking Error) | MIE (Control Effort) |
| :--- | :---: | :---: |
| **Linear State Feedback** | **0.0369** | 2.5208 |
| **Non-Linear Feedback** | 0.0721 | **2.2850** |
| **Feedback Linearization (b)**| 0.2011 | 6.6622 |
| **Feedback Linearization (x,y)**| 0.1452 | 2.2799 |

> **Conclusion:** *Linear State Feedback* provided the highest tracking precision, whereas *Non-Linear Feedback* offered the most energy-efficient approach.

---

## 📁 Repository Structure
* `unicycle.slx` & `unicycle_analysis.slx`: Main Simulink models containing the control logic, switching mechanisms, and unicycle kinematics.
* `script.mlx`: MATLAB Live Script for parameter initialization, graph generation, and performance metrics calculation.
* `RendezVousUnicycleControl.pptx / .pdf`: Comprehensive presentation detailing the theoretical background, controller design, and simulation results.

---

## 👨‍💻 Contributors
- **Metehan Kurtoğlu** | MSc. Control Systems Engineer
  [LinkedIn](https://www.linkedin.com/in/metehankurtoglu/) | [GitHub](https://github.com/MScMetehan)
- **Leonardo Rossi**
- **Sezer Yakıt**
